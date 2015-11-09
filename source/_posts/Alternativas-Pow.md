title: 'Alternativas: Pow'
tags:
  - automatização
  - ruby on rails
categories:
  - Alternativas
date: 2015-11-09 08:10:00
---
Se você é um desenvolvedor Ruby e usa um Mac, há uma grande possibilidade de você já ter usado o [Pow](http://pow.cx/). Mas caso você não conheça, o Pow é um servidor [Rack](http://rack.github.io/) para Mac OS X de configuração zero (ou mínima, pelo menos), que permite que você sirva seus apps Rack localmente pela url `http://<seu_app>.dev` em questão de minutos.

Uma das fraquezas do Pow é o fato de ele ser disponível somente para Mac OS X, e se você tem usuários Linux no seu time e o seu app necessita do Pow no ambiente de desenvolvimento isso pode ser um impedimento. É por isso que post visa justamente oferecer alternativas ao Pow, para você que usa outro sistema operacional!

<img src="/img/posts/logo-pow.png"/>

<!-- more -->

Se você usa Linux, pode até afirmar que consegue fazer o que o Pow faz simplesmente usando o `/etc/hosts`. Mas como lidar com _port forwarding_? Múltiplos apps? Além do mais, não é nada prático ficar editando este arquivo quando você pode simplesmente usar algo que funciona como o Pow, não é? Bom, para sua supresa, existe algo assim para Linux, o [Prax](https://github.com/ysbaddaden/prax)!

### Prax

O Prax funciona _quase_ que como o Pow, porém ele é implementado em Ruby puro. Ele tem uma instalação também bem prática, nada de complicações de editar o arquivo de _hosts_ nem nada do tipo.

Você notará que no próprio [site do Prax](http://ysbaddaden.github.io/prax/) existe uma mini-documentação, porém eu sugiro que, caso for instalá-lo, siga aqui pelo blog, pois a documentação no site está incompleta, e o que vou falar aqui é baseado em algumas respostas de _issues_ do repositório.

Para instalar o Prax você primeiramente deve ter o Ruby instalado (vale Ruby "normal", RVM, Rbenv, entre outros, entraremos neste assunto daqui a pouco). Depois de conferir se o Ruby está instalado na sua máquina, rode os seguintes comandos:

```sh
$ sudo git clone git://github.com/ysbaddaden/prax.git /opt/prax
$ /opt/prax/bin/prax install
```

Pronto, o Prax já está instalado :)

### Configurando para gerenciadores de versão

Se você usa algum gerenciador de versão do Ruby, na wiki do Prax há um [guia de configuração](https://github.com/ysbaddaden/prax/wiki/Ruby-Version-Managers) para o chruby, rbenv, RVM e ry.

### Apontando para seu app

Agora você só precisa configurar para que o Prax aponte para o seu app. Você pode fazer de duas maneiras:

#### App rodando na porta 80

Se o seu app roda na porta 80, você não precisará avisar que porta ele se encontra para o Prax, basta rodar o seguinte comando dentro da pasta do seu app:

```sh
$ prax link # linka seu app ao Prax, mais fácil que usar o `ln` com o Pow ;)
$ prax start # inicia o Prax
```

#### App rodando em outra porta

Se o seu app roda em alguma porta diferente, você precisará avisar isso ao Prax de uma outra maneira (lembrando: __não__ é necessário fazer o passo que configura para a porta 80). Basta entrar na pasta do seu app e rodar:

```sh
$ echo <porta_do_seu_app> > ~/.prax/<nome_do_seu_app> # avisa o Prax sobre a porta
$ prax start # inicia o Prax
```

Esta segunda parte não se encontra na documentação, mas pode ser encontrada no [issue #11](https://github.com/ysbaddaden/prax/issues/11) do repositório do Prax. Repare que aqui o funcionamento é _idêntico_ ao do Pow.

### Port para linguagem Crystal

O autor do Prax também possui um port dele para a linguagem Crystal, o [Prax.cr](https://github.com/ysbaddaden/prax.cr), pode ser interessante caso você tenha passado por algum problema de configuração do Ruby, já que a linguagem Crystal é compilada.

### Bam

Existe uma outra alternativa, que alega funcionar inclusive tanto no Linux, quanto no Windows (ou quase) e no Mac OS X, chamado [Bam](https://github.com/jweslley/bam). Este não vou fazer uma análise porque não cheguei a usar, mas se você já usou e tem algo a dizer sobre, sinta-se livre para comentar ali em baixo.

### Conclusão

Bom, é isso, pessoal. Há de se concordar que o Prax não é uma alternativa 100% ao Pow, mas posso garantir por experiência própria que ele dá conta do recado na maioria dos casos! Caso conhecer alguma outra alternativa ao Pow, basta comentar ali em baixo :D