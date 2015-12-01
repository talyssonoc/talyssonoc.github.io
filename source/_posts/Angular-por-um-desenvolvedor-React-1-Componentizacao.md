title: 'Angular por um desenvolvedor React #1: Componentização'
tags:
  - angular
  - react
categories:
  - Angular por um desenvolvedor React
date: 2015-11-30 08:30:00
---
Quando ouvi falar do Angular pela primeira vez, achei que a ideia era genial! Para uma pessoa que já havia mexido com o Backbone, não precisar se preocupar com o DOM diretamente era um paraíso. Com o tempo, lendo reviews de programadores influentes que usaram, acabei mudando de ideia.

Com o React foi exatamente o contrário. A primeira vista achei estranho, simples demais, e JSX me parecia uma maluquice. Porém com o tempo fui notando o potencial que a biblioteca tinha, principalmente com a capacidade de permitir _serverside rendering_ e virei fã.

Hoje, depois de meses mexendo com o React e sem dar muita importância ao Angular, noto que em parte o Angular é mais _mal entendido_ do que ruim. Não, ainda não gosto do framework, e o fato de não permitir _serverside rendering_ influencia nisso (não, coisas como o [Prerender](https://prerender.io/) ou o [EscapedFragment.io](http://escapedfragment.io/) não me convencem). Mas depois de ler alguns posts que vou citar ao longo deste primeiro post, resolvi tentar novamente fazer algo em Angular, seguindo algumas coisas que aprendi com o React. E neste primeiro post sobre o assunto vou falar sobre componentização!

<img src="https://angularjs.org/img/AngularJS-large.png"/>

<!-- more -->

### Angular não componentizado

Componentes _isolados_ que ~~teoricamente~~ só acessam dados dos seus _props_, do seu _state_ ou do _context_ para mim foi uma das grandes sacadas do React. É incrível o quanto isso pode promover a reaproveitabilidade de um componente. Componentes estes que podem ser testados separadamente sem muito problema.

Já no Angular, por outro lado, há um intenso uso do `$scope`. Apesar de fazer sentido, e parecer super prático jogar uma função ou um dado no `$scope` e ele estar disponível pra você lá, a ideia é estranha, por vários motivos. O Angular alega ser mais testável, o que concordo que pode ser afirmado se você levar em conta que o uso de [_dependency injection_](https://docs.angularjs.org/guide/di) no framework é algo bem útil. Porém, usar o `$scope` já deixa _estranho_ de se testar. Continua fácil? Sim. Mas, por exemplo, em testes de controllers você acaba testando o que está no `$scope`, não no controller. Os `$scope`s não são os controllers, eles também não são os models dentro de um controller (dado que de um escopo mais interno você seria capaz de acessar o de cima). Testar o que está no `$scope` dentro de um teste de controller parece meio estranho, não?

Usar um `ng-controller` também é algo meio estranho, principalmente quando você não usa o `Controller as`. Isso também diminui a reusabilidade, ou pelo menos a manutenibilidade da mesma. Já pensou ter que passar por todo lugar onde um tal controller é usado porque agora ele tem um novo dado dentro dele?

Pois é, é para casos assim que existem as [directives](https://docs.angularjs.org/guide/directive)! Mas espera aí, usar directives para componentizar mas continuar usando `$scope` ainda não ajuda muita coisa, testar ainda vai ter aquele cheiro de "_estou testando o que eu não deveria estar testando aqui_".

Foi depois de ler os artigos [Sane, scalable Angular apps are tricky, but not impossible](https://medium.com/@bluepnume/sane-scalable-angular-apps-are-tricky-but-not-impossible-lessons-learned-from-paypal-checkout-c5320558d4ef) e [ Refactoring Angular Apps to Component Style](http://teropa.info/blog/2015/10/18/refactoring-angular-apps-to-components.html), e começar a associar algumas ideias que vieram do React aplicadas ao Angular que notei que era sim possível usar a ideia de componentes isolados com o Angular!

### Definindo tipos de componentes

Quando comecei a pensar mais sobre o assunto, principalmente o ponto de _fazer tudo ser uma diretiva_ do artigo do pessoal do PayPal, notei que haveriam diferentes _tipos_ de componentes. O modo como um componente equivalente à uma página inteira seria programado era diferente de como um componente bem mais reutilizável (um componente de upload, por exemplo) seria programado.

E mais, deicidi que eu usaria somente diretivas do tipo `E` ou `A`. Nada de `EA`, nem `C`, nem nenhuma outra mistura. Usar o tipo de `restrict` dos componentes consistentemente é algo que também ajuda a entender para que cada componente serve de maneira semântica.

### Componentes de página

Como dito no artigo do PayPal, até páginas inteiras seriam melhor usadas se também fossem transformadas em diretivas, o que ajuda inclusive na hora de criar as _routes_ do seu app.

Então deicidi que eu usaria diretivas com `restrict: 'E'` com escopo isolado, com controllers que seriam usados somente por elas, inclusive usando `controllerAs` igual a `'ctrl'` para todas as páginas. Usar sempre `'ctrl'` facilita para que você não precise ficar voltando no arquivo da diretiva para saber que nome foi usado para o controller, e se o controller precisar mudar de nome você não precisará mudar o código do template da diretiva também.

Desta forma, toda dependência que deva ser injetada em um componente será injetada no controller da mesma, nunca diretamente na diretiva.

Se estivéssemos usando ES2016/ES7 para definir um componente de página, seria da seguinte forma:

```js
// MyPage.js
class MyPage {
	constructor() {
    	this.restrict = 'E';
        this.scope = {};
        this.controller = 'MyController';
        this.controllerAs = 'ctrl';
        this.template = '<div>Hello, {{ ctrl.name | uppercase }}</div>';
    }
}
app.directive('myPage', (...args) => new MyPage(...args));

// MyController.js
class MyController {
	static $inject = ['getName'];

	constructor(getName) {
    	this.name = getName();
    }
}
app.controller('MyController', MyController);

// routes.js
// ...
$routeProvider.when('/my-page', {
   	template: '<my-page></my-page>'
});
// ...
```

### Componentes burros

Se você já tem algum conhecimento de React, já sabe o que é um componente burro. Os componentes burros só acessam dados vindo "de cima" e não fazem data-fetching de nenhuma maneira. Eles existem para serem renderizados apenas com dados que vem das `props`, sem saber a origem dos mesmos.

Pois é, isto também pode ser reproduzido com Angular. A lógica é bem parecida com os componentes de página, com algumas pequenas diferenças:

- Eles recebem atributos quando usados, desta forma iremos usar o `bindToController` para receber estes atributos, já que eles também terão escopo isolado, nada de usar `$scope`;
- Componentes burros podem (não quer dizer que devam) fazer _transclusion_.

Simples, não? Pois é, porém por muito tempo a comunidade Angular não usou este tipo de _mindset_ para desenvolver diretivas. Este estilo de usar componentes, que nasceu com o React, se provou tão eficiente quanto a reusabilidade e testabilidade, que o Angular 1.5 vai até ter um método `.component()` que funciona como um wrapper para o `.directive()` com alguns valores já pré-definidos. Você pode ler mais sobre isso no artigo [Exploring the Angular 1.5 .component() method](http://toddmotto.com/exploring-the-angular-1-5-component-method/) do Todd Motto.

Se você ainda não sabe, o `bindToController` de uma diretiva permite que dados que você passar para a diretiva através de atributos serão salvos como propriedades do controller da mesma. E as diretivas com _transclusion_ permitem que você passe elementos filhos de uma diretiva (se você já usou o React, a ideia é semelhante ao `this.props.children`).

Veja abaixo como ficaria uma diretiva de um componente burro:

```js
// Greet.js
class Greet {
	constructor() {
    	this.restrict = 'E';
        this.scope = {};
        
        this.controller = 'GreetController';
        this.controllerAs = 'ctrl';
        
        this.bindToController = {
        	name: '='
        };
        
        this.template = `
        	<div>
            	Hello, <b>{{ ctrl.upperName() }}</b>
            </div>`;
    }
}
app.directive('greet', (...args) => new Greet(...args));

// GreetController.js
class GreetController {
	upperName() {
    	return this.name.toUpperCase();
    }
}
app.controller('GreetController', GreetController);
```

Agora, com este componente, até podemos reescrever o template da nossa _page_ do item anterior pra algo assim:

```js
	this.template = '<div><greet name="name"></greet></div>';
```

Este é um exemplo besta, que não demonstra bem o poder do uso de componentes burros, mas com um pouco de prática nisso você notará a liberdade que este _approach_ te dá.

Além do mais, notou que agora, sem usar `$scope`, testar o controller destas nossas diretivas testa __realmente__ o controller, e não o `$scope` que ele tem acesso?

### Componentes helpers/diretivas

Estes componentes são bem diferentes dos citados anteriormente. Estes terão acesso ao `$scope` (apesar de que vão usá-los somente para escrita, __nunca__ para leitura internamente). Além do fato que em alguns apps a existência deste tipo de componente pode não se fazer necessária.

Uma outra forma de ver estes componentes é tê-los como _mixins_. Eles são usados para isolar-se lógicas que são usadas em mais de um componente. De maneira geral, vou chamá-los apenas de diretivas. Confuso? Você já vai entender.

Vamos dizer que você está escrevendo um blog, e quer que em várias páginas você acessará informações do blog em si (como o nome do blog, todos os autores e afins). Não fica meio repetitivo escrever o _fetch_ destes dados toda vez no controller da diretiva da sua página? Ok, podemos isolar esta lógica numa factory/provider/service. Mas, ainda assim, não fica repetitivo injetar a mesma factory/provider/service no controller da página? Minha solução pra isso foi criar as diretivas.

Estes componentes, diferentemente dos anteriores, são do tipo `A`. O que significa que você os usará como atributos. E mais, eles não terão um escopo isolado.

Cada diretiva adicionará ao escopo de onde foi adicionado somente __uma__ variável, com o seu nome, numa espécie de namespace. Dentro desta variável ele deixará acessível _funções_ e atributos para serem usados dentro do escopo em que a diretiva foi inserida. Estas funções devem ser [funções puras](https://en.wikipedia.org/wiki/Pure_function), de modo que os componentes não criem dependência com a lógica usada dentro da diretiva. Caso for alguma dependência de lógica (por exemplo, um cálculo que vai ser usado em vários lugares do sistema), aí sim isso deve ser isolado em uma factory/provider/service.

Ainda confuso? Vamos a um exemplo:

```js
// Blog.js
class Blog {
	constructor() {
    	this.restrict = 'A';
        
        this.controller = 'BlogController';
        this.controllerAs = 'blog'; // note que aqui não é 'ctrl'
    }
}
app.directive('blog', (...args) => new Blog(...args));

// BlogController.js
class BlogController {
	static $inject = ['$scope'];
    
    constructor($scope) {
    	this.data = $scope.blog = {};
        
        this.data.name = 'My blog';
        this.data.authors = ['Talysson'];
        
        this.data.getName = () => { // atenção ao uso de arrow-function por causa do `this`
        	return this.data.name;
        };
    }
}
app.controllers('BlogController', BlogController);
```

Deu pra sacar? Veja que agora podemos reescrever o `template` do nosso componente `Greet` da seguinte maneira:

```js
this.template = `
	<div data-blog>
    	Hello, <b>{{ ctrl.name }}</b>, welcome to {{ blog.getName() }}
    </div>`;
```

Uma função exportada por uma diretiva __nunca__ deve modificar seus parâmetros, caso houver algum.

Bom, como um desenvolvedor React, minha primeira impressão de um modo bom para se usar o Angular foi pensar no modo de componentização. Espero que tenham gostado deste primeiro post sobre o assunto!

O código para este primeiro post se encontra no repositório [talyssonoc/componentized-angular](https://github.com/talyssonoc/componentized-angular/tree/componentization). Você notará que ele está um pouco mais lapidado e ainda não está usando o router (ele foi citado no post para mostrar o motivo de porque uma página também deve ser escrita com uma diretiva), resta a você dar uma explorada no repositório! (Repare que o link é para o primeiro release, que corresponde à este primeiro post).

Sinta-se livre para comentar sobre algo que deixei passar, principalmente se você tem mais experiência com Angular e sabe que algo do que foi descrito acima tem potencial para dar problemas futuros, ou até mesmo sobre algum _typo_ que cometi ao longo do post.

Até a próxima!