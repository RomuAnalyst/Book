# Objectif de la formation {#intro}

<span style='color: red;'>Version provisoire et temporaire de la formation Insee 'Travail collaboratif avec R'</span>

Ce cours consiste en une introduction/initiation à l'usage du logiciel **R**.
Dans ce document sont présentés les concepts principaux du logiciel **R** (éléments de langage, données manipulées, manipulation de données, ...).  

Ce document vise à présenter avec `Rstudio` la manipulation sde données, le traitement et l'analyse, en passant par l'étape graphique.



# Présentation de R et de son environnement

## Qu'est-ce que <i class="fab fa-r-project"></i> ?
Le logiciel **R** est un langage dédié à la statistique. 
Il a été développé à partir des années 90 à l'University of Auckland, Nouvelle-Zélande. 
Son implémentation principale est en open source (gratuit et modifiable) **R** : [cran.r-project.org](http://cran.r-project.org). 

**R** est un [langage interprété](http://www.france-ioi.org/algo/course.php?idChapter=561&idCourse=2368) (comme `Python`) et non compilé, c'est-à-dire que les commandes tapées au clavier sont directement exécutées sans qu'il soit besoin de construire un programme complet. On dit également qu'il est "exécuté à la volée".
Par exemple on peut à partir d'une ligne de commande écrire :


```r
print('Hello world!')
```

```
## [1] "Hello world!"
```

Pour simplifier son utilisation, il est possible d'écrire des scripts c'est à dire une suite de commandes qui se trouvent dans un fichier dont l’extension est `.R` mais on pourrait tout aussi bien les écrire dans un `.txt`.

Pour simplifier l'utilisation de **R**, il est nécessaire d'avoir une interface graphique (appelée aussi *GUI* pour Graphic User Interfaces). Celle offerte par **R** est très simpliste et beaucoup préfèrent utiliser **RStudio** ([www.rstudio.com](www.rstudio.com)) à juste titre. Cet outil permet de réellement fluidifier le travail avec ce langage.

## Prise en main de **R-studio**

La fenêtre de **RStudio** se divise généralement en quatre sous-fenêtres: en partant de haut à gauche et en les parcourant dans le sens horaire on trouve :

1. un éditeur de texte pour les scripts
2. l'espace de travail ou d'historique de commandes
3. le navigateur de fichiers, graphiques, packages, documentations
4. la console **R**, c'est à dire la ligne de commande ainsi que les résultats des exécutions du code.

Typiquement on tape le code dans l'éditeur et on l’exécute ensuite dans la console. Pour cela on place le curseur dans la ligne qu'on veut exécuter et on envoie la commande à la console à l'aide de la combinaison `cmd Retour` dans IOS et `ctrl Retour` sous Windows ou tout simplement à l'aide de la commande `Run`.
 
## L'aide en ligne
**R** dispose d'une documentation très complète et l'aide en ligne peut être très utile pour l'utilisation de fonctions, librairies et jeux de données. On peut accéder directement à l'aide en tapant `?` suivi par la _fonction_ (ou autre instruction, jeu de données,...) sur laquelle on souhaite se renseigner :

```r
?mean
```
affichera par exemple la page d'aide pour la fonction `mean()`. La commande 

```r
help(mean)
```
aura le même effet.

On peut aussi trouver énormément d'informations sur le web : par exemple en cherchant à l'aide d'un moteur de recherche un problème lié à une tâche **R** on trouve presque toujours une réponse (souvent dans des forum ouverts sur le site [Cross Validated](https://stats.stackexchange.com/)).   

Le but de cette introduction tutorielle est de vous apprendre l’utilisation élémentaire de **R**. Bien que les objets et commandes de bases y soient introduits, cette introduction n'est pas une référence complète au langage **R** (loin de là!), vous serez donc amenés à utiliser l'aide et à chercher des informations sur le web. A chaque étape, vous êtes encouragés à taper les commandes et à en comprendre le résultat : la meilleur façon d'apprendre un langage est d'écrire et débugger beaucoup de lignes de code! 


## Packages
Les deux grands avantages de **R** est d'être gratuit et open source. De ce fait il jouit d'une
 communauté d'utilisateurs très active dans le monde scientifique (statistiques, science des données, bioinformatique, sciences sociales,...). Il est de plus très utilisé par la communauté scientifique et de plus en plus dans les entreprises. 
 
Toute nouvelle méthode statistique a très rapidement une implémentation dans ce langage, ce qui n'est pas toujours le cas pour d'autres langages. Cela enrichi considérablement le logiciel et se fait à l'aide de ce qu'on appelle des paquets (ou *packages* ou *library*) Ces derniers sont développés par les  utilisateurs et les développeurs. On peut les installer pour augmenter les capacités et possibilités du logiciel dans des domaines très variés de la statistique mais pas seulement en statistique. Il en existe un très grand nombre sur le site du **CRAN** : [cran.r-project.org](http://cran.r-project.org).


Pour installer un package:


```r
install.packages("dplyr") 
# On telecharge et installe le package dplyr utilisé dans la manipulation de données
```

Une fois un package installé, il faudra le charger en mémoire à chaque fois qu'une nouvelle session est ouverte:


```r
library(dplyr) # sans guillemets!
require(dplyr) # fonction équivalente
```
 
Important : il est à noter que `#` sert à commenter les instructions.






