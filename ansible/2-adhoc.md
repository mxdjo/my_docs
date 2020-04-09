## Ad-Hoc et premiers modules ##
Nous allons utiliser notre première commande ansible.  
Pour utiliser ansible à partir de la ligne de commande, nous devons fournir au moins deux éléments. Le 1er élément est Host ou le groupe d'Host que nous voulons configurer. Ensuite on fournit le module et par moment les arguments du module. On peut aussi fournir l'utilisateur qui exécute la commande. 

### Nos premieres commandes ###

Nous allons utiliser le module setup comme premier module.    

```
ansible nom_de_la_machine_ou_ip -m setup
```
Le module setup 
#On commencera par le ping ensuite module setup, shell, copy, 
