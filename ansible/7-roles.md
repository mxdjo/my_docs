Maintenant que nous savons utiliser les "includes" et les variables. Nous pouvons developper les roles. Les rôles sont la manière recommandée pour developper un playbook.Les roles permettent d'organiser nos projets. Ils facilitent la réutilisation des playbook.On pourra les partager sur GitHub/GItlab ou Ansible Galaxy.  Les rôles sont créés en utilisant la commande *ansible-galaxy*

```
ansible-galaxy init webserver
```   
Quand on crée le role, Ansible Galaxy crée une structure qui contient un fichier README.md, nos tasks, nos handlers, nos variables, etc...
Nous pouvons nous-même créer manuellement cette structure
Quand un role est créé, c'est facile de l'utiliser dans un playbook.  

Une fois créé, on l'appelle dans un playbook en lieu et place des tasks   

```
- hosts: all
  roles:
    - webserver
```

