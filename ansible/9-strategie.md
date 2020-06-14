# Stratégie #

## Strategy ##

Supposons qu'on a un playbook à exécuter sur une multitude de serveurs. 
Par défaut, Ansible exécute la première tache sur tous les serveurs avant de passer à la deuxième qui elle aussi devra être exécutée sur tous les serveurs avant la troisième ...
Cette stratégie est appelée stratégie linéaire.
Pour que chaque serveur exécute les taches de façon indépendante (sans attendre que les autres finissent), on utilise une autre stratégie: free

```yaml
- name: Deployer des Applications
  strategy: free
  hosts: host1, host2, host4
  tasks:
  ##Suite du code
```

Il existe au moment de la redaction de cet article 4 stratégies: debug, free, host_pinned et linear. Voir <https://docs.ansible.com/ansible/latest/plugins/strategy.html#strategy-plugins>

Il est possible de changer la strategie par défaut en la définissant dans le fichier de configuration ansible.cfg sous la section [defaults]

```ini
[defaults]
strategy = free
```

## Forks ##

On sait que Ansible exécute les taches de façon parallèle sur les serveurs.Cependant par défaut, le nombre de **serveurs simultanément configuré** est limité à **5**

On peut changer ce nombre dans le fichier de configuration ansible.cfg. 

```ini
[defaults]
forks = 30
```

```bash
ansible-playbook -f 30 mon_playbook.yml
```

 On peut aussi faire la précision lors de l'exécution du playbook


Il faut cependant s'assurer que nous avons la ressource suffisante en CPU et RAM et bande passante.

