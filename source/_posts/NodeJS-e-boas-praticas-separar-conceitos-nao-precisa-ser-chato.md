title: NodeJS e boas práticas - separar conceitos não precisa ser chato
tags:
  - javascript
  - nodejs
  - ddd
  - clean architecture
  - repository
categories:
  - Estudos
date: 2017-04-03 08:30:00
---
Softwares tendem a mudar o tempo todo, e uma coisa que pode definir o quão bom é um código é justamente a facilidade que se tem para alterá-lo. Mas o que torna um código fácil de se dar manutenção?

> ...se você tem medo de mudar alguma coisa, ela está claramente mal projetada. - Martin Fowler

<img src="/img/posts/separation.jpg"/>

<!-- more -->

### Separação de conceitos e responsabilidades

Junte as unidades que mudam pelo mesmo motivo, separe as que mudam por motivos diferentes. Seja esta unidade uma função, uma classe ou um módulo, este são [o princípio da responsabilidade única e a separação de conceitos](https://8thlight.com/blog/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html).

Projetar software que se baseia no _Single responsibility principle_ (ou SRP) e na _Separation of concerns_ (ou SoC) de modo que alterá-lo seja _fácil_ começa na arquitetura.

### Arquitetura

Uma _responsabilidade_ em desenvolvimento de software é uma tarefa a qual uma unidade se propõe a realizar: representar o conceito de "produto" na sua aplicação, receber requisições da rede, salvar um usuário no banco de dados, entre outros. Reparou que nestes três exemplos as responsabilidades não parecem nem pertencer a uma mesma categoria? Isso se deve ao fato de elas serem responsabilidades de _camadas_ diferentes, onde cada camada também pode ser dividida em _conceitos_. Seguindo o exemplo, a responsabilidade "salvar um usuário no banco de dados" se encaixa na camada que se comunica com o banco, dentro do conceito de usuário.

De maneira geral, as arquiteturas que aplicam os conceitos acima tendem a separar o código em 4 camadas:

#### Camada de domínio

Nesta camada você definirá as unidades que se relacionam diretamente com o seu domínio, onde representarão entidades do domínio e suas regras de negócio, por exemplo, numa aplicação que contém usuários e times teríamos: a classe `User`, a classe `JoinTeamPolicy` que controla se certo usuário pode fazer parte de um certo time, entre outros. Esta é a camada mais isolada e importante do seu software, e será utilizada pela _camada de aplicação_ para definir os casos de uso.

#### Camada de aplicação

A camada de aplicação realizará a interação entre as unidades da _camada de domínio_ para definir o comportamento da sua aplicação que não pertence diretamente ao seu domínio, incluindo os casos de uso, como uma classe `JoinTeam` que recebe uma instância de `User` e uma de `Team` como parâmetro, e utiliza a classe `JoinTeamPolicy` para checar essa possibilidade.

A camada de aplicação também serve de _adapter_ para a _camada de infraestrutura_. Digamos que em sua aplicação é possível enviar emails. A classe que se comunica diretamente com o servidor de email (chamaremos de `MailChimpService`) pertencerá à _camada de infraestrutura_, já a classe que será usada pela camada de aplicação para enviar emails pertencerá à _camada de aplicação_ e será chamada de `EmailService`, que utilizará o `MailChimpService` internamente. Desta forma toda à sua aplicação, com exceção do `EmailService`, não precisará saber detalhes sobre o serviço de email utilizado, apenas que a classe `EmailService` envia emails.

#### Camada de infraestrutura

É a mais baixa das camadas, que se comunicará diretamente com o que está externo à sua aplicação, como o banco de dados, serviços de email e sistemas de fila.

Uma característica de aplicações multicamada é a utilização do [_repository pattern_](https://martinfowler.com/eaaCatalog/repository.html) para a comunicação com o banco de dados (ou algum outro serviço externo de persistência, como uma API). O _repository_ será um objeto que será tratado mais ou menos como uma coleção, e as camadas que o utilizarão (as de _domínio_ e de _aplicação_) não precisarão saber qual tecnologia de persistência está sendo usado (semelhante ao exemplo sobre serviços de email). A ideia é que a [interface](https://en.wikipedia.org/wiki/Interface_(computing)#Software_interfaces_in_object-oriented_languages) a ser implementada pelo _repository_ pertença à camada de domínio (ou seja, a camada de domínio apenas saberá os métodos que o _repository_ terá e quais parâmetros eles aceitam) e a implementação desta interface esteja na _camada de infraestrutura_, isto torna ambas as camadas mais flexíveis, inclusive na hora de testar. Como em JavaScript não há o conceito de interface, apenas imagina-se uma e cria-se a implementação na _camada de infraestrutura_ normalmente.

#### Camada de interfaces de entrada

Esta camada contém todos os pontos de entrada da sua aplicação, como _controllers_, a CLI, _websockets_, interface gráfica (caso não seja uma aplicação web). Na _camada de interfaces de entrada_ não se deve haver nenhum conhecimento sobre as regras de negócio, casos de uso, tecnologias de persistência, nem nenhuma outra lógica, apenas a passagem dos dados de entrada (como parâmetros de uma URL) para um caso de uso da _camada de aplicação_ e a devolução da resposta da mesma para o usuário.

### NodeJS e separação de conceitos

Ok, mas depois de toda essa teoria, como isso ficaria em uma aplicação Node? A verdade é que alguns padrões usados em arquiteturas multicamadas se encaixam muito bem com padrões usados no mundo JavaScript!

#### NodeJS e a camada de domínio

A camada de domínio no Node pode ser composta por simples [classes ES6](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Classes), mas existem diversas bibliotecas que você pode usar tanto com ES6 quanto ES5 para a criação de entidades de domínio, como: [Structure](http://github.com/talyssonoc/structure/), [Ampersand State](https://github.com/AmpersandJS/ampersand-state), [tcomb](https://www.npmjs.com/package/tcomb) e [ObjectModel](https://github.com/sylvainpolletvillard/ObjectModel).

Veja um exemplo simples utilizando o Structure:

```javascript
const { attributes } = require('structure');

const User = attributes({
  id: Number,
  name: {
    type: String,
    required: true
  },
  age: Number
})(class User {
  isLegal() {
    return this.age >= User.MIN_LEGAL_AGE;
  }
});

User.MIN_LEGAL_AGE = 21;
```

Repare que não incluí nesta lista os models do Backbone, nem bibliotecas como Sequelize e Mongoose, pois essas bibliotecas devem ser usadas na _camada de infraestrutura_ para a comunicação com o exterior, e o resto da aplicação não precisa saber que estão sendo usadas.

####  NodeJS e a camada de aplicação

Os casos de uso pertencem à _camada de aplicação_ e podem ter mais do que apenas "sucesso" e "falha" como resultado (diferentemente das promises). Um padrão utilizado com o Node que funciona bem para casos assim são os [_event emitters_](https://nodejs.org/api/events.html). Você pode fazer com que a classe do seu caso de uso estenda `EventEmitter` e emitir eventos para cada um dos resultados. Desta maneira no seu _controller_ você só precisará executar o caso de uso e adicionar _listeners_ pelos resultados, assim:

```javascript
// CreateUser.js

const EventEmitter = require('events');

class CreateUser extends EventEmitter {
  constructor({ usersRepository }) {
    super();
    this.usersRepository = usersRepository;
  }

  execute(userData) {
    const user = new User(userData);

    this.usersRepository
      .add(user)
      .then((newUser) => {
        this.emit('SUCCESS', newUser);
      })
      .catch((error) => {
        if(error.message === 'ValidationError') {
          return this.emit('VALIDATION_ERROR', error);
        }

        this.emit('ERROR', error);
      });
  }
}
```

O caso de uso realiza a separação dos dois tipos de erro que vem do _repository_, mas quem usa o caso de uso não precisa (nem deve) saber da existência do `usersRepository`.

Desta forma, no seu _controller_ você terá algo assim:

```javascript
// UsersController

const UsersController = {
  create(req, res) {
    // Leia abaixo sobre a parte de infraestrutura e injeção
    // de dependência para entender como esta instância será criada. 
    const createUser = new CreateUser({ usersRepository });

    createUser
      .on('SUCCESS', (user) => {
        res.status(201).json(user);
      })
      .on('VALIDATION_ERROR', (error) => {
        res.status(400).json({
          type: 'ValidationError',
          details: error.details
        });
      })
      .on('ERROR', (error) => {
        res.sendStatus(500);
      });

    createUser.execute(req.body.user);
  }
};
```

#### NodeJS e a camada de infraestrutura

A implementação da _camada de infraestrutura_ costuma não apresentar grandes dificuldades, só deve-se tomar cuidado para não vazar lógica desta camada para as superiores. Você pode, por exemplo, usar models do [Sequelize](https://www.npmjs.com/package/sequelize) para fazer a implementação de um _repository_ que se comunica com um banco SQL, e dar ao _repository_ métodos com nomes que não implicam a existência do SQL internamente, como o método `add` citado acima. Assim, criaremos implementação de um `SequelizeUsersRepository`que será passado para quem depende do _repository_ de usuários apenas como `usersRepository` que obedece a _interface_ imaginária `UsersRepository`, de modo a não se saber da existência do Sequelize nas outras camadas. Segue um exemplo:

```javascript
// SequelizeUsersRepository.js

class SequelizeUsersRepository {
  add(user) {
    const { valid, errors } = user.validate();

    if(!valid) {
      const error = new Error('ValidationError');
      error.details = errors;

      return Promise.reject(error);
    }

    return UserModel
      .create(user.attributes)
      .then((dbUser) => dbUser.dataValues);
  }
}
```

A ideia é a mesma para bancos de dados não relacionais, serviços de email, serviços de fila, APIs externas e afins.

#### NodeJS e a camada de interfaces de entrada

Para esta camada existem várias possibilidades de implementação com Node. Para a entrada de requisições HTTP o [Express](https://npmjs.com/package/express) é o pacote mais usado, mas você pode usar também o [Hapi](https://www.npmjs.com/package/hapi) ou o [Restify](https://www.npmjs.com/package/restify). No fim das contas esta escolha é só um detalhe de implementação, e mudá-la não deve afetar nenhuma das outras camadas (se migrar de Express para Hapi, por exemplo, causou mudanças em outras camadas da sua aplicação, é sinal de que há acoplamento entre elas!).

#### Encaixe entre as camadas

Fazer com que uma camada se comunique diretamente com outra também pode ser ruim e causar acoplamento. Uma solução comum para este problema, não só no Node, é a utilização de _dependency injection_. Esta técnica consiste em fazer que toda dependência de uma classe seja recebida no seu construtor em vez de criada pela própria instância, criando o que se chama de _inversion of control_.

Utilizando esta técnica você consegue isolar bem as dependências de uma classe, tornando a mais flexível e bem mais fácil de ser testada pois _mockar_ as dependências se torna algo trivial.

Para o Node existe um ótimo pacote para _depedency injection_ chamado [Awilix](https://www.npmjs.com/package/awilix), que permite que você utilize a técnica sem acoplar seu código à ferramenta, e não sentir que está usando aquele ~~estranho~~ mecanismo de _dependency injection_ do Angular 1, por exemplo. O autor do Awilix tem uma ótima [série de artigos](https://medium.com/@Jeffijoe/dependency-injection-in-node-js-2016-edition-f2a88efdd427) sobre _dependency injection_ com Node e introdução à como usar o Awilix que vale a pena conferir. Se você está usando o Express, pode ser interessante também usar o [Awilix-Express](https://www.npmjs.com/package/awilix-express).

### Exemplo prático

Mesmo com todos estes exemplos e explicações sobre camadas e conceitos acima, acredito que nada melhor do que um exemplo prático de uma aplicação utilizando uma arquitetura multicamadas para te convencer de que pode ser simples de usá-la. Por isso, criei um [boilerplate para web APIs com Node](https://github.com/talyssonoc/node-api-boilerplate) que aplica arquitetura multicamadas já com o básico necessário configurado, inclusive [todo documentado](https://github.com/talyssonoc/node-api-boilerplate/wiki) (na medida do possível para uma primeira versão) para que você possa praticar e até usar para o _kickstart_ de uma aplicação web com Node, o _boilerplate_ já está pronto pra ser usado em produção!

### Informação adicional

- [FourLayerArchitecture](http://wiki.c2.com/?FourLayerArchitecture)
- [Architecture - The Lost Years](https://www.youtube.com/watch?v=WpkDN78P884)
- [The Clean Architecture](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html)
- [Hexagonal Architecture](http://wiki.c2.com/?HexagonalArchitecture)
- [Domain-driven Design](http://dddcommunity.org/)