# Liens vers le dataset
https://www.kaggle.com/datasets/team-ai/spam-text-message-classification

# EDA
## Objectif
- Détecter les messages qui sont des spams.
## Analyse de base
- Taille du jeu de donnée : (5572, 2)
- Type des données : 2 str
- Valeurs manquantes : 0
- Lignes en double : 0
- Target : 'Category' - 13% de spams
# Modèle utilisé
BERT model :
- Modèle conçu par Google AI.
- Comprend le contexte bidirectionnel du language (prend en compte les mots précédents et les mots suivants).
- Gére très bien le texte brute
# Résultat
Avec l'utilisation du modèle BERT, nous arrivons à prédire à 98% si un texte est un spams ou non.
Il y a un léger overfitting qui réduit la prédiction des textes.