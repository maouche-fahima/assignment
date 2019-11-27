# assignment
mon travail
install.packages("tidyverse")
library(tidyverse)
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy))
  ggplot(data = mpg)
 mpg
 
#3.2.4 Exercices:
 ggplot(data = mpg)
 1- ggplot(data = mpg) crée un graphique vide
 2- Combien de lignes sont dedans mpg? Combien de colonnes?
 mpg
le nombre de ligne est de 234 et le nombre de colonnes est de 11.
3- Que drv décrit la variable? Lisez l'aide pour ?mpg savoir
?mpg
 f = front-wheel drive, r = rear wheel drive, 4 = 4wd
4- Faire un nuage de points hwyvs cyl
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = hwy, y = cyl))
 
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = cyl, y = hwy))
  
5- Que se passe-t-il si vous faites un diagramme de dispersion de classvs drv? Pourquoi l'intrigue n'est pas utile?

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = class, y = drv))
  
  l'intrigue n'est pas utile car chaque classe a un ou deux drv est les variables ne sont pas continues. il est peut etre plus utile de faire un histogramme. 
 
#3.3 Mappages esthétiques:
 
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class))
  
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, size = class))
  
# Left
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, alpha = class))

# Right
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, shape = class))
  
choix de couleur 
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
  
#3.3.1 Exercices:

1- Qu'est-ce qui ne va pas avec ce code? Pourquoi les points ne sont pas bleus?
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))
  
   le probleme avec le code c'est que la caractéristique esthetique va en dehors de aes() en dans le code on a pas fermer la fonction aes().
   
2- Quelles variables mpgsont catégoriques? Quelles variables sont continues? (Indice: tapez ?mpgpour lire la documentation de l'ensemble de données). Comment pouvez-vous voir cette information lorsque vous courez mpg?
mpg

Les variables catégorielles (ou qualitatives) mesurent juste des “états”, des catégories. Il n’y a pas d’échelle de valeurs.

Une variable continue peut prendre, en théorie, une infinité des valeurs, formant un ensemble continu

les variable continues: displ, hwy
les variables catégorielle: trans, cyl, year, class, fl, drv.

3- Assignez une variable continue à color, sizeet shape. Comment ces esthétiques se comportent-elles différemment pour les variables catégorielles par rapport aux variables continues?

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class))
  
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, size = class))

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, shape = class))
  
4- Que se passe-t-il si vous associez la même variable à plusieurs esthétiques?

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy,size = class, color = class, shape = class))

5- Que fait l' stroke esthétique? Avec quelles formes travaille-t-il?

?geom_point

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class, stroke = 3))
  
il travaille sur la taille des point.

6- Qu'advient-il si vous associez une esthétique à autre chose qu'un nom de variable, comme aes(colour = displ < 5)? Notez que vous devrez également spécifier x et y.

ggplot(data = mpg) +
geom_point(mapping = aes(x = displ, y = hwy, color = displ < 5))

on aura tous les point de displ < 5 en bleu est tous les point de autres points en rouge.

#3.5 facettes:
#pour une variable on utilise:
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)
  
#pour deux variable on utilise:
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_grid(drv ~ cyl)

#3.5.1 Exercices:
1- Que se passe-t-il si vous modifiez une variable continue?

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ displ, nrow = 2)
  
  pour chaque valeur de displ "variable continue" on aura un graphe avec toutes les valeurs de hwy possible
  
2- À quoi correspondent les cellules vides de la parcelle facet_grid(drv ~ cyl)? Comment se rapportent-ils à cette intrigue?

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = drv, y = cyl))
  facet_grid(drv ~ cyl)
   les cellules vides correspondent a des valeurs de displ qui n'ont pas de valeurs Y sur la parcelle(5-4); (5-r);(r-4)

3- Quelles parcelles le code suivant fait-il? Que fait .-il?

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)
  
  ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)
  
  on utilise ce code dans le cas ou on veut pas utiliser de facette dans la dimension des lignes ou des colonnes, utilisez .plutôt un nom de variable.
  il permets donc d'observer les nuage de points suivant une variable en colone dans le cas "facet_grid(. ~ cyl)" ou en ligne " facet_grid(drv ~ .)" mais pas les deux au meme temps.
  
  4- Prenez la première parcelle à facettes dans cette section:
  
  ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)
  
#avantages: 
permets d'observer l'evolution displ par rapport a hwy pour chaque class de voiture separrement; contrairement a la couleur qui represente toutes les variation sur le meme graphe.
#incovénients:  
elle pemret pas la compraison de l'evolution pour les différents type de voiture. 

5- Lire ?facet_wrap. Que fait nrow-il? Que fait ncol-il? Quelles autres options contrôlent la disposition des panneaux individuels? Pourquoi ne pas facet_grid()avoir nrow et des ncol arguments?

#nrow: permet de détérminer le nombre de ligne de parcelle

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, ncol = 2)
#ncol: permet de détérminer le nombre de colonnes de parcelle

6- Lors de l'utilisation, facet_grid()vous devez généralement mettre la variable avec plus de niveaux uniques dans les colonnes. Pourquoi?

  ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_grid(cyl ~ drv)

afin d'avoir plus de détail sinon on peut rien voir sur le nuage de point.

#3.6 Objets géométriques:

#3.6.1 Exercices:

1- Quel géom utiliseriez-vous pour dessiner un graphique en courbes? Une boîte à moustaches? Un histogramme? Un graphique en aires?

Un geom est l'objet géométrique qu'un plot utilise pour représenter des données.

2- Exécutez ce code dans votre tête et prédisez à quoi ressemblera la sortie. Ensuite, exécutez le code dans R et vérifiez vos prédictions.
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE)
  
3- Que fait show.legend = FALSE-il? Que se passe-t-il si vous l'enlevez?
Pourquoi pensez-vous que je l'ai utilisé plus tôt dans le chapitre?

ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE)
show.legend = FALSE permet de separer par groupe de couleur les différents ligne de tendance. si on l'enleve on aura 3 ligne de tendance avec la meme couleur.
  
5- Ces deux graphiques seront-ils différents? Pourquoi pourquoi pas?

ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()
  
  ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
  
  aucune différence entre les deux graphe car les deux codes permetes d'éxécuter la méme chose 
  
6- Recréez le code R nécessaire pour générer les graphiques suivants.
  
  
  ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
  
  ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE)
  
   ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth(se = FALSE)
  
  ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  geom_smooth(mapping = aes(x = displ, y = hwy, group = drv))
  
#3.7 Transformations statistiques:
#3.7.1 Exercices:

1- À quoi est associé le geom par défaut stat_summary()? Comment pourriez-vous réécrire le tracé précédent pour utiliser cette fonction geom au lieu de la fonction stat?

ggplot(data = diamonds) + 
  stat_summary(mapping = aes(x = cut, y = depth),
    fun.ymin = min,
    fun.ymax = max,
    fun.y = median)
 demo <- tribble(
  ~cut,         ~freq,
  "Fair",       1610,
  "Good",       4906,
  "Very Good",  12082,
  "Premium",    13791,
  "Ideal",      21551
)
    ggplot(data = demo) +
  geom_bar(mapping = aes(x = cut, y = freq), stat = "identity")
?stat_bin

2- Que fait geom_col()-il? En quoi est-ce différent geom_bar()?

?geom_col

geom_bar () utilise stat_count () par défaut: il compte le nombre d'observations à chaque position x. geom_col () utilise stat_identity (): il laisse les données telles quelles.

4- Quelles variables stat_smooth()calcule? Quels paramètres contrôlent son comportement? 
?stat_smooth
Utilisez stat_smooth () si vous souhaitez afficher les résultats avec un geom non standard.

5- Dans notre diagramme à barres de proportion, nous devons définir group = 1. Pourquoi? En d'autres termes, quel est le problème avec ces deux graphiques?

#3.8 Ajustements de position:

ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, colour = cut))
  
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = cut))
  
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity))
  
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + 
  geom_bar(alpha = 1/5, position = "identity")
  
ggplot(data = diamonds, mapping = aes(x = cut, colour = clarity)) + 
  geom_bar(fill = NA, position = "identity")
  
 ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity), position = "dodge")
  
#3.8.1 Exercices:

1- Quel est le problème avec cette intrigue? Comment pourriez-vous l'améliorer?

ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point()
  
  ggplot(data = mpg) + 
  geom_point(mapping = aes(x = cty, y = hwy), position = "jitter")
  
  Vous pouvez éviter ce maillage en réglant le réglage de la position sur «jitter». position = "jitter"ajoute une petite quantité de bruit aléatoire à chaque point. Cela répartit les points car il n'y a pas deux points susceptibles de recevoir la même quantité de bruit aléatoire.
  
2- Quels paramètres pour geom_jitter()contrôler la quantité de jitter?

Ajouter un caractère aléatoire semble être un moyen étrange d'améliorer votre graphique, mais s'il rend votre graphique moins précis à petite échelle, il le rend plus révélateur à grande échelle. Parce que c'est une opération utile, ggplot2 est livré avec un raccourci pour geom_point(position = "jitter"): geom_jitter().

3- Comparez et contrastez geom_jitter()avec geom_count().

ggplot(data = mpg) + 
  geom_count(mapping = aes(x = cty, y = hwy))
  
ggplot(data = mpg) + 
  geom_jitter(mapping = aes(x = cty, y = hwy))
  
ggplot(data = mpg) + 
  geom_count(mapping = aes(x = cty, y = hwy), position = "jitter")
  
4- Quel est le réglage de la position par défaut geom_boxplot()? Créez une visualisation du mpgjeu de données qui le démontre.

ggplot(data = mpg) + 
  geom_boxplot(mapping = aes(x = cty, y = hwy,group = class))
  

#3.9 Systèmes de coordonnées :
#3.9.1 Exercices:

1-Transformez un graphique à barres empilées en un graphique à secteurs à l'aide de coord_polar().

ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop.., group = 1)) +
  coord_polar()

2-Que fait labs()-il? Lire la documentation.
?labs
3- Quelle est la différence entre coord_quickmap()et coord_map()?


ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop.., group = 1)) +
  coord_quickmap()
  
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) +
  geom_point() + 
  coord_map()
  
4- Qu'est-ce que l'intrigue ci-dessous vous dit à propos de la relation entre ville et autoroute mpg? Pourquoi est coord_fixed()important? Que fait geom_abline()-il?

ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) +
  geom_point() + 
  geom_abline() +
  coord_fixed()
il reduit la taille de graphe 

#4 flux de travail: bases
4.4 Pratique:
1- Pourquoi ce code ne fonctionne pas?

 my_variable <- 10
my_varıable

library(tidyverse)
library(tidyverse)

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy))
  
fliter(mpg, cyl = 8)
filter(diamond, carat > 3)

#5 Transformation de données:
library(tidyverse)
install.packages("nycflights13")
library(nycflights13)
nycflights13::flights
jan1 <- filter(flights, month == 1, day == 1)

#5.2.4 Exercices:
1- Trouver tous les vols qui:
filter(flights, month == 1, day == 1)

jan1 <- filter(flights, month == 1, day == 1)
(dec25 <- filter(flights, month == 12, day == 25))


***Eu un retard d'arrivée de deux heures ou plus:
filter(flights, year == 2013, arr_delay >= 2)
***Volé à Houston ( IAHou HOU):
filter(flights, flights == HOUSTON)