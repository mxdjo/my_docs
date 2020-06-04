Pour définir une variable d'environnement sur le serveur distant:
il faut le déclarer au niveau que hosts et tasks 
```
- name: Deploy a web application
  hosts: slave1,slave2
  become: true
  vars:
    mysql_root: "rootmysql"

  environment:
     FLASK_APP: /opt/app.py
```
