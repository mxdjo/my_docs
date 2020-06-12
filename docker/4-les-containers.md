# Les containers #

PS: Cet article est la copie d'un article de Ajdaini Hatim. J'ai vraiment aimé l'explication et ai décidé de le garder juste au cas où le blog devopssec.fr disparaissait


## Différence entre images et containers ##

Nous avons aussi vu que sur docker un conteneur est une instance d'exécution d'une image plus précisément un conteneur est ce que l'image devient en mémoire lorsqu'elle est exécutée (c'est-à-dire une image avec un état ou un processus utilisateur).

## Quelques commandes ##

### Créer un container ###

Pour créer une instance de notre image, ou autrement dit créer un conteneur, alors nous utiliserons une commande que nous avions déjà vue sur les chapitres précédents, soit:

```bash
docker run [OPTIONS] <IMAGE_NAME ou ID>
```

Nous allons pour le moment créer un conteneur basé sur l'image hello-world, et pour faire les choses dans les règles de l'art, nous allons d'abord commencer par télécharger notre image depuis le Docker Hub Registry, et ensuite on va exécuter notre image afin de créer notre conteneur.

```