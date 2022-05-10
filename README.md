# Procédure open drone map


## Instructions:

1)  Procédure du traitement vidéo \
https://docs.google.com/document/d/1KOqPm8Hj5J-rNuk6TQHmydN5djKZmRTZ73CtMEVwr1I/edit


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
