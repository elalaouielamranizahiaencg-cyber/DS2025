# Rapport d'Analyse Approfondie du PIB
## Comparaison Internationale Multi-Pays

---

## 1. INTRODUCTION ET CADRAGE

### 1.1 Objectif de l'analyse

Cette analyse vise à examiner les performances économiques de plusieurs pays à travers l'étude comparative de leur Produit Intérieur Brut (PIB). L'objectif principal est de :
- Comparer les économies de différents pays sur plusieurs dimensions (PIB nominal, PIB par habitant, croissance)
- Identifier les tendances économiques mondiales et régionales
- Évaluer la compétitivité économique relative des nations analysées
- Fournir une base factuelle pour comprendre les dynamiques de croissance économique

### 1.2 Méthodologie générale employée

L'analyse repose sur une approche quantitative combinant :
1. **Analyse descriptive** : Calcul de statistiques synthétiques (moyennes, médianes, écarts-types)
2. **Analyse comparative** : Comparaison des indicateurs entre pays et dans le temps
3. **Visualisation de données** : Graphiques multiples pour faciliter l'interprétation
4. **Analyse de tendances** : Étude de l'évolution temporelle et des taux de croissance

La méthodologie suit les standards d'analyse économétrique en utilisant Python et ses bibliothèques scientifiques.

### 1.3 Pays sélectionnés et période d'analyse

**Pays sélectionnés** (10 économies représentatives) :
- **États-Unis** : Plus grande économie mondiale
- **Chine** : Deuxième économie mondiale, croissance rapide
- **Allemagne** : Leader européen
- **Japon** : Grande économie asiatique développée
- **France** : Grande économie européenne
- **Royaume-Uni** : Économie post-Brexit
- **Inde** : Économie émergente à forte croissance
- **Brésil** : Leader sud-américain
- **Canada** : Économie développée riche en ressources
- **Afrique du Sud** : Représentant africain

**Période d'analyse** : 2015-2024 (10 ans)

Cette période permet d'observer :
- Les impacts de la pandémie COVID-19 (2020-2021)
- La reprise économique post-pandémique
- Les tensions géopolitiques récentes
- Les évolutions structurelles à moyen terme

### 1.4 Questions de recherche principales

1. Quelles sont les économies ayant connu la croissance la plus forte sur la période ?
2. Comment le PIB par habitant varie-t-il entre pays développés et émergents ?
3. Quels pays ont le mieux résisté aux chocs économiques récents ?
4. Existe-t-il des corrélations entre taille économique et taux de croissance ?
5. Quelles tendances émergent pour l'économie mondiale post-2020 ?

---

## 2. PRÉSENTATION DES DONNÉES

### 2.1 Source des données

**Source principale** : Banque mondiale (World Bank Open Data)
- Base de données : World Development Indicators (WDI)
- Accès : https://donnees.banquemondiale.org
- Fiabilité : Données officielles collectées auprès des instituts statistiques nationaux

**Source secondaire** : Fonds Monétaire International (FMI)
- Base de données : World Economic Outlook Database
- Utilisée pour validation croisée

### 2.2 Variables analysées

| Variable | Description | Unité | Utilisation |
|----------|-------------|-------|-------------|
| **PIB nominal** | Production totale de biens et services | Milliards USD courants | Comparaison de taille économique |
| **PIB par habitant** | PIB divisé par la population | USD par personne | Niveau de vie et richesse |
| **Taux de croissance** | Variation annuelle du PIB réel | % annuel | Dynamisme économique |
| **PIB PPA** | PIB ajusté selon le pouvoir d'achat | Milliards USD PPA | Comparaison réelle du pouvoir d'achat |
| **Part du PIB mondial** | Contribution au PIB mondial | % | Poids économique relatif |

### 2.3 Période couverte

- **Période principale** : 2015-2024
- **Données historiques** : Disponibles depuis 1960 (non utilisées ici)
- **Fréquence** : Annuelle
- **Dernière mise à jour** : Octobre 2024

### 2.4 Qualité et limitations des données

**Points forts** :
- Données officielles validées internationalement
- Méthodologie harmonisée entre pays (SCN 2008)
- Couverture géographique exhaustive
- Historique long permettant les analyses temporelles

**Limitations identifiées** :
1. **Comparabilité** : Différences méthodologiques entre pays malgré l'harmonisation
2. **Délais de publication** : Certaines données 2024 sont des estimations préliminaires
3. **Économie informelle** : Sous-estimation dans certains pays émergents
4. **Taux de change** : Volatilité affectant les comparaisons en USD
5. **Révisions** : Les données peuvent être révisées rétroactivement

**Données manquantes** :
- Quelques pays ont des données incomplètes pour 2024 (estimations utilisées)
- Certains indicateurs PPA ont un décalage temporel

### 2.5 Tableau récapitulatif des données (2024)

| Pays | PIB nominal (Mds USD) | PIB/hab (USD) | Croissance (%) | Part PIB mondial (%) |
|------|----------------------|---------------|----------------|---------------------|
| États-Unis | 28 781 | 86 601 | 2.8 | 25.8 |
| Chine | 18 532 | 13 136 | 4.9 | 16.6 |
| Allemagne | 4 660 | 55 868 | -0.2 | 4.2 |
| Japon | 4 291 | 34 358 | 0.9 | 3.9 |
| France | 3 130 | 47 360 | 1.1 | 2.8 |
| Royaume-Uni | 3 495 | 51 075 | 1.0 | 3.1 |
| Inde | 3 942 | 2 731 | 7.2 | 3.5 |
| Brésil | 2 331 | 10 825 | 3.2 | 2.1 |
| Canada | 2 242 | 57 162 | 1.2 | 2.0 |
| Afrique du Sud | 400 | 6 485 | 0.6 | 0.4 |

*Source : Banque mondiale, octobre 2024. Le PIB mondial total est estimé à 111 326 milliards USD.*

---

## 3. CODE D'ANALYSE ET TRAITEMENT DES DONNÉES

### 3.1 Configuration initiale et importation des bibliothèques

Avant d'exécuter le code, nous importons toutes les bibliothèques nécessaires pour l'analyse.

```python
# =============================================================================
# IMPORTATION DES BIBLIOTHÈQUES
# =============================================================================

# Bibliothèque pour la manipulation de données tabulaires
import pandas as pd

# Bibliothèque pour les calculs numériques
import numpy as np

# Bibliothèques pour la visualisation de données
import matplotlib.pyplot as plt
import seaborn as sns

# Configuration pour améliorer l'apparence des graphiques
from matplotlib import rcParams

# Module pour gérer les avertissements
import warnings

# Ignorer les avertissements non critiques pour un affichage plus propre
warnings.filterwarnings('ignore')

# =============================================================================
# CONFIGURATION GLOBALE DES GRAPHIQUES
# =============================================================================

# Définir le style Seaborn pour des graphiques professionnels
sns.set_style("whitegrid")

# Configurer la palette de couleurs (10 couleurs distinctes)
sns.set_palette("husl", 10)

# Paramètres matplotlib pour la qualité et le style
rcParams['figure.figsize'] = (14, 8)  # Taille par défaut des figures
rcParams['font.size'] = 11  # Taille de police
rcParams['axes.labelsize'] = 12  # Taille des labels d'axes
rcParams['axes.titlesize'] = 14  # Taille des titres
rcParams['xtick.labelsize'] = 10  # Taille des graduations X
rcParams['ytick.labelsize'] = 10  # Taille des graduations Y
rcParams['legend.fontsize'] = 10  # Taille de la légende
rcParams['figure.titlesize'] = 16  # Taille du titre principal

# Configuration pour l'export en haute résolution
rcParams['savefig.dpi'] = 300
rcParams['savefig.bbox'] = 'tight'

print("✓ Bibliothèques importées avec succès")
print("✓ Configuration graphique appliquée")
```

**Explication** : Ce bloc configure l'environnement Python complet. Pandas permettra de manipuler les données comme dans Excel, NumPy pour les calculs, et Matplotlib/Seaborn pour créer des visualisations professionnelles. La configuration garantit des graphiques de haute qualité.

---

### 3.2 Création du jeu de données

Nous créons maintenant un DataFrame contenant toutes les données du PIB pour les 10 pays sur la période 2015-2024.

```python
# =============================================================================
# CRÉATION DU DATASET PRINCIPAL
# =============================================================================

# Liste des années analysées
annees = list(range(2015, 2025))

# Création du dictionnaire de données basé sur les sources de la Banque mondiale
# Valeurs en milliards USD (PIB nominal)
donnees_pib = {
    'Année': annees,
    
    # États-Unis - Leader mondial
    'USA': [18237, 18745, 19543, 20612, 21433, 20893, 23315, 25464, 27361, 28781],
    
    # Chine - Deuxième économie mondiale
    'Chine': [11015, 11233, 12310, 13894, 14280, 14687, 17734, 17963, 18015, 18532],
    
    # Allemagne - Leader européen
    'Allemagne': [3377, 3479, 3693, 3949, 3861, 3846, 4260, 4086, 4456, 4660],
    
    # Japon - Grande économie asiatique
    'Japon': [4389, 4949, 4872, 4971, 5082, 4975, 4940, 4256, 4213, 4291],
    
    # France - Grande économie européenne
    'France': [2439, 2472, 2583, 2715, 2630, 2603, 2958, 2783, 3031, 3130],
    
    # Royaume-Uni - Économie post-Brexit
    'Royaume-Uni': [2932, 2704, 2855, 2829, 2759, 2708, 3186, 3089, 3340, 3495],
    
    # Inde - Économie émergente dynamique
    'Inde': [2103, 2294, 2652, 2713, 2622, 2671, 3176, 3385, 3730, 3942],
    
    # Brésil - Leader sud-américain
    'Brésil': [1802, 1798, 2063, 1919, 1877, 1445, 1609, 1920, 2173, 2331],
    
    # Canada - Économie développée riche en ressources
    'Canada': [1556, 1532, 1653, 1736, 1741, 1644, 1991, 2139, 2242, 2242],
    
    # Afrique du Sud - Représentant africain
    'Afrique du Sud': [318, 296, 349, 368, 352, 335, 419, 405, 377, 400]
}

# Création du DataFrame pandas
df_pib = pd.DataFrame(donnees_pib)

# Affichage des premières lignes pour vérification
print("\n=== APERÇU DES DONNÉES PIB (en milliards USD) ===")
print(df_pib.head())

# Informations sur le dataset
print(f"\n=== INFORMATIONS SUR LE DATASET ===")
print(f"Nombre d'années : {len(df_pib)}")
print(f"Nombre de pays : {len(df_pib.columns) - 1}")
print(f"Période couverte : {df_pib['Année'].min()} - {df_pib['Année'].max()}")
```

**Explication** : Ce code crée la structure de données principale. Les valeurs du PIB sont issues des données officielles de la Banque mondiale. Chaque colonne représente un pays, chaque ligne une année. Le DataFrame pandas facilite toutes les opérations ultérieures.

---

### 3.3 Création des données PIB par habitant

Maintenant, créons un second DataFrame pour le PIB par habitant, indicateur clé du niveau de vie.

```python
# =============================================================================
# DONNÉES PIB PAR HABITANT
# =============================================================================

# PIB par habitant en USD (données Banque mondiale)
donnees_pib_hab = {
    'Année': annees,
    'USA': [56764, 57638, 59532, 62587, 64530, 62551, 69288, 75236, 80036, 86601],
    'Chine': [7990, 8117, 8879, 10000, 10262, 10500, 12614, 12741, 12741, 13136],
    'Allemagne': [41178, 42161, 44550, 47603, 46445, 46208, 51203, 48718, 53571, 55868],
    'Japon': [34524, 39002, 38428, 39290, 40247, 39538, 39313, 33950, 33815, 34358],
    'France': [37675, 37897, 39339, 41177, 39907, 39257, 44408, 41645, 45239, 47360],
    'Royaume-Uni': [44377, 40412, 42491, 41897, 40406, 39229, 45850, 44253, 47590, 51075],
    'Inde': [1606, 1732, 1981, 2009, 1927, 1947, 2277, 2410, 2635, 2731],
    'Brésil': [8814, 8727, 9977, 9238, 8996, 6893, 7609, 9040, 10205, 10825],
    'Canada': [43596, 42349, 45077, 46813, 46327, 43242, 51988, 55196, 57162, 57162],
    'Afrique du Sud': [5725, 5274, 6161, 6422, 6073, 5722, 7055, 6760, 6217, 6485]
}

# Création du DataFrame PIB par habitant
df_pib_hab = pd.DataFrame(donnees_pib_hab)

print("\n=== APERÇU PIB PAR HABITANT (en USD) ===")
print(df_pib_hab.head())

# Statistiques descriptives rapides
print("\n=== STATISTIQUES PIB PAR HABITANT (2024) ===")
pib_hab_2024 = df_pib_hab[df_pib_hab['Année'] == 2024].drop('Année', axis=1)
print(f"PIB/hab minimum : {pib_hab_2024.min().min():,.0f} USD ({pib_hab_2024.min().idxmin()})")
print(f"PIB/hab maximum : {pib_hab_2024.max().max():,.0f} USD ({pib_hab_2024.max().idxmax()})")
print(f"PIB/hab moyen : {pib_hab_2024.mean().mean():,.0f} USD")
```

**Explication** : Le PIB par habitant divise le PIB total par la population, donnant une mesure plus précise du niveau de vie moyen. Les États-Unis dominent largement, tandis que l'Inde, malgré un PIB total élevé, a un PIB par habitant faible en raison de sa population immense.

---

### 3.4 Calcul des taux de croissance

Calculons maintenant les taux de croissance annuels du PIB, indicateur crucial de la dynamique économique.

```python
# =============================================================================
# CALCUL DES TAUX DE CROISSANCE ANNUELS
# =============================================================================

# Initialiser un dictionnaire pour stocker les taux de croissance
donnees_croissance = {'Année': annees}

# Liste des pays (toutes les colonnes sauf 'Année')
pays = [col for col in df_pib.columns if col != 'Année']

# Calculer le taux de croissance pour chaque pays
for pays_nom in pays:
    # Extraire la série temporelle du PIB pour ce pays
    serie_pib = df_pib[pays_nom].values
    
    # Initialiser la liste des taux de croissance (premier élément = NaN car pas de référence)
    taux_croissance = [np.nan]
    
    # Calculer le taux de croissance année par année
    # Formule : ((PIB_année_n - PIB_année_n-1) / PIB_année_n-1) * 100
    for i in range(1, len(serie_pib)):
        taux = ((serie_pib[i] - serie_pib[i-1]) / serie_pib[i-1]) * 100
        taux_croissance.append(taux)
    
    # Ajouter au dictionnaire
    donnees_croissance[pays_nom] = taux_croissance

# Créer le DataFrame des taux de croissance
df_croissance = pd.DataFrame(donnees_croissance)

print("\n=== TAUX DE CROISSANCE DU PIB (% annuel) ===")
print(df_croissance.tail())  # Afficher les 5 dernières années

# Statistiques sur les taux de croissance 2020-2024
print("\n=== CROISSANCE MOYENNE 2020-2024 (post-COVID) ===")
croissance_recente = df_croissance[df_croissance['Année'] >= 2020].drop('Année', axis=1)
croissance_moyenne = croissance_recente.mean().sort_values(ascending=False)
for pays_nom, taux in croissance_moyenne.items():
    print(f"{pays_nom:15s} : {taux:+6.2f}%")
```

**Explication** : Le taux de croissance mesure la variation en pourcentage du PIB d'une année à l'autre. Un taux positif indique expansion, négatif indique récession. Le calcul utilise la formule standard : (valeur_actuelle - valeur_précédente) / valeur_précédente × 100. L'année 2015 n'a pas de taux car elle n'a pas d'année de référence précédente.

---

### 3.5 Préparation des données pour l'analyse

Transformons les données en format long (tidy data) pour faciliter certaines analyses et visualisations.

```python
# =============================================================================
# TRANSFORMATION EN FORMAT LONG (TIDY DATA)
# =============================================================================

# Convertir le DataFrame PIB en format long
# Chaque ligne = une observation (pays, année, valeur)
df_pib_long = df_pib.melt(
    id_vars=['Année'],           # Colonne à conserver comme identifiant
    var_name='Pays',             # Nom pour la colonne des pays
    value_name='PIB_milliards'   # Nom pour la colonne des valeurs
)

# Idem pour le PIB par habitant
df_pib_hab_long = df_pib_hab.melt(
    id_vars=['Année'],
    var_name='Pays',
    value_name='PIB_par_habitant'
)

# Idem pour la croissance
df_croissance_long = df_croissance.melt(
    id_vars=['Année'],
    var_name='Pays',
    value_name='Taux_croissance'
)

# Fusionner tous les DataFrames en un seul dataset complet
df_complet = df_pib_long.merge(
    df_pib_hab_long, 
    on=['Année', 'Pays']
).merge(
    df_croissance_long, 
    on=['Année', 'Pays']
)

print("\n=== DATASET COMPLET (format long) ===")
print(df_complet.head(10))
print(f"\nNombre total d'observations : {len(df_complet)}")
print(f"Variables disponibles : {list(df_complet.columns)}")

# Sauvegarder les données nettoyées (optionnel)
# df_complet.to_csv('donnees_pib_propres.csv', index=False, encoding='utf-8')
```

**Explication** : La transformation en format "long" réorganise les données : au lieu d'avoir un pays par colonne, on a une ligne par observation (pays-année). Ce format facilite les analyses groupées et certaines visualisations. La fonction `melt()` effectue cette transformation, puis `merge()` combine tous les indicateurs en un seul DataFrame.

---

### 3.6 Nettoyage et vérification des données

Vérifions la qualité des données et gérons les valeurs manquantes éventuelles.

```python
# =============================================================================
# NETTOYAGE ET VÉRIFICATION DES DONNÉES
# =============================================================================

print("\n=== VÉRIFICATION DE LA QUALITÉ DES DONNÉES ===")

# Vérifier les valeurs manquantes
valeurs_manquantes = df_complet.isnull().sum()
print("\nNombre de valeurs manquantes par colonne :")
print(valeurs_manquantes)

# Vérifier les valeurs aberrantes ou négatives
print("\nVérification des valeurs négatives :")
print(f"PIB négatifs : {(df_complet['PIB_milliards'] < 0).sum()}")
print(f"PIB/hab négatifs : {(df_complet['PIB_par_habitant'] < 0).sum()}")

# Statistiques sur les taux de croissance (peuvent être négatifs légitimement)
print("\nStatistiques des taux de croissance :")
print(df_complet['Taux_croissance'].describe())

# Gérer les NaN dans les taux de croissance (année 2015)
# On peut soit les laisser, soit les remplacer par 0, soit les interpoler
print(f"\nNombre de taux de croissance NaN : {df_complet['Taux_croissance'].isna().sum()}")

# Créer une version sans NaN pour certaines analyses
df_sans_nan = df_complet.dropna()
print(f"Observations après suppression des NaN : {len(df_sans_nan)}")

# Vérifier les doublons
doublons = df_complet.duplicated(subset=['Année', 'Pays']).sum()
print(f"\nNombre de lignes dupliquées : {doublons}")

print("\n✓ Vérification terminée - Données prêtes pour l'analyse")
```

**Explication** : Cette étape cruciale vérifie l'intégrité des données. On cherche les valeurs manquantes (NaN), les valeurs aberrantes, et les doublons. Les NaN dans les taux de croissance pour 2015 sont normaux (pas d'année précédente pour calculer). Les autres colonnes ne devraient pas avoir de valeurs manquantes.

---

## 4. ANALYSES STATISTIQUES DÉTAILLÉES

### 4.1 Statistiques descriptives globales

Commençons par une vue d'ensemble statistique des données.

```python
# =============================================================================
# STATISTIQUES DESCRIPTIVES
# =============================================================================

print("\n" + "="*80)
print("STATISTIQUES DESCRIPTIVES - PIB NOMINAL (milliards USD)")
print("="*80)

# Statistiques pour l'année 2024 (la plus récente)
pib_2024 = df_pib[df_pib['Année'] == 2024].drop('Année', axis=1)

stats_2024 = pd.DataFrame({
    'Moyenne': pib_2024.mean(),
    'Médiane': pib_2024.median(),
    'Écart-type': pib_2024.std(),
    'Minimum': pib_2024.min(),
    'Maximum': pib_2024.max(),
    'Coefficient de variation': (pib_2024.std() / pib_2024.mean() * 100)
})

# Trier par PIB décroissant
stats_2024 = stats_2024.sort_values('Moyenne', ascending=False)
print("\n", stats_2024)

# Statistiques globales
print(f"\n{'='*80}")
print("RÉSUMÉ STATISTIQUE GLOBAL (2024)")
print(f"{'='*80}")
print(f"PIB total cumulé des 10 pays : {pib_2024.sum().sum():,.0f} Mds USD")
print(f"PIB moyen : {pib_2024.mean().mean():,.0f} Mds USD")
print(f"Écart-type moyen : {pib_2024.std().mean():,.0f} Mds USD")
print(f"Coefficient de variation : {(pib_2024.std().mean() / pib_2024.mean().mean() * 100):.1f}%")

# Calculer les parts du PIB mondial (estimation 111 326 Mds USD)
pib_mondial_2024 = 111326
parts_pib = (pib_2024.iloc[0] / pib_mondial_2024 * 100).sort_values(ascending=False)
print(f"\n{'='*80}")
print("PART DU PIB MONDIAL (2024)")
print(f"{'='*80}")
for pays_nom, part in parts_pib.items():
    print(f"{pays_nom:15s} : {part:5.2f}%")

print(f"\nPart cumulée des 10 pays : {parts_pib.sum():.1f}% du PIB mondial")
```

**Explication** : Les statistiques descriptives fournissent une synthèse numérique. La moyenne indique le PIB typique, la médiane le point central (moins sensible aux extrêmes), l'écart-type mesure la dispersion. Le coefficient de variation (écart-type/moyenne × 100) permet de comparer la variabilité entre différentes distributions.

---

### 4.2 Analyse de l'évolution temporelle

Analysons maintenant comment le PIB a évolué dans le temps pour chaque pays.

```python
# =============================================================================
# ANALYSE DE L'ÉVOLUTION TEMPORELLE
# =============================================================================

print("\n" + "="*80)
print("ÉVOLUTION DU PIB (2015-2024)")
print("="*80)

# Calculer la croissance totale sur la période
pays_liste = [col for col in df_pib.columns if col != 'Année']
evolutions = pd.DataFrame({
    'PIB_2015': df_pib[df_pib['Année'] == 2015][pays_liste].iloc[0],
    'PIB_2024': df_pib[df_pib['Année'] == 2024][pays_liste].iloc[0]
})

# Calculer la variation absolue et relative
evolutions['Variation_absolue'] = evolutions['PIB_2024'] - evolutions['PIB_2015']
evolutions['Variation_pourcent'] = ((evolutions['PIB_2024'] - evolutions['PIB_2015']) 
                                     / evolutions['PIB_2015'] * 100)

# Calculer le taux de croissance annuel moyen composé (TCAM ou CAGR)
# Formule : CAGR = (Valeur_finale / Valeur_initiale)^(1/nombre_années) - 1
nombre_annees = 9  # 2015 à 2024 = 9 ans
evolutions['TCAM'] = ((evolutions['PIB_2024'] / evolutions['PIB_2015']) 
                      ** (1/nombre_annees) - 1) * 100

# Trier par TCAM décroissant
evolutions = evolutions.sort_values('TCAM', ascending=False)

print("\n", evolutions)

print(f"\n{'='*80}")
print("CHAMPIONS DE LA CROISSANCE (2015-2024)")
print(f"{'='*80}")
for idx, row in evolutions.head(3).iterrows():
    print(f"{idx:15s} : +{row['Variation_pourcent']:6.1f}% (TCAM: {row['TCAM']:5.2f}%/an)")

print(f"\n{'='*80}")
print("CROISSANCE LA PLUS FAIBLE")
print(f"{'='*80}")
for idx, row in evolutions.tail(3).iterrows():
    print(f"{idx:15s} : +{row['Variation_pourcent']:6.1f}% (TCAM: {row['TCAM']:5.2f}%/an)")
```

**Explication** : Cette analyse examine la performance sur toute la période. Le TCAM (Taux de Croissance Annuel Moyen Composé) est particulièrement utile car il lisse les variations annuelles pour donner un taux de croissance moyen équivalent. C'est le taux qui, appliqué chaque année, donnerait la même croissance totale.

---

### 4.3 Comparaison des PIB par habitant

Analysons maintenant le niveau de vie à travers le PIB par habitant.

```python
# =============================================================================
# ANALYSE DU PIB PAR HABITANT
# =============================================================================

print("\n" + "="*80)
print("ANALYSE PIB PAR HABITANT (2024)")
print("="*80)

# Extraire les données 2024
pib_hab_2