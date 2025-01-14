# refabes-docker


## Introduction
refabes-docker est un projet qui a pour vocation de regrouper les différentes instances Openrefine.

## Prérequis

Disposer de :
- ``docker-compose``
- ``.env-dist``

Ce projet se compose de deux fichiers, le premier "docker-compose.yml" regroupe les paramètres, répertoires et profils des instances Openrefine.
Le dernier fichier ".env-dist" est un template pour la création du fichier .env qui sera utilisé pour les variables d'environnement.

## Liste des Openrefine présent à l'ABES :

|  Nom |
|-------------------:|
| refalignements | 
| refbacon | 
| refhub   | 
| refidref | 
| refmovies |
| reforcid | 
| refperio | 
| refsudoc | 
| reftheses | 

## Installation 

Déployer la configuration docker dans un répertoire :
```bash
# adaptez /opt/pod/ avec l'emplacement où vous souhaitez déployer l'application
cd /opt/pod/
git clone https://github.com/abes-esr/refabes-docker.git refxxxxxx
```

Configurer l'application depuis l'exemple du [fichier ``.env-dist``](./.env-dist) (ce fichier contient la liste des variables) :
```bash
cd /opt/pod/refXXXXXXX/
cp .env-dist .env
# personnaliser alors le contenu du .env
```

## Démarrage et arrêt

Pour lancer l'instance(s), il faut bien penser à modifier la variable OPENREFINE_CONTAINER_NAME présent dans le fichier .env. On retrouve cette valeur à plusieurs endroits dans le [fichier ``docker-compose.yml``](./docker-compose.yml) :
```bash
OPENREFINE_CONTAINER_NAME=refxxxxx
```
Puis, il suffit de rentrer la commande suivante :

```bash
sudo docker compose up -d
```
Pour stopper une instance :

```bash
cd /opt/pod/refXXXXXXX/

docker-compose down
```

Pour redémarrer une instance :
```bash
docker-compose restart
```

Pour supprimer les données :

```bash
docker compose down -v

#Et supprimer les volumes : 
rm -fr volumes
```

## Allocation de ressources pour les conteneurs

Pour ajuster l'allocation de ressources pour les conteneurs (par exemple, mémoire, CPU), vous pouvez modifier la valeur des variables d'environnement suivantes dans votre fichier ``.env`` :

- `OPENREFINE_MEM_LIMIT`: Mémoire allouée au conteneur (par exemple: "512m" pour 512 Mo), valeur par défaut "5g".
- `OPENREFINE_CPU_LIMIT`: CPU alloué au conteneur (par exemple: "0.5" pour allouer 50% d'un CPU), valeur par défaut "5".
- `OPENREFINE_PORT`: Définit le port à utiliser.
- `OPENREFINE_VERSION` : Définit la version de l'image à utiliser.
- `OPENREFINE_REFINE_MEMORY` : Définit la valeur mémoire JAVA HEAP à utiliser.

## Mises à jour 

Pour mettre à jour les containers sur les nouvelles versions d'Openrefine, il faut créer une nouvelle release de l'image, à partir de ce dépôt : [Openrefine
](https://github.com/abes-esr/openrefine)


Une fois la nouvelle release créée, il faut alors modifier la version à utiliser dans le .env.

## Sauvegarde
Pour sauvegarder les données des différents projets, il faut faire une sauvegarde complète du répertoire "./volumes/refXXXXX".

## Restauration

Pour restaurer un projet, il faut récupérer le backup de celui-ci, vérifier qu'il soit bien au format XXXXXX.project et le copier dans le répertoire /volumes/refXXXXX correspondant. Openrefine pourra alors le détecter et l'afficher sur la page d'accueil.
