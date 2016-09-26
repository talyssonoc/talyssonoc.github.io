title: 'Angular por um desenvolvedor React #2: Fluxo de dados'
tags:
  - angular
  - react
  - flux
categories:
  - Angular por um desenvolvedor React
date: 2015-12-14 08:09:00
---
No post passado da série [Angular por um desenvolvedor React](http://talyssonoc.github.io/categories/Angular-por-um-desenvolvedor-React/) introduzi o conceito de componentes a serem usados no Angular bastante semelhante com os padrões usados em aplicações desenvolvidas com React.

Neste segundo post vou falar um pouco sobre o fluxo de dados, o modo como a mudança do estado da aplicação pode ser propagada para todos os componentes e um pouco da minha opinião sobre o _two-way data binding_ e como ele deve ser usado.

<img src="https://angularjs.org/img/AngularJS-large.png"/>

<!-- more -->

Assim como com o React, eu gosto bastante da [arquitetura Flux](http://facebook.github.io/flux/) e a ideia de ter um fluxo único de dados. Ela é uma arquitetura que pode ser aplicada independente de framework ou linguagem. Cheguei inclusive à fazer alguns experimentos usando [arquitetura flux em um app jQuery](https://github.com/talyssonoc/jquery-flux-todo), e não houve nada que achei ser _impossível_ sem estar usando o React. (Caso veja o código do app com jQuery, pode ser que encontre algumas coisas feias no código, eu não cheguei a me dedicar tanto nele, dado que foi apenas um experimento).

Em meus estudos sobre Angular tendo React em mente, comecei a pensar em modos de criar apps que não fiquem pouco manuteníveis ou difíceis de testar por conta do _two-way data binding_.

Caso você não tenha familiaridade com o termo, _two-day [data binding](https://docs.angularjs.org/guide/databinding)_ é uma funcionalidade de um sistema que permite que duas unidades que compartilhem dados entre si possam modificar uma a outra. Em se tratando de MVC, seria um caso onde modificações na view são refletidas no model, e modificações no model são refletidas na view, algo bem comum em aplicações feitas com Angular.

Mas qual o problema nisso? Em geral, nenhum, mas as pessoas costumam abusar desta funcionalidade sem notar que isto pode ser nocivo. Digamos que você tem um componente __B__ dentro de um componente __A__. Você passa um dado __x__ de A para B, e a view de B possui _two-way data binding_ para modificar x. Isso será refletido em A também, e isso criará um acoplamento entre estes dois componentes. Acho que não preciso me aprofundar muito no caso para que você note o problema em código acoplado, certo?

E como resolver este problema? E, sendo mais específico, como resolver este problema _em um app Angular_? Eu acredito que a solução seja usar algo semelhante à arquitetura flux, utilizando três conceitos: a) estado local intermediário, b) estado compartilhado persistente, e c) comunicação entre componentes.

### Estado local intermediário

O primeiro passo é notar que estado local é algo não totalmente evitável. É bom, e saudável, evitar o máximo de estado local possível. O pessoal que usa o React que está lendo este post vai entender bem ao que me refiro. Enquanto o React tem _built-in_ um sistema para gerenciamento de estado interno de um componente (vide [setState](https://facebook.github.io/react/docs/component-api.html#setstate), o próprio Facebook sugere que você evite ao máximo o uso de armazenamento de estado dentro de um componente e favoreça o uso de [componentes burros](https://preact.gitbooks.io/react-book/content/jsx/dumb.html)).

Porém as vezes é _necessário_ armazenar um estado intermediário localmente. Quer um exemplo? Um componente de _accordion menu_ onde mais de um menu pode estar aberto ao mesmo tempo. Em uma aplicação flux você pode muito bem manter os dados de qual menu está aberto dentro de uma [_store_](https://facebook.github.io/flux/docs/overview.html#stores), mas note que isso não é _dado_ do sistema, não é necessariamente parte do _estado_ do sistema, e pode ser armazenado localmente dentro do componente. Porém, desde que os dados sobre quais menus estão abertos não precisem ser compartilhados com outra parte do sistema, ou não sejam relevantes para o estado geral do sistema. Um outro exemplo, um pouco mais prático: dados de um formulário. Eu acredito que dados que serão enviados para o backend e processados devam ser mantidos locais internamente ao formulário até o momento de envio para o backend, sem armazenar os dados na(s) store(s).

Sinceramente, eu acredito que este tipo de dado deva ser o __único__ usado com _two-way data binding_. Entende o que eu digo? Já que é um dado local, fazer este binding de dados não vai vazar para o resto do sistema. Se, após algumas alterações locais, este dado precisar ser compartilhado com o resto do sistema e/ou persistido, ele será transformado em um estado compartilhado persistente (como é o caso dos formulários citado acima).

### Estado compartilhado persistente

Se você já desenvolveu ou mexeu com uma aplicação flux, saiba que este tipo de estado pode ser entendido como: dados que são salvos em uma store. Dados que fazem parte do _estado do sistema_.

Por exemplo, digamos que você tem um campo onde o usuário pode editar o texto do mesmo à vontade, que nada mais se alterará no sistema, porém quando ele apertar _enter_, o conteúdo do campo deva ser exibido numa mensagem de boas vindas ao usuário no topo da página.

No momento em que este dado é "publicado" para o resto da aplicação, ele deixa de ser um dado local temporário, e passa a ser um dado compartilhado persistente. De maneira análoga, ele deixa de estar dentro do _state_ de um componente do React e passa a ser um dados que vai chegar ao componente em forma de _prop_.

Mas como avisar o resto da aplicação sobre esta mudança? Bom, agora entra a parte mais importante do post: comunicação entre componentes.

### Comunicação entre componentes

A comunicação entre os diferentes componentes da sua aplicação é o que dita o fluxo de dados da mesma. Ter vários _two-way data bindings_ espalhados de maneira desorganizada no seu sistema tornará ele pouco manutenível e será pouco _debugável_. Isso fará com que analizar erros na sua aplicação seja bem mais difícil.

Se você já tem experiência com React e flux, já deve ter pensado: _poxa, isso pode ser resolvido por um dispatcher_. E você está certo! Mas tem um detalhe.

Usar um simples _dispatcher_ ou [_event emitter_](https://nodejs.org/api/events.html) no seu sistema Angular, apesar de funcionar, não é a melhor opção por causa do [`$digest` loop](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$digest) do Angular.

O _digest loop_ é a ordem em que as checagens, alterações, _watches_ e renderizações são feitas _automaticamente_ pelo Angular. É um ciclo que deve ser respeitado para manter o bom funcionamente e, principalmente, __previsibilidade__ da sua aplicação. Se você já mexeu um pouco com Angular já deve ter se deparado com algum erro mais ou menos assim:

> Error: $digest already in progress

Isso significa que o ciclo de `$digest` já estava em progresso e algo tentou iniciá-lo novamente. Acredite, este é um problema bem chato de identificar a causa as vezes, e que pode acabar acontecendo se você usar um _event emitter_ comum na sua aplicação. Mas como usar algo parecido com um _dispatcher_ e que respeite o `$digest`? A resposta é: usar o `$rootScope`!

Toda aplicação Angular tem um escopo que é pai de todos os outros escopos, ele é chamado de [`$rootScope`](https://docs.angularjs.org/api/ng/service/$rootScope). Assim como qualquer outro escopo do Angular, ele possui os métodos `$on` e `$emit`, que é tudo que precisamos para construir um _event emitter_ simples, rápido, e que respeita o `$digest`. Vamos lá? Veja um exemplo usando ES6:

```js
const eventEmitterService = [
  '$rootScope',
  ($rootScope) => {
    return {
      on: (...args) => {
        $rootScope.$on(...args);
      },
      emit: (...args) => {
        $rootScope.$emit(...args);
      }
    }
  }
];

app.factory('eventEmitter', eventEmitterService);
```

Pronto! Simples, não? Pois é, agora você você consegue compartilhar os dados entre seus componentes (e factories, e services e tudo mais) de uma maneira organizada e permitir que outras partes do seu sistema possam esperar pela mudança. Sacou aqui a semelhança com o esquema de usar _actions_ e _stores_ do flux?

Agora, no nosso exemplo ali do campo de texto, você pode ter um componente que tem um estado interno do conteúdo do campo e, quando o usuário pressionar _enter_, você usar o nosso event emitter para emitir o evento `TEXT_CHANGED` (ou algo do tipo) com o novo texto.

E isto não precisa ser aplicado somente a textos. Em experiências recentes minhas com o Angular, eu fiz com que o _controller_ da página de um post de blog ouvisse as modificações nos comentários daquele post. Assim, quando o usuário cria um novo comentário, ele é persistido no servidor e, quando a resposta de confirmação do servidor chega, eu emito um evento `ADD_COMMENT` que é ouvido pelo _controller_ da página e ele atualiza a sessão de comentários sem ter que recarregar a página.

Você pode ver um exemplo de como usar este _approach_ na tag de data-flow do nosso [repositório de apoio](https://github.com/talyssonoc/componentized-angular/tree/data-flow).

Espero que tenham gostado, até a próxima!