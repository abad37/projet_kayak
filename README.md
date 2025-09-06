## 📖 Contexte

Kayak est un moteur de recherche de voyages appartenant à Booking Holdings.  
Le marketing a identifié un besoin fort : **70% des utilisateurs aimeraient plus d’informations fiables sur leur destination**.  

L’objectif est de créer une application capable de :
- Recommander les **meilleures destinations** (top-5 villes en France) selon la météo.
- Recommander les **meilleurs hôtels** (top-20) selon Booking.com.
- Visualiser ces résultats sur des **cartes interactives**.

## 🎯 Objectifs

1. **Scraper les données destinations** :
   - Récupérer coordonnées GPS via **Nominatim** (API gratuite).
   - Récupérer météo via **OpenWeatherMap API**.
   - Définir des critères pour estimer la "météo idéale" (pluie, température, humidité, etc.).

2. **Scraper Booking.com** :
   - Nom, URL, coordonnées, score utilisateur, description des hôtels.

3. **Stockage et ETL** :
   - Stocker les données brutes en CSV dans un **Data Lake (AWS S3)**.
   - Créer une base SQL (AWS RDS), nettoyer les données, les charger dedans.

4. **Visualisation** :
   - Créer deux cartes (Plotly) :
     - **Top-5 villes** (meilleure météo).
     - **Top-20 hôtels**.

## 🛠️ Qualité & bonnes pratiques

- **Reproductibilité** :  
  - Fixer les seeds (numpy, sklearn) pour assurer la même sélection de top villes.  
  - Sauvegarder les CSV intermédiaires (avant/après nettoyage).  

- **Industrialisation** :  
  - Prévoir un pipeline ETL (Airflow ou Prefect) pour automatiser : scraping → stockage → nettoyage → chargement RDS.  
  - Déploiement dans un conteneur Docker pour faciliter la portabilité.  

- **Sécurité & conformité** :  
  - Ne pas exposer les `API_KEY` en clair dans le code (utiliser `.env`).  
  - Respecter les règles d’utilisation des APIs et du scraping.  


