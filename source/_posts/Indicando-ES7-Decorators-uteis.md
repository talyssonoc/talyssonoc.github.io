title: 'Indicando: ES7 Decorators úteis'
tags:
  - angular
  - design patterns
  - javascript
  - react
categories:
  - Indicando
date: 2015-11-16 08:38:00
---
Você sabe o que é um _decorator_? De maneira resumida, decorator é um [_design pattern_](/2015/10/28/Porque-padroes-sao-importantes/#design-patterns) que permite que você adicione funcionalidades a um objeto! A Wikipedia tem um [artigo sobre o _decorator pattern_](https://en.wikipedia.org/wiki/Decorator_pattern) que pode te ajudar a entender o que é o padrão.

E você sabia que o ES7/ES2016 possui decorators em sua especificação? Pois é, já é possível usar decorators no JavaScript a partir de _transpilers_ como o [Babel](http://babeljs.io/), que podem ser usados, por exemplo, para tornar classes _singletons_, ou adicionar _debounce_ à métodos.

> Mas espera, eu li na descrição dos decorators que eles adicionam funcionalidades à um objeto individual sem alterar os outros da mesma classe, qual é que é essa aí de tornar uma classe um singleton? Isso não faz sentido!

Caso você tenha tido a reação acima, talvez você tenha se esquecido (ou não saiba) que classes/funções em JavaScript são instâncias de `Function` ;)

Este post não visa _ensinar_ o que são decorators, nem como usá-los no JavaScript, o [post do Addy Osmani sobre ES2016 decorators](https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841) pode fazer isso muito melhor do que eu! O que vim fazer aqui é simplesmente te indicar bons pacotes de decorators para usar com JavaScript/NodeJS.

<!-- more -->

### [core-decorators](https://www.npmjs.com/package/core-decorators)

Este pacote possui vários decorators inspirados em decorators e [_annotations_](https://en.wikipedia.org/wiki/Annotation) que já vem built-in em algumas linguagens, como `@deprecate`, `@autobind`, `@debounce`, entre outros.

### [lodash-decorators](https://www.npmjs.com/package/lodash-decorators)

E aí, o que acha de ter diversas funções do [lodash](https://www.npmjs.com/package/lodash) em forma de decorators? Bom, né? É justamente isso que este pacote vai te permitir.

### [express-decorators](https://www.npmjs.com/package/express-decorators)

Se o seu app é feito usando o [express](https://www.npmjs.com/package/express), ter decorators que te permitem _linkar_ classes ES6 à funcionalidades do mesmo (transformar uma classe em um controller, um método em um handler de rota, ou em um middleware, por exemplo), o pacotre express-decorator pode te ajudar bastante.

### [hapi-decorators](https://www.npmjs.com/package/hapi-decorators)

Mas se o seu negócio é usar o [hapi](https://www.npmjs.com/package/hapi) ao invés do express, o hapi-decorator é uma escolha para você, ele é baseado nos decorators para express. :)

### [koa-router-decorators](https://www.npmjs.com/package/koa-router-decorators)

E se seu app é feito usando o [koa](https://www.npmjs.com/package/koa) e tem o roteamento feito com o [koa-router](https://github.com/alexmingoia/koa-router), também existe uma opção como as anteriores para você.

### [async-decorators](https://www.npmjs.com/package/async-decorators)

Já está usando [async/await](https://github.com/tc39/ecmascript-asyncawait) em seus códigos? O async-decorators possui alguns decorators que podem te ajudar, como o o `@memoize` e o `@serialize`.

### [react-mixin](https://www.npmjs.com/package/react-mixin)

Se você usava React antes usando o [`React.createClass`
](https://facebook.github.io/react/docs/top-level-api.html#react.createclass) e agora usa classes do ES6 já deve saber que usar _mixins_ como usava antes não é possível com as classes, certo? Com o react-mixin você vai ser capaz de usar mixins no React normalmente, mesmo com classes, usando [decorators](https://www.npmjs.com/package/react-mixin#but-it-s-at-the-end-of-the-file) tanto para métodos quanto para classes.

### [angular-decorators](https://www.npmjs.com/package/angular-decorators)

E por último, se o seu app é feito com Angular também existem decorators que melhoram a sintaxe que você vai usar na hora de criar `modules`, `providers`, `services`, entre outras _ngCoisas_.

Bom, estas foram minhas dicas de decorators, espero que sejam úteis para vocês. E se você sabe mais algum decorator (ou coleções deles) para serem adicionadas nesta lista, pode comentar ali em baixo!
