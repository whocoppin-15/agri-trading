Auteur : Anthony Razafindrakoto

# 🌾 Commodity Middle Office & Trade Analytics Engine

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Pandas](https://img.shields.io/badge/Library-Pandas-orange)
![Focus](https://img.shields.io/badge/Focus-Commodities%20Middle%20Office-green)

Un moteur d'analyse de données Middle Office développé en Python, conçu pour simuler la centralisation des positions (*"One Position"*), le calcul du Mark-to-Market (MTM), la décomposition du P&L (*PnL Explain*) et le contrôle automatisé de réconciliation comptable sur un desk agro-industriel (Sucre, Éthanol, Blé).

---

## 🎯 Contexte & Enjeux Business

Dans le trading de matières premières physiques et dérivées :
1. **Dispersion des données :** Les contrats physiques (achats/ventes) et les couvertures financières (Futures ICE, Matif) sont souvent gérés dans des systèmes distincts.
2. **Risque de Change (FX) :** La monnaie fonctionnelle de reporting (EUR) s'oppose aux cotations de marché en USD, générant une exposition au risque FX.
3. **P&L Explain & Réconciliation :** Le Middle Office doit expliquer quotidiennement les facteurs de variation du PnL (effet Prix de marché vs effet FX Carry) et détecter automatiquement les écarts (*breaks*) entre le MTM Front/Middle et le MTM Comptable.

---

## ⚙️ Fonctionnalités Principales

### 1. Consolidation *"One Position"* & Normalisation Devise
* **Pipeline ETL :** Génération et agrégation automatisée de données de marché (Spot, Futures, Taux FX USD/EUR) et de flux de trades (Physique & Dérivés).
* **Multi-Currency Conversion :** Normalisation en temps réel de toutes les expositions financières vers la devise de reporting (€ EUR).
* **One Position Nette :** Aggrégation des quantités et évaluation MTM globale par instrument et sous-jacent.

### 2. Décomposition du P&L (*PnL Explain*)
* **PnL MTM Journalier :** Suivi de la variation quotidienne du portefeuille MTM ($J$ vs $J-1$).
* **Effet Prix vs Effet FX Carry :** Isolation de l'impact de la fluctuation des prix des commodités d'une part, et de l'impact des variations du taux de change USD/EUR sur l'exposition USD sous-jacente d'autre part.

### 3. Contrôle & Détection Automatisée d'Anomalies (*Breaks*)
* **Moteur de Réconciliation :** Comparison systématique du MTM calculé par le Middle Office avec les données de MTM Comptable.
* **Alerting paramétrable :** Détection automatique et mise en évidence des écarts dépassant un seuil de tolérance (ex: $> 10\,000$ €).

---

## 🛠️ Architecture & Technologies

* **Langage :** Python 3.10+
* **Librairies clés :**
  * `pandas` : Manipulation de données tabulaires complexes, fusions (`merge`), agrégations (`groupby`) et fonctions temporelles (`shift`).
  * `numpy` : Calculs vectoriels, générations statistiques et logiques conditionnelles (`np.where`).
  * `datetime` : Gestion des fenêtres d'analyse et séries temporelles.

---

## 🚀 Structure du Code & Exécution

### Structure des données manipulées :
1. `df_physical_positions` : Contrats d'achat/vente physiques (Sucre, Éthanol, Blé).
2. `df_financial_hedges` : Couvertures sur marchés organisés (Futures Dec26, Jan27, Mar26).
3. `df_market_data` : Prix de marché Spot, Futures et cours de change USD/EUR.

### Lancer la simulation :
```bash
# 1. Cloner le projet
git clone [https://github.com/ton-pseudo/commodity-middle-office-engine.git](https://github.com/ton-pseudo/commodity-middle-office-engine.git)

# 2. Installer les dépendances
pip install pandas numpy

# 3. Exécuter le script
python main.py
