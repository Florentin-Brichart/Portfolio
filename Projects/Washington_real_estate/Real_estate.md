# Liens vers les datasets
https://www.kaggle.com/datasets/kanchana1990/washington-real-estate-sold-properties-data-2026/data
https://simplemaps.com/us-zips/WA/

# EDA
## Objectif
- Prédire le prix de vente des propriétés
## Analyse de base
- Taille du jeu de donnée : (12017, 15)
- Type des données : 2 str et 13 float
- Valeurs manquantes : 14 colonnes dont 1 colonne à 80%. Beaucoup de colonnes très corrélées.
- Lignes en double : 0
- Target : 'lastSoldPrice'
## Ajout de variables
Ajout de la taille de la population des villes via un autre jeu de données.    
Création d'une zone géographique en fonction du code zip
## Visualisation univariée
