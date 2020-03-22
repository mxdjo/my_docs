Nous voulons dire à Vagrant que nous allons utiliser un playbook Ansible contenu dans le dossier "provisioning"

```
config.vm.provision "ansible_local" do |ansible|
ansible.playbook = "provisioning/playbook.yml"
end
```

