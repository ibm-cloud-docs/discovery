---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# Traitement des incidents

Astuces relatives au traitement des incidents liés à l'utilisation du service {{site.data.keyword.discoveryshort}}.

Si vous rencontrez des problèmes lors de l'utilisation du service {{site.data.keyword.discoveryshort}}, essayez une ou plusieurs des astuces décrites ci-après pour identifier et résoudre ces problèmes. 

-   L'ingestion d'un document peut échouer en raison d'une non-concordance de type entre les données présentes dans les document en cours et des données similaires présentes dans un document déjà versé. Par exemple, une zone peut être du type **date** dans un document et être du type **string** dans un document suivant, ce qui empêche l'indexation de ce dernier. 

    L'opération de prévisualisation ne peut pas prédire les non-concordances de type car elle teste uniquement un document et ne conserve aucune trace des résultats de conversion.
-   Les indexations rapides ou à grande échelle de documents peuvent parfois entraîner le redémarrage du service de recherche dorsal. Si cela se produit, demandez de l'aide auprès du support {{site.data.keyword.IBM}}. 
