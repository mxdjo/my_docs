Le fichier de configuration de ansible est ansible.cfg. 
Ansible le recherche dans cet ordre: 
* ANSIBLE_CONFIG (une variable d'environnement)
* ansible.cfg ( dans le repertoire courant)
* /home/ansible.cfg (dans le repertoire /home)
* /etc/ansible/ansible.cfg

On peut définir certains paramètres dans ce fichier,comme l'emplacement du fichier inventory, le chemin du dossier temporaire d'Ansible.
Ces paramètres sont définis dans la section [ðefaults]   

## Quelques paramètres ##
* inventory = /etc/ansible/hosts  ;  on donne le fichier où sont listés nos hotes   
* ask_pass = True ; On veut savoir si Ansible doit demander un mot de passe par defaut.Par défaut, ce paramètre est à no   
* ask_sudo_pass = True ; Similaire à ask_pass, demande le mot de passe sudo.Le comportement par défaut est à no.
* ask_vault_pass = true ; mot de passe vault   
* force_handlers = True; Cela permet de forcer les handlers meme quand la tache echoue     
* log_path=/var/log/ansible.log; par défaut pas de log.Il faut cependant s'assurer que l'utilisateur d'ansible a les droits sur le dossier d'écriture /var/log   
* remote_tmp = ~/.ansible/tmp
* local_tmp = ~/.ansible/tmp   

* module_name = command; le module par défaut utiliser la commande "ansible" (commande adhoc).Notons que le module par défaut ne supporte ni pipe, ni parametre
