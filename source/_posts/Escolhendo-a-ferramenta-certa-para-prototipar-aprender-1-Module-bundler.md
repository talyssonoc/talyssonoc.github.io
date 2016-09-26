title: 'Escolhendo a ferramenta certa para prototipar/aprender #1: Module bundler'
date: 2016-08-18 08:15:54
tags:
  - browserify
  - webpack
  - babel
  - react
categories:
  - Escolhendo a ferramenta certa
---
Se tem uma coisa que aumenta a barreira de entrada para o mundo JavaScript é a escolha e configuração das ferramentas que serão usadas. Este caso se agrava ainda mais quando se está começando a aprender uma nova biblioteca e você ainda não sabe como configurar a ferramenta, ou quando só está querendo prototipar algo rápido e perda de tempo é inaceitável. O caso retratado pelo tweet abaixo te soa familiar?

<blockquote class="twitter-tweet" data-lang="pt"><p lang="en" dir="ltr">Marc was almost ready to implement his &quot;hello world&quot; React app <a href="https://t.co/ptdg4yteF1">pic.twitter.com/ptdg4yteF1</a></p>&mdash; Thomas Fuchs (@thomasfuchs) <a href="https://twitter.com/thomasfuchs/status/708675139253174273">12 de março de 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Pensando nisso, resolvi fazer uma série de posts sobre como escolher a ferramenta certa na hora de prototipar uma aplicação ou quando se está estudando algo novo, ferramentas de fácil (ou nenhuma) configuração, começando por um dos tipos mais imprescindíveis quando se trata de front-end: os [_module bundlers_](/2015/12/08/Porque-tooling-e-importante/#transpilers-preprocessors-e-bundlers)!

<!-- more -->

### O hype: Webpack

Quando se trata de _module bundlers_, hoje em dia o hype é usar Webpack. Em posts sobre [tooling](/2015/12/08/Porque-tooling-e-importante/) pela internet a fora, o Webpack (e, algumas vezes, o Rollup) é o aclamado. Porém, raramente estes posts citam a dificuldade de se escrever um arquivo de configuração do Webpack. Vamos concordar, você pode muito bem começar com um arquivo vindo de um boilerplate e usá-lo por um tempo, mas não seria interessante já começar conhecendo as ferramentas que você está usando? Ou, melhor ainda, começar usando uma ferramenta que dispensa configurações?

Imagine você, recém entusiasta de React. Vai precisar configurar o Babel para compilar seu JSX (que, possivelmente no começo você ainda nem sabe do que se tratam estes dois!), vai precisar configurar o loader do Babel para o Webpack para que seu navegador consiga entender módulos do Node. Sem contar que, se quiser aprender a escrever testes, vai ter que se preocupar também com como fazer seus testes rodarem compilados pelo Webpack. E a lista de pré-requisitos para começar a escrever seu _Hello world_ com React só aumenta. A história se repete com TypeScript, CoffeeScript, entre outros. Em não muito tempo, antes que você se torne um desenvolvedor React (que, até pouco tempo atrás, nem sabia do que exatamente se tratava o Webpack), você poderá adicionar o seguinte item no seu curriculum:

<blockquote class="twitter-tweet" data-lang="pt"><p lang="en" dir="ltr">Senior Webpack configuration manager</p>&mdash; Kimmo Puputti (@kpuputti) <a href="https://twitter.com/kpuputti/status/730766290755944448">12 de maio de 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Veja bem, de forma alguma estou falando _mal_ do Webpack. Ele é uma ferramenta poderosíssima, que ainda pretendo falar sobre em posts futuros desta série. O Webpack está num estágio tão avançado atualmente que você consegue usá-lo como um _asset pipeline_ completo, usando-o para compilar e minificar JavaScript, processar CSS/SASS/PostCSS/Stylus/Less, compactar e gerar sprites de imagens, carregar fontes, entre várias outras funcionalidades. Você consegue transformar realmente o Webpack no núcleo do provimento de assets da sua aplicação. Mas ter todas estas funcionalidades enquanto você só quer aprender ou prototipar algo parece meio exagero, não acha?

### A solução prática: Browserify

Lembra-se de quando o Browserify era o _new kid on the block_ do JavaScript? Quando tudo se baseava em usar CommonJS nos módulos, instalar o [Browserify](http://npmjs.com/package/browserify), e rodá-lo para gerar o bundle dos seus módulos? Bons tempos, não? :) Bom, saiba que estes _bons tempos_ não acabaram! O Browserify ainda é uma ferramenta ótima (e prática) para _bundling_ de JavaScript, bastante mantida pela comunidade, e com vários plugins/transforms disponíveis por aí!

Você lembra da dificuldade que teve na última vez que precisou configurar o Webpack para compilar o JavaScript da sua aplicação? Vamos tentar fazer o mesmo com Browserify, agora mesmo:

Crie uma pasta `test_browserify` no seu computador, e rode o comando `npm init` dentro dela, para que o npm gere um novo `package.json`. Você pode simplesmente apertar _enter_ para aceitar todas as opções com o valor padrão.

Após criar o `package.json`, vamos criar duas pastas dentro de `test_browserify`, vamos chamar uma de `src` (onde ficará o código da sua aplicação) e a outra de `dist` (onde o código compilado será enviado). Repare que nada disso tem a ver com o Browserify, estamos apenas criando algumas pastas como acontece em qualquer outra aplicação.

Dentro da pasta `test_browserify/src`, vamos criar dois arquivos: `index.js` e `logger.js`.

O código do nosso arquivo `index.js` será:

```js
  var logger = require('./logger');

  logger.log();
```

E o nosso `logger.js` vai ter o seguinte código:

```js
  module.exports = {
    log: function() {
      console.log('Esta função está no arquivo logger.js :)');
    }
  };
```

Bem simples, certo? Dois arquivos JavaScript, o primeiro importando o segundo e executando uma função do mesmo. Agora entra o Browserify. Vamos usá-lo para gerar um bundle desta nossa inútil mini-aplicação.

Dentro da pasta `test_browserify`, rode o seguinte comando para instalar o Browserify como uma dependência de desenvolvimento do nosso projeto: `npm install --save-dev browserify`. Após isso você verá que o Browserify está listado como uma dependência no arquivo `package.json`.

Vamos adicionar um novo npm script para executar o Browserify. Dentro do campo `scripts` do seu `package.json` haverá já um script de teste (que simplesmente alerta que nenhum comando de testes foi configurado, podemos ignorar este fato), logo depois dele vamos adicionar o script de compilação. A opção `scripts` do seu `package.json` vai ficar assim:

```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "browserify src/index.js -o dist/index.js"
  },
```

Agora vamos executar o nosso novo npm script! Dentro da pasta `test_browserify`, execute o comando `npm run build`. Agora cheque o conteúdo do arquivo `dist/index.js`. O conteúdo de toda a sua aplicação está ali, não está? :)

Viu só? Configuramos o _bundling_ da sua aplicação JavaScript em menos de 5 minutos! E você até consegue entender o que aconteceu:

Quando você chama o comando `browserify src/index.js -o dist/index.js` dentro do nosso npm script, o que você está dizendo a ele é: "comece pelo meu arquivo `src/index.js` e percorra todas as suas dependências recursivamente, gere um arquivo com o código de todas estas dependências, e salve no arquivo `dist/index.js`". E é isso!

### Ok, mas e o Babel?! E o React? E o TypeScript?

_Calma lá, configurei o bundling da minha aplicação, mas tentei colocar uma classe no meu arquivo e não funcionou, como assim?!_ Acontece que o Browserify _por padrão_ só gera o arquivo com a árvore de dependências da aplicação, mas podemos adicionar _transforms_ a ele para que ele saiba  compilar novas sintaxes. Vamos configurar o Browserify para compilar seus módulos usando o Babel?

Para isso vamos usar uma transform do Browserify chamada [babelify](https://www.npmjs.com/package/babelify). Além do babelify, vamos também instalar o preset do Babel que sabe compilar ES2015. Vamos lá, execute o comando `npm install --save-dev babelify babel-preset-es2015` na pasta `test_browserify`, que irá instalar o babelify e o preset de ES2015.

Após a instalação do `babelify` e do `babel-preset-es2015`, vamos criar um arquivo `.babelrc` na pasta `test_browserify`, apenas para dizer ao Babel (através do babelify) quais presets gostaríamos de usar. O conteúdo do nosso arquivo `.babelrc` será simplesmente:

```json
  {
    "presets": ["es2015"]
  }
```

Agora vamos modificar o nosso npm script de `build` no nosso arquivo `package.json` para avisar ao Browserify que ele deve usar o babelify. O nosso comando agora vai ficar assim:

```json
  "build": "browserify src/index.js -o dist/index.js -t [ babelify ]"
```

Vamos modificar o conteúdo do nosso arquivo `src/logger.js` para usarmos algo com ES2015 para que possamos ver o resultado? Vamos deixá-lo assim:

```js
  class Logger {
    log() {
      console.log('Esta função está no arquivo logger.js :)');
    }
  }

  module.exports = new Logger();
```

Agora execute `npm run build` novamente e cheque o conteúdo do arquivo `dist/index.js`! Você verá que o código de toda aplicação estará ali, e a nossa classe vai ter sido compilada pelo babelify :)

Se quiser ver rodando no browser, crie um arquivo `index.html` dentro da pasta `test_browserify` com o seguinte conteúdo:

```html
  <html>
  <head>
    <title>Browserify</title>
  </head>
  <body>
    <script src="dist/index.js"></script>
  </body>
  </html>
```

Depois abra este arquivo no seu navegador, abra o console do navegador e veja que a mensagem foi logada lá.

Bem prático, não? Novamente, adicionamos compilação com Babel na nossa aplicação em menos de 5 minutos.

Se quiser permitir que sua aplicação agora também compile React/JSX, basta rodar o comando `npm install --save-dev babel-preset-react && npm install --save react`, para instalar o preset do Babel que compila React, e o próprio React na sua aplicação. Depois adicionar o preset `react` no seu array de presets do arquivo `.babelrc` e pronto! Agora seu comando `npm run build` também compila React.

Quer compilar também TypeScript com o Browserify de maneira fácil? Não seja por isso, você pode usar o [tsify](https://www.npmjs.com/package/tsify). CoffeeScript talvez? Use o [coffeeify](https://www.npmjs.com/package/coffeeify). Precisa dar `require` em arquivos de texto, como o código fonte para templates do Handlebars? Use o [stringify](https://www.npmjs.com/package/stringify).

### Mas eu preciso de watch!

Quer evitar de ter que rodar seu comando de build toda vez que modifica a sua aplicação? Que tal deixar um processo rodando ouvindo as modificações no seu código que rodará o Browserify automaticamente todas vez que uma modificação for feita? Para isso existe o [watchify](https://www.npmjs.com/package/watchify).

Para instalá-lo basta rodar `npm install --save-dev watchify`. Agora basta usá-lo no seu script da mesma forma que você usava o `browserify`, porém como `watchify`. Vamos modificar novamente o campo `scripts` do nosso `package.json` para adicionar o watchify. Ele vai ficar assim:

```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "browserify src/index.js -o dist/index.js -t [ babelify ]",
    "watch": "watchify src/index.js -o dist/index.js -t [ babelify ]"
  },
```

Agora execute `npm run watch`, e você verá que o watchify vai ficar esperando modificações no seu código para recompilá-lo. Modifique algum arquivo da sua aplicação (o nosso `logger.js`, por exemplo) enquanto este o comando `npm run watch` está rodando, e depois verifique o conteúdo do arquivo `dist/index.js`. Note que as modificações estarão lá!

### E os sourcemaps?

Precisa dos sourcemaps da sua aplicação para ter melhores mensagens de erros no console enquanto está desenvolvendo? A solução com o Browserify é simples! Simplesmente adicione a flag `--debug` no seu comando (tanto para o `browserify` quanto para o `watchify`) e pronto, agora o sourcemap do seu código estará no final do seu `dist/index.js` quando sua aplicação for compilada.

Com esta adição, o campo `scripts` do seu `package.json` ficará assim:

```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "browserify src/index.js -o dist/index.js -t [ babelify ] --debug",
    "watch": "watchify src/index.js -o dist/index.js -t [ babelify ] --debug"
  },
```

### Seja feliz

Bom, o básico que gostaria de passar para vocês sobre como escolher um module bundler para _prototipar_ ou _aprender algo novo_ é isso. Vá de Browserify, não sofra com longos arquivos de configuração, foque no que você está tentando aprender e na sua aplicação, não no _tooling_. Se mais tarde você sentir necessidade de algo que o Browserify não oferece, aí sim considere aprender como usar o Webpack. Mas acredite, pra quando se está estudando ou testando uma ideia rápida, o Browserify será mais do que o suficiente :)

Saiba também que o Browserify é muito mais do que isso, ele também possui ferramentas para permitir _hot reload_ de código, compilação e injeção de CSS, entre outros! Isso é assunto para um outro post, que não cabe a esta série. Mas se o assunto te interessou, recomendo a leitura do [Browserify Handbook](https://github.com/substack/browserify-handbook). Ele é um guia bem interessante, diretamente no _readme_ do repositório, sobre todas as capacidades do Browserify.

Agora vá ser feliz enquanto prototipa uma ideia ou aprende algo novo! :D