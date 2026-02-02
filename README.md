# 🚀 E-Commerce Big Data Pipeline  
## Architecture Medallion – 9.3 Go de données (≈ 25M événements)


## 🧠 Contexte & Objectifs

Ce projet met en œuvre un **pipeline Big Data de bout en bout** destiné à traiter un dataset e-commerce massif de **9.3 Go** (≈ **25 millions d’événements utilisateurs**).

🎯 **Objectifs principaux :**
- Concevoir un pipeline ETL scalable et robuste
- Appliquer une **Architecture Medallion (Bronze / Silver / Gold)**
- Optimiser les performances Spark (I/O, shuffles, mémoire)
- Produire des **données analytiques exploitables par le métier**
- Générer des **KPIs de rentabilité e-commerce**

Le projet s’inscrit dans une logique **Data Engineering orientée production**.

---

## 🏗️ Architecture Medallion

L’architecture est organisée en trois couches garantissant **qualité, traçabilité et performance** :

### 🥉 Bronze – Raw Layer
- Ingestion des fichiers CSV bruts
- Lecture optimisée via **Column Pruning**
- Conservation des données sources sans transformation
- Objectif : **traçabilité & audit**

### 🥈 Silver – Refined Layer
- Nettoyage avancé et normalisation
- Typage strict des colonnes (**Schema Enforcement**)
- Application de **8 tests de qualité des données**
- Stockage au format **Apache Parquet** partitionné
- Objectif : **fiabilité & cohérence**

### 🥇 Gold – Curated Layer
- Enrichissement métier
- Jointures optimisées via **Broadcast Join**
- Agrégations analytiques (CA, marges, volumes)
- Alimentation d’une base SQL analytique
- Objectif : **prise de décision**

---

## ⚡ Optimisations & Performance

Le pipeline a été conçu pour exploiter efficacement le calcul distribué Spark :

| Optimisation | Description | Impact |
|---|---|---|
| **Apache Parquet** | Format colonnaire compressé | 🚀 Lecture **3.9x plus rapide** |
| **Partitionnement** | Par `event_type` | 📉 Réduction massive des I/O |
| **Broadcast Join** | Diffusion des petites tables | ❌ Suppression du shuffle |
| **Schema Enforcement** | Typage strict en Silver | ✅ 0 erreur critique |
| **Lazy Evaluation** | Exploitation du moteur Spark | ⚙️ Exécution optimisée |

---

## 📊 Données & Insights Business

Les données finales sont exposées via une base SQL analytique :

📂 **Base :** `ecommerce_db`

### KPIs produits :
- 🏆 **Top marques par chiffre d’affaires**
- 📈 **Analyse de marges par catégorie**
- 💰 Détection de **marques à forte rentabilité (~15%)**
- 🧪 **Audit qualité du catalogue**
- 🔍 Suivi du comportement utilisateur

Ces indicateurs permettent un **pilotage stratégique des ventes e-commerce**.

---

## 🧰 Stack Technique

- **Apache Spark 3.x**
- **Databricks**
- **Python (PySpark)**
- **Apache Parquet**
- **SQL Analytics**
- **Dataset REES46 (Kaggle)**

---

## 📁 Structure du Projet

```bash
project/
├── data/
│   ├── bronze/                 # Données brutes (Raw Layer)
│   │   ├── main/               #Source 1
│   │   └── enrich/             #Source 2
│   │
│   ├── silver/                 # Données nettoyées et normalisées
│   │   ├── main_clean/         # Nettoyage des données principales
│   │   ├── enrich_clean/       # Nettoyage des données enrichies
│   │   └── joined/             # Jointures validées
│   │
│   └── gold/                   # Données métier prêtes à l’analyse
│       ├── marts/              # Tables analytiques (Data Marts)
│       ├── aggregates/         # KPIs et agrégations métier
│       └── exports/            # Exports finaux (CSV / SQL)
│
├── src/
│   ├── ingestion/              # Scripts d’ingestion (Bronze)
│   ├── transforms/             # Transformations Spark (Silver & Gold)
│   ├── quality/                # Tests et contrôles qualité
│   └── utils/                  # Fonctions utilitaires communes
│
├── notebooks/                  # Notebooks Databricks (exploration & pipeline)
├── configs/                    # Fichiers de configuration
│
├── reports/
│   ├── data_quality/           # Rapports de qualité des données
│   └── benchmarks/             # Mesures de performance & optimisations
│
└── README.md                   # Documentation du projet

