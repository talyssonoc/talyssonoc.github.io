title: Porque críticas e code review são importantes?
tags:
  - code review
categories:
  - Porque é importante?
date: 2016-01-12 20:07:00
---
Você já parou pra pensar o quão importante é ter pessoas no seu projeto criticando e revisando seu código? Te apontando possíveis problemas e melhoras que talvez você não tenha conseguido ver quando escreveu? Já xingou o código de um projeto legado sem pensar que talvez uma maneira de melhorá-lo seja aumentar o _code review_?

Acontecimentos recentes me fizeram ficar pensando neste fato, com coisas que aconteceram comigo mesmo, e então resolvi fazer este post como uma reflexão sobre o assunto: a importância de críticas e _code reviews_, além de saber _lidar_ com as críticas e não levar para o lado pessoal.

<img src="https://davidwalsh.name/demo/code-review.png"/>

<!-- more -->

### Esfriando a cabeça

Atualmente estou trabalhando num projeto que possui bastante código legado, código que já passou pela mão de vários desenvolvedores, principalmente o front-end. Como todo código legado, há a tendência de encontrar uma certa quantidade de código não muito agradável, e isso por vezes me irrita, e me pego pensado "como foi que isso passou na revisão?!".

Depois de me espantar com esse tipo de coisa, tomei como uma missão pra mim passar a comentar mais em PRs ([_pull requests_](https://help.github.com/articles/using-pull-requests/)) que eu veja código propenso a problemas, para que, no futuro, quem mexer no código não passe pela mesma situação que eu.

As semanas passaram, e eis que recentemente uma PR minha foi bastante comentada, principalmente os códigos que envolviam back-end dela. E cada vez que eu arrumava algo, surgiam novas críticas, algumas mudanças que, pra mim, não faziam muito sentido, ou eram irrelevantes para a qualidade do código. E, posso dizer, isso também me irritou. Curioso, não?

Pois é, após ficar pensando porque tantos comentários, imaginando o que é que eu não estava enxergando de problema no código, cheguei a conclusão: os autores dos comentários tinham a mesma intenção que eu quando decidi ser mais ativo nos comentários para gerar códigos melhores, e se eu "desobedecesse" às sugestões eu só estaria gerando mais código ruim para o futuro, e talvez tenha sido isso o que aconteceu aos códigos que me irritaram anteriormente.

E foi o que me fez esfriar a cabeça quanto a isso, e talvez seja o que você deva fazer também quando comentários em seus códigos te irritatem.

### Criando o costume

Acho que pelo item anterior você já pode sacar o porque de ser importante revisar e criticar código, não é?

É importante também criar o costume, a cultura, de revisar código no seu projeto, na sua empresa, nos seus códigos open-source, entre outros!

Para que isso funcione um dos passos essenciais é trabalhar com algum sistema de gerenciamento de versão e revisão, como o [Git](https://git-scm.com/), [Subversion](https://subversion.apache.org/), ou [Mercurial](https://www.mercurial-scm.org/), sendo o Git o mais conhecido deles. Este tipo de gerenciador permite que você crie "galhos" nas versões do seu código, tornando possível que programadores diferentes trabalhem com partes diferentes do código (ou até a mesma) sem que as mudanças de um afete o ambiente do outro, de modo que, quando alguém for revisar o seu código, ele consiga analisar isoladamente suas mudanças. O [Git Flow](http://danielkummer.github.io/git-flow-cheatsheet/) é um exemplo de como trabalhar seguindo este esquema.

Após a adoção de uma ferramenta assim, usá-la corretamente e de suma importância, e com o tempo você colherá os frutos tendo códigos melhores.

É importante lembrar a equipe de que isso não é uma burocracria criada para enrolar o projeto, e sim um filtro que permite diminuir a quantidade de bugs e códigos ruins que entrarão na _code base_ principal.

### Não seja um idiota

Emprestando o tempo usado como título de códigos de condutas de conferências, a regra também deve se aplicar quando você está tenso seu código revisado/criticado ou revisando/criticando: não seja um idiota.

Inicialmente, que fique claro que não passei por nada do tipo em projetos recentes.

Evite agir como o [Linus Torvalds](http://lkml.iu.edu/hypermail/linux/kernel/1510.3/02866.html) nos comentários, tente entender a perspectiva da outra pessoa, e tenha em mente que, esteja você criticando ou sendo criticado, a ideia é sempre melhorar o código e seguir um padrão, e não forçar gostos pessoais.

Se você não concorda (completa ou parcialmente) com a mudança sugerida, debata o caso de forma civilizada, não ignore nem seja _agressivo_ falando que algo não faz sentido, ou que a pessoa está mais atrapalhando do que ajudando. Muitos programadores tendem a levar para o lado pessoal quando tem seus códigos criticados, quando não notam que isso na verdade é uma ótima oportunidade para se aprender mais sobre o projeto e sobre desenvolvimento em geral.

Se acha que está certo, tente provar seu ponto, comente com links, pesquisas de performance, ou qualquer coisa que passe confiança, nada de "porque do outro jeito é melhor" ou "eu não gosto de código deste jeito".

### O código, não você

E, por fim, é importante lembar que o que está sendo criticado é o código, não você. Raramente haverá comentários de cunho pessoal. A única coisa que te afetará é que, caso você aprenda algo com os comentários, não só o código melhorará, como você também. Então tente não esquentar com isso!

Fonte das imagens:

- [Code review](https://davidwalsh.name/code-review)