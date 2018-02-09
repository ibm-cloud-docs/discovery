---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

# Configuration de Data Crawler

Pour configurer Data Crawler dans le but d'explorer votre référentiel, vous devez spécifier l'adaptateur d'entrée approprié dans le fichier `crawler.conf`, puis configurer les informations spécifiques au référentiel dans les fichiers de configuration d'adaptateur d'entrée.
{: shortdesc}

Avant d'effectuer les modifications décrites dans les étapes ci-après, prenez soin de créer votre répertoire de travail en copiant le contenu du répertoire `{installation_directory}/share/examples/config` dans un répertoire de travail sur votre système, par exemple, `/home/config`.

**Important :** vous ne devez pas modifier directement les exemples de fichier de configuration fournis. Vous devez les copier, puis les éditer. Si vous éditez les exemples de fichier internes, il se peut que votre configuration soit remplacée si vous mettez à niveau Data Crawler ou retirée si vous désinstallez Data Crawler. 

**Remarque :** les fichiers du répertoire `config` mentionnés dans ce guide, par exemple, `config/crawler.conf`, font référence aux fichiers de votre répertoire de travail et NON aux fichiers du répertoire `{installation_directory}/share/examples/config` installé. 

Les valeurs spécifiées sont celles qui sont définies par défaut dans `config/crawler.conf` et elles configurent le connecteur Filesystem :

1.  Ouvrez le fichier `config/crawler.conf` dans un éditeur de texte. 

    -   Affectez à l'option `crawl_config_file` la valeur `.conf` que vous avez précédemment modifiée, par exemple, `connectors/filesystem.conf`.
    -   Affectez à l'option `crawl_seed_file` la valeur `-seed.conf` que vous avez précédemment modifiée, par exemple, `seeds/filesystem-seed.conf`.
    -   Définissez les options `output_adapter`, `class` et `config` pour le service {{site.data.keyword.discoveryshort}}, comme suit : 

        ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: codeblock}

    Ce fichier contient d'autres paramètres facultatifs qui peuvent être définis de manière appropriée pour votre environnement. Pour plus d'informations sur la définition de ces valeurs, voir :[Configuration des options d'exploration](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options), [Configuration de l'adaptateur d'entrée](/docs/services/discovery/data-crawler-discovery.html#input-adapter), [Configuration de l'adaptateur de sortie](/docs/services/discovery/data-crawler-discovery.html#output-adapter) et [Options supplémentaires de gestion des explorations](/docs/services/discovery/data-crawler-discovery.html#additional-crawl-management-options). 

1.  Ouvrez le fichier `discovery/discovery_service.conf` dans un éditeur de texte Modifiez les valeurs suivantes qui sont propres au service {{site.data.keyword.discoveryshort}} que vous avez précédemment créé sur {{site.data.keyword.Bluemix}} :

    -   `environment_id` - ID d'environnement du service {{site.data.keyword.discoveryshort}}. 
    -   `collection_id` - ID de collection du service {{site.data.keyword.discoveryshort}}. 
    -   `configuration_id` - ID de configuration du service {{site.data.keyword.discoveryshort}}. 
    -   `configuration` - Emplacement du chemin d'accès complet du fichier `discovery_service.conf`, par exemple, `/home/config/discovery/discovery_service.conf`.
    -   `username` - Données d'identification par nom d'utilisateur pour le service {{site.data.keyword.discoveryshort}}. 
    -   `password` - Données d'identification par mot de passe pour le service {{site.data.keyword.discoveryshort}}. 

    Ce fichier contient d'autres paramètres facultatifs qui peuvent être définis de manière appropriée pour votre environnement. Pour plus d'informations sur la définition de ces valeurs, voir [Configuration des options de service](/docs/services/discovery/data-crawler-discovery.html#configuring-service-options). 

1.  Après avoir modifié ces fichiers, vous êtes prêt à explorer vos données. Reportez-vous à la rubrique[Exploration de votre référentiel de données](/docs/services/discovery/data-crawler-run.html#crawling-your-data-repository) pour continuer.

## Configuration des options d'exploration
{: #configuring-crawl-options}

Le fichier `config/crawler.conf` contient des informations qui indiquent à Data Crawler quels sont les fichiers à utiliser pour l'exploration (adaptateur d'entrée), où envoyer la collection de fichiers explorés une fois l'exploration terminée (adaptateur de sortie), ainsi que d'autres options de gestion de l'exploration. 

**Remarque** : tous les chemins d'accès aux fichiers sont relatifs au répertoire `config`, sauf indication contraire.

Pour accéder au manuel intégré au produit qui est relatif au fichier `crawler.conf` et qui contient les toutes dernières informations, tapez la commande suivante dans le répertoire d'installation de Data Crawler : `man crawler.conf`
{: tip}

Les options qui peuvent être définies dans ce fichier sont les suivantes :

### Adaptateur d'entrée
{: #input-adapter}

-   **`class`** - Usage interne uniquement ; définit la classe de l'adaptateur d'entrée de Data Crawler. La valeur par défaut est `com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl`
-   **`config`** - Usage interne uniquement ; définit la configuration de structure de connecteur. La clé de la configuration par défaut dans ce bloc qui doit être transmise à l'adaptateur d'entrée choisi est `connector_framework`. 

    La structure de connecteur est ce qui vous permet de communiquer avec vos données. Il peut s'agir de données internes à l'entreprise ou de données externes sur le Web ou dans le cloud. Les connecteurs permettent d'accéder à un certain nombre de sources de données différentes, tandis que la connexion est en fait contrôlée par le processus d'exploration.

    **Important :** les données extraites par l'adaptateur d'entrée de la structure de connecteur est mise en cache localement. Elles ne sont pas stockées sous forme chiffrée. Par défaut, les données sont mises en cache dans un répertoire temporaire dont le contenu doit être effacé au réamorçage et elles ne doivent être lisibles que par l'utilisateur qui a exécuté la commande du moteur d'exploration.

    Il est possible que ce répertoire puisse survivre au moteur d'exploration si la structure de connecteur devait disparaître avant de pouvoir nettoyer les fichiers après lui. Etudiez soigneusement l'emplacement de vos données en cache ; vous pouvez les placer sur un système de fichiers chiffré, mais soyez conscient de l'impact que cela pourrait avoir sur les performances. Vous seul pouvez déterminer l'équilibre approprié entre vitesse et sécurité pour vos explorations.
-   **`crawl_config_file`** - Fichier de configuration à utiliser pour l'exploration. La valeur par défaut est `connectors/filesystem.conf`.
-   **`crawl_seed_file`** - Fichier de départ de l'exploration à utiliser pour l'exploration. La valeur par défaut est `seeds/filesystem-seed.conf`. 
-   **`id_vcrypt_file`** - Fichier de clés utilisé pour le chiffrement de données par Data Crawler ; la clé par défaut incluse avec le moteur d'exploration est `id_vcrypt`. Utilisez le script vcrypt dans le dossier `bin` si vous avez besoin de générer un nouveau fichier `id_vcrypt`. 
-   **`crawler_temp_dir`** - Dossier temporaire du moteur d'exploration pour les journaux du connecteur. La valeur par défaut, `tmp`, est fournie. S'il n'existe pas déjà, le dossier `tmp` est créé dans le répertoire de travail en cours.
-   **`extra_jars_dir`** - Ajoute un répertoire de fichiers JAR supplémentaires au chemin d'accès aux classes de la structure de connecteur. 

    **Remarque** : relatif au répertoire `lib/java` de la structure de connecteur. 

    -   Cette valeur doit être `oakland` lorsque le connecteur SharePoint est utilisé. 
    -   Cette valeur doit être `database` lorsque le connecteur Database est utilisé. 

    Vous pouvez laisser cette valeur vide (par exemple, une chaîne vide "") lorsque vous utilisez d'autres connecteurs. 

-   **`urls_to_filter`** - Liste blanche d'URL à explorer, sous la forme d'une expression régulière Data Crawler n'explore que les adresses URL qui correspondent à l'une des expressions régulières fournies.

    La liste des domaines contient les domaines de niveau supérieur les plus courants ; ajoutez-en si nécessaire.

    La liste des types d'extension de fichier contient les extensions de fichier prises en charge par le service d'orchestration, pour cette version de Data Crawler.

    Vérifiez que le domaine de votre adresse URL de départ est autorisé par le filtre. Par exemple, si l'adresse URL de départ est semblable à `http://testdomain.test.in`, ajoutez"`in`" au filtre de domaines.

    Vérifiez que votre adresse URL de départ ne sera pas exclue par un filtre, faute de quoi, le moteur d'exploration pourrait se bloquer.

-   **`max_text_size`** - Taille maximale, en octets, d'un document avant que ce dernier ne soit enregistré sur le disque par la structure de connecteur. Lorsqu'une valeur supérieure est affectée à ce paramètre, la quantité de documents écrits sur disque diminue, mais la quantité de mémoire requise augmente. La valeur par défaut est `1048576`
-   **`extra_vm_params`** - Permet d'ajouter des paramètres Java supplémentaires à la commande utilisée pour lancer la structure de connecteur.

-   **`bootstrap_logging`** - Enregistre le journal de démarrage de la structure de connecteur ; utile uniquement pour un débogage avancé. Les valeurs possibles sont `true` ou `false`. Le fichier journal sera écrit dans `crawler_temp_dir`. 

-   **`read-timeout`** - Définit le délai (exprimé en secondes) pendant lequel le moteur d'exploration attend une réponse de la structure de connecteur. La valeur par défaut est 5 secondes.

### Adaptateur de sortie
{: #output-adapter}

-   **`class`** - Définit la classe de l'adaptateur de sortie de Data Crawler.
-   **`config`** - Définit la clé de configuration à transmettre à l'adaptateur de sortie. La chaîne doit correspondre à une clé de cet objet de configuration. Dans l'exemple de code suivant :

    ```
    class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

    config - "discovery_service"

    discovery_service {
        include "discovery/discovery_service.conf"
      }
    ```
    {: codeblock}

    La clé de configuration est `discovery_service`.

Vous devez sélectionner un adaptateur de sortie en spécifiant son paramètre `class` et sa clé `config`.

-   **{{site.data.keyword.discoveryshort}} Service Output Adapter** - Télécharge les documents explorés dans le service {{site.data.keyword.discoveryfull}}. Sélectionnez cet adaptateur en définissant le paramètre `class` et la clé `config` comme suit :

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            include "discovery/discovery_service.conf"
          }
```
{: codeblock}

-   **Test Output Adapter** - L'adaptateur de sortie de test écrit une représentation des fichiers explorés sur disque, dans un emplacement spécifié. Sélectionnez cet adaptateur en définissant le paramètre `class` et la clé `config` comme suit :

    Un autre paramètre, `output_directory`, sélectionne le répertoire dans lequel la représentation des données explorées doivent être écrites. 

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`** - Spécifie les options des nouvelles tentatives en cas de tentatives infructueuses d'envoi à l'adaptateur de sortie.

    -   `max_attempts` - Nombre maximal de nouvelles tentatives. La valeur par défaut est `10`
    -   `delay` - Délai minimal entre les tentatives, exprimé en secondes. La valeur par défaut est `2`
    -   `exponent_base` - Facteur déterminant l'évolution du délai sur chaque tentative infructueuse. La valeur par défaut est `2`

    La formule est la suivante :

        **`d(nth_retry) - delay * (exponent_base ^ nth_retry)`**

    Par exemple, les paramètres par défaut correspondant à un délai d'1 seconde et à une base d'exposant de 2, provoqueront le report de 2 secondes au lieu d'1 seconde du second nouvel essai, la troisième tentative, et le report de 4 secondes du nouvel essai suivant. 

        `d(0) - 1 * (2 ^ 0)` - 1 second
        `d(1) - 1 * (2 ^ 1)` - 2 seconds
        `d(2) - 1 * (2 ^ 2)` - 4 seconds

    Par conséquent, avec les paramètres par défaut, uns soumission sera tentée jusqu'à 10 fois, occasionnant une attente d'environ 1022 secondes, soit un peu plus de 17 minutes. Ce délai est approximatif car un délai supplémentaire est ajouté pour éviter l'exécution simultanée de plusieurs nouvelles soumissions. Ce temps "aléatoire" peut aller jusqu'à 10 %, par conséquent, la dernière tentative dans l'exemple précédent pourrait être reportée d'un délai pouvant aller jusqu'à 7,7 secondes. Le délai d'attente n'inclut pas le temps passé à se connecter au service, à télécharger les données ou à attendre une réponse.

    La valeur `output_timeout` est prioritaire par rapport au temps d'attente. Si le temps d'attente total pour les tentatives dépasse cette valeur, la soumission échoue même si elle aurait dû être retentée.
    {: tip}

### Options supplémentaires de gestion des explorations
{: #additional-crawl-management-options}

-   **`full_node_debugging`** - Active le mode débogage ; les valeurs possibles sont `true` et `false`.

    **Important :** cela permettra de placer la totalité des données de chaque document exploré dans les journaux.    

-   **`logging.log4j.configuration_file`*** - Fichier de configuration à utiliser pour la journalisation. Dans l'exemple de fichier `crawler.conf`, cette option est définie dans `logging.log4j` et sa valeur par défaut est `log4j_custom.properties`. Cette option doit être définie de la même manière qu'un fichier `.properties` ou `.conf` soit utilisé.   
-   **`shutdown_timeout`** - Spécifie la valeur du délai d'attente, en minutes, avant l'arrêt de l'application. La valeur par défaut est de `10`.   
-   **`output_limit`** - Nombre le plus élevé d'éléments indexables que le moteur d'exploration tentera d'envoyer simultanément à l'adaptateur de sortie. Cette valeur peut être inférieure en fonction du nombre de coeurs disponibles pour effectuer le travail. Elle indique qu'à tout moment, pas plus de "x" éléments indexables seront envoyés à l'adaptateur de sortie en attente de retour. La valeur par défaut est de `10`.   
-   **`input_limit`** - Limite le nombre d'URL pouvant être demandé en une seule fois à partir de l'adaptateur d'entrée. La valeur par défaut est `3`.   
-   **`output_timeout`** - Délai, exprimé en secondes, avant que Data Crawler n'abandonne une demande émise vers l'adaptateur de sortie, puis supprime l'élément dans la file d'attente de l'adaptateur de sortie afin de permettre un traitement supplémentaire. La valeur par défaut est `1200`.

Il est important de prendre en considération les contraintes imposées par l'adaptateur de sortie, car elles peuvent avoir un impact sur les limites définies ici. La valeur`output_limit` définie concerne uniquement le nombre d'objets indexables pouvant être envoyés en même temps à l'adaptateur de sortie. Une fois qu'un objet indexable a été envoyé à l'adaptateur de sortie, il est "pointé", comme défini par la
variable `output_timeout`. Il est possible que l'adaptateur de sortie dispose lui-même d'un régulateur l'empêchant de pouvoir traiter
autant d'entrées qu'il n'en reçoit. Par exemple, l'adaptateur de sortie d'orchestration peut comporter un pool de connexions,
configurable pour les connexions HTTP au service. Si sa valeur par défaut est de 8, par exemple, et que vous affectez à `output_limit` un nombre supérieur à 8, des processus seront en attente d'exécution. Des délais d'attente sont alors à prévoir.   
-   **`num_threads`** - Nombre d'unités d'exécution en parallèle qui peuvent être exécutées simultanément. Cette valeur peut être un entier, qui indique directement le nombre d'unités d'exécution en parallèle, ou une chaîne, au format `"xNUM"`, qui indique le coefficient multiplicateur du nombre de processeurs disponibles. Par exemple, `"x1.5"`. La valeur par défaut est `"30"`. 

## Configuration des options de service
{: #configuring-service-options}

Le service {{site.data.keyword.discoveryshort}} indique au moteur d'exploration comment gérer les fichiers explorés lorsque le service {{site.data.keyword.discoveryfull}} est utilisé. 

Pour accéder au manuel intégré au produit qui est relatif au fichier `discovery-service.conf` et qui contient les toutes dernières informations, tapez la commande suivante dans le répertoire d'installation de Data Crawler :


  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

Les options par défaut peuvent être modifiées directement en ouvrant le fichier `config/discovery/discovery_service.conf` et en spécifiant les valeurs suivantes, propres à votre cas d'utilisation :

-   **`http_timeout`** - Délai, en secondes, de l'opération de lecture/d'indexation des documents ; la valeur par défaut est de `125`.
-   **`proxy_host_port`** - Facultatif - Lorsque vous exécutez Data Crawler derrière un pare-feu, vous pouvez être amené à définir le nom d'hôte et le numéro de port du proxy afin de permettre à Data Crawler de communiquer avec le service {{site.data.keyword.discoveryshort}}. La valeur par défaut pour cette option est une chaîne vide et, si vous devez la modifier, la nouvelle valeur doit être au format `"<host>:<port>"`.
-   **`concurrent_upload_connection_limit`** - Nombre de connexions simultanées autorisées pour le téléchargement des documents. La valeur par défaut est `2`.

    **Remarque :** Lorsque l'adaptateur de sortie du service d'orchestration est utilisé, ce nombre doit être supérieur ou égal à la valeur `output_limit` définie lors de la configuration des options d'exploration.    

-   **`base_url`** - URL vers laquelle vos documents explorés seront envoyés. Pour l'édition actuelle du service {{site.data.keyword.discoveryshort}}, la valeur est `https://gateway.watsonplatform.net/discovery/api`.   
-   **`environment_id`** - Emplacement de votre collection de documents explorés au niveau de l'URL de base.    
-   **`collection_id`** - Nom de la collection de documents que vous configurez dans le service {{site.data.keyword.discoveryshort}}.
-   **`api_version`** - Usage interne uniquement. Date de la dernière modification apportée à la version d'API.   
-   **`configuration_id`** - Nom du fichier de configuration que le service {{site.data.keyword.discoveryshort}} utilise. 
-   **`username`** - Nom d'utilisateur utilisé pour l'authentification auprès de l'emplacement de votre collection de documents explorés.    
-   **`password`** - Mot de passe utilisé pour l'authentification auprès de l'emplacement de votre collection de documents explorés. 

L'adaptateur de sortie du service {{site.data.keyword.discoveryshort}} peut envoyer des statistiques afin de permettre à {{site.data.keyword.IBM}} de mieux comprendre et servir ses utilisateurs. Les options suivantes peuvent être définies pour la variable `send_stats` :

-   **`jvm`** - Les statistiques de la machine virtuelle Java (JVM) envoyées incluent le fournisseur Java et sa version, tels qu'indiqués par la machine virtuelle Java utilisée pour exécuter Data Crawler. La valeur admise est `true` ou `false`. La
valeur par défaut est `true`.
-   **`os`** - Les statistiques du système d'exploitation envoyées incluent le nom du système d'exploitation, sa version et son architecture, tels qu'indiqués par la machine virtuelle Java utilisée pour exécuter Data Crawler. La valeur admise est `true` ou `false`. La
valeur par défaut est `true`.
