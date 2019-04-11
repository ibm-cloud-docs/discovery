---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Initiation à Data Crawler
{: #getting-started-with-the-data-crawler}

Cette rubrique explique comment utiliser Data Crawler pour ingérer des fichiers à partir de votre système de fichiers local, dans le but de les utiliser avec le service {{site.data.keyword.discoveryfull}}.
{: shortdesc}

Utilisez Data Crawler uniquement pour explorer les bases de données ou les partages de fichier. Dans tous les autres cas, vous devez utiliser le connecteur {{site.data.keyword.discoveryshort}} approprié. Pour plus de détails, voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources). Plus aucune assistance n'est disponible pour Data Crawler si vous utilisez ce composant avec une source de données prise en charge par les connecteurs {{site.data.keyword.discoveryshort}}.
{: important}

Avant d'exécuter cette tâche, créez une instance du service {{site.data.keyword.discoveryshort}} dans {{site.data.keyword.Bluemix}}. Pour exécuter cette tâche, vous aurez besoin des données d'identification qui sont associées à l'instance du service que vous avez créée.

## Créer un environnement
{: #dc-create-environment}

Utilisez la méthode bash POST /v1/environments pour créer un environnement. Considérez votre environnement comme un entrepôt dans lequel vous
stockez toutes vos boîtes de documents. L'exemple
suivant permet de créer un environnement nommé
`my-first-environment` :

Remplacez `{apikey}` par vos données d'identification du service.

(Pour plus d'informations sur l'utilisation des données d'identification {apikey}, voir [Initiation à l'API](/docs/services/discovery?topic=discovery-gs-api#gs-api).)

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

L'API
renvoie une réponse qui inclut des informations telles que votre ID d'environnement, le
statut de l'environnement et le volume de stockage utilisé par l'environnement. Ne passez
pas à l'étape suivante tant que le statut de votre environnement n'indique pas
`ready`. Lorsque vous créez l'environnement, si le statut
renvoie `status:pending`, utilisez la méthode `GET
/v1/environments/{environment_id}` pour vérifier le statut jusqu'à ce qu'il
affiche "ready". Dans cet exemple, remplacez `{apikey}` par les données d'identification du service et remplacez `{environment_id}` par l'ID d'environnement renvoyé lors de la création de l'environnement.

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
```
{: pre}

## Créer une collection
{: #dc-create-collection}

Ensuite, utilisez la méthode `POST
/v1/environments/{environment_id}/collections` pour créer une collection. Considérez
une collection comme une boîte dans laquelle vous stockez vos documents dans votre
environnement. Cet exemple permet de créer une collection nommée
`my-first-collection` dans l'environnement que vous
avez créé à l'étape précédente ; il utilise la configuration par défaut :

-   Remplacez `{apikey}` par vos données d'identification du service.
-   Remplacez `{environment_id}` par l'ID d'environnement associé à l'environnement que vous avez créé à l'étape 1.

Avant de créer une collection, vous devez
obtenir l'ID de votre configuration par défaut. Pour
connaître votre ID de configuration `configuration_id` par défaut,
utilisez la méthode `GET /v1/environments/{environment_id}/configurations` :

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
```
{: pre}

Une
fois que vous disposez de l'ID de configuration par défaut, utilisez-le pour créer votre collection. Remplacez `{configuration_id}` par l'ID de configuration par défaut qui est associé à votre environnement.

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

L'API renvoie une réponse qui inclut des informations telles que votre ID
de collection, le statut de la collection et le volume de stockage utilisé
par la collection. Ne passez
pas à l'étape suivante tant que le statut de votre collection n'indique pas `online`. Lorsque
vous créez la collection, si le statut renvoie
`status:pending`, utilisez la méthode `GET
/v1/environments/{environment_id}/collections/{collection_id}` pour vérifier le
statut jusqu'à ce qu'il soit prêt. Dans cet exemple, remplacez `{apikey}` par les données d'identification du service, `{environment_id}` par l'ID d'environnement et `{collection_id}` par l'ID de collection renvoyé précédemment au cours de cette étape.

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
```
{: pre}

## Télécharger des exemples de document
{: #dc-download-documents}

Téléchargez les documents suivants :

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>

## Télécharger et installer Data Crawler
{: #download-and-install-the-data-crawler}

1.  Vérifiez la configuration requise de votre système

    -   Java Runtime Environment version 8 ou ultérieure

        **Remarque :** votre variable d'environnement `JAVA_HOME` doit être correctement définie, ou ne pas être définie du tout, pour que le moteur d'exploration puisse être exécuté.
    -   Red Hat Enterprise Linux 6 ou 7, ou Ubuntu Linux 15 ou 16. Pour obtenir des performances optimales, il est recommandé d'exécuter Data Crawler sur sa propre instance de Linux, qu'il s'agisse d'une machine virtuelle, d'un conteneur ou d'un matériel.
    -   2 Go de mémoire vive au minimum sur le système Linux

1.  Ouvrez un navigateur et connectez-vous à votre compte [{{site.data.keyword.Bluemix_notm}}![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/){: new_window}.
1.  A partir de votre tableau de bord {{site.data.keyword.Bluemix_notm}}, sélectionnez le service {{site.data.keyword.discoveryshort}} que vous avez précédemment créé.
1.  Sous **Automate the upload of content to the Discovery service**, sélectionnez le lien de téléchargement approprié pour votre système (DEB, RPM ou ZIP) afin de télécharger Data Crawler.
1.  En tant qu'administrateur, utilisez les commandes appropriées pour installer le fichier archive que vous avez téléchargé :

    -   Sur les systèmes, tels que Red Hat et CentOS, qui utilisent des packages rpm, utilisez une commande semblable à la suivante : `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   Sur les systèmes, tels que Ubuntu et Debian, qui utilisent des packages deb, utilisez une commande semblable à la suivante : `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Les scripts Crawler sont installés dans `{installation directory}/bin` ; par exemple, `/opt/ibm/crawler/bin`. Assurez-vous que `{installation_directory}/bin` est défini dans votre variable d'environnement `PATH` pour que les commandes Crawler fonctionnent correctement.

    Les scripts Crawler sont également installés dans `/usr/local/bin`, par conséquent, cela peut aussi être ajouté à votre variable d'environnement `PATH`.
    {: tip}

## Créer votre répertoire de travail
{: #dc-working-directory}

Copiez le contenu du répertoire `{installation_directory}/share/examples/config` dans un répertoire de travail sur votre système, par exemple, `/home/config`.

**Avertissement :** vous ne devez pas modifier directement les exemples de fichier de configuration fournis. Vous devez les copier, puis les éditer. Si vous éditez les exemples de fichier internes, il se peut que votre configuration soit remplacée si vous mettez à niveau Data Crawler ou retirée si vous désinstallez Data Crawler.

**Remarque :** les fichiers du répertoire `config` mentionnés dans ce guide, par exemple, `config/crawler.conf`, font référence aux fichiers de votre répertoire de travail et NON aux fichiers du répertoire `{installation_directory}/share/examples/config` installé.

## Configurer les options d'exploration
{: #dc-configure-crawl-options}

Pour configurer Data Crawler dans le but d'explorer votre référentiel, vous devez spécifier quels fichiers du système local explorer et à quel service {{site.data.keyword.discoveryshort}} envoyer la collection de fichiers explorés une fois l'exploration terminée.

1.  **`filesystem-seed.conf`** - Ouvrez le fichier `seeds/filesystem-seed.con` dans un éditeur de texte. Modifiez l'attribut `value` directement sous l'attribut `name-"url"` et remplacez-le par le chemin d'accès au fichier que vous souhaitez explorer. Par exemple : `value-"sdk-fs:///TMP/MY_TEST_DATA/"`

    **Remarque :** les URL doivent débuter par `sdk-fs://`. Par conséquent, pour explorer, par exemple, `/home/watson/mydocs`, la valeur de cette adresse URL doit être `sdk-fs:///home/watson/mydocs` (le troisième / est nécessaire !)

    Sauvegardez et fermez le fichier.

1.  **`discovery_service.conf`** - Ouvrez le fichier `discovery/discovery_service.conf` dans un éditeur de texte Modifiez les valeurs suivantes qui sont propres au service {{site.data.keyword.discoveryshort}} que vous avez précédemment créé sur {{site.data.keyword.Bluemix_notm}} :

    -   `environment_id` - ID d'environnement du service {{site.data.keyword.discoveryshort}}.
    -   `collection_id` - ID de collection du service {{site.data.keyword.discoveryshort}}.
    -   `configuration_id` - ID de configuration du service {{site.data.keyword.discoveryshort}}.
    -   `configuration` - Emplacement du chemin d'accès complet du fichier `discovery_service.conf`, par exemple, `/home/config/discovery/discovery_service.conf`.
    -   `apikey` - Données d'identification pour le service {{site.data.keyword.discoveryshort}}.
1.  **`crawler.conf`** - Ouvrez le fichier `config/crawler.conf` dans un éditeur de texte.

    -   Définissez les options `output_adapter`, `class` et `config` pour le service {{site.data.keyword.discoveryshort}}, comme suit :

        ```bash
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
      }
        ```
        {: pre}

1.  Après avoir modifié ces fichiers, vous êtes prêt à explorer vos données.

## Analyser vos données
{: #dc-crawl}

Exécutez la commande suivante : `crawler crawl --config [config/crawler.conf]`

Une exploration sera exécutée avec le fichier de configuration `crawler.conf`.

**Remarque :** le chemin d'accès au fichier de configuration transmis via l'option `--config -c` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/crawler.conf` ou `./crawler.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/crawler.conf`.

## Effectuer des recherches dans vos documents
{: #dc-search}

Finalement, utilisez la méthode `GET
/v1/environments/{environment_id}/collections/{collection_id}/query` pour
effectuer des recherches dans votre collection de documents. L'exemple suivant renvoie toutes les entités
nommées `IBM` :

-   Remplacez `{apikey}` par vos données d'identification du service.
-   Remplacez `{environment_id}` par l'ID d'environnement associé à l'environnement que vous avez créé à l'étape 1.
-   Remplacez `{collection_id}` par l'ID de collection associé à la collection que vous avez créée à l'étape 2.

```bash
curl -u "apikey:{apikey}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## Résultats
{: #dc-results}

Vous avez lancé des requêtes sur des documents dans un environnement et une collection que vous avez créés. Vous pouvez maintenant commencer à effectuer des tâches de personnalisation en ajoutant d'autres documents à la collection.
