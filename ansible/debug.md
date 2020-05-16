```
- name: show return value of command module
  hosts: server
  tasks:
   - name: capture output of id command
     command: id -un
     register: login
   - debug: var=login
```
The output of the debug module would look like this:

```
TASK: [debug var=login] *******************************************************
ok: [server1] => {
"login": {
"changed": true,
"cmd": [
"id",
"-un"
],
"delta": "0:00:00.002180",
"end": "2015-01-11 15:57:19.193699",
"invocation": {
"module_args": "id -un",
"module_name": "command"
},
"rc": 0,
"start": "2015-01-11 15:57:19.191519",
"stderr": "",
"stdout": "vagrant",
"stdout_lines": [
"vagrant"
]
"warnings": []
```
* la clé changed: est présente dans les valeurs retournées par les modules Ansible. Pour les modules command et shell, c'est toujours à moins qu'on mette une clause: changed_when.   
* la clé cmd: contient les commandes invoquées.
* la clé rc: contient les codes de retour. Si c'est un non-zero, Ansible assume que la tache a échoué dans l'exécution.  
* la clé stderr: contient le message d'erreur    


