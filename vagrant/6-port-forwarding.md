Selon Wikipédia, Le réacheminement de port (port forwarding ou port mapping en anglais) consiste à rediriger des paquets réseaux reçus sur un port donné d'un ordinateur ou un équipement réseau vers un autre ordinateur ou équipement réseau sur un port donné.   
Par exemple: Si la machine invitée (la VM) exécute un serveur Web écoutant sur le port 80, vous pouvez effectuer un mappage de port transféré sur le port 8080 (ou autre) sur votre machine hôte. Vous pouvez ensuite ouvrir votre navigateur sur localhost: 8080 et parcourir le site Web, pendant que toutes les données réseau réelles sont envoyées à l'invité.   

### Définition du port forwarding ###

Le forwarding nécessite deux paramètres, le port sur la VM et le port sur l'hôte, comme ceci:

```
Vagrant.configure("2") do |config|
  config.vm.network "forwarded_port", guest: 80, host: 8080
end
```

Par défaut, le protocol utilisé est TCP.Pour utiliser le trafic UDP, il faut aussi spécifier **protocol: 'udp'** :  
```
Vagrant.configure("2") do |config|
  config.vm.network "forwarded_port", guest: 2003, host: 12003, protocol: "tcp"
  config.vm.network "forwarded_port", guest: 2003, host: 12003, protocol: "udp"
end
```
