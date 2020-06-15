# Débuter avec git #

## Installation ##

Git est par défaut sur MacOS et la plupart des systèmes Linux modernes.
Si vous devez cependant l'installer, veuillez suivre le lien: <https://git-scm.com/downloads>

## Identité ##

La première chose à faire après installation de  git, c''est de configurer son identité. Il faut bien qu'on sache qui "blamer" :)
On doit fournir son nom et son adresse e-mail avec les commmandes suivantes:

```bash
git config --global user.name " Mon nom complet"
```

```bash
git config --global user.email "monemail@domain.com"
```

## Les commandes de bases ##

Pour mieux comprendre certaines commandes,imagineons une boîte. Vous pouvez mettre des choses dans la boîte. Vous pouvez sortir des choses de la boîte. Cette boîte est le **staging area** (traduisez la zone de transit) de Git. Nous pouvons faire des bricoles dans cette boite. Faire **un Commit**, c'est comme sceller cette boîte et y coller une étiquette. Le contenu de cette boîte est votre changement. Alors, pourquoi ne pas donner une signification à l'étiquette ? Vous n'apposeriez pas d'étiquette sur une boîte de déménagement contenant des articles de cuisine pour dire simplement "choses".


### Commencer à traquer les fichiers ###

Pour dire à git qu'on veut commencer à traquer les changements dans un fichier on utilise git init

```bash
git init
```

On peut dès cet instant voir l'état du projet ( savoir s'il y'a eu du changement non pris en compte par exemple) en utilisant git status

```bash
git status
```

Une fois qu'on crée un fichier, le status va changer. Git nous montrera le(s) fichier(s) ajouté(s)/créé(s) mais qui ne sont pas traqués.

Nous pouvons dire à git de les traquer en faisant git add. git add permet d'ajouter tous les fichiers modifiés et nouveaux (non traqués) dans le répertoire courant et tous les sous-répertoires à la *staging area* (alias l'index), les préparant ainsi à être inclus dans le prochain *commit*

```bash
git add nom_du_fichier
```

Après le add, il faut faire un commit. Le commit permet de sauvegarder le changement.On utilise l'option -m ou --message pour préciser le changement effectué.

```bash
git commit -m nom_du_fichier
# On git commit --message nom_du_fichier
```

Le "add" et le "commit" devront être faits à chaque fois pour enregistrer les changements.
Avant le add on peut faire un git diff pour voir les changements effectués.

```bash
git diff
```

Il est possible de voir tous les commit en faisant git log

```bash
git log
```

Pour chaque commit, on verra son ID, l'auteur du commit et la date à laquelle le commit a été fait.

Il est possible en une seule commande de faire un "add" et un "commit". Il suffit juste d'ajouter -a à la commande de commit

```bash
git commit -a -m "Changement effectué"
```
