# COllaboration #

* Créer une branche pour travailler sur une autre version du fichier en parallèle

```bash
git branch ma-nouvelle-branche
```

* Se placer sur la branche "ma-branche"

```bash
git checkout ma-branche
```

Une fois qu'on a fini de travailler sur notre branche, il faut rapatrier les changements sur la branche master.
Pour le faire, il faut faire un merge

```bash
git merge nom-de-la-branche-a-merger
```

Pour supprimer une branche

```bash
git branch -d ma-branche
```

Il faut cependant s'assurer d'avoir mergé les changements ont été mergés sinon on aura une erreur.

