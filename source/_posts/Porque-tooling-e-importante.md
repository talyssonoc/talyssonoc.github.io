title: Porque tooling é importante?
tags:
  - tooling
  - javascript
categories:
  - Porque é importante?
date: 2015-12-08 08:35:00
---
Quando se trata de desenvolvimento, o lado humano é sempre o elo mais fraco. Isso se aplica tanto à [segurança da informação](https://en.wikipedia.org/wiki/Social_engineering_%28security%29) quando à confiança que se pode ter no código da aplicação. A possibilidade de um programador inserir um bug no código é _bem maior_ do que a do compilador gerar um código com problemas.

Dado que máquinas tendem a errar menos, o que podemos fazer é passar responsabilidade de algumas tarefas para o computador, ou seja, __automatizá-las__. Automatizar suas tarefas não só fará com que você crie aplicações mais confiáveis, como também terá um fluxo de desenvolvimento mais rápido. Isto pode ser feito pelo que chamamos no mundo do desenvolvimento de _tooling_.

Neste post vou discutir a importância de usar este tipo de ferramenta, que é importante inclusive para o seu [aprofundamento na linguagem](http://talyssonoc.github.io/2015/02/06/Se-aprofundando-em-uma-linguagem/#tooling).

<img src="/img/posts/tools.jpg"/>

<!-- more -->

Não vão ser poucas as vezes que você vai ser questionado sobre _o porquê_ de usar tooling, _o porquê_ de usar automatização mesmo em tarefas aparentemente triviais. Em contrapartida, haverá diversas pessoas tentando te convencer a usar _tooling_ sem te dizer exatamente qual a importância que isso terá no desenvolvimento da sua aplicação!

Pra tentar te convencer da importância do uso de _tooling_, vou separar estas ferramentas em categorias, e debater sobre a importância de cada uma delas.

### Gerenciadores de dependência

Eu considero os gerenciadores de dependência como o mínimo de _tooling_ que você deve ter no seu projeto. Isso é, se você for o tipo de pessoa que não gosta de usar ferramentas externas no seu desenvolvimento, se acha isso tudo desnecessário ou você simplesmente não se adapta a usá-las, use pelo menos um gerenciador de dependência.

Se você conhece o [Twelve-Factor App](http://12factor.net/) saberá que não estou falando bobagem. O segundo item da lista de fatores já diz respeito à [declaração de dependências](http://12factor.net/dependencies). As dependências do seu projeto devem ser declaradas explicitamente em algum tipo de arquivo-manifesto (e.g.: _package.json_, _Gemfile_, _composer.json_, _Vagrantfile_, entre outros) e devem estar isoladas do seu código.

Isso quer dizer que você não deve baixar manualmente as dependências e jogar lá em uma pasta _vendor_, ou pior: entre os arquivos da sua aplicação. Não! Elas devem estar declaradas e ser baixadas automaticamente por um gerenciador de dependências.

A importância disso? Organização, versionamento e facilidade de _setup_ do projeto. Se você precisa atualizar uma dependência, é muito mais fácil e confiável ir lá no seu arquivo-manifesto onde suas dependências estão declaradas, alterar a versão da dependência e usar seu gerenciador de dependências baixar a versão configurada do que procurar os arquivos de terceiros entre os seus, apagar e baixar os novos manualmente.

Você já deve ter se deparado com um cenário do tipo: vários arquivos `jquery.min.js` espalhados pelas pastas do projeto, as vezes até em versões diferentes! Já pensou se precisar atualizar o jQuery e ter que sair procurando estes arquivos para substituí-los?

E mais! Se é uma dependência de _backend_, fica muito mais fácil saber se alguma biblioteca do sistema operacional precisa ser baixada se você já tiver essas dependências declaradas em algum lugar, permitindo inclusive que o próprio gerenciador te avise sobre a necessidade da biblioteca (se você já usou algum pacote do Composer com uma dependência de algum módulo do PHP, saberá do que eu estou falando).

Deu pra sacar? Faça um favor a si mesmo e use, pelo menos, um gerenciador de dependências! Segue alguns exemplos de gerenciadores de dependência para diferentes linguagens:

- JavaScript: [npm](https://www.npmjs.com/)
- Ruby: [Bundler](http://bundler.io/)
- PHP: [Composer](https://getcomposer.org/)
- Python: [pip](https://pypi.python.org/pypi/pip)
- Java: [Maven](https://maven.apache.org/)
- Haskell: [Cabal](https://www.haskell.org/cabal/)

### Transpilers, preprocessors e bundlers

Possivelmente um dos tipos mais usados de ferramentas por desenvolvedores _frontend_, os transpilers/preprocessors/bundlers permitem que o programador tenha mais conforto na hora de desenvolver sua aplicação, crie códigos mais manuteníveis, e gera uma série de facilidades.

Vamos para o exemplo mais prático: JavaScript não possuia um padrão para módulos até este ano. E, inclusive hoje em dia, é necessário usar de artifícios que nos permita escrever códigos separados em módulos, de preferência que nos permita evitar a inserção de vários tags `script` no HTML.

Estes artifícios podem ser chamados de _bundlers_, que nos permitem escrever códigos em padrões de módulos como o CommonJS e o AMD (Asynchronous Module Definition), que por padrão não são entendidos pelo navegador, e gerar códigos que o navegador consegue entender e que respeitam as limitações impostas pelos módulos (como escopos isolados, por exemplo).

Dentro do JavaScript, podemos citar como exemplos de _bundlers_ o [Browserify](http://browserify.org/), o [webpack](https://webpack.github.io/) e o [rollup.js](rollupjs.org/).

Com comportamento semelhante podemos citar os transpilers, preprocessors e postprocessors. Eles permitem adicionar à linguagem features que elas não possuem, como permitir que classes do JavaScript possam ser _compiladas_ para funções com protótipos para serem usadas em navegadores antigos, utilização de [JSX](https://facebook.github.io/jsx/), ou utilizar funções e variáveis no CSS.

Se você é programador, já deve ter sacado a importância de ferramentas assim. Já pensou ter que percorrer todos seus arquivos CSS toda vez que uma cor principal do seu sistema mudar? Se fosse em uma linguagem de programação você já teria parametrizado isso, não? Pois é, porque não fazer isso com CSS também?

Pois é, em se tratando de transpilers JavaScript você tem __diversas__ opções, você pode encontrar mais sobre isso no post [JavaScript: adicione açúcar a gosto e pare de reclamar](http://talyssonoc.github.io/2015/11/23/JavaScript-adicione-acucar-a-gosto-e-pare-de-reclamar/) e lá se aprofundar mais sobre o assunto!

Quanto aos preprocessors e postprocessors, você tem a sua disposição, por exemplo, o [Sass](http://sass-lang.com/) e o [PostCSS](https://github.com/postcss/postcss), que de maneiras diferentes e complementares permitem que você evolua _bastante_ seu ciclo de desenvolvimento de CSS, possibilitante inclusive a escrita de módulos em CSS!

Você consegue encontrar mais sobre o assunto nos [guias para iniciantes de Sass](http://thesassway.com/beginner), nos tutoriais da [Level Up Tuts](https://www.youtube.com/playlist?list=PL2CB1F80266E986EA) e nesta [talk do Fernando Fleury sobre PostCSS](https://www.youtube.com/watch?v=hWNzhKIa34w).

Se você ainda não confia nesse tipo de ferramenta, vou citar _novamente_ uma frase do Kyle Simpson, conhecido na internet como @getify e desenvolvedor de ferramentas como o Browserify:

> Transpiled code isn’t great code, but it’s probably better than the code you’ve been writing for the last 20 years.

### Linters/analisadores estáticos

Os linters são ferramentas que analisam o seu código de maneira estática, ou seja, sem executá-los, à procura de possíveis problemas e erros de digitação (como por exemplo, um `=` no lugar onde deveria haver um `==`), permite encontrar [_code smells_](http://martinfowler.com/bliki/CodeSmell.html), más práticas e códigos mal formatados.

Quer alguns exemplos? Um linter pode te ajudar a identificar códigos duplicados, variáveis não usadas, utilização de classes inexistentes, duplicação de regras do CSS, entre outros!

E se você acha que você mesmo consegue fazer isso sozinho, sem usar de um linter, lembre-se da frase do começo do post: o lado humano é o sempre o elo mais fraco. A possibilidade de algum código propenso a falha passar sem ser percebido pelos seus olhos é bem maior do que caso isso for checado por um programa escrito para isso.

Um exemplo bom pra você que ainda não entendeu o que é um linter é o [write good](https://github.com/btford/write-good), ele é um linter de _inglês_. Sim, isso mesmo, ele analisa suas frases escritas em inglês que checa por más práticas de escritas e possiveis erros no seu texto!

Segue alguns exemplos de linters:

- JavaScript: [ESLint](http://eslint.org/) e [JSHint](http://jshint.com/)
- Sass/CSS: [scss-lint](https://github.com/brigade/scss-lint)
- Ruby: [RuboCop](https://github.com/bbatsov/rubocop) e [Hound](https://houndci.com/)
- PHP: [PHP Analyzer](https://scrutinizer-ci.com/docs/tools/php/php-analyzer/)

### Task runners e builders

Ao conhecer todos esses tipos de ferramentas, você deve estar se perguntando o quão difícil é para gerenciar e intergrar todas elas, não? Pois saiba que há uma categoria destas ferramentas feita justamente para executar várias dessas ferramentas, integrá-las e permitir nomear tarefas. Estas ferramentas são chamadas de _task runners_.

Já imaginou, toda vez que você precisar fazer um _release_ de uma aplicação você ter que rodar a CLI do Sass e do Babel manualmente? Já pensou ter que rodar seu linter em cada um dos seus códigos um por um? Pois é, aí reside a importância dos _task runners_!

Os _task runners_, de maneira geral, permite que você crie e nomeie tarefas do seu ciclo de desenvolvimento, inclusive permitindo que elas componham novas tarefas.

Por exemplo, você pode ter uma tarefa que faz o lint dos seus códigos JavaScript e CSS, uma outra que faz o lint dos códigos Ruby, uma outra que compila e minifica seu JavaScript, e uma outra que executa todos os testes. Com estas tarefas você pode criar uma nova que faz o lint do código, executa os testes e, se eles passarem, executa cada uma tarefas de _build_ do seu código.

Se você é um desenvolvedor Rails, já deve estar acostumada com tarefas do Rake que facilitam sua vida, ou a criação de npm scripts, como um _watch_, para agilizar o desenvolvimento. Conseguiu entender a importância?

Segue alguns exemplos de _task runners_ e _builders_:

- JavaScript/CSS: [gulp](http://gulpjs.com/), [grunt](http://gruntjs.com/) e [brunch](http://brunch.io/)
- Ruby: [Rake](https://github.com/ruby/rake)
- PHP: [Phing](https://www.phing.info/) e [Artisan](http://laravel.com/docs/5.1/artisan)
- Java: [Ant](http://ant.apache.org/) e [Gradle](http://gradle.org/)

### Pinceladas finais

Deu pra entender a importância do uso de _tooling_? Se você já sabia a importância e como usar estas ferramentas, espero ter aprofundado ainda mais o seu conhecimento!

Se você é um desenvolvedor front-end, tenho alguns links para te indicar:

- [Front-end tooling: porque e como?](https://speakerdeck.com/talyssonoc/front-end-tooling-porque-e-como)
- [Book of Modern frontend tooling](http://tooling.github.io/book-of-modern-frontend-tooling/build-systems/grunt/linter.html)
- [W3C Modern Tooling](https://w3c.github.io/modern-tooling/)

O ponto chave deste post é: __automatize, seja como for, seja qual for a ferramenta que te deixar confortável, automatize!!!__

Ainda existem muitas outras categorias de ferramentas, como os _scaffolders_, _test runners_ e tudo mais, até a próxima!

Fonte das imagens:

- [Tools](http://www.ecmag.com/section/your-business/cool-tools-hand-tools)