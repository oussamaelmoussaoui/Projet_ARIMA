# Projet Time Series — ARIMA / SARIMA

Ce dépôt contient deux projets de séries temporelles réalisés dans le cadre du module **Time Series**. L’objectif est d’appliquer une démarche complète d’analyse, de préparation, de modélisation, d’évaluation et d’interprétation sur deux séries temporelles mensuelles.

## Projets réalisés

### Projet 1 — Monthly Armed Robberies in Boston

Le premier projet porte sur une série temporelle représentant le nombre mensuel de vols à main armée à Boston. L’objectif est d’analyser la dynamique de la criminalité dans le temps, d’étudier la stationnarité de la série, puis de construire des modèles de prévision adaptés.

Fichier principal :

```text
01_boston_robberies_arima.ipynb
```

Dataset utilisé :

```text
Robberies.csv
```

### Projet 2 — Monthly Sales of French Champagne

Le deuxième projet porte sur les ventes mensuelles de champagne en France. Cette série présente une saisonnalité annuelle très marquée, notamment avec des pics importants en fin d’année. L’objectif est d’étudier la tendance, la saisonnalité, la variabilité et de proposer un modèle de prévision adapté.

Fichier principal :

```text
02_champagne_sales_corrected.ipynb
```

Dataset utilisé :

```text
champagne.csv
```

## Objectifs du projet

Les objectifs principaux sont :

- analyser visuellement et statistiquement chaque série temporelle ;
- identifier la tendance, la saisonnalité et la variabilité ;
- tester la stationnarité avec les tests ADF et KPSS ;
- appliquer les transformations nécessaires : logarithme, différenciation, différenciation saisonnière ;
- analyser les graphiques ACF et PACF ;
- construire des modèles de référence simples ;
- modéliser les séries avec AR, MA, ARMA, ARIMA et SARIMA ;
- comparer les performances des modèles ;
- analyser les résidus du modèle retenu ;
- justifier le choix du modèle final.

## Structure recommandée du dépôt

```text
Projet-Time-Series/
│
├── data/
│   ├── Robberies.csv
│   └── champagne.csv
│
├── notebooks/
│   ├── 01_boston_robberies_arima.ipynb
│   └── 02_champagne_sales_corrected.ipynb
│
├── rapport/
│   └── rapport_projet_time_series.pdf
│
├── README.md
└── requirements.txt
```

## Méthodologie suivie

La même démarche est appliquée aux deux projets afin de respecter une structure cohérente.

### 1. Analyse exploratoire

Cette partie permet de comprendre la série avant toute modélisation.

Elle contient :

- présentation du contexte ;
- visualisation de la série originale ;
- calcul des statistiques descriptives : moyenne, variance, écart-type ;
- analyse de la moyenne mobile et de l’écart-type mobile ;
- interprétation de la tendance, de la variance et de la saisonnalité ;
- décomposition additive et multiplicative ;
- premières hypothèses sur la dynamique de la série.

### 2. Transformation et préparation

Cette partie prépare les données pour les modèles ARIMA/SARIMA.

Elle contient :

- création de variables temporelles ;
- tests de stationnarité ADF et KPSS ;
- transformation logarithmique ;
- différenciation simple ;
- différenciation saisonnière ;
- analyse ACF/PACF ;
- découpage chronologique train/test.

Le découpage train/test respecte l’ordre temporel afin d’éviter le data leakage. Les données futures ne sont jamais utilisées pour entraîner un modèle censé prédire le futur.

### 3. Modélisation

Plusieurs modèles sont testés afin de comparer les approches simples et avancées.

Modèles de référence :

- modèle naïf ;
- moyenne mobile.

Modèles statistiques :

- AR(p) ;
- MA(q) ;
- ARMA(p,q) ;
- ARIMA(p,d,q) ;
- SARIMA(p,d,q)(P,D,Q,s).

Une partie de l’implémentation est réalisée manuellement avec `numpy`, notamment pour les baselines et certains mécanismes AR/MA/ARMA. Les modèles avancés sont ensuite estimés avec `statsmodels`.

### 4. Évaluation et diagnostic

Les modèles sont évalués à l’aide de plusieurs métriques :

- MAE : Mean Absolute Error ;
- MSE : Mean Squared Error ;
- RMSE : Root Mean Squared Error.

Les modèles ARIMA/SARIMA sont également comparés avec :

- AIC ;
- BIC.

Le diagnostic du modèle final repose sur :

- l’analyse graphique des résidus ;
- l’ACF des résidus ;
- le test de Ljung-Box ;
- la vérification de la normalité ;
- l’étude de la stabilité de la variance.

### 5. Conclusion

Chaque projet se termine par une conclusion qui résume :

- les caractéristiques principales de la série ;
- le modèle retenu ;
- les performances obtenues ;
- l’interprétation métier ;
- les limites du travail ;
- les améliorations possibles.

## Interprétation métier des deux projets

### Boston Robberies

La série des vols à main armée permet d’étudier l’évolution temporelle d’un phénomène criminel. L’analyse cherche à déterminer si les valeurs passées peuvent expliquer les valeurs futures et si une tendance ou une structure temporelle existe.

Le modèle final doit être interprété dans le contexte de la sécurité urbaine. Il peut fournir une prévision statistique, mais il ne remplace pas une analyse sociologique ou criminologique plus complète. Des facteurs externes comme les politiques publiques, les changements économiques ou les événements exceptionnels peuvent influencer la série.

### Champagne Sales

La série des ventes de champagne présente une forte saisonnalité annuelle. Les pics de ventes apparaissent principalement en fin d’année, ce qui correspond aux périodes de fêtes.

L’analyse montre que la saisonnalité est probablement multiplicative, car l’amplitude des pics augmente avec le niveau moyen des ventes. Un modèle SARIMA est donc particulièrement pertinent pour capturer la structure saisonnière de cette série.

## Installation

Créer un environnement virtuel :

```bash
python -m venv venv
```

Activer l’environnement :

Sous Windows :

```bash
venv\Scripts\activate
```

Sous Linux/MacOS :

```bash
source venv/bin/activate
```

Installer les dépendances :

```bash
pip install pandas numpy matplotlib statsmodels scipy scikit-learn jupyter
```

Ou avec un fichier `requirements.txt` :

```bash
pip install -r requirements.txt
```

## Lancement des notebooks

Lancer Jupyter Notebook :

```bash
jupyter notebook
```

Puis ouvrir les fichiers :

```text
01_boston_robberies_arima.ipynb
02_champagne_sales_corrected.ipynb
```

Les fichiers CSV doivent être placés soit dans le même dossier que les notebooks, soit dans un dossier `data/`.

## Bibliothèques utilisées

Les principales bibliothèques utilisées sont :

- `pandas` pour la manipulation des données ;
- `numpy` pour les calculs numériques ;
- `matplotlib` pour les visualisations ;
- `statsmodels` pour les tests statistiques et les modèles ARIMA/SARIMA ;
- `scipy` pour certains tests statistiques ;
- `sklearn` ou des fonctions manuelles pour l’évaluation des modèles.

## Livrables

Les livrables du projet sont :

- les notebooks Jupyter des deux projets ;
- les datasets utilisés ;
- le rapport final ;
- le présent fichier README ;
- éventuellement un fichier `requirements.txt`.

## Limites

Les modèles ARIMA/SARIMA reposent uniquement sur les valeurs passées de la série. Ils ne prennent pas en compte les variables externes comme les événements économiques, sociaux, politiques ou commerciaux.

Pour améliorer le projet, il serait possible d’ajouter :

- des variables exogènes ;
- une validation walk-forward plus détaillée ;
- une comparaison avec des modèles de machine learning ;
- une analyse plus approfondie des ruptures de tendance ;
- une automatisation de la sélection des paramètres ARIMA/SARIMA.

## Conclusion générale

Ces deux projets montrent une démarche complète de modélisation des séries temporelles. Le premier projet applique les méthodes ARIMA sur une série liée aux vols à main armée à Boston, tandis que le second met en évidence l’importance de la saisonnalité dans les ventes mensuelles de champagne.

L’objectif principal n’est pas seulement d’obtenir une bonne prévision, mais aussi de comprendre la dynamique des séries, de justifier chaque choix méthodologique et d’interpréter les résultats dans leur contexte.
