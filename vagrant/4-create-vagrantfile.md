### Qu'est ce qu'un Vagrantfile ###

Le **Vagrantfile** est le fichier indispensable pour configurer notre machine virtuelle.
Toutes les configurations liées à la VM y sont.


### Pourquoi ne l'avons nous pas créé au début ####

Comme nous l'avons vu précédemment, la première étape dans la configuration d'un projet Vagrant est de créer un **Vagrantfile**.  
nous avons commencé notre apprentissage par la commande "vagrant init".En réalité, cette commande crée un Vagrantfile dans le dossier où nous l'exécutons.  
La syntaxe des Vagrantfiles est Ruby. Cependant Hashicorp (la société derrière le projet Vagrant) nous assure qu'il n'est pas nécessaire de connaitre Ruby pour créer un Vagrantfile car ce ne sont que des déclarations de variables qu'on fait.  

### Chemin de recherche des Vagrantfiles ###
Lorsque nous exécutons la commande *vagrant* , Vagrant remonte l'arborescence des dossiers pour rechercher un Vagrantfile.  
Si la commande est exécutée dans le dossier */home/johndoe/projets/learn/*, Vagrant recherchera les fichiers dans cet ordre jusqu'à trouver le fichier Vagrantfile.   

```
/home/johndoe/projets/learn/Vagrantfile
/home/johndoe/projets/Vagrantfile
/home/johndoe/Vagrantfile
/home/Vagrantfile
/Vagrantfile
```

Il est possible de changer le chemin de début de la recherche en modifiant la variable d'environnement VAGRANT_CWD.  

### Syntaxe de configuration ###
Si vous exécutez la commande *vagrant init* dans un dossier vide, le contenu du ficher Vagrantfile est de ce format:

```
Vagrant.configure("2") do |config|
  # ...
end
```   
Le "2" sur la première ligne représente la version de l'obet *config* qui sera utilisé pour la configuration du bloc ( le bloc commence par "do" et finit au "end").Cet objet peut être différent d'une version de Vagrant à une autre.   
Actuellement il existe 2 versions supportées. La version 1 représente la configuration de Vagrant 1.0.x et la version pour les versions de 1.1 à 2.0.x.

```
**Vagrant.configure("2") do |config|**   
//Toute la configuration liée à la machine virtuelle est ici

	**config.vm.provider "virtualbox" do |vb|
//Toute la configuration liée au provider est sous cette section

	**end**
**end**
```

exemple une VM Centos 7 avec 4 Go de RAM

```
Vagrant.configure("2") do |config|
	config.vm.box = "centos/7"
 	config.vm.provider "virtualbox" do |vb|
	vb.memory = "4096"
  end
end
```

