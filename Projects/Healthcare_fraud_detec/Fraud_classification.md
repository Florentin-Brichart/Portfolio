# Liens vers le dataset
https://www.kaggle.com/datasets/nudratabbas/healthcare-fraud-detection-dataset

# EDA
## Objectif
- Prédire si une demande de remboursement est frauduleuse.
## Analyse de base
- Taille du jeu de donnée : (10000, 20)
- Type des données : 10 str, 7 int et 3 float
- Valeurs manquantes : 3 colonnes avec 350 lignes.
- Lignes en double : 0
- Target : 'Is_Fraud'
## Visualisation des données
- 'Claim_ID' ne donne pas d'information (0 NaN et 100% de valeurs uniques)
- 'Provider_ID' et 'Claim_Submission_Date' demanderait une analyse plus approfondie (feature engineering, gestion datetime).   
- Les valeurs manquantes n'ont pas de relations entre elles.
# Preprocessing
Le projet se concentre en priorité sur la création d'un perceptron.   
Pour simplifier le premier modèle, nous allons supprimer les lignes avec des NaN, 'Claim_ID', 'Provider_ID' et 'Claim_Submission_Date'.    
Ensuite, on standardise les données quantitatives en gardant les valeurs aberrantes via RobustScaler.    
Puis on encode les données non-numériques avec un mapping ordinal ou avec un one hot encoder.
# Résultat
Avec le preprocessing et le perceptron créée, nous arrivons à prédire à plus de 99% les données du test_data.
Nous avons aussi créé une fonction qui prédit si une demande de remboursement est frauduleuse.