---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-08"

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

# Intégration à Watson Knowledge Studio

Vous pouvez intégrer un modèle personnalisé à partir de {{site.data.keyword.knowledgestudiofull}} au service {{site.data.keyword.discoveryshort}} afin de fournir des enrichissements d'entité et de relations personnalisés.
{: shortdesc}

Vous avez ainsi la possibilité d'appliquer les fonctions d'amélioration de document du service {{site.data.keyword.discoveryshort}} avec des informations propres à certains domaines, tels qu'un secteur d'activité ou une discipline scientifique. Vous pouvez utiliser à la fois des données publiques et vos propres données exclusives dans votre modèle d'enrichissement.

Vous pouvez utiliser l'API de service ou les outils {{site.data.keyword.discoveryshort}} pour intégrer un modèle {{site.data.keyword.knowledgestudioshort}} au service {{site.data.keyword.discoveryshort}}.

## Avant de commencer

Avant de pouvoir intégrer un modèle personnalisé à partir de {{site.data.keyword.knowledgestudioshort}} au service {{site.data.keyword.discoveryshort}}, vous devez créer et déployer le modèle à l'aide de {{site.data.keyword.knowledgestudioshort}}. Pour plus d'informations sur la création et le déploiement de modèles, voir la [documentation {{site.data.keyword.knowledgestudioshort}}![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window}. Vous avez besoin de l'ID unique du modèle déployé pour l'intégrer au service {{site.data.keyword.discoveryshort}}.

## Intégration de votre modèle personnalisé à l'aide de l'API

1.  Procurez-vous l'ID de votre environnement {{site.data.keyword.discoveryshort}} en procédant comme indiqué dans l'article [List environments ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}. Notez l'ID de l'environnement.
1.  Répertoriez les ID de votre configuration ou de vos configurations {{site.data.keyword.discoveryshort}} en cours en procédant comme indiqué dans l'article [List configurations ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} Notez l'ID de la configuration que vous souhaitez intégrer à votre modèle personnalisé {{site.data.keyword.knowledgestudiofull}}.
1.  Téléchargez une copie de votre configuration {{site.data.keyword.discoveryshort}} en cours en exécutant les commandes suivantes dans un interpréteur de commandes bash ou un environnement équivalent, tel que Cygwin pour Windows. Remplacez `{environment_id}` et `{configuration_id}` par les ID que vous avez notés au cours des deux étapes précédentes.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07" > my_config.json
    ```
    {: pre}

    Cette commande permet d'afficher le contenu de votre fichier de collection et de placer ce contenu dans un fichier JSON nommé `my_config.json`.
1.  Ouvrez le fichier `my_config.json` dans un éditeur de texte et effectuez les modifications suivantes :
    1.  Remplacez la valeur de la zone `"name"` par un texte décrivant la finalité de la nouvelle configuration. Vous pouvez éventuellement modifier également la valeur de la zone `"description"`.

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  Mettez à jour les zones d'enrichissement avec des informations relatives au modèle {{site.data.keyword.knowledgestudioshort}}. En supposant que les zones d'enrichissement contenaient à l'origine :

        ```json
        "enrichments": [
        {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {}
                }
            }
        }]
        ```
        {: codeblock}

    1.  Mettez à jour le fichier comme suit, en remplaçant l'ID unique du modèle {{site.data.keyword.knowledgestudioshort}} décrit dans la section "Avant de commencer" pour  `{watson_knowledge_studio_model_ID}` :

        ```json
        "enrichments": [
        {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50,
                        "model": "{watson_knowledge_studio_model_ID}"
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {
                      "model": "{watson_knowledge_studio_model_ID}"
                    }
                }
            }
        }]
        ```
        {: codeblock}

1.  Sauvegardez le fichier `my_config.json`.
1.  Utilisez un valideur JSON, tel que [JSLint ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://jslint.com){: new_window} pour valider, et le cas échéant, corriger votre fichier JSON édité avant d'exécuter les étapes suivantes.
1.  Mettez à jour la configuration comme indiqué ci-après. Une fois de plus, vous avez besoin des ID `{environment_id}` et `{configuration_id}` que vous avez collectés au début de cette procédure.

    ```bash
    curl -X PUT -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    **Remarque :** si vous créez une nouvelle configuration ou si vous modifiez la configuration par défaut, vous devez créer une nouvelle configuration personnalisée au lieu de mettre à jour une configuration existante. Avant de créer une nouvelle configuration, vérifiez que la zone `"configuration_id":` a été retirée du fichier `my_config.json`, puis exécutez la commande suivante :

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
    ```
    {: pre}

    Les deux commandes renvoient le contenu du fichier de configuration mis à jour.

## Intégration de votre modèle personnalisé à l'aide des outils Discovery

Vous pouvez intégrer un modèle personnalisé {{site.data.keyword.knowledgestudioshort}} à l'enrichissement [Entity Extraction](/docs/services/discovery/building.html#entity-extraction) ou [Relation Extraction](/docs/services/discovery/building.html#relation-extraction) à l'aide des outils {{site.data.keyword.discoveryshort}}.

1. Procurez-vous l'ID de modèle (`Model ID`) de votre modèle {{site.data.keyword.knowledgestudioshort}}.
1. Dans les outils {{site.data.keyword.discoveryshort}}, cliquez sur l'icône **Manage Data** dans l'angle supérieur gauche pour ouvrir l'écran **Manage data**, puis créez ou ouvrez une collection. **Remarque :** Si vous sélectionnez une collection existante, celle-ci doit être vide. Dans le cas contraire, vous devrez réingérer ces documents après la création de votre nouveau fichier de configuration. 
1. A la section **Configuration** de l'écran **Manage Data** de votre collection, cliquez sur **Switch**, puis sur **Create a New Configuration**. Donnez un nom à la configuration. 
1. Cliquez sur **Add enrichments** et sélectionnez l'enrichissement **Entity Extraction** ou **Relation Extraction**.
1. Entrez l'ID de modèle (`Model ID`) dans la zone `Custom Model ID` de l'enrichissement sélectionné. Le modèle {{site.data.keyword.knowledgestudiofull}} personnalisé remplacera le modèle par défaut de cet enrichissement. 
1. Cliquez sur **Apply**, puis sur **Done**.

Lorsque des documents sont téléchargés dans une collection de données, ils sont convertis et enrichis à l'aide du fichier de configuration choisi pour cette collection. Si vous affectez un nouveau fichier de configuration à une collection existante après avoir téléchargé des documents, ces derniers continueront d'être convertis à l'aide du fichier de configuration d'origine. Tous les documents téléchargés après le changement de fichier de configuration utiliseront le nouveau fichier de configuration. Si vous souhaitez que **toute** la collection utilise la nouvelle configuration, vous devrez créer une nouvelle collection, choisir ce nouveau fichier de configuration et télécharger à nouveau tous les documents.

**Remarque :** seul le modèle {{site.data.keyword.knowledgestudiofull}} peut être affecté à un enrichissement.

## Etapes suivantes

Utilisez le service {{site.data.keyword.discoveryshort}} avec votre nouvelle configuration pour ingérer des données privées. Les documents que vous ingérez avec la configuration mise à jour sont automatiquement enrichis avec les données provenant de votre modèle personnalisé.
