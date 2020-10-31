# Attributs de qualité

## Disponibilité

S'intéresse aux défaillances et aux fautes du système.

En défaillance, on s'intéresse au temps de réparation:

  alpha = MTTF / (MTTF + MTTR)

  MTTF = Mean Time To Failure (temps moyen entre deux pannes)
  MTTR = Mean Time To Repair (temps moyen pour réparer)

### Scenario
- **Source**: distinction entre interne et externe au système
- **Stimulus**:
    - Omission: le composant échoue a répondre
    - Crash: omission a répétition
    - Minutage: réponse arrive en avance ou en retard
    - Réponse: composant répond avec une valeur incorrecte
- **Artéfacts**: la ressource qui doit être hautement disponible (base de données, balanceur, ...)
- **Environnement**: état du système quand la faute **survient**
- **Réponse**: détection de la faute, basculement, notification, ...
- **Mesure de la réponse**: temps de réparation, % de disponibilité

### Tactiques architecturales

1. Les tactiques peuvent complémenter d'autres tactiques.

...Ex: Tactique de redondance: Disponibilité ++
...=> stratégie de synchronisation
...=> load balancing: Performance ++

2. Collection de tactiques ~= patrons architecturaux

3. L'objectif des tactiques est de contrôler en amont la réponse d'un stimulus.

Le but est d'empêcher la faute de devenir une défaillance ou du moins, borner l'impact d'une panne.

INSERT DIAGRAM disponibilité #1

Nous avons trois grandes approches:
1. Détecter les pannes
2. Réparer les pannes (fault recovery)
  - Préparer le système à être réparable
  - Réintroduction d'un composant
3. Prévenir les pannes

#### Détection des pannes
- Pins/echo: émettre un ping et un autre composant réponds dans un temps prédeterminé
- Pulsation: version bonifiée du ping/echo. On émet un ping de manière périodique
- Exception: soulevée lorsqu'une faute survient

#### Réparation des pannes
- Votation: processus executé sur plusieurs composants, plusieurs réponses sont envoyées au voteur. Permet d'identifier le processus/composant fautif.
- Redondance active: typiquement, tous les composants redondants répondent et la première réponse est conservée par le client.
- Redondance passive (_warm spare_): mise à jour périodique des backups. Un temps de mise à jour est nécessaire.
- Rechange (_cold spare_): un système pré-configuré en attente de remplacer des composants.

##### Réintroduction
- Arrière-plan: s'assurer du fonctionnement du composant avant de le réintroduire
- Resynchronisation: mise à jour de l'état avant la réintroduction.
- Rollback: état incohérent détectée. -> Pointes au dernier état stable

#### Prévention des pannes
- Retirer les services: retrait volontaire d'un composant/service afin de prévenir une panne.
- Transactions: regroupement séquentiel d'étapes que l'on peut refaire/défaire.
- Monitoring: créer une nouvelle instance lorsqu'un processus fautif est détectée.

## Performance

La performance s'intéresse au minutage (timing) des événements qui arrivent dans le système.

La quantité et la provenance des événements affectent la performance.

### Scénario

- **Source**: le stimulus arrive de sources (potentiellement multiples) externe ou interne.
- **Stimulus**: représente l'arrivée des événements en différentes catégories:
  - Périodique
  - Sporadique:
  - Stocastique: distribution probabiliste aléatoire (distribution de poisson par exemple)
- **Artéfacts**: le système et ses services
- **Environnement**: différents modes d'opération (normales, surchages, hors ligne, en ligne, ...)
- **Réponse**: Le traitement de l'événement pouvant causer un changement dans l'environnement
- **Mesure de la réponse**: temps pris par le système pour répondre à l'événement. S'exprime de différentes façon:
  - Latence (délais)
  - Débit (throughput): événements, opérations par seconde
  - Échéance (deadline): au sens "temps maximum alloué"
  - Sautillement (jitter): déplacement saccadé, irrégulier par rapport à la valeur normales. Variation du temps de traitement.
  - Taux d'omission (miss rate): ratio des événements perdus ou erronés sur le total.
  - Perte de données

### Tactiques architecturales

INSERT DIAGRAM performance #1

Deux grandes contributions au temps de réponse:
 1. Consommation de ressources: CPU, mémoire, disque, bande passante, ...
 2. Temps de blocage: contention/disponibilité des ressources, dépendance avec d'autres composants

#### Demande de ressources
- Efficacité calculatoire/algorithmique
- Réduire l'arrivée des événements: modification de la fréquence d'échantillonnage par exemple
- Réduire les intermédiaires (contradiction avec une tactique de modifiabilité)
- Borner le temps d'exécution

#### Offre des ressources
- Colateralité (concurrency): exécution en parallèle, équilibrage des charges (load balancing)
- Copies de données: utilisation de zones tampons pour éviter la contention d'une ressource (exemple: cache vs ram)
- Ajouter des ressources: simple a proposer mais souvent difficile  à justifier (augmentation)

#### Arbitrage des ressources
- Stratégie d'ordonnancement:
  - FIFO
  - priorités fixes: selon importance de la tâche, sa deadline, etc...
  - priorités dynamiques: round-robin, priorisations des événements arrivant à échéance

## Modifiabilité

Concerne le coût (au sens large) du changement.

Deux préoccupations:
1. Qu'est-ce qui peut changer (artéfact)
2. Quand est-ce que le changement arrive

### Scénario

- **Source**: qui effectue le changement ou la demande.
- **Stimulus**: le changement à effectuer. On peut ajouter/modifier/retirer une fonctionnalité. La demande peut concerner un attribut de qualité.
- **Artéfacts**: partie du système sur laquelle le changement s'opére: fonction, plateforme, interface utilisateurs, envrionnement d'exécution, un canal de communication, ...
- **Environnement**: à quel moment on effectue le changement: implémentation, compilation, tests, configuration, déploiement, maintenance, ...
- **Réponse**: l'entité effectuant le changement doit localiser le changement,
- **Mesure de la réponse**: coût du changement (temps, argent, effort, ressources, retard sur d'autres projets)

### Tactiques architecturales

1. Réduire le nombre de modules affectés:
  - coût d'une modification: moins de modules affectés, moins cher que ça coûte
2. Limiter les modifications à un module local.:
  - Notion de dépendance indirecte
  - effet ricochet (doit modifier B pour modifier A)
3. Réduire le temps et coût de déploiement

#### Localiser le changement
- Cohérance sématique: relations et responsabilité d'un module.
  - couplage et cohésion (anticipation de changements, limiter les options possibles)
- Généralisation: élargir la portée des fonctions

#### Limiter l'effet ricochet
- Types de dépendances: syntaxique, sémantique, séquencement, identité, ...
- Masquer l'information: quelques interfaces publiques seulement
- Intermédiaires:
  - Données: proxy, repository, MVC, publications-abonnement, factory, ...
  - Syntaxe: façade, bridge, médiateur, proxy, factory, ...

#### Retarder le moment d'association
- Permettre de prendre certaines décisions au moment de charger l'application en mémoire ou lord de l'exécution.
  - Fichiers de configuration/protocoles
  - Polymorphisme
  - Enregistrement/remplacement de composants à l'exécution: plug & play, publication-abonnement

## Sécurité

De façon générale, la sécurité se mesure par la capacité à résister à des accès non autorisés.

Plusieurs dimensions:
 - Confidentialité: protection contre des accès non autorisés.
 - Intégrité: données et services rendus tels qu'intentionnés
 - Disponibilité: système disponible pour les utilisateurs légitimes
 - Nonrepudiation: possibilité de vérifier que l'émetteur et le destinataire sont bien les parties ayant respectivement envoyé ou reçu le message
 - Assurance (authentication): l'autre partie est celle qu'elle prétend être
 - Audits: reconstruire a posteriori ce qui c'est passé

### Scénario

- **Source**: la source de l'attaque peut-être humaine ou un autre système
- **Stimulus**: une attaque ou tentative de brisé la sécurité
- **Artéfacts**: l'attaque cible un service, un processus ou les données du système
- **Environnement**: état du système au moment de l'attaque
- **Réponse**: autoriser les utilisateurs légitimes. Rejeter l'accès aux autres. Permettre l'octroi et le retrait de permissions.
- **Mesure de la réponse**: difficulté d'organiser une attaque

### Tactiques architecturales

#### Résister aux attaques
  - Authentification des usagers: mots de passe complexes, expiration des mots de passes, certificats numérique, biométrie, etc...
  - Gestion des accès: niveaux de permissions, groupes et rôles
  - Confidentialité: encryption des données et canaux de communication
  - Intégrité des données: somme de contrôle, hachage
  - Limiter l'exposition et l'accès: répartir les services sur plusieurs hôtes, aucun ne permettent l'accès à tout. Ex: parefeu avec zones (DMZ)

#### Détecter les attaques

  - Systèmes de détection d'intrusion: analyse du traffic réseau et recherche de patterns. Analyse de paquets/protocoles/messages

#### Se relever d'une attaque

  - Retrouver l'état fonctionnel: tactiques de disponibilité, le système est en panne
  - Identifier l'attaquant: piste d'audit, liste des contrôle des accès, profile des utilisateurs.

## Testabilité

La testabilité est la facilité pour un logiciel à montrer ses défauts.
Ou encore la probabilité (en supposant que le système contient au moins un défaut) que la prochaine exécution des tests résulte en une panne.

### Scénario
- **Source**: test unitaire, intégration, système, développeur, groupe externe, ...
- **Stimulus**: rencontre d'un jalon (milestone) dans le cycle de vie du logiciel
- **Artéfacts**: design, section de code, système en entier
- **Environnement**: phase de design, développement, compilation, déploiement, maintenance
- **Réponse**: basée sur l'observabilité et la contrôlabilité lors de l'exécution des tests
- **Mesure de la réponse**: pourcentage de couverture, nombre d'instructions testées, tempous pour performer les tests. Probabilité qu'une faute existe.

### Tactiques architecturales

Faciliter les tests (montrer les défauts) d'une application lorsqu'un nouvel incrément se termine.

#### Capturer les entrées/sorties
  - Enregistrements: sauvegarde des données, réutilisation d'un scénario de test.
  - Séparer l'interface de l'implémentation: permet de substituer des composants dans une section (patron Proxy)
  - Créer des interfaces de tests spécialisés: séparation du fonctionnement régulier pour un scénario de test bien précis

#### Monitoring interne
  - Composant dédié capturant l'état actuel du système: charge, performance, ressources, piste audit, ...

## Conviviabilité (usability)

S'intéresse à la facilité avec laquelle l'utilisateur accomplit sa tâche et le niveau de support offert par le système.

Plusieurs dimensions:
  - Apprentissage des fonctionnalités du système
  - Utilisation efficace du système
  - Minimiser l'impact des erreurs
  - Adaptation du système au besoin de l'utilisateur
  - Accroissement de la confiance et de la satisfaction du client

### Scénario

- **Source**: toujours l'utilisateur final
- **Stimulus**: volonté exprimée par l'utilisateur d'utiliser efficacement le système, apprendre de nouvelles fonctionnalités et se sentir confortable avec le système
- **Artéfacts**: toujours le système ou une partie spécifique
- **Environnement**: à l'exécution ou lors de la configuration
- **Réponse**: proposer ou même anticiper les fonctionnalités demandées
- **Mesure de la réponse**: temps d'exécution d'une tâche, nombre d'étapes, taux d'erreur, niveau de satisfaction, niveau de connaissance, données et temps perdu

### Tactiques architecturales

  1. Faciliter le travail de l'utilisateur
  2.  Fournir le support approprié

#### Durant l'exécution
  - Fournir une rétroaction sur l'état actuel du système (progrès, étapes, ...)
  - Possibilité d'émettre des commandes de base: undo/redo, grouper, afficher, ...
  - Maintenir une cohérence:
    - de la tâche: qu'est-ce que l'utilisateur tente d'accomplir? Anticiper les prochaines étapes
    - de l'utilisateur: quel est le niveau de connaissance de l'utilisateur? Proposer un niveau de support adapté
    - du système: comportement attendu du système et niveau de rétroaction attendu

#### Durant la phase de design

  - Séparation de l'interface utilisateur du reste de l'application (MVC, PAC, MVVM, MVI,)
