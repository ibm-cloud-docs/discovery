---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Atualizando seu plano
{: #upgrading-your-plan}

O serviço do {{site.data.keyword.discoveryfull}} oferece três planos que fornecem diferentes níveis de recursos e de capacidades para atender às suas necessidades.
{: shortdesc}

Veja [Planos de precificação do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/pricing-details.html) e [Catálogo do {{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} para obter detalhes.

## Atualizando seu serviço
{: #service} 

Para redimensionar seu plano de Lite para Avançado:

1. Abra o [{{site.data.keyword.Bluemix_notm}} painel](https://console.{DomainName}/dashboard). 
1. Clique em sua instância de serviço do {{site.data.keyword.discoveryshort}} para abrir o painel de serviço do {{site.data.keyword.discoveryshort}}.
1. Na página **Gerenciar** de seu serviço {{site.data.keyword.discoveryshort}}, clique em **Fazer upgrade** para escolher o plano Avançado. Isso abrirá a página  ** Plan ** . Siga as etapas para concluir seu upgrade. 
1. Retorne para a página **Gerenciar** e clique em **Ativar ferramenta** para abrir o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.
   - Se você nunca tiver criado um ambiente para seu plano Lite antes do upgrade para Avançado, clique no ícone ![Cog](images/icon_settings.png) e escolha **Criar ambiente**. Uma tela exibirá as opções para seu plano Avançado. Escolha a que se ajusta às suas necessidades. (`X-Small`, `Small`, `Medium-Small`, `Medium`, `Medium-Large`, `Large`, `X-Large`, `XX-Large`).
   - Se você tiver criado um ambiente para seu plano Lite antes do upgrade para Avançado, seu novo ambiente de plano Avançado será `Small` por padrão. 

## Alternando de uma camada Avançado para outra
{: #advanced} 

Se você já tiver um plano Avançado e desejar fazer upgrade dele para um tamanho de plano maior, será possível fazer isso usando a [API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#update-environment){: new_window}. 

Para obter informações detalhadas sobre os limites de armazenamento do plano Avançado e a precificação, veja [Planos de precificação Avançado](/docs/services/discovery/pricing-details.html#advanced).

É possível fazer upgrade de seu tamanho de plano Avançado, mas não é possível reduzir para um tamanho menor. Os tamanhos de plano avançados disponíveis são: 

Tamanho do plano | Etiqueta  
--------- | ------ 
Extra-Pequ | XS 
Pequeno | S 
Médio-Pequeno | MS 
Médio | M 
Médio-Grande | ML 
Grande | L
Extra-Grande | XL 
XX-Grande | XXL 

- A consulta e a indexação podem continuar durante o upgrade. O tempo necessário para fazer upgrade depende de uma série de fatores. É possível pesquisar seu ambiente usando a API enquanto o upgrade é concluído.
- Mover de um nível de Avançado para outro não requer a criação de novas instâncias. 
- Uma vez concluído o upgrade, você será faturado na nova taxa do plano.

## Atualizando para um plano Premium
{: #premium}

Se você estiver interessado em um plano Premium, entre em contato com [Vendas](https://ibm.biz/contact-wdc-premium).  
