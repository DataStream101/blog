---
title:  "Dyoniso Un Systeme Expert Pour La Recommandation Des Vins"
date: 2019-12-03
tags: [project, expert system, reccomandation]
---
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/cover.png)
{: style="text-align: center;"}

*Quel vin choisir pour accompagner tel ou tel mets ?* C’est une question très répandue quand qu’il s’agit de définir un menu.
{: style="text-align: justify;"}

En effet, le choix d’un vin en fonction d’un mets, plus qu’un art, c’est une science qui demande de prendre en compte plusieurs facteurs afin de produire une alliance réussite.
{: style="text-align: justify;"}

L’objectif de ce projet a été la conception et implémentation d’un Système Expert qui, en reproduisant les connaissances des experts humaines dans le domaine gastronomique et œnologique,  soit en mesure de conseiller à un utilisateur la variété de vin qu’il lui faut en fonction du plat qu’il veut servir. 
{: style="text-align: justify;"}

Mais avant d'entrer dans le vif du sujet, il faut tout d'abord comprendre qu’est-ce que c’est un système expert.
{: style="text-align: justify;"}

## Les Système Experts
{: style="text-align: center;"}

Un Système Expert est l'une des différentes applications de l’Intelligence Artificielle. Il s'agit d'un programme qui permet de modéliser numériquement le raisonnement d’un professionnel spécialiste dans un domaine particulier.
{: style="text-align: justify;"}

Un Système Expert est un programme interactif qui constitue une aide à la décision. Souvent employé dans la diagnostique (médicale ou technique), il est capable de trouver une solution à une problématique qui lui est donnée en se basant sur ses propres connaissances, ses propres règles de déduction et les éléments fournis par l’utilisateur.
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/se.png)

Un Système Expert se compose de deux éléments :
*   Une **base de connaissances** (récupérée auprès des experts humains et encapsulée sous forme de ***règles*** et de ***faits***)
{: style="text-align: justify;"}

*	Un mécanisme d'inférence (appelé **moteur d’inférence**) lui permettant d'utiliser ces connaissances pour répondre à des questions et résoudre un problème. Le moteur d’inférence est la partie algorithmique du système qui effectue la sélection et l’application des règles sur la base des faits qu’il connait et des éléments fournis par l’utilisateur.
{: style="text-align: justify;"}

## Le Workflow et les outils techniques
{: style="text-align: center;"}
Développer un système expert est un processus qui s’articule en plusieurs étapes :

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/etapes.png)

1.&nbsp;&nbsp;&nbsp;Il faut tout d’abord récupérer la connaissance auprès des experts humains
{: style="text-align: justify;"}
2.&nbsp;&nbsp;&nbsp;Une fois cette connaissance récupérée, il faut la représenter sous forme de faits et règles
{: style="text-align: justify;"}
3.&nbsp;&nbsp;&nbsp;Ensuite, il faut développer un mécanisme d'inférence qui soit capable d’inférer la solution à une problématique qui lui est posée
{: style="text-align: justify;"}
4.&nbsp;&nbsp;&nbsp;Finalement, il faut mettre en place une interface graphique qui permet à l’utilisateur d’interagir avec le programme.
{: style="text-align: justify;"}
 
Pour la réalisation de ce projet, deux différents langages de programmation ont été utilisés :
{: style="text-align: justify;"}
*	**Prolog**, un langage de programmation logique (ou déclarative) crée en 1972 par A. Colmerauer et Ph. Roussel, utilisé pour le codage de la base de connaissance du Système Expert. 
{: style="text-align: justify;"}
*	**Python 3.7** pour le traitement des données, la programmation du moteur d’inférence du Système Expert ainsi que de l’interface utilisateur.
{: style="text-align: justify;"}

Le code complet est disponible [ici](link github).<br>
{: style="text-align: justify;"}

## Les Données et l'Architecture de Dyoniso
{: style="text-align: center;"}

Dans la pratique, les connaissances sont récupérées en échangeant avec des experts humains mais, dans le cadre de ce projet, elles ont été extrapolées à partir d’un dataset disponible sur la plateforme de Data Science Kaggle et disponible [ici](https://www.kaggle.com/zynicide/wine-reviews#winemag-data-130k-v2.csv).
{: style="text-align: justify;"}
Ce dataset, recense les avis donnés par des sommeliers ou des amateurs de vin sur 130.000 différentes bouteilles ainsi que des informations complémentaires sur ces vins qui peuvent être regroupées en trois catégories:
{: style="text-align: justify;"}
- 	Informations géographiques
- 	Informations relatives à la personne qui a testé le vin
-   Informations relatives au vin

Sur la base des données à disposition, j'ai identifié les différents éléments que le système devait prendre en compte pour produire une recommandation.
{: style="text-align: justify;"}
En particulier, cette recommandation aurait été le résultat d’une séquence d’interactions entre le système et un utilisateur selon le schéma suivant
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/schema.png)

Du coup, le système doit être en mesure d’indiquer une variété de vin (ex. merlot, sauvignon blanc, etc.) en fonction non seulement de la catégorie du plat (apéritif, entrée, plat principal ou dessert) mais également de l’ingrédient principal du plat (s’il s’agit de viande rouge ou blanche, de poisson de mer, etc).
{: style="text-align: justify;"}
En outre, il doit donner la possibilité à l’utilisateur d’indiquer un prix maximum qu’il était prêt à dépenser.
{: style="text-align: justify;"}

Dans les sections suivantes, on va détailler l’approche technique utilisée dans chaque étape du processus d’implémentation du Système Expert. 
{: style="text-align: justify;"}

## 1ère Étape - Acquisition des Connaissances
{: style="text-align: center;"}

Le premier objectif a été l’extrapolation des informations relatives aux appariements vin/plat  contenues dans la variable 'description' du jeu de données. 
{: style="text-align: justify;"}

L'analyse d'un échantillon de descriptions a montré que dans une partie prépondérante de textes des mots liés à la nourriture étaient employés pour décrire les caractéristiques organoleptiques du vin et non pour suggérer un pariage.
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/desc.png)

Dans l'exemple ci-dessus, dans la première description, on fait référence à la viande rôtie pour décrire les odeurs de la variété de vin Syrah, alors que dans la deuxième description, on trouve la suggestion d’accompagner la variété Zindfandel avec de la viande grillée.  
{: style="text-align: justify;"}

À cause de ça, au lieu de rechercher des mots-clés liés à la norriture via la méthode de la *tokenisation*, j’ai décidé de rechercher des séquences de mots-clés qui pouvaient identifier de façon unique des plats.
{: style="text-align: justify;"}

Pour ça, je me suis servie d'un algorithme de NLP appelé *RAKE* (qui permet d’identifier des séquences de mots-clés dans un texte en analysant la fréquence d’apparition d’un mot ainsi que sa proximité avec d’autres mots) dans le but d'isoler des séquences de mots-clés liées à la norriture.
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/rake.png)

Au résultat issu de l'alogorithme RAKE, j'ai appliqué une autre technique de NLP, qui s’appelle *Part Of Speech Tagging*, et qui permet d’attribuer à un mot qui apparaît dans un texte la catégorie grammaticale correspondante en fonction du contexte.
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/pos.png)

En analysant le résultat, j’ai remarqué qu’il y avait des schémas récurrents dans la construction grammaticale qui pouvaient m’aider à mieux cibler les suggestions des plats.
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/pos_rec.png) 
{: style="text-align: center;"}

L’étape suivante a été la définition d’une fonction qui m’a permis d’extraire seulement les séquences de mots qui correspondaient aux schémas identifiés et, sur la base de ça, de matcher chacune variété de vin contenue dans le dataset avec la catégorie d'ingrédient pour laquelle celle variété-là était suggérée.
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/fonc.png)

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/match.png)

Dans le cadre du processus d’acquisition des connaissances, des opérations de traitement se sont rendues nécessaires sur la variable *Variété*.
{: style="text-align: justify;"}
En effet, un examen de ses valeurs a montré qu’il y avait des variétés qui étaient le résultat d’un mélange entre plusieurs cépages. Vu que mon objectif était de construire un système capable de donner une indication exhaustive, j’ai décidé de supprimer toutes les variétés indiquées comme ‘blend’.
{: style="text-align: justify;"}

La deuxième opération que j’ai réalisée, a été une harmonisation des noms des cépages réstant. En effet, je me suis confrontée à deux problématiques : dans certains cas des cépages avaient une différente appellation selon la région où ils étaient produits, dans d’autres cas, une même variété, était indiquée en différentes langues. Pour réaliser ce processus d’harmonisation, je me suis servie du site web appelé [*wine-searcher*](https://www.wine-searcher.com/) qui contient des fiches descriptives très détaillées pour les différents cépages.
{: style="text-align: justify;"}

Toujours à l’aide du site web *wine-searcher*, j’ai créé une nouvelle variable « Type » qui informe sur le type de vin (blanc, rouge, rosé) donné par chacune variété de vin.
{: style="text-align: justify;"}

En accord avec son architecture, l’un des éléments que le système aurait pris en compte pour produire sa recommandation aurait été la préférence de prix de l’utilisateur.
{: style="text-align: justify;"}
Toutefois, vu que le dataset de départ contenait les informations relatives au prix des *bouteilles* recensées mais aucune indication sur le prix par variété et vu que le système aurait sorti la suggestion d’une variété de vin et pas d’une bouteille en particulier, il me fallait définir une valeur de tendance pour le prix de chaque *variété*.
{: style="text-align: justify;"}
Pour ça, après avoir converti le prix des bouteilles en euro, j’ai calculé la moyenne des prix des bouteilles pour chaque variété et c’est cette valeur moyenne que j’ai pris en compte au moment de modéliser la base de connaissances.
{: style="text-align: justify;"}



## 2ème Étape - Modélisation de la Base des Connaissances
{: style="text-align: center;"}

La Base de Connaissances est une représentation formelle de la connaissance humaine dans le domaine considéré.
{: style="text-align: justify;"}

Il s’agit d’une collection de clauses de deux types, les faits et les règles, qui décrivent l’ensemble des propriétés d’objets réels (dans le cadre de ce projet les variétés de vin) et des relations entre les différents objets.
{: style="text-align: justify;"}

*	Les **Faits** représentent des données élémentaires que l’on considère comme vraies.
Dans la syntaxe de Prolog, il s'agit de formules atomiques constituées d'un prédicat suivi d’un ou d’une liste ordonnée de termes qui représentent les objets auxquels s'applique le prédicat.
{: style="text-align: justify;"}

Un exemple d'un fait défini dans la base de connaissance de Dyoniso est le suivant
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/fait.png)
{: style="text-align: center;"}

*	Les **Règles** sont des propositions qui énoncent la dépendance/relation d’un fait par rapport à d’autres faits.<br><br>
Une règle se compose toujours de deux parties : 
>-	Une partie de conditions qui portent sur les objets présents dans la base de connaissances sous forme de faits
>-	Une partie contenante les informations à déduire sur les objets qui valident les conditions définies dans la première partie. 
{: style="text-align: justify;"}
Un exemple d'une règle définie dans la base de connaissance de Dyoniso est le suivant

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/regle.png)

Quand une règle est appelée, son résultat est obtenu via un mécanisme d’unification. 
{: style="text-align: justify;"}
La base de connaissance complète est disponible [ici](link github).<br>


## 3ème Étape - Implémentation du Moteur d'Inférence et de l'Interface Utilisateur
{: style="text-align: center;"}

La 3ème et 4ème étape du processus ont été intégralement réalisées en Python.
Pour l’implémentation de l’interface utilisateur j’ai adopté le paradigme de la **Programmation Orientée Objets** et je me suis servie de la librairie *Tkinter*.
{: style="text-align: justify;"}

Chaque catégorie de plat a été représentée par un ensemble de classes et, au sien de chacune d’entre elles, une partie du moteur d’inférence a été imbriqué.
{: style="text-align: justify;"}

Cette approche modulaire m’a permis de gérer l’interaction entre l’utilisateur et le système expert de façon différente en fonction de la catégorie choisie, au tout début, par l’utilisateur. 
{: style="text-align: justify;"}

Le code complet est disponible [ici](link github).<br>


# Le Résultat
{: style="text-align: center;"}

Au démarrage de Dyoniso, la fenêtre du Menu Principale s’ouvre et le système demande à l’utilisateur de choisir la catégorie de plat pour laquelle il souhaite trouver un vin à accompagner.
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/menu.png)
{: style="text-align: center;"}


Lorsqu’il choisit la catégorie **Apéritif**, le système demande à l’utilisateur d’indiquer le type de vin qu’il préfère entre rouge, blanc ou rosé ou s’il n’a aucune préférence.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/apero_pref.png)
{: style="text-align: center;"}

Una fois sa préférence validé, le système lui demande s’il souhaite indiquer le prix maximum qu’il est prêt à dépenser. 
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/apero_prix.png)
{: style="text-align: center;"}

Après la validation du choix du prix, une nouvelle fenêtre contenante la recommandation sortie par le système s’ouvre. 
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/recom_page.png)
{: style="text-align: center;"}

En appuyant sur le bouton *Cliquer pour découvrir nos conseils*, la variété de vin suggérée par le système s’affiche ainsi qu’une description de ses caractéristiques principales.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/recom.png)
{: style="text-align: center;"}

Ensuite, l’utilisateur peut cliquer sur le bouton *Notre cave à vin* pour visualiser une sélection de bouteilles de la variété de vin suggérée avec leurs prix et le pays producteur.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/cave.png)
{: style="text-align: center;"}

Lorsque l’utilisateur choisit la catégorie **Entrée**, le système lui demande d’indiquer le type d’entrée qu’il va servir. 
{: style="text-align: justify;"}
Si l’entrée appartient aux catégories *Charcuterie* ou *Coquillages*, la question suivante que le système va lui poser est au sujet du prix.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/coq.png)
{: style="text-align: center;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/coq_prix.png)
{: style="text-align: center;"}

Par contre, si l’entrée appartient aux catégories *Quiche*, *Soupe* ou *Salade*, le système demande à l’utilisateur de lui fournir des informations complémentaires au sujet des ingrédients qu’il va utiliser.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/quiche.png)
{: style="text-align: center;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/ingr_quiche.png)
{: style="text-align: center;"}

Par exemple, si l’utilisateur indique comme ingrédient principal le fromages, le système lui demande quel type de fromages entre affinés, doux ou de chèvre/brebis, il va utiliser.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/choix_from.png)
{: style="text-align: center;"}

Une fois son choix validé, le système lui demande s’il souhaite indiquer le prix maximum qu’il est prêt à dépenser.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/quiche_prix.png)
{: style="text-align: center;"} 

En fonction de ce que l’utilisateur a indiqué, le système sort sa recommendation.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/recom_quiche.png)
{: style="text-align: center;"} 

Dans le cas où l’utilisateur choisit la catégorie **Plat Principal**, le système lui demande de sélectionner une catégorie de plat principal entre plat principal à base de Viande, Poisson, Pâtes ou Riz, Plat Exotique ou Épicés et Plat Végétariens.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/pp.png)
{: style="text-align: center;"} 

Après, le système lui demande d’indiquer le nom de la recette que l’utilisateur va cuisiner.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/recette.png)
{: style="text-align: center;"} 

Una fois le nom de la recette saisi, le système lui demande s’il souhaite indiquer le prix maximum qu’il est prêt à dépenser.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/prix_pp.png)
{: style="text-align: center;"} 

Et, en fonction de ce que l’utilisateur a indiqué, il sort sa recommendation.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/recom_pp.png)
{: style="text-align: center;"}

Lorsque l’utilisateur choisit la catégorie **Dessert**, le système lui demande d’indiquer le type de dessert qu’il va servir entre *Dessert au Chocolat* et *Dessert aux Fruits*.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/dessert.png)
{: style="text-align: center;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/dessert_choix.png)
{: style="text-align: center;"}


Une fois son choix validé, le système lui demande s’il souhaite indiquer le prix maximum qu’il est prêt à dépenser.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/prix_dessert.png)
{: style="text-align: center;"} 

En fonction de ce que l’utilisateur a indiqué, il sort sa recommendation.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-12-03-dyoniso-un-systeme-expert-pour-la-recommandation-des-vins/recom_dessert.png)
{: style="text-align: center;"}