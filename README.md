# Projet_Data354_ETL_DEGBUN_JOSUE ![Status](https://img.shields.io/badge/status-stable-brightgreen) ![Python Version](https://img.shields.io/badge/python-3.11%20%7C%20%3E%3D3.6-blue) ![MongoDB](https://img.shields.io/badge/MongoDB-7.0-green) ![Jupyter](https://img.shields.io/badge/Jupyter-yes-brightgreen)

![entreprise](https://github.com/degbun/Projet_Data354_ETL_DEGBUN_JOSUE/blob/main/__pycache__/data354.png)

Le projet vise à construire un ETL (Extract, Transform, Load) pour l'extraction et le traitement des données relatives à la qualité de l'air provenant de l'API AirQuino. Ensuite il s'agira de la création d'un modèle de Machine Learning pour effectuer des prévisions sur les deux prochaines heures.

## Structure du projet
1. `Images/`:
    Dossier contenant 5 images liées au Dashboard réalisé sur superset pour la visualisation
   - image1.jpg: Montre l'évolution du CO_moyen vs PM2.5 moyen dans la station1 et la station2
   - image2.jpg: Elle fait une comparaison de l'évolution du CO_moyen de la station1 vs station2 puis l'évolution de PM2.5 moyen de la station1 vs station2
   - image3.jpg: montre la valeur max de CO_moyen de le station1 vs station2 puis la valeur max PM2.5 moyen de la station1 vs station2
   - image4.jpg: montre le waterfall de CO_moyen et PM2.5 moyen de la station1
   - image5.jpg: montre le waterfall de CO_moyen et PM2.5 moyen de la station2
     
2.  `airflow.station1.csv`: le fichier csv des données agrégées de la station1


3. `airflow.station2.csv`  :  le fichier csv des données agrégées de la station2

4. `data_processing.py` : fournit un ensemble de fonctions pour l'extraction, la transformation et le chargement (ETL) de données. Ces fonctions seront utilisées par le processus ETL principal (etl.py)

5.  `etl.py`:Le script etl.py coordonne l'extraction, la transformation et le chargement (ETL) des données provenant de deux stations spécifiques en appelant les fonctions définies dans data_processing.py, puis stocke les résultats dans deux collections distinctes de MongoDB.
   
6.  `model_prediction_co_station1.joblib` : modèle pré-entraîné pour la prédiction du CO moyen de la station1

7.  `model_prediction_co_station2.joblib` : modèle pré-entraîné pour la prédiction du CO moyen de la station2

8.  `model_prediction_pm2.5_station1.joblib` : modèle pré-entraîné pour la prédiction du PM2.5 moyen de la station1

9.  `model_prediction_pm2.5_station2.joblib` : modèle pré-entraîné pour la prédiction du PM2.5 moyen de la station2

10.   `requirements.txt`: pour installer les dépendances.
    
11.  `station1_data.json` : données  json de la station1 sous forme

12. `station2_data.json` : données  de la station2 sous forme json

13.  `station1_serie_temporelle.ipynb` : Notebook pour implémenter  un modèle de prédiction de CO_moyen et PM2.5 moyen pour la station1

14. `station2_serie_temporelle.ipynb`  : Notebook pour implémenter un modèle de prédiction de CO_moyen et PM2.5 moyen pour la station2

## Installation
Avant de procéder à l'installation, assurez-vous d'être dans le répertoire du projet. Utilisez la commande suivante pour installer les dépendances nécessaires à l'aide du fichier requirements.txt :
```bash
pip install -r requirements.txt
```
## Exécution du script ETL
### Configuration de la Base de Données MongoDB
Avant d'exécuter le script ETL, assurez-vous de configurer correctement votre base de données MongoDB. Suivez ces étapes pour la configuration :

#### Étape 1: Installation de MongoDB
Assurez-vous que MongoDB est installé sur votre machine. Vous pouvez le télécharger à partir du site officiel de MongoDB sur: [Téléchargement MongoDB](https://www.mongodb.com/try/download/community)

#### Étape 2: Démarrage de MongoDB
Démarrez le serveur MongoDB en local sur le port 27017 de votre machine. Vous pouvez utiliser la commande suivante :
```bash
mongod --port 27017
```
Ou encore utiliser MongoDB Compass pour lancer un noeud Mongo. Télécharger MongoDB Compass sur :[Téléchargement MongoDB Compass](https://www.mongodb.com/try/download/shell)

#### Étape 3: Création des Collections
Ouvrez votre terminal MongoDB et assurez-vous que votre base de données "airflow" existe. Si elle n'existe pas, vous pouvez la créer en utilisant la commande suivante :
```bash
use airflow
```
Ensuite, créez les collections "station1" et "station2" dans la base de données "airflow".
```bash
db.createCollection("station1")
```
```bash
db.createCollection("station2")
```
#### Étape 4: Exécution du Script ETL
Maintenant, vous pouvez exécuter le script ETL pour extraire, transformer et charger les données dans les collections "station1" et "station2" de la base de données "airflow". Utilisez la commande suivante :
```bash
python etl.py
```
## Architecture du ETL
La structure du ETL est représentée ci-dessous :
![architecture](https://github.com/degbun/Projet_Data354_ETL_DEGBUN_JOSUE/blob/main/__pycache__/architecture.jpg)

## Vue de la base de données
Voici un exemplaire de la base de données:![base de données](https://github.com/degbun/Projet_Data354_ETL_DEGBUN_JOSUE/blob/main/__pycache__/bd_nosql.png)

## Réponses aux questions 
### 1. Quelle serait votre stratégie de mise en production de votre ETL?
La stratégie pour mettre en production notre système ETL comprend plusieurs étapes essentielles. Tout d'abord, nous nous assurerons de sa stabilité en effectuant des tests approfondis dans un environnement de pré-production. Ces tests automatisés et d'évaluation des performances garantiront le bon fonctionnement du système avant son déploiement en production.

Les mises à jour et correctives seront gérées de manière transparente grâce à des outils de gestion de versions tels que Git. Ansible, un outil de déploiement, assurera un déploiement contrôlé. En cas de problème, des procédures de retour à la version précédente seront mises en place.

Pour gérer l'augmentation prévue de la charge, nous aurons recours à Kubernetes, qui permet un ajustement flexible de la capacité du système.
### 2. Quelle serait votre stratégie pour que declencher votre ETL automatiquement chaque heure ?
Pour automatiser l'exécution régulière de notre processus ETL toutes les heures, nous allons utiliser Apache Airflow, un outil d'orchestration de flux de travail bien établi. Voici comment nous planifions la mise en œuvre de cette stratégie de manière concrète et accessible.

- Configuration du Planificateur :

Nous allons configurer le planificateur d'Apache Airflow pour automatiser le déclenchement de notre processus ETL chaque heure à l'avenir. La définition d'un DAG avec une expression cron permettra une exécution ponctuelle et régulière de notre flux de travail, assurant ainsi la mise à jour périodique de nos données.

- Gestion des Erreurs :

Pour renforcer la fiabilité de notre système à l'avenir, nous allons intégrer une gestion proactive des erreurs à chaque tâche du DAG. En cas d'échec d'une tâche, des notifications immédiates seront déclenchées pour alerter notre équipe, facilitant ainsi une intervention rapide et efficace afin de résoudre tout problème.

En adoptant cette approche, avec une configuration soigneuse du planificateur et une gestion active des erreurs, nous nous assurerons que notre processus ETL s'exécute de manière fiable et cohérente, tout en étant prêts à réagir rapidement en cas de besoin. C'est la clé de notre stratégie réussie pour maintenir un système automatisé performant.
							
## Auteur: 
DEGBUN JOSUE
 

 
![Auteur](https://github.com/degbun/Projet_Data354_ETL_DEGBUN_JOSUE/blob/main/__pycache__/moi-modified.png)
