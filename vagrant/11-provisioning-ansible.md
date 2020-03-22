Nous voulons utiliser notre VM vagrant comme machine de provision utilisant Ansible

```
config.vm.provision "ansible" do |ansible|
ansible.playbook = "provisioning/playbook.yml"
end
```   
Cette configuration nous permettra donc de provisionner notre VM en utilisant un playbook Ansible, à partir de notre host. Il faut donc installer Ansible sur notre Host. Aussi notre hote doit avoir une version de OpenSSH qui supporte ControlPersist.   
Si nous sommes à notre première exécution du "vagrant init" et que nous n'avons pas encore créé le fichier "provisioning/playbook.yml", on aura normalement une erreur:  
**`playbook` does not exist on the host: /home/mxdjo/learn-ansible/provisioning/playbook.yml**    


Si Ansible n'est pas installé sur notre ordinateur (par exemple, parce que nous sommes sous Windows), nous devons utiliser la configuration suivante:
```
config.vm.provision "ansible_local" do |ansible|
ansible.playbook = "provisioning/playbook.yml"
end
```
Cela permettra d'exécuter Ansible à partir de notre VM


