title: Porque padrões são importantes?
tags:
  - design patterns
  - padrões
categories:
  - Porque é importante?
date: 2015-10-28 21:26:00
---

Primeiramente, oi de novo :)

Depois de meses e meses de sumiço daqui, com vontade de voltar a escrever mas sem muita inspiração ou energia para isso, estou de volta, e espero que dessa vez eu consiga manter meu ritmo de pelo menos um post por semana.

Este é o primeiro post da categoria "Porque é importante?". Os posts dessa categoria vão se focar em debater sobre o porque tal conceito, ferramenta ou técnica é importante, e porque você deve dar atenção ao mesmo.

Neste post, vamos falar um pouco sobre padronização em geral, de convenções à _design patterns_!

<img src="http://imgs.xkcd.com/comics/standards.png" />

<!-- more -->

### Definição

O dicionário Aurélio define [padrão](http://dicionariodoaurelio.com/padrao) como:

> 1. Tipo oficial de pesos e medidas.

> 2. O que serve de referência.

Vamos focar na segunda definição, `O que serve de referência`.

Ter uma referência quando se está programando é bastante importante, pois te ajuda a definir mais rapidamente onde você colocará tal código, como partes diferentes do código se comunicarão, além de facilitar que você entenda como o código que já existe funciona.

### Convenções

As convenções de nomeação, organização de pastas e afins são uns dos grandes agentes que permitem que os arquivos do seu projeto se mantenham organizados em todo o seu decorrer.

No desenvolvimento de software existe um conceito chamado [Convenção sobre configuração](https://en.wikipedia.org/wiki/Convention_over_configuration), este conceito prega que apenas _exceções_ da sua aplicação devem ser configuradas manualmente. Tudo que for dentro dos padrões só precisa seguir a convenção especificada e já funcionará automaticamente.

O pessoal do Ruby on Rails sabe bem do que estou falando, pois ele segue muito bem o conceito de convenção sobre configuração. Quer um exemplo? Por padrão todo model tem o nome no singular e em [CamelCase](https://en.wikipedia.org/wiki/CamelCase), e é associado a uma tabela no banco de dados no plural e em [snake_case](https://en.wikipedia.org/wiki/Snake_case).

Um outro exemplo é o modo como funciona o [roteamento de resources](http://guides.rubyonrails.org/routing.html#crud-verbs-and-actions)!

Conseguiu notar o quanto o uso de convenções é importante? ;)

### Generalização

Seguir padrões também permite que generalização de código, que gera reaproveitamento de código, que por si gera desenvolvimento mais rápido e confiável!

Vamos supor que sua aplicação expõe uma API. Já pensou se alguns _endpoints_ retornassem JSON e outros XML? E se alguns retornassem um JSON com uma chave `data` com um _array_ de dados, mas outras com uma chave com o nome do _resource_ que você requisitou? Não haveria um modo comum de consumir esta API, seria necessário que a requisição para cada um desses _endpoints_ fosse tratado individualmente! Isso ocasionaria em mais código a ser escrito, mais código a ser testado, e mais código a ser modificado caso toda a sua API mudasse!

E mais, pro pessoal do CSS. Já pensou se toda vez que você quisesse um botão de uma nova cor, mas com o mesmo tamanho de fonte dos outros, você precisasse reescrever todo o estilo do botão novamente? E se esse tamanho mudasse?!

Pois é, tentar generalizar o código faz com que, com o passar do tempo, você tenda a ter que escrever *menos* código na sua aplicação, pois a parte mais pesada já está feita e pronta para ser aproveitada, você só vai precisar configurar a pequena parcela específica da sua nova _feature_. Notou a semelhança com o item sobre convenções?

### Design patterns

Se você já programou alguma coisa além do básico na sua vida, você possivelmente já ouviu falar de _design patterns_ (caso não, talvez você deva começar por [aqui](/2015/02/01/Como-comecar-a-programar-ou-aprender-uma-nova-linguagem/)).

Os _design patterns_ são soluções genéricas e reutilizáveis para problemas recorrentes na hora de desenvolver uma solução para um problema. Os primeiros _design patterns_ a serem documentados foram escritos no livro [Design Patterns - Elements of Reusable Object-Oriented Software](http://c2.com/cgi/wiki?DesignPatternsBook), por uns caras conhecidos como _Gang of Four_ (por isso o livro também é conhecido como o "livro do GoF").

Vamos supor que, por algum motivo, você quer que uma certa classe do seu projeto possa ser instanciada uma só vez e, toda vez que ela for usada, a mesma instância deve ser usada. Complicado? Simples? Independente do quão complexo você pensa ser este problema, saiba que já há um _design pattern_ que documenta como fazer isso, ele é chamado de [Singleton](https://en.wikipedia.org/wiki/Singleton_pattern).

Preferi exemplificar o _singleton_ pois ele é o mais simples de ser compreendido. Mas podemos aqui citar um outro que você possivelmente conhece, o [MVC](http://martinfowler.com/eaaCatalog/modelViewController.html)! Sim, ele também é um _design pattern_ mas que, ao contrário do _singleton_, ele foi documentado pelo desenvolvedor Martin Fowler, no livro [Patterns of Enterprise Application Architecture](http://martinfowler.com/books/eaa.html).

É de extrema importância que você conheça a maior quantidade de _design patterns_ possível. Mesmo que não os decore, pense em procurar entre os já documentados toda vez que você cair em um problema que não consegue pensar numa boa solução, possívelmente alguém já pensou nela por você. Isso não só fará com que o desenvolvimento do seu projeto seja mais rápido, como permitirá que uma nova pessoa que entrar no projeto e já conhecer o _design pattern_ usado consiga ter uma ideia de como seu sistema funciona sem ter que escavar o código fonte todo.

### Conclusão

E aí? Consegui te convencer da importância da padronização na hora de desenvolver? Caso tenha alguma dúvida ou sugestão, sinta-se livre para comentar ali em baixo!

Fonte das imagens:

* [Standards](http://xkcd.com/927/)