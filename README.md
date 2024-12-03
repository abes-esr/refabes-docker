# refabes-docker


## Introduction
refabes-docker est un projet qui a pour vocation de regrouper les différentes instances Openrefine.

## Prérequis

Disposer de :
- ``refine.ini``
- ``docker-compose``
- ``.env-dist``

Ce projet se compose de trois fichiers, le premier "docker-compose.yml" regroupe les paramètres, répertoires et profils des instances Openrefine.
Le deuxième fichier "refine.ini", est le fichier de configuration de la mémoire des instances.
Le dernier fichier ".env-dist" est un template pour la création du fichier .env qui sera utilisé pour les variables d'environnement.


## Installation 

Déployer la configuration docker dans un répertoire :
```bash
# adaptez /opt/pod/ avec l'emplacement où vous souhaitez déployer l'application
cd /opt/pod/
git clone https://github.com/abes-esr/refabes-docker.git
```

Configurer l'application depuis l'exemple du [fichier ``.env-dist``](./.env-dist) (ce fichier contient la liste des variables) :
```bash
cd /opt/pod/refabes-docker/
cp .env-dist .env
# personnaliser alors le contenu du .env
```

## Démarrage et arrêt

Pour lancer une instance, il suffit de rentrer la commande suivante :

```bash
sudo docker compose --profile refmovies up -d
```
Pour stopper une instance :

```bash
cd /opt/pod/refabes-docker/

docker-compose --profile refmovies down
```

Pour redémarrer une instance :
```bash
docker-compose restart
```

Pour supprimer les données :

```bash
docker compose --profile refmovies down -v

#Et supprimer les volumes : 
rm -fr volumes
```

## Allocation de ressources pour les conteneurs

Pour ajuster l'allocation de ressources pour les conteneurs (par exemple, mémoire, CPU), vous pouvez modifier la valeur des variables d'environnement suivantes dans votre fichier ``.env`` :

- `OPENREFINE_REFXXXX_MEM_LIMIT`: Mémoire allouée au conteneur (par exemple: "512m" pour 512 Mo), valeur par défaut "5g".
- `OPENREFINE_REFXXXX_CPU_LIMIT`: CPU alloué au conteneur (par exemple: "0.5" pour allouer 50% d'un CPU), valeur par défaut "5".
- `OPENREFINE_REFXXXX_PORT`: Définit le port à utiliser.
- `OPENREFINE_REFXXXX_VERSION` : Définit la version de l'image à utiliser. 

