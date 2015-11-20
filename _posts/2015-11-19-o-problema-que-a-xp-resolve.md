---
layout: post
title: O problema que a XP resolve 
date: 19/11/2015
description: ''
tags:
- Agile
- metodologias
- eXtreme Programming
---

Provavelmente você já foi apresentado ao modelo de desenvolvimento de software em cascata. Seja nas aulas da faculdade ou em alguma conferência, sempre haverá alguém criticando o modelo. Esse discurso geralmente vem acompanhado do que parece ser a solução de todos os problemas do desenvolvimento: metodologias ágeis.

O modelo cascata foi herdado da construção civil. O entravamento do processo se da ao grande custo de uma mudança depois que a execução do projeto começava. Se eu fosse o engenheiro de algum projeto eu certamente não ia querer descobrir que tem algum cálculo errado depois que o cimento já secou. Felizmente, isso não é uma verdade para a programação.

Em um campo tão dinâmico como a criação de softwares/produtos, ter espaço e flexibilidade para manobrar é um recurso indispensável para atingir resultados positivos durante o trajeto.

Muito se fala de como implementar agile, sprints, iterações, TDD e todas as outras coisas que separam as pessoas descolados das demais, mas afinal: por que metodologias ágeis (nesse caso, a XP)? 

A resposta é simples: **gerenciamento de riscos**.

_- Tá, mas esse também é o problema que a modelo cascata resolve, não?_

Sim! A diferença está no custo das alterações em diferentes etapas do processo. Diferente do cimento, o código é flexível e alterações são simples de executar.

Se com rigidez nas mudanças o custo aumento, o inverso também é verdade. As alterações no código não crescem exponencialmente ao longo do tempo se compactarmos as etapas de análise, desenvolvimento e teste em pequenos ciclos.

A XP (programação extrema ou _eXtreme programming_) oferece uma série de recursos que nos possibilita ser **flexíveis à mudanças, errar barato, analizar e aprender**.

![Modelo tradicional vs. Modelo Ágil](/img/2015-11-19-o-problema-que-a-xp-resolve/agile_cascade.gif)


Existem excelentes livros sobre programação extrema e seria muito ingênuo da minha parte tentar cobrir tudo em um blog post. Irei abordar os quatro que mais me chamaram a atenção.

**Simplicidade**

Fazer o simples é muito mais difícil do que parece e tentar antecipar mudanças é uma reação natural. Porém, se levarmos em consideração o custo de uma mudança na XP, postergar decisões o máximo possível e agir nelas quando realmente for necessário pode ser uma opção. O que é um problema hoje pode não ser amanhã.

Luciano ramalho disse no livro Fluent Python: "Premature abstraction is as bad as premature optimization."


**Feedback**

Aprender com os erros é essencial, mas pra isso precisamos saber quando estamos errando. Se conseguirmos agir sobre os erros cedo, menores serão as consquências. Por isso é preciso ter ferramentas que nos ajudem a saber quando estamos errando no código, quando estamos errando com os clientes, quando estamos errando como equipe, etc.

Uma analogia possível é dirigir um carro. Você faz alterações pequenas e frenquetes ao invés de alterações grandes, sempre atento ao feedback para não sair da pista.


**Comunicação**

No livro[1] XP explicada, Kent Beck destaca a importância da comunicação com a seguinte frase:

> _Quando analisamos os problemas que ocorreram nos projetos, vemos que muitos deles foram provocados por alguém que não conversou com outro alguém sobre alguma coisa importante._

A XP propõe diversas práticas que só serão possíveis com boa comunicação. Pareamento(para programar e para outras atividades), integração contínua, ambientes compartilhados, etc. É muito importante que a comunicação seja clara, transparente e esteja disponível para todos membros da equipe. 


**Equipe**

Para mim, equipe é o item mais importante. A equipe deve ser incluida em todas as etapas de um projeto, pois são quem implementamo que foi planejado. Participando do planejamento, a equipe pode negociar o escopo da tarefa quando achar necessário e sugerir alternativas técnicas para as novas features.

Outro ponto importante é Manter uma cultura de feedback entre os membros da equipe. Confiança e transparência são essenciais para que quando as noticías não tão boas chegarem o possa agir e resolver os desafios juntos.
Feedback, simplicidade, comunicação e equipe


<br>
Guiado por esses e outros mais valores da XP, o desenvolvimento de software se torna algo menos burocrático, mais prazeroso e produtivo. Sempre lembrando que nenhuma destas práticas estão escritas na pedra. O importante é o evoluir da forma que mais se encaixe no seu contexto.


[1] - "Programação eXtrema(XP) explicada", escrito por Kent Beck e publicado pela Bookman.
