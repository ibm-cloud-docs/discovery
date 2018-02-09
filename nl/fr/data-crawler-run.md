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

# Exécution de votre référentiel de données

Une fois les options d'exploration correctement configurés, vous pouvez exécuter un moteur d'exploration sur votre référentiel de données.
{: shortdesc}

Vous ne devez jamais exécuter le moteur d'exploration en tant qu'utilisateur `root`, sauf si vous avez besoin d'accéder à des fichiers lisibles uniquement par l'utilisateur `root`.
{: tip}

Exécutez la commande suivante : `crawler`

Le moteur d'exploration vous invite à lire la documentation qui explique ce qu'il faut faire. Vous pouvez exécuter une exploration test, ou exécuter une exploration, en plus d'autres options d'exploration. 

## Exécution d'une exploration test

Exécutez la commande suivante : `crawler testit`

Cette commande permet d'exécuter une exploration test qui explore uniquement l'adresse URL de départ et affiche les URL mises en file d'attente. Si l'adresse URL de départ est convertie en un contenu indexable (par exemple, il s'agit d'un document), ce contenu est envoyé à l'adaptateur de sortie, et il s'affiche à l'écran. Si
l'extraction de l'adresse URL de départ entraîne la mise en file d'attente d'adresses
URL, ces adresses URL seront affichées et aucun contenu ne sera envoyé à l'adaptateur de
sortie. Par défaut, cinq adresses URL placées en file d'attente sont affichées.

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande crawl, par exemple : `crawler testit --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`. 

En outre, vous pouvez définir le nombre limite d'adresses URL placées en file d'attente qui sont affichées en tant qu'option de la commande testit, par exemple : `crawler testit --limit [number]`

## Exécution d'une exploration

Exécutez la commande suivante : `crawler crawl`

Cette commande permet d'exécuter une exploration avec le fichier de configuration par défaut (`crawler.conf`).

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande crawl, par exemple : `crawler crawl --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`. 

## Redémarrage d'une exploration

Exécutez la commande suivante : `crawler restart`

Cette commande exécute un redémarrage d'exploration en démarrant une nouvelle exploration avec le fichier de configuration par défaut (`crawler.conf`).

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande restart, par exemple : `crawler restart --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`. 

## Reprise d'une exploration

Exécutez la commande suivante : `crawler resume`

Cette commande permet de reprendre l'exécution d'une exploration à l'endroit où elle s'était arrêtée, avec le fichier de configuration par défaut (`crawler.conf`).

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande resume, par exemple : `crawler resume --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`. 

## Actualisation d'une exploration

Exécutez la commande suivante : `crawler refresh`

La commande actualise une exploration précédente avec le fichier de configuration par défaut (`crawler.conf`).

Vous pouvez également spécifier un fichier de configuration personnalisée en tant qu'option dans la commande refresh, par exemple : `crawler refresh --config [config/myconfigfile.conf]`

Le chemin d'accès au fichier de configuration transmis via l'option `--config` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif, tel que `config/myconfigfile.conf` ou `./myconfigfile.conf`, ou au format de chemin d'accès absolu, tel que `/path/to/config/myconfigfile.conf`. 
