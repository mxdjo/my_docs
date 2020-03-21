Vagrant suit le concept de box.   
Les boxes sont des images de base utilisés pour cloner des machines virtuelles.  
A la date de rédaction, le catalogue des Boxes est le lien suivant : https://app.vagrantup.com/boxes/search

Les noms des box sont selon la nomenclature suivante: **user/nomDeLabox**
Je vous conseille d'utiliser le filtre des résultats pour choisir les Boxes compatibles avec son provider (Virtualbox dans mon cas).  
Comme premiere box, je choisis une box Centos.   

Plusieurs choix s'offrent à nous cependant la box officielle est "centos/7".  
L'installation de la box se fait avec la commande suivante:  
```
vagrant box add centos/7
```

Pour voir la list des boxes téléchargés:
```
vagrant box list
```

On peut supprimer une box en faisant:
```
vagrant box remove user/box
```

