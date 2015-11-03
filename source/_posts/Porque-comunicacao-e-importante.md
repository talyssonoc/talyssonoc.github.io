title: Porque comunicação é importante?
tags:
  - comunicação
  - bug report
  - expectativa
categories:
  - Porque é importante?
date: 2015-11-01 01:15:00
---

Que a comunicação é um fator de extrema importância eu sei que você concorda (~~eu espero~~), mas você já se perguntou _quais_ aspectos a comunicação (ou a falta dela) afeta mais? Essa é a ideia desse post!

A comunicação pode ser definida como o ato de _transmitir uma mensagem e, eventualmente, receber uma mensagem de resposta_. Porém frequentemente as pessoas esquecem que _transmitir uma mensagem_ não é simplesmente emiti-la, mas sim fazer com que seu interlocutor __entenda__ a mesma.

<img src="http://vidadesuporte.com.br/wp-content/uploads/2014/04/Suporte_970.jpg" />

<!-- more -->

### Expectativas

Se comunicar com os membros do time e com os _stakeholders_ de forma a controlar suas expectativas talvez seja um dos maiores pontos em relação à importância da comunicação. Caso uma parte do projeto vá atrasar a saída, é melhor dizer o quanto antes for sabido do fato para o cliente do que surpreendê-lo com uma entrega incompleta no dia da reunião de demonstração. Avisar a membros do time que algum membro se ausentará, ter alguém com informações importantes sobre o produto sempre disponível (a distração nesses casos é mínima, dado que o envio dessas informações pode ser de maneira informal e rápida, veja o item abaixo ;)), ter descrições fiéis do que será gerado no fim do _sprint_ (sim, é difícil, mas o esforço vale a pena)... talvez seja um dos maiores pontos para não causar sustos na hora das entregas ou nos _reviews_ dos _sprints_.

### Formal vs. informal

Um ponto a se ponderar é o que deve ser tratado de maneira formal vs. o que pode ser comunicado informalmente. Comunicação formal é sempre mais lenta, mais metódica, porém a fonte dos dados é sempre mais _confiável_. Utilizar o email de maneira formal o tempo todo para pedir ajuda com uma determinada parte do código pode atrasar muito o processo, assim como usar um sistema de mensagens instantâneas (como o Slack, HipChat...) para documentar os requisitos pedidos pelo cliente torna este dado pouco _oficial_.

É importante separar o que deve ser usado com cada meio de comunicação, assim como ter em mente que a qualquer momento você pode, por exemplo, tomar uma decisão importante usando um sistema de mensagens instantâneas para agilizar a comunicação e posteriormente oficializá-lo com um email respondido por todos os envolvidos confirmando.

Seja qual for o nível de seriedade do meio de comunicação, a clareza é sempre um ponto de extrema importância. Não espere que o pessoal do jurídico saiba o que é uma _requisição AJAX_, por exemplo. Explique, dê exemplos, use analogias, seja claro.

### Reuniões

Vamos (teoricamente) entrar num consenso: reuniões são chatas. Reuniões são, geralmente, cheias de cerimônias, burocracias e afins. Porém, acima de tudo, necessárias. Periodicamente é importante ter uma reunião um pouco mais séria (os _sprint reviews_, _release review_, entre outros), mas uma grande maioria dos assuntos que são tratados nestas reuniões podem ser convertidos em reuniões mais ágeis, menos formais, como as [_standup meetings_](https://www.mountaingoatsoftware.com/agile/scrum/daily-scrum), e, caso surja algum assunto de maior relevância, ele pode ser simplesmente oficializado através de um email (veja o item anterior).

### Bug report

A falta de clareza e descrição nos _bug reports_ são uma grande causa da demora para evoluir um software e resolver problemas do mesmo. Não são raros os casos em que pessoas que fazem _bug report_ (tanto usuários, quanto _stakeholders_ e membros do time) de maneira bastante superficial, sem reportar o contexto em que o problema aconteceu (browser que estava usando, sistema operacional...), ou até sem reportar qual foi o erro de fato. É comum ver coisas do tipo:

> Não funcionou 100%

> Está dando problema

> O botão não funciona

Esses são exemplos reais que vi recentemente no Google Play. Agora pense: como o time de desenvolvimento vai poder resolver os possíveis problemas dos dados aplicativos sem saber exatamente o que acontece, e quanto acontece?

Conscientizar os usuários do seu produto, assim como as pessoas que o testam antes do _release_ sobre a importância de um _bug report_ descritivo é bastante importante e, como você pode ver pelos exemplos acima, de __extrema__ importância para a evolução do projeto.

### Pedindo ajuda

Assim como reportar _bugs_, a clareza na hora de pedir ajuda é de extrema importância.

Indo direto ao ponto mais crítico, é preciso tomar cuidado para não cair no chamado ["X-Y" Problem](http://mywiki.wooledge.org/XyProblem). Digo isso porque é uma das maiores causas de perguntas não responsidas no [StackOverflow](http://stackoverflow.com/). O problema é o seguinte:

1. Usuário quer fazer X
2. Usuário não sabe fazer X, mas acha que vai descobrir como fazer se ele souber como fazer Y
3. Usuário também não sabe fazer Y
4. Usuário pede ajuda com Y
5. Outro usuário ajuda com Y, mas fica confuso porque Y parece um problema estranho de se resolver
6. Depois de muito tempo perdido, fica claro que Usuário quer fazer X e Y nem resolvia o problema

Na passagem desses passos, muito tempo de desenvolvimento e, consequentemente, __dinheiro__ é perdido.

O próprio StackOverflow tem um bom guia de [como pedir ajuda](http://stackoverflow.com/help/how-to-ask) que pode ser aplicado à varios outros contextos que não sejam o StackOverflow.

### Nunca espere que algo seja subentendido

Voltamos ao ponto _clareza_. Evitar que coisas sejam subentendidas é também algo que agiliza, e muito, o processo de desenvolvimento. Isso é de ainda mais peso quando trata-se da comunicação intersetorial. É comum o designer ou o UX esperar que o desenvolvedor subentenda que uma certa animação aconteça, mas se esquece que o PSD ou o _mock_ não possui animações. Ou o frontend esperar que o backend subentenda que a JSON API tem que aceitar tal parâmetro.

Esperar que algo seja feito errado, que ou a dúvida surja, antes que algo mais descritivo seja produzido pode se tornar um veneno para o seu projeto. Nem sempre todos os membros do time estarão disponíveis para responder dúvidas, portanto ser claro na hora de descrever algo é de extrema importância.

### Conclusão

Esses foram os pontos mais críticos quanto à comunicação que achei importante levantar, baseados em experiências e observações minhas. Caso não tenha notado, o centro da discussão foi: __clareza__. Ser claro evita mals entendidos, que evita retrabalho e travamentos no desenvolvimento.

Sinta-se livre para comentar coisas a serem corrigidas e acrescentadas!

Leitura complementar:

- [How To Communicate Effectively In IT Projects](http://www.smashingmagazine.com/2014/06/communicating-effectively-in-projects/)

Fonte das imagens:

- [Telefone sem fio](http://vidadesuporte.com.br/suporte-a-serie/telefone-sem-fio/)