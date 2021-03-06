# Les containers #

PS: Cet article est la copie d'un article de Ajdaini Hatim. J'ai vraiment aimé l'explication et ai décidé de le garder juste au cas où le blog devopssec.fr disparaissait

## Différence entre images et containers ##

Nous avons aussi vu que sur docker un conteneur est une instance d'exécution d'une image plus précisément un conteneur est ce que l'image devient en mémoire lorsqu'elle est exécutée (c'est-à-dire une image avec un état ou un processus utilisateur).

## Quelques commandes ##

### Récuperation des informations ###

 Pour commencer on va d'abord récupérer la liste des commandes possible :

 ```bash
 docker help

 ```

 A la fin du résultat, nous avons cette ligne:

 ```bash
Run 'docker COMMAND --help' for more information on a command.

 ```

 Cette ligne nous informe qu'il est possible d'avoir de l'auto-complétion sur n'importe quelles sous-commandes/options de Docker, je m'explique, si vous tapez la commande suivante (avec un espace à la fin et sans la lancer) :

 ```bash
 docker volumes
 ```

 Résultat

 ```bash
 create   -- Create a volume
inspect  -- Display detailed information on one or more volumes
ls       -- List volumes
prune    -- Remove all unused volumes
rm       -- Remove one or more volumes
```

Il est possible d'avoir des informations sur notre installation Docker

```bash
docker info
```

Resultat

```bash
Client:
 Debug Mode: false

Server:
 Containers: 1
  Running: 0
  Paused: 0
  Stopped: 1
 Images: 1
 Server Version: 19.03.11
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
### Suite en bas ####
```

### Créer un container ###

Pour créer une instance de notre image, ou autrement dit créer un conteneur, alors nous utiliserons une commande que nous avions déjà vue sur les chapitres précédents, soit:

```bash
docker run [OPTIONS] <IMAGE_NAME ou ID>
```

Exemple: docker run dockertraining/hello_world

La première fois que nous exécutons la commande, Docker doit déterminer si dockerinaction/
hello_world est déjà installé. S'il ne parvient pas à le localiser sur votre ordinateur (car
c'est la première chose que vous faites avec Docker), Docker passe un appel vers Docker Hub. Docker Hub est un registre public fourni par Docker Inc. Docker Hub répond à l'exécution de Docker sur votre ordinateur où dockertraining/hello_world peut être trouvé, et
Docker démarre le téléchargement.

![Docker run pour la 1ere fois](images/docker-run-image.png)

Lorsque nous exécutons pour la seconde fois, Docker vérifie à nouveau si dockertraining/hello_world est installé. Cette fois, il le trouve et peut construire un nouveau container. Le processus est le suivant:

![Docker run pour la 2eme fois](images/docker-run-2nd.png)

Pour notre tutoriel,nous allons pour le moment créer un conteneur basé sur l'image hello-world, et pour faire les choses dans les règles de l'art, nous allons d'abord commencer par télécharger notre image depuis le Docker Hub Registry, et ensuite on va exécuter notre image afin de créer notre conteneur.

Etape 1: téléchargement de l'image hello-world

```bash
docker pull hello-world:latest
```

Etape 2: Instanciation de l'image hello-world

Créer un container, c'est créer une instance de l'image

```bash

docker run hello-world:latest
```

Avouons-le, cette image n'est pas vraiment utile, car elle n'est prévue que pour afficher un petit message d'information et en plus de ça elle se ferme directement après. Téléchargeons une image plus utile, comme par exemple l'image Ubuntu, et pourquoi pas la manipuler avec l'interpréteur de commandes bash et de télécharger dessus des outils comme l'outil git

 Étape 1 : Téléchargement de l'image ubuntu :

 ```bash
 docker pull ubuntu:latest
 ```

  Étape 2 : Instanciation de l'image ubuntu :

  ```bash
  docker run ubuntu:latest
  ```

   Vous : "Ah mais attend mais moi quand je lance mon image Ubuntu, mon conteneur se quitte directement après, est-ce que les commandes sont bonnes ? !"

   éponse est oui, vos commandes sont bien les bonnes mais ce n'est pas le cas pour vos options, car oui cette commande docker run possède beaucoup d'options consultables soit depuis la doc officielle <https://docs.docker.com/engine/reference/commandline/run/> ,  soit depuis commande docker run --help.

   Comme vous, pouvez le constater il existe beaucoup d'options, mais rassurez-vous, car vous n'avez pas besoin de tous les connaître, voici pour le moment les options qui nous intéressent pour ce chapitre :

* -t : Allouer un pseudo TTY (terminal virtuel)
* -i : Garder un STDIN ouvert (l'entrée standard plus précisément l'entrée clavier)
* -d : Exécuter le conteneur en arrière-plan et afficher l'ID du conteneur

Dans notre cas nous avons besoin d'une Tty (option -t) et du mode interactif (option -i) pour interagir avec notre conteneur basé sur l'image Ubuntu. Tentons alors l'exécution de ces deux options :

```bash
docker run -ti ubuntu:latest
```

On obtient un prompt de ce genre:

```bash
root@c1477a72f9cb:/#
```

Nous sommes maintenant à l'intérieur de notre conteneur ubuntu avec un jolie shell 😍.

Profitons-en pour télécharger l'outil git, mais juste avant n'oubliez pas de récupérer les listes de paquets depuis les sources afin que votre conteneur sache quels sont les paquets disponibles en utilisant la commande apt update, ce qui nous donnera la commande suivante :

```bash
apt update && apt install git -y
```

On peut voir la version de git installée

```bash
git --version
```

Resultat

```bash
git version 2.25.1
```

Je profite un peu de cette partie pour vous montrer la puissance des conteneurs. Je vais détruire mon conteneur Ubuntu avec la commande rm -rf /*. Si vous souhaitez faire comme moi, alors ASSUREZ-VOUS BIEN AVANT QUE VOUS ETES DANS UN CONTENEUR. Après avoir lancé cette commande je peux vous affirmer d'ores et déjà dire que j'ai bien détruit mon conteneur, preuve à l'appui je ne peux même plus lancer la commande ls

```bash
root@c1477a72f9cb:/# ls
bash: /bin/ls: No such file or directory
```

 Vous : "Mais tu es fou de lancer cette commande destructrice !"

 Ne vous inquiétez pas, je vais réparer mon conteneur en même pas 1 seconde. Je vais d'abord commencer par quitter mon conteneur avec la commande exit et ensuite je vais demander à mon moteur Docker la phrase suivante : "abra cadabra Docker crée-moi un nouveau conteneur" :

```bash
docker run -ti ubuntu:latest
```

Résultat

```bash
root@93fa34cb8cea:/# ls
bin   dev  home  lib32  libx32  mnt  proc  run   srv  tmp  var boot  etc  lib   lib64  media   opt  root  sbin  sys  usr
```

 Tout est en ordre chef ! Mon conteneur est de nouveau fonctionnel et devinez quoi cette réparation ne m'a même pas pris 1 seconde à faire (oui je tape vite au clavier 😁). Cette puissance de pouvoir créer rapidement des conteneurs à la volée avec une latence quasi inexistante est possible, car nous avions préalablement téléchargé notre image Ubuntu sur notre machine locale. Et comme notre image contient déjà son propre environnement d'exécution, alors elle est déjà prête à l'emploi et elle n'attend plus qu'à être exécutée !

Par contre dans mon nouveau conteneur, si je lance la commande git --version, alors je vais obtenir une belle erreur m'indiquant que git est inexistant dans mon conteneur.

```bash
bash: git: command not found
```

 Pourquoi ? Car les données et les fichiers dans un conteneur sont éphémères !

Vous : "Quoi ? Il existe bien un moyen pour sauvegarder mes données ??? Dit moi oui please please ???"

Bien sûr que oui, sinon les conteneurs ne serviraient pas à grand-chose. Il existe deux façons pour stocker les données d'un conteneur, soit on transforme notre conteneur en image (cependant ça reste une méthode non recommandée, mais je vous montrerai à la fin de ce chapitre comment l'utiliser), soit on utilise le système de volume, nous verrons cette notion dans un autre chapitre dédié aux volumes.

Pour le moment je souhaite vous montrer l'utilité de l'option **-p** de la commande docker run. Pour mieux comprendre cette option je vais utiliser l'image officielle d'Apache. Bon, maintenant vous connaissez la routine, on télécharge l'image et on l'exécute, mais juste avant j'aimerais bien vous montrer trois autre options utiles de la commande docker run :

* **--name** : Attribuer un nom au conteneur
* **--expose**: Exposer un port ou une plage de ports (on demande au firewall du conteneur de nous ouvrir un port ou une plage de port)
* **-p** ou **--publish**: Mapper un port déjà exposé, plus simplement ça permet de faire une redirection de port

Par défaut l'image apache expose déjà le port 80 donc pas besoin de lancer l'option --expose, pour notre exemple nous allons mapper le port 80 vers le 8080 et nommer notre conteneur en "monServeurWeb", ce qui nous donnera comme commande :

```bash
docker pull httpd:latest
```

```bash
docker run --name monServeurWeb -p 8080:80 httpd:latest
```

 Une fois votre image exécutée, visitez http://localhost:8080 ou http://@_IP_de_la_machine:8080 et vous verrez la phrase "It works"!


### Afficher la liste des container ###

Pour supprimer notre conteneur, il faut d'abord l'identifier et par la suite récolter soit son id, soit son nom. Ça sera l'occasion de vous dévoiler une commande que vous utiliserez beaucoup, cette commande vous permettra de lister les conteneurs disponibles sur votre machine.

```shell
docker container ls
```

Résultat de la commande

```shell
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
832209264a66        httpd:latest        "httpd-foreground"   3 seconds ago       Up 2 seconds        0.0.0.0:8080->80/tcp   monServeurWeb2
```
Voici l'explication des différentes colonnes :
* CONTAINER ID : id du conteneur
* IMAGE : L'image sur laquelle c'est basé le conteneur
* COMMAND : Dernière commande lancée lors de l'exécution de votre image (ici la commande httpd-foreground permet de lancer le service apache en premier plan)
* CREATED : date de création de votre conteneur
* STATUS : statut de votre conteneur, voici une liste des différents états d'un conteneur :
       
  * created : conteneur créé mais non démarré (cet état est possible avec la commande docker create)
  * restarting : conteneur en cours de redémarrage
  * running : conteneur en cours d'exécution
  * paused : conteneur stoppé manuellement (cet état est possible avec la commande docker pause)
  * exited : conteneur qui a été exécuté puis terminé
  * dead : conteneur que le service docker n'a pas réussi à arrêter correctement (généralement en raison d'un périphérique occupé ou d'une ressource utilisée par le conteneur)

* PORTS : les ports utilisés par votre conteneur
* NAMES : nom de votre conteneur


### Supprimer un container ###

 Maintenant que nous avons pu récupérer l'id ou le nom du conteneur, on est capable de supprimer notre conteneur avec la commande suivante : 

 ```bash
 docker rm <CONTAINER NAME ou ID>
 ```

Ce sera donc:

```bash
docker rm monServeurWeb
```

### Exécuter une commande dans un container ###

Il existe une commande docker exec qui permet de lancer n'importe quelle commande dans un conteneur déjà en cours d'exécution. Nous allons l'utiliser pour récupérer notre interpréteur de commande /bin/bash, ce qui aura pour but de se connecter directement à notre conteneur Apache.

```bash
docker exec -ti monServeurWeb /bin/bash
```

Pour s'amuser un peu, on va changer le message de la page d'accueil : 

```bash
echo "<h1>Docker c'est vraiment cool</h1>" > /usr/local/apache2/htdocs/index.html
```

 Pour quitter votre conteneur sans le détruire, utilisez le raccourcis suivant : Ctrl + P + Q

 ### Afficher les logs d'un container ###

  Dès fois, vous aurez besoin de déboguer votre conteneur en regardant les sorties/erreurs d'un conteneur.

Il existe pour cela la commande *docker logs* qui vient avec deux options très utiles :
* -f : suivre en permanence les logs du conteneur (correspond à tail -f)
* -t : afficher la date et l'heure de réception des logs d'un conteneur

```bash
docker logs -ft monServeurWeb
```

### Transformer son container en images ###

Voici la commande qui permet de transformer un conteneur en image, afin de stocker nos données

**Attention**
**Je le répète mais c'est très important, cette commande n'est pas vraiment recommandée, pour stocker vos données. Il faut pour ça utiliser les volumes, que nous verrons dans un autre chapitre.**

la commande est la suivante

```bash
docker commit <CONTAINER NAME or ID> <NEW IMAGENAME>
```

exemple:

```bash
docker commit monUbuntu ubuntugit
```

On peut donc voir notre nouvelle image avec "docker images"
