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
# Configuration de vm vagrant avec private network ip 192.168.33.10
