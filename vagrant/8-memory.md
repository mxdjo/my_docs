Par défaut, Vagrant attribue 512 Mo de RAM à la VM.
Pour customiser,il faut configurer le Vagrantfile comme ceci:

```

Vagrant.configure("2") do |config|
 
config.vm.provider "virtualbox" do |vb|

	vb.memory = "MEMOIRE_EN_MB"
	end
end
```
