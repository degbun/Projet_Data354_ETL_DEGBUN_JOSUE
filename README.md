# Projet_Data354_ETL_DEGBUN_JOSUE
Le projet vise à construire un ETL (Extract, Transform, Load) pour l'extraction et le traitement des données relatives à la qualité de l'air provenant de l'API AirQuino. Ensuite il s'agira de la création d'un modèle de Machine Learning pour effectuer des prévisions sur les deux prochaines heures.

## Structure du projet
1. **images/**:
    Dossier contenant 5 images liées au Dashboard sur superset pour la visualisation
   - image1.jpg: Montre l'evolution du CO_moyen vs PM2.5 moyen dans la staion1 et la station2
   - image2.jpg: Elle fait une comparaison de l'évolution du CO_moyen de la station1 vs station2 puis l'évolution de PM2.5 moyen station1 vs station2
   - image3.jpg: Montre la valeur max de CO_oyen de le station1 vs station2 puis la valeur max PM2.5 moyen de la station1 vs station2
   - image4.jpg: Montre le waterfall de CO_moyen et PM2.5 moyen de la station1
   - image5.jpg: Montre le waterfall de CO_moyen et PM2.5 moyen de la station2
2. **airflow.station1.csv** : le fichier csv aggrégées des données de la station1


3. **airflow.station2.csv** :  le fichier csv aggrégées des données de la station2

4. **data_processing.py** : fournit un ensemble de fonctions pour l'extraction, la transformation et le chargement (ETL) de données. Ces fonctions seront utilisées par le processus ETL principal (etl.py)

5. **etl.py** :Le script etl.py coordonne l'extraction, la transformation et le chargement (ETL) des données provenant de deux stations spécifiques en appelant les fonctions définies dans data_processing.py, puis stocke les résultats dans deux collections distinctes de MongoDB.
   
6. **model_prediction_co_station1.joblib** : Modèle pré-entraîné pour la prédiction du CO moyen de la station1

7. **model_prediction_co_station2.joblib** : Modèle pré-entraîné pour la prédiction du CO moyen de la station2

8. **model_prediction_pm2.5_station1.joblib** : Modèle pré-entraîné pour la prédiction du PM2.5 moyen de la station1

9. **model_prediction_pm2.5_station2.joblib** : Modèle pré-entraîné pour la prédiction du PM2.5 moyen de la station2

10. **requirements.txt** : pour installer les dépendances.
    
11. **station1_data.json** : données sous forme json de la station1

12. **station2_data.json** : données sous forme json de la station2

13. **station1_serie_temporelle.ipynb** : Notebook pour implementer modèle de prédiction de CO_moyen et PM2.5 moyen pour la station1

14. **station2_serie_temporelle.ipynb** : Notebook pour implementer modèle de prédiction de CO_moyen et PM2.5 moyen pour la station2

## Installation
```bash
pip install -r requirements.txt
```
