================
DM - Data Mining
================
| Dispensé par : *Rémy Cazabet* (2023 - Sept.Nov)

Introduction, Data Description
==============================

Types de données
----------------

*	**Nomimal** : Pas d'ordre à priori.
*	**Ordinal** : Peuvent être ordonnées.
*	**Interval** : Intervalles de valeurs numériques (ex: température 30°-20° = 15°-5°).
*	**Ratio** : Opérations sur des valeurs numériques.

| Dans la vraie vie, c'est plus compliqué. Il faut faire des choix de modélisations.
| Il y a des pièges : latitude/longitude, date, etc.
| Il manque souvent des valeurs dans les datasets. Ou les données peuvent être erronées.

.. topic:: 2 problèmes communs

	*	Valeurs out-of-range (ex: un poids de personne négatif).
	*	Zeros (ex: un poids de personne de 0kg).

| Une seule feature :math:`\rightarrow` univariate (ex: Age).
| Dans la vraie vie :math:`\rightarrow` multivariate (ex: (Age, Sexe, Poids, Taille, etc.)).

Décrire une variable
--------------------

*	Moyenne
*	Médiane
*	Mode
*	Min/Max
*	...

.. admonition:: Définition

	| Une **distribution** est une déscription de la fréquence à laquelle on retrouve des items.
	| C'est une fonction générée décrivant la possibilité d'observer un évènement possible.
	| Elle peut être **discrète** ou **continue**.

.. topic:: Distribution normale

	| Beaucoup de problèmes réels suivent une distribution normale.
	| Variations aléatoires autour d'une moyenne définie.

	.. figure:: img/dm-distribution.png
		:scale: 50%

.. topic:: Distribution de la loi puissance

	| Un changement relatif sur une quantité résulte en un changement proportionnellement relatif sur une autre quantité.
	| Ex: Les tremblements de terre 10 fois plus puissants sont :math:`x` fois moins fréquents.

	.. figure:: img/dm-lawpower.png
		:scale: 50%

P-value
~~~~~~~

.. admonition:: Définition

	| La **p-value** est la probabilité que ma donnée observée soit observable sur une distribution générée.
	| Une p-value élevée a de grande probabilité de venir d'une hypothèse nulle.

| On met un *threshold* sur la p-value (comme 0.05).
| Si la p-value est inférieure au *threshold*, on peut dire que la donnée a peu de chance que la donnée observée soit observable sur une distribution générée.
| Si elle est au-dessus, on peut dire que c'est probable.

Variance
~~~~~~~~

| Moyenne des carrés des écarts à la moyenne.

.. math::
	Var(X)=\sigma^{2}=E[(X-\mu)^{2}] \\
	\sigma^{2}={\frac {1}{N^{2}}\sum _{i<j}(x_{i}-x_{j})^{2}

Déviation standard
~~~~~~~~~~~~~~~~~~

| Racine carrée de la variance.

.. math::
	\sigma =\sqrt{\sigma ^{2}}=\sqrt{E[(X-\mu )^{2}]}

Interactions de variables
-------------------------

Matrice de covariance
~~~~~~~~~~~~~~~~~~~~~

| Extension de la variance à plusieurs variables.
| La covariance est dure à interpréter. Si elle est supérieur à 0, il y a un lien de corrélation.
| On la normalise pour obtenir le coefficient de corrélation.

.. math::
	\begin{bmatrix}
	Var(X_{1}) & Cov(X_{1},X_{2}) & \cdots & Cov(X_{1},X_{n}) \\
	Cov(X_{2},X_{1}) & Var(X_{2}) & \cdots & Cov(X_{2},X_{n}) \\
	\vdots & \vdots & \ddots & \vdots \\
	Cov(X_{n},X_{1}) & Cov(X_{n},X_{2}) & \cdots & Var(X_{n})
	\end{bmatrix}

	Cov(X,Y)=E[(X-E[X])(Y-E[Y])] \\
	Cov(X,X)=Var(X)

Coefficient de corrélation
~~~~~~~~~~~~~~~~~~~~~~~~~~

| Coefficient de corrélation de Pearson.

*	Normaliser la covariance par la déviation standard.
*	Pas besoin d'avoir des données normalisées.
*	| **+1** : corrélation positive parfaite :math:`X=aY`.
	| **-1** : corrélation négative parfaite :math:`X=-bY`.
	| **0** : On ne peut rien dire.

.. math::
	\rho_{X,Y}={\frac {Cov(X,Y)}{\sigma _{X}\sigma _{Y}}}

Corrélation de Spearman
~~~~~~~~~~~~~~~~~~~~~~~

| Coefficient de corrélation de rang de Spearman.
| Montre la corrélation entre 2 variables avec un fonction non-linéaire.
| Coefficient de corrélation de Pearson appliqué aux rangs des données.

.. math::
	r_{s}=\rho_{R(X),R(Y)}={\frac {Cov(R(X),R(Y))}{\sigma _{R(X)}\sigma _{R(Y)}}}

Notions de distances
~~~~~~~~~~~~~~~~~~~~

.. figure:: img/dm-euclidean.png
	:scale: 50%

	**Distance euclidienne** : :math:`\sqrt{(x_{1}-x_{2})^{2}+(y_{1}-y_{2})^{2}}`

.. figure:: img/dm-manhattan.png
	:scale: 50%

	**Distance de Manhattan** : :math:`|x_{1}-x_{2}|+|y_{1}-y_{2}|`

.. figure:: img/dm-chebychev.png
	:scale: 50%

	**Distance de Chebychev** : :math:`\max(|x_{1}-x_{2}|,|y_{1}-y_{2}|)`

Feature scaling
~~~~~~~~~~~~~~~

*	**Normalisation** : :math:`x'=\frac{x-min(x)}{max(x)-min(x)}\;:\;x'\in[0,1]`
*	**Normalisation à la moyenne** : :math:`x'=\frac{x-avg(x)}{max(x)-min(x)}\;:\;0=mean`
*	**Standardisation** : :math:`x'=\frac{x-\bar{x}}{\sigma}\;:\;0\rightarrow mean\;:\;-1/+1\rightarrow std`

Règles d'or
-----------

| Dans la vraie vie, les données ne suivent pas une distribution théorique ; les propriétés sont toujours corrélées ; les relations sont toujours non-linéaires.
| **GIGO** : Garbage In, Garbage out.

Clustering beyond k-means
=========================

Clustering
----------

K-means
~~~~~~~

.. admonition:: Définition

	| Pour un nombre de cluster :math:`k`, trouver partition de données minimisant la distance inter-cluster, équivalent à :
	
	*	La distance carrée de points à leur centroïde.
	*	La distance carrée entre les éléments d'un cluster.

.. math::
	argmin_{s}\sum_{i=1}^{k}\sum_{x\in S_{i}}||x-\mu_{i}||^{2} = argmin_{s}\sum_{i=1}^{k}|S_{i}|Var(S_{i})

| Découvrir l'optimum gobal est NP-difficile.

*	K-means naïf : Convergence vers un mauvais minimum local si un centroïde initial mauvais.
*	K-means++ : Améliore les résultats. A une tendance à chercher des clusters de mêmes tailles, et circulaires.

| Les données doivent être normalisées.

Mélanges Gaussien (Gaussian mixtures)
-------------------------------------

| Chaque clusers peuvent être décrit avec une distribution normale centrée sur son centroïde, avec la probabilité d'observer un point descendant avec la distance au centroïde.

.. admonition:: Définition

	| On définit un modèle génératif pour :math:`k` clusters.

	*	Chaque cluster est définit par une distribution gaussiène définit par un centroïde et une matrice de variance ou covariance.
	*	On doit trouver les paramètres :math:`\Theta` (centres, variances) qui maximisent la probabilité d'observer les données :math:`X`.
	*	On cherche donc : :math:`\Theta^{*}=argmax_{\Theta}P(X|\Theta)`

| Permet de trouver des clusters de formes non-circulaires, de tailles différentes.
| On ajoute un paramètre de *force* :math:`\pi` pour chaque cluster. :math:`p(X) = \sum_{i=1}^{k}\pi_{i}G(X|\mu_{i},\sigma_{i})`

.. admonition:: Algorithme EM (Expectation Maximization)

	| :math:`Z` l'assignation sur les points pour leur plus grande probabilité d'appartenance à un cluster.

	#.	Initialiser :math:`\Theta` aléatoirement.
	#.	Répéter jusqu'à convergence :

		#.	**E-step** : Calculer :math:`Z` pour :math:`\Theta` courant.
		#.	**M-step** : Actualiser :math:`\Theta` avec :math:`Z` courant.

| Utiliser la **Minimum Description Length (MDL)** pour choisir le nombre de clusters.

DBSCAN
------

| Définition de paramètres locaux :

*	:math:`\epsilon` : La distance maximale pour que 2 points ne soient pas considérés comme différents.
*	**minPts** : Le nombre minimum de points atteignables.
*	Pas de défintion de nombre de clusters.
*	**Core point** : Un point avec au moins :math:`minPts` points dans un rayon de :math:`\epsilon`.

.. admonition:: Algorithme

	#.	Créer un graphes avec les points comme noeuds et les arcs entre les points à une distance inférieure à :math:`\epsilon`.
	#.	Détecter les composantes connexes du graphe.
	#.	Pour les noeuds non-core. Si il y a aucun *core point* atteignable, on l'oublie tel du bruit. Sinon, on l'ajoute à la composante connexe du *core point* atteignable.

| **Forces** : Pas besoin de définir un nombre de clusters ; peut découvrir des formes arbitraires ; notion de bruit.
| **Faiblesses** : Définir :math:`\epsilon` est compliqué ; risque d'étirement des clusters.

Evaluation de clustering
------------------------

| 2 types d'évaluation :

*	**External evaluation (extrinsic)** : Il y a un *ground truth*, qui peut être une approximation de ce que l'on veut.
*	**Internal evaluation (intrinsic)** : Il n'y a pas de *ground truth*. On évalue les propriétés intrinsèques des clusters.

Score silhouette
~~~~~~~~~~~~~~~~

#.	:math:`a(i)` : La distance moyenne entre :math:`i` et les autres points du cluster.
#.	:math:`b(i)` : Le minimum des distances moyennes entre :math:`i` et les points du cluster le plus proche.
#.	:math:`s(i)` =

	*	Si :math:`a(i) < b(i)` : :math:`1 - \frac{a(i)}{b(i)}`
	*	Si :math:`a(i) > b(i)` : :math:`\frac{b(i)}{a(i)} - 1`
	*	Si :math:`a(i) = b(i)` : :math:`0`

| Le coefficient silhouette est la moyenne des :math:`s(i)` pour tous les points.

Davies-Bouldin Index (DBI)
~~~~~~~~~~~~~~~~~~~~~~~~~~

| La moyenne des ratios de similarité de chaque clusters avec le cluster le plus proche.
| Une valeur faible indique des clusters bien séparés.

Dunn Index
~~~~~~~~~~

.. math::
	DI_{m} = \frac{min_{1\leq i < j \leq m} \delta(C_{i}, C_{j})}{max_{1\leq k \leq m} \Delta_{k}}

| Avec :

*	:math:`\delta(C_{i}, C_{j})` : La distance entre les clusters :math:`C_{i}` et :math:`C_{j}`.
*	:math:`\Delta_{k}` : Le diamètre du cluster :math:`C_{k}`.

Networks I - Centralities
=========================

.. admonition:: Notation d'un graphe 

	| :math:`G=(V,E)`

	*	:math:`V` est l'ensemble des noeuds (ou sommets) du graphe.
	*	:math:`E` est l'ensemble des arêtes (ou liens) du graphe.
	*	:math:`u \in V` est un noeud du graphe.
	*	:math:`(u,v) \in E` est une arête du graphe.

.. admonition:: Densité

	*	**Degré moyen** : :math:`<k> = \frac{2|E|}{|V|}`
	*	**Densité** : :math:`d = \frac{2|E|}{|V|(|V|-1)}`
	*	**Coefficient de clustering** : Les triangles sont importants dans les vraies réseaux. :math:`C_{u} = d(H(N_{u}))`
	*	**Moyenne du coefficient de clustering** : :math:`<C> = \frac{1}{|V|}\sum_{u \in V} C_{u}`
	*	**Coefficient de clustering global** : :math:`C^{G} = \frac{3\Delta}{\Delta^{max}}`

.. admonition:: Paths, Walks, Distance

	*	**Walk** : Séquence de noeuds adjacents.
	*	**Path** : *Walk* sans noeuds répétés.
	*	**Path length** : Nombre d'arêtes dans un *Path*.
	*	**Weighted path length** : Somme des poids des arêtes dans un *Path*.
	*	**Shortest path** : *Path* de longueur minimale.
	*	**Weighted shortest path** : *Path* de poids minimal.
	*	**Distance** : Longueur du *Shortest path*.
	*	**Diamètre** : Distance maximale entre deux noeuds du graphe. :math:`<l> = \frac{1}{|V|(|V|-1)}\sum_{i \neq j} d_{ij}`

Centralitées
------------

| On peut mesurer l'importance d'un noeud avec la **centralitée**.

*	**Farness** : Distance moyenne vers tous les noeuds du graphe. :math:`farness(u) = \frac{1}{|V|-1} \sum_{v \in V, v \neq u} l_{u,v}`
*	**Closeness** : Inverse de la farness. :math:`closeness(u) = \frac{|V|-1}{\sum_{v \in V, v \neq u} l_{u,v}}`
*	**Centralité harmonique** : :math:`harmonic(u) = \frac{1}{|V|-1} \sum_{v \in V, v \neq u} \frac{1}{l_{u,v}}`
*	**Centralité de proximité** : Mesure comment un noeud joue un rôle de pont. :math:`C_{B}(v) = \sum_{s \neq v \neq t \in V} \frac{\sigma_{st}(v)}{\sigma_{st}}` avec :math:`\sigma_{st}` le nombre de *Shortest path* de :math:`s` à :math:`t` et :math:`\sigma_{st}(v)` le nombre de *Shortest path* de :math:`s` à :math:`t` passant par :math:`v`.

Définitions récursives
----------------------

| Les **noeuds importants** sont ceux qui sont connectées à des **noeuds importants**.

.. math::
	C_{u}^{t+1} = \frac{1}{\lambda} \sum_{v \in N_{u}} C_{v}^{t}

| Avec : :math:`\lambda` un facteur de normalisation.

PageRank
~~~~~~~~

| 2 améliorations principales : 

*	Sur les graphes dirigées, problème de noeuds sources : on ajoute un gain central constant sur tous les noeuds.
*	Les noeuds avec une grande centralitée la donne à leurs voisins.

| Idée de base : PageRank peut être interprété comme un *random walk* avec un restart.

Networks II - Détection de communautés
======================================

| La détection de communautés est comme le problème de clustering, mais sur des graphes.

Quelques algos
--------------

Girvan & Newman
~~~~~~~~~~~~~~~

.. admonition:: Algorithme de Girvan & Newman

	#.	Calculer la *betweenness* de chaque arêtes.
	#.	Enlever l'arête avec la plus grande *betweenness*.
	#.	Répéter jusqu'à ce qu'il n'y ait plus d'arêtes.

| Introduction de la **modularité**. On la calcule sur une partition du graphe.
| Elle compare le nombre d'arêtes dans une communauté avec le nombre d'arêtes attendues dans une communauté aléatoire.

.. math::
	Q = \frac{1}{(2m)} \sum_{vw}[A_{vw} - \frac{k_{v}k_{w}}{2m}]\delta(c_{v},c_{w})

*	:math:`\delta(c_{v},c_{w})` : 1 si :math:`v` et :math:`w` sont dans la même communauté, 0 sinon.
*	:math:`A_{vw}` : 1 si :math:`v` et :math:`w` sont connectés, 0 sinon.
*	:math:`\frac{k_{v}k_{w}}{2m}` : Probabilité que :math:`v` et :math:`w` soient connectés dans un graphe aléatoire.

| La modularité compare le réseau avec un **null network**.
| Le but de la méthode de Girvan et Newman et d'optimiser la modularité.

Louvain
~~~~~~~

.. admonition:: Algorithme de Louvain

	#.	Initialiser chaque noeud dans sa propre communauté.
	#.	Répéter jusqu'à convergence : pour chaque noeuds, pour chaque voisins, si ajouter le noeud à la communauté du voisin augmente la modularité, on le fait.
	#.	Création d'un ensemble induit : chaque communauté devient un noeud, et les arêtes sont la somme des poids entre les communautés.

Infomap
~~~~~~~

| Trouver la partition qui minimise la description de n'importe quel *random walk* sur le graphe. On veut compresser la description des random walks.
| Infomap définit une fonction de qualité à la place de la modularité. Tout algorithme peut être utilisé pour optimiser cette fonction.
| Infomap peut reconnaître des random walks, pas des communautés.

Stochastic Block Model (SBM)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| **SBM** est basé sur les statistiques.
| Chaque noeud correspond à une seule communauté. Pour chaque paire de communauté, on associe une densité qui est la probabilité qu'une arrête existe.
| On précise le nombre de clusters.

Evaluation de structure de communautés
--------------------------------------

| Comme pour le clustering :

*	**Intrinsèque / interne** : Fonction de qualité de partition, fonction de qualité des communautés.
*	**Comparaison des communautés observés et attendues** : Vrai réseau avec *ground truth*.

Prédiction de liens
-------------------

| Quels sont les liens manquants ou futurs ?

*	Basé sur les **graphes** : 

	*	**Local** : Grand clustering
	*	**Global** : 2 hubs non reliés ont plus de chance d'avoir des liens sur des petits noeuds pas liés.
	*	**Meso-scale** : Des probabilités de liens différentes pour des noeuds de communautés différentes.

*	Basé sur les **informations des noeuds** :

	* 	Sur les **features** même.
	*	Combiner avec du **ML**.

Première approche (Non-supervisé) - Heuristique
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| Le principe est de donner un score basé sur la topologie du graphe :math:`f(v_{i},v_{j})` exprimant la probabilité que :math:`v_{i}` et :math:`v_{j}` soient liés.
| :math:`\Gamma(x)` : les voisins de :math:`x`.

.. admonition:: Common Neighbour (CN)

	| *Les amis des mes amis sont mes amis.*
	| :math:`CN(x,y) = |\Gamma(x) \cap \Gamma(y)|`

.. admonition:: Coefficicent de Jaccard

	| Intuition :

	*	**Haute probabilité** : 2 personnes qui connaissent seulement les mêmes 3 personnes.
	*	**Basse probabilité** : 2 personnes qui connaissent 3 personnes sur 1000.

	| :math:`JC(x,y) = \frac{|\Gamma(x) \cap \Gamma(y)|}{|\Gamma(x) \cup \Gamma(y)|}`

.. admonition:: Hub promoted

	| Intuition : Normaliser par le nombre de voisins.
	| :math:`HP(x,y) = \frac{|\Gamma(x) \cap \Gamma(y)|}{min(|\Gamma(x)|,|\Gamma(y)|)}`

.. admonition:: Adamic adar

	| Intuition : Un noeud connecté seulement à une personne représente plus qu'un noeud connecté à 1000 personnes.
	| :math:`AA(x,y) = \sum_{z \in \Gamma(x) \cap \Gamma(y)} \frac{1}{log(|\Gamma(z)|)}`

.. admonition:: Resource allocation

	| Pénalise plus qu'Adamic Adar.
	| :math:`RA(x,y) = \sum_{z \in \Gamma(x) \cap \Gamma(y)} \frac{1}{|\Gamma(z)|}`

.. admonition:: Preferential attachment

	| Intuition : Les noeuds avec beaucoup de voisins ont plus de chance d'avoir des liens avec des nouveaux noeuds.
	| :math:`PA(x,y) = |\Gamma(x)| \cdot |\Gamma(y)|`

.. admonition:: D'autres scores

	| **Sorenson Index** : :math:`SI(x,y) = \frac{|\Gamma(x) \cap \Gamma(y)|}{|\Gamma(x)| + |\Gamma(y)|}`
	| **Salton Cosine Similarity** : :math:`SC(x,y) = \frac{|\Gamma(x) \cap \Gamma(y)|}{\sqrt{|\Gamma(x)| \cdot |\Gamma(y)|}}`
	| **Hub Depressed** : :math:`HD(x,y) = \frac{|\Gamma(x) \cap \Gamma(y)|}{max(|\Gamma(x)|,|\Gamma(y)|)}`
	| **Leicht-Holme-Nerman** : :math:`LHN(x,y) = \frac{|\Gamma(x) \cap \Gamma(y)|}{|\Gamma(x)| \cdot |\Gamma(y)|}`

.. admonition:: Structure de communautéS

	*	On calcule la structure de communautés sur le graphe.
	*	Si les noeuds sont dans la même communauté, on assigne un gros score, sinon un petit score.

Seconde approche (Supervisé) - Score de similarité
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| On utilise les algorithmes de ML pour apprendre à combiner les heuristique.
| On utilise les heuristiques comme features.

Classification de noeuds
------------------------

| On veut prédire la classe d'un noeud :

*	Valeurs manquantes.
*	Apprendre des informations sur des personnes sur des réseaux sociaux.
*	Type d'article sur Wikipedia.

Méthodes récentes
~~~~~~~~~~~~~~~~~

*	**Deep Neural Network (DNN)** : Utiliser comme *state of the art* pour les tâches supervisées.
*	**Graph Convolutional Neural Network (GCN)** : Prédiction de liens ; classification de noeuds ; classification de graphes ; etc.
*	**Variational Graph Autoencoder (VGA)** : Prédiction de liens ; graph embedding ; etc.
*	**Graph Attention Networks (GAT)** : Méchanisme d'attention pour les graphes.
*	**Diffusion, Convutionnal, Recurrent NN (DCRNN)** : Données dynamiques.

Pour plus d'informations : :ref:`GNN`

Recommendation / Factorisation matricielle
==========================================

| Le **facteur latent** est un problème populaire de DM. Avec 2 types de données, comment reconstruire une information. *(tâche non supervisée)*
| Les **recommendations basées sur le contenu** décrivent les objets avec des features. On recommande des objets qui ont des features similaires. *Souvent, pas très efficace.*
| Le **filtrage collaboratif** utilise les utilisateurs comme features.

Définition du modèle
--------------------

| On modèlise les données avec une matrice :math:`U \times I`. Avec :math:`U` les utilisateurs et :math:`I` les items.
| :math:`X(u, i)` reprèsente les intéractions entre les utilisateurs et les items.

.. admonition:: Extraire une baseline

	| On estine une score de baseline :math:`(u,i)` basé sur 2 constantes : :math:`b_{u}`, :math:`b_{i}`.

	*	:math:`b_{u}` : Capture la tendance de :math:`u` a donner des grands ou petits scores.
	*	:math:`b_{i}` : Capture la tendance de :math:`i` a recevoir des petits ou grands scores.
	*	On minimise : :math:`\sum_{r_{ui} \in R_{train}} (r_{ui}-(\mu + b_{u} + b_{i}))^{2}+\lambda (b_{u}^{2} + b_{i}^{2})`.
	*	:math:`\mu` : Note moyenne pour un utilisateur et un item aléatoire.

User-based KNN
--------------

.. admonition:: K-Nearest-Neighbors

	#.	Trouver :math:`k` voisins les plus similaires d'un item.
	#.	Prédire la note de l'item comme la moyenne des notes des :math:`k` voisins.

| Appliqué aux utilisateurs :

#.	Trouver les :math:`k` voisins les plus similaires.
#.	Chaque voisins *vote* pour les items qu'ils aiment.

.. figure:: img/dm-knn.png
	:scale: 50%

	User-based KNN

| Calculer la similarité entre des utilisateurs :

*	**Jaccard similarity** *(binaire)* : :math:`\frac{|likes(u \& v)|}{(union like)}`
*	**Mean Squared Difference (MSD)** *(notes)*
*	**Cosine similarity** *(notes)* : :math:`cos(\Theta) = \frac{A \cdot B}{||A|| \cdot ||B||} = \frac{\sum_{i=1}^{n} A_{i}B_{i}}{\sqrt{\sum_{i=1}^{n} A_{i}^{2}} \sqrt{\sum_{i=1}^{n} B_{i}^{2}}}`
*	**Cosine similarity** *(binaire)* : :math:`\frac{|likes(u \& v)|}{\sqrt{|likes(u)|} \sqrt{|likes(v)|}}`

Item-based Collaborative Filtering
----------------------------------

| On veut évaluer l'intérêt de :math:`(u,i)` : 

#.	Pour chaque item :math:`x` aimé par :math:`u`, on calcule la similarité entre :math:`x` et :math:`i`.
#.	:math:`(u,i)` est la moyenne des similarité de :math:`(x,i)` pour chaque item :math:`x` aimé par :math:`u`.

.. figure:: img/dm-ibcf.png
	:scale: 50%

	Item-based Collaborative Filtering

Matrix Factorization Collaborative Filtering
--------------------------------------------

*	On commence avec une matrice :math:`A` *(type user/interaction)*.
*	On cherche 2 matrices :math:`U` et :math:`V`, afin de minimiser une fonction de coût :math:`L(A, UV)`.

.. figure:: img/dm-mfcf.png
	:scale: 50%

	Matrix Factorization Collaborative Filtering

.. figure:: img/dm-objFunc.png
	:scale: 50%

	Objective functions

.. admonition:: Optmisation

	| **Weighted Alternating Least Square (WALS)**

	#.	Initialiser à des valeurs aléatoires.
	#.	Répéter jusqu'à convergence :

		#.	Fixer :math:`U` et résoudre :math:`V`.
		#.	Fixer :math:`V` et résoudre :math:`U`.

*	**MF + Regularization** : :math:`\sum_{r_{ui} \in obs} (r_{ui}-\hat{r}_{ui})^{2} + \lambda (||q_{i}||^{2} + ||p_{u}||^{2})`

	*	:math:`q_{i}` et :math:`p_{u}` : espaces latents.
	*	:math:`\lambda` : controle la force de la régularisation.

*	**MF + Baseline** : :math:`\sum_{r_{ui} \in obs} (r_{ui}-\hat{r}_{ui})^{2} + \lambda (b_{i}^{2} + b_{u}^{2} + ||q_{i}||^{2} + ||p_{u}||^{2})`

	*	:math:`b_{i}` et :math:`b_{u}` : scores espérés pour les items et les utilisateurs.

Evaluation des systèmes de recommandations
------------------------------------------

*	Cacher des utilisateurs : 

	#.	On entraine avec toutes les données sur une partition des utilisateurs.
	#.	On valide sur les autres utilisateurs, considérés comme nouveaux.

*	Cacher des paires :math:`(u,i)` :

	#.	On cache un nombre de paires :math:`(u,i)` aléatoirement.
	#.	On évalue sur ces paires cachées.

Variante de MF - Non-negative Matrix Factorization (NMF)
--------------------------------------------------------

| On veut des facteurs positifs, puisque certaines variables pouvaient s'annuler dans un MF classique.

Co-Clustering
-------------

| L'objectif est de trouver des sous-matrices denses au sein d'une matrice.

.. math::
	Q = \sum_{i}^{n} \sum_{j}^{d} A_{ij} - \frac{k_{i}k_{j}}{|A|}\delta_{ij}

*	:math:`A` : matrice à co-clusterisé, dimension :math:`n \times d`.
*	:math:`k_{i}` : le degré pondéré de :math:`i`.
*	:math:`\delta_{ij} = 1` : :math:`i,j` sont du même co-cluster.
*	:math:`|A|` : Somme de toutes les valeurs dans la matrice.

Reduction de dimension *Low dimensionality embedding*
=====================================================

| Avoir des centaines/milliers d'attributs est un problème pour l'analyse de données. On veut donc réduire le nombre d'attributs, tout en gardant les informations importantes.
| La réduction de dimensions peut créer une variable seule qui capture ce qui est commun.

PCA
---

.. admonition:: Définition

	| La **Principal Component Analysis (PCA)** définit de nouvelles dimensions qui sont des combinaisons linéaires des dimensions originales.
	| L'objectif est de concentrer la *variance* sur certaines dimensions.

.. admonition:: Algorithme

	#.	Trouver un *axe*, un vecteur qui minimise la variance. *(la distance carré de tout les points à cet axe)*
	#.	Pour :math:`d` in :math:`(initial_d - 1)` : Trouver un autre axe orthogonal à tout les précédents qui minimise la variance.
	#.	Garder la première k-dimension.

| En pratique on cherhce les vecteurs propres de la matrice de covariance de la matrice de données centrées. Si on veut :math:`k` nouvelles dimensions, on garde les :math:`k` vecteurs propres avec les plus grandes valeurs propres.

Manifolds
---------

.. admonition:: Principe général

	#.	Définir une notion de distance entre les éléments dans l'espace original.
	#.	Définir une notion de distance entre les éléments dans l'espace réduit.
	#.	Minimiser la différence entre les distances.

MDS
~~~

| La **Multi-Dimensional Scaling (MDS)** minimise simplement la distance entre l'espace original et l'espace réduit.

.. admonition:: Algorithme

	#.	Calculer toutes les distances entre les objets, ce qui donne une matrice de similarité.
	#.	Calculer le PCA de la matrice de similarité.

Isomap
~~~~~~

| Une variation de MDS.

#.	On définit un graphe tel que les noeuds sont connectés si leur distance est inférieure à un threshold.
#.	Calcule de la matrice de similarité, tel que la distance soit la distance du plus court chemin dans le graphe pondéré.
#.	Appliquer MDS.

T-SNE
-----

| La **t-distributed Stochastic Neighbor Embedding (t-SNE)** est une méthode non-linéaire de réduction de dimensions. *(actuellement la plus populaire)*

| Distance dans l'espace original :math:`P` :

*	Pour calculer à quel point :math:`j` est loin de :math:`i`, on considère une distribution normal centrée en :math:`j` avec une variance de :math:`\sigma`.
*	Mathématiquement : la distance est donnée avec :math:`s_{j|i}^{P} = e^{-\frac{||x_{i}-x_{j}||^{2}}{2\sigma^{2}}}`.
*	:math:`P_{j|i} = \frac{s_{j|i}^{P}}{\sum_{k \neq i} s_{j|k}^{P}}` : La probabilité que :math:`j` soit un voisin de :math:`i`.

| :math:`\sigma` faible préserve surtout les distances locales. :math:`\sigma` donne plus d'importance aux longues globales.

Low dimensionality embedding
----------------------------

| Actuellement l'usage de la réduction de dimensions sert à encoder des objets complexes en vecteurs.

.. admonition:: Exemples

	*	**Word2Vec** : Réduction de dimensions pour les mots.
	*	**Doc2Vec** : Réduction de dimensions pour les documents.
	*	**Node2Vec** : Réduction de dimensions pour les noeuds de graphes.

Word Embedding
--------------

| Vu dans le cours de BIML : :ref:`BIML-WE`.

Graph Embedding
---------------

.. admonition:: *Skipgram* générique

	*	Prend en entrée :

		*	L'élément à englober.
		*	Une liste de *contexte*.

	*	Donne en sortie : Un embedding avec des propriétés

		*	Fonctionne bien avec le machine learning
		*	Les éléments similaires sont proche dans l'espace.
		*	Garde à peu près la structure globales.

Deepwalk
~~~~~~~~

| **Deepwalk** est une méthode de *skipgram* pour les graphes.

#.	Génère des *phrases* avec une marche aléatoire.
#.	Applique *skipgram*.

Node2Vec
~~~~~~~~

| **Node2Vec** utilise une marche aléatoire biaisée pour tuné le contexte pour capturer *ceux que l'on souhaite*.

Rôles des embeddings
--------------------

| Dans *Node2Vec/Deepwalk*, le contexte collecté contient des *labels* des noeuds rencontrés. On pourrait mémoriser les *propriétés* des noeuds.

Deep Learning and embeddings
----------------------------

| Après chaque couches de DNN, les objets sont représentés par les vecteurs. On peut ensuite utiliser ses embeddings pour d'autres tâches.

Objects/Vectors to Graphs
-------------------------

.. admonition:: Approche simple : Matrice de corrélation

	#.	Calculer la corrélation entre les variables.
	#.	Garder les corrélations au-dessus d'un threshold.
	#.	Les valeurs de corrélations peuvent être utilisées comme poids.

| On peut utiliser les graphes comme alternative à la réduction de dimensions pour la visualisation.
| Dans beaucoup de cas, le réseau va être trop dense pour l'analyser. On peut utiliser une *backbone extraction* qui est une méthode qui retient les arrêtes importantes.

Frequent Pattern Mining
=======================

| L'objectif est de trouver les objets qui apparaissent souvent ensemble.

.. admonition:: Définition

	*	**Objets** : :math:`I={i_{1}, i_{2}, ..., i_{n}}`
	*	**Transaction** : :math:`(t_{i} \subseteq I)`
	*	**Database** : :math:`D={t_{1}, t_{2}, ..., t_{m}}`
	*	**Itemset** : :math:`X \subseteq I`

	*	**Support absolu** d'un itemset :math:`X` in :math:`D` : Nombre de transactions contenant :math:`X`.
	*	**Support relatif** : :math:`\frac{abs_support(X)}{|D|}`
	*	**Itemset fréquent** : Itemset avec un support supérieur ou égal au plus petit support donné.

	*	**Association rule** : :math:`X \rightarrow Y` avec :math:`X,Y \subseteq I` et :math:`X \cap Y = \emptyset`.
	*	**Support** de :math:`X \rightarrow Y` : :math:`W = X \cup Y`

Scores d'intérêt
----------------

.. math::
	conf(X \Rightarrow Y) = P(Y|X) = \frac{supp(X \cap Y)}{supp(X)} = \frac{nombre \; de \; transactions \; contenant \; X \; et \; Y}{nombre \; de \; transactions \; contenant \; X}

.. note::
	La confiance n'est pas symétrique.

| Si :math:`Y` à une grande confiance, mais est aussi fréquent, la confiance n'est pas suffisante.
| On utilise donc le **lift** : :math:`lift(X \Rightarrow Y) = \frac{conf(X \Rightarrow Y)}{supp(Y)}`.

| :math:`leverage(A \rightarrow C) = support (A \rightarrow C) - support(A) \times support(C)` : est la différence entre la fréquence observée de :math:`A` et :math:`C` apparaissant ensemble et la fréquence attendue si :math:`A` et :math:`C` étaient indépendants. 0 montre une indépendance.

Frequent Itemset Extraction
---------------------------

.. admonition:: Approche naïve

	#.	Générer tous les itemsets possibles.
	#.	Calculer le support de chaque itemset.

.. warning::
	| Problème d'explosion combinatoire.

*	Si :math:`X_{1}` est fréquent, alors :math:`X_{2} \subset X_{1}` est fréquent.
*	Si :math:`X_{1}` n'est pas fréquent, alors :math:`X_{2}, X_{1} \subset X_{2}` n'est pas fréquent.

.. admonition:: Trick

	#.	Trouver les itemsets fréquents de taille 1.
	#.	Trouver les itemsets fréquents de taille 2, en utilisant que les itemsets fréquents de taille 1.
	#.	Répéter pour toutes les tailles.

| On définit un pattern **closed** comme un pattern fréquent, et un pattern **maximal** comme un pattern qui n'est pas un sous-pattern d'un autre pattern fréquent.

Algorithme Apriori
------------------

.. figure:: img/dm-algoApriori.png
	:scale: 50%

Une question de recherche : Communities in degenerate link streams
==================================================================

| La plupart des réseaux sont dynamiques. Les noeuds et les liens apparaissent et disparaissent au cours du temps.

Slowly evolving networks (SEN)
------------------------------

| Les arrêtes change lentement. Le réseau est bien définit à tout moment :math:`t`.
| Un analyse statique à chaque temps :math:`t` donne une vision dynamique.

Unstable/Degenerate temporal networks
-------------------------------------

.. figure:: img/dm-lsandig.png
	:scale: 50%

	Interval Graph *(en haut)* et Link Stream *(en bas)*

| Une solution est de le transformer en SEN avec une aggregation/sliding window.

Centralités & Propriété d'un réseau dans un Stream Graph
--------------------------------------------------------

.. admonition:: Définition

	| Le **Stream Graph** permet de représenter n'importe quel type de graphe dynamique.

	.. math::
		S = (T, V, W, E)

	*	:math:`T` : L'ensemble des temps.
	*	:math:`V` : L'ensemble des noeuds.
	*	:math:`W` : Les noeuds présent à un temps :math:`V \times T`.
	*	:math:`E` : Les liens présent à un temps :math:`V \times V \times T`.

| Time-Entity designation : 

*	:math:`V_{t}` : L'ensemble des noeuds à un temps :math:`t`.
*	:math:`E_{t}` : L'ensemble des liens à un temps :math:`t`.
*	:math:`G_{t}` : Snapshot du graphe à un temps :math:`t`, :math:`G_{t} = (V_{t}, E_{t})`.
*	:math:`v_{t}` : Existe si :math:`v \in V_{t}`.
*	:math:`(u,v)_{t}` : Existe si :math:`(u,v) \in E_{t}`.
*	:math:`T_{u}` : L'ensemble des temps où le noeud :math:`u` existe.
*	:math:`T_{(u,v)}` : L'ensemble des temps où le lien :math:`(u,v)` existe.
*	:math:`N_{u}` : La fraction du temps où le noeud :math:`u` existe, :math:`N_{u} = \frac{|T_{u}|}{|T|}`.
*	:math:`L_{(u,v)}` : La fraction du temps où le lien :math:`(u,v)` existe, :math:`L_{(u,v)} = \frac{|T_{(u,v)}|}{|T|}`.

| Redéfinition des notions de graphe :

*	:math:`N = \sum_{v \in V} N_{v} = \frac{|W|}{|T|}` : Nombre de noeuds.
*	:math:`L = \sum_{(u,v) \in E} L_{(u,v)} = \frac{|E|}{|T|}` : Nombre de liens.
*	:math:`d = \frac{L}{L_{max}}` : Densité du graphe.

| Dans les SG, un cluster :math:`C` est un sous-ensemble de :math:`W`.

.. note::
	| J'ai skip des notions parce que bon... définir des trucs et ne pas les utiliser ça suffit.

Random Models for dynamix networks
----------------------------------

*	**Snapshot Shuffling** : Garde l'ordre des snapshots, mais mélange les liens.
*	**Sequence Shuffling** : Mélange les snapshots, mais garde les liens.
*	**Link Shuffling** : Garde le temps d'activation des paires de noeuds, rend aléatoire le graphe aggréger.
*	**Timeline Shuffling** : Garde le graphe aggréger, mais rend aléatoire le temps d'activation des paires de noeuds.

Dynamic Community Detection
---------------------------

| Différentes approches :

*	**Instant optimal** :

	*	Permet de réutiliser des algorithmes statiques.
	*	Pas de *partition smoothing*.
	*	Les labels peuvent être *smoothed*.
	*	Simple à parallèliser.

*	**Temporal trade-off** : 

	*	Ne peut pas être parallelisé (itératif).
	*	Bien pour les analyses en temps réels.

*	**Croos-Time** :

	*	Demande de connaître l'évolution entière en avance.
	*	Bien pour les interprétation à postériori.

.. note::

	*	**No Smoothness** : Aucune partition à l'instant :math:`t` doit être la même que celle trouvé par un algorithme statique.
	*	**Smoothness** : Une partition à l'instant :math:`t` est un compromis entre les *bonnes* communautés d'un graphe à l'instant :math:`t` et les similitudes avec des partitions à différent moments.

| *Puis il parle de sur quoi il bosse atm donc c'est pas grave.*