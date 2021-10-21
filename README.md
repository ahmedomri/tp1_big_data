Dans mon exemple je collecte les données du mois de décembre à partir du site Web de Bay Wheels https://s3.amazonaws.com/baywheels-data/index.html. Puis je crée ma table dans le nootebook, Et je récupère le DataFrame en utilisant SPARK SQL. 
En passant à l’exploration des données j’ai utilisé la méthode « to_pandas() » de PySpark pour pouvoir utilisé pandas  pour faciliter la manipulation et l'analyse des données. Ensuite j’ai pu visualiser les informations sur les données qui sont la taille du DataFrame, le type des colonnes, et si la colonne peut être null ou non. Puis j’ai visualisé les statistiques sur l’ensemble des variables. Et j’ai vérifier si les colonnes contiennent des valeurs null et j’ai calculé le pourcentage de ces valeurs pour chaque colonne. A la fin de cette visualisation j’ai détecté type de Problèmes :

•	Problème de Qualité des données :
-	Types de données erronés « start_time », « end_time » et « user_type ».
-	Valeurs nulles dans les colonnes « start_station_id », « start_station_name », « end_station_id », « end_station_name » et « rental_access_method ».

•	Problèmes de propreté des données :
-	 Des colonnes individuelles sont manquantes pou « hour », « weekday name » et « duration in minute ».
-	 Les données ne sont pas ordonnées par date.
-	 Colonnes qui ne seront pas utilisées.

Pour régler ces problèmes j’ai procédé au nettoyage des données en effectuant les étapes suivantes :

•	Suppression des colonnes qui ne seront pas utilisées : "start_station_id", "end_station_id", "start_station_latitude", "start_station_longitude", "end_station_latitude", "end_station_longitude" and "bike_id" .
•	Suppression de la colonne "rental_access_method" car elle contient 81% des null.
•	Suppression des enregistrements qui contiennent des valeurs null pour les colonnes : 'start_station_name' et 'end_station_name'.
•	Attribuer le type correcte pour les colonnes : start_time, end_time , user_type .
•	Création des colonnes intermédiaires pour mieux analyser nos données : `start_time_hour`, `end_time_hour`, `time_day_of_week` et `duration_minute`.
•	Ordonner les données par date.
A la fin de cette étape on obtient notre Dataset finale qui prêt pour l’analyse.

La dernière étape c’étais l’analyse des données en passant par l’analyse univariée, bivariée et multivariée.
•	Conclusion de l’analyse univariée de la durée de trajet en minute, les heurs de déplacement, les jours de déplacement et le type d’utilisateur : 
-	La majorité des trajets a une durée comprise entre 5 et 14 minutes.
-	Lorsque nous regardons les heures de déplacement, nous constatons un pic de déplacements entre 7 et 9 et un autre pic entre 16 et 18.
-	Lorsque nous regardons les jours de la semaine, nous remarquons que du lundi au vendredi, nous avons la plupart des déplacements avec des pics le lundi et le mardi et les minimums pendant le week-end.
-	Nous voyons ici que plus de 54,4% des utilisateurs qui utilisent les services sont des clients et 45.1 sont des abonnés.

•	Conclusion de l’analyse bivariée de la durée des trajets par les autres caractéristiques :
-	Les utilisateurs "clients" ont tendance à faire des trajets plus longs que les utilisateurs "abonnés".
-	Pendant les week-ends, les gens ont tendance à faire des voyages plus longs.
-	Une forte baisse des abonnés pendant les week-ends, tandis que le client utilisateur subit une baisse moins importante.
-	Une tendance à l'augmentation des déplacements entre 8 et 9 heures et entre 17 et 18 heures, principalement pour les usagers "clients". Les usagers "Abonnés" suivent une tendance plus discrète.

•	Conclusion de l’analyse multivariée de la durée moyenne des trajets en minutes, le type d'utilisateur et les autres caractéristiques :
-	La durée moyenne d'un voyage par heure, place le "Client" avec une augmentation du temps pendant les heures du matin entre 00h et 4h où il n' y a pas de moyen de transport dans ces heures, tandis que l'"Abonné" a peu de variation pendant la journée.
-	Le "Client" consacre plus de temps aux voyages pendant le week-end, alors que l'"Abonné" a peu de volatilité pour le week-end.



