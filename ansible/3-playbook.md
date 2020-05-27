Les playbooks Ansible  sont  des fichiers YAML utilisés pour informer Ansible sur ce qu'il devrait faire.

Le concept est simple. ce n'est qu'une série de commandes (tasks) ansibles, comme celles que nous avons utilisées avec l'outil CLI ansible. Ces tâches visent un ensemble spécifique d'hôtes / groupes.   

Nous avons juste besoin de dire ce que nous voulons faire en utilisant les bons modules ansibles.   


### Notre premier playbook ###
 
Nous allons faire ping sur tous nos hôtes pour notre premier playbook.

Un playbook peut contenir:

* **hosts** :la section des cibles/machines à configurer
* **vars** : la section des variables
* **tasks**:: la section des taches à effectuer
* **handlers**: ce sont des tasks "un peu spéciales"

##### hosts #####
La déclaration des hosts ressemble à un truc de ce genre: 

```
- hosts: webservers
```

##### vars #####
Ici nous pouvons déclarer des variables qui peuvent être utilisés dans tout le playbook.

```
vars:
 apache_version: 2.6.2
```
Nous verrons devant comment mieux utiliser les variables

##### tasks #####

La section tasks est la dernière section de chaque play. Elle contient une liste des actions que vous voulez qu'Ansible exécute dans l'ordre où vous voulez qu'elles soient exécutées. 
```
tasks:
- name: install apache
  action: yum name=httpd state=installed
- name: configure apache
  copy: src=files/httpd.conf dest=/etc/httpd/conf/httpd.conf
- name: restart apache
  service:
    name: httpd
    state: restarted
```

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

### Paramètres optionnels dans les playbooks ####

En plus des _tasks_ et des _hosts_, on peut avoir dans un playbook _become_ qui permet d'exécuter le playbook en tant qu'autre utilisateur ( root) par exemple, _vars_ qui définit une liste de variables et leurs valeurs

### Vérifier son playbook avec ansible-lint ###
ansible-lint nom_du_playbook

ansible-lint doit cependant être installé avec pip

```
pip install ansible-lint
```

### Exercice ###
Créons un playbook qui permet d'installer la Stack LAMP sur Ubuntu/Debian

