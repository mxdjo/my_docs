Quand on exécute un playbook, Ansible ramène le statut de chaque tache qu'il exécute dans son play.
EN exécutant le playbook que vous aviez écrit pour installer pour la première voir, vous avez surement vu un message de ce type:

TASK: [installer apache] *********************************************************
changed: [192.168.33.10]

Quand il est exécuté pour la seconde fois par contre, le statut est le suivant

TASK: [installer apache] *********************************************************
ok: [192.168.33.10]

### Utilité des handlers ###

Quand on crée/modifie un fichier de configuration d'un service, il faut parfois redemarrer le service pour que le changement soit pris en compte.   
Pour l'exemple, nous allons modifier le contenu du fichier /etc/ssh/sshd_config  
Nous allons activer/desactiver (chacun selon le cas dans lequel il se trouve) l'authentification par mot de passe.
Le module utilisé est "lineinfile"  

```
---
- hosts: 192.168.33.10
  tasks:
    - name: Update SSH configuration to be more secure.
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "^PasswordAuthentication"
        line: "PasswordAuthentication no"
        state: presents
```

Le changement est certes fait mais pas encore pris en compte.Il va falloir redemarrer le service. On aurait pu le faire en une seule fois en écrivant notre playbook précédent comme ceci 

```
---
- hosts: 192.168.33.10
  tasks:
    - name: Desactiver la connexion SSH par mot de passe.
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "^PasswordAuthentication"
        line: "PasswordAuthentication no"
        state: present
      notify: restart sshd
   handlers:
    - name: restart sshd
      service: 
        name: sshd
        state: restarted
```
Un handler est une tâche dont l'exécution est conditionnée par le changement d'état que renvoie une tâche.
Remarquons la présence du champ notify.Il est ce qui est suivi par Ansible pour déterminer s'il doit exécuter le handler ou pas.

Comment cela fonctionne:
1.  Ansible exécute la tache
2. Si l'état après exécution de la tache est "OK" alors Ansible n'exécute pas le handler qui est rattaché à la tâche.   
Si l'état est changed, alors Ansible exécutera le handler.   

Note: les handlers sont mis à la fin des playbook.Puisque Ansible exécute les taches selon l'ordre défini dans le play, le handler sera exécuté en dernière position.   

### Utilisation de variables ####
Il est possible d'utiliser des variables dans nos playbooks et dans nos templates.   
Les variables doivent être mises entre des doubles parenthèses: {{ variables}}.  
Pour exemple, nous utiliserons toujours le fichier /etc/ssh/sshd_config.Supposons qu'on veuille changer le Port SSH et désactiver la connexion SSH de l'utilisateur Root.Notre playbook devrait ressembler à ceci:

```
- hosts: 192.168.33.10
  tasks:
    - name: Securiser l acces SSH.
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "{{ item.regexp }}"
        line: "{{ item.line }}"
        state: present
      with_items:
         - {
            regexp: "^PasswordAuthentication",
            line: "PasswordAuthentication no"
            }
         - {
            regexp: "^PermitRootLogin",
            line: "PermitRootLogin no"
            }
         - {
            regexp: "^Port",
           line: "Port 2236"
           }
      notify: restart ssh

  handlers:
    - name: restart ssh
      service:
        name: ssh 
        state: restarted

```

### Declarer des variables dans la commande ###
On peut déclarer les variables dans la ligne de commande   

```

- name: pass a message on the command line
  hosts: localhost
  vars:
    greeting: "you didn't specify a message"
  tasks:
   - name: output a message
     debug: msg="{{ greeting }}"
```

La commande ansible-playbook est:
```
ansible-playbook greet.yml -e greeting=hiya
```


### Exercice ###
Créons un playbook qui installe wordpress sous notre serveur ubuntu/debian.   
    
**Aide**   

Installer Wordpress équivaut à:
* Installer la Stack LAMP
* Créer la base de données et l'utilisateur de cette BDD
* Télécharger l'archive de Wordpress et le désarchiver
* Configurer le fichier wp-config.php
