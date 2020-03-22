###  Definition de python3 comme interpréteur par défaut ###
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
vim /etc/ansible/ansible.cfg
```
### (Optionnel)Configuration de vm vagrant avec private network ip 192.168.33.10 ###

Le but est d'attribuer une adresse IP à notre VM. Si vous l'avez déja fait sous Virtualbox ou Vmware Workstation, vous pouvez sauter cette étape.   
Il faut modifier le Vagrantfile comme en ajoutant ceci:

```
   config.vm.network "private_network", ip: "192.168.33.10"

```

### Configuration de la connexion SSH par clé

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
 
**note**: Avec les VM faites avec Vagrant, il faut parfois activer l'authentifciation par clé pour pouvoir copier la clé.Dans ce cas, il faut mettre le paramètre PasswordAuthentication à yes dans le fichier /etc/ssh/sshd_config

```
sudo vim /etc/ssh/sshd_config
```
```
PasswordAuthentication yes
```

Une fois la clé copiée, on peut passer à autre chose.  

