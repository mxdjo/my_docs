###  Definition de python3 comme interpréteur par défaut ###
Comme nous l'avons vu précédemment, python est l'un des pré-requis pour utiliser Ansible.  
A la date de redaction de ce fichier, Python2 est déprécié.
Il faut donc installer python3 si cela n'a pas été déja fait ( A installer selon votre distribution).
Ensuite il faut définir python3 comme interpréteur par défaut  .

```
echo "alias python=python3" >> ~/.bash_aliases
```
### Installation de Ansible ####

On peut soit installer Ansible via le gestionnaire de paquet de notre distribution ou via pip. Je préfère la seconde option.  
```
pip3 install ansible
```

### Vérification post-installation ###
Après installation de Ansible, il faut vérifier si le fichier de configuration principal a été bien généré. Pour se faire, il suffit de voir la version installée.   

```
ansible --version
```
La ligne critique est "config file" qui a parfois une valeur "none".   
Créer le fichier /etc/ansible/ansible.cfg peut régler le problème.   
```
mkdir -p /etc/ansible
```

```
touch /etc/ansible/ansible.cfg
```

Note: Ansible recherche le fichier "ansible.cfg" dans les endroits suivants (selon cet ordre):
1. Dans le fichier défini comme variable d'environnement ANSIBLE_CONFIG
2. /ansible.cfg (ansible.cfg dans le répertoire actuel)
3. ~/.ansible.cfg (.ansible.cfg dans le dossier personnel de l'utilisateur)
4. /etc/ansible/ansible.cfg

### Configuration de la connexion SSH par clé ###

La connexion se fait par SSH.  
Il faut donc configurer une connexion SSH par clé.   
On génère d'abord la clé SSH
```
ssh-keygen
```

Ensuite on copie la clé sur la machine à controler 
```
ssh-copy-id username@IPdelamachine
```
La phrase de passe nous sera demandée.  
Ce processus est un peu différent pour les VM vagrant.  

#### Gestion de clés SSH avec les VM vagrant ####

##### Méthode 1 #####

Quand on veut utiliser la méthode précédente avec les VM faites avec Vagrant, il faut parfois activer l'authentification par mot de passe pour pouvoir copier la clé SSH sur la VM vagrant.Dans ce cas, il faut mettre le paramètre PasswordAuthentication à yes dans le fichier /etc/ssh/sshd_config.
On se connecte à la VM via vagrant ssh
```
vagrant ssh
```
Ensuite on modifie le fichier de configuration du service SSH
```
sudo vim /etc/ssh/sshd_config
```
```
PasswordAuthentication yes
```
Il faut maintenant ressortir et définir une adrese IP à la machine  
Sur l'hôte Vagrant, il faut modifier le Vagrantfile en ajoutant ceci:

```
config.vm.network "private_network", ip: "X.X.X.X"

```
On peut maintenant copier la clé avec ssh-copy-id

```
ssh-copy-id username@X.X.X.X
```

On peut maintenant faire des commandes ad-hoc pour vérifier la connexion entre ansible et la machine à controler

##### Méthode 2 #####
Avez vous remarqué que vagrant ne demande pas de mot de passe lorsqu'on se connecte à un guest vagrant en utilisant "vagrant ssh". C'est parce que vagrant génère une clé sur l'hôte Vagrant pour faciliter la connexion.  
Il est possible de retrouver la clé utilisée pour une machine en démarrant la machine et utilisant la commande "vagrant ssh-config"

```
vagrant up
```

```
vagrant ssh-config
```

Les lignes qui nous intéressent sont:
``` 
HostName 127.0.0.1
  User vagrant
  Port 2222
  IdentityFile /home/mario/learning-projects/learn-ansible/.vagrant/machines/default/virtualbox/private_key
```

