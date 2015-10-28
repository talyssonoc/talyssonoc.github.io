title: Como começar a programar ou aprender uma nova linguagem
date: 2015-02-01 17:54:00
tags:
  - linguagens
  - iniciante
categories:
  - Estudos
---

Boom! De repente você quer (ou _precisa_) aprender uma nova linguagem, ou mesmo começar sua vida na progrmaação, e não faz ideia de por onde começar, onde procurar, como _praticar_, onde achar pessoas na mesma situação ou que já sabem o que você deseja aprender. __O que fazer?__

Neste post vou falar um pouco sobre como aprender uma nova linguagem, onde procurar conteúdo, entre outros!

<!-- more -->

### _RTFM_

Antes de começar a escrever códigos com uma linguagem é necessário aprender o básico da linguagem, saber a sintaxe, o paradigma e tudo mais, não?

<img style="width: 350px" src="http://imgs.xkcd.com/comics/rtfm.png"/>

Quando se está começando com uma nova linguagem, uma ótima coisa a se fazer é, primeiramente verificar se no site oficial da mesma existe um _Get started_. Esses guias costumam dar um basicão da linguagem, algo bem por cima: introdução da sintaxe, tipos (se for uma [linguagem tipada](https://en.wikipedia.org/wiki/Type_system)), funções padrão, criação de estruturas/classes, entre outros.

Após isso, pode ser uma boa procurar se o autor da linguagem, ou algum _expert_ da mesma, já lançou algum conteúdo de apoio oficial, como o _JavaScript: The Good Parts_, do [Douglas Crockford](http://crockford.com/).

Durante o aprendizado, se algum detalhe não ficou claro no conteúdo que você está usando para estudar, você pode também olhar na API da linguagem, que pode ser encontrado no próprio site oficial ou em sites como o [OverAPI.com](http://overapi.com/).

### Olá, mundo!

Se você ainda não programa, talvez não tenha entendido a (tentativa de) brincadeira no título do primeiro post deste blog. "Olá, mundo" é o um padrão seguido como o primeiro programa que se deve fazer quando se aprende uma nova linguagem. Como o próprio nome diz, um programa que simplesmente exibe "Olá, mundo!" na tela. Isso pode variar em alguns casos, como o [blink](http://arduino.cc/en/tutorial/blink), o "Olá, mundo" do Arduino, que faz piscar o led 13 da placa.

Explicações a parte, é importante fazer este programa e, logo de começo, tentar entendê-lo. Dizem uns até que, caso não o faça, você cairá numa maldição em relação à linguagem pretendida e nunca se dará bem com ela.

Caso você seja um iniciante em JavaScript, por exemplo, o seu "Olá, mundo" ficaria assim (aperte F12 no seu navegador, vá à aba Console, e use o código abaixo).

```js
console.log('Olá, mundo!');
```

Sim, simples assim! Em todo tutorial, apostila, livro ou documentação decente de uma linguagem, você será apresentado ao "Olá, mundo" da mesma. Como eu disse ali em cima, logo após escrever (não vale copiar e colar!) seu programa inicial, tente entendê-lo, procurar no Google as funções e _features_ da linguagem que usou nele.

Caso queira ver exemplos de "Olá, mundo" em outras linguagens, a Wikipédia possui uma [lista de programas "Olá, mundo"](http://en.wikipedia.org/wiki/List_of_Hello_world_program_examples).

### Algoritmos clichê

Assim que aprender e entender o "Olá, mundo", é comum (e efetivo!) escrever alguns programas clichê com a linguagem, coisas comuns que te ajudarão a notar o que ainda não sabe sobre a linguagem, e a procurar sobre (dicas de onde procurar conteúdo sobre a linguagem estarão nos próximos itens deste mesmo post!). Alguns exemplos:

- Modificar o "Olá, mundo" para ler o nome do usuário e cumprimentá-lo
- Calculadora básica
- Descobrir se um número é primo
- Calcular [sequência de Fibonacci](http://en.wikipedia.org/wiki/Fibonacci_number)
- Multiplicação de matrizes compatíveis de qualquer dimensão
- Testar se um número obedece à [conjectura de Collatz](http://en.wikipedia.org/wiki/Collatz_conjecture)

Após este ponto, você já estará um pouco mais acostumado com a linguagem!

### Resolução de problemas

Quando já estiver mais confiante com a linguagem, procure outros algoritmos para implementar, desafios, e tente resolvê-los.

Um site com bons exercícios que eu costumava usar quando estava aprendendo é o SPOJ. Ele possui um grande acervo de [algoritmos clássicos](http://www.spoj.com/problems/classical/) e [desafios](http://www.spoj.com/problems/challenge/) para serem implementados!

### Estou preso, me ajudem!

Quando estamos aprendendo, há sempre um ponto, uma pedra no caminho, que acabamos travando, geralmente um problema em relação à linguagem, e não à sua lógica, que te faz desanimar (ou o contrário!) por não saber como procurar. E pior, em alguns casos parece não haver a solução em lugar algum!

<img style="width: 550px" src="http://imgs.xkcd.com/comics/wisdom_of_the_ancients.png"/>

A dica é não se desesperar e saber onde procurar (ou perguntar) pela resposta.

Eu costumo seguir a seguinte ordem quando não consigo resolver o problema usando somente o Google:

1. Procurar na documentação;
2. Procurar nos _known issues_ da linguagem para ver se não é realmente um bug;
3. Procurar no [StackOverflow](http://stackoverflow.com/);
4. Procurar no sub-[Reddit](http://www.reddit.com/) da linguagem;
5. Perguntar no StackOverflow e, se ninguém responder;
6. Perguntar no sub-Reddit da linguagem.

### Programar, programar, programar!

Assim como outras atividades da vida, programar não é algo que basta ler a teoria e não praticar. Você já viu alguém ler um livro sobre andar de bicicleta sem nunca ter encostado em uma antes e depois sair andando?

Da mesma forma, para aprender a programar em uma linguagem, dominá-la, é importante programar usando a mesma, exaustivamente se necessário.

### Conversar sobre

Por fim, se você conhecer alguma outra pessoa que esteja estudando a mesma linguagem, ou já saiba usá-la, converse com a pessoa sobre, discuta o porque de usar uma função ao invés de outra, como faria tal coisa, vai ver que só o fato de discutir já vai te ajudar bastante!

Bom, são essas as minhas dicas para iniciantes na programação ou em uma nova linguagem de programação. Em breve farei um post para quem já sabe uma linguagem mas quer se aprofundar nela!

Fonte das imagens:

* [RTFM](http://xkcd.com/293/)
* [Wisdom of the Ancients](http://xkcd.com/979/)