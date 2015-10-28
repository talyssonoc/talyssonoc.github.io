title: "We need to go deeper: Se aprofundando em uma linguagem"
date: 2015-02-06 23:29:00
tags:
  - linguagens
  - intermediário
categories:
  - Estudos
---

O post anterior era direcionado para pessoas que nunca programaram antes, ou que estão começando uma nova linguagem e ainda estão meio perdidas. Ele pode ter parecido meio genérico, meio _desnecessauro_, mas quando eu comecei a programar, há cerca de 6 anos atrás, eu queria muito ter encontrado algo que me direcionasse naquele começo.

Este post é pra quem já sabe uma linguagem, mas quer se aprofundar mais nela, se especializar, saber usar ferramentas de apoio (como _task runners_, repositórios de pacotes...), não precisar de tutorial de tudo pra ter capacidade de criar algo com a linguagem, entre outros.

<!-- more -->

"Mas, Talysson, quem você acha que é pra falar sobre esse assunto?!". Bom, eu não sou profissional em alguma linguagem, por enquanto, mas posso dizer que já sei JavaScript o bastante pra me encaixar na descrição que fiz na parágrafo anterior (mas nunca parei de aprender!), e é um processo que só aconteceu por que mudei meu modo de ter contato com a linguagem no último ano, então resolvi falar um pouco sobre isso.

### GitHub e a comunidade

A primeira mudança a se fazer para se aprofundar em uma linguagem é acompanhar a comunidade da mesma, seguir desenvolvedores que se destacam, entre outros. E que lugar melhor pra isso do que o [GitHub](https://github.com/)?

Com uma conta no GitHub você poderá passar a seguir outros perfis de desenvolvedores, e ver novos repositórios que eles se interessaram (o que fará com que você conheça novas ferramentas da linguagem). Com o tempo você passará a observar códigos nessas linguagens, e isso te fará crescer e aprender muito, acredite.

Procure saber quem são os desenvolvedores mais notáveis dentro da linguagem ou biblioteca que quer se aprofundar, siga-os no GitHub e/ou Twitter, siga também o criador na linguagem, desenvolvedores de bibliotecas, empresas que tem o open-source como cultura, entre outros.

Uma outra forma de interagir com a comunidade é acessando o sub-[Reddit](http://reddit.com) da linguagem, eles costumam ser bastante movimentados, com todo tipo de gente anunciando novidades e/ou respondendo dúvidas!

### _Coding style_

Uma outra coisa a se __educar__ é seguir algum _coding style_ adotado pela comunidade da linguagem que você usa. Você perceberá que em alguma linguagens é mais comum usar aspas simples, mesmo a linguagem suportanto também as duplas, simplesmente porque toda a comunidade decidiu assim, ou é mais comum usar identação com dois espaços, etc.

Há muitas ferramentas que podem te ajudar a seguir um _coding style_, e uma das melhores é o [EditorConfig](http://editorconfig.org/). O EditorConfig é um plugin com suporte a vários editores de código e IDEs que formata seu código da maneira que você configurou no seu arquivo `.editorconfig`.

Assim, basta ir em algum repositório importante da linguagem que você usa e pegar o arquivo `.editorconfig` e configurar para usá-lo no seu projeto.

Existem também ferramentas que checam se o seu código está seguindo um dado padrão, não diretamente no seu editor, mas fora dele. No mundo do JavaScript pode-se citar o [JSHint](https://www.npmjs.com/package/jshint) e o [JSCS](https://www.npmjs.com/package/jscs).

### _Programming is awesome!_

Uma coisa que eu não conhecia a existência até cerca de 6 meses atrás são os "awesome" de uma linguagem. Alguns desenvolvedores costumam criar listas de links importantes para uma linguagem ou biblioteca, separá-los por tópico.

Você pode ver um exemplo aqui de um dos [awesome-javascript](https://github.com/sorrycc/awesome-javascript), eles costumam possuir bastante conteúdo, de ótima qualidade, de ferramentas e informações para você poder se aprofundar.

Existem também alguns desenvolvedores que listam vários destes awesomes em um repositório, como esses abaixo:

* [awesome-awesomeness](https://github.com/bayandin/awesome-awesomeness)
* [awesome](https://github.com/sindresorhus/awesome)
* [awesome-awesome](https://github.com/emijrp/awesome-awesome)

E, claro, tem sempre aqueles que vão além e reúnem listas de listas que reúnem awesomes, como você pode ver no repositório [awesome-awesome-awesome](https://github.com/t3chnoboy/awesome-awesome-awesome).

### Fique por dentro das novidades

Ficar por dentro de novas criações, bibliotecas, plugins e afins para a linguagem que você está estudando também é bastante importante para você se aprofundar. Um jeito de fazer isso de uma forma fácil, sem ficar procurando vários sites, é assinar o Weekly da linguagem correspondente.

Existem Weekly's sobre várias linguagens e frameworks, e eles enviam um _digest_ toda semana para seu e-mail com as novidades e informações!

Abaixo segue o link de algumas:

* [JavaScript Weekly](http://javascriptweekly.com/)
* [Node Weekly](http://nodeweekly.com/)
* [Go Weekly](http://golangweekly.com/)
* [Ruby Weekly](http://rubyweekly.com/)
* [Rails Weekly](https://rails-weekly.ongoodbits.com/)
* [CSS Weekly](http://css-weekly.com/)
* [Android Weekly](http://androidweekly.net/)

É claro que existem várias outras, veja neste link um [jeito fácil de achar a weekly da sua linguagem](http://goo.gl/vJ3WtY).

### Produzir

Uma outra forma de se aprofundar é tentar produzir algo, criar um framework (sem medo de estar reinventando a roda, afinal só assim você vai descobrir problemas reais), uma biblioteca, tentar resolver _issues_ do repositório oficial, entre outros! Desta forma você poderá receber _feedback_ da comunidade, críticas (as vezes negativas, mas não desanime!), conhecer outros desenvolvedores no mesmo nível que o seu para dividir projetos.

### Testes

Depois de começar a produzir, notará que ter um código manutenível costuma implicar no uso de testes automatizados, testes unitários, testes de integração, entre outros.

Começar a escrever testes e conhecer frameworks de testes para a linguagem que você usa é um bom jeito de se aprofundar nela! Não sabe onde achar conteúdo ou nomes de frameworks de testes? Veja o item acima "_Programming is awesome!_". =)

### _Tooling_

Assim que começar a testar, possivelmente vai notar que executar os testes na mão o tempo todo, ou ter que dar _build_ no projeto manualmente antes de testar vai fazer sua produtividade cair. E é aí que entram as ferramentas!

Usar _task runners_ (como o [Gulp](http://gulpjs.com/) ou o [Grunt](http://gruntjs.com/), do JavaScript) facilita muito a vida, você poderá criar tarefas que executam todos os testes de uma só vez, ou que constroem seu projeto de forma automatizada (sem correr o risco de você esquecer algo toda vez), minificar o código (no caso do JavaScript ou CSS), checar seu _coding style_, ou até integrar todos estes passos (por exemplo, checar se segue o _coding style_, depois executar os testes e, se passarem, dar _build_ no projeto e fazer o _deploy_ do mesmo).

Assim como frameworks de testes, informações sobre ferramentas para a linguagem que você está usando podem ser encontradas no tópico "_Programming is awesome!_".