title: 'JavaScript sem padrões: não é bem assim'
tags:
  - javascript
  - nodejs
categories:
  - Discussões
  - Indicando
date: 2016-03-28 08:44:00
---
Antes de explicar do que se trata este post, me sinto na necessidade de falar do que _não se trata_ este post. Este não é um post sobre usar ponto-e-vírgula ou não (para este assunto você pode ver [aqui](https://brendaneich.com/2012/04/the-infernal-semicolon/), [aqui](https://github.com/twbs/bootstrap/issues/3057), [aqui](https://github.com/feross/standard/issues/78), [aqui](https://twitter.com/brendaneich/status/626224324731518976), [aqui](https://github.com/airbnb/javascript), [aqui](http://javascript.crockford.com/code.html), [aqui](https://contribute.jquery.org/style-guide/js/), [aqui](https://google.github.io/styleguide/javascriptguide.xml) ou aq... chega, né?). Este post também não é sobre qual framework MVC/MVP/MVVC/Flux/CQRS você deve usar (mas espere para ver uma pincelada não-polêmica sobre  assunto no final do post).

Mas espera, se não é sobre isso, sobre o que é este post?

Bom, a ideia do post começou na minha cabeça quando surgiram os posts "The sad state of &lt;alguma coisa relacionada com JavaScript&gt;" e "&lt;Alguma coisa relacionada com JavaScript&gt; fatigue". E teve seu ápice quando li o post [State of the Art in JavaScript in 2016](https://medium.com/javascript-and-opinions/state-of-the-art-javascript-in-2016-ab67fc68eb0b) e com o caso [npm](http://blog.npmjs.org/post/141577284765/kik-left-pad-and-npm) vs [Azer](https://medium.com/@azerbike/i-ve-just-liberated-my-modules-9045c06be67c#.332jufimr) vs [kik](https://medium.com/@mproberts/a-discussion-about-the-breaking-of-the-internet-3d4d2a83aa4d). Mais especificamente com a discussão em volta do que a remoção do módulo [left-pad](https://www.npmjs.com/package/left-pad).

Com todo o alarde gerado sobre o JavaScript não ter esta função no _core_, ou não ter uma biblioteca oficial que contenha este tipo de função, com a impressão das pessoas de que o JavaScript não tem bibliotecas básicas padrão (mesmo as que não fazem sentido serem parte do _core_, mas que sejam a primeira opção na hora de resolver um dado problema) senti a necessidade de escrever um post que mostrasse que a comunidade JavaScript tem sim bibliotecas padrão assim. E é sobre isto que este post vai falar. Você pode enxergar este post como uma espécie de [awesome](/2015/02/06/Se-aprofundando-em-uma-linguagem/#programming-is-awesome), porém mais descritivo e com foco apenas nas ferramentas mais usadas de cada categoria.

<!-- more -->

### Funções básicas

Dado que um dos estopins para este post foi a confusão por causa do `left-pad`, acho válido que esta seja a primeira categoria. Nesta categoria há duas opções:

- [lodash](https://www.npmjs.com/package/lodash): Se você não tem preferência por um estilo de programação (você entederá o porque de eu dizer isto no bullet abaixo), simplesmente opte pelo `lodash`. Ele terá a maioria das funções que você precisa, e se você ainda está confuso sobre usar `lodash` ou `underscore`, leia [esta issue](https://github.com/jashkenas/underscore/issues/2182).
- [Ramda](https://www.npmjs.com/package/ramda): Mas se você quer algo mais funcional, vá de Ramda. Me desculpe pessoal do [lodash/fp](https://github.com/lodash/lodash/wiki/FP-Guide), mas o Ramda sai na frente. Se quiser saber o porque, leia a sessão "What's different?" do [site do Ramda](http://ramdajs.com/0.20.0/index.html).

### Servidor e autenticação

Esta é uma das poucas categorias dentro do universo JavaScript que não há _tantas_ opções (perceba que aqui não incluo frameworks para aplicações, mas sim algo mais _baixo nível_).

- [Express](https://www.npmjs.com/package/express): O Express é, de longe, o microframework para criação de servidores mais usado da comunidade do Node. Mesmo com toda a [confusão recente envolvendo o Douglas Wilson](http://thefullstack.xyz/history-express-javascript-framework/), esta ainda é a melhor opção. A comunidade que produz bibliotecas que funcionam com Express é bem maior que a do Hapi e do Restify, e se você precisar de algo _ainda mais baixo nível_, opte pelo [Connect](https://www.npmjs.com/package/connect).
- [Passport](https://www.npmjs.com/package/passport): Se você precisa adicionar autenticação à sua aplicação Node, Passport é a melhor opção. Com dezenas das chamadas ["estratégias" de autenticação](http://passportjs.org/), incluindo autenticação com [Facebook](https://github.com/jaredhanson/passport-facebook), [Twitter](https://github.com/jaredhanson/passport-twitter), [OAuth](https://github.com/jaredhanson/passport-oauth), [JWT](https://github.com/themikenicholson/passport-jwt) e vários outros, o Passport é a opção mais completa.

### Promises e programação assíncrona

Programação assíncrona é um dos grandes fortes do JavaScript, seja usando [Promises](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) ou não. Porém, como o gerenciamento manual de código assíncrono é difícil e o surgimento de Promises na especificação linguagem é recente, ainda é necessário usar bibliotecas que facilitam o uso de código assíncrono, veja as melhores opções a se usar para este tipo de problema:

- [async](https://www.npmjs.com/package/async): Se você vai trabalhar com código assíncrono sem usar promises, nem perca tempo procurando outras opções, escolha o `async`. Esta foi uma das primeiras bibliotecas grandes à resolver o problema com código assíncronos e atualmente já tem mais de 800 mil downloads diários (números tirados do próprio NPM).
- [Bluebird](https://www.npmjs.com/package/bluebird): É a biblioteca de promises mais performática atualmente, sendo até [100 vezes mais rápida](https://github.com/petkaantonov/bluebird/issues/381) que sua concorrente [Q](https://www.npmjs.com/package/q), que também não é uma má opção se você vai usar promises no _browser_. Para o caso geral ou quando estiver em dúvida, opte pelo `Bluebird`.

### CLI

Com o surgimento de frameworks e aplicações não-web construídas com Node, criar uma CLI se tornou um fator bem importante, com dezenas e dezenas de opções à se escolher, seguem as principais:

- [Inquirer](https://www.npmjs.com/package/inquirer): Se você precisa fazer uma CLI bastante interativa, com perguntas, checkboxes, listas e tudo mais, sua melhor opção será usar o Inquirer. Esta é, inclusive, a biblioteca usada que adiciona toda aquela interação ao [yo](https://www.npmjs.com/package/yo).
- [minimist][https://www.npmjs.com/package/minimist]: Mas se você que algo mais baixo nível, apenas para _parse_ dos argumentos passados por linha de comando, escolha o `minimist`. Se você esteve na comunidade Node desde o início você deve se lembrar do [optimist](https://www.npmjs.com/package/optimist), que foi descontinuado em favor do [yargs](https://www.npmjs.com/package/yargs). Sendo assim, usar o `minimist` ou o `yargs` torna-se apenas questão de preferência pela API. Na dúvida prefira o `minimist` por ser mais usado, com cerca de 700 mil downloads diários.

### Logging e debug

Debugar aplicações Node de maneira prática nunca foi uma tarefa muito fácil, mas já há opções muito boas. Quanto à _logging_, este "setor" da comunidade JavaScript foi, por muito tempo, dominado pelo [Winston](https://www.npmjs.com/package/winston), que hoje em dia está longe de ser a opção devido a altíssima quantidade de _bugs_ presentes no mesmo. Saiba então o que usar:

- [debug](https://www.npmjs.com/package/debug): Apesar do nome, o `debug` é uma biblioteca de _logging_ bem minimalista que pode ser configurada facilmente e ativada/desativada com o uso de variáveis de ambiente. Precisou de uma biblioteca de _logging_ básica: use o `debug`.
- [morgan](https://www.npmjs.com/package/morgan): O `morgan` é um _logger_ de requisições HTTP extretamente útil, e que tem em seu núcleo o próprio `debug`, citado acima.
- [node-inspector](https://www.npmjs.com/package/node-inspector): O Node Inspector é hoje a mais usada estratégia de _debug_ usada em aplicações Node, com uma configuração um pouco mais complicada que a sua concorrente mas que vale a pena de se usar. Uma alternativa ao Node Inspector seria o [ironNode](https://www.npmjs.com/package/iron-node), que apesar de ainda ser pouco usado vem crescendo bastante dentro da comunidade. Na dúvida, opte pelo `Node Inspector`.

### Envio de emails

- [nodemailer](https://www.npmjs.com/package/nodemailer): Aqui nào há dúvidas: precisou enviar emails em uma aplicação Node, use o `Nodemailer`. Com [plugins](https://github.com/nodemailer/nodemailer#send-using-a-transport-plugin) para os serviços de email mais populares do mercado o `Nodemailer` é a opção mais completa para este tipo de tarefa.

### Banco de dados

Nesta categoria vou apresentar duas opções para casos bem distintos mas que são, claramente, as melhores opções para cada um dos dois casos:

- [sequelize](https://www.npmjs.com/package/sequelize): Se sua aplicação precisa se conectar com um banco de dados SQL (Postgres, MySQL, MariaDB, SQLite ou Microsoft SQL Server), opte pelo `Sequelize`. Dentre todas as opções de ORMs para Node (e há muitas), o `Sequelize` se sobresai por ter uma das [melhores documentações](http://docs.sequelizejs.com/en/latest/), além de uma [CLI](https://github.com/sequelize/cli) bastante completa, com suporte à [_migrations_](https://github.com/sequelize/cli#migration) e _generators_.
- [mongoose](https://www.npmjs.com/package/mongoose): Este é um outro caso onde não há discussão: se sua aplicação vai se conectar a MongoDB, simplesmente use o Mongoose. É a opção mais usada e com a comunidade mais ativa para usar MongoDB com Node.

### Testes e cobertura

Esta é uma daquelas partes meio polêmicas, onde é necessário tomar cuidado para não ser opinado demais, vamos lá:

- [mocha](https://www.npmjs.com/package/mocha): O `Mocha` é o framework de testes mais usado na comunidade do JavaScript. Você não deve usar somente ele para seus testes (veja os próximos bullets), mas e não sabe bem por onde começar com testes em JavaScript, esta será sua melhor opção, principalmente levando-se em conta a comundiade deste módulo.
- [chai](https://www.npmjs.com/package/chai): O `Chai` é uma biblioteca de asserção que pode ser usada perfeitamente em conjunto com o `Mocha`. Com a opção de usar o estilo TDD ou BDD de escrita de testes.
- [sinon](https://www.npmjs.com/package/sinon): Já o `Sinon` é uma biblioteca que facilita o uso de [_spys_ e _stubs_](http://www.giulianovarriale.com/conhecendo-sinon-js-spy-e-stub/) em testes JavaScript. Você pode estar pensando que usar o Jasmine é uma melhor opção do que usar o combo Mocha + Chai + Sinon, mas posso afirmar que, após um certo tempo trabalhando com o Jasmine você começa a tropeçar em problemas que simplesmente não existiriam se você usasse estas três bibliotecas.
- [enzyme](https://www.npmjs.com/package/enzyme): Se a sua aplicação é feita com React e você pretende (e eu espero que pretenda) testar seus componentes, simplesmente use o Enzyme. Com uma API __extremamente__ mais simples que a do [React Test Utilities](https://facebook.github.io/react/docs/test-utils.html), o `Enzyme` do pessoal do AirbBnB será sua melhor opção. Quer um motivo? Eu aposto que você prefere procurar um elemento renderizado com a classe `my-class` usando `component.find('.my-class')` (com o Enzyme) do que com `ReactTestUtils.findRenderedDOMComponentWithClass('my-class')` (com o React Test Utilities), não é mesmo?
- [supertest](https://www.npmjs.com/package/supertest): Precisa fazer testes com requisições HTTP? Use o `supertest`. Ele usa internamente o `superagent` e permite criar testes com HTTP com uma sintaxe simples e idiomática.
- [factory-girl](https://www.npmjs.com/package/factory-girl): Se você veio da comunidade Ruby, uma coisa que você pode ter sentido falta na hora de escrever testes que usam o banco de dados é uma boa biblioteca de _factory_. Com o `factory-girl` este problema acaba. Com uma API bastante prática e [vários adapters](https://www.npmjs.com/browse/keyword/factory-girl) para ORMS, o `factory-girl` é a melhor opção caso você precise testar usando o banco de dados.
- [istanbul](https://www.npmjs.com/package/istanbul): O Istanbul é o módulo mais usado e completo de geração de _code coverage_ para Node. Se precisar gerar _coverage_ do seu código, não tenha dúvida, use o Istanbul.

Você pode estar se perguntando "Mas e o [tape](https://www.npmjs.com/package/tape)? E o [AVA](https://www.npmjs.com/package/ava)?". Bom, eu não me esqueci deles, mas dado que eles possuem problemas para rodar testes no navegador, por exemplo (que facilitaria o _debug_ em casos de erro) preferi não adicionar eles à lista.

### Sockets

Sockets são também um dos grandes pontos fortes do Node na hora de desenvolver uma aplicação _web_. Mas qual biblioteca escolher?

- [primus](https://www.npmjs.com/package/primus): Para começar com o pé direito quando for trabalhar com sockets no Node, use o Primus. Ele é uma abstração que te permite usar diversas bibliotecas de socket de maneira genérica. Daí em diante vira só uma questão de foco da sua aplicação para escolher qual biblioteca usar.
- [socket.io](https://www.npmjs.com/package/socket.io): Usando como _adapter_ do Primus ou não, o `Socket.IO` é a biblioteca de socket mais usada pela comunidade do Node. Na dúvida, escolha o `Socket.IO`, dada a quantidade de _features_ e aplicações grandes que o usa.
- [sockjs](https://www.npmjs.com/package/sockjs): Mas se você quer uma biblioteca com menos features mas mais performática, você pode optar por usar o `SockJS`, que não tem, por exemplo, suporte à salas mas aguenta mais requisições simultâneas sem ferir a performance do seu servidor.

### Data

Trabalhar com datas em JavaScript é uma outra tarefa que, por muito tempo, foi uma tarefa chata, mas há um certo tempo que temos um vencedor na hora de resolver este problema:

- [moment](https://www.npmjs.com/package/moment): Se você precisa trabalhar com dadas, efetuar operações com elas e tudo mais, não pense duas vezes e use o `Moment`.
- [moment-timezone](https://www.npmjs.com/package/moment-timezone): Se, além de trabalhar com datas você precisa trabalhar com _timezones_, você pode usar este plugin para o `Moment` chamado `Moment Timezone`, e seus problemas estarão resolvidos.

### Imutabilidade e programação reativa

O título desta seção é composto por dois termos que estão _bastante_ em foco na comunidade JavaScript atual. Mais quais bibliotecas usar?

- [immutable](https://www.npmjs.com/package/immutable): Se sua aplicação precisará usar dados imutáveis, escolha o `ImmutableJS`. Produzido pelo pessoal do Facebook, o `ImmutableJS` possui uma [ótima documentação](https://facebook.github.io/immutable-js/docs/), super completa, além da própria biblioteca ser completíssima.
- [rxjs](https://www.npmjs.com/package/rxjs): Vindo da família de [Reactive Extensions](http://reactivex.io/), que possui implementações para várias linguagens, o RxJS é hoje a biblioteca para programação reativa mais em foco na comunidade JavaScript, principalmente por ser usado internamente em um framework front-end que não vou me atrever a citar _ainda_.

### Lint

Após ano tendo esta parte do "mercado" JavaScript dominado pelo JSLint e o JSHint, a comunidade JavaScript finalmente ganhou uma nova opção, renovada e que não sofre dos bugs que seus antecessores sofriam:

- [eslint](https://www.npmjs.com/package/eslint): O `ESLint` é a melhor opção atualmente para _linting_ de código JavaScript, inclusive com suporte completo à ES2015/ES6, além de plugins para suportar regras específicas do JSX.

### Bundling e compilação

Esta é uma outra parte polêmica dentro da comunidade JavaScript, principalmente quando o assunto é _bundling_. Perceba agora que é tudo uma questão de necessidade:

- [babel](https://www.npmjs.com/package/babel): Nesta parte não há muito dúvida. Precisou compilar código ES6+ para JavaScript que os browsers atuais entendem, escolha o Babel. Outras opções como o [traceur](https://www.npmjs.com/package/traceur), do Google, não tem uma comunidade nem minimamente tão ativa quanto a do Babel.
- [browserify](https://www.npmjs.com/package/browserify) / [webpack](https://www.npmjs.com/package/webpack): E aqui começa a polêmica. E agora, `browserify` ou `webpack`? É apenas uma questão de necessidade, e eu falo sério. Você precisa apenas traduzir CommonJS de modo que o navegador entenda, sem `require`s dinâmicos, só com JavaScript (usando, ou não, o Babel) de uma maneira prática e rápida de __configurar__? Não pense muito, escolha o `browserify`. Quer algo mais elaborado, que compile também para outros padrões de módulos (como AMD, por exemplo), quer compilar CSS também, com uma flexibilidae maior, _code splitting_ e tudo mais, ao custo de ter bem mais trabalho configurando? Use o `webpack`. É só isso.

### A polêmica chega ao seu ápice

Eu disse, no começo do post, que eu passaria rapidamente e sem muita polêmica, pelo assunto _frameworks_.

Eu não vou te falar aqui que React é melhor do que Angular ou Ember (apesar de, pessoalmente, eu preferir o React), ou que o CycleJS é melhor porque é mais funcional e reativo, mas vou citar aqui coisas que, ao meu ver, dominaram esta fatia do mercado JavaScript:

- DOM Virtual: independentemente se é usando [React](https://www.npmjs.com/package/react), o [Ember](https://www.npmjs.com/package/ember) que possui o Glimmer, o [virtual-dom](https://www.npmjs.com/package/virtual-dom) ou o [CycleJS](https://www.npmjs.com/package/@cycle/core), que usa o `virtual-dom` internamente, a tendência do uso de DOM virtual para minimizar as alterações no DOM "de verdade" do navegador é notável. Eu diria que, independente do que você vá escolher como framework, prefira um que use DOM Virtual. (Nota: estou sendo bem pessoal aqui)
- Eventos: A "era" de comunicação direta entre componentes UI, que acarretava em partes da tela não serem atualizadas, acabou. Com o surgimento de arquiteturas como o [Flux](https://facebook.github.io/flux/) e o crescimento da proramação funcional reativa (ou FRP), adotado pelo CycleJS por exemplo, que permite a noticação de toda a UI sobre modificações e atualizações da tela, este tipo de problema já está basicamente resolvido, tornando-se apenas uma questão de opinião e gosto pela API na hora de escolher qual framework usar.

Eu sei que o post ficou longo, mas espero ter conseguido alcançar o objetivo de mostrar que o JavaScript tem bibliotecas padrão e reconhecidas, basta você saber pra onde olhar.