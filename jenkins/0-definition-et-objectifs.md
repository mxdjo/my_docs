# Jenkins, kézako #

Jenkins est un outil d'automatisation open source écrit en Java avec des plugins conçus pour l'intégration continue. Jenkins est utilisé pour construire et tester vos projets logiciels en continu, ce qui permet aux développeurs d'intégrer plus facilement les modifications apportées au projet et aux utilisateurs d'obtenir plus facilement une nouvelle version. Il vous permet également de livrer votre logiciel en continu en l'intégrant à un grand nombre de technologies de test et de déploiement.

Jenkins réalise l'intégration continue à l'aide de plugins. Les plugins permettent l'intégration de différentes étapes de DevOps. Si vous souhaitez intégrer un outil particulier, vous devez installer les plugins pour cet outil. Par exemple : Git, Maven 2, Amazon EC2, éditeur HTML, etc.


## Fonctionnement de Jenkins ##

![architecture Jenkins](images/jenkins-architecture.png)

Source image: edureka https://www.edureka.co/blog/what-is-jenkins/

Le schéma ci-dessus illustre le fonctionnement de Jenkins :

* Tout d'abord, un développeur push le code sur le dépôt de code source. Pendant ce temps, le serveur Jenkins vérifie à intervalles réguliers si des modifications ont été apportées au dépôt.
* Peu de temps après le commit, le serveur Jenkins détecte les changements qui ont eu lieu dans le dépôt de code source. Jenkins récupère ces changements et commence à préparer une nouvelle version.
* Si la compilation échoue, l'équipe concernée en sera informée.
 Si la compilation est réussie, Jenkins déploie alors le serveur de test intégré.
* Après les tests, Jenkins génère un retour d'information et informe les développeurs des résultats de la compilation et des tests.
* Il continuera à vérifier le dépôt de code source pour les changements apportés au code source et le processus entier se répète sans cesse.

## Intégration continue, Définition ##

Nous avons vu que Jenkins est un logiciel d'intégration continue mais qu'est-ce qu'une intégration continue ?
C'est une pratique de développement qui permet aux développeurs de pouvoir apporter des modifications sur leur code source. Cela va simplement permettre de voir s'il y a des problèmes/bugs ou non.

De surcroît, l'intégration continue permet aux développeurs de ne pas attendre que le logiciel soit développé intégralement pour procéder aux tests. Et permet aussi de ne pas oublier d'élèments afin d'améliorer la qualité du produit.

Elle est assurée via les plugins.

Pour que l'intégration soit envisageable sur un projet, quelques pré-requis doivent être mis en place, à savoir :

* Partager le code source de l'application entre tous les développeurs en utilisant Git par exemple.

* Mettre en place des tests d'intégration de manière automatisés.

L'intégration continue comporte certains avantages tels que :

* Les tests automatisés permettent d'identifier les eventuels changements assez rapidement.

* Les problèmes d'intégration étant détectés rapidement, ils seront ainsi corrigés sans avoir à attendre.

Mais aussi un désavantage :

L'intégration continue engendre des frais supplémentaires

## Livraison continue ##

Pendant que l'intégration continue (CI) est le processus qui consiste à automatiser la construction et le test du code chaque fois qu'un membre de l'équipe apporte des modifications au contrôle de version. La livraison continue (CD) est quant à elle le processus de construction, de test, de configuration et de déploiement d'un environnement de construction à un environnement de production.

Sources: https://www.supinfo.com/articles/single/7077-jenkins
https://www.edureka.co/blog/what-is-jenkins/
