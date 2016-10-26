title: 'JavaScript: as partes desconhecidas'
author: Talysson
tags:
  - javascript
categories:
  - Estudos
date: 2016-10-26 08:10:00
---
Caso esteja se perguntando: não, este não é um daqueles posts sobre "esquisitices" do JavaScript (bom, talvez algumas, mas não de uma forma negativa).

O que quero mostrar neste post são _features_ pouco conhecidas do JavaScript, até mesmo entre desenvolvedores experientes. Topa o desafio de ter seu conhecimento desafiado? Vamos lá :)

<img src="/img/posts/js-lock.png"/>

<!-- more -->

### Aridade de funções

Dentro da matemática, aridade é a quantidade de operandos que uma função/operação recebe. No mundo da programação o termo não muda muito de significado: a aridade de uma função/método é a quantidade de parâmetros obrigatórios da mesma. Por exemplo:

```js
function superUsefulFunction(x, y) {
  console.log('Look:', x, y);
}

function evenMoreUsefulFunction(x, y = 1) {
  console.log('Ok, now it is serious', x, y);
}
```

A aridade da nossa função `superUsefulFunction` é 2, já a aridade da função `evenMoreUsefulFunction` é 1, pois o parâmetro `y` é opcional. Pegou o conceito?

Bom, se você já sabia o que era aridade, até esse ponto nada de novo foi aprendido. Mas você sabe como se descobre a aridade de uma função em JavaScript? Espero que não esteja achando que é com alguma maluquice de usar `.toString()` na função e contar a quantidade de parâmetros usando uma regex.

Pois então, em JavaScript as funções possuem uma propriedade `.length` ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/length)) que nos diz a aridade da função. Então, podemos fazer o seguinte:

```js
console.log(superUsefulFunction.length); // 2
console.log(evenMoreUsefulFunction.length); // 1
```

É assim que, por exemplo, o Express sabe se a função que passamos para tratar uma rota é um _handler_ (aridade 2, `(req, res)`), um _middleware_ (aridade 3, `(req, res, next)`) ou um _error handler_ (aridade 4, `(err, req, res, next)`).

Uma nota importante: o `.length` só diz a quantidade de parâmetros obrigatórios __antes__ do primeiro parâmetro opcional. Por exemplo:

```js
function someFunction(x, y = 1, z) {
  // I do nothing :)
}
```

Portanto, nossa função `someFunction` tem `.length` igual a __1__, e não 2.

### O que _bound functions_ e lambdas tem em comum?

Ao ver o título desta parte, aposto que você deve ter dito "ah, é a dinamicidade do `this`!". Pois errou :)

Antes de me aprofundar mais no assunto, vou explicar o que é uma _bound function_, caso não saiba. Uma _bound function_ é uma função que foi retornada do método `.bind` de uma outra função. Por exemplo:

```js
function normalFunction() {
  console.log('Hello', this.name);
}

const boundFunction = normalFunction.bind({ name: 'JS' });
```

No código acima, a função `boundFunction` é, adivinhe... sim, uma _bound function_. Bom, ok, agora você já foi apresentado às _bound functions_.

Já os lambdas são as funções do ES6/ES2015 também conhecidas como _arrow-functions_:

```js
const lambda = (x) => {
  console.log(x);
};
```

Mas o que elas tem em comum entre si, já que não é a não-dinamicidade do `this`? Acontece que a não-dinamicidade do `this` dentro de lambdas e _bound functions_ não funcionam da mesma forma, mas tem um efeito direto igual: __elas não tem prototype__.

Caso você não saiba, "classes" em JavaScript são nada mais que _syntax sugar_ para funções construtoras. Antes do surgimento do ES2015, era assim que criávamos "classes" em JavaScript:

```js
function MyClass() {
  this.instanceVariable = 2;
}

MyClass.prototype.instanceMethod = function() {
  console.log(this.instanceVariable);
};

var obj = new MyClass();
obj.instanceMethod(); // 2
```

Para adicionarmos métodos de instância às nossas classes criávamos funções no `prototype` das funções.

Agora voltando ao fato de elas não possuirem prototype, veja só:

```js
function MyClass {}
const BoundClass = MyClass.bind(null);
const lambda = () => { console.log('Something'); }

console.log(MyClass.prototype); // MyClass {}
console.log(BoundClass.prototype); // undefined
console.log(lambda.prototype); // undefined

new BoundClass(); // retorna uma instância de MyClass, e não de BoundClass
new lambda(); // lança uma exceção pois lambda não é uma função construtora
```

Sabia dessa?

### O valor numérico de objetos

Presumo que você já saiba como funciona e para que serve o método `.toString()` de um objeto em JavaScript certo? O nome é bem explicativo, e é comum em outras linguagens, ele retorna a representação textual de um objeto para casos em que, por exemplo, o objeto é concatenado com uma _string_:

```js
const obj = {
  toString() { return 'World'; }
};

console.log('Hello, ' + obj); // 'Hello, World'
```

Até aí nada de novo sob o sol. Mas você sabia que também é possível expressar o valor _numérico_ de um objeto caso ele seja usado, por exemplo, numa soma?

Pois é, isso pode ser feito implementando-se o método `.valueOf()` de um objeto:

```js
const obj = {
  valueOf() { return 22; }
};

console.log(obj + 20); // 42
```

Isso pode ser bastante útil caso você esteja implementando _wrapper classes_ para números, como criar uma classe `Integer` ou `Float`, que o JavaScript não possui (lembrando que todo número, inteiro ou não, é da classe `Number` no JavaScript).

### NaN, o diferentão

O `NaN` (`Not a Number`, [MDN](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/NaN)) é sempre alvo de piadas por parte de pessoas de fora da comunidade JavaScript (e até mesmo das de dentro da comunidade, porque não?). E vamos citar as duas causas dessa zueira toda neste item.

A primeira delas, que é o primeiro fato desconhecido do JavaScript desta seção, é que: __o `NaN` é o único valor em JavaScript que é diferente de si mesmo__ (ok, agora você sacou a piada no título desta seção :P). E sim, você entendeu certo, é isso que acontece:

```js
console.log(NaN === NaN); // false
```

Isso costuma ser tão confuso para quem não está acostumado com o fato, que existe até uma função `Number.isNaN()` para que você possa checar se um valor é `NaN`, já que fazer `NaN === NaN` não funciona. E sabe como essa função é implementada? Segue um polyfill da mesma:

```
Number.isNaN = function(value) {
  return value !== value;
};
```

Sim, simples assim.

Agora vai o segundo fato notável desta seção (que _quase_ podemos dizer que é uma esquisitice do JavaScript antes de saber o motivo): o valor `NaN`, _que significa `Not a Number`_, __é um number__. Ou seja:

```js
console.log(typeof NaN); // 'number'
```

WHAT?! É, é isso mesmo que você acabou de ler, e isso __tem explicação__.

Isso acontece porque números em JavaScript implementam a especificação [IEEE 754](https://en.wikipedia.org/wiki/IEEE_floating_point), onde o `NaN` é usado para representar uma _indeterminação_ matemática. Portanto o resultado de operações como `Infinity / Infinity` (ou até alguma mais maluca, como `'abc' / 2`) retornam `NaN`. O retorno de uma operação numérica deve sempre retornar _um valor numérico_, e por isso o `NaN` é considerado um número que simboliza que o valor não é um número válido. O que também explica o porque de `NaN !== NaN`, você não diria que `Infinity / Infinity` e `'thing' / 3` são valores iguais, diria?

### O operador vírgula

Em linguagens de programação em geral a vírgula `,` é usada como um separador, certo? Bom, pois saiba que em JavaScript a vírgula _também_ é um operador, e muito útil!

O operador vírgula permite que você especifique uma sequência de valores que serão interpretados e somente o último deles será o valor da expressão. Confuso? Vamos lá:

```js
var x = 2;
var obj = {
  addX() {
    x++;
    return 'something';
  }
};

console.log((obj.addX(), obj.addX(), x)); // 4
```

O par adicional de parênteses ali é intencional, ele transforma as vírgula num _operador_. Todas as expressões serão processadas, e só o valor da última será retornado da expressão `(obj.addX(), obj.addX(), x)`, no caso o do próprio `x`.

Parece maluquice? Pois saiba que isso é bastante útil para debug, e mais: é uma técnica bastante usada em minificação de código, verifique aí o código minificado da sua aplicação que eu garanto que você achará o operador vírgula sendo usado :)

### Criando links a partir de uma string

Me diga aí, em aplicações feitas com jQuery (ou JavaScript puro), quantas vezes você acabou fazendo algo assim:

```js
const link = '<a href="' + url + '">' + text + '</a>';
```

Algo bastante comum, não? Mas você sabia que a classe `String` do JavaScript possui um método para te ajudar com isso? É o método `.link()` ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/link)). Com ele, para criar o link do exemplo acima, bastava fazer:

```js
const link = text.link(url);
```

Sem concatenação manual, e bem mais simples de ler e dar manutenção!

Infelizmente o método não possui opções para adicionar propriedades à string da tag gerada, mas já quebra um galho.

### Debugando de forma fácil

Se você tem contato com o mundo Ruby, deve conhecer o famoso `binding.pry`, bastante útil na hora de debugar aplicações Rails, por exemplo. Uma coisa bastante comum é ver o pessoal reclamar a falta de algo como o `binding.pry` para JavaScript, e tenho algo a dizer: isso é falta de conhecimento da linguagem.

Todos os browsers mais famosos já implementam uma _keyword_ que permite pausar a execução de um código e permitir que você investigue o lugar onde a execução parou. Esta _keyword_ se chama `debugger`.

Quer ver como funciona? Crie um arquivo HTML com o código abaixo, abra o seu navegador com o console JavaScript aberto, e abra o arquivo:

```html
<body>
  <script>
    var x = 3;
    debugger;
    console.log(x);
  </script>
</body>
```

Você verá que a execução vai parar onde você colocar o `debugger;` e permitir que você tenha total controle para debugar (ainda mais poderoso que o `binding.pry`, eu diria).

E mais! O `debugger` também funciona para debugar aplicações Node, você pode ver o link sobre ele na [própria documentação do Node](https://nodejs.org/api/debugger.html).

Essas são algumas dicas de "segredos" do JavaScript, espero que tenham gostado e aprendido coisas novas neste post!