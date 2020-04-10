Les playbooks Ansible  sont  des fichiers YAML utilisés pour informer Ansible sur ce qu'il devrait faire.

Le concept est simple. ce n'est qu'une série de commandes (tasks) ansibles, comme celles que nous avons utilisées avec l'outil CLI ansible. Ces tâches visent un ensemble spécifique d'hôtes / groupes.   

Nous avons juste besoin de dire ce que nous voulons faire en utilisant les bons modules ansibles.   


### Notre premier playbook ###
 
Nous allons faire ping sur tous nos hôtes pour notre premier playbook.

Chaque playbook doit contenir:
* des hôtes à configurer
* une liste de tâches à exécuter sur ces hôtes 

```
---
### Le playbook commence par les trois tirets du haut

#On définit ensuite les hôtes sur lesquels executés ces plays et les tasks
- hosts: all
  tasks:
   - name: Make sure that we can connect to the machine
     ping:

```

On exécute le playbook avec la commande :

```
#ansible-playbook chemin_vers_le_play/nom_du_playbook

ansible-playbook playbook.yml
```
### Notre second playbook  ###

Nous allons maintenant faire un playbook pour installer le serveur web apache.  
Je précise que la machine à provisionner est un debian-based.  
Le module pour faire les installations de paquets sur les systèmes Debian-based est le module **apt**. La documentation pour utiliser bien ce module est ici https://docs.ansible.com/ansible/latest/modules/apt_module.html  
On peut aussi avoir la documentation d'un module en ligne de commande "ansible-doc nom_du_module"
   

Notre playbook pour installer Apache sera comme suit:   

```
--
- hosts: all
  tasks:
    - name: Installer un serveur web apache2 sur notre Debian
      apt:
        name: apache2
        state: present


```
Nous aurons normalement une erreur "Permission denied". Ce qui est tout à fait normal car l'installation de paquets nécessite des droits de super utilisateur.Cependant Ansible se connecte par défaut avec l'utilisateur 'vagrant' (dans mon cas). C’est là que l’option **become** (qui contrôle quel utilisateur exécute les commande) est très pratique. "become" peut être ajouté à deux endroits différents dans notre playbook. Il peut être ajouté à côté de la tâche qui nécessite plus d'autorisations, ou il peut être ajouté au niveau de chaque playbook, ce qui signifie que chaque commande sera exécutée avec autorisations d'administrateur.   
Notre playbook devient:
``` 
---
- hosts: all
  become: true
  tasks:
    - name: Installer un serveur web apache2 sur notre Debian
      apt:
        name: apache2
        state: present
```

On exécute le playbook:  
```
ansible-playbook playbook.yml
```

Parfois cela peut nécessiter de préciser le mot de passe du super utilisateur.Dans ce cas, on utilise l'option --ask-become-pass  ou -K   
```
ansible-playbook -K playbook.yml
```

### Vérifier son playbook avec ansible-lint ###
ansible-lint nom_du_playbook

ansible-lint doit cependant être installé avec pip

```
pip install ansible-lint
```

### Exercice ###
Créons un playbook qui permet d'installer la Stack LAMP sur Ubuntu/Debian

