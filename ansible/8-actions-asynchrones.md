# Les actions asynchrones #

Comme nous l'avons vu auparavant, Ansible utilise la connexion SSH pour gérer nos serveurs.La connexion SSH est établie pour juste le temps des taches dans notre playbook
On veut pouvoir:

* Exécuter un processus et le vérifier plus tard (donc demander que la connexion soit maintenue)

* Exécuter plusieurs actions à la fois et vérifier plus tard.

Cela peut être avec les actions asynchrones.^

* Exécuter et ne pas attendre la fin

Supposons que nous avons un script appellé /opt/monitor.sh pour monitorer nos serveurs.Ce script pour son exécution complète a besoin de 5 minutes. Nous ne voulons cependant pas qu'Ansible garde la connexion active jusqu'à ce que la tâche finisse.
On va juste dire Ansible d'exécuter la tache et vérifier chaque minute.Nous utilisons
 pour ce besoin la directive "async"

 ```YAML

- name: Deploy Web application
  hosts: webserver
  tasks:
    command: ./opt/monitor.sh
    async: 360
 ```

 Par défaut Ansible vérifie l'exécution à intervalle régulier de 10 secondes. Nous venons avec la directive de spécifier 60 secondes pour les vérifications avec la directive "poll"

  ```YAML

- name: Deploy Web application
  hosts: webserver
  tasks:
    command: ./opt/monitor.sh
    async: 360
    poll: 60
 ```

 async: pendant combien de temps exécuter la tâche
 poll: A quel intervalle de temps vérifier l'exécution

Aussi nous devons savoir que tous les modules ne supportent pas "async" donc nous devons vérifier si le module qui nous intéresse le prend en compte.
