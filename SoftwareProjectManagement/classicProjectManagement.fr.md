# Gestion de projet plus classique

## Introduction

Les problèmes les plus fréquents sont la planification, estimation, coordination et contrôle, mesure, communication et gestion des risques.

Les 4 grands référentiels à connaitre sont:
- le CMMI présente les processus de gestion de projets logiciels;
- ISO/IEEE 12207, liste toutes les activités obligatoires/optionnelles pour un projet de génie logiciel;
- ISO/IEEE 16326, présente le plan de projet normalisé de l'ingénieur logiciel;
- le PmBok, organisation de certification pour la gestion de projet en général (pas spécialisé en logiciel).

Avec une approche classique, nous ne controlons pas:
- les parties prenantes décident du succès d'un projet;
- l'équipe qui est souvent imposée;
- on ne peut pas plaire à tous les intervenants;
- si on ne fait pas un contrôle régulier de chaque membre de l'équipe il y a de grandes chances que le projet déraille;
- il y aura sans doute des changements.

## Processus de planification de projet

Élaborer le plan de projet:
- Description de la situation actuelle
- Décrire les objectifs d'affaires
- Décrire le système existant
- Décrire les limites du prijet
- Décrire la structure de découpage du projet (WBS)
- Lister les produits livrables visés
- Établir les critères d'acceptation du produit
- Identifier les contraintes
- Lister les hypothèses
- Présenter l'organigramme des participants
- Décrire les parties prenantes, comités, documentation et tests
- Détailler chaque mécanisme de gestion de projet:
  - Gestion de l'intégration
  - Gestion des délais
  - Gestion des coûts
  - Gestion de la qualité
  - Gestion des RH
  - Gestion des communications
  - Gestion des risques
- Réalisation
- Échéancier détaillé préliminaire

## Techniques de planification

~ cOMPLETE ~

### Découpage d'un projet WBS

- Subdiviser le projet en unités gérables (des Jalons)
- Le WBS est aussi nommé Jalonnement d'un projet
- Un Jalon est associé à une activité qui permet de faire le point sur l'avancement du projet
- Ses bénéfices sont:
  - meilleure planification: la décomposition facilite l'estimation des durées à accorder à chaque opération. Elle donne en outre une vision globale du travail à faire grâce à une représentation visuelle;
  - maitrise du suivi: la décomposition des livrables facilite le management global du projet: affecter des jalons, revoir l'articulation des travaux, etc;
  - meilleure communication: elle simplifie les échanges entre les parties prenantes du projet et fait gagner du temps à tous en offrant une vision exhaustive des différentes phases;
  - meilleure gestion des couts: l'allocation des moyen et leur suivi sont plus précis, L'élaboration d'un buget prévisionnel est facilitée;
  - meilleure gestion des risques: identification des zones critiques et mise en place de scénarios préventifs.

### Estimation d'une activité

**La technique Delphi** (en équipe) propose:
- Étape 1: le modérateur prépare une courte présentation du projet ou demande à un client, un analyste, un chef de produit de présenter sa problématique
- Étape 2: Le modérateur demande les estimations individuelles à 3 experts
- Étape 3: Chaque expert fait son estimation dans son coin, comme il le souhaite
- Étape 4: Le modérateur collecte les résultats (anonymes) et calcule la moyenne
- Étape 5: Le modérateur informe les experts de cette moyenne (on peut l'écrire sur un tableau blanc par exemple): chacun peut alors évaluer sa propre estimation par rapport à cette moyenne. On échange sur les résultats, on argumente...Fin du 1er tour.
- Étape 6: Le modérateur demande à nouveau les estimations individuelles aux experts qui livrent encore leur estimation
- Étape 7: Le modérateur collecte à nouveau les résultats et calcule la moyenne
- Étape 8: Le modérateur informe les experts de cette moyenne. Il y a de nouveau discussion...Fin du 2ème tour...

**L'estimation descendante** (individuelle) propose:
- Étape 1: L'estimateur établi l'effort nécessaire (j) pour un module _Simple/Moyen/Complexe_
- Étape 2: Il découpe les modules à effectuer selon leur complexité
- Étape 3: Additionne l'effort total de l'itération
- Étape 4: Multiplie par un facteur de risque

**la technique de taille fonctionnelle (Points de fonction)** (à deux) propose:
- Étape 1: L'estimateur établi les frontières du logiciel à estimer
- Étape 2: Identifie les Entrées/Sorties
- Étape 3: Identifie les Mouvements de données
- Étape 4: Additionne le total des Points de fonctions
- Étape 5: Identifie la valeur, en J/P, selon la bd (ISBSG)[https://www.isbsg.org] ou ses données historiques
- Étape 6: Compare avec un collègue (fait la moyenne)

**La technique d'estimé ascendante** (seul) propose:
- Assigner un estimé en jours sur votre découpage WBS détaillé et additionner.

### Mesurer et contrôler le projet

1. Décider de la fréquence de votre rapport d'avancement
2. Gérer les écarts:
  - Prolonger la durée du prijet
  - ajouter plus de ressources
  - utilisant des ressources plus spécialisées
  - améliorer divers éléments du processus de développement
  - améliorer la technologie et / ou
  - réduire les fonctionnalités à livrer.
3. Mesurer et contrôlet les livrables:
  - effort en jours: quantité de travail dépensée pour diverses activités
  - calendrier en jours: réalisation des jalons mesurés de manière objective (activités effectuées, en cours ...)
  - coût en $: dépenses pour divers types de ressources, y compris les efforts
  - progrès en %: travaux terminés, acceptés et définis
  - caractéristiques du produit: exigences mises en oeuvre et dont l'efficacité a été démontrée.
  - attributs de qualité du projet: défauts (nombre), fiabilité (%), disponibilité (%), ...
  - risque en jours ou en $ supplémentaires: état des factueurs de risque et action d'atténuation

**Post-Mortem**: permets de tirer des leçons et donc améliorer le processus.

### Élaborer le plan de projet

- **Le processus de gestion de l’intégration** : Cette activité consiste à coordonner
adéquatement les divers éléments du projet. Elle comporte la mise en œuvre du plan de
projet et le contrôle intégré des changements. Les décisions suite à une demande de
changement devraient être prises à l’intérieur de 5 jours suivant la date de la demande. La
même durée doit être allouée pour la prise de décision d’un point en suspens.
- **Le processus de gestion du contenu** : Cette activité consiste à s’assurer que toutes les
activités nécessaires au succès du projet, et seulement celles-ci, font partie du projet. Elle
comporte le démarrage, la planification du contenu, la définition, la vérification du contenu,
et le contrôle des modifications du contenu.
- **Le processus de gestion des délais** : Cette activité comprend les processus nécessaires
pour s’assurer que le projet contient tout le travail requis, et uniquement celui-ci, pour
assurer la bonne fin du projet. Elle comporte l’identification et le séquencement des
activités, l’estimation de la durée des activités, l’élaboration et le contrôle de l’échéancier.
- **Le processus de gestion des couts** : Cette activité consiste à effectuer le suivi des couts
nécessaires à la réalisation du projet pour s’assurer que le projet soit réalisé en respectant
le budget approuvé. Elle est constituée de la planification des ressources, l’estimation des
couts, la budgétisation et le contrôle des couts.
- **Le processus de gestion de la qualité** : Cette activité consiste à s’assurer que le projet
réponde aux besoins pour lesquels il a été entrepris. Elle comporte la planification,
l’assurance et le contrôle de la qualité. Puisqu’atteindre la satisfaction des mandataires
(utilisateur et client) est un des principaux objectifs du projet, il est important que le
progrès vers ce but soit évalué formellement et périodiquement. Ceci se produit lors de
l'atteinte des jalons importants principaux du projet (par exemple, confirmation de la
conception de l'architecture du logiciel, revue technique d'intégration du logiciel). Les
variations par rapport aux exigences établies sont identifiées et les actions appropriées
d’ajustements sont mises en oeuvre.
- **Le processus de gestion des ressources humaines** : Cette activité consiste à s’assurer
de l’utilisation la plus efficace possible des ressources dans le projet. Elle comporte la
planification de l’organisation, l’obtention des ressources humaines et le développement
de l’équipe.
- **Le processus de gestion des communications** : Cette activité consiste à effectuer, la
collecte, la diffusion, l’archivage et, par la suite, le traitement final des informations
concernant le projet, de façon adéquate et en temps voulu. Elle est constituée de la
planification de la communication, la diffusion de l’information (gestion du changement),
les rapports d’avancement et la clôture administrative.
- **Le processus de gestion des approvisionnements** : Cette activité consiste à assurer
l’obtention des produits et des services qui permettent de réaliser le contenu du projet, de
l’extérieur de l’entreprise. Elle comporte la planification des approvisionnements, la
préparation des appels d’offres, les appels d’offres, le choix des fournisseurs, la gestion
administrative des contrats et la clôture des contrats. Préparer et exécuter les contrats
avec des fournisseurs, surveiller l'exécution du fournisseur, et accepter les produits de
fournisseur, les incorporant comme appropriés.
- **Le processus de gestion des risques** : Cette activité consiste à identifier, à analyser et à
répondre aux risques du projet. Elle implique qu’on augmente la probabilité et l’impact des
évènements positifs et de diminuer la probabilité et l’impact des évènements défavorables
au projet. Elle comporte la planification de la gestion des risques, l’identification, l’analyse
qualitative et l’analyse quantitative des risques, la planification des stratégies de réponse,
et le suivi et le contrôle des risques.
