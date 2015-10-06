---
layout: post
title: Integrando go com Slack the easiest way
date: 10/08/2015
tags:
- Slack
- Go CI
- Continuous Integration
twitter_text: 'Integrando go com Slack the easiest way'
---

Continuous integration (CI) é um processo de desenvolvimento que permite as alterações sejam integradas o mais rápido possível, evitando problemas de integração como conflitos, repetição de código e commits gigantes, por exemplo.

Feedback rápido é o conceito chave de CI, e para conseguirmos isto de uma forma automatizada precisamos de ferramentas.

Existem várias no mercado como Jenkins, Travis, Hudson, etc.

<br>
Uma delas é o [Go Continuous Delivery](http://www.go.cd/), ferramenta open source desenvolvida pela ThoughtWorks que permite
automatizar os processos através de um pipeline, como mostra a figura abaixo.

![Go Pipeline](/img/2015-08-10-integrando-go-slack/go_pipeline.png)
<br><br>

Neste exemplo, todas as etapas foram executadas com sucesso... Mas e se alguma etapa falhar?

Aí é alerta vermelho! (sem trocadilhos)

Um build vermelho deve ser corrigido imediatamente. As estratégias possíveis são enviar um novo commit que corrige os erros do anterior ou desfazer as alterações que quebraram e resolvê-las sem a pressão de estar travando a ferramenta de CI.

Quando isso acontece, o time todo tem que ficar ciente e tomar alguma ação. É ai que entra o Slack.

O Slack é um poderosíssimo mensageiro com vários plugins e opcões de customização e que vem sendo adotado por várias equipes de desenvolvimento ágil.

<small>(Fun fact: O Slack é a empresa mais nova a chegar ao valuation de US$ 1 bi, demorando apenas 8 meses)</small><br><br>

O que torna o Slack tão fácil de integrar é o serviço de [Incoming Webhooks](https://api.slack.com/incoming-webhooks), que permite publicar postagens no chat apenas efetuando um POST request pra uma URL única gerada pela api.

<br>

<b>DISCLAIMER</b>: Há um plugin para o Go de integração com o slack, mas que depende de muitas configurações em ambos os lados. [https://github.com/ashwanthkumar/gocd-slack-build-notifier/releases](https://github.com/ashwanthkumar/gocd-slack-build-notifier/releases)

<br>

Dados os conceitos, vamos ao passo a passo.

<br>

#### Parte 1 - Configurando o Slack

1\. Tenha um board no [Slack](https://slack.com) e acesse \<seu-board\>.slack.com/services/new/incoming-webhook

2\. Crie um novo webhook no canal do Slack que desejar

![Slack selecionar channel](/img/2015-08-10-integrando-go-slack/slack_create_webhook.png)

3\. Customize

Aqui, é possível editar o canal de envio e até criar um avatar diferente para o bot que enviará suas mensagens.

![customizar bot](/img/2015-08-10-integrando-go-slack/slack_configure_bot.png)

Depois de editar, é só salvar as alteracões e copiar sua URL para usarmos no GO.

<br><br>

#### Parte 2 - Configurando o GO

1\. Acesse o painel de configurações do seu pipeline

Aqui você pode adicionar uma nova task e associá-la ao status do processo (sucesso, falha ou ambos)

![painel de configuração do go server](/img/2015-08-10-integrando-go-slack/painel-de-config-job.png)

<br>

2\. Adicione job tasks

Selecione curl no campo "Lookup Commands" e preencha os campos da sequinte forma. É muito importante <b>incluir apenas um parâmetro por linha</b>.

curl -X POST --data-urlencode "payload={\"text\": \"Build is GREEN! Uhuull.\"}" <your-url>

![adicionar task ao job](/img/2015-08-10-integrando-go-slack/adicionar-nova-task.png)
<br><br>

Adicione também uma task que é executada quando o job falha. Você pode fazer isso manualmente alterando o texto ou [usando um script](https://gist.github.com/giovaneliberato/2a8ecb9b8f107f3eaf22) que alterna a mensagem dada uma flag de status.

<br><br>

#### Parte 3 - Enjoy

Depois disso, é só esperar o próximo processo de build ser disparado e receberá o status no seu channel do Slack.

![Bot nofiticando slack](/img/2015-08-10-integrando-go-slack/bot-notificacao.png)

<br>
Caso hajam muitas mensagens, também é valido criar um canal exclusivo para estas notificações e ativar as [notificações de desktop](https://slack.zendesk.com/hc/en-us/articles/201355156-Desktop-notifications)

<br>

Espero que o artigo tenha sido útil, abraços e obrigado pela leitura!
