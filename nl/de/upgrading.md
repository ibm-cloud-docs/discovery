---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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

# Upgrade Ihres Plans durchführen
{: #upgrading-your-plan}

Der {{site.data.keyword.discoveryfull}}-Service bietet drei Pläne, die für Sie je nach Bedarf verschiedene Ebenen von Ressourcen und Funktionalität bereitstellen.
{: shortdesc}

Weitere Informationen finden Sie unter [Preisstrukturpläne für {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) und im [{{site.data.keyword.discoveryshort}}-Katalog ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/catalog/services/discovery){: new_window}.

## Upgrade für Ihren Service durchführen
{: #service}

Gehen Sie wie folgt vor, um ein Upgrade Ihres Plans von Lite auf Advanced durchzuführen:

1. Öffnen Sie das [{{site.data.keyword.Bluemix_notm}}-Dashboard](https://{DomainName}/dashboard). 
1. Klicken Sie auf Ihre {{site.data.keyword.discoveryshort}}-Serviceinstanz, um die Dashboardseite des {{site.data.keyword.discoveryshort}}-Service zu öffnen.
1. Klicken Sie auf der Seite **Verwalten** Ihres {{site.data.keyword.discoveryshort}}-Service auf **Upgrade**, um den Advanced-Plan auszuwählen. Hierdurch wird die Seite **Plan** geöffnet. Führen Sie die Schritte aus, um das Upgrade abzuschließen. 
1. Kehren Sie zur Seite **Verwalten** zurück und klicken Sie auf **Tool starten** , um das {{site.data.keyword.discoveryshort}}-Tool zu öffnen.
   - Wenn Sie vor dem Upgrade auf Advanced noch keine Umgebung für Ihren Lite-Plan erstellt haben, klicken Sie auf das Symbol ![Cog](images/icon_settings.png) und wählen Sie die Option **Umgebung erstellen** aus. In einer Anzeige werden die Optionen für den Advanced-Plan angezeigt. Wählen Sie die für Ihre Bedürfnisse passenden Optionen aus  (`X-Small`, `Small`, `Medium-Small`, `Medium`, `Medium-Large`, `Large`, `X-Large`, `XX-Large`).
   - Wenn Sie vor dem Upgrade auf Advanced eine Umgebung für Ihren Lite-Plan erstellt haben, ist Ihre neue Advanced-Plan-Umgebung standardmäßig `Small`. 

## Wechsel von einer Advanced-Preisstufe zu einer anderen
{: #switchadvanced} 

Wenn Sie bereits über einen Advanced-Plan verfügen und ein Upgrade auf eine größere Plangröße durchführen möchten, können Sie dies über die [API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery#update-an-environment){: new_window} tun. 

Ausführliche Informationen zu Speichergrenzwerten und Preisen für den Advanced-Plan finden Sie unter [Advanced-Preisstrukturpläne](/docs/services/discovery?topic=discovery-discovery-pricing-plans#advanced).

Folgenden Größen für Advanced-Pläne sind verfügbar: 

Plangröße | Bezeichnung  
--------- | ------ 
X-Small | XS 
Small | S 
Medium-Small | MS 
Medium | M 
Medium-Large | ML 
Large | L
X-Large | XL 
XX-Large | XXL 

- Das Abfragen und Indexieren kann während des Upgrades fortgesetzt werden. Die für das Upgrade erforderliche Zeit hängt von einer Reihe von Faktoren ab. Sie können Ihre Umgebung unter Verwendung der API abfragen, während das Upgrade ausgeführt wird.
- Wenn Sie von einer Stufe von Advanced zu einer anderen wechseln, müssen Sie keine neuen Instanzen erstellen. 
- Sobald das Upgrade abgeschlossen ist, wird Ihnen die neue Planrate in Rechnung gestellt.
- Wenn Sie später feststellen, dass Sie eine kleinere Plangröße benötigen, sollten Sie die entsprechende Plangröße definieren, Ihre Daten migrieren und dann den größeren Plan stornieren. 

## Upgrade auf einen Premium-Plan durchführen
{: #premium}

Wenn Sie Interesse an einem Premium-Plan haben, wenden Sie sich an den [Vertrieb](https://ibm.biz/contact-wdc-premium).  
