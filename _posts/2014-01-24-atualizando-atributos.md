---
layout: post
title: Atualizando atributos de forma genérica
date: 27/01/2014
description: 'Usando métodos built-in para abstrair classes'
tags:
- python
- OO
twitter_text: 'Atualizando atributos de forma genérica em python'
---

Uma das coisas coisas que mais tem me encantado (e desafiado) ultimamente na hora de programar é escrever o código da maneira mais elegante e reutilizável possível e isso requer algum conhecimento de engenharia de software e principalmente conhecimento das "mágicas" que a sua linguagem de programação proporciona.

Meu mais recente desafio foi escrever uma função em python que atualiza um objeto sem conhecer seu tipo. Assim, seria possível reutilizar a função para qualquer objeto, independente de seus atributos.

<br>
<strong>EDIT</strong>: O Danilo Bellini indicou alguns erros e eu efetuei as devidas correções. O método <strong>getattr</strong> foi substituido pelo <strong>hasattr</strong> e a chamada de função <strong>update_obj(a, values)</strong> foi substituida por <strong>update_obj(a, \*\*values)</strong>.
Pra ver as explicações do Danilo é só acessar o tópico que eu criei no grupo Python Brasil no facebook [clicando aqui](https://www.facebook.com/groups/python.brasil/permalink/471425519628990/?stream_ref=2) e você pode ver a versão original deste post [clicando aqui](https://github.com/giovaneliberato/giovaneliberato.github.io/blob/eb3e7ff840c046561e749790b9c6a43b4afab98c/_posts/2014-01-24-atualizando-atributos.md)

<br>
Pra exemplificar, vou mostrar como seria a primeira abordagem. Vamos usar como base duas classes: Pessoa e Animal.

<br>
{% highlight python linenos %}
    class Pessoa(object):
        def __init__(self):
            self.nome = ''
            self.idade = 0


    class Animal(object):
        def __init__(self):
            self.nome_cientifico = ''
            self.peso = 0.0
{% endhighlight %}
<br>

No exemplo acima, temos duas classes diferentes com atributos diferentes.
Caso fosse preciso atualizar estes objetos o jeito mais "bronco" seria mudar estes atributos na mão, deste jeito:

<br>
{% highlight python linenos %}
    p = Pessoa()
    p.nome = 'Giovane'
    p.idade = 21
    # salva objeto 'p' no banco

    a = Animal()
    a.nome_cientifico = "Gorilla gorilla gorilla"
    a.peso = 620.0
    # salva objeto 'a' no banco

{% endhighlight %}
<br>


Isto pode não parecer muito difícil com estes exemplos, mas se imaginarmos um banco de uma aplicação média/grande, teremos dezenas de tabelas e modelos com 5 atributos (em média) cada um e estas linhas de atribuição começam a crescer e crescer cada vez mais.

Minha solução pra este problema foi criar uma função totalmente independente do tipo do objeto, com a única missão de atualizar atributos e isso só foi possível através de métodos built-in do python <strong>hasattr</strong> e <strong>setattr</strong>.

<br>
De acordo com a documentação oficial do python, as definições destes métodos são as seguintes:

<h4>hasattr</h4>
<blockquote>
    Os argumentos são um objeto e uma string. O resultado é verdadeiro se a string for o nome de um dos atributos do objeto e False se não. (Isso é implementado chamando getattr(objeto, nome) e verificando se a execução gera um AttributeError ou não.)
</blockquote>


<br>
<h4>setattr</h4>
<blockquote>
    [..] Os argumentos são um objeto, uma string e um valor qualquer. Este string pode ser um atributo existente no objeto um novo atributo. A função atribui o valor para a variável, desde que o objeto permita. Por exemplo, setattr(x, 'foobar', 123) é equivalente a x.foobar = 123.
</blockquote>

<br>

Com estes métodos em mão, é possível criar uma função de 4 linhas que atualiza qualquer objeto, deste jeito:

{% highlight python linenos %}
    def update_obj(obj, **kwargs):
        for attr, value in kwargs.items():
            if hasattr(obj, attr):
                setattr(obj, attr, value)
{% endhighlight %}
<br>

Nesta função, recebemos um parâmetro identificado pelos dois asteriscos, também conhecido como kwargs (keyword args). Assim, podemos invocar a função passando um dicionário ou atributos nomeados.

Em seguida, iteramos sobre o dicionário de atributos a serem atualizados e verificamos se aquele objeto possui determinado atributo. A 3ª linha desta função lançaria uma exceção caso o valor False não fosse passado como parâmetro default, neste caso o programa só não entra no if.

Por ultimo, utilizamos o setattr para atualizar o valor de determinado atributo do objeto.

<br>
Um exemplo de utilização:

{% highlight python linenos %}
    class Pessoa(object):
        def __init__(self):
            self.nome = ''
            self.idade = 0


    class Animal(object):
        def __init__(self):
            self.nome_cientifico = ''
            self.peso = 0.0


    def update_obj(obj, **kwargs):
        for attr, value in kwargs.items():
            if hasattr(obj, attr, False):
                setattr(obj, attr, value)

    p = Pessoa()
    # funciona passando parâmetros nomeados
    update_obj(p, nome="giovane", idade=21)

    a = Animal()
    values = {
        'nome_cientifico': 'Gorilla gorilla gorilla',
        'peso': 620.0
    }
    # e também passando um dicionário como parâmetro (utilizando os asteriscos para indicar que é um dicionário de parâmetros)
    update_obj(a, **values)

{% endhighlight %}
<br>


Este é um código muito simples mas que traz uma economia gigante no tempo de desenvolvimento e manutenção. Guarde e use assim que possível, vai te livrar de muitas linhas de código.


ps: A lista completa de métodos built-in do python esta [disponível aqui](http://docs.python.org/2/library/functions.html)

ps2: Agora meu blog tem um fórum powered by disqus, qualquer dúvida ou sugestão é só comentar abaixo ;D
