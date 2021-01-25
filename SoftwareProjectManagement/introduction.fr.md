# Introduction à la gestion de projet logiciel (et à l'AQL)

## Détails
**Sigle du cours**: GTI510
**Enseignant**: Alain April

## Gestion de projet

### Introduction

Défis: gardé la motivation de l'équipe, faire le suivi, gardé une trace de la vie du projet

### La gestion de projet - logiciel et TI

PMI - une certification très intéressante à passer. Propose des pratiques génériques de gestion de projet.

Difficultés spécifiques au domain:
- domaine "jeune" et intangible ce qui rends la compréhension avec le client difficile
- difficultés d'estimations (la construction estime avec le pied carré qui possède un prix fixe, en logiciel nous facturons à la fonctionnatlité cependant le prix n'est absolument pas fixe)
- les attentes souvent gargantuesque et demandé pour hier.

Fonctionnalités, personnel, échéance, coût et qualité sont les 5 dimensions qui représentent les compromis à négocier avant de démarrer un projet logiciel. Elles sont disposés dans un pentagone.

Cycle de vie (life cycle): évolution d'un système, produit, service, projet ou autre entité d'origine humain de la conception à la retraite (ISO 12207)

Cycle de développement (Development Life Cycle): processus de cycle de vie du logiciel qui comporte des activités d'analyse des besoins, de conception, de développement. d"intégration, de tests
d'intallation et de soutien pour l'acceptation des produits logiciels (IS 90003)

### Le choix d'un cycle de vie

En 1960 on programme directement, en 1970 le logiciel se construit comme un édifice: on planifie l'ensemble puis on le programme.
Au vu de la lenteur et du cout des cycles de vie classiques, les évolutions technologiques ainsi que la
pression à aller toujours plus vite ont généré toutes sortes de propositions de cycles de vie.

#### Les différents cycles de vie

**Cascade**

ADD DIAGRAM

**Rapid Application Development (RAD)**
Conserve le fonctionnement d'un cycle de vie en cascade, cependant un prototype est développé puis présenté au client.

ADD DIAGRAM

**Incrémental**

ADD DIAGRAM

**RUP**

Une des premières version des cycles agile.

ADD DIAGRAM

**Agile**

Il existe plusieurs variante de ce cycle, comme: SCRUM, Kanban ou Extreme Programming Project

### Impact du choix de cycle de vie sur la planification et la gestion de projet logiciel

Chaque cycle de vie comporte des défis spécifiques à son utilisation tandis que certains cycles de vie sont plus adapté pour un projet spécifique.

## AQL

Basé en trois points:
- l'assurance qualité
- développement
- tests

Chaque point impact le suivant: Assurance Qualité -> améliore -> Développement -> alimente -> Tests -> rapporte -> Assurance Qualité

Les grandes catégories de causes d'erreurs du logiciel

Pendant la conception, on parle **erreurs**.
Pendant les essais on parle de **fautes**.
En production c'est une **défaillance du système**.

A des fins d'amélioration il est conseillé de noter la provenance des erreurs.

L'assurance qualité prévient les défauts tandis que le controle qualité effectue les tests pour trouver les défauts
