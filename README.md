# DataChallenge
# 📌 Prédiction de la consommation d'électricité en France 2022

## 📖 Description du projet
Ce projet vise à prédire la consommation d'électricité en France pour l'année 2022 avec une fréquence de 30 minutes. Nous exploitons des caractéristiques temporelles, des données météorologiques et diverses techniques d'apprentissage profond pour générer des prédictions précises, soumises à la plateforme CodaBench pour évaluation.

## 🗂 Structure des fichiers
```
📂 Répertoire du projet
│── GroupeZZ.ipynb        # Notebook Jupyter contenant tout le code, y compris différentes méthodes, la recherche de modèles et l'optimisation
│── train.py              # Script d'entraînement générant model.pth, scaler_X.pkl, scaler_y.pkl
│── predict.py            # Script de prédiction générant pred_final.csv
│── train.csv             # Données d'entraînement
│── test.csv              # Données de test (année 2022, toutes les 30 minutes)
│── meteo.parquet         # Données météorologiques
│── model.pth             # Modèle entraîné
│── scaler_X.pkl          # Paramètres de mise à l'échelle des caractéristiques
│── scaler_y.pkl          # Paramètres de mise à l'échelle de la cible
│── pred_final.csv        # Résultats des prédictions à soumettre sur CodaBench
│── README.md             # Documentation du projet
```

## ⚙ Installation des dépendances
Ce projet utilise **Python 3.8+** et les bibliothèques suivantes :
```bash
pip install pandas numpy matplotlib holidays seaborn statsmodels torch tqdm joblib scikit-learn
```

## 🚀 Exécution
### 1️⃣ Entraînement du modèle
```bash
python train.py
```
Fichiers générés après l'entraînement :
- `model.pth` (modèle sauvegardé)
- `scaler_X.pkl` (scaler des caractéristiques d'entrée)
- `scaler_y.pkl` (scaler de la cible)

### 2️⃣ Prédiction
```bash
python predict.py
```
Génère `pred_final.csv`, le fichier de prédiction final.

### 3️⃣ Soumission sur CodaBench
Compressez `pred_final.csv` et soumettez-le sur CodaBench :
```bash
zip submission.zip pred_final.csv
```

## 🛠 Prétraitement des données
Les principales étapes de traitement des données incluent :
- **Caractéristiques temporelles** : conversion en UTC, extraction des jours, jours fériés, vacances scolaires, impact du COVID-19.
- **Encodage** : encodage sinusoïdal pour les variables périodiques, One-Hot Encoding pour les variables catégorielles.
- **Données météorologiques** : fusion des variables climatiques (température, vent, humidité) à partir de `meteo.parquet`.

## 🧠 Modèles utilisés
Nous avons testé plusieurs modèles :
- **MLPClassic** (Perceptron Multi-couches)
- **MLPWithoutDrop**
- **MLPWithoutAttention**
- **MLPWithAttentionAll**

Le meilleur modèle sélectionné est **MLPWithAttentionAll**, affiné grâce à la recherche par grille.

## 📊 Métriques d'évaluation
Les performances du modèle sont évaluées avec **l'erreur quadratique moyenne racine (RMSE)**.

## 🏆 Résultats finaux
Score obtenu sur CodaBench : 7689.66

## ☁️ Environnement d'exécution
L'expérimentation a été réalisée sur Google Colab avec un GPU **T4**, permettant un entraînement efficace du modèle.

## 👨‍💻 Équipe
- **ZHOU Jie** - Développeur principal
- **ZHEN Youwei** - Partie de prétraitement des données et réglage des hyperparamètres
