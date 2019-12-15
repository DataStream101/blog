---
title: "Les facteurs clés de succès d’une campagne de crowdfunding"
date: 2019-09-15
tags: [project, EDA]
---

L’objectif de ce projet a été une analyse exploratoire des facteurs qui permettent d’expliquer la réussite d’une campagne de financement participatif, dans le but de mettre en évidence les conditions auxquelles les porteurs de projet doivent être attentifs afin de maximiser la réussite de leur campagne.<br>
{: style="text-align: justify;"}

Le traitement des données a été réalisé en Python. Le code complet est disponible [ici](https://github.com/DataStream101/Crowdfunding-campaigns-analysis-in-Python).<br>
{: style="text-align: justify;"}

Les tests statistiques ont été réalisés en R.<br>
{: style="text-align: justify;"}


## Le contexte
{: style="text-align: center;"}

Le crowdfunding (ou financement participatif, en français) est un modèle de financement alternatif aux méthodes traditionnelles dont le développement a été possible grâce à l’apparition d’internet qui intensifie et facilite les interactions entre les personnes.<br>
{: style="text-align: justify;"}

La particularité du crowdfunding c’est le fait qu’il s’agit d’un modèle de désintermédiation dans lequel les investisseurs se retrouvent en relation directe avec les porteurs de projets, sans devoir passer par l’intermédiation des institutions financières traditionnelles.<br>
{: style="text-align: justify;"}

Même si le phénomène du crowdfunding a connu une grande popularité depuis son début en 2001, le taux de réussite des campagnes de financement participatif reste faible.<br>
{: style="text-align: justify;"}

## Source des données et description du dataset
{: style="text-align: center;"}


La base de données utilisée dans le cadre de cette analyse est issue de la plate-forme américaine Kickstarter, conçue pour le financement de projets créatifs, dont les porteurs sont des artistes, des musiciens ou des cinéastes.<br><br>
La base de données contient des informations concernant 18.142 projets, parus sur une période de 6 mois décembre 2013 – juin 2014.<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/data.png)  

## Nettoyage des données
{: style="text-align: center;"}


*	Puisque sur Kickstarter on trouve projets internationaux, dont le montant objectif est exprimé en des différentes divises, seulement les projets dont la divise était le dollar ont été retenus
{: style="text-align: justify;"}
*	L’analyse de la distribution de la variable montant objectif a montré une structure asymétrique, avec des valeurs inexplicablement élevées par rapport à la nature des projets présentés.
Afin de ne pas introduire des biais dans les résultats, toutes les observations dont le montant demandé ne représentait pas un effort sérieux de récolte de fonds ont été supprimées.<br><br>
Seulement les observations ayant un montant objectif compris entre 100 et 30.000 $ ont été gardées.
{: style="text-align: justify;"}

## Variables analysées et hypothèses
{: style="text-align: center;"}

A partir des données à disposition, les différentes variables qui peuvent expliquer le la réussite ou non d’une campagne ont été classifiées selon trois catégories :<br>
{: style="text-align: justify;"}

&nbsp;&nbsp;1.&nbsp;&nbsp;Facteurs liés à la **STRUCTURE de la CAMPAGNE** : Parmi ces facteurs on suppose que le montant objectif ainsi que la durée de la campagne soient corrélés négativement avec le résultat final. Par contre, on suppose que la popularité de la catégorie d’activité dans laquelle le porteur a présenté son projet soit corrélée positivement avec la réussite d’un projet.<br> 
{: style="text-align: justify;"}
&nbsp;&nbsp;2.&nbsp;&nbsp;Facteurs liés à la **COMMUNICATION** : Au moment de la présentation du projet et tout au long la période de collecte, le porteur de projet communique avec les contributeurs potentiels à l’aide de différents outils, dans le but réduire l’asymétrie informative et attirer les bailleurs de fond. On suppose que toutes les variables prises en compte soient toutes corrélées positivement avec la réussite d’un projet<br>
{: style="text-align: justify;"}
&nbsp;&nbsp;3.&nbsp;&nbsp;Facteurs **« RESEAU** » : Les porteurs d’un projet ont la possibilité de joindre le compte d’un réseau social (dans ce cas Facebook) au projet.
Cette communauté en ligne joue en rôle clé dans le processus de financement participatif, puisque les internautes peuvent accroitre la visibilité des projets (à travers le partage des informations concernant les projets) et influencer le comportement des bailleurs des fonds (à travers les commentaires postés sur la page liée au projet).<br>
Ces variables sont des indicateurs du niveau d’engouement du public pour les projets. Du coup, on suppose qu’elles soient corrélées positivement avec la réussite d’un projet.
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/facteurs.png)  

## Méthode d’analyse
{: style="text-align: center;"}
Afin de mettre en évidence les conditions favorables à la réussite d’une campagne de crowdfunding, une analyse comparative de deux sous-échantillons de la base de données de départ (identifié sur la base de la valeur de la variable dichotomique *State*) a été réalisée, dans le but d’identifier des différences dans la distribution des variables entre les projets échoués, d’un côté, et ceux qui ont eu succès, d’autre côté.<br>
{: style="text-align: justify;"}

## Résultats
{: style="text-align: center;"}
En ce qui concerne le taux de réussite, on remarque que seulement la moitié (pour la précision le 54%) de la totalité des projets ont eu succès.<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/pie.png)  
{: style="text-align: center;"}

Mais le résultat le plus intéressent on le trouve alors que l’on analyse la valeur moyenne du montant effectivement récolté en pourcentage du montant demandé.<br><br>
En effet, en moyenne, les projets échoués n’arrivent à collecter que le 13% du montant objectif, alors que les projets ayant succès ont la tendance a dépasser leur objectif et collectent en moyenne le 195% de leur objectif.<br>
{: style="text-align: justify;"}

On peut expliquer ce résultat comme une conséquence du fait que les investisseurs imitent leurs pairs. 
Du coup, soit les projets parviennent à attirer ces premiers investisseurs qui lancent la tendance et incitent les autres à investir dans les mêmes projets, soit ils n’y parviennent pas et on remarque alors, qu’ils n’arrivent pas du tout à faire financer leur projet.<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/goal.png)  
{: style="text-align: center;"}

### Analyse des facteurs liés à la Structure de la Campagne
{: style="text-align: center;"}

#### Montant Objectif
A niveau global, le montant objectif est distribué entre les valeurs limites de 100 et 30 000€. Il s’agit d’une distribution asymétrique, ayant une valeur moyenne de 7.500 € et une valeur médiane de 5.000€.<br>
La plupart des projets ont un montant objectif inférieur à 10.000 €.<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/goal_amount.png)  
{: style="text-align: center;"}

Si on observe plus en détail cette distribution, on s’aperçoit que la plupart des projets demande un montant égal à 5.000, 10.000, 3000 ou 2.000€.<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/10_goal_amount.png)  
{: style="text-align: center;"}

Lorsqu’on considère la distribution du montant demandé entre les deux groupes (projets échoués et réussis), on trouve que pour les projets qui échouent, le montant demandé en moyenne est de 8790 €, 37% plus que celui demandé pour les projets ayant succès qui est en moyenne égal à 6.400 €.<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/dist_goal_amount.png) 
{: style="text-align: center;"}

Si on analyse les deux distributions en utilisant un autre indicateur de tendance centrale, la médiane, on trouve la même tendance<br>
{: style="text-align: justify;"}
 - sa valeur est de 4000 €, pour les projets ayant succès alors que pour ceux qui échouent est sensiblement plus élevé, égal à 6000 €<br>
 - également, pour la plupart des observations qui appartiennent au groupe des projets réussis, la valeur du montant demandé se situe dans un intervalle des valeurs moins étalé par rapport à celui des projets qui échouent.<br>
 {: style="text-align: justify;"}

Afin de vérifier la significativité statistique de ce résultat un test t de Welch de comparaison des moyennes a été réalisé.
{: style="text-align: justify;"}
Il permet de conclure, avec un niveau de confiance de 95%, qu’en effet le montant objectif moyen des projets qu’échoue est supérieur à celui des projets qu’on succès, ce qui confirme l’hypothèse que la valeur du montant objectif influence la réussite d’une campagne.<br>
{: style="text-align: justify;"}

#### Durée de la campagne
Les porteurs de projets ont la possibilité de choisir le délai dans lequel l’objectif doit être accompli.<br>
On peut remarquer en observant le graphique suivant que la distribution de la variable « Durée » se situe principalement entre 20 et 30 jours (65% des projets).<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/duree.png) 
{: style="text-align: center;"}

Lorsqu’on compare la distribution de la durée entre les deux groupes, on remarque que, même si on trouve la même valeur de tendance centrale dans les deux groupes, la proportion de projets ayant une durée supérieure à 30 jours est majeure dans le groupe des projets échoués.
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/duree_distr.png) 
{: style="text-align: center;"}


Comme dans le cas précédent, le résultat du test t de Welch de comparaison des moyennes qui permet de conclure, avec un niveau de confiance de 95%, que la durée moyenne des campagnes des projets qu’échoue est supérieure à celle des projets qu’on succès, ce qui confirme l’hypothèse que la durée d’une campagne influence sa réussite.<br>
{: style="text-align: justify;"}

#### Catégorie d’activité

Le graphique suivant représente les catégories disponibles dans la plateforme en fonction du nombre de projets parus dans chacune. On peut voir que les 3 catégories les plus populaires sont la Musique, les Films et Vidéos, Edition (qui regroupent environ 50% de tous les projets de la plateforme).<br>
{: style="text-align: justify;"}
 
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/pop_cat.png) 
{: style="text-align: center;"}

Lorsque l’on comparer la distribution des projets réussis et échoués par chaque catégorie, on remarque que la proportion des projets ayant succès est plus élevée dans les catégories moins populaire (Théatre, Dance et Comics) avec une seule exception, celle de la catégorie musique.
{: style="text-align: justify;"}
En particulier, les projets dans les catégories Dance, Théatre et Comics ont un taux de réussite de 74%, 72%, 61% respectivement, qui sont plus haut du taux de réussite moyen de tous les projets (52%).
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/cat_distr.png) 
{: style="text-align: center;"}


Un test Chi2 d’indépendance permet de conclure, avec un niveau de confiance de 95%, qu’en effet la catégorie dans laquelle se situe un projet influence sa réussite.
{: style="text-align: justify;"}

### Analyse des facteurs liés à la Communication
{: style="text-align: center;"}

#### Nombre de mots
Plus la description est détaillée, plus le porteur est en mesure de réduire l’asymétrie informative et d’instaurer un climat de confiance envers son projet.
{: style="text-align: justify;"}

Au niveau global, on trouve que les descriptions des projets contiennent, en moyenne, 615 mots
{: style="text-align: justify;"}

En effet, si on compare la distribution du nombre de mots contenus dans la description du projet, pour les projets échoues et pour ceux qui ont eu succès, on remarque que les derniers ont la tendance à avoir une distribution des valeurs plus étalée (42% d’entre eux ont une description plus longue de la moyenne à niveau global) par rapport à ceux qui échoues (29%).
{: style="text-align: justify;"}
 
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/long.png) 
{: style="text-align: center;"}


Le résultat du test t de Welch de comparaison des moyennes qui permet de conclure, avec un niveau de confiance de 95%, que le nombre de mots moyen dans la description des projets qu’échoue est inférieur à celui des projets qu’on succès, ce qui confirme l’hypothèse que le nombre de mots dans la description d’un projet influence la réussite de sa campagne
{: style="text-align: justify;"}

#### Nombre d'actualités postés par le porteur d'un projet sur son état d'avancement

Le fait de poster des actualités sur l’état d’avancement du projet, peut être à l’origine d’un effet boule de neige : autres investisseurs peuvent se convaincre de la validité du projet et du coup être encouragés à contribuer.
{: style="text-align: justify;"}

En effet, si on compare la distribution du nombre d'actualités postés pour les projets échoues et pour ceux qui ont eu succès, on remarque que les derniers ont la tendance à avoir un nombre d’actualités plus grand (5 actualités postées en moyenne pour les projets réussis) par rapport à ceux qui échoues (1 seule actualité postée en moyenne).
{: style="text-align: justify;"}
 
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/updates.png) 
{: style="text-align: center;"}
 

Le résultat du test t de Welch de comparaison des moyennes qui permet de conclure, avec un niveau de confiance de 95%, que le nombre d’actualités postées en moyen pour les projets qu’échoue est inférieur à celui des projets qu’on succès, ce qui confirme l’hypothèse que le nombre d’actualités postées par le porteur d’un projet influence la réussite de sa campagne.
{: style="text-align: justify;"}

#### Nombre d’images

Une image vaut mieux que mille mots.<br>
L’emploi d’images en complément de la description peut être un atout pour attirer l’attention des investisseurs.<br>
Au niveau global, 62% des porteurs enrichissent leur description de photos.
{: style="text-align: justify;"}

Si on compare la distribution du nombre d’images pour les projets échoues et pour ceux qui ont eu succès, on remarque que les derniers ont la tendance à avoir un nombre d’images plus grand (7 images en moyenne pour les projets réussis) par rapport à ceux qui échoues (4 images en moyenne).
{: style="text-align: justify;"}
 
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/images.png) 
{: style="text-align: center;"}
 

Le résultat du test t de Welch de comparaison des moyennes qui permet de conclure, avec un niveau de confiance de 95%, que le nombre d’images en moyen attachées à la description des projets qu’échoue est inférieur à celui des projets qu’on succès, ce qui confirme l’hypothèse que le nombre d’images postées par le porteur d’un projet influence la réussite de sa campagne.
{: style="text-align: justify;"}

### Analyse des facteurs Réseau
{: style="text-align: center;"}

#### Nombre de commentaires au projet 

Le nombre de commentaires postés par les bailleurs de fonds est un indicateur de leur niveau d’engouement dans le projet et également du niveau d’interaction entre eux et le porteur du projet.
{: style="text-align: justify;"}

Si on compare la distribution du nombre de commentaires postés pour les projets échoues et pour ceux qui ont eu succès, on remarque que les derniers ont la tendance à avoir une distribution des valeurs significativement plus étalée (29 commentaires postées en moyenne pour les projets réussis) par rapport à ceux qui échoues (seulement 2 commentaires postées en moyenne).
{: style="text-align: justify;"}
 
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/comments.png) 
{: style="text-align: center;"}

Le résultat du test t de Welch de comparaison des moyennes qui permet de conclure, avec un niveau de confiance de 95%, que le nombre de commentaire en moyen postés pour les projets qu’échoue est inférieur à celui des projets qu’on succès, ce qui confirme l’hypothèse que le nombre de commentaires postées par les internautes influence la réussite d’une campagne.
{: style="text-align: justify;"}

#### Nombre de partages du projet via les réseaux sociaux

Si on compare la distribution du nombre de partages via le réseau social pour les projets échoues et pour ceux qui ont eu succès, on remarque que les derniers ont la tendance à avoir une distribution des valeurs significativement plus étalée (474 partages en moyenne) par rapport à ceux qui échoues (104 partages en moyenne).
{: style="text-align: justify;"}
 
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/shares.png) 
{: style="text-align: center;"}
 

Le résultat du test t de Welch de comparaison des moyennes qui permet de conclure, avec un niveau de confiance de 95%, que le nombre moyen de partages via le réseau social pour les projets qu’échoue est inférieur à celui des projets qu’on succès, ce qui confirme l’hypothèse que le nombre de partages effectués par la communauté en ligne influence la réussite d’une campagne.
{: style="text-align: justify;"}

### Résultats tests statistiques
{: style="text-align: center;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-09-15-crowdfunding-analysis/tests.png) 
{: style="text-align: center;"}

## Conclusions
{: style="text-align: center;"}
•&nbsp;&nbsp;Plus l’objectif à atteindre est élevé, moins il y a de chance d’atteindre cet objectif
Un montant élevé peut être perçu comme un comportement avide des porteurs de projets.
Afin d’assurer la réussite de leur projet, les créateurs peuvent diminuer leur objectif tout en le dépassant par la suite.<br>
{: style="text-align: justify;"}
•&nbsp;&nbsp;Plus la campagne s’étend, plus les chances d’atteindre l’objectif diminuent<br>
On peut expliquer cela par le fait qu’une campagne plus longue peut être perçue comme un signe de manque de confiance de la part de l’entrepreneur dans son propre projet.<br>
{: style="text-align: justify;"}
•&nbsp;&nbsp;Plus une description est détaillée (en termes de nombre de mots et d’images), plus il y a de chance que la campagne soit positive<br>
{: style="text-align: justify;"}
•&nbsp;&nbsp;Le fait que le porteur poste des actualités sur l’état d’avancement de son projet peut avoir un impact positif sur sa réussite<br>
{: style="text-align: justify;"}
•&nbsp;&nbsp;Le nombre de fois qu’un projet est partagé via le réseau social ainsi que le nombre de commentaires peuvent influencer de façon positive la réussite d’une campagne<br>
{: style="text-align: justify;"}
