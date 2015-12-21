title: 'Angular por um desenvolvedor React #3: Eventos'
tags:
  - angular
  - react
categories:
  - Angular por um desenvolvedor React
date: 2015-12-21 08:00:00
---
O Angular, como diz a [própria documentação](https://docs.angularjs.org/guide/introduction), é um framework para criação de aplicações dinâmicas que aposta em código declarativo, dado que código assim é melhor para a programação de interfaces web.

O problema é que ainda assim as pessoas costumam esquecer a importância de usar _código declarativo_ e o código da sua aplicação acaba perdendo um pouco da sua expressividade. Quer um exemplo? O excessivo uso da função [link](https://docs.angularjs.org/api/ng/service/$compile#-link-) quando cria-se uma diretiva!

Em mais este post da série [Angular por um desenvolvedor React](http://talyssonoc.github.io/categories/Angular-por-um-desenvolvedor-React/) vou discutir um pouco sobre como acho que devam ser usados os eventos dentro do Angular dado meu _background_ com desenvolvimento com o React.

<img src="https://angularjs.org/img/AngularJS-large.png"/>

<!-- more -->

Uma das bases da expressividade de um código escrito usando Angular reside no fato de que você pode programar diretamente no HTML, através de tags e diretivas. Algo que chega até a ser curioso: quando o código coloca HTML no JavaScript, como faz o React, dizem ser loucura e mistura de conceitos; quando coloca-se JavaScript no HTML, como faz o Angular, chamam de "maior expressividade do template", vai entender.

Existem diversas diretivas que existem para permitir que você trabalhe com eventos dentro do seu template. Atente-se ao fato que "evento" neste post diz respeito à eventos do DOM, como _click_, _submit_, entre outros. Estas diretivas cortam a necessidade de cerca de 95% dos casos onde as pessoas costumam usar a função `link`. Então, assim como no primeiro post da série nós paramos de usar o `$scope`, neste post vamos parar de usar mais uma outra coisa:

### Abolir a função `link`

Talvez pareça radical demais, loucura demais. Mas vamos começar com a premissa de __nunca__ usar a função `link`. Eu sei que você vai arrumar um jeito de encontrar casos em que é extremamente necessário. Para estes casos também temos um jeito, mas deixemos eles de lado por enquanto e vamos para os casos mais comuns.

Caso você não saiba, a opção `link` de uma diretiva especifica uma função que te dá acesso ao elemento do DOM em que a diretiva está, comumente usado para adicionar _event listeners_ aos elementos. Notou aí o problema com a expressividade? Se você coloca os seus _listeners_ somente dentro da função `link` seu código perde uma parte da expressividade. Ao olhar o template da sua diretiva, um usuário não saberá os eventos que acontecem por ali.

Portanto vamos lá: abolindo a função `link`!

### Diretivas de fábrica

O Angular já vem _de fábrica_ com várias diretivas para adicionar _event listeners_ ao seus elementos. Eles funcionam bem semelhante aos [eventos suportados pelo React](https://facebook.github.io/react/docs/events.html). Seguindo a documentação do sistema de eventos do React, eu separei aqui uma lista, na mesma ordem, dos eventos providos _de fábrica_ pelo Angular através de diretivas:


#### Clipboard Events

- [ngCopy](https://docs.angularjs.org/api/ng/directive/ngCopy)
- [ngCut](https://docs.angularjs.org/api/ng/directive/ngCut)
- [ngPaste](https://docs.angularjs.org/api/ng/directive/ngPaste)

#### Keyboard Events

- [ngKeydown](https://docs.angularjs.org/api/ng/directive/ngKeydown)
- [ngKeypress](https://docs.angularjs.org/api/ng/directive/ngKeypress)
- [ngKeyup](https://docs.angularjs.org/api/ng/directive/ngKeyup)

#### Focus Events

- [ngFocus](https://docs.angularjs.org/api/ng/directive/ngFocus)
- [ngBlur](https://docs.angularjs.org/api/ng/directive/ngBlur)

#### Form Events

- [ngChange](https://docs.angularjs.org/api/ng/directive/ngChange)
- [ngSubmit](https://docs.angularjs.org/api/ng/directive/ngSubmit)

#### Mouse Events

- [ngClick](https://docs.angularjs.org/api/ng/directive/ngClick)
- [ngDblclick](https://docs.angularjs.org/api/ng/directive/ngDblclick)
- [ngMousedown](https://docs.angularjs.org/api/ng/directive/ngMousedown)
- [ngMouseenter](https://docs.angularjs.org/api/ng/directive/ngMouseenter)
- [ngMouseleave](https://docs.angularjs.org/api/ng/directive/ngMouseleave)
- [ngMousemove](https://docs.angularjs.org/api/ng/directive/ngMousemove)
- [ngMouseover](https://docs.angularjs.org/api/ng/directive/ngMouseover)
- [ngMouseup](https://docs.angularjs.org/api/ng/directive/ngMouseup)

#### Touch Events

Depende de [ngTouch](https://docs.angularjs.org/api/ngTouch).

- [ngClick](https://docs.angularjs.org/api/ngTouch/directive/ngClick)
- [ngSwipeLeft](https://docs.angularjs.org/api/ngTouch/directive/ngSwipeLeft)
- [ngSwipeRight](https://docs.angularjs.org/api/ngTouch/directive/ngSwipeRight)

Notou a quantidade de diretivas para eventos do DOM que você já tem por padrão? Veja abaixo um exemplo de um código usando a função `link`:

```js
// ElementDirective.js
// ...
link: function(scope, element, attrs, controller) {
	$(element)
    .find('.my-button')
    .on('click', function(e) {
    	controller.handleClick(e);
    });
}
```

```html
// element.html
<div>
	<button class="my-button">Click me</button>
</div>
```

E agora um código usando somente diretivas:

```html
<div>
    <button ng-click="ctrl.handleClick($event)">Click me</button>
</div>
```

Notou como o segundo é mais claro para quem lê o código do template? E mais! Possuir código que delega um evento do DOM para um método do _controller_ da sua diretiva diminui a quantidade de código não testado (já que a função `link` raramente é restada), aumentando seu _code coverage_ se o método no seu controller possuir teste para ele.

Caso você esteja acompanhando a série de posts também pelo repositório no Github, veja aqui um exemplo de [código declarativo com evento](https://github.com/talyssonoc/componentized-angular/blob/master/app/client/js/components/name-input/name-input.html#L2).

### Eventos customizados

Ok, ok, sabemos que as vezes você precisará de eventos customizados de algum tipo no seu template. Como lidar com isso?

Primeiramente vamos concordar que esses casos são exceções, então vamos criar uma exceção para algo que já falamos neste post: _abolir o uso do `link`_.

Você deve se lembrar do primeiro post da série sobre Angular por um desenvolvedor React quando falamos sobre [diretivas helpers](http://talyssonoc.github.io/2015/11/30/Angular-por-um-desenvolvedor-React-1-Componentizacao/#componentes-helpers-diretivas), certo? Estas diretivas eram as únicas que possuiam escopo não-isolado.

Se você entendeu que tipo de diretivas essas são, deve ter também relacionado que diretivas como `ng-click`, `ng-submit` e afins se encaixam neste tipo de diretiva.

Então vamos às nossas novas regras neste post:

- O uso da função `link` de uma diretiva deve acontecer somente em diretivas helper;
- Nenhum tipo de lógica deve estar contida dentro do _event listener_, somente delegação de chamada para o controller do componente;
- E, por último: __sempre__ que precisar de um evento custom crie uma diretiva helper o mais genérica possível para este evento e teste-a.

### Conclusão sobre eventos

Este post é bem curto mas a ideia dele é ir direto ao ponto: tenha o código para eventos também declarativo.

Permitir que a pessoa que lê seu código entenda-o mesmo quando vê somente o template significa que seu código está bem mais legível e expressivo, e aproveita uma feature bastante importante do Angular.

Qualquer sugestão, crítica ou algo do gênero, é só clicar ali em baixo!