# Procédure open drone map


## Instructions:

1)  Procédure du traitement vidéo \
1.01- Joindre les morceaux vidéos ensemble avec un logiciel de traitement de vidéo. \
\
1.02- Splitter la vidéo pour supprimer les séquences inutiles ( il faut noter la durée des séquences  supprimées pour ajuster la synchronisation de la vidéo avec les données GPS). \
\
1.03- Créer un tableau excel et inscrire le début et la fin de chaque vidéo (temps UTC), les convertir en “Running-Time” (convertir la durée en seconde). \
\
1.04- Extraire les données GPS spécifiques pour la vidéo ( en utilisant les informations en utilisants les données de l'étape 1.3). \
\
1.05- Préparer le fichier “CSV” (Long,Lat,Temps,Running-Time) \
![csv format]("https://user-images.githubusercontent.com/85508789/168834044-1dbf58fb-5070-41c1-8a41-9c61325fbb71.png")
\
1.06- Ouvrir le logiciel Dashware et charger la vidéo dans “Input Settings” \
\
1.07- Choisir le fichier GPS et le “data profile” afin d’extraire les informations utiles. \
\
1.08- Modifier l’affectation des lignes et colonnes du fichier GPS pour bien décoder les bonnes informations. \
\
1.09- Vérifier la synchronisation de la vidéo avec les données GPS, Ajuster au besoin. \
\
1.10- Validation des données avant la création de la vidéo finale en comparant le résultat avec celui obtenu avec GIS a travers le module “Analysis by position”. \
\
1.11- Créer la vidéo finale. \
\
1.2- Extraire les images avec ffmpeg ou autre:
ffmpeg -i VIDEO -vf fps=X PATH/frame%d.png
example:
```
ffmpeg -i video.mp4 -vf fps=5 ~/projet/photos_set/frame%d.png
```
1.3- interpoler les coordonnees et ajouter le metadata aux images a l'aide d'un script \
TODO :
- lien vers code du script
- format du fichier excel
- comment executer le script

2)  Créer structure de répertoire du projet

-   Se connecter à tsunami en ssh\
\
2.1)    instruction de connexion ssh: \
https://drive.google.com/file/d/1EIDbcydEsTeYsmdIYh2SNnl2VOy8Px1g/view?usp=sharing

-   allez dans /data/ODM/datasets
```
cd /data/ODM/datasets
```
-   créer répertoire avec le nom du projet
```
mkdir nom_du_projet
```
-   changer les permissions
```
chmod -R 777 nom_du_projet
```

3)  Transférer les photos via ftp dans tsunami dans le répertoire du projet\
\
3.1)    instruction de connexion ftp: \
https://drive.google.com/file/d/1EIDbcydEsTeYsmdIYh2SNnl2VOy8Px1g/view?usp=sharing

-   les images doivent se retrouver dans un répertoire nommé images\
ex: /data/ODM/datasets/nom_du_projet/images

4)  exécuter ODM

copier la commande et changer la variable nom_du_projet
```
sudo docker run -ti --rm -v /data/ODM/datasets:/datasets --gpus all opendronemap/odm:gpu --project-path /datasets nom_du_projet --min-num-features 800
```


5)  Transférer les dossiers & fichiers nécessaires

dans "/data/ODM/datasets/nom_du_projet" il y aura les répertoires suivant:
-   odm_filterpoints/ qui contient un nuage de point

-   odm_georeferencing/ qui contient des fichiers pour les coordonnées gps
    de la trajectoire

-   odm_orthophoto/ qui contient 3 orthophotos identiques

-   odm_report/ qui contient un fichier pdf du rapport de traitement
    que ODM a fait (très intéressant)
