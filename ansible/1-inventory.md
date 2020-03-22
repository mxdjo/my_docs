Dans la gestion de la configuration, l'outil que vous utilisez doit savoir sur quelles machines il doit fonctionner. C'est ce qu'on appelle un inventaire (inventory). Sans inventaire, nous aurions un ensemble de playbooks qui définissent l'état de votre système souhaité, mais nous ne saurions pas sur quelles machines vous devez les exécuter.  

### Le fichier inventory par défaut ###

Par défaut, Ansible lit le fichier _/etc/ansible/hosts_ comme son fichier d'inventaire par défaut. Cependant, l'utilisation de ce fichier n'est pas recommandée. Nous devons donc conserver un fichier d'inventaire différent pour chaque projet que nous avons et le transmettre aux commandes ansible et ansible-playbook à l'aide de l'option –i. Un exemple d'un fichier d'inventaire qu'on passe à _ansible_ avant d'exécuter le module ping:

```
#ansible all –i /path/to/inventory –m ping
ansible all /home/my_hosts -m ping
```
Mon fichier inventory (/home/my_format) est au format INI, un peu comme ceci:  
```
host1.exemple.com
host2.example.ci
192.168.9.29
```

Si nous utilisons par le port standard SSH, nous pouvons le préciser avec ansible_port

```
192.0.1.8 ansible_port=2255
```
Il existe plusieurs autres options.Les plus utilisées sont:  
* ansible_user: L'utilisateur qui se connecte à la machine distante via SSH. ansible_user=michael serait le même que: ssh michael@host1.example.com.  
* ansible_ssh_pass: Si l'utilisateur auquel nous nous connectons à une machine requiert un mot de passe, nous pouvons le spécifier dans le fichier d'inventaire avec ansible_ssh_pass.
Remarque: Ceci est très peu sûr et vous devez utiliser l'authentification par clé SSH ou utiliser l'indicateur --ask-pass sur la ligne de commande pour fournir le mot de passe au moment de l'exécution.  
* ansible_ssh_private_key_file: Préciser Le fichier de clé SSH utilisé pour se connecter. ansible_ssh_private_key_file=/chemin/vers/id_rsa serait la même chose que ssh –i /chemin/vers/id_rsa  
* ansible_become_method: la méthode utilisée pour avoir les droits de super utilisateur.La valeur par défaut est sudo.Ce pourrait etre sudo,su ou doas.  


Il est possible de déclarer un groupe d'hôtes. L'intérèt est de pouvoir assigner des variables communes (comme le même serveur ntp/proxy..). Pour illustrer, nous utiliserons l'exemple de la documentation officielle d'Ansible

```
[atlanta]
host1
host2

[atlanta:vars]
ntp_server=ntp.atlanta.example.com
proxy=proxy.atlanta.example.com

``` 
