# Les rôles #

Maintenant que nous savons utiliser les "includes" et les variables. Nous pouvons developper les roles. Les rôles sont la manière recommandée pour developper un playbook.Les roles permettent d'organiser nos projets. Ils facilitent la réutilisation des playbook.On pourra aussi les partager sur GitHub/GItlab ou Ansible Galaxy.  Les rôles sont créés en utilisant la commande *ansible-galaxy*

```bash
ansible-galaxy init mysql_db
```
Quand on crée le role, Ansible Galaxy crée une structure qui contient un fichier README.md, nos tasks, nos handlers, nos variables, etc...
Nous pouvons nous-même créer manuellement cette structure

On peut aussi créer les dossiers manuellement (cf arborescence du dossier webserver)

```bash
roles/
├── webserver
│   └── tasks
│       └── main.yml
└── mysql_db
    ├── defaults
    │   └── main.yml
    ├── files
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── README.md
    ├── tasks
    │   └── main.yml
    ├── templates
    ├── tests
    │   ├── inventory
    │   └── test.yml
    └── vars
        └── main.yml
```

Une fois créé, on l'appelle dans un playbook en lieu et place des tasks

```YAML
- hosts: all
  roles:
    - webserver
```

