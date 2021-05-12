# La culture qualité

## Introduction

Ce chapitre est une mise en contexte des enjeux qualité dans le domaine logiciel
- Coût de la qualité
- Culture qualité
- Code de déontologie de l'ingénieur logiciel de l'IEEE/ACM

Pour l'ingénieur membre de son ordre professionnel, l'importance de la qualité
fait partie de la _responsabilité civile_ de sa profession et doit être gérée
avec soin.

## Coût de la qualité

Les composants du coût de la qualité:
- **Coût de prévention** pour prévenir l'occurrence d'erreurs dans les diverses
étapes durant le processus de développement ou de maintenance (formation, achat
  de logiciel, ...)
- **Coût de détection**, coût de vérification ou d'évaluation d'un produit ou
d'un service pendant les différentes étapes du processus de développement (tests)
- **Coût de défaillance (non-conformité, reprise)**:
  - **Coût de défaillance interne**: le coût résultant des anomalies avant que le
  produit ou le service ne soit livré au client.
  - **Coût de défaillance externe**: le coût encouru par la compagnie quand c'est
  le client qui découvre des défauts.
  - **Coût de préjudice commercial**: le coût de dégradation de l'image de
  l'entreprise, coût de la perte de clients.

**Coût du projet = réalisation + défaillance + évaluation + prévention**

| Catégorie majeure | Sous-catégorie | Définition | Coût élémentaire typique |
| ---	| ---	| ---	| ---	|
| Coûts de prévention | Établir les fondements de  la qualité | Efforts pour définir la qualité, établissement d’objectifs de qualité, de normes et de seuil de qualité. Analyse de compromis liés à la qualité. | Définition de critères de succès des tests d’acceptation et de normes reliées à la qualité. |
|                       	| Interventions orientées projet et processus 	| Efforts pour prévenir la mauvaise qualité ou améliorer le processus de qualité. 	| Formation, améliorations de processus, collecte de mesures et analyse. |
| Coûts de détection    	| Découvrir l'état du produit | Découvrir le niveau de la  non-comformité. | Test, assurance qualité logicielle. Inspections, revues. |
|                       	| S'assurer de l'atteinte de  la qualité | Mécanismes de contrôle de  la qualité.	| Audits de qualité du produit, décision de livraison de nouvelles versions. |
| Coûts de défaillances 	| Anomalie interne | Problèmes de qualité détectés  _avant_ la livraison au client. | La gestion des défauts avant la livraison, les reprises, les revues et les tests à effectuer à nouveau. |
|                       	| Anomalie externe | Problèmes de qualité détectés  _après_ la livraison au client. | Support technique des versions livrées, enquête de plaintes, avis de défaut, mise à niveau et correction des erreurs. |

## Culture qualité

Selon Wiegers, une culture saine est composée des éléments suivants:
- L’engagement personnel de chaque chef de projet à créer des projets de qualité
en appliquant systématiquement les pratiques efficaces de génie logiciel;
– l’engagement de l’organisme par les gestionnaires de tous les niveaux à fournir
un environnement dans lequel la qualité logicielle est un facteur fondamental de
succès et qui permet à chaque développeur de réaliser ce but;
– l’engagement de tous les membres de l’équipe à améliorer continuellement les
processus qu’ils emploient et à améliorer continuellement les produits qu’ils
créent.

### Principes culturels en génie logiciel

1. Ne jamais laisser votre patron ou votre client vous inciter à faire un mauvais
travail;
2. Les personnes doivent sentir que le travail qu'ils effectuent est apprécié;
3. L’éducation continue est la responsabilité de chaque membre d’équipe;
4. La participation du client est le facteur le plus critique de la qualité
logicielle;
5. Votre plus grand défi est de partager la vision du produit final avec le client;
6. L'amélioration continuelle de votre processus de développement logiciel est
possible et essentielle;
7. Les procédures de développement logiciel peuvent aider à établir une culture
commune des bonnes pratiques;
8. La qualité est la première priorité ; la productivité à long terme est une
conséquence normale de qualité;
9. Tâcher que ce soit un pair, plutôt qu'un client, qui trouve un défaut;
10. Une clé de la qualité logicielle est de réitérer beaucoup de fois sur toutes
les étapes de développement excepté le codage: on ne code qu’une fois;
11. Contrôler les rapports d’erreurs et les demandes de changement est essentiel
à la qualité et la maintenance;
12. Si vous mesurez ce que vous faites, vous pouvez apprendre à le faire mieux;
13. Faites ce qui semble raisonnable; ne recourez pas au dogme;
14. Vous ne pouvez pas changer tout en même temps. Identifiez les changements
qui rapporteront les plus grands avantages, et commencez à les mettre en application
dès lundi prochain.

## Les cinq (5) dimensions d'un projet logiciel et les compromis

Dans un pentagone, où les sommets sont: **Fonctionnalités**, **Qualité**, **Coût**,
**Échéance**, **Personnel**.

Trois états (rôles) pour chaque dimension:
- un objectif (driver) est une raison spécifique et importante pour laquelle le
projet doit être réalisé. Il n’y a pas de flexibilité;
- une contrainte est un facteur externe qui n’est pas sous le contrôle du chef de
projet. Il y a très peu de flexibilité;
- un degré de liberté (ce qui n’est pas objectif ou contrainte). Grande flexibilité.

## Les neurosciences et le profil cognitif des participants au projet

Pourquoi traiter de ce sujet dans un cours de gestion de projet:
- la prise de décision et le travail d’équipe sont importants en Gestion de projet;
- Connaître notre mode de fonctionnement avec soi et les autres est donc un
atout pour la réussite;
- Dans le cours de gestion, tenir compte de la psychologie et des besoins des
individus est une constante (ex.: pyramide des besoins de Maslow);
- La gestion de projet implique la compréhension de la psychologie.

Selon les travaux de Sperry, chaque hémisphère du cerveau est spécialisé dans un
type de pensée. Le gauche est **logique**, **analytique**, **séquentiel** tandis
que le droit est **spatial**, **visuel**, **affectif**.

## Le code de déontologie

Le code est là pour régir l'exercice de la profession d'ingénieur. Il contient un
ensemble de droits et devoirs que chaque ingénieur se doit de respecter, la conduite
 à suivre ainsi que les rapports entre les ingénieurs et le public.

Posséder un code de déontologie pour une entreprise cela:
1. Attirer de nouveaux employés
  - Attirera des employés consciencieux et engagés et qui veulent être impliqués
  dans une organisation qui produit un logiciel de qualité.
2. Image professionnelle
  - Promotion d’une image de marque pour votre société.
    - En retour, cela laissera le public savoir que la société travaille
    pour le bien du public et accepte fièrement cette responsabilité.
  - Augmentera le respect du public de votre société et améliorera la qualité de
  logiciel qu’il produit.
3. Confiance du public
  - Informe le public que leurs intérêts sont à coeur de l'entreprise, tout en les
  informants des standards de la compagnie
4. Déploiement et adoption au niveau international
  - Un code adopté à la grandeur de la planète par tous les ingénieurs logiciels
  et leur employeurs (voir [Software Engineering Ethics](https://www.etsu.edu/cbat/computing/seeri/))

### Les intentions du code de déontologie

1. Documenter les engagements moraux et professionnels des ingénieurs logiciels
2. Informer les praticiens des normes auxxquelles la société s'attend à ce que
les ingénieurs logiciels attendent les uns des autres.
3. Informer le public des responsabilités de la profession.

### L'intérêt du public

Le souci pour la santé, la sureté et le bienêtre du public est _primordial_,
c'est-à-dire que _l'intérêt du public est central_ à ce code de déontologie.

Il existe huit (8) principes (aspirations) qui ont été ordonnées pour refléter
l'ordre dans lequel les professionnels du logiciel doivent considérer leurs
obligations morales:
  - Les principes identifient les relations éthiques qui régissent les personnes,
  les groupes et les organisations, ainsi que les obligations principales associées
   à ces relations.

| **Principe**  | **Description**	|
|---------- |------------	|
| Le public | Les ingénieurs logiciels doivent agir dans l’intérêt public en tout temps. |
| Le client et l'employeur 	| Les ingénieurs logiciels doivent agir de manière à servir le mieux possible les intérêts de leurs clients et de leur employeur, toujours en fonction de l’intérêt public. |
| Le produit | Les ingénieurs logiciels doivent s’assurer que leurs produits et les modifications connexes sont conformes aux normes professionnelles les plus élevées possibles. |
| Le jugement | Les ingénieurs logiciels doivent maintenir leur intégrité et leur indépendance dans leur jugement professionnel. |
| La gestion | Les gestionnaires et les responsables de génie logiciel doivent souscrire à une approche éthique de la gestion du développement et de la maintenance des logiciels et s’employer à en faire la promotion. 	|
| La profession | Les ingénieurs logiciels doivent s’assurer de l’intégrité et la réputation de la profession en tenant compte de l’intérêt public.	|
| Les collègues | Les ingénieurs logiciels doivent être justes et appuyer leurs collègues. |
| Soi-même | Les ingénieurs logiciels doivent être en situation d’apprentissage continu et promouvoir une approche éthique à la pratique de leur profession. |
