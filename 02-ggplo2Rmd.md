# Utiliser *GGplot2* pour faire et superposer des graphiques{#ggplo2}



<style type="text/css">
.red {
  color: red;
}
</style>





Le but de la visualisation de données étant de représenter graphiquement des données brutes (ou quasi-brutes), il est souvent nécessaire de prendre en compte plusieurs variables. Nous devons donc aller plus loin que les graphiques de base (nuage de points, droite de regression, boite à moustache, diagramme en barres ou circulaires, ...), pour les combiner par exemple.

Avec le langage de base (package `graphics` notamment), il est possible de faire des graphiques évolués, mais avec beaucoup de paramétrages *à la main*. Pour cela on va commencer par s'intéresser au jeu de données `mtcars`.


```r
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```

```r
# ?mtcars ou help(mtcars)
str(mtcars)
```

```
## 'data.frame':	32 obs. of  11 variables:
##  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
##  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
##  $ disp: num  160 160 108 258 360 ...
##  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
##  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
##  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
##  $ qsec: num  16.5 17 18.6 19.4 17 ...
##  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
##  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
##  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
##  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
```

```r
plot(mtcars$hp,mtcars$mpg)
```

<img src="02-ggplo2Rmd_files/figure-html/mtcars-1.png" width="672" />

Essayons d'améliorer ce graphique...
Ci dessous, un exemple de graphique avancé, représentant 4 variables (trois quantitatives et une qualitative), ainsi qu'une explication succincte des différentes fonctions utilisées, et quelques paramètres de celles-ci.  



```r
par(family = "serif", mar = c(5, 4, 2, 0)+.1)
couleurs_am = brewer.pal(3, "Dark2")
plot(mpg ~ hp, 
     data = mtcars,
     pch = 19,
     cex = wt/3,
     col = couleurs_am[mtcars$am+1],
     main = "Consommation en fonction de la Puissance",
     sub = "Source : 1974 Motor Trend US magazine", font.sub = 3, cex.sub = .8,
     xlab = "Puissance (en ch)",
     ylab = "Consommation en Miles/Galon",
     bty = "n", axes = FALSE)
axis(1, lwd = 0, lwd.ticks = .5)
at.y = axis(2, lwd = 0, lwd.ticks = .5, labels = FALSE)
text(y = at.y, x = 35, labels = at.y, srt = 0, pos = 2, xpd = TRUE)
l1 = legend("topright", legend = c("Automatique", "Manuelle"), 
       col = couleurs_am, bty = "n", cex = .8, pch = 19,
       text.width = 50, text.col = couleurs_am, 
       title = "Boite de vitesse", title.col = "black")
legend(l1$rect$left, l1$rect$top-l1$rect$h-1, 
       legend = range(mtcars$wt), title = "Poids  (1000 lbs)",
       pch = 19, pt.cex = range(mtcars$wt)/3, bty = "n", cex = .8, col = gray(.5),
       text.width = 50, adj = -.25)
outliers_hp = subset(mtcars, subset = hp > 250)
text(outliers_hp$hp, outliers_hp$mpg, row.names(outliers_hp), pos = c(3, 2), cex = .8, font = 4)
outliers_mpg = subset(mtcars, subset = mpg > 30)
text(outliers_mpg$hp, outliers_mpg$mpg, row.names(outliers_mpg), pos = 4, cex = .8, font = 4)
```
  
<center>![ ](pics/images/Consommation en fonction de la puissance.png)</center>  



- La fonction `par()` permet de modifier les paramètres graphiques, tel que :
    - `mar` pour les marges (un vecteur numérique de taille 4 qui permet de définir les tailles des marges dans l'ordre suivant : bas, gauche, haut, droite. Par défaut il vaut c(5.1, 4.1, 4.1, 2.1) )
    - `family` pour la famille de police d'écriture
    - certains paramètres ci-après sont définissables globalement dans la fonction `par()`, ou localement dans les fonctions suivantes
- Les paramètres de la fonction `plot()`
    - `pch` : symbole utilisé pour chaque point (ici `19` indique un rond plein)
    - `cex` : taille du point (ici en fonction de la variable `wt`)
    - `col` : couleur des points (ici en fonction de la variable  `am`)
    - `main`, `sub`, `xlab`, `ylab` : resp. titre, sous-titre, intitulé en abscisse et intitulé en ordonnée
    - `*.sub` : indication spécifique pour le sous-titre 
    - `bty` : type de la boite (ici `n` veut dire rien autour du graphique)
    - `axes` : présence ou non des axes (non ici)
- La fonction `axis()` qui permet d'ajouter un axe (`1` : en abscisse, et `2` : en ordonnée)
    - si rien d'indiqué pour `at`, utilisation des `ticks` par défaut
    - `lwd` : largeur de la ligne (ici non-présente)
    - `lwd.ticks` : largeur des ticks (assez fine ici)
    - renvoie les valeurs des ticks
- La fonction `text()` permet d'écrire du texte sur le graphique
    - le `x = 35` est choisi par expérience
    - `srt` : angle du texte
    - `pos` : ajustement du texte par rapport aux coordonnées indiquées
    - `xpd` : permet d'écrire en dehors du graphique (dans les marges donc)
- La fonction `legend()` permet d'ajouter une légende
    - position : soit $(x,y)$, soit chaine spécifique
    - `legend` : texte des items
    - `col`, `bty`, `cex`, `pch` : identique à précédemment
    - `text.width` et `text.col` : largeur du texte des items et couleur(s)
    - `title` et `title.col` : titre de la légende (et couleur du titre)
    - renvoie une liste avec deux objets (`rect` qui contient des infos sur le rectangle occupé par la légende dans le graphique et `text` qui contient les coordonnées du texte des items)
    - `pt.cex` : taille des symboles
    - `adj`: ajustement du texte
    






L'utilisateur souhaite réaliser des graphiques (nuages de points, histogrammes, densité...) et les personnaliser (légendes, titres, échelles...).

::: {.recommandation data-latex=""}
Il est recommandé d'utiliser le package ggplot2 qui permet de réaliser et de personnaliser un grand nombre de représentations graphiques;
Il est conseillé aux utilisateurs débutants d'utiliser l'add-in esquisse pour se familiariser avec ggplot2.

Vous pouvez également accéder à `esquisse` en exécutant le code suivant:


```r
library(esquisse)
esquisser()
```


L'objectif du *package* `ggplot2` est de fournir une approche unique pour produire quasiment toute représentation graphique de données. Ce _package_ propose un grand nombre de fonctions permettant de personnaliser finement les représentations graphiques. Cette fiche n'est donc qu'une introduction succincte à `ggplot2`. Pour des formations plus détaillées, se référer à {#ggplot2Ressources}.



### Introduction

**La fonction essentielle de `ggplot2` est `ggplot()`.** Il faut définir quatre éléments pour construire un graphique avec `ggplot()`: 

- la **table de données** ;
- le ***mapping*** : on définit dans l'_aesthetic_ (ou `aes`) le lien entre les variables des données et ce que l'on veut représenter sur le graphique (quelle variable sur l'axe `x`, sur l'axe `y`, quelle variable pour définir une graduation de couleurs...) ;
- la **forme géométrique ou _geometry_ ** : on définit la représentation graphique qu'on souhaite utiliser. Les géométries ont toutes un nom qui commence par `geom_`; par exemple, il faut utiliser la géométrie `geom_point()` pour réaliser un nuage de points;
- les **paramètres** : on définit les autres paramètres qui dépendent de constantes (par exemple : je veux que toutes mes lignes soient rouges ou de taille 2 pixels).

**La construction d'un graphique repose sur le principe de couches successives.** Les différentes couches graphiques se superposent et s'enchaînent grâce à l'**opérateur `+`**, comme un pipe. Il est possible d'aller à la ligne dans une instruction `ggplot()`, il suffit que l'opérateur `+` figure à la fin de la ligne.

Voici un exemple de code qui crée un nuage de points (géométrie `geom_point()`) à partir des données `mes_donnees`, avec les variables `variable1` en abscisse et `variable2` en ordonnée:

<details>
  <summary>**Se mettre d'accord sur la trame qui sera le squelette du rapport**</summary>

```r
library(ggplot2)
ggplot(data = iris) + 
  geom_point(mapping = aes(x = iris$Sepal.Length, y = iris$Sepal.Width))
```

```
## Warning: Use of `iris$Sepal.Length` is discouraged. Use `Sepal.Length` instead.
```

```
## Warning: Use of `iris$Sepal.Width` is discouraged. Use `Sepal.Width` instead.
```

<img src="02-ggplo2Rmd_files/figure-html/unnamed-chunk-3-1.png" width="672" />
</details> 






```r
library(ggplot2)
ggplot(data = iris) + 
  geom_point(mapping = aes(x = iris$Sepal.Length, y = iris$Sepal.Width))
```

### Le *mapping* et l'utilisation d'`aes()` {#mapping}

Le *mapping* désigne dans `ggplot2` la relation entre un **attribut graphique** de la `geometry` (abscisse, ordonnée, couleur...) et **une variable** présente dans la table de données. On déclare le *mapping* grâce à la fonction `aes()` (pour _aesthetic_), qui sert donc à identifier les variables que l'on souhaite représenter sur le graphique. 

**Les arguments fondamentaux de `aes()` sont les variables représentées sur l'axe des abscisses et l'axe des ordonnées (`x` et `y`).** Par exemple, on écrit `aes(x = niveau_vie_median, y = taux_chomage)` si l'on souhaite représenter pour chaque iris le taux de chômage (sur l'axe `y`) en fonction du niveau de vie médian (sur l'axe `x`).


Par ailleurs, la fonction `aes()` admet d'autres arguments qui permettent de modifier l'apparence des attributs graphiques selon une troisième variable du jeu de données. Voici les arguments supplémentaires les plus courants:

Attribut   |Description
-----------------|------------------------------------
**`color`**| Couleur des lignes ou des points
**`shape`**| Forme des points
**`size`**| Taille des points
**`alpha`**| Transparence des points
**`fill`**| Couleur des surfaces
**`linetype`**| Type de ligne (continue, pointillée, ...)


Dans l'exemple qui suit, on représente pour chaque iris le taux de chômage (sur l'axe `y`) en fonction du niveau de vie médian (sur l'axe `x`), en colorant les points en fonction de la part des cadres et professions intellectuelles supérieures parmi les actifs de l'iris (`color = part_cadres`).



Il est également possible d'utiliser ces mêmes arguments pour modifier un attribut graphique sans le lier à une variable. En ce cas, on définit l'attribut **à l'extérieur de l'_aesthetic_** (donc à l'extérieur de `aes()`). Voici l'exemple précédent, modifié pour que tous les points soient (rouge), et non en fonction d'une variable. L'argument `color` est donc à l'extérieur de `aes()`.



::: {.remarque data-latex=""}
La notion de *mapping* et la définition des attributs graphiques à l'intérieur et à l'extérieur d'`aes()` sont une des principales difficultés de `ggplot2`. Il est normal de tâtonner lorsqu'on commence à les utiliser. Pour s'y retrouver, il suffit de suivre la règle suivante. **Si on établit un lien entre les valeurs d’une variable et un attribut graphique, il s'agit d'un _mapping_ qui doit être défini à _l'intérieur_ de la fonction `aes()`. Dans le cas contraire, il s'agit d'un simple paramètre du graphique, qui doit être défini à _l'extérieur_ de la fonction `aes()`.**
:::

### Les formes géométriques

La forme géométrique ou _geometry_ désigne le type de représentation graphique utilisée (nuage de points, histogrammes...). On spécifie le type de représentation que l'on souhait en utilisant une fonction dont le nom commence par **`geom_`**. Le tableau ci-dessous présente quelques représentations graphiques classiques. 

_geometry_         | Description              | Arguments 
-------------------|--------------------------|------------------------------------
`geom_point()`     |	Nuage de points 	      | `x`, `y`, `shape`, `fill`, `size`
`geom_line()`	     | Ligne                    | `x`, `y`, `linetype`
`geom_bar()`       |	Diagramme en barres 	  | `x`, `fill`, `linetype`, `weight`
`geom_histogram()` |	Histogramme 	          | `x`, `fill`, `linetype`, `weight`
`geom_boxplot()`	 | Boîte à moustaches 	    | `x`, `y`, `fill`, `weight`
`geom_density()`	 | Courbe de densité        |	`x`, `y`, `fill`, `color`, `linetype`

Voici deux exemples d'utilisation.





::: {.remarque data-latex=""}
Il existe un grand nombre de géométries dans `ggplot2`. Vous pouvez en afficher la liste en exécutant la commande `help.search("^geom_", package = "ggplot2")`.

Par ailleurs, de très nombreux *packages* proposent encore d'autres géométries pour réaliser des représentations graphiques particulières (cartes avec `ggmap`, arbres généalogiques avec `ggtree` et `ggenealogy`, résultats d'élections avec `ggparliament`...).
:::
