# Séance 7: maintenance et modules

**Note** : (_facultatif_) S'il y a des questions dans ce labo, répondez y dans un fichier nommé
`./labo/reponse-labo.md`.  Le fichier doit être dans un format `Markdown`. Utilisez le projet
`inf3135-h2020` pour déposer le fichier demandé. Utiliser le même fichier pour tous les exercices.

##### Format du fichier Markdown
 + Séance 2 (Header 1)
 + Exercice {1..n} (H2)
 + Question {1..n} (H4)
 + S`2`.E`3`.Q`1` (strong) `est une valeur qui change bien sûr`
 + La réponse dans une section script (code block)

**Note**: Il est recommandé de versionner vos réponses aux exercices à l'aide
de Git. Un seul dépôt est amplement suffisant pour tous les laboratoires, en
divisant les fichiers dans des répertoires.

 > > Pourquoi versionner vos exercices avec Git: afin de
vous entraîner à utiliser le logiciel (commandes) naturellement.

## 0 - Refaire le tp1 (en 2h)

Vous allez dans ce laboratoire refaire ou compléter le tp1.  À la fin de la période, vous devez avoir un projet
fonctionnel avec toutes les composantes nécessaires. Vous êtes capable.

## 1 - Makefile

Compléter et modifier le Makefile afin d'avoir toutes les dépendances exigées dans le tp1. Vous avez sûrement
besoin d'une cible nommée `data`. Avez-vous une cible `flop.o` ?  Avez-vous des tubes (unix) ? 
Avez-vous des commandes comme `cd` ou `..` dans votre Makefile ?  Si oui il est temps de faire le ménage. Fixez ça!

## 2 - tp1.c

Faire des tests qui ne soient pas redondants.  C'est le temps pour vous de faire le minimum.  Pour ce faire vous allez
uniquement coder les fonctions requises uniquement.  Vos tests sont-ils déterministes.  Si vous avez des random sûrement
pas.  Si vous avez des boucles dans votre code est-ce que celles-ci en font trop ?  Quand nous avons des nombres tels
que `float` ou `double` il est important de prendre des précautions.  Quelles sont telles ? Qu'avez-vous fait pour garantir
que les tests unitaires soient exactement ce que vous avez en tête ? Avez-vous des modules des fichiers d'entêtes (.h) ?

+ Q1. Combien de fonctions sont nécessaires pour tester tous les cas ?
+ Q2. Avez-vous des includes personnels ?

## 3 - valgrind

Il souhaitable d'utiliser `valgrind` pour compléter les exercices de cette séance. Vous allez donc créer une cible nommée `leak`
afin de vérifier s'il y a une fuite de mémoire dans votre programme.

+ Q1. Pourquoi utilisé valgrind ?
+ Q2. Est-ce facile d'utiliser valgrind ?
+ Q3. Est-ce que valgrind est utile ?

## 4 - liste.sh

Réviser le fichier liste.sh afin de produire ce qui est demandé. Le programme `script` nommé `liste.sh` est un programme `bash`
qui devrait être simple et court.  Assurez-vous que c'est le cas.  Il doit traiter des informations sur `stdin` et produire un
résultat sur `stdout`.

## 5 - Évaluation

Vous avez fini super.  Vous demandez au voisin de revoir votre projet.  Il doit être critique et vous dire tout ce qui ne
va pas. Vous allez faire de même pour une autre personne.  

Q1. Êtes-vous satisfait de votre livrable ? Pourquoi ?
Q2. Comment ce nomme cet exercice de révision de code d'une autre personne ?
Q3. Qu'avez-vous appris de cet exercice ?
Q4. Est-ce facile de lire le code des autres ?
Q5. Est-ce que votre projet `tp1` fonctionne mieux ?
Q6. Voulez-vous un (1) point bonus ? Est-ce que votre binôme vous donne un point ? Pourquoi ?

## - 6 Git

Assurez-vous que le labo est bien fait et envoyez vos fichiers dans gestion de version.

### FIN.
---

##### Auteur Guy Francoeur, édition H2020
