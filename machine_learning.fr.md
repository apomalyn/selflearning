# Apprentissage Machine


## Machine Learning

Le concept est simple: on fournit des observations à l'algorithme et le laisse trouvé une manière de déterminés la réponse.
Par exemple, on fournit des images de chat, et on laisse la machine trouvé une méthode pour reconnaitre les chats.

Pour entrainer le modèle, on doit lui fournir des observations qui peuvent être:
- étiquetées: avec le label qui décrit l'observation, qui fournir la "bonne réponse"
- non étiquetées
- partiellement étiquetées

Et le modèle va nous donner une réponse, cette réponse peut être (le type est défini par nous):
- Classes binaires
- Classes discrètes (nominales ou ordinales): chat, chien, personnes (nominales), une étoile, deux étoiles, trois étoiles (ordinales)
- Classes continues: un prix, une quantité, une valeur qui n'est pas naturellement divisé en catégorie
- Groupes (cluster):
- Règles

### Les types de modèles

Il existe différent types de modèles:
- supervisés: c'est le plus fréquent, essentiellement utile pour de la classification. Il demande des observations étiquetées.
- non supervisés: utile pour les groupement (clustering), pour trouver des règles d'associations.
- semi supervisés: utile quand le nombre de données est beaucoup trop important.

#### Supervisé

Le modèle suit: _f(x1, ..., xn) = y_, avec _y_ la réponse du modèle et xn les attributs (features) qui sont les variables d'entrée

Si _y_ est nominal ou discret c'est problème de classification
Si _y_ est continu on est face à un problème de régression

#### Nonsupervisé

Étant donné que nous ne possédons pas d'étiquettes (_y_),

#### Semi-supervisé

On possède quelque étiquette, le modèle va donc essayer de créé des groupes avec une frontière de décision basée uniquement sur les observations étiquetés.

### Séquence de traitements

1. Training: avec un set d'observations
2. Testing: avec un autre set.
3. Recommence à l'étape 1 si le pourcentage de bonne prédiction est insuffisant
4. Modèle prêt

### ZéroR

Se base sur la réponse (_y_) uniquement, il ignore les observations. La réponse est basé sur la plus grande fréquence d'une réponse.
Exanple: 14 observations, 9 fois _y = true_, 5 fois _y = false_. Donc le modèle va retourné _true_.

| Outlook  	| Temp 	| Humidity 	| Windy 	| Play 	|
|----------	|------	|----------	|-------	|------	|
| Sunny    	| Hot  	| High     	| False 	| No   	|
| Sunny    	| Hot  	| High     	| True  	| No   	|
| Overcast 	| Hot  	| High     	| True  	| Yes  	|
| Rainy     | Mild  | High      | False   | Yes   |
| Rainy     | Cool  | Normal    | False   | Yes   |
| Rainy     | Cool  | Normal    | True    | No    |
| Overcast  | Cool  | Normal    | True    | Yes   |
| Sunny     | Mild  | High      | False   | No    |
| Sunny     | Cool  | Normal    | False   | Yes   |
| Rainy     | Mild  | Normal    | False   | Yes   |
| Sunny     | Mild  | Normal    | True    | Yes   |
| Overcast  | Mild  | High      | True    | Yes   |
| Overcast  | Hot   | Normal    | False   | Yes   |
| Rainy     | Mild  |  High     | True    | No    |

N'est jamais utilisé.

### OneR

Modèle: choisir le meilleur attribut pour classifier.

If bestAttribute=val1 then Play = ?
If bestAttribute=val2 than Play = ?
...

Pour toute les valeurs possibles des l'attributs.

### Knn (K nearest neighbors)

La méthode des K plus proches voisins est fondée sur les données du corpus d'apprentissage qui sont les plus proches de la nouvelle
observation pour laquelle on désire faire une prédiction.

La méthode est donc sensible au choix de la mesure de distance ainsi qu'à la dimension de l'espace de travail. Plus le nombre
d'attributs est grand, plus les points sont dispersés dans cet espace et moins cette méthode est utilisable.

Les applications de Knn:
- problème de petite dimension (peu d'attributs)
- pour les problèmes de grande dimension:
  - réduire le nombre d'attributs en sélectionnant les meilleurs
  - réduire la dimension par des techniques spécifiques (ex: analyse en composantes principales - ACP)

**Particularité (Voronoi region)**

### Arbre de décision

#### Entropie

Voir slides 30 - 32 du cours 2

p: Proportion d'exemples correspondant à l'étiquette "oui" dans le jeu de données.
H = -p*log_2(p) - (1-p)log_2(1-p)

Pour l'exemple:
Les H de _f2_ sont:
H(D2,0) = - 6/6 * log_2(6/6) - 0 = 0
H(D2,1) = - 3/13 * log_2(3/13) - 10/13 log_2(10/13) = 0.78


On fait l'entropie moyenne de chaque attribut:

EM(j) = (1 - p_j) * H(Dj,0) + pj * H(Dj,0)

Pour l'exemple:

EM = (6 / 19) * 0 + (13/19) * 0.78 = 0.53.

Toujours dans l'exemple, on choissirait l'attribut _f2_ étant donné qu'il a l'entropie la plus faible.

**Objectif**: trouvé le meilleur attribut (récursivement).
**Critère d'arrêt**:
- Cesser la récursion:
  - Si le noeud est suffisamment homogène (basse entropie)
  - Si les données contiennent de multiples instances du même _x_ mais avec différentes valeurs _y_.
- Créer la feuille avec comme valeur de sortie le _y_ le plus fréquent parmi toutes les valeurs possibles.

### Bayes naïf

#### Fondements

**Classifieur statistique**: prédictions probabilistes
**Fondements théorique**: théorème de Bayes
**Performance**: Un classifieur bayésien simple (Bayes naïf) offre des résultats
 comparables aux arbres de décision et à certains réseaux neuronaux.
**Standard**: Même si en dernier ressort, ils ne seront pas choisis, les méthodes
 bayésiennes fournissent des standards pour comparer les autres méthodes.

**Théorème de Bayes**: Étant donné un ensemble d’entraînement X, la probabilité a
posteriori d’une hypothèse H, P(H|X) est égale à:

P(H|X) = P(X|H)P(H) / P(X)

**Classification**: X appartient à la classe Ci SSI la probabilité P(Ci|X) est la plus
élevée parmi toutes les probabilités P(Ck|x) des k classes.

#### Dérivation de Bayes naïf

On simplifie encore en supposant que les attributs sont indépendants: voir slides 46 cours 2

Si l'attribut A_k est discret ou nominal, alors la probabilité P(x_k | Ci) = le nombre
de classe Ci où Ak = x_k divisé par | Ci | (# de tubles de classe Ci dans les données D).


## Processus d'apprentissage

La création d'un modèle se fait en deux parties: **apprentissage** et **validation**.

Il faut donc partager le dataset entre l'apprentissage et la validation.

### Split et erreurs

Habituellement, le split du dataset est de 2/3 pour l'entraînement et 1/3 pour les tests/validations.
Dans tout les cas il faut faire attention à l'échantillonnage.

Il est également important de faire attention à la **stratification** des données, c'est-à-dire
assurer une distribution égale (soit de la valeur de sortie ou d'un attribut) dans l'ensemble
d’entraînement et l'ensemble (s) de test / validation.

Types d'erreurs:
- **Erreur de resubstitution**: le taux d'erreur sur l'ensemble d'apprentissage
- **Erreur de test**: le taux d'erreur sur l'ensemble de test

### Validation croisée

Quand notre dataset de trop petite taille, le classique 70-30% (70% train, 30% evaluate) créé un biais
sous-estimation.

À la place au utilise la **validation croisée**. On divise le dataset en k set (5 majoritairement).

// TODO INSERT DIAGRAM Cours 2 p.56

- Les résultats finaux: moyenne des k résultats
- À utiliser lorsque l'ensemble ne peut pas être divisé
efficacement entre un ensemble d’entraînement et de test.
- Typiquement, k = 10. Si k = n, alors il s'agît du leave-one-out.
- On peut également répéter m fois le processus (m * k résultats)

### Précision et rappel

Posons A, les réponses réel du dataset et B les prédiction de réponse du modèle.

**Précision**: Pour tous les positif dans B, combien sont effectivement positif dans A.
Il se calcul comme suit: `TP / (TP + FP)`
**Rappel (recall)**: Pour tous les positif dans A, combien sont correctement prédits par le modèle.
Il se calcul comme suit: `TP / (TP + FN)`

Avec:
- **TP: True Positive**: le modèle prédit "Positive" tandis que c'était positif (bonne prédiction)
- **TN: True Negative**: le modèle prédit "Negative" tandis que c'était négatif (bonne prédiction)
- **FP: False Positive**: le modèle prédit "Positif" tandis que c'était négatif (mauvaise prédiction)
- **FN: False Negative**: le modèle prédit "Negative" tandis que c'était positif (mauvaise prédiction)

### F-mesure

Avec _p_ pour la précision et _r_ pour le rappel (recall).

- `F_1 = 2*(p*r)/(p+r)` moyenne harmonique entre _p_ et _r_
- `F_beta = ((1 + Beta^2) * TP)/((1+Beta^2) * TP + Beta^2 * FN + FP)`, si Beta -> 0 => précision, si Beta -> infini => rappel

### Arbres de régression

// TODO Complete

### Apprendre à classifier des images

La classification d'images est un sujet complexe, il rencontre les problèmes suivant:
- Fossé sémantique: là où on voit un chat, l'ordinateur voit une grille de nombres de 0 à 255
- Le point de vue: si le point de vue change, le même object devient complétement différent pour une image.
- La lumière
- Déformation: un même objet peut prendre différente forme/posture (un chat allongé, sur le dos, assis, debout sur 2 pattes, ...)
- Occlusion: un object peut-être dissimulé ou partiellement visible dans l'image

#### Approche Data-driven
