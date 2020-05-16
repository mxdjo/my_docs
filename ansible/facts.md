Quand Ansible exécute un Playbook, avant la premiere tache,il se passe ceci:

```
GATHERING FACTS **************************************************
ok: [nom_du_serveur]
```
Ansible demande en fait à l'hote slave tous les détails sur lui: CPU, OS, adresse IP,RAM, info sur le disque et autres.Les informations sont stockés dans une variable appellée *facts* et ils agissent comme les autres variables.

Un playbook pour connaitre le système d'exploitation de la machine:   
```
---
- name: get OS of all machines
  hosts: all
  gather_facts: true
  tasks:
    - debug: var=ansible_distribution
```

On a ce resultat:

```
PLAY [get OS of all machines] **************************************************

TASK [Gathering Facts] *******************************************************
ok: [slave1]
ok: [192.168.56.102]

TASK [debug] *******************************************************************
ok: [slave1] => {
    "ansible_distribution": "Ubuntu"
}
ok: [192.168.56.102] => {
    "ansible_distribution": "Ubuntu"
}

PLAY RECAP *********************************************************************
192.168.56.102             : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
slave1                     : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  

```
