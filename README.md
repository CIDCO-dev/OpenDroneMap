# Procédure open drone map

&nbsp;



## Procédure globale

&nbsp;

1)  Préprocessing du vidéo (méthode à déterminer)

2)  Créer structure de répertoire du projet

3)  Transférer les photos via ftp dans tsunami dans le répertoire du projet

4)  Exécuter ODM

5)  Transférer les dossiers & fichiers nécessaires
```
    - /data/ODM/datasets/<nom_du_projet>/
    - odm\_filterpoints -> nuage de points -> .ply
    - odm\_georeferencing -> coordonnées -> .txt , .json , .laz
    - odm\_orthophoto -> .tif
    - odm_report/ -> pdf
```
&nbsp;

&nbsp;
## Instructions

1)  Préprocessing du vidéo


2)  Créer structure de répertoire du projet
```
-   Se connecter à tsunami

-   allez dans /data/ODM/datasets

-   créer répertoire avec le nom du projet

-   >chmod -R 777 <nom du projet> security ?
```

3)  Transférer les photos via ftp dans tsunami dans le répertoire du projet
```
-   les images doivent se retrouver dans un répertoire nommé images

-   ex: /data/ODM/datasets/<nom du projet>/images
```

4)  exécuter ODM

copier la commande et changer <nom du projet>
```
>sudo docker run -ti --rm -v /data/ODM/datasets:/datasets --gpus all opendronemap/odm:gpu --project-path /datasets <nom du projet\> --min-num-features 800
```


5)  Transférer les dossiers & fichiers nécessaires

dans "/data/ODM/datasets/\<nom\_du\_projet\>" il y aura les répertoires suivant:
```
-   odm_filterpoints/ qui contient un nuage de point

-   odm_georeferencing/ qui contient des fichiers les coordonnees gps
    de la trajectoire

-   odm_orthophoto/ qui contient 3 orthophotos identiques

-   odm_report/ qui contient un fichier pdf du rapport de traitement
    que ODM a fait (très intéressant)
```
