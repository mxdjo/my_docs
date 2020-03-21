Pour installer un plugin, on fait la commande:   
```
vagrant plugin install nom_du_plugin
```

### Plugins ###
Des plugins utiles sont:
* vagrant-hostmanager : permet le fichier /etc/hosts 
* vagrant-google : Permet à Vagrant de controler et provisionner les instances GKE
* vagrant-share : Permet de partager sa VM partout dans le monde (Par SSH, HTTP ou sur un LAN). Ce qui facilite la collaboration. Ce plugin permet d'utiliser la commande "vagrant share" pour effectuer le partage https://www.vagrantup.com/docs/share/
* vagrant-aws

```
vagrant plugin install vagrant-share
```
```
vagrant plugin install vagrant-hostmanager
```
