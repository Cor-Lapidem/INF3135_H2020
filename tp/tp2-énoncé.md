# Travail pratique 2

#### Guy Francoeur :copyright: édition H2020

  L'objectif est de continuer notre initiation à la programmation avec le langage C. Cette fois nous allons
  un peu plus loin dans notre processus de création et de réflexion.  Vous devez dans ce travail livrer un
  programme de qualité irréprochable qui tient compte de critères déjà vus. Spécifiquement vous devez lire
  et produire des données sur l'entrée et la sortie standard respectivement.
  
  De plus, vos sources seront maintenues dans un gestionnaire de version/source de type git.
  
  La compréhension et la prise de décision sont aussi des objectifs à atteindre durant la mise en oeuvre,
  la réalisation, de vos travaux.
  
  Le travail est à réaliser **individuellement**.

## Sujet (rappel)

Chaque session nous avons un sujet unique que nous traînons pendant les 15 semaines.  Cette fois encore,
je continue avec cette bonne habitude.  L'avantage est que nous n'avons pas à apprendre des sujets différents
pour chaque travail pratique.  Ainsi nous pouvons vraiment concentrer l'effort sur ce qui est important, 
c'est-à-dire la construction et la maintenance de logiciels.  Pour nous c'est avec le langage C.  Un langage
de programmation important qui produit des logiciels dits performants, mais il n'en serait rien sans des
programmeurs qui savent ce qu'ils font.

MCAS est un logiciel qui a été installé sur des avions. Le Boeing 737 MAX 8 est l'avion qui utilise ce système.
Il existe des problèmes avec ce système.  Nous allons tenter ensemble de réaliser des programmes qui sont
similaires et qui traitent des problèmes rencontrés.  ICI Radio-Canada a produit un bijou de reportage qui
traite de ce sujet.  Je vous invite à regarder et comprendre sans assumer de faits le vidéo de l'émission
découverte qui suit. Bonne écoute.

[Video BOEING 737 MAX 8 : DES RÉVÉLATIONS TROUBLANTES :copyright: ICI Radio-Canada (Découverte)](https://ici.radio-canada.ca/tele/decouverte/site/segments/reportage/141372/boeing-max-ecrasement)

## Description du travail

  Vous devez dans un fichier nommé `tp2.c` coder la nouvelle version du système MCAS.  Ce système gère des
  données en entrée (stdin) et en sortie (stdout).  Il est très compliqué de déployer des programmes dans un
  avion.  C'est une activité critique qui ne laisse pas de place pour l'erreur.  Vous devez réussir du premier
  coup, il n'y a pas de place pour une deuxième chance.  La date de livraison doit être respectée.

  Cette fois vous utiliserez les fonctions valides disponibles dans `flop.h` et `flop.o` pour réaliser le travail.
  
  Le rôle du programme `tp2.c` et de son exécutable est de traiter toutes les lignes de données.  Dans certains
  cas vous avez à produire des données sur le canal standard.  Ceci simule le dialogue (les données) des boîtes
  noires de l'avion.  Le résultat en sortie est celui qui sera évalué.
  
  Le programme exécutable peut être lancé en ligne de commande avec différentes syntaxes :

```bash
$ ./tp2

$ cat file.dat | ./tp2

$ ./script.sh | ./tp2

$ head -n 100 file.txt | ./tp2
...
```

#### Vous devez réaliser le travail selon les contraintes suivantes:

- Les fichiers d'entête standard sont tous permis. Tel que `#include <stdio.h>`;
- Vous devez utiliser les fichiers `flop.h` et `flop.o` qui sont fournis dans `tp2.zip`;
- `cUnit` est la librairie non standard acceptée (car elle ne fait pas du langage C de base) ;
- Les questions devront **toutes** être posées dans le forum de discussion GitHub section *Issues*;
- Vous devez contribuer aux questions posées au moins une fois maximum deux fois;
- Une demande de solution (réponse), comment faire ceci ou cela sera considéré comme un **plagiat**;
- Votre travail sera réalisé et livré dans le dépôt distant `inf3135-h2020-tp1`, toujours privé;
- Les fichiers seront maintenus dans la branche nommée `tp2`;
- La branche `master` est pour les rétroactions et commentaires de l'enseignant;
- Ne garder que les fichiers essentiels dans votre projet (dépôt distant);
- La gestion des répertoires doit se faire de façon absolue (nommé) à partir de votre répertoire de travail;
  + Vous ne pouvez pas utiliser `..` ou la commande `cd` dans votre travail;
- La simplicité de vos livrables est exigée.  Aucun code ésotérique ne sera accepté.

Définition :
 + ésotérique : Se dit d'un mode d'expression, d'une œuvre qui n'est compréhensible que des initiés;

Synonyme :
 + mystérieux : Qui est incompréhensible ou inexplicable;

Source : Larousse FR

#### Critère d'évaluation pour les fonctions
- un angle d'incidence est valide pour les intervalles inclusifs suivants :
   + TARMAC entre 0.2 et -0.2
   + DECOLLAGE entre 2.5 ET 51.0
   + VOL entre 9.0 et -9.0
   + ATTERRISSAGE (APPROCHE) entre -0.5 et -29.5
- la borne inférieure afin de considérer les volets ouverts (valeur incluse)
   + 0.900
- ~~la tolérance entre les angles des volets (gauche vs droite)~~
   + ~~0.5~~
- la tolérance du stabilisateur horizontal (gauche vs droite) est inférieure ou égale à
   + 0.300
- le MCAS est désactivé si l'angle du stabilisateur horizontal est en dehors de 
   + -1.900 et 1.900
- la tolérance entre les capteurs d'angle d'incidence doit être inférieur ou égale à
   + 0.250 
- la tolérance entre les capteurs de l'ouverture (longueur) des volets est inférieure ou égale à 
   + 1.250 **volet_ouverture_marge(G, D)**
- la longueur maximale d'un volet (cette fonction n'est pas fournie)
   + 108.000 **aucune fonction existe pour ce critère**
 
 **NOTE les valeurs sont inclusives.**

 **ATTENTION les valeurs ne devront jamais être arrondi. Vous devez considérer 3 décimales seulement.**
 
### Rôle de votre programme

 Le rôle de votre programme est de lire des transactions.  Les transactions sont décrites dans la section
 **Transaction en entrée / Transaction en sortie**.  Les transactions sont très formelles.  Il s'agit d'un
 système dit critique, aucune nuance possible.  Ceci ne veut pas dire que les transactions ou le système
 est exempt d'erreurs.  Vous ne devez, en aucun temps (jamais), laisser le hasard gérer la situation.

Voici comment les cas et les traitements :
 + Si un capteur donne une valeur inacceptable, vous devez réagir immédiatement;
   - voir cas trx `03`: timestamp = 161;
   - un code de trx `08` sera généré;
 + Si un capteur donne `ERROR`, vous devez réagir à la troisième manifestation de `ERROR`;
   - voir cas `04`: timestamp = {176, 178, 179};
   - un code de trx `06` sera généré;
 + MCAS doit être déactivé lorsqu'un `système` est en erreur;
   - voir cas trx `05`;
 + MCAS sera réactivé lorsque tous les `systèmes` seront opérationnels;
   - voir cas trx `05`: cas particulier.
   - voir cas trx `06` et `07`;
   - les trx `06` sont utilisées avec les trx `07`;
 + MCAS n'est pas actif lorsque les volets sont ouverts;

### Transaction en entrée

01: Changement d'état de l'appareil
 + ```<timestamp> 01 <etat>```
 + ```<size_t> 01 <ETAT_TARMAC = 0, ETAT_DECOLLAGE, ETAT_VOL, ETAT_ATTERRISSAGE, ETAT_ETEINT>```
```
91 01 0
1929999 01 4
1979998 01 9
```

02: Lecture d'un capteur d'angle d'incidence
 + ```<timestamp> 02 <A1|A2> <angle|ERROR>```
 + ```<size_t> 02 <A1|A2|A3> <float|ERROR>```
```
124 02 A1 5.5
125 02 A2 ERROR
129 02 A3 5.6
141 02 A4 10.5 //n'existe pas
142 02 A1 377.29 //est une erreur à gérer. les valeurs acceptées sont entre [0-360] degrés
...
144 02 A1 12.125
145 02 A2 24.250
```

03: Lecture de longueur de l'ouverture d'un volet (gauche ou droite)
 + ```<timestamp> 03 <G|D> <longueur|ERROR>```
 + ```<size_t> 03 <G|D> <float|ERROR>```
```
145 03 G 0.0
146 03 D 1.0019
151 03 G 11.200
156 03 D 12.100
161 03 D -1.700
167 03 G ERROR
170 03 G 10.000
171 03 G 12.500
```

04: Lecture d'un capteur de l'angle stabilisateur horizontal
 + ```<timestamp> 04 <G|D> <angle|ERROR>```
 + ```<size_t> 04 <G|D> <float|ERROR>```
```
175 04 G 0.5
176 04 D ERROR
176 04 G 0.56
178 04 D ERROR
179 04 D ERROR
```

05: Erreur provenant d'un autre système
 + ```<timestamp> 05 <système> <error_code>```
 + ```<size_t> 05 <[11-19]> <unsigned int>```
 + error_code = 0 , signifie un rétablissement, de nouveau fonctionnel
 
```
183 05 19 911
185 05 19 0
191 05 15 1
198 05 16 2
199 05 15 0
```

### Transaction en sortie

> > La première ligne à écrire est la version de la librairie flop.
> >
> > Le mot `version #:` suivit de l'information de version retourné par la fonction `flop_version(...)`
> > contenu dans flop.h et flop.o
> >
> > similaire à
```
version #: 0.0.10004
```

06: Détection des erreurs de système
 + ```06 <système> <timestamp> [information additionnelle]```
 + ```06 <VOLET=11,SH,AI,ETAT|[15-19]> <size_t> [ ... ]```
 
07: Système de nouveau fonctionnel 
 + ```07 <système> <timestamp>```
 + ```07 <VOLET=11,SH,AI,ETAT|[15-19]> <size_t>```

08: Détection d'une valeur inacceptable provenant de senseurs
 + ```08 <sensor> <timestamp> [information additionnelle]```
 + ```08 <VOLET=11|SH|AI|ETAT> <size_t> [D|G|valeur]```

09: Indication des moments où le système MCAS est actif ou inactif
 + ```09 <MCAS> <ON|OFF>```
 + ```09 MCAS ON```
 
#### exemple
```
version #: 0.0.10004
09 MCAS OFF
...
09 MCAS ON
08 13 142 A1
...
08 11 161 D
06 11 170 MARGE
06 12 179 3X
09 MCAS OFF
06 19 183
07 19 185
...
```

## Makefile

  Il est obligatoire d'inclure un fichier `Makefile` dans votre projet pour
  faciliter la compilation et les autres actions requises. Celui-ci doit
  minimalement offrir les services suivants :
  
- Le Makefile du `tp1` sera utilisé et modifié avec quelques changements :
  + La commande `make tp1` est la nouvelle commande pour construire l'exécutable `tp1`;
  + La commande `make` employée seule devra exécuter la cible `default` qui est dépendante de tp2;
  + La cible `tp2` doit exister pour construire l'exécutable `tp2`;

- Lorsqu'on entre `make clean`, le projet revient dans son état d'origine, c'est-à-dire
  son état lors de la récupération initiale;

- Lorsqu'on entre `make lib`, le téléchargement du fichier 
  https://github.com/guyfrancoeur/INF3135_H2020/raw/master/tp/tp2.zip
  se fait de façon automatique dans un répertoire (./data). Par la suite, la décompression
  est nécessaire;

- Lorsqu'on entre `make test-tp1a` le programme `tp1` s'exécutera.
- Lorsqu'on entre `make test-tp1b` le programme `tp1` avec `liste.sh` s'exécutera afin de lister les fonctions valides.

- Lorsqu'on entre `make test-tp2` le programme `tp2` s'exécutera.

- Les programmes seront compilés et évalués avec les options suivant `-Wall -pedantic -std=c11`;

### Complément

+ `-std=c11` indique au compilateur de traiter le code selon le standard C11 (2011) (et donc 
de rejeter certaines extensions comme celles de GNU par exemple)
+ `-pedantic` permet de signaler les avertissements, ou warnings, selon la norme ISO
+ `-Wall` permet de signaler un grand nombre d'autres warnings décrit dans le man gcc.
En effet, la grande permissivité de C réduit l'aide du compilateur (lorsque qu'il n'y a pas d'option)
pour traquer certaines erreurs et les mauvaises pratiques de programmation.

## .gitignore

+ Votre projet (dépôt distant) doit contenir uniquement les fichiers strictement nécessaires; 
+ Votre projet ne doit pas contenir de fichiers `objet` ou `binaire` par exemple.

## liste.sh

 Votre programme exécutable tp1 liste beaucoup de choses lorsqu'il est lancé.  Le fichier nommé `liste.sh`
 recevra par stdin le stdout de tp1. Par la suite, vous devez lister uniquement les noms des fonctions qui sont
 valides et fonctionnelles. Il y aura certainement plusieurs fonctions qui vont être listées.
 
 #### exemple de sortie:
 ```
 angle_incidence_marge_v1
 ```

## README.md

  Votre projet doit contenir un fichier nommé `README.md` qui décrit le contenu et qui **respecte le
  format Markdown**. Il doit minimalement contenir les informations ci-bas :

~~~~
   # Travail pratique X

   ## Description

   <description du projet en quelques phrases>
   <mentionner le contexte (cours, sigle, université, etc.)>

   ## Auteur

   <prénom et nom> (<code permanent>)

   ## Fonctionnement

   <expliquez brièvement comment faire fonctionner votre projet, en inscrivant
   au moins deux exemples d'utilisation (commande lancée et résultat affiché)>

   ## Contenu du projet

   <décrivez brièvement chacun des fichiers contenus dans le projet (une phrase
   par fichier)>

   ## Processus de réflexion et démarche 
   
   <inclure par référence le fichier reflexion.md>

   ## Références

   <citez vos sources ici>

   ## Statut et auto-évaluation

   <indiquez si le projet est complété ou s'il y a des bogues>
   <mon travail vaut quelques points en fonction du barème>
   
~~~~

# Remise

  La totalité de votre travail doit être remise au plus tard le **21 mars 2020** à **21h59** ET (heure du Québec).
  Après cette date, une pénalité de **10 points par jour** de retard sera appliquée.

  La remise se fait **obligatoirement** par l'intermédiaire de la plateforme `Github https://github.com/` 
  
  **Aucune remise par courriel ne sera acceptée** (le travail sera considéré comme non remis).

  Le nom de votre dépôt doit être `inf3135-h2020-tp1` (en minuscules). Vous devez ajouter l'utilisateur
  `guyfrancoeur` comme collaborateur. Ceci permettra de récupérer et possiblement de déposer quelques commentaires
  (fichiers) dans votre projet. ~~Vous devez faire une demande de modification du fichier nommé `tp2.depot`
  via GitHub afin d'ajouter votre `url` de dépôt distant GitHub. Ceci fait votre remise sera complète.~~

  Votre projet devrait minimalement contenir, à la racine du dépôt, les fichiers de type `Unix/Linux` et `ascii` suivants :

- Un fichier `tp2.c` contenant le code source de votre projet, ainsi que votre fonction `main`;
- Un fichier `README.md` selon le format proposé;
- Un fichier `reflexion.md` qui démontre le processus de réflexion durant le travail;
- Un fichier nommé `Makefile` complet et optimal;
- Un fichier nommé `cp.txt` avec votre code permanent en majuscule;
- Un fichier de script bash nommé `liste.sh` réalisé lors du tp1;
- Un fichier nommé `tp1.c` réalisé lors du tp1;
- Un fichier ``.gitignore``.

  L'usage de la commande `rm` dans votre travail est permise.  Avec de grands pouvoirs viennent de grandes responsabilités. 

  Les travaux seront corrigés sur le serveur Java. Vous devez donc vous assurer
  que votre programme fonctionne **sans modification** sur celui-ci.

# Barème de correction

| Critère | Sous-critère | Points |
| ------- |:------------ | ------:|
| Récupération      | récupération sans problème et dépôt privée     | 1.0 |
| Makefile          |                                                | 3.0 |
| Compilation       | sans avertissement ni erreur                   | 2.0 |
| Fonctionnabilité  | tests seront lancés (comparaison binaire)      | 8.0 |
| Branche (git)     | nommée tp2 (branche de developpement)          | 1.0 |
| Issues (git)      | intervention                                   | 1.0 |
| Optimal (git)     |                                                | 1.0 |
| Professionnel     | :wink: (simple et sans mystère)                | 2.0 |
| Markdown          | README.md (reflexion)                          | 1.0 |
| Bonus             | GitHub Action (YAML)                           | 1.0 |
| **Total**         |                                                | 21/20 |

---
Guy Francoeur :copyright: édition H2020
