---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-14"

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

# Connexion à des sources de données
{: #sources}

Le service {{site.data.keyword.discoveryshort}} vous permet de vous connecter à des documents et de les explorer à partir de sources distantes.
{: shortdesc}

Vous pouvez vous connecter à une source de données et extraire des documents selon un planning (si vous le souhaitez) dans le service {{site.data.keyword.discoveryshort}} en configurant une collection à associer à cette source. Chaque collection peut être configurée avec une source de données. Le service {{site.data.keyword.discoveryshort}} extrait des documents de la source de données en utilisant un processus appelé exploration. L'exploration est le processus qui consiste à systématiquement explorer et extraire des documents de l'emplacement de départ spécifié. Seuls les éléments explicitement spécifiés par vous sont explorés par le service {{site.data.keyword.discoveryshort}}. Les types suivants de source de données peuvent être explorés : 

-  [Box](/docs/services/discovery/connect.html#connectbox)
-  [Salesforce](/docs/services/discovery/connect.html#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)

La connexion à une source de données peut être effectuée à l'aide des outils {{site.data.keyword.discoveryshort}} ou de l'API. Les outils {{site.data.keyword.discoveryshort}} fournissent une méthode simplifiée de connexion qui nécessite une moindre compréhension des systèmes source, tandis que l'API offre une interface plus granulaire et hautement configurable qui requiert une meilleure compréhension de la source à laquelle vous vous connectez. La présentation de processus suivante vous permet de savoir quelles section du présent document lire ensuite :

1.  Lisez les [exigences générales liées à la source](/docs/services/discovery/connect.html#gen_req) pour une vue générale des éléments requis.
2.  Lisez les exigences spécifiques à votre système source : 
    -  [Box](/docs/services/discovery/connect.html#connectbox)
    -  [Salesforce](/docs/services/discovery/connect.html#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)
3.  Lisez les instructions de configuration de source basées sur votre choix de configuration : 
    -  [Utilisation des outils](/docs/services/discovery/connect.html#source_tooling)
    -  [Utilisation de l'API](/docs/services/discovery/connect.html#source_api)

## Exigences générales liées à la source
{: #gen_req}

Les exigences générales suivante s'appliquent à toutes les sources de données : 

-  La taille limite du fichier document individuel pour Box, Salesforce et SharePoint Online est de 10 Mo.
-  Vous aurez besoin des données d'identification et des emplacements de fichier (ou URL) pour chaque source de données - ces informations sont généralement fournies par un développeur/administrateur système de la source de données.
-  Vous aurez besoin de connaître les ressources de la source de données à explorer. Ces informations peuvent être fournies par l'administrateur de la source. Lors d'une exploration de Box ou Salesforce, la liste des ressources disponibles est présentée lors de la configuration d'une source utilisant les outils {{site.data.keyword.discoveryshort}}.
-  L'exploration d'une source de données utilise des ressources (appels API) de la source de données. Le nombre d'appels dépend du nombre de documents explorés. Un niveau approprié de service (Enterprise, par exemple) doit être obtenu pour la source de données et l'administrateur du système source doit être consulté. 
-  Les types de fichier suivants peuvent être ingérés par {{site.data.keyword.discoveryshort}}, tout autre type de document étant ignoré :
   -  Microsoft Word
   -  PDF
   -  HTML
   -  JSON
-  Les explorations de source {{site.data.keyword.discoveryshort}} ne supprime pas les documents stockés dans une collection. Lorsqu'une source est à nouveau explorée, les nouveaux documents sont ajoutés, les documents mis à jour sont modifiés dans la version en cours et les documents supprimés restent en tant que version stockée en dernier. 

## Box
{: #connectbox}

Lors de la connexion à une source Box, assurez-vous que l'instance à laquelle vous prévoyez de vos connecter est un plan Enterprise ou supérieur. 

Configuration d'un compte Box à utiliser avec {{site.data.keyword.discoveryshort}} :

1.  Créez une application personnalisée Box sur `https://app.box.com/developers/console` (utilisez l'URL Box de votre société).
1.  Effectuez ensuite l'une des opérations suivantes :
    - Sélectionnez un **accès à l'application** de niveau `Enterprise`, puis continuez en utilisant des utilisateurs gérés existants.
      OU
    - Sélectionnez un **accès à l'application** de niveau `Application` puis créez un `utilisateur d'application` avec l'application nouvellement créée à l'aide de l'[API Box ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.box.com/reference#create-app-user){: new_window}.
1.  Activez les **portées d'application** suivantes :
    - `Read and Write All Folders Stored In Box` (droit de lecture et écriture sur tous les dossiers stockés dans Box)
    - `Manage Users` (gérer des utilisateurs)
1.  Activez les **fonctions avancées** suivantes : 
    - `Perform Actions as Users` (exécuter des actions en tant qu'utilisateur)
    - `Generate User Access Tokens` (générer des jetons d'accès utilisateur)
1.  Demandez à l'administrateur d'autoriser votre ID client d'application `https://app.box.com/master/settings/openbox` en tapant l'`ID client` de `https://app.box.com/developers/console` dans la zone `API Key`.
1.  Générez la `public/private keypair` (paire de clés publique/privée qui sera téléchargée sur votre ordinateur).
1.  Ouvrez le fichier téléchargé et copiez/collez les zones dans {{site.data.keyword.discoveryshort}}. Retirez la nouvelle ligne de fin `\n` à la fin de `privateKey` lorsque vous copiez la ligne dans {{site.data.keyword.discoveryshort}}.

**Remarque :** {{site.data.keyword.discoveryshort}} ne prend pas en charge l'exploration d'application personnalisée en tant que tel (vous ne pouvez pas simuler les droits d'accès vous-même). 

Les données d'identification suivantes sont requises pour la connexion à une source Box, vous devez vous les procurer auprès de votre administrateur Box (à moins que vous ne les ayez déjà obtenues en configurant une application personnalisée Box à l'aide des étapes précédentes) : 

-  `client_id` - `client_id` (ID client) de la source à laquelle ces données d'identification permettent de se connecter.     
-  `enterprise_id` - `enterprise_id` (ID entreprise) du site Box auquel ces données d'identification permettent de se connecter.
-  `client_secret` - `client_secret` (secret client) de la source à laquelle ces données d'identification permettent de se connecter. Cette valeur n'est jamais renvoyée et est utilisée uniquement lors de la création ou de la modification des données d'identification. 
-  `public_key_id` - `public_key_id` (ID clé publique) de la source à laquelle ces données d'identification permettent de se connecter. Cette valeur n'est jamais renvoyée et est utilisée uniquement lors de la création ou de la modification des données d'identification. 
-  `private_key` - `private_key` (clé privée) de la source à laquelle ces données d'identification permettent de se connecter. Cette valeur n'est jamais renvoyée et est utilisée uniquement lors de la création ou de la modification des données d'identification. 
-  `passphrase` - `passphrase` (phrase passe) de la source à laquelle ces données d'identification permettent de se connecter. Cette valeur n'est jamais renvoyée et est utilisée uniquement lors de la création ou de la modification des données d'identification. 

Lors de l'identification des données d'identification, il peut être utile de consulter la [documentation du développeur Box ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.box.com/){: new_window}.

Autres éléments à prendre en considération lors de l'exploration de Box :

-  Les notes Box étant stockées au format JSON, toute note se trouvant dans les dossiers spécifiés sera ingérée par {{site.data.keyword.discoveryshort}}.
-  Lors de l'utilisation de l'API, vous devrez disposer d'une liste des ID dossier et des ID propriétaire associés à chaque dossier que vous souhaitez explorer. Les outils {{site.data.keyword.discoveryshort}} vous permettent de parcourir et sélectionner du contenu à explorer.

## Salesforce
{: #connectsf}

Lors de la connexion à une source Salesforce, assurez-vous que l'instance à laquelle vous prévoyez de vos connecter est un plan Enterprise ou supérieur. 

Les données d'identification suivantes sont requises pour la connexion à une source Salesforce, vous devez vous les procurer auprès de votre administrateur Salesforce : 
-  `url` - `url` de la source à laquelle ces données d'identification permettent de se connecter. 
-  `username` - `username` (nom d'utilisateur) de la source à laquelle ces données d'identification permettent de se connecter. 
-  `password` - Le `password` est une concaténation du mot de passe Salesforce et d'un jeton de sécurité Salesforce valide. Cette valeur n'est jamais renvoyée et est utilisée uniquement lors de la création ou de la modification des données d'identification. 

Lors de l'identification des données d'identification, il peut être utile de consulter la [documentation du développeur Salesforce ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.salesforce.com/docs/){: new_window}.

Autres éléments à noter lors de l'exploration de Salesforce :

-  Les articles provenant de Knowledge Center sont explorés uniquement si leur **version** est `published` et si leur langue est `en-us`.
-  Lors de l'utilisation de l'API, vous devrez disposer d'une liste des objets Salesforce que vous souhaitez explorer. Les outils {{site.data.keyword.discoveryshort}} vous permettent de parcourir et sélectionner du contenu à explorer.


## SharePoint Online
{: #connectsp}

Lors de la connexion à une source Microsoft SharePoint Online, assurez-vous que l'instance à laquelle vous prévoyez de vos connecter est un plan Enterprise (E1) ou supérieur. 

Les données d'identification suivantes sont requises pour la connexion à une source SharePoint Online, vous devez vous les procurer auprès de votre administrateur SharePoint : 

-  `organization_url` - `organization_url` de la source à laquelle ces données d'identification permettent de se connecter. 
-  `site_collection.path` - `site_collection.path` de la source à laquelle ces données d'identification permettent de se connecter. 
-  `username` - `client_id` (ID client) de la source à laquelle ces données d'identification permettent de se connecter. 
-  `password` - `password` de la source à laquelle ces données d'identification permettent de se connecter. Cette valeur n'est jamais renvoyée et est utilisée uniquement lors de la création ou de la modification des données d'identification. 

Lors de l'identification des données d'identification, il peut être utile de consulter la [documentation du développeur Microsoft SharePoint ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Autres éléments à noter lors de l'exploration de Microsoft SharePoint Online :

-  Lors de l'utilisation de l'API, vous devrez disposer d'une liste des chemins de collecte de site SharePoint que vous souhaitez explorer. Les outils {{site.data.keyword.discoveryshort}} vous permettent de parcourir et sélectionner du contenu à explorer. Pour explorer la totalité de votre site SharePoint Online, ne sélectionnez pas plusieurs chemins d'accès (URL) dans cette zone. Dans ce cas de figure, entrez un `/` dans la zone `site_collection.path`.

## Utilisation des outils
{: #source_tooling}

La connexion à une source données à l'aide des outils {{site.data.keyword.discoveryshort}} est effectuée via la création d'une collection spécifique à une source. Procédez comme suit pour créer une collection source et l'explorer :

1.  Depuis la page **Manage data** des outils {{site.data.keyword.discoveryshort}}, sélectionnez **Connect a data source**.
2.  Sélectionnez la source de données à laquelle vous souhaitez vous connecter. 
3.  Entrez vos données d'identification source et cliquez sur Connect. Vos données d'identification doivent être obtenues auprès de votre administrateur système source.
4.  Choisissez les données à explorer, ainsi que la fréquence de synchronisation. 
5.  Cliquez sur **Save & Sync objects** pour démarrer l'exploration de votre source de données. Vous êtes alors redirigé vers l'écran de statut de la collecte qui est mis à jour au fur et à mesure de l'ajout de documents à la collection.

L'exploration synchronise les données initialement, puis selon la fréquence spécifiée.
**Remarque :** Si vous modifiez un élément de l'écran **Sync settings** puis cliquez sur **Save and Sync objects**, une exploration est alors lancée (ou redémarrée si déjà en cours). 

## Utilisation de l'API
{: #source_api}

Utilisez le processus suivant pour créer une collection connectée à une source de données à l'aide de l'API.
1.  Créez des données d'identification pour la source à laquelle vous vous connectez à l'aide l'[API de données d'identification source ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window}. Enregistrez le **credential_id** renvoyé pour les données d'identification nouvellement créées. 
2.  Créez une configuration à l'aide de l'[API de configuration ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}. Cette configuration doit comporter un objet **source** qui définit ce qui doit être exploré. L'objet **source** doit contenir le **credential_id** que vous avez enregistré plus tôt.
    ```json
    "source" : {
      "type" : "salesforce",
      "credential_id" : "{credential_id}",
      "schedule" : {
        "enabled" : true,
        "time_zone" : "America/New_York",
        "frequency" : "weekly"
      },
      "options" : {
         "site_collections" : [ {
         "site_collection_path" : "/sites/TestSiteA",
         "limit" : 10
         } ]
      }
    }
    ```
    {: codeblock}
    Enregistrez le **configuration_id** renvoyé de la configuration nouvellement créée.
3.  Créez une collection à l'aide de l'[API Collections ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}. L'objet qui définit la collection doit contenir le **configuration_id** que vous avez enregistré précédemment.

L'exploration source débute dès que la collection est créée, puis selon la fréquence spécifiée.
**Remarque :** Si vous modifiez un élément de l'objet **source** de la configuration, une nouvelle exploration est alors démarrée (ou redémarrée si déjà en cours). 

## Spécification d'un `customer_id`
{:# source_customer_id}

Une zone `customer_id` d'un document {{site.data.keyword.discoveryshort}} ingéré peut être utilisée pour supprimer du contenu en fonction du `customer_id` à l'aide de la méthode **user-data** dans l'API. Les documents entrants qui proviennent d'une source de données ne reçoivent pas automatiquement un `customer_id` lorsqu'ils sont ingérés. Si votre application requiert la définition d'un `customer_id`, vous pouvez en spécifier une (ou plusieurs) des zones entrantes provenant du système source pour être copiées et utilisées en tant que `customer_id`. Pour ce faire, vous devez modifier la configuration utilisée pour la connexion à la source.

1.  Exécutez un exemple de requête et identifiez les zones à utiliser comme `customer_id`.
2.  Modifiez la configuration. Vous aurez besoin d'ajouter une section **Normalization** pour pouvoir créer la zone `customer_id`.
    -  Dans les outils, accédez à votre collection t cliquez sur le lien **edit** de la section configuration. Cliquez ensuite sur l'onglet **Normalization** et ajoutez-y une normalisation **copy** pour créer la zone `customer_id`. Cliquez ensuite sur **Apply & save**.
    ![Copy normalization](images/norm_copy.png)
    -  Lors de l'utilisation de l'API, ajoutez l'objet suivant au tableau **Normalization**"
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  La prochaine exploration planifiée ajoutera la zone `customer_id` à tous les documents. Si vous souhaitez qu'une exploration débute immédiatement, modifiez la configuration source (**Sync settings** dans les outils).

Voir la [sécurité des informations ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/docs/services/discovery/information-security.html){: new_window} pour plus d'informations, notamment sur la suppression basée sur un `customer_id`.
