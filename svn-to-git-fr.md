# Migration d'un dépôt svn vers git

## Création du fichier users

Il va falloir dans un premier temps créer un fichier de correspondance des users svn vers ceux de git.

Ce fichier est structuré de la manière suivante :

user_svn = Prénom Nom <email>

Pour faciliter la récupération des users, le script suivant sera utile :

```bash
#!/usr/bin/env bash
authors=$(svn log -q | grep -e '^r' | awk 'BEGIN { FS = "|" } ; { print $2 }' | sort | uniq)
for author in ${authors}; do
  echo "${author} = NAME <USER@DOMAIN>";
done
```

Il permettra de récupérer tous les users ayant effectués un commit dans le dépôt.

Pour l'utiliser rien de plus simple, il va falloir créer un fichier users.sh, y copier le script et l'exécuter dans un dépôt local svn.

Le script va afficher dans le terminal les informations des users svn. Il faut copier le résultat et l'insérer dans un fichier users.txt.

Maintenant la prochaine étape est de compléter le NAME et USER@DOMAIN par les bonnes informations.

## Création du dépôt git en local

Maintenant que l'on a nôtre fichier de users complété on va cloner le projet svn via git, cela nous permettra de conserver l'historique svn dans git.

```bash
git svn clone --authors-file ~/users.txt https://scm.site.com/svn/projet/trunk projet-git
```

**Note** : ~/users.txt correspond au chemin vers le fichier de correspondance créé juste au-dessus.

Pour le reste cela ne change pas d'un clone habituel avec git à la différence que l'on ne cible pas un dépôt git mais svn.

Laissez le temps à git de rapatrier les fichiers en local.

## Vérification du bon fonctionnement du clone

Rendez-vous dans le projet à peine cloné et contrôlez que le fichier de correspondance a bien été appliqué.
En ligne de commande cela donne : git log.

Vous aurez alors quelque chose comme :

```
commit 22752b20d42010a51726a4a5c91ad13e1708c3d6
Author: **Yohan Tambe** <**yohan.tambe@gmail.com**>
Date:   Fri Aug 22 11:51:22 2014 +0000

    Ajout d'une admin de traduction

    git-svn-id: https://scm.site.com/svn/project/trunk@406 703f388a-15d5-4b26-bb9c-851d89ded662
```

Si la ligne "Author" n'est pas correctement renseignée c'est que la table de correspondance n'était pas correcte. Dans ce cas il va falloir réitérer l'opération.

## Push vers le dépôt distant git

On va maintenant pusher vers le dépôt git.

Dans un premier temps on va indiquer à git où envoyer les fichiers. Cela se fait via la commande suivante :

```bash
git remote add origin url
```

L'url sera donnée par gitlab sur la page d'accueil du projet. Elle se forme de la façon suivante :

`git@gitlab.site.com:project/project.git`

Une fois cela effectué il ne reste plus qu'à envoyer les fichiers sur le dépôt. Voici la commande :

git push -u origin master

Le paramètre -u (alias de --set-upstream) permet de créer la branche master sur origin. Les prochains push sur le master ne nécessiteront donc plus le paramètre -u pour pusher.

Voilà tout est maintenant fonctionnel pour travailler sous git.
