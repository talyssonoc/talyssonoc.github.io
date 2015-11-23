title: 'JavaScript: adicione açúcar a gosto e pare de reclamar'
tags:
  - coffeescript
  - javascript
  - syntax sugar
  - typescript
categories:
  - Discussões
date: 2015-11-23 08:30:00
---
Reclamar do JavaScript é um dos atuais _hypes_ na programação, alguns reclamando das novas features que estão surgindo, outros reclamando que deveria estar indo ainda mais rápido, outros ainda reclamando que a linguagem é simplesmente ruim e ponto. Sinceramente, acho que a única resposta que serve para todos esses tipos de reclamação é: adicione açúcar a gosto e pare de reclamar.

Antes que comece com "_ah, mas não dá pra fazer X com JavaScript, minha linguagem tem X no core_" eu espero que você leia o post até o fim.

<img src="/img/posts/keep-calm-and-add-sugar.png"/>

<!-- more -->

A primeira coisa que você deve considerar quando for reclamar que JavaScript não faz algo é: a não ser que os desenvolvedores dos browsers mais usados implementem hoje a tal _feature_ que você quer, e todos os usuários atualizem seus navegadores assim que o _update_ sair, a linguagem passar a ter a tal _feature_ na especificação não vai fazer que todos que acessem seu site tenham acesso à ela. Compreendeu agora?

Diferentemente da _sua linguagem que tem X no core_, JavaScript roda no navegador do cliente (NodeJS não se encaixa nesta parte da discussão, mas ao longo do post ele voltará a equação). Então, ao invés de ficar reclamando que JavaScript não faz algo, simplesmente _adicione açúcar_ e faça-o fazer.

E mais, se você usa o argumento de o fato de o JavaScript "monopolizar" o front-end ser uma coisa ruim, pense um pouco: se só com JavaScript e CSS já existe essa fragmentação imensa de hoje em dia, já imaginou se existisse ainda mais linguagens com diferentes especificações? É, pois é, então vamos lá.

### Syntatic sugar

Se você ainda não sabe, adicionar [syntatic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar) à uma linguagem/código significa implementar algo nesta linguagem para deixar ela mais simples de compreender por humanos, enquanto o funcionamento "por baixo dos panos" continua utilizando somente o que a linguagem oferece inicialmente.

O uso de _syntatic sugar_ é de grande importância no JavaScript, principalmente quando se trata de uma _feature_ que pode ser adicionada usando-se um [polyfill](https://en.wikipedia.org/wiki/Polyfill), pois isso faz com que JavaScript tenha uma quantidade _ainda_ maior de possibilidades a oferecer ao programador. Mas se é algo que _parece_ não ser ser possível usando _polyfill_, não se precipite, você pode se surpreender!

### Mas eu quero fazer X!

Ok, vamos lá, você quer que JavaScript consiga fazer algo. Porque não parar de reclamar e adicionar esta _feature_ de alguma maneira? As pessoas reclamavam que era difícil manipular o DOM com a API original, e daí nasceram bibliotecas como o MooTools e o jQuery, nem tudo tem que vir built-in na linguagem.

Reclamar que algo não vem no _core_ da linguagem está longe de ser um motivo para você dizer que JavaScript é uma linguagem ruim. Se você já ouviu falar de [LISP](https://en.wikipedia.org/wiki/Lisp_%28programming_language%29) alguma vez na sua vida vai saber muito bem do que eu estou falando.

O _core_ do LISP não possui tantas capacidades assim, a quantidade de palavras reservadas da linguagem é bastante limitada, mas ainda assim as pessoas consideram o LISP como a maior das linguagens de programação. Porque? Entre outros motivos, pela capacidade de a linguagem poder ser incrementada através de [macros](http://c2.com/cgi/wiki?LispMacro). Os macros do LISP permitem adicionar _syntax sugar_ à linguagem de uma maneira impressionante. O que nos leva ao próximo ponto.

### Mas a sintaxe não permite!

Dizer que a sintaxe de uma linguagem de JavaScript não é amigável ou não te permite fazer _também_ não é um desculpa.

Você já ouviu falar das linguagens que compilam para JavaScript? Pois é, existem várias, pra todo tipo de gosto, cada um com seu _syntax sugar_ diferente.

Prefere algo mais tradicional, que continue usando a sintaxe do JavaScript mas adicione novas features? O [Babel](http://babeljs.io/) ou o [sweet.js](http://sweetjs.org/) devem ser o suficientes pra você (E mais: se você optou pelo Babel, saiba que tudo que ele adiciona tem a pretensão de estar no core do JavaScript alguma hora, já que ele trabalha com _stages_, inclusive para ser usado nativamente dentro de um app NodeJS, que vai rodar dentro do seu servidor e não vai depender do navegador do cliente). Não gosta de ter que usar um _transpiler_ de código? Dê uma olhada no [ease.js](https://www.gnu.org/software/easejs/), então.

Você é do tipo de pessoa que prefere uma sintaxe diferente, com blocos baseados em indentação? Talvez [CoffeeScript](http://coffeescript.org/) seja o seu negócio. E se você gosta da sintaxe do Coffee mas ainda assim acha que falta algo para melhorar sua vida quando está trabalhando com código assíncrono, dê uma olhada no [IcedCoffeeScript](http://maxtaco.github.io/coffee-script/).

Prefere linguagens tipadas? Acha que elas são mais seguras e te ajudam a desenvolver melhor? Sem problemas, talvez antes de reclamar por este motivo você deva dar uma chance ao [TypeScript](http://www.typescriptlang.org/), da Microsoft, ao [Dart](https://www.dartlang.org/), do Google, ou ao [Flow](http://flowtype.org/), do Facebook. Empresas grandes adicionando seus próprios açúcares ao JavaScript, qual sua desculpa? :)

É um fã de programação funcional? Acha que JavaScript "puro" não é funcional o bastante (e não é mesmo)? Olha, acho que você ainda não deve conhecer o [Elm](http://elm-lang.org/) nem o [LiveScript](http://livescript.net/) para estar reclamando assim. Se você se sente confortável programando em Haskell, a curva de aprendizagem destas linguagems vai ser bem suave para você.

### Mas não dá pra fazer polyfill de X!

Bom, agora espera lá. Não dá pra fazer polyfill do que você quer fazer, ou não dá pra fazer isso de maneira que você conhece?

Vou te dar um exemplo de algo que o JavaScript não suporta, e te mostrar um exemplo de _syntax sugar_ que torna possível, o que acha? Que tal implementar algo como o `method_missing` do Ruby em uma linguagem que compila para JavaScript? Bom, [clique aqui](http://goo.gl/Q82mfO) e veja com seus próprios olhos :)

Entendeu agora o que eu quero dizer? Falar que JavaScript não é capaz de algo só mostra que você está se limitando ao que te parece confortável, porque muito possívelmente o que você quer é possível de ser implementado sim.

Quer usar o sistema de classes, módulos e tipos do Ruby no front-end? Dê uma olhada no [Opal](http://opalrb.org/). Já existem até _adapters_ de bibliotecas bem conhecidas do JavaScript para ele, como o [jQuery](https://github.com/opal/opal-jquery) e o [React](https://github.com/zetachang/react.rb). Além de frameworks produzidos especialmente para a linguagem, como o [Inesita](https://github.com/inesita-rb/inesita) e o [Volt](https://github.com/voltrb/volt).

É mais fã do Python? Que tal experimentar o [Brython](http://brython.info/), o [Skulpt](http://www.skulpt.org/) ou o [PyPy.js](https://github.com/pypyjs/pypyjs) antes de falar algo? Já existe até um pessoal fazendo a [comparação da velocidade do CPython às do Brython, do Skulpt e do PyPy.js](https://brythonista.wordpress.com/2015/03/28/comparing-the-speed-of-cpython-brython-skulpt-and-pypy-js/).

Prefere Clojure e linguagens LISP-like? O [ClojureScript](https://github.com/clojure/clojurescript) tem uma comunidade maior e mais forte do que você pode imaginar, o [Om](https://github.com/omcljs/om) que o diga! O Om é um adapter do React para ClojureScript, que é usado, por exemplo, para fazer o front-end do [CircleCI](https://circleci.com). Não acredita? [Veja com seus próprios olhos](https://github.com/circleci/frontend).

Gosta mesmo é de Scala? Talvez te supreenda então a existência do [Scala.js](http://www.scala-js.org/), que inclusive também tem adapters para bibliotecas como o [React](https://github.com/japgolly/scalajs-react) e o [Angular](https://github.com/greencatsoft/scalajs-angular).

Bom, eu não vou ficar aqui citanto todas as possiblidades que possam te levar a reclamar que _a sua linguagem faz isso mas JavaScript não_. O Jeremy Ashkenas, criador do CoffeeScript, já fez uma [lista de linguagens que compilam para JavaScript](https://github.com/jashkenas/coffeescript/wiki/list-of-languages-that-compile-to-js) para que você dê uma olhada antes de reclamar. Que tal?

E, me desculpe, mas se você vai usar agora a desculpa de que o código gerado por esses compiladores não é performático, vou precisar te lembrar que existem por aí linguagens que alegam que a _programmer experience_ é mais importante que a performance, além de citar o Kyle Simpson, aka [@getify](https://twitter.com/getify), autor da série [You don't know JS](https://github.com/getify/You-Dont-Know-JS/blob/master/README.md#you-dont-know-js-book-series) com a seguinte frase:

> Transpiled code isn't _great_ code, but it's probably better than the code you've been writing for the last 20 years.

### Mas...

Ok, talvez você só reclame porque é o que você gosta de fazer, nesse caso eu não tenho muito a dizer além de: __keep calm and stop complaining__.

Mas se você entendeu o que eu quis dizer, notou que as capacidades do JavaScript estão limitadas apenas pela quantidade de açúcar que você adiciona na linguagem: __parabéns__. Você sacou que o JavaScript é _praticamente_ o [assembly](http://c2.com/cgi/wiki?AssemblyLanguage) do desenvolvimento web, uma grande quantidade de pessoas não entende, mas criam alternativas _mais alto nível_ que permitem gerar assembly no final.

Se você ainda tem algumas reclamações quanto a coisas como o `this` do JavaScript, ou como funciona a _prototype chain_ da linguagem, temos duas alternativas aqui:

1) Aprenda a linguagem direito antes de sair reclamando por aí;
2) Simplesmente não use essas coisas que você não entende.

Existe uma vertente de programadores JavaScript que simplesmente não usam mais o `this`, por exemplo, e isso não faz deles maus programadores.

E, por fim, se gostou dessa ideia de adicionar açúcar mas ainda não achou algum JavaScript-like que te satisfaça, o que pode ser dito a você é: _stop complaining and bring your own JavaScript_.

Fonte das imagens:

- [Keep calm and add sugar](http://www.keepcalm-o-matic.co.uk/p/keep-calm-and-add-sugar/)