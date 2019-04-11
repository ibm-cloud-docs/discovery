---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-01-28"

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

# Exécution de votre référentiel de données
{: #crawling-your-data-repository}

Une fois les options d'exploration correctement configurés, vous pouvez exécuter un moteur d'exploration sur votre référentiel de données.
{: shortdesc}

Utilisez Data Crawler uniquement pour explorer les bases de données ou les partages de fichier. Dans tous les autres cas, vous devez utiliser le connecteur {{site.data.keyword.discoveryshort}} approprié. Pour plus de détails, voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources). Plus aucune assistance n'est disponible pour Data Crawler si vous utilisez ce composant avec une source de données prise en charge par les connecteurs {{site.data.keyword.discoveryshort}}.
{: important}

Vous ne devez jamais exécuter le moteur d'exploration en tant qu'utilisateur `root`, sauf si vous avez besoin d'accéder à des fichiers lisibles uniquement par l'utilisateur `root`.
{: tip}

Exécutez la commande suivante : `crawler`

Le moteur d'exploration vous invite à lire la documentation qui explique ce qu'il faut faire. Vous pouvez exécuter une exploration test, ou exécuter une exploration, en plus d'autres options d'exploration.

## Exécution d'une exploration test
{: #running-test-crawl}

Exécutez la commande suivante : `crawler testit`

Cette commande permet d'exécuter une exploration test qui explore uniquement l'adresse URL de départ et affiche les URL mises en file d'attente. Si l'adresse URL de départ est convertie en un contenu indexable (par exemple, il s'agit d'un document), ce contenu est envoyé à l'adaptateur de sortie, et il s'affiche à l'écran. Si
l'extraction de l'adresse URL de départ entraîne la mise en file d'attente d'adresses
URL, ces adresses URL seront affichées et aucun contenu ne sera envoyé à l'adaptateur de
sortie. Par défaut, cinq adresses URL placées en file d'attente sont affichées.

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande crawl, par exemple : `crawler testit --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`.

En outre, vous pouvez définir le nombre limite d'adresses URL placées en file d'attente qui sont affichées en tant qu'option de la commande testit, par exemple : `crawler testit --limit [number]`

## Exécution d'une exploration
{: #running-crawl}

Exécutez la commande suivante : `crawler crawl`

Cette commande permet d'exécuter une exploration avec le fichier de configuration par défaut (`crawler.conf`).

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande crawl, par exemple : `crawler crawl --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`.

## Redémarrage d'une exploration
{: #restarting-crawl}

Exécutez la commande suivante : `crawler restart`

Cette commande exécute un redémarrage d'exploration en démarrant une nouvelle exploration avec le fichier de configuration par défaut (`crawler.conf`).

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande restart, par exemple : `crawler restart --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`.

## Reprise d'une exploration
{: #resuming-crawl}

Exécutez la commande suivante : `crawler resume`

Cette commande permet de reprendre l'exécution d'une exploration à l'endroit où elle s'était arrêtée, avec le fichier de configuration par défaut (`crawler.conf`).

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande resume, par exemple : `crawler resume --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`.

## Actualisation d'une exploration
{: #refresh-crawl}

Exécutez la commande suivante : `crawler refresh`

La commande actualise une exploration précédente avec le fichier de configuration par défaut (`crawler.conf`).

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande refresh, par exemple : `crawler refresh --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`.
