Les réseaux privés Vagrant permettent d'accéder à la machine invitée par une adresse privée.   
Les plages d'adresses IP privées sont les suivantes:  
* 10.0.0.0-10.255.255.255   
* 172.16.0.0-172.31.255.255   
* 192.168.0.0-192.168.255.255  

Le network identifier pour configurer un réseau privé sur Vagrant est : **Network identifier**: private_network  

### Configuration DHCP ###
```
Vagrant.configure("2") do |config|
  config.vm.network "private_network", type: "dhcp"
end
```
Cela va attribuer une adresse IP privée. L'adresse IP peut etre déterminée après connexion par SSH (vagrant ssh), avec une commnande comme **ifconfig**

### Configuration IP statique ###
Il est aussi possible de spécifier une adresse IP à vagrant.  
```
Vagrant.configure("2") do |config|
  config.vm.network "private_network", ip: "192.168.50.4"
end
```
