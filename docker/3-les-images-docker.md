# Les images #

 Sur Docker, un conteneur est lancé en exécutant une image. "Attends mais c'est quoi une image Docker" ?

Une image est un package qui inclut tout ce qui est nécessaire à l'exécution d'une application, à savoir :

* le code
* L'exécution
* Les variables d'environnement
* Les bibliothèques
* Les fichiers de configuration

Une image docker est créée à partir d'un fichier nommé le Dockerfile. Une image est un modèle composé de plusieurs couches, ces couches contiennent notre application ainsi que les fichiers binaires et les bibliothèques requises. Lorsqu'une image est instanciée, son nom est un conteneur, un conteneur est donc une image en cours d'exécution.

 Pour mieux comprendre le système de couche, imaginons par exemple qu'on souhaite déployer notre application web dans un serveur LAMP (Linux Apache MySQL PHP) au moyen de Docker. Pour créer notre stack (pile en français), nous aurons besoin de :

* Une couche OS pour exécuter notre Apache, MySQL et Php
* Une couche Apache pour démarrer notre serveur web et pourquoi pas la config qui va avec (.htaccess, apache2.conf, site-available/, etc ...)
* Une couche php qui contiendra un interpréteur Php mais aussi les bibliothèques qui vont avec (exemple : php-curl)
* Une couche Mysql qui contiendra notre système de gestion de bases de données Mysql

Au total, notre image docker sera composée de 4 couches

![couches docker lamp](images/docker-lamp-image-layers.png)

Source: devopssec.fr - apprendre docker

## Lsiter les images Docker téléchargées ##

Dans les chapitres précédents, nous avions lancé la commande "docker run hello-world".  Pour information cette commande télécharge une image depuis le Docker Hub Registry et l'exécute dans un conteneur. Lorsque le conteneur s'exécute, il vous affiche un petit message d'information et se ferme directement.

 Voici la commande qui permet de répertorier les images Docker téléchargées sur votre ordinateur :

```bash

docker image ls

```

 ou encore la commande:

```bash
docker images
```

 Resultat

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        5 months ago        13.3kB
```

## Supprimer une image Docker ##

 Maintenant si on souhaite supprimer une image Docker, on aura besoin soit de son soit de son nom. Une fois qu'on aura récupéré ces informations, on peut passer à la suite en lançant la commande suivante :

avec l'id de l'image :

```bash
docker rmi bf756fb1ae65  
```

avec le nom de l'image

```bash
docker rmi hello-world
```

Cette commande enverra un message d'erreur

```bash
Error response from daemon: conflict: unable to remove repository reference "hello-world" (must force) - container 76ee57d41b9d is using its referenced image bf756fb1ae65
```

Ce message d'erreur nous explique, qu'on ne peut pas supprimer notre image Docker car des conteneurs ont été instanciés depuis notre image "hello-world" (dans notre cas le container avec l'ID 76ee57d41b9d). En gros si on jamais on supprime notre image "hello-world", ça va aussi supprimer nos conteneurs car ils se basent sur cette image. Dans notre cas ça ne pose aucun problème, d'ailleurs pour résoudre ce problème l'erreur nous informe qu'on doit forcer la suppression pour éliminer aussi les conteneurs liés à notre image (must force)

Pour forcer la suppression, on utilise l'option --force ou -f

```bash
docker rmi -f hello-world
```

Quand nous avons plusieurs images avec le même nom mais avec des tags différents alors vous devez préciser le tag dans votre commande rmi, pour ainsi être sûr de supprimer la bonne image. Pour information par défaut Docker prend le tag latest.

Voici une commande qui permet de supprimer toutes les images disponibles sur notre machine :

```bash

docker rmi -f $(docker images -q)
# docker images -q : montre seulement les ID de nos images
```

## Télécharger une image depuis le Docker Hub Registry ##

Maintenant rentrons dans du concret et téléchargeons une image plus utile comme par exemple l'image officielle d'Ubuntu. "Oui mais ou est-ce que je peux retrouver la liste des images disponibles ?"

Un Registry (registre en français) est une application côté serveur qui permet de stocker et de distribuer des images Docker, le Docker Hub Registry est le registre officiel de Docker.

Il existe deux façons pour voir si une image est disponible dans le Docker Hub Registry, la première consiste à visiter le site web et vous recherchez directement le nom de l'image dans la barre de recherche
 La deuxième manière pour lister les images disponibles dans le Docker hub Registry, c'est de passer par la ligne de commande :

```bash
 docker search ubuntu

```

Resultat

```bash
NAME                                                      DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
ubuntu                                                    Ubuntu is a Debian-based Linux operating sys…   10995               [OK]                
dorowu/ubuntu-desktop-lxde-vnc                            Docker image to provide HTML5 VNC interface …   438                                     [OK]
rastasheep/ubuntu-sshd                                    Dockerized SSH service, built on top of offi…   244                                     [OK]
consol/ubuntu-xfce-vnc                                    Ubuntu container with "headless" VNC session…   220                                     [OK]
ubuntu-upstart                                            Upstart is an event-based replacement for th…   109                 [OK]                
ansible/ubuntu14.04-ansible                               Ubuntu 14.04 LTS with ansible                   98                                      [OK]
neurodebian                                               NeuroDebian provides neuroscience research s…   68                  [OK]                
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5      ubuntu-16-nginx-php-phpmyadmin-mysql-5          50                                      [OK]
ubuntu-debootstrap                                        debootstrap --variant=minbase --components=m…   44                  [OK]                
nuagebec/ubuntu                                           Simple always updated Ubuntu docker images w…   24                                      [OK]
i386/ubuntu                                               Ubuntu is a Debian-based Linux operating sys…   21                                      
1and1internet/ubuntu-16-apache-php-5.6                    ubuntu-16-apache-php-5.6                        14                                      [OK]
1and1internet/ubuntu-16-apache-php-7.0                    ubuntu-16-apache-php-7.0                        13                                      [OK]
eclipse/ubuntu_jdk8                                       Ubuntu, JDK8, Maven 3, git, curl, nmap, mc, …   12                                      [OK]
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mariadb-10   ubuntu-16-nginx-php-phpmyadmin-mariadb-10       11                                      [OK]
1and1internet/ubuntu-16-nginx-php-5.6-wordpress-4         ubuntu-16-nginx-php-5.6-wordpress-4             7                                       [OK]
1and1internet/ubuntu-16-apache-php-7.1                    ubuntu-16-apache-php-7.1                        6                                       [OK]
darksheer/ubuntu                                          Base Ubuntu Image -- Updated hourly             5                                       [OK]
pivotaldata/ubuntu                                        A quick freshening-up of the base Ubuntu doc…   4                                       
1and1internet/ubuntu-16-nginx-php-7.0                     ubuntu-16-nginx-php-7.0                         4                                       [OK]
pivotaldata/ubuntu16.04-build                             Ubuntu 16.04 image for GPDB compilation         2                                       
1and1internet/ubuntu-16-php-7.1                           ubuntu-16-php-7.1                               1                                       [OK]
1and1internet/ubuntu-16-sshd                              ubuntu-16-sshd                                  1                                       [OK]
pivotaldata/ubuntu-gpdb-dev                               Ubuntu images for GPDB development              1                                       
smartentry/ubuntu                                         ubuntu with smartentry                          1                                       [OK]
```

On souhaite n'avoir que les images officielles

```bash
docker search --filter "is-official=true" ubuntu

```

Pour télécharger une image, il faut faire la commande

```bash
docker pull ubuntu
```

Par défaut, l'image téléchargée est *latest*.On peut cependant préciser l'image que nous voulons avec un tag.

```
docker pull ubuntu:16.04
```
