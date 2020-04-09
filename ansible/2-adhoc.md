## Ad-Hoc et premiers modules ##
Nous allons utiliser notre première commande ansible.  
Pour utiliser ansible à partir de la ligne de commande, nous devons fournir au moins deux éléments. Le 1er élément est Host ou le groupe d'Host que nous voulons configurer. Ensuite on fournit le module et par moment les arguments du module. On peut aussi fournir l'utilisateur qui exécute la commande. 

### Nos premieres commandes ###

Nous allons utiliser le module ping comme premier module.    

```
ansible nom_de_la_machine_ou_ip -m ping
```
Nous allons maintenant utiliser le module setup

```
ansible nom_ou_ip_machine -m setup
```
Le prochain module à utiliser est le module command. Il permet d'exécuter des commandes shell sur la machine distante

```
ansible nom_ou_ip_machine -m command -a pwd
```
Dans ce cas, on exécute la commande "pwd". L'option -a permet de donner un arguement au module. Cependant le module command est le module par défaut pour les commandes adhoc. On aurait pu donc faire: 

```
ansible nom_ou_ip_machine -a pwd
```

Vous pouvez vous référer à la documentation de Ansible pour voir les autres modules.
