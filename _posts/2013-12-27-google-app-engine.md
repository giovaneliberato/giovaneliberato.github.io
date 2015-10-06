---
layout: post
title: Python + App Engine
date: 27/12/2013
description: 'Aplicativos na nuvem do Google'
tags:
- python
- paas
- google app engine
twitter_text: 'Aplicativos na nuvem do Google'
---

Recentemente, meu amigo e mestre Renzo Nucciteli fez um post muito legal explicando por que ele é um prisioneiro feliz utilizando o Google App Engine, você pode ler [clicando aqui](http://blog.nuccitec.com.br/2013/12/google-app-engine-historia-de-um.html).

Comecei a trabalhar com desenvolvimento web + python a pouco mais de um ano apadrinhado pelo Renzo na startup [QMágico](http://www.qmagico.com.br). O QMágico é uma plataforma de educação inteligente que está no GAE.

Assim como o Renzo, me tornei um grande fã da plataforma por facilitar muito a vida do desenvolvedor. Neste tempo que estou no QMágico nunca tivemos que nos preocupar se o servidor iria aguentar ou se teríamos que montar um plano contra ataques DDOS (pelo contrário, o Google te da desconto se sua aplicação sofrer um ataque desses).

O Google App Engine é uma serviço do tipo PasS (Platform as a service), assim como o Heroku.

Atualmente, há três tipos de coisas as a service, como mostra a imagem abaixo.


![Cloud stack](/img/2013-12-27-google-app-engine/cloud_stack.gif)


Diferente dos serviços de cloud da Amazon, que é um IasS (Infrastructure as a service), ou do próprio QMágico, que é um SaaS (Software as a service), os serviços de PasS entregam ao desenvolvedor uma caixa preta, mas é uma caixa preta cheia de felicidade hehe.

O que eu quis dizer, é que nestes serviços o desenvolvedor não precisa se preocupar com infraestrutura, SO, escalonamento, balanceamento de carga e todas essas coisas que deixam os SysOps e SysAdmins sem sono. O desenvolvedor só precisa se preocupar com o código.

A principal característica das plataformas como serviço é que os desenvolvedores tem um ambiente facilmente configurável para desenvolver e disponibilizar suas aplicações. No GAE, por exemplo, pra subir uma aplicação configurada com python 2.7 só e preciso configurar o arquivo app.yaml do projeto, e pra mudar do python 2.7 pro 3.3 também é simples.


Porem, nem tudo é perfeito, ou como dizem na nossa área: "there's no silver bullet".

No QMágico, todos gostamos das facilidades do GAE, mas recentemente a aplicação começou a crescer e a demandar estratégias computacionais que eram muito difíceis de/não valiam a pena fazer no PasS da google, como gerenciamento de filas, processamento paralelo e o uso de diferentes tipos de banco de dados (o GAE usa somente seu banco nativo, o Big Table).

Deste modo, a equipe de engenheiros se viu de frente de um dilema: a facilidade ou a limitação? A resposta foi simples: os dois.

Não abandonamos o App Engine, seria muito difícil por causa do lock-in (coisa que o Renzo explica no post dele que eu mencionei no início). O que fizemos foi modularizar nosso produto em vários serviços, para que cada parte da aplicação rode no servidor mais eficiente para a tarefa.

Funciona assim: coisas que podem/conseguem rodar no GAE ficam la, coisas que precisam de um ambiente específico, como processamento paralelo, rodam em outros servidores e conversam entre sí através de APIs REST.

Assim conseguimos dividir as responsabilidades, modularizar a aplicação e ainda reutilizar os módulos para outros projetos.

Minha consideração final é: utilizem o Google App Engine (de preferência com python hahaha), ele é ótimo para aplicações pequenas e médias, e caso sua aplicação se torne grande ou tenha necessidades muito específicas, é possível contorná-las com um pouco de malandragem e experiência :)

Pra aprender mais e se tornar mais um prisioneiro feliz, acompanhe este curso do Renzo explicando todos os detalhes da plataforma e sua facilidade de integração com o python aqui: [Python + App Engine: Você programa e o google escala](https://www.youtube.com/watch?v=HYU5rO3trPc&list=PLA05yVJtRWYQMVMp9gFvaW2KZSpR_sZsH)


Por enquanto é isso pessoal, abraços!
