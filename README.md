# Unsupervised Job–Candidate Matching System with Explainable AI

L’objectif est de construire un système intelligent de **matching entre CV et offres d’emploi**, capable de :

- Calculer un **score de compatibilité** entre le profil du candidat et les offres disponibles
- Classer les résultats en :
  - `Highly Compatible`
  - `Moderately Compatible`
  - `Low Compatibility`
- Fournir **des explications claires** sur les incompatibilités
- Déployer une application complète avec **FastAPI** pour le backend et **React** pour le frontend
- Suivre les expérimentations via **MLflow** et déployer l’application avec **Docker**

  
---

## 🗂️ Datasets utilisés

1. **Hugging Face – Data Science Job Salaries**  
   - Salaires, expérience, pays, remote ratio, company size  
   - Lien : [huggingface.co/datasets/hugginglearners/data-science-job-salaries](https://huggingface.co/datasets/hugginglearners/data-science-job-salaries)

2. **Kaggle – Job Listings Dataset**  
   - Titre des postes, compétences, descriptions, types de contrats  

3. **Scraping éthique** sur **Indeed / Adzuna / Jooble API**  
   - Job title, location, salary, skills keywords  
   - Respect strict de `robots.txt` et des conditions d’utilisation

> Les datasets sont fusionnés et normalisés pour créer le dataset final exploitable par le modèle.

---

## 🧠 Méthodologie

### 1. Préprocessing
- Nettoyage du texte (CV et description des jobs)
- Vectorisation : TF-IDF et Sentence-BERT embeddings
- Extraction des compétences (skills) et des niveaux d’expérience

### 2. Modélisation non supervisée
- **Similarité cosinus** pour mesurer la proximité CV ↔ Jobs
- **Clustering (KMeans / Agglomerative)** pour regrouper les candidats et jobs similaires
- **Anomaly Detection (Isolation Forest)** pour détecter les CV très éloignés du cluster cible
- **Scoring de compatibilité** :  
  - `>0.75` → Highly Compatible  
  - `0.45–0.75` → Moderately Compatible  
  - `<0.45` → Low Compatibility

### 3. Explicabilité
- Analyse des **skills manquants**
- Niveau d’expérience non compatible
- Écart avec le cluster cible
- Génération d’explications automatiques pour chaque décision

---

## Backend (FastAPI)

Endpoints principaux :
- `/health` → Vérifie que le service est opérationnel
- `/match_cv` → Retourne les offres compatibles avec le CV soumis
- `/explain` → Fournit les raisons des incompatibilités
- `/top_jobs` → Retourne les meilleures recommandations

---

## Frontend (Angular)

Fonctionnalités :
- Upload CV ou saisie d’une description
- Résultats interactifs : score, décision, explication
- Dashboard : distribution des offres, skills demandées, remote ratio
- Interface responsive et agréable

---

##  Déploiement (Docker + Docker Compose)

- Backend containerisé
- Frontend containerisé
- MLflow server (tracking des expériences)
- Commande de lancement :


Répartition complète des tâches
🔹 Week 1 — Foundations & Data

Objectif : Choisir les datasets, scraper les jobs, faire le nettoyage et l’EDA.

Tâches de Ghada :

Choisir les datasets Hugging Face + Kaggle

Fusion et nettoyage des datasets

EDA : analyser salaires, skills, expérience

Visualisations & insights

Tâches d’Anwar :

Choisir les datasets Hugging Face + Kaggle

Scraping éthique des jobs

Fusion et nettoyage des datasets (support)

🔹 Week 2 — NLP & Preprocessing

Objectif : Nettoyer les textes et transformer les données en features exploitables pour le modèle.

Tâches de Ghada :

Text cleaning (CV et offres d’emploi)

Feature extraction : skills, expériences

Embeddings TF-IDF / Sentence-BERT

Tâches d’Anwar :

Normalisation des colonnes

Mapping de l’expérience

Préparer le dataset final pour les embeddings

🔹 Week 3 — Unsupervised Modeling & MLflow

Objectif : Créer le modèle non supervisé, calculer la similarité, clusterisation, anomaly detection, et suivre les expérimentations.

Tâches de Ghada :

Similarité cosinus CV ↔ Jobs

Clustering KMeans / Agglomerative

Anomaly detection (Isolation Forest)

Calcul du score de compatibilité

Suivi des expérimentations via MLflow

Tâches d’Anwar :

Validation des résultats des modèles

Documentation des résultats et insights

🔹 Week 4 — Backend FastAPI

Objectif : Développer l’API pour exposer les modèles et les résultats.

Tâches de Ghada :

Implémenter la logique ML dans l’API (calcul des scores et explications)

Logs et monitoring des endpoints

Tâches d’Anwar :

Développement endpoints /match_cv, /explain

Batch processing & validation des inputs

Support dans l’intégration de la logique ML

🔹 Week 5 — Frontend React

Objectif : Créer l’interface utilisateur pour uploader CV et afficher résultats.

Tâches de Ghada :

Validation des résultats ML côté frontend

Tâches d’Anwar :

Upload CV / formulaire description

Dashboard : compatibilité & graphiques

API calls & gestion des states

🔹 Week 6 — Docker & Deployment

Objectif : Containeriser backend et frontend et tester le déploiement complet.

Tâches de Ghada :

Dockeriser le backend

docker-compose orchestration

Tests de déploiement

Tâches d’Anwar :

Dockeriser le frontend

docker-compose orchestration

Tests de déploiement

🔹 Week 7 — Final Review & CI/CD

Objectif : Préparer la documentation, la présentation, et automatiser avec CI/CD.

Tâches de Ghada :

Rédaction du README et documentation finale

Présentation ML pipeline

Tests finaux

Tâches d’Anwar :

Rédaction du README et documentation finale

Présentation Frontend / UI

CI/CD GitHub Actions

Tests finaux


<img width="1536" height="1024" alt="architecture" src="https://github.com/user-attachments/assets/1d2aaa8b-e29f-441a-a8b7-ed4f693af9ab" />
