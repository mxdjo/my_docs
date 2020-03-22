Dans la gestion de la configuration, l'outil que vous utilisez doit savoir sur quelles machines il doit fonctionner. C'est ce qu'on appelle un inventaire (inventory). Sans inventaire, nous aurions un ensemble de playbooks qui définissent l'état de votre système souhaité, mais nous ne saurions pas sur quelles machines vous devez les exécuter.  

### Le fichier inventory par défaut ###

Par défaut, Ansible lit le fichier _/etc/ansible/hosts_ comme son fichier d'inventaire par défaut. Cependant, l'utilisation de ce fichier n'est pas recommandée. Nous devons donc conserver un fichier d'inventaire différent pour chaque projet que nous avons et le transmettre aux commandes ansible et ansible-playbook à l'aide de l'option –i. Un exemple d'un fichier d'inventaire qu'on passe à _ansible_ avant d'exécuter le module ping:

```
#ansible all –i /path/to/inventory –m ping
ansible all /home/my_hosts -m ping
```
