# Documentation des vues

## 7 règles

1. Rédiger du point de vue du lecteur
2. Éviter la répétition inutile
3. Éviter l'ambiguïté (expliquer les formalismes utilisés)
4. Utiliser une organisaiton standard
5. Documenter l'exposé des motifs ("rationale")
6. Garder la documentation à jour
7. (Faire) réviser la documentation pour son aptitude à l'emploi ("fitness for purpose")

## Intérêts des parties prenantes

### Gestionnaire de projets
- cédule: module, complexité, dépendances
- assignation des ressources
- budget
- plan de contingence (livrer une partie du système?)

Agie sur:
=> vues affectation: attribution de tâches, déploiements.

=> modules: décomposition, utilise, couches

### Développeur
- Soumis à des contraintes dès le départ:
  - attributs de qualité à rencontrer
  - systèmes patrimoniaux
  - interfaces
  - budget, ressources
  - modèle de données
  - fonctionnalités à implémenter
  - librairies existantes à utiliser

Agie sur:
- modules + C&C (éléments logiciels)
- diagramme de contexte haut niveau

### Testeur et intégrateur
Testeur unitaire: même information que le développeur + emphase sur les specifications comportementales

Testeur boîte noir: documentation des interfaces des éléments

### Concepteur d'autres systèmes

- Interoperabilité avec d'autres systèmes. L'architecture définit les protocles nécessaires aux opérations du problème
  - On accès à la documentation des interfaces
  - Le modèle de données avec lequel les autres devront intéragir
  - Diagrammes de contexte de haut niveau

### Mainteneur

- Même information que les développeurs afin d'opérer les changements sous les mêmes constraintes.
- Accès à l'exposé des motifs afin de s'imprégner du raisonnement initial du développeur
  - Sauver du temps en ne se posant pas les mêmes questions.
- Localiser le changement: décomposition + utiliser

### Application ligne de produits

- Similaire à intégrateur plus: guide de variabilité des différentes vues modulaires et C&C

### Client

- Celui qui paye pour le système.
  - Progression des coûts et avancement du projet: une vue "filtrée" d'allocation des tâches
  - Vue déploiement: comment le système s'insère dans son parc d'équipement actuel

### Utilisateur

Peut certainement bénificier d'intuitions concernant le système, ce qu'il fait et comment on peut l'utiliser

### Analyste

S'intéresse à la capacité du design à rencontrer les objectifs de qualité du système.
- Performance: création de modèles afin de simuler des temps de calcul. Vues de processus et communication
- Précision/fiabilité: résultat attendu (testabilité)
- modifiabilité: jauger l'impact d'un changement: utilisations, décomposition, matrice DSM.
- sécurité: vue de déploiement afin d'identifier les connexions externes, vue C&C. flux de données et mécanismes de contrôle. Vue décomposition: modules responsables de l'authentification et l'intégrité.
- disponibilité: vues C&C de processus et communication. Identifier les mécanismes de redondance. Identifier l'interblocage potentiel. Vue de déploiement
- convivialité: décomposition modulaire afin d'analyser l'information présentée à l'utilisateur final.

### Support et infrastructure

- Responsable de la configuration et le maintien de l'environnement de:
  - développement
  - production
  - déploiement

### Nouvelle partie prenante

- Interessé à l'information de haut niveau, introduction au système, contraintes/arbitrages (exposé des motifs), vues de haut niveau.

### Futur architecte

Tout!

## Documentation des interfaces

Les éléments ont des interfaces avec lesquelles ils intéragissent:
- modules: services fournies
- composants: ports
- connectuers: rôles

Tout ce qui est visible de l'extérieur deveint, une forme de contrat, un engagement que l'élément rencontrera ses obligations _prescrites_.

Exemples d'interactions:
- appels de fonctions/méthodes
- requêtes web
- flux de données
- mémoire partagée
- messages/événements

### Organisation de la documentation des interfaces
1. Identité: nommer l'interfaced lorsque l'élément a plusieurs interfaces
2. Ressources: fournies/requis (méthodes, procédures, etc...)
  1. Syntaxe: signature de la ressource pour une utilisation adéquate
  2. Sémantique: résultat obtenu lorsqu'on utilise la ressource?
  - Paramètres et valeurs de retour
  - Changement dans l'état visible de l'extérieur
  - Effets secondaires sur l'environnement: destruction d'un objet?
  - Résultat observable via l'interface utilisateur
  - Mode d'exécution de la ressource: suspendu, bloqué, synchrone, etc..
  - Restriction à l'utilisation: initialisation nécessaire, niveau de permissions, thread safe, etc...
  3. Gestion des erreurs: conditions et exceptions soulevées par la ressource
3. Type de données: structures, classes, énumérations, enregistrements, etc...
  - Qui est responsable de la déclaration et l'assignation des valeurs
  - Opérations permises sur les membres
  - Mécanismes de conversion vers d'autres types
4. Gestion des erreurs: souvent préférable d'avoir un traitement des erreurs commun à un ensemble de ressources.
5. Variabilité: possibilité de paramétrer/configurer l'élément
  - Étalement des valeurs possibles pour les paramètres
6. Attributs qualité: performance, disponibilité, etc... attendue par le système. C'est le "combien" des scénarios de qualité
7. Exposé des motifs: contraintes, compromis, designs alternatifs
8. Guide: exemples concrets, sections de code, diagrammes de séquences, etc...
