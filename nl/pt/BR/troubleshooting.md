---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

subcollection: discovery

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# FAQs
{: #faqs}

Perguntas mais freqüentes sobre o serviço do  {{site.data.keyword.discoveryshort}} .

## Posso fazer upload de matrizes JSON?
{: #array}
{: faq}

É possível fazer upload de uma matriz JSON, mas cada seção deve ser transferida por upload individualmente. Por exemplo, o JSON a seguir não pode ser transferido por upload para o serviço:

```json
[{
  "accepted": 1, "answer": "Não deve haver nenhum problema para mantê-lo ligado o tempo todo, no entanto, deve-se considerar qualquer contador que você possa ter como o uso do código millis. Dos documentos do Arduino em milis, este número voltará a ser zero após aproximadamente 50 dias. citação de bloco - Então, para projetos que estão ativos por longos períodos de tempo, talvez um problema não seja visto imediatamente, mas algo assim pode aparecer e causar erros no caminho. ", "answerScore": "49", "authorUserId": "3", "authorUsername": "Butzke", "downModVotes": 0, "id": 2, "subtitle": "Estou criando um servidor da web Arduino simples e quero mantê-lo ligado o tempo todo. Então, ele deve aguardar para continuar trabalhando continuamente. Estou usando um Arduino Uno com uma blindagem Ethernet. Ele é alimentado com uma fonte de alimentação de saída simples 5V 1A. Minhas perguntas - Tenho problemas para deixar o Arduino ligado o tempo todo? li - Existe alguma outra placa do Arduino melhor recomendada para isso? li - Existem precauções que devo ter em relação a isso? li ul ", "tags": "<arduino-uno><web-server><ethernet>", "title": "Um Arduino é capaz de ser executado 24 horas por dia, sete dias por semana?",
      "upModVotes": 49,
      "userId": "11",
      "userReputation": 4535,
      "username": "sachleen",
      "views": 3234
}, {
  "accepted": 0, "answer": "Além da menção de Sachleen a Milli, que afirma que qualquer calor de eletroeletrônico pode ser perturbador. Não é provável que o micro controlador em si seja um problema enorme da perspectiva do calor, mas outros componentes, como a fonte de alimentação, podem causar problemas. li - Se o código usa EEPROMWrite, o EEPROM é classificado apenas para algo em torno de 100 mil gravações. li ul ", "answerScore": "24", "authorUserId": "3", "authorUsername": "Butzke", "downModVotes": 0, "id": 3, "subtitle": "Estou criando um servidor da web Arduino simples e quero mantê-lo ligado o tempo todo. Então, ele deve aguardar para continuar trabalhando continuamente. Estou usando um Arduino Uno com uma blindagem Ethernet. Ele é alimentado com uma fonte de alimentação de saída simples 5V 1A. Minhas perguntas - Tenho problemas para deixar o Arduino ligado o tempo todo? li - Existe alguma outra placa do Arduino melhor recomendada para isso? li - Existem precauções que devo ter em relação a isso? li ul ", "tags": "<arduino-uno><web-server><ethernet>", "title": "Um Arduino é capaz de ser executado 24 horas por dia, sete dias por semana?", "upModVotes": 24, "userId": "13", "userReputation": 489, "username": "Matthew G.",
      "views": 3234
}]
```
{: codeblock}

Para fazer upload dessas informações para o serviço, divida a matriz e faça upload de cada seção
como segue:

Seção 1:

```json
{
  "accepted": 1, "answer": "Não deve haver nenhum problema para mantê-lo ligado o tempo todo, no entanto, deve-se considerar qualquer contador que você possa ter como o uso do código millis. Dos documentos do Arduino em milis, este número voltará a ser zero após aproximadamente 50 dias. citação de bloco - Então, para projetos que estão ativos por longos períodos de tempo, talvez um problema não seja visto imediatamente, mas algo assim pode aparecer e causar erros no caminho. ", "answerScore": "49", "authorUserId": "3", "authorUsername": "Butzke", "downModVotes": 0, "id": 2, "subtitle": "Estou criando um servidor da web Arduino simples e quero mantê-lo ligado o tempo todo. Então, ele deve aguardar para continuar trabalhando continuamente. Estou usando um Arduino Uno com uma blindagem Ethernet. Ele é alimentado com uma fonte de alimentação de saída simples 5V 1A. Minhas perguntas - Tenho problemas para deixar o Arduino ligado o tempo todo? li - Existe alguma outra placa do Arduino melhor recomendada para isso? li - Existem precauções que devo ter em relação a isso? li ul ", "tags": "<arduino-uno><web-server><ethernet>", "title": "Um Arduino é capaz de ser executado 24 horas por dia, sete dias por semana?",
      "upModVotes": 49,
      "userId": "11",
      "userReputation": 4535,
      "username": "sachleen",
      "views": 3234
}
```
{: codeblock}

Seção 2:

```json
{
  "accepted": 0, "answer": "Além da menção de Sachleen a Milli, que afirma que qualquer calor de eletroeletrônico pode ser perturbador. Não é provável que o micro controlador em si seja um problema enorme da perspectiva do calor, mas outros componentes, como a fonte de alimentação, podem causar problemas. li - Se o código usa EEPROMWrite, o EEPROM é classificado apenas para algo em torno de 100 mil gravações. li ul ", "answerScore": "24", "authorUserId": "3", "authorUsername": "Butzke", "downModVotes": 0, "id": 3, "subtitle": "Estou criando um servidor da web Arduino simples e quero mantê-lo ligado o tempo todo. Então, ele deve aguardar para continuar trabalhando continuamente. Estou usando um Arduino Uno com uma blindagem Ethernet. Ele é alimentado com uma fonte de alimentação de saída simples 5V 1A. Minhas perguntas - Tenho problemas para deixar o Arduino ligado o tempo todo? li - Existe alguma outra placa do Arduino melhor recomendada para isso? li - Existem precauções que devo ter em relação a isso? li ul ", "tags": "<arduino-uno><web-server><ethernet>", "title": "Um Arduino é capaz de ser executado 24 horas por dia, sete dias por semana?", "upModVotes": 24, "userId": "13", "userReputation": 489, "username": "Matthew G.",
      "views": 3234
}
```
{: codeblock}
