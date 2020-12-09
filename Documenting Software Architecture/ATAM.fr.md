# ATAM - Évaluation d'une architecture

**Pourquoi faire une évaluation?**
- On peut le faire, c'est peu couteux et augmente les chances de succès de l'architecture
- Le succès du système en dépend fortement
- Technique de mitigation de risques peu coûteuse

**Quand?**
- Idéalement le plus tôt possible
- Alternativement:
  - quand un ébauche d'architecture est prête
  - avant de commencer le développement
  - avant de modifier un système patrimonial
  - pour comprendre un système "hérité"
  - avant de se procurer un gros système
  - choisir parmi plusieurs alternatives

**Coût**
La compagnie AT&T a fait plus de 300 évaluations de projets de 700 personnes-jour. Les statistiques suivantes sont sorties de cette expérience:
- Évaluations en général coutent: 70 personnes-jour
- ATAM: 36 personnes-jour

**Avantages**
- Finance: AT&T: sauve 10% du coût des projets
- L'évaluation se paie elle-même
- Force une préparation
- Force une documentation rigoureuse des motifs
- Problèmes découverts tôt et donc réglé en avance
- Validation des exigences

**Techniques:**
- de questionnement basés sur:
  - scénarios
  - checklist
  - questionnaires
  - des mesures
  - lattix

**Évaluations planifiées ou non**
- planifiée souhaitable
- non planifié: il y a un problème en cours de projets

**Pré-conditions pour l'application de ATAM**
- But et exigences clairement articulés
- Portée contrôlée: 3 à 5 buts
- Rentable pour des projets moyens/grandes
- Personnel clé disponible

**Résultats**
- Rapport décrivent des zones de préoccupations avec données supportant le raisonnement.
- Préoccupations triées par ordre d'importance.
- Amélioration continue sur le processus lui-même.

## Participants et rôles
- **Responsable de l'évaluation/l'équipe**: mise en place du processus, pilote l'évaluation. Rôle de facilitateur dans l'élaboration des scénarios. Analyse du rapport final.
- **"Scribe" de scénarios**: écrit les scénarios sur tableau à feuilles mobiles ("flipchart").
- **"Scribe" général**: capturer les informations sur support numérique.
- **Timekeeper**: limite le temps alloué aux débats.
- **Process enforcer**: exécution des différentes étapes de ATAM, s'assure que le processus se déroule correctement.
- **Observateur**: membre discret. Amélioration continue du processus lui-même.
- **Questionneur**: enrichir les débats.

## Extrants - présentation de l'architecture
- Consise: l'architecture devrait se présenter en une heure.
- Objectifs commerciaux: pour certains développeurs, il seront exposés au contexte d'affaures pour la première fois.
- Scénarios: les objectifs commerciaux se manifestent via les scénarios de qualité prioritaires.
- Mappage: entre les décisions architecturales et les exigences de qualité.
- Points sensibles et de compromis: certaines décisions architecturales affectent certains attributs de qualité ciblés.
- Risque / non-risque: certains choix architecturaux peuvent influencer négativement certains attributs.
- Grands thèmes de risque: regroupement de risques.

Autres extrants:
- Sens de "communauté entre les parties prenantes"
- Canaux de communications ouverts

## Les différentes phases
| Phase | Activité | Participants | Durée typique |
| --- | --- | --- | --- |
| 0 | Partenariat et préparation | Responsable équipe d'évaluation et décideurs clefs du projet | Informellement au gré des besoins, quelques semaines |
| 1 | Évaluation | Équipe d'évaluation et décideurs du projet | 1 jour suivi d'échanges sur 1 à 3 semaines |
| 2 | Évaluation (suite) | Équipe d'évaluation, décideurs du projet et parties prenantes | 2 jours | 
| 3 | Suivi | Équipe d'évaluation et client de l'évaluation | 1 semaine |

0: préparation logistique, formalités administratives.
1 et 2: analyse en 9 étapes
  - étapes 1 à 6 durant la phase 1
  - étapes 7 à 9 durant la phase 2 avec toutes les parties prenantes
3: livraison du rapport final.

### Étapes
1. **Présentaion du processus ATAM**: explication du processus à toutes les personnes impliquées. Identification des attentes.
2. **Présentation des déclencheurs d'activité commerciale ("business drivers")**: pourquoi on fait ce système, que doit-il réaliser? Dans quel contexte?
3. **Présentation de l'architecture**: tous les architectes utilisent des approches mais tous ne connaissent psa le jargon "officiel". Vues de haut niveau: vue de contexte, décomposition modulaire, déploiement, C&C.
4. **Identification des approches architecturales**: ne pas confondre avec analyse. _Identifier_ les approches: tactiques, styles architecturaux, répertorier sous forme de catalogue.
5. **Construction de l'Arbre d'utilité des attributs de qualité**: identifier les attributs de qualité "racines" en travaillant avec les decideurs clés. Les "business drivers" de l'étape 2 devraient alimenter les noeuds principaux. À chaque embranchements, les scénarios sont raffinées et décomposés. (voir p.13 du cours).
Au dernier niveau de l'arbre une clef est présente devant chaque feuille, par exemple: (M, L). C'est la priorité de la feuille, il faut la comprendre comme suit:
<br/>Priorité de gauche: importance de la feuille pour le succès du système.
<br/> Priorité de droite: difficulté à réaliser la feuille
<br/> 3 niveaux: low, medium, high
6. **Analyse des approches architecturales**: analyse des scénarios priorisés.
<br/>-> Départager les risques vs les non-risques.
Quelles feuilles sont étudiées? Dépend du context/Temps: choisir les combinaisons de priorités.
 - Risque: décision architecturale qui pourrait causer des problèmes à un attribut de qualité.
<br/>-> Empêcher soit la réponse ou la mesure de la réponse
 - Non-risque: bonne décision architecturale avec raisonnement à l'appui.
 - Points de sensibilité: paramètre architectural pour lequel un léger changement cause une grande variation d'un attribut de qualité. Ex: le niveau de confidentialité d'un lien VPN sensible au nombre de bits d'encryption.
 - Points de compromis: décision architecturale qui affecte plusieurs attributs de qualité. Ex: mécanisme d'encryption pourrait affecter la performance.

 Tout les points de sensibilité et de compromis sont des risques potentiels.
7. **Remue-méninges et assignation de priorités aux scénarios**
8. **Ré-exploration des approches architecturales**
9. **Présentation finale / rapport**
