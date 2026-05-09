# Liens vers les datasets
https://www.kaggle.com/datasets/kanchana1990/washington-real-estate-sold-properties-data-2026/data
https://simplemaps.com/us-zips/WA/

# EDA
## Objectif
Prédire le prix auquelle les propriétés se vendent :
- Quand elle est déjà mise en vente.

## Analyse de base
- Taille du jeu de donnée : (12017, 15)
- Type des données : 2 str et 13 float.
- Valeurs manquantes : 14 colonnes dont 1 colonne à 80%. Beaucoup de colonnes très corrélées.
- Lignes en double : 0
- Target : 'lastSoldPrice'

## Suppresion de variables
D'après la documentation 'list_to_sold_ratio' et 'price_per_sqft' sont calculé via le target.    
On les supprime pour ne pas influencer le target.    

## Ajout de variables
Ajout de la taille de la population des villes via un autre jeu de données.    
Création d'une zone géographique en fonction du code zip.

## Visualisation univariée
#### Variables numériques :
- Données asymétrique à droite ou à gauche. Transformation par équilibrer les valeurs (log, ...) ?
- 'population' a plusieurs pics. Regroupement en différentes tailles de villes ?
- Enormément de valeurs abérantes. Cela pourrait être des erreurs d'incrémentation ou des énormes propriétés.

#### Variables - salle de bain :
- 'bath_full' et 'bath_full_calc' ont des valeurs incohérentes (supérieurs à 'bath').
- On ne gardera qu'une des trois variables.

#### Variables catégorielles :
- Distribution des régions et des types de propriété inégales.
- Deux catégories de propriété sont sous représentés. Ecarter du modèle ?

#### Variable "sanitized_text" :
C'est un texte premodifier pour supprimer les informations personnelles.
- 15% doublons.
    - Même propriété vendu avec le prix légèrement modifié ?
    - Même type de propriété ?
    - Propriétés collées ?
    - Même vendeur ?
- 'Length_text' et 'mean_word_length_text' distribution globalement normale
- 'Word_count_text' 2 pics --> deux types de texte ? mais seulement sur le nombre de mots
- 'mean_sent_length_text' asymétrie à droite

## Valeurs manquantes
#### zip / group_zip / population :
- Peu de NaN : 3 à 5 --> supprimer ou médiane/mode.
- zip (98206) n'est pas dans le jeu de données secondaire.
    - Correspond à Everett, Washington --> 114,070 population en 2026.

#### year_built :
- Quand type == land, la logique est de ne pas avoir d'années de construction.
    - Les lignes avec une années correspondent à des emplacements de port.
    - Supprimer l'année ? mettre un marqueur (année hors de l'étude, ...) ? Ajouter une variable booléenne ? 
- Pour les autres NaN, il n'y a pas similitude. Remplacer par la médiane. 

#### listPrice :
Pas de similitude.    
Utilisation médiane.

#### stories : 
- Quand type == land, la logique est de ne pas avoir d'années de construction.
- Quand type == coop :
    -  Pas d'étage pour la propriété donc = 0 ? (peu probable)
    - Erreur d'incrémentation ? (5 valeurs ce qui est possible) donc prendre la médiane de "condo" (tous les deux des copropriétés)
- Pour les autres, utilisation de leurs médianes

#### beds :
- Quand type == land, la logique est de ne pas avoir d'années de construction.
- Pour les autres, utilisation de leurs médianes 

#### garage :
Même reflexion qu'avec "stories"

#### baths / baths_full / baths_full_calc :
- Quand type == land, la logique est de ne pas avoir d'années de construction.
- Pour les autres, utilisation de leurs médianes 

#### Proportion des NaN :
Beaucoup de lignes avec une majorité de NaN.  
On pourrait se poser la question si on doit les garder ou mettre un seuil limite. (maximum 70% / 80% / 90% de NaN pour une même ligne ?)

## Visualisation multivariée
#### Variables / target :
- Comme attendu 'listPrice' a une relation linéaire avec le target. Ce n'est pas le cas pour les autres variables numériques.    
- Les propriétés 'farm type' sont les seuls sans valeurs aberrantes.
- 4 régions sur 5 ont des intervalles très similaires.

#### Variables / Log de target :
- log sqft : relation a tendance linéaire.
- Tous les graphiques sont moins écrasés (limitation des valeurs aberrantes).

#### Pairplot :
Utilisation du log target pour limiter les valeurs aberrantes.    
- 'listPrice' et 'sqft' ont une relation linéaire qui sépare bien le tagret
- 'stories' est trop écrasé par ces valeurs aberrantes
- Les caractéristiques (beds, baths, ...) ont une séparation de prix entre les habitations clasiques et luxueuse
- Les variables textuelles n'apporte pas beaucoup d'informations

#### Corrélation :
- Corrélation élevé / très élevé pour les caractéristiques de la propriété (beds, baths, ...) et le prix proposé à la vente.
- Corrélation élevé / très élevé pour les variables textuelles.
- Différences entre Pearson et Spearman, présences de relations non linéaires.



# Démarches du modèle
## Variables gardé

## Remplissage des valeurs manquantes

## 