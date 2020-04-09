### C'est quoi Ansible ###

Michael DeHaan a pris le nom Ansible dans le livre Ender's Game de Orson Scott C
ard. Dans ce livre, l'ansible était utilisé pour controler un nombre important d
e bateaux à distance et au même moment. Nous pouvons prendre les bateaux comme une métaphore de serveurs distants.   
Ansible est souvent décrit comme un outil de gestion de configuration de la même catégorie que _Chef_, _Puppet_ et _Salt_. Quand on parle de gestion de configuration, on fait allusion aux outils décrivant l'état des serveurs, ensuite utilisant quelques outils pour s'assurer que les paquets voulus sont installés, les fichiers de configuration contiennent les valeurs attendues ou aient les permissions voulues, les services dont on a besoin sont activés, etc...  

### Comment fonctionne Ansible ###

Mettre image ici   
Un utilisateur qu'on appelera Marc utilise Ansible pour configurer trois serveurs Ubuntu qui doivent faire tourner le service nginx.  
Elle va écrire un script Ansible appellé _serveursweb.yml_.Dans le vocabulaire Ansible, ce script est appellé *Playbook*. Un playbook décrit quels _hosts_(serveurs distants) configurer et la liste des _tasks_ (taches pour les anglophobes) à exécuter sur ces hosts. Pour avoir le service nginx fonctionnel sur nos 3 serveurs, il faut :
* Installer le paquet nginx
* Générer un fichier de configuration nginx
* Démarrer le service nginx

Ainsi sera les 3 tasks à écrire dans notre playbook serveursweb.yml.  
Une fois le playbook écrit, il faut l'exécuter en utilisant la commande *ansible-playbook*  
Ansible va se connecter par SSH aux 3 serveurs puis exécuter la première tache sur les 3 de façon simultanée.Dans notre exemple, la première tache sera d'installer le paquet:

```
- name: "Installer Nginx"
  apt:
    name: nginx
    state: present
```
Ansible va:
1. générer un script Python qui installe le paquet nginx
2. copier le script sur les 3 serveurs
3. Exécuter le script sur les serveurs
4. Attendre que l'exécution soit complète
5. Passer à la prochaine tache dans le playbook

Notons que Ansible exécute les taches dans l'ordre que nous avons spécifié dans le playbook.   

### Avantages d'Ansible ###
Quelles sont les raisons qui peuvent pousser à choisir Ansible au détriment des autres outils de gestion de configuration?  
1. La syntaxe facile des playbooks: Le language utilisé pour les playbooks est le YAML, un language facile à lire et à écrire( tant que vous respectez les indentations) 
2. Pas/peu de dépendance: Pour gérer un serveur avec Ansible, il faut que ce serveur ait SSH et Python 2.5+, ou encore Pyton2.4 associé à la librairie Python simplejson.    
3. Un outil **Push-based** : Certains outils de gestion de configuration comme Chef et Puppet utilisent des agents. Ils sont dits "pull-based" par défaut. Sur un système pull based, les étapes de configuration sont les suivantes : 
* Vous faites un changement dans le script de gestion de la configuration  
* Vous faites un "push" vers le service central de gestion de configuration
* Les agents installés sur les serveurs à configurer se reveillent, font des vérification régulières selon un temps défini
* Les agents se connectent au service central de gestion
* Les agents téléchargent la nouvelle configuration dans les scripts

Par constrate, avec les outils Push-based par défaut comme Ansible
* On modifie le playbook
* On exécute le playbook
* Ansible se connecte aux serveurs, exécute les modules qui changent l'état des serveurs

L'approche push-based a un avantage signifiant: nous choississons quand faire un changement sur les serveurs sans attendre un certain temps.    
Vous aurez pu choisir un outil pull-based. 
Cependant je choisis personnellement Ansible à cause de la communauté qui la soutient.Tout projet open-source n'est rien sans sa communauté. Avec le mouvement Devops, plusieurs personnes s'intéressent au langage Python

### Que devons nous avoir comme pré-requis pour utiliser Ansible ###
Ansible vient pour faciliter certaines choses. Il faut cependant savoir comment cela se fait plus ou moins de façon manuelle. Parmi les pré-requis, l'utilisateur d'Ansible doit savoir:  
* Se connecter à une machine en utilisant Ansible
* Installer des paquets
* Créer des utilisateurs/groupes
* Utiliser la commande sudo
* Définir les permissions sur un fichier
* Démarrer ou arrêter un service
* ...
Si vous êtes familiers avec ces choses, vous pourrez utiliser facilement Ansible. Aussi Ansible utilise YAML pour les playbooks et Jinja2 pour les templates donc nous aurons à apprendre ces deux languages qui sont cependant faciles à comprendre.  

