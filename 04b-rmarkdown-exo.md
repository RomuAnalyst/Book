# `R Markdown`: un exercice pour créer son premier document {#rmdexo}



## Quelques éléments d'explication

### Objectif

L'objectif est d'exploiter et analyser les données sur les naissances 2017.
L'analyse sera centrée sur les 3 axes définis dans
l'expression des besoins [ici](#besoins).
Le travail sera réalisé en mode collaboratif par des équipes de personnes 
(les mêmes que pour la [partie Git](#git)).

* Un premier temps sera consacré à la production d'une première version de document
* Un second temps sera consacré aux modifications  (amélioration, évolution, modifications).


### Le produit attendu

* Un rapport au format `html` centralisant les résutats attendus. Ce rapport sera généré par un fichier `.Rmd`
* Le rapport final ainsi que les fichiers constitutifs du projet seront contenus dans un projet `monprojet.Rproj`. 
* Ce projet sera d'une part stocké sur `Gitlab`, d'autre part accédé via `R Studio` par chaque contributeur. 


### Expression des besoins {#besoins}

L'étude sera réalisée sur une région au choix.

Elle devra comporter les éléments suivants : 

* Un rapide descriptif de la source ;
* Revenu médian des communes dans la région choisie et comparaison avec les autres régions de France hexagonale.
Cette comparaison doit comporter un tableau et un graphique;
* Une analyse d'au moins une autre variable économique ou démographique lorsque cette information est disponible;
* Si vous avez le temps, une carte en utilisant un fonds de carte communal de 2016 disponible sur [le site de l'IGN](https://geoservices.ign.fr/documentation/diffusion/telechargement-donnees-libres.html#les-bases-de-donn%C3%A9es-au-format-vectoriel) ou, en interne à l'Insee, [sur creacartes](https://creacartes.insee.fr/accueil).


Les 3 derniers parties devront intégrer des illustrations de votre choix ou celles proposées. 
Le texte devra contenir au moins un résulat d'une instruction `R`.


### Données mobilisées

Pour cet exercice, on utilise les données de revenu au niveau communal issues
de Filosofi 2016. Grâce à Pierre Lamarche, il existe deux packages `R` qui 
facilitent l'accès à ces données disponibles sur insee.fr: `doremifasol` et
`doremifasolData`. Ils sont disponibles sur la page Github
[InseeFrLab](https://github.com/InseeFrLab). En l'occurrence, nous allons
utiliser `doremifasolData` qui ne nécessite pas, une fois installé, de connexion
internet pour accéder aux données. Pour l'installer:


```r
devtools::install_github('inseeFrLab/doremifasoldata', ref = "main")
```


::: {.conseil data-latex=""}
Sur  `AUS`, cette commande ne fonctionnera pas. Il faut aller chercher le
package sur un dépôt nexus: 


```r
install.packages("doremifasolData", repos = "https://nexus.insee.fr/repository/r-local")
```
:::


## Organisation de l'équipe projet


###  Comment s'organiser ? {-}

Voici des propositions pour l'organisation (cliquer sur chaque item pour
dérouler):


<details>
  <summary>**Se mettre d'accord sur la trame qui sera le squelette du rapport**</summary>
1. Champs et définitions : quelle région, quelle(s) variable(s), etc.
2. Quelle information représenter ?
    * quelles statistiques ?
    * quel tableau ?
    * quelle visualisation ?
3. Comment présenter l'information ?
</details> 

<details>
<summary>**Identifier les tâches**</summary>
* Créer le projet 
* Initier le document Rmardown avec le squelette  de la trame de travail
* récupérer et vérifier les données &#8594 *coeur de l'instruction R dans un chunk ou dans un script R ?*
* quels packages choisir ?
* préparer les données &#8594 *même question *
* construire les statistiques &#8594 *même question *
* peut-on modulariser ?
* Lors de cette étape penser :
    + reproductibilité.
    + quelles instructions externaliser du fichier Rmd ?`
</details> 

<details>
  <summary>**Se mettre d'accord sur l'organisation des fichiers et les branches à créer**</summary>
    * Un exemple d'arborescence de projet
    
    ![](./pics/04_markdown/exple_arborescence.png)
    
    * Créer une branche par partie

</details> 

<details> 
<summary>**Affecter les tâches**</summary>
* Si nécessaire, prioriser les tâches
* Ouvrir des *issues* sur `Gitlab` et éventuellement utiliser les *Milestones*
* Possibilité de le faire sur Trello si l'ensemble de l'équipe est d'accord
</details> 

<details>
<summary> **Intégrer les éléments dans le document squelette Rmd** </summary>
* quelles instructions R externaliser du fichier R Markdown
* commiter via Git depuis RStudio (n'oubliez pas les conseils de prudence du chapitre [Git](#git))
* mettre à jour le dépôt via Git depuis RStudio et Gitlab
</details> 

::: {.conseil data-latex=""}
Ne pas oublier les bonnes pratiques évoquées précédemment et celles, plus génériques, évoquées dans la documentation [utilitR](https://www.book.utilitr.org/).
:::

:::: {.exo data-latex=""}
**Exercice 3**

Réaliser ce premier document qui contiendra à la fois résultats et commentaires associés.


A vous de jouer !

![](./pics/04_markdown/partonsalaventure.gif)

::::
    

<!---
Une petite correction à faire
---->



## Demande de modifications

L'un des avantages de `R Mardown` est la mise à jour dynamique de
document. Nous allons voir comment intégrer facilement : 

* d'évolution
* amélioration
* modification

### Cas d'une demande d'amélioration {-}

Il est peu coûteux de changer des paramètres de mise en forme avec `R Markdown`

:::: {.exo data-latex=""}
1. Imaginons qu'on vous demande finalement de numéroter les sections. Faire la modification
2. On vous demande de revoir le thème `ggplot` pour utiliser le thème `theme_bw` sur tous les graphiques
::::



### Cas d'une demande d'évolution {-}

:::: {.exo data-latex=""}
Reproduire le même rapport avec les données 2015 : avez-vous fait un programme reproductible ?
::::


### Cas d'une demande de modification {-}

:::: {.exo data-latex=""}
Ajouter une partie sur l'évolution entre 2015 et 2016 du revenu de chaque commune
::::



