# 🏢 Prédiction de Consommation Énergétique et Émissions CO2 des Bâtiments

> **Projet 3 - Parcours Data Scientist - OpenClassrooms**  
> Modélisation supervisée pour la prédiction de la consommation énergétique et des émissions de gaz à effet de serre des bâtiments non-résidentiels de Seattle (2016).

---

## 🚀 Installation et Lancement

### Prérequis

- Python 3.12 ou supérieur
- Git

### Étapes d'installation

```bash
# 1. Cloner le dépôt
git clone

# 2. Créer un environnement virtuel
python3 -m venv env

# 3. Activer l'environnement
source env/bin/activate  # Linux/macOS
# OU
env\Scripts\activate     # Windows

# 4. Mettre à jour pip
pip install --upgrade pip

# 5. Installer les dépendances
pip install -r requirements.txt

# 6. Vérifier l'installation
pip list
```

### Lancer le notebook

```bash
# Ouvrir avec VS Code
code P3_template_modelistation_supervisee_data_scientist.ipynb

# OU avec Jupyter Notebook
jupyter notebook P3_template_modelistation_supervisee_data_scientist.ipynb
```

**⚠️ Important :** Sélectionnez le kernel Python de l'environnement virtuel (`env/bin/python`) dans VS Code.

---

## 📊 Description du Projet

### Objectifs

Construire **deux modèles de régression supervisée** pour prédire :

1. **La consommation énergétique** (`SiteEnergyUse(kBtu)`)
2. **Les émissions de CO2** (`TotalGHGEmissions`)

des bâtiments non-résidentiels de Seattle, à partir de leurs caractéristiques structurelles et d'usage.

### Dataset

- **Source** : 2016 Building Energy Benchmarking
- **Taille initiale** : 3 376 bâtiments × 46 colonnes
- **Taille finale** : 1 649 bâtiments × 40 colonnes (après nettoyage)
- **Période** : Année 2016

### Variables clés

**Features principales :**
- `PropertyGFATotal` : Surface totale du bâtiment (ft²)
- `LargestPropertyUseTypeGFA` : Surface de l'usage principal
- `PrimaryPropertyType` : Type de bâtiment (Hôpital, Bureau, etc.)
- `YearBuilt` : Année de construction
- `NumberofBuildings` : Nombre de bâtiments dans le complexe
- `NumberofFloors` : Nombre d'étages

**Variables créées (Feature Engineering) :**
- `BuildingAge` : Âge du bâtiment
- `EnergyPerSurface` : Ratio énergie/surface (prédicteur #1 pour CO2)
- `SurfaceGasInteraction` : Interaction surface × gaz naturel
- `HasNaturalGas`, `HasElectricity`, `HasSteam` : Indicateurs sources d'énergie
- `DistanceToCenter` : Distance au centre-ville (Haversine)

---

## 🎯 Résultats Principaux

### Target 1 - Consommation Énergétique

| Métrique | Valeur |
|----------|---------|
| **Meilleur modèle** | Random Forest (Bagging) - Optimisé |
| **R² CV (Base)** | 0.7159 (72% variance expliquée) |
| **R² CV (Optimisé)** | **0.7288** (73% variance expliquée) |
| **Amélioration** | **+1.8%** |
| **Top Features** | PropertyGFABuilding(s) (16.78%), PropertyGFATotal (13.71%), LargestPropertyUseTypeGFA (9.31%) |

**💡 Pourquoi Random Forest gagne ?**  
Plus robuste aux outliers grâce au **bagging** (parallélisation d'arbres). L'optimisation via GridSearchCV (144 combinaisons testées) a permis d'améliorer significativement les performances (+1.8%).

### Target 2 - Émissions de CO2

| Métrique | Valeur |
|----------|---------|
| **Meilleur modèle** | LightGBM (Boosting) - Optimisé 🚀 |
| **R² CV (Base)** | 0.9214 (92% variance expliquée) |
| **R² CV (Optimisé)** | **0.9218** (92% variance expliquée) |
| **Amélioration** | **+0.05%** |
| **Top Features** | SiteEnergyUse (16.97%), EnergyPerSurface (12.05%), DistanceToCenter (10.15%) |

**💡 Pourquoi LightGBM gagne ?**  
Capte mieux les **interactions complexes** entre features grâce au **boosting** séquentiel. L'optimisation via GridSearchCV (108 combinaisons testées) a confirmé les hyperparamètres quasi-optimaux (+0.05%).

---

## 🛠️ Méthodologie

### 1. Analyse Exploratoire (EDA)

- Nettoyage des données (suppression Multifamily, valeurs négatives)
- Analyse des distributions (transformation log nécessaire)
- Matrice de corrélation (9 variables clés)
- Visualisations interactives (Plotly)

### 2. Feature Engineering

- Création de 10 nouvelles features
- Gestion du data leakage (exclusion EnergyPerSurface pour Target 1)
- Encodage OneHot des variables catégorielles
- Imputation des valeurs manquantes

### 3. Modélisation

**Algorithmes testés (4) :**
1. Linear Regression (baseline)
2. Random Forest (bagging) ⭐
3. Support Vector Regressor (SVR)
4. LightGBM (boosting) ⭐

**Architecture :**
- **Pipeline sklearn** : Encapsule preprocessing (ColumnTransformer) + modèle
- **Cross-Validation K-Fold** : K=5 splits pour évaluation robuste
- **Avantage** : Pas de data leakage, évaluation sur 5 validations différentes

**Optimisation :**
- **GridSearchCV avec Pipeline + CV** : Optimisation robuste des hyperparamètres
- Target 1 (Energy) : 144 combinaisons testées → **+1.8% d'amélioration**
- Target 2 (CO2) : 108 combinaisons testées → **+0.05% d'amélioration**

### 4. Évaluation

- **Métriques** : R² CV (mean±std), RMSE CV, MAE CV
- **Validation** : Cross-Validation K-Fold (K=5) - Pas de Train/Test unique
- **Feature Importance** : Extraction depuis modèles entraînés
- **Analyse overfitting** : Écart R² Train - R² CV (Overfit Gap)

---

## 📈 Enseignements Clés

1. **Les features d'interaction sont CRUCIALES**  
   `EnergyPerSurface` + `SurfaceGasInteraction` = 31.42% de l'importance pour CO2

2. **Bagging vs Boosting - Le contexte compte**  
   - **Random Forest** : Meilleur sur données avec outliers (Target 1)
   - **LightGBM** : Meilleur sur données avec interactions complexes (Target 2)

3. **La transformation log est essentielle**  
   Distribution asymétrique → log1p(target) améliore drastiquement les performances

4. **GridSearchCV avec Pipeline + CV améliore les performances**  
   L'approche robuste (Pipeline + Cross-Validation) permet une optimisation efficace (+1.8% et +0.05%)

5. **Les variables GFA (surface par usage) sont prédictives**  
   `LargestPropertyUseTypeGFA` est le 2ème prédicteur le plus fort (+0.846 corrélation)

---

## 🔧 Technologies Utilisées

| Catégorie | Librairies |
|-----------|------------|
| **Data Science** | pandas, numpy, scikit-learn |
| **ML Avancé** | LightGBM |
| **Visualisation** | matplotlib, seaborn, plotly |
| **Statistiques** | statsmodels |
| **Notebook** | jupyter, ipykernel |

---

## 📊 Tableau Récapitulatif Final

| Target      | Meilleur Modèle        | R² CV (Base) | R² CV (Optimisé) | Amélioration | Algorithme |
| ----------- | ---------------------- | ------------ | ---------------- | ------------ | ---------- |
| **Énergie** | Random Forest          | 0.7159       | **0.7288**       | **+1.8%**    | Bagging    |
| **CO2**     | LightGBM               | 0.9214       | **0.9218**       | **+0.05%**   | Boosting   |

**💡 Conclusion :** GridSearchCV avec Pipeline + Cross-Validation a permis d'optimiser les deux modèles de manière robuste, évitant la suroptimisation sur un seul split de données.

---

## 🎓 Compétences Démontrées

✅ Nettoyage et exploration de données (EDA)  
✅ Feature Engineering créatif (10 nouvelles features)  
✅ Prévention du data leakage  
✅ Modélisation supervisée (4 algorithmes)  
✅ Optimisation hyperparamètres (GridSearchCV)  
✅ Analyse de performance (R², overfitting)  
✅ Comparaison Bagging vs Boosting  
✅ Visualisation interactive (Plotly)  
✅ Documentation et reproductibilité

---

## 🚀 Applications Business

Ces modèles permettent de :

- Prédire la consommation énergétique et les émissions CO2 de nouveaux bâtiments
- Prioriser les actions d'efficacité énergétique selon les features importantes
- Estimer l'impact de rénovations structurelles (surface, usage, sources d'énergie)
- Guider les politiques publiques de réduction des émissions

---

## 🆘 Support

En cas de problème :

1. Vérifiez que Python 3.12+ est installé : `python3 --version`
2. Vérifiez que l'environnement est activé : `which python` (doit pointer vers `env/bin/python`)
3. Réinstallez les dépendances : `pip install -r requirements.txt`
4. Redémarrez le kernel Jupyter

Pour toute question, consultez la documentation du notebook ou les commentaires dans le code.
