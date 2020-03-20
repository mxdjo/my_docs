### Installation de vagrant ###
L'installation est vraiment facile.   
Il suffit de récupérer le paquet compatible à notre plateforme sur le site https://www.vagrantup.com/downloads.html 


### Notre premiere box ####
Pour notre premiere box, nous allons utiliser alpine. C'est aussi possible d'utiliser le "Ubuntu" de Hashicorp mais il est trop lourd pour des premiers tests.

On saisira les commandes suivantes:

```
vagrant init alpine/alpine64
```
```
vagrant up
```

La première commande va créer un fichier "Vagrantfile" indispensable pour initialiser une box.   

#### Connexion à la machine ####

La commande "vagrant up" va créer une machine virtuelle sur Virtualbox et ayant comme OS alpine.   
On peut normalement se connecter à la machine par ssh en utilisant la commande suivante: 
```
vagrant ssh
```

#### Destruction de la machine ####
Un des gros avantages de Vagrant c'est la facilité de création et de destruction de VM.Nous avons vu plus haut comment créer une machine, la destruction se fait avec la commande "vagrant destroy"

```
vagrant destroy
```


