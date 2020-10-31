# Patrons architecturaux

Il existe trois grand types de structures:
- **Module**:
  - éléments: unité d'implémentation basées sur le code
  - relations: dépend de, est un, utilise, est un sous-module, ...
- **Composant & Connector (C&C)**:
  - éléments: entités logicielles executables
  - relations: communique avec, transmet à, se synchro avec
  - exemples: client-server, données partagées, ...
- **Affectaction/Allocation**:
  - éléments: unités administratives, modules, composnats
  - relations: est attribué à, est testé par, ...
  - exemples: implémentation, déploiement, attribution de tâches, ...

## C&C

**Composant**: éléments calculatoires et de dépôt de données présents à l'exécution: processus, clients, serveur, entrepôt de données.

**Connecteur**: Les connecteurs sont des éléments logiciels de premier plan. Contraire aux vues modules où les relations sont dans les "connecteurs". Canaux d'interaction liens de communication, protocoles, flux d'information, accès aux données partagées


**TODO INSERT DIAGRAM PAGE 3 #1**

Dans C&C, les relations sont des "points d'attache".
- Les **ports** sont les interfaces des composants. Il s'agit d'un point d'interaction entre un composant et son environnement.
- Les **rôles** sont les interfaces des connecteurs. Ils définissent les façons que peuvent utiliser les composants dans les différents chemins d'interaction des connecteurs.

### Relations
1. "Attachment" point d'attache:
Le port "p" d'un composant est _attaché_ à un connecteur ayant un rôle "r" si le composant interagit via le connecteur utilisant l'interface prescrite par "p" en se conformant aux attentes de "r".

**TODO INSERT DIAGRAM PAGE 3 #2**

2. Délégation d'interfaces. Possibilité de décomposer un composant en sous-structures

**TODO INSERT DIAGRAM PAGE 3 #3**

### Propriétés
Propres à chaque style architectural (souvent reliées aux attributs de qualité.)

Exemple:
  - fiabilité: redondance, synchronisation, etc..
  - performance
  - fonctionnalité: fonction effectuée par un élément C&C
  - sécurité
  - colatéralité: multi-thread, interblocage
  - tier: dans quel tier réside le composant

### Spécialisation - type - instance
1. Spécialisation / type

**TODO INSERT DIAGRAM PAGE 3 #4**

2. Instanciation

**TODO INSERT DIAGRAM PAGE 3 #5**

### Styles de la famille C&C

Cette famille est divisé en 4 grandes familles:
1. Flux de données: calcul basé sur le flux des données à travers le système.
2. Appel-retour: les composants interagissent via des invoctations synchrones des différentes fonctionnalités offertes par les composants.
3. Événements: les composants interagissent via des messages ou événements asynchrones.
4. Dépôt de données: interactions via de large entrepôts de données partagées et persistantes dans le temps.

#### Pipe & filter

**TODO INSERT DIAGRAM PAGE 3 #6**

Éléments:
- filtre: composant transformant les données lues sur les ports d'entrées en d'autres données écrites sur les ports de sortie
- pipe: connecteur acheminent les données du port de sortie d'un filtre vers le port d'entrée d'un autre filtre.
  - Rôle unique "data in/out" préservant le séquencement des données et n'altérent pas le contenu

Utilité
- Améliore la réutilisation: indépendanxe des filtres.
  => modifiabilité ++, testabilité ++
- Améliore le début: calcul incrémental parallélisable. => performance ++
- Facilite la compréhension globale du système

#### Client-Serveur
Invocation du service par le client via un appel synchrone. Le client attend, ou est bloqué, jusqu'au moment où le fournisseur de services retourne la réponse.

#### Éléments
- client: composant invoquant le service
- serveur: composant fournissant le service
- connecteur: requête/réponse (request/reply)

#### Contraintes
- Clients et serveurs connectés via les connecteurs request/reply
- Le serveur peut-être client d'un autre serveur
- La spécialisation peut s'imposer:
  - le nombre d'attaches sur un port donné
  - relations permises entre les serveurs
  - protocole spécifique de communication

#### Utilité

- Modifiabilité et réutilisabilité en factorisant les services communs.
- Améliore la disponibilité et l'extensibilité avec la possibilité d'intégrer des serveurs de relève
- Analiser de façon globale les dépendances, le début et les possibles brèches de sécurité.

#### Architecture client-serveur à N-niveaux (N-tier)

- Préoccupations transverses ("crosscut") des composants: aggrégation des composants dans des regroupements hiérarchiques avec _restrictions_ sur les canaux de communications entre les composants.

### Publication abonnement

Forme possibles du style:
1. Invocation implicite: le composant s'abonne en enrgistrant une de ses procédures à un événement en particulier. La procédure est invoquée implicitement lorsque l'événement survient.
2. Routage complet: l'ensemble des événements sont acheminés aux composantes abonnées.
3. Bloquant: l'annonceur d'un événement peut bloquer jusqu'à ce que l'événement soit complétement traité par le système.

#### Utilité

- Transmettre des événements et messages à des destinataires inconnues.
- Découpler l'interface utilisateur du reste de l'application. Convivialité ++ Testabilité ++
- Réutilisation simple

### Égal à égal (Peer to peer)

- Communication de type requête/réplique sans l'asymétrie du style client-serveur.
- En principe, un composant peut intéragir avec n'importe quel autre composant en invoquant ses services.
- Composant "pair" agit à la fois comme client et serveur.
- Le connecteur requête/réplique fait le lien entre les pairs du réseau cherche et identifie les différents "pairs" du réseau en invoquent ses services.

#### Utilité

- Disponibilité ++
- Extensibilité ++: facile d'ajouter un noeud au réseau
- Permet la distribution à grande échelle: partage de fichier (bit torrent), messagerie (skype)
- Perfomance ++: haut débit

### Architecture orientée services (SOA)

- Collection de composants distribués fournissant/consommant des services.
- Technologies hétérogènes: composants potentiellement implémentés avec différents langages et executés dans différentes plateformes.

## Composants
- De base: dédiés à la production et/ou à la consommation de services.
- Spécialisés:
  - enterprise service bus (ESB)
    - Routage des messages
    - Convertir les données/protocoles
    - Gérer les transactions
    - Renforcer la sécurité
- Registre des services: permet d'enregistrer et effectuer des requêtes à l'exécution.
  - Association tardive des méthodes ('late binding time')
  - Modifiabilité ++
- Serveur d'orchestration: exécutent un script (une séquence) suivant l'arrivée d'un événement.
- Type appel/retour:
  - SOAP: dans la couche applicative (au dessus de http)
  - REST: extension du protocole http. (post, get, put, delete)
- Messages asynchrones: échange de messages de type Publication-abonnement ou point-à-point.

### En couches

- Modifiabililté: un changement dans un niveau inférieur se faire derrière les interfaces disponibles pour les couches supérieures.
- Portabilité: l'interface ne devrait pas exposer des fonction dépendantes de la plateforme d'utilisation.

#### Contraintes:

- Chaque partie du logiciel est alloué dans une seule couche.
- Au moins deux couches
- Pas de boucles circulaires
- Ponts à éviter

## Aspects



## Documentation

### Utilise
- Un programme P1 peut utiliser P2 sans l'appeler. Ex: P1 s'attend à ce que P2 laisse un résultat de calcul via une variable partagée. P1 utilise P2.
- P1 peut appeler P2 sans l'utiliser. Ex: P2 est un gestionnaire d'exception que P1 appelle lorsqu'il détecte une erreur. Le bon fonctionnement de P1 ne dépend pas de P2.
