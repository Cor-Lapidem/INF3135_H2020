# Séance 6: Type abstrait de données et modularité

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

## 0a - Makefile

Pour tous les exercices qui suivent, vous devez ajouter au fichier `Makefile` ce qui est nécessaire pour automatiser
la production de vos exécutables (et/ou objets).  De plus, il est souhaitable de produire une cible de test pour chacun.

Si vous cherchez des noms pour vos `exécutables` et `cibles` labo_05_1, labo_05_2, ... etc. Il s'agit, 
de mot labo suivi du numéro de la séance, et, terminant par le numéro de l'exercice.

Il est fort possible que je visite votre dépôt pour vérifier vos avancements.

À ceci, vous allez ajouter deux cibles :
+ all_labo_test :
+ all_labo_build :

Vous avez aussi compris que `all_labo_test` est dépendant de `all_labo_build`.

## 0b - valgrind

Il souhaitable d'utiliser `valgrind` pour compléter les exercices de cette séance.

+ Q1. Pourquoi utiliser valgrind ?

## 1 - Implémentation d'une pile (*stack*)

- Une pile contient des objets insérés et retirés selon le principe dernier inséré, premier sorti (last-in-first-out LIFO);
- Les objets peuvent être insérés à tout moment, mais seulement le dernier (le plus récemment inséré) peut être retiré;
- La _stack_ est ordonnée;

```c
// stack.h

//libre à vous, faites votre implémentation
//je vais vérifier les solutions
```

+ Q1. Quelle est la différence entre les mots anglais suivant : stack vs pile vs heap ?
+ Q2. Produire un fichier d'entête (.h).
+ Q3. Produire un fichier source (.c).
+ Q4. Produire un fichier test_stack.c qui référence et utilise les fichiers `.h` et `.c`.
+ Q5. Produire un fichier Makefile pour automatiser certaines tâches.

## 2 - Implémentation d'une file (*queue*)

Complétez l'implémentation d'une structure de données de type "file" (en anglais *queue*) à partir des déclarations suivantes:

```c
typedef struct Queue_s {
  int capacity;
  int size;
  int front;
  int rear;
  int *elements;
} Queue_t;

extern Queue_t * initQ(int maxQueueSize);
extern void dequeueQ(Queue_t *Q);
extern int frontQ(Queue_t *Q);
extern void enqueueQ(Queue_t *Q,int element);
extern void deleteQ(Queue_t *Q); // finir par ceci (bien vu Fanny)
```

+ Dans cet exercice, nous voulons prendre de bonnes habitudes, et tenter de réaliser un `type abstrait de données` de façon autonome.
+ Le but est de le rendre le `type abstrait`, le plus complet possible sans optimisation de code.
+ Il n'y a pas de mauvaise réponse à priori.
+ Assurez-vous de gérer correctement la mémoire (sans fuite de mémoire)!

Questions:
+ Q1.  Quelle est la difficulté que vous avez rencontrée ?
+ Q2.  Avez-vous des fuites de mémoire ou des accès illicites à des zones mémoires (*out of bounds*) ?

## 3 - Implémenter un Array Dynamique (*Vector*)

Dans cet exercice vous devez construire une structure de données capable d'accepter un nombre `limite de int` d'éléments.
Lors de la création, vous devez déterminer la capacité, exemple 2.  Lorsque cette capacité sera insuffisante, vous devrez
étendre le Vecteur.

Voici la définition et les prototypes

```c
typedef struct {
  int size;      // slots used so far
  int capacity;  // total available slots
  int *data;     // array of integers we're storing
} Vector_t;

extern void initV(Vector_t *vector, int capacity);
extern void appendV(Vector_t *vector, int value);
extern int getV(Vector_t *vector, int index);
extern void setV(Vector_t *vector, int index, int value);
static void extendV(Vector_t *vector);
extern void freeV(Vector_t *vector);
```

Questions :
+ Q1. Quelle est la difficulté que vous avez rencontrée ?
+ Q2. Avez-vous des fuites de mémoire ou des accès illicites à des zones mémoires (*out of bounds*) ?
+ Q3. Avez-vous eu recours à internet ou des exemples pour compléter l'exercice ?

### FIN.
---

##### Auteur Guy Francoeur, édition H2020
###### basé sur le matériel d'Alexandre Blondin Massé, Professeur
