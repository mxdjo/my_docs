Certains modules recherchent les fichiers/dossiers dans un dossier par défaut.   
L'arborescence du projet peut être ainsi:  
```
|── files
│   └── app
│       ├── index.php
│       └── search.php
|       
|
|── templates
│   ├── db-config.php.j2
│   └── table.sql.j2
|   
|── vars
│   └── main.yml
|  
└── ansible.cfg
└── hosts
└── Playbook.yml

```
Le playbook sera ainsi:   

```
  - name: remove default index.html
    file:
      path: /var/www/html/index.html
      state: absent

  - name: upload web app source
    copy:
      src: app/
      dest: /var/www/html/

  - name: deploy php database config
    template:
      src: "db-config.php.j2"
      dest: "/var/www/html/db-config.php"

```
Notez qu'on n'a pas eu besoin de préciser le chemin complet(files/app/) car le module copy regarde par défaut dans le dossier files.  
Voici les dossiers par défaut par module:
* **module copy: files/**    

On a la structure suivante:
```
.
├── ansible.cfg
├── files
│   └── test.txt
└── playbook.yml

```

On veut par exemple copier sur le fichier test notre slave ansible.

On fera ceci:   
```
- name: copy file from local host to remote host (relative path, ./files/)
  copy:
    src: test.txt
    dest: $HOME/test.txt
```
copy se chargé d'utiliser le chemin relatif *files/test.txt*.    
On peut cependant utiliser le chemin absolu */chemin/vers/files/test.txt* mais la premiere methode est la meilleure


* **module template: templates/**
