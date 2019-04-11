---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-01-15"

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

# Analyse syntaxique de contrats
{: #contract_parsing}

Element Classification renvoie des contrats analysés syntaxiquement, avec une analyse de chaque élément identifié.

Les sections suivantes expliquent de quelle manière l'analyse est fournie par l'objet JSON renvoyé.

## Types
{: #contract_types}

Le tableau `types` inclut un certain nombre d'objets, contenant chacun les clés `nature` et `party` dont les valeurs identifient un distique pour l'élément.

Les tables suivantes recensent les valeurs possibles pour les clés `nature` et `party` :

| `nature`         |Description                                                |
|:----------------:|-----------------------------------------------------------|
|`Definition`      |Cet élément permet de clarifier un terme, une relation ou d'autres objets similaires. Aucune action n'est requise pour respecter l'élément, et aucune partie prenante n'est concernée.|
|`Disclaimer`      |L'objet `party` de l'élément n'est pas tenu de respecter les termes spécifiés par l'élément mais il ne lui est pas interdit de le faire.|
|`Exclusion`       |L'objet `party` de l'élément ne respectera pas les termes spécifiés par l'élément.|
|`Obligation`      |L'objet `party` de l'élément est tenu de respecter les termes spécifiés par l'élément.|
|`Right`           |L'objet `party` de l'élément est assuré de recevoir les termes spécifiés par l'élément.|

Chaque clé `nature` fonctionne en paire avec une clé `party`, laquelle contient le nom ou le rôle de la ou les parties prenantes s'appliquant à la nature (exemples (non exhaustifs) : `Buyer`, `IBM` ou `All Parties`). Notez que pour la nature `Definition`, la partie prenante est toujours `None`.

## Parties
{: #contract_parties}

Le tableau `parties` présente les participants répertoriés dans le contrat. Chaque objet `party` est associé à d'autres objets qui fournissent des détails sur la partie prenante, notamment :

  - `role` : rôle de la partie prenante. Les valeurs sont répertoriées dans le tableau qui suit la liste.
  - `importance` : importance de la partie prenante. Les valeurs possibles sont `Primary` pour une partie prenante principale et `Unknown` pour une partie prenante non principale.
  - `addresses` : tableau qui identifie les adresses.
    - `text` : adresse.
    - `location` : emplacement de l'adresse, tel qu'il est défini par ses index `begin` et `end`.
  - `contacts` : tableau qui définit les noms et les rôles des contacts identifiés dans le document d'entrée.
    - `name` : nom d'un contact.
    - `role` : rôle du contact.

Les valeurs de `role` pouvant être renvoyées pour des contrats incluent, mais ne se limitent pas à :

| `role`           |Description                                                |
|:----------------:|-----------------------------------------------------------|
|`Buyer`           |Partie prenante chargée du paiement des biens ou des services mentionnés dans le contrat.|
|`End User`        |Partie prenante qui interagit avec les biens ou les services fournis ; se distingue explicitement de l'élément `Buyer`.|
|`None`            |Aucune partie prenante n'a été identifiée pour l'élément.|
|`Supplier`        |Partie prenante chargée de la distribution des biens ou des services mentionnés dans le contrat.|

## Categories
{: #contract_categories}

Le tableau `categories` définit le sujet traité dans la phrase. 

Les catégories et les descriptions de ce tableau dépendent des lois en vigueur aux Etats-Unis et peuvent ne pas s'appliquer dans d'autres pays.
{: important}

Les catégories actuellement prises en charge sont notamment les suivantes :

| `categories`     |Description                                                |
|:----------------:|-----------------------------------------------------------|
|`Amendments`      |Eléments qui spécifient les corrections apportées au contrat après qu'il a été signé ou les modifications apportées à un contrat standard. Inclut des discussions des conditions pour le changement des termes d'un contrat.|
|`Asset Use`       |Eléments qui font référence à la façon don une partie prenante peut utiliser ou non les actifs d'une autre partie. Ceci s'applique de manière spécifique à une partie prenante ayant accès à ou utilisant des actifs tels que des licences, de l'équipement, des outils ou du personnel de l'autre partie tout en remplissant ses obligations conformément à l'accord, permissions et restrictions qui en découlent incluses.  Cela ne s'étend pas aux spécifications des obligations ou droits d'une partie prenante concernant des biens, services, licences acquis, etc., car ceux-ci appartiennent aux actifs propres de la partie plutôt qu'aux actifs d'une autre partie.|
|`Assignments`     |Eléments qui décrivent la cession des droits et/ou des obligations à une partie prenante.|
|`Audits`          |Eléments faisant référence au droit d'une partie prenante d'examiner ou réviser la conformité, ou aux exigences qu'une partie doit respecter pour l'inspection ou l'examen de conformité. Ceci inclut des références à la conservation des enregistrements (principalement car faisant référence au doit d'inspection) et à la maintenance et la conservation des enregistrements d'activité qui pourraient être examinés.|
|`Business Continuity`|Eléments faisant référence aux conséquences si la totalité de l'activité de l'une des parties était vendue.|
|`Communication`  |Elément faisant référence aux exigences de communiquer, répondre, notifier ou fournir des mentions légales ; ou bien informations concernant les modifications apportées au contrat. Inclut également des références aux détails concernant les méthodes de communication, l'acte ou le processus d'échange d'informations, ainsi que les moyens acceptables d'échanger des informations entre parties prenantes (ainsi que d'autres parties n'étant pas nécessairement directement impliquées dans le contrat).|
|`Confidentiality` |Eléments décrivant la façon dont les parties prenantes peuvent ou non utiliser des informations apprises au cours de l'exécution du contrat et à compter de celui-ci. Inclut également des discussions sur les informations devant être tenues confidentielles, telles que la conservation de secrets commerciaux ou la non divulgation d'informations commerciales.|
|`Deliverables`    |Eléments spécifiant les articles, tels que des biens ou des services, qu'une partie prenante fournit à une autre selon les termes du contrant, généralement en échange d'un paiement. Inclut la discussion concernant la préparation des livrables.|
|`Delivery`        |Eléments qui spécifient les moyens ou modes de transfert des livrables (choses, par opposition aux services de personne) depuis une partie prenante vers une autre. Inclut des discussions sur les caractéristiques de livraison, comme la planification ou l'emplacement.|
|`Dispute Resolution`|Eléments traitant des provisions pour règlement de différend (par exemple, au sujet de la main-d'oeuvre, des factures ou de la facturation) pouvant surgir entre les parties contractantes.  Les exemples de provision peuvent inclure le versement selon une procédure définie, comme un panel d'arbitrage, un processus pour l'obtention d'une injonction, l'abandon d'un droit à procès ou l'interdiction de poursuite d'un recours collectif. Inclut également des références à la loi applicable ou au conflit de droit du contrant, par exemple un pays ou une juridiction spécifique. |
|`Force Majeure`   |Elément qui font référence à des événements inattendus ou perturbateurs hors du contrôle d'une partie prenante et qui pourraient empêcher cette partie de remplir ses obligations contractuelles.|
|`Indemnification` |Eléments qui spécifient la résolution de certains engagements, quand une partie du contrat a la charge de version une compensation à une autre partie suite à une perte ou des dommages subis pendant la durée du contrat ou causée par les circonstances du contrat. Inclut également des références à toute dispense légale suite à des pertes ou dommages.|
|`Insurance`       |Eléments faisant référence à la couverture d'assurance ou aux termes de la couverture fournie par une partie à une autre (y compris les parties tierces telles que des sous-traitants ou autres). Inclut différentes assurances, notamment l'assurance médicale.|
|`Intellectual Property`|Eléments qui discutent de l'affectation des droits (droits d'auteur, brevets et secrets commerciaux, par exemple) aux parties prenantes du contrat. Inclut des référence aux brevets, droits de demande de brevet, marques, noms commerciaux, logos, noms de domaine, droits d'auteur, ainsi que toute application et enregistrement de tels schémas, modèles industriels, inventions, paternité, savoir-faire, secrets commerciaux, programmes logiciels et autres informations de propriété intangibles. Inclut également la discussion des conséquences de la violation des droits de propriété intellectuelle.|
|`Liability`       |Eléments qui décrivent la méthode utilisée pour déterminer quand et comment les torts sont imputés à une partie prenante. Des exemples peuvent inclure, sans être limités à, des instructions concernant la limitation de responsabilité, des réclamation de tiers, ainsi que des réparations, remplacements ou remboursements tels qu'exigés de la partie en faute.|
|`Payment Terms & Billing`|Eléments qui détaillent comment et quand une partie prenante doit payer ou être payée, ainsi que les articles ou frais pour lesquels les parties paieront ou seront facturées. Inclut des références aux modes de paiement ou mécanismes de paiement.|
|`Pricing & Taxes` |Eléments qui font référence à des montants ou des chiffres spécifiques associés à des livrables individuels qui sont échangés (par exemple, combien quelque chose coûte) en vue de satisfaire les termes du contrat. Inclut des références à des chiffres ou méthodes spécifiques de calcul des prix ou des montants de taxe.|
|`Privacy`         |Eléments concernés par le traitement des informations personnelles sensibles, concernant généralement leur protection (par exemple, pour satisfaire les réglementations en vigueur telles que le RGPD).|
|`Responsibilities`|Eléments qui discutent des tâches accessoires au contrat qui sont sous le contrôle d'une seule partie, spécifiquement centrées sur la discussion de supervision des employés.|
|`Safety and Security`|Eléments faisant référence à la sécurité physique ou la protection de cybersécurité des personnes, données ou systèmes. Des exemples incluent des discussions sur les vérifications d'historique, précautions de sécurité, la sécurité de l'espace de travail, les protocoles d'accès sécurisé et les défauts de produit pouvant présenter un danger.|
|`Scope of Work`   |Eléments qui définissent ce qui se trouve dans le contrat versus ce qui ne s'y trouve pas ; en conséquence, ce qui est promis d'être fait. Des exemples incluent des instructions définissant une commande spécifique ou décrivant les buts ou objectifs exposés dans le contrat.|
|`Subcontracts`    |Eléments qui font référence au recrutement de parties prenantes pour effectuer certaines tâches dans le cadre du contrat, et permissions, droits, restrictions et conséquences relatifs à ces tâches et qui en découlent.|
|`Term & Termination`|Eléments qui font référence à la durée du contrat, au planning et aux modalités de résiliation de contrat, ainsi que les conséquences de la résiliation, y compris les obligations qui s'appliquent au moment ou après la résiliation.|
|`Warranties`      |Eléments qui font référence aux promesses et obligations en cours définis au contrat et qui sont actuellement vraies et continueront de l'être dans le futur. Eléments discutant des conséquences liées à la rupture de telles promesses ou obligations, et les droits à réparation à la situation (y compris, mais non limité à, la demande de dommages). Cette catégorie ne s'applique pas aux éléments purement concernés par des instructions de représentation (instructions de fait sur le passé ou le présent), ou aux éléments qui font des suppositions quant aux choses qui se sont produites dans le passé.|

## Attributes
{: #attributes}

Le tableau `attributes` indique les attributs identifiés dans la phrase. Chaque objet du tableau comporte trois clés : `type` (le type de l'attribut de la table suivante), `text` (le texte applicable), et `location` (les index `begin` et `end` de l'attribut dans le document d'entrée). Les attributs actuellement pris en charge sont notamment les suivants :

| `attributes`     |Description                                                |
|:----------------:|-----------------------------------------------------------|
|`Address`         |Adresse postale.                                          |
|`Currency`        |Valeur et unités monétaires.                                  |
|`DateTime`        |Date, heure, plage de dates ou intervalle.                   |
|`Location`        |Emplacement géographique ou région.                         |
|`Organization`    |Organisation.                                           |
|`Person`          |Personne.                                                  |

## Dates d'effet
{: #effective_dates}

Le tableau `effective_dates` identifie les dates pendant lesquelles le document est appliqué.

| `effective_dates`|Description                                                |
|:----------------:|-----------------------------------------------------------|
|`text`            |Date d'effet, répertoriée sous la forme d'une chaîne.                     |
|`confidence_level`|Niveau de fiabilité de l'identification de la date d'effet. Les valeurs possibles sont `High`, `Medium` et `Low`.|
|`location`        |Emplacement de la date, tel qu'il est défini par ses index `begin` et `end`.|

## Montants des contrats
{: #contract_amounts}

Le tableau `contract_amounts` identifie les montants monétaires spécifiés dans le document.

| `contract_amounts`|Description                                               |
|:----------------:|-----------------------------------------------------------|
|`text`            |Montant du contrat, répertorié sous la forme d'une chaîne.                  |
|`confidence_level`|Niveau de fiabilité de l'identification du montant du contrat. Les valeurs possibles sont `High`, `Medium` et `Low`.|
|`location`        |Emplacement du montant du contrat, tel qu'il est défini par ses index `begin` et `end`.|

## Dates de fin
{: #termination_dates}

Le tableau `termination_dates` identifie les dates de fin du document.

| `contract_amounts`|Description                                               |
|:----------------:|-----------------------------------------------------------|
|`text`            |Date de fin, répertoriée sous la forme d'une chaîne.                  |
|`confidence_level`|Niveau de fiabilité de l'identification de la date de fin. Les valeurs possibles sont `High`, `Medium` et `Low`.|
|`location`        |Emplacement de la date de fin, tel qu'il est défini par ses index `begin` et `end`.|

## Provenance
{: #provenance}

Chaque objet des tableaux `types` et `categories` inclut un tableau `provenance_ids`. Le tableau `provenance_ids` possède une ou plusieurs clés. Chaque clé est une valeur hachée que vous pouvez envoyer à IBM pour fournir des commentaires ou recevoir du support.
