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

|  Nom | Port réservé| URL dev | URL test | URL prod | Machine hôte (-dev/-test/-prod) |
|------|-------:|-------|-------|-------|-------|
| refalignements | 13334 | [https://refalignements-dev.abes.fr/](https://refalignements-dev.abes.fr/) | [https://refalignements-test.abes.fr/](https://refalignements-test.abes.fr/) | [https://refalignements.abes.fr/](https://refalignements.abes.fr/) |  diplotaxis6 |
| refbacon | 13336 | [https://refbacon-dev.abes.fr/](https://refbacon-dev.abes.fr/) | [https://refbacon-test.abes.fr/](https://refbacon-test.abes.fr/) | [https://refbacon.abes.fr/](https://refbacon.abes.fr/) | diplotaxis5 |
| refhub   | 13337 | [https://refhub-dev.abes.fr/](https://refhub-dev.abes.fr/) | [https://refhub-test.abes.fr/](https://refhub-test.abes.fr/) | [https://refhub.abes.fr/](https://refhub.abes.fr/) | diplotaxis5 |
| refidref | 13338 | [https://refidref-dev.abes.fr/](https://refidref-dev.abes.fr/) | [https://refidref-test.abes.fr/](https://refidref-test.abes.fr/) | [https://refidref.abes.fr/](https://refidref.abes.fr/) | diplotaxis4 |
| refmovies | 13341 | [https://refmovies-dev.abes.fr/](https://refmovies-dev.abes.fr/) | [https://refmovies-test.abes.fr/](https://refmovies-test.abes.fr/) | [https://refmovies.abes.fr/](https://refmovies.abes.fr/) | diplotaxis4 |
| reforcid | 13340 | [https://reforcid-dev.abes.fr/](https://reforcid-dev.abes.fr/) | [https://reforcid-test.abes.fr/](https://reforcid-test.abes.fr/) | [https://reforcid.abes.fr/](https://reforcid.abes.fr/) | diplotaxis6 |
| refperios | 13333 | [https://refperios-dev.abes.fr/](https://refperios-dev.abes.fr/) | [https://refperios-test.abes.fr/](https://refperios-test.abes.fr/) | [https://refperios.abes.fr/](https://refperios.abes.fr/) | diplotaxis3 |
| refsudoc | 13339 | [https://refsudoc-dev.abes.fr/](https://refsudoc-dev.abes.fr/) | [https://refsudoc-test.abes.fr/](https://refsudoc-test.abes.fr/) | [https://refsudoc.abes.fr/](https://refsudoc.abes.fr/) | diplotaxis3 |
| reftheses | 13342 | [https://reftheses-dev.abes.fr/](https://reftheses-dev.abes.fr/) | [https://reftheses-test.abes.fr/](https://reftheses-test.abes.fr/) | [https://reftheses.abes.fr/](https://reftheses.abes.fr/) | diplotaxis2 |




## Installation 

Déployer la configuration docker dans un répertoire :
```bash
# adaptez /opt/pod/ avec l'emplacement où vous souhaitez déployer l'application
cd /opt/pod/
git clone https://github.com/abes-esr/refabes-docker.git refxxxxxx-docker
```

Configurer l'application depuis l'exemple du [fichier ``.env-dist``](./.env-dist) (ce fichier contient la liste des variables) :
```bash
cd /opt/pod/refXXXXXXX-docker/
cp .env-dist .env
# personnaliser alors le contenu du .env
```

## Démarrage et arrêt

Pour lancer l'instance, il faut bien penser à modifier la variable OPENREFINE_CONTAINER_NAME présent dans le fichier .env. On retrouve cette valeur à plusieurs endroits dans le [fichier ``docker-compose.yml``](./docker-compose.yml) :
```bash
OPENREFINE_CONTAINER_NAME=refxxxxx-docker
```
Puis, il suffit de rentrer la commande suivante :

```bash
sudo docker compose up -d
```
Pour stopper une instance :

```bash
cd /opt/pod/refXXXXXXX-docker/

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

- `OPENREFINE_MEM_LIMIT`: Mémoire allouée au conteneur et définit égalament la valeur mémoire JAVA HEAP à utiliser. (par exemple: "512m" pour 512 Mo).
- `OPENREFINE_CPU_LIMIT`: CPU alloué au conteneur (par exemple: "0.5" pour allouer 50% d'un CPU), valeur par défaut "5".
- `OPENREFINE_PORT`: Définit le port à utiliser.
- `OPENREFINE_VERSION` : Définit la version de l'image à utiliser.

## Mises à jour 

Pour mettre à jour les containers sur les nouvelles versions d'Openrefine, il faut créer une nouvelle release de l'image, à partir de ce dépôt : [Openrefine
](https://github.com/abes-esr/openrefine)


Une fois la nouvelle release créée, il faut alors modifier la version à utiliser dans le .env.

## Sauvegarde
Pour sauvegarder les données des différents projets, il faut faire une sauvegarde complète du répertoire "./volumes/refabes" de l'instance que l'on souhaite sauvegarder, ainsi qu'une copie du .env

## Restauration d'une instance

Pour restaurer une instance Openrefine, il faut récuperer la sauvegarde du .env du projet concerné. Puis se mettre dans le repertoire /opt/pod/ et refaire les étapes d'installation.

```bash
# adaptez /opt/pod/ avec l'emplacement où vous souhaitez déployer l'application
cd /opt/pod/
git clone https://github.com/abes-esr/refabes-docker.git refxxxxxx-docker
```
Enfin, placer la sauvegarde du .env dans ce répertoire et lancer le docker-compose.yml.

## Restauration d'un projet

Pour restaurer un projet, il faut récupérer le backup de celui-ci, vérifier qu'il soit bien au format XXXXXX.project et le copier dans le répertoire /volumes/refabes de l'instance que l'on souhaite restaurer. Openrefine pourra alors le détecter et l'afficher sur la page "Ouvrir un projet". 
