Il est possible de faire une synchronisation de dossiers de sorte à pouvoir partager les fichiers de la machine host à la VM et vice versa et cela sans utiliser un outil tiers comme SCP (ou WinSCP pour les WIndows).  
Ce pourrait aussi être utile quand on veut coder et qu'il n'y a pas d'éditeur du style VScode ou Sublime Text sur notre VM si cette dernière est un OS serveur sans interface graphique.   

### Création du dossier sur la machine Guest ###
Supposons que nous avons toujours une VM CentOS 7.   
On se connecte avec **vagrant ssh** et on crée le dossier avec **mkdir**
```
vagrant ssh
```
On se rend dans le dossier personnel de l'utilisateur vagrant et on crée un dossier "mesSupersFichiers"

```
mkdir mesSupersFichiers
``

### Configuration du Vagrantfile ###

Supposons que sur ma machine host le dossier à synchroniser est nommé **src** et se trouve dans le meme repertoire que le Vagrantfile.Le fichier Vagrantfile devra être configuré ainsi:  
```
Vagrant.configure("2") do |config|
  # autres configurations ici

  config.vm.synced_folder "src/", "/home/vagrant/mesSupersFichiers"
end

```

Une fois terminée, on redemarre la VM avec la commande "vagrant reload"

```
vagrant reload
 ```

### Test ###

Pour tester, on se rend sur la VM dans le dossier créé et on crée un fichier.  
On crée un autre fichier sur la machine host et on vérifie si les deux fichiers sont présents sur les deux machines.  

