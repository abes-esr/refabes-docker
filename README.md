# refabes-docker


## Introduction
refabes-docker est un projet qui a pour vocation de regrouper les différentes instances Openrefine.

## Prérequis
Ce projet se compose de trois fichiers, le premier "docker-compose.yml" regroupe les paramètres, répertoires et profils des instances Openrefine.
Le deuxième fichier "refine.ini", est le fichier de configuration de la mémoire des instances.

## Installation 

Pour lancer une instance, il suffit de rentrer la commande suivante :

```
sudo docker compose --profile refmovies up -d
```
