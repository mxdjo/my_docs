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
