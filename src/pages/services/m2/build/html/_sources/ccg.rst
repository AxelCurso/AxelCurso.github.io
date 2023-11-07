=========================================
CCG - Combinatoire, Complexité et Graphes
=========================================

*Samba Ndojh NDIAYE*

Complexité
==========
Complexité d'un algorithme
--------------------------
| Complexité en temps : estimation du nombre d'instructions
| Complexité en espace : estimation de l'espace mémoire

| :math:`\mathcal{O}(f(n)) \leadsto \exists c,n_{0}\,tq\,\forall n > n_{0},nb_instructions\,<\,c.f(n)`

.. admonition:: Exemples de complexités

	*	:math:`\mathcal{O}(log(n))` : logarithmique
	*	:math:`\mathcal{O}(n)` : linéaire
	*	:math:`\mathcal{O}(n^{k})` : polynomial
	*	:math:`\mathcal{O}(k^{n})` : exponentiel

Complexité d'un problème : classe de complexité
-----------------------------------------------
Complexité du meilleur algorithme résolvant l'instance la plus difficile du problème X.

Classe P
~~~~~~~~
| Il existe un algorithme polynomial résolvant X.
| :math:`Complexité\,de\,X<\mathcal{O}(n^{k})`

.. admonition:: Exemples de problèmes

	*	Rechercher un élément dans un tableau
	*	Tier un tableau, un fichier, une liste...
	*	Rechercher un plus court chemin entre 2 sommets d'un graphe

Classe NP
~~~~~~~~~
| Il existe un algorithme non-déterministe polynomial résolvant X.
| :math:`P\subseteq NP`

.. admonition:: Machine de Turing non déterministe

	*	exécute un nombre fini d'alternatives en parallèle
	*	:math:`X\in NP \Rightarrow vérif(X)\in P`

Classe NP-complet
~~~~~~~~~~~~~~~~~
Un problème NP-complet est un problème algorithmique pour lequel aucune solution rapide (en temps polynomial) n'est connue pour sa recherche, mais toute solution proposée peut être vérifiée rapidement.

.. admonition:: Vérifie ces propriétés

	*	Il est possible de vérifier une solution efficacement (en temps polynomial) ; la classe des problèmes vérifiant cette propriété est notée NP
	*	Tous les problèmes de la classe NP se ramènent à celui-ci via une réduction polynomiale ; cela signifie que le problème est au moins aussi difficile que tous les autres problèmes de la classe NP

.. admonition:: Démonstration de NP-complétude

	*	Montrer que X est dans NP
	*	Trouver une procédure polynomiale pour transformer un problème NP-complet en X

Classe NP-difficile
~~~~~~~~~~~~~~~~~~~
| Un problème NP-difficile est un problème au moins aussi difficile que ceux de la classe NP. (X pas forcément dans NP)
| :math:`NPcomplet\subset NPdifficile`

| Problème indécidable : il n'existe pas d'algorithme résolvant le problème.
| Exemple : problème de l'arrêt

.. note::
	Pour en savoir plus : `Le zoo des compléxités <https://complexityzoo.net/Complexity_Zoo>`__.

Exemples de problèmes complexes
===============================
SAT
---

| Problème de satisfiabilité booléenne.

*	Problème de décision : peut-on satisfaire toutes les clause ? :math:`\rightsquigarrow` NP-complet dans le cas général et polynomial si toutes les clause ont au plus 2 littéraux.
*	Problème d'optimisation : quel est le plus grand nombre de clause satisfaites ? :math:`\rightsquigarrow` NP-difficile.
*	Espace de recherche : :math:`O(2^{n})` où :math:`n` est le nombre de variables.

CSPs
----

| Problème de satisfaction de contraintes défini par :math:`(X, C, D)`.

*	:math:`X = {X_{1}, ..., X_{n}}` : ensemble des variables.
*	:math:`D(X_{i})` : domaine de :math:`X_{i}`.
*	:math:`C = {C_{1}, ..., C_{m}}` : ensemble des contraintes.

| On obtient donc : 

*	Problème de décision : peut-on satisfaire toutes les contraintes ? :math:`\rightsquigarrow` NP-complet dans le cas général, polynomial dans certains cas et parfois indécidable.
*	Problème d'optimisation : quel est le plus grand nombre de contraintes satisfaites ? :math:`\rightsquigarrow` NP-difficile.
*	Espace de recherche : :math:`k^{n}` si :math:`|X| = n` et :math:`|D(X_{i})| = k, \forall X_{i} \in X`.

Problème dans les graphes
-------------------------

| Exemple de problèmes ploynomiaux :

*	Déterminer les sous-ensembles de sommets connectés.
*	Trouver le plus court chemin entre 2 sommets.
*	Trouver un chemin passant 1 fois par chaque arc (Eulérien).
*	Connecter un ensemble de sommets au plus faible coût.
*	Maximiser un flot de véhicule dans un réseau de transport.

| Exemple de problèmes NP-complets/NP-difficiles :

*	Trouver un plus court cycle Hamiltonien.
*	Trouver :math:`k` sommets connectés 2 à 2 par des arrêtes.
*	Colorier les sommets.
*	Partitionner les sommets.
*	Comparer des graphes.

Problème de planification
-------------------------

| Défini par :

*	Un ensemble (potentiellement infini) d'états :math:`E`.
*	Un état initial :math:`E_{0} \in E`.
*	Un ensemble d'états finaux :math:`F \subset E`.
*	Un ensemble d'opérations :math:`O` permettant de passer d'un état à un autre.

| Un plan est une séquence d'opérations permettant de passer de l'état initial à un état final.

*	Problème de décision : existe-t-il un plan ? :math:`\rightsquigarrow` Algorithme polynomial.
*	Problème d'optimisation : quel est le plus court plan ?

Transition de phases
====================

| La difficulté d'un problème n'est pas la même en fonction de la taille de l'instance.
| Par exemple, cela peut dépendre du nombre de variables :math:`n` et du nombre de clauses :math:`p`. On peut donc faire des études de satisfiabilité :math:`\frac{p}{n}`.
| La **transition de phases** correspond à un pic de difficulté dans la résolution et est indépendant de l'algorithme utilisé. La transition de phases se trouve là où le taux de satisfiabilité est de 50%.

| On estime le taux de *constrainedness* :math:`\kappa` d'une instance :

*	Soit :math:`2^{n}` l'espace de recherche de l'instance.
*	Soit :math:`p` le nombre de solutions estimé de l'instance.
*	:math:`\kappa = 1-\frac{log_{2}(p)}{n}`

| La transition de phases se trouvent là où :math:`\kappa = 1`.

*	Si :math:`\kappa \approx 0` : l'instance est sous-contraintes.
*	Si :math:`\kappa \approx 1` : l'instance est critique.
*	Si :math:`\kappa \approx \infty` : l'instance est sur-contraintes.

`Pour en savoir plus <https://www.ijcai.org/Proceedings/91-1/Papers/052.pdf>`__ : Where the really hard problems are ? *(P. Cheeseman, B. Kanefsky et W.M. Taylor, [IJCAI’1991])*

Approches complètes
===================



Approches incomplètes
=====================

| Résolution de problèmes de satisfaction :math:`\rightarrow` recherche de la combinaison *maximisant la satisfaction*.
| Exploration optimiste de l'espace de recherche :math:`E`.

*	**Intensifier** la recherche autour des zones prometteuses.
*	**Diversifier** la recherche pour explorer de nouvelles zones.

| Qualité améliorée au fil du temps. Mais pas de garantie d'optimalité... Mais une complexité polynomiale.

*	Approches basées sur le **voisinage** : Nouvelles combinaisons construites à partir de combinaisons existantes.
*	Approches basées sur la **construction** : Nouvelles combinaisons construites à l'aide de modèles.

.. admonition:: Principe général

	*	Génération de une ou plusieurs combinaisons initiales.
	*	Tant que la qualité est insuffisante et que le temps maximum n'est pas atteint : On créer une plusieurs nouvelles combinaisons à partir d'une ou plusieurs combinaisons existantes.

| Trois instanciations de ce modèle :

*	**Recherche locale** : Sélection de la combinaison créée ; création d'une combinaison par mouvement.
*	**Optimisation par essaim de particules (PSO)** : Création de combinaisons par déplacement / vitesse ; mise à jour de la vitesse.
*	**Algorithmes génétiques** : Sélection des meilleures combinaisons de la génération ; création de combinaisons par croisement + mutation.

Voisinage et paysage
====================

.. admonition:: Définition d'un graphe de voisinage :math:`G=(E,V)`

	*	:math:`E` : Ensemble de combinaisons (espace de recherche).
	*	:math:`A` : Une approche incomplète basée sur le voisinage.
	*	:math:`V={(e_{i},e_{j}) | A peut visiter e_{j} à partir de e_{i}}`
	*	:math:`V(e_{i}) = {e_{j} | (e_{i},e_{j})\in V}` : Notation pour le voisinage d'une combinaison de :math:`e_{i}`.

	| En général :math:`V` n'est pas orienté. et :math:`G` doit être connexe.

.. admonition:: Définition d'un paysage de recherche

	| Un problème d'optimisation :math:`P=(E, f)` et un graphe de voisinage :math:`G=(E,V)`.

.. admonition:: Définitions

	*	**Optimum local** : Un point dont tous les voisins sont moins bons.
	*	**Plateau** : Ensemble de points connexes dans le graphe :math:`G=(E,V)` ayant tous la même valeur pour :math:`f`.
	*	**Bassin d'attraction d'un optimum local** : Point que l'on peut atteindre depuis :math:`e` (le minimum local) sans jamais monter.

*	Paysage avec un seul optimum local et pas de plateau :math:`\rightarrow` stratégie : *intensifier*.
*	Paysage rugueux : nombreux optima et distribution uniforme :math:`\rightarrow` stratégie : *diversifier*. Pas de corrélation entre qualité et distance à l'optimum global.
*	Paysage de type *masif central* :math:`\rightarrow` stratégie : *intensifier* et *diversifier*.

Recherche locale
================

.. admonition:: Algorithme Recherche Local :math:`(E, V, f)`

	#.	:math:`e` :math:`\leftarrow` une combinaison de :math:`E`
	#.	:math:`e*` :math:`\leftarrow` :math:`e`
	#.	Tant que :math:`f(e*)` :math:`\lt` borne et temps maximum non atteint

		#.	Choisir :math:`e' \in V(e)`
		#.	:math:`e` :math:`\leftarrow` :math:`e'`
		#.	Si :math:`f(e) \lt f(e*)` Alors :math:`e*` :math:`\leftarrow` :math:`e`
	
	#.	Retourner :math:`e*`

| Différentes stratégies pour choisir :math:`e' \in V(e)`

Gloutonne (ou *greedy local search*)
------------------------------------

| Choisir une combinaison :math:`e' \in V(e) \; tq \; f(e') \geq f(e)`.

*	**Best improvment** : choisir le voisin qui maximise :math:`f`.
*	**First improvment** : choisir le premier voisin qui améliore :math:`f`.

Random Walk
-----------

| Introduire la probabilité :math:`p_{noise}` de choisir un mouvement aléatoire.

#.	Soit :math:`x` un nombre tiré aléatoirement entre 0 et 1.
#.	Si :math:`x \leq p_{noise}` alors choisir un voisin aléatoire de :math:`e' \in V(e)` (*diversification*).
#.	Sinon choisir :math:`e' \in V(e)` qui maximise :math:`f` (*intensification*).

.. note::
	*	:math:`p_{noise} = 0` : recherche locale gloutonne.
	*	:math:`p_{noise} = 1` : recherche locale aléatoire.
	
	| En général, :math:`0.01 \leq p_{noise} \leq 0.1`.

Threshold Accepting
-------------------

| Introduire un seuil d'aléatoire pur :math:`\tau`.
| Choisir le premier voisin tel que :math:`f(e') - f(e) \gt \tau`.

.. note::
	*	:math:`\tau \rightarrow -\infty` : aléatoire pure.
	*	:math:`\tau \geq 0` : les mouvements dégradants la solution sont interdits.

Simulated Annealing
-------------------

| Introduire une température :math:`T` qui décroit à chaque mouvement.
| Choisir le premier voisin :math:`e \in V(e)` tel que soit :

*	:math:`f(e') \geq f(e)` : *intensification*.
*	:math:`x \lt e^{\frac{f(e') - f(e)}{T}}` : *diversification*. Où :math:`x` est un nombre aléatoire entre 0 et 1.

.. note::
	*	:math:`T \rightarrow \infty` : aléatoire pure.
	*	:math:`T \rightarrow 0` : glouton pure.

Taboue
------

#.	Introduire une liste taboue :math:`l` initialisée à vide.
#.	On ajoute le dernier mouvement à chaque itération (*ne garder que les :math:`k` derniers mouvements*).
#.	Choisir la combinaison :math:`e' \in V(e)` qui maximise :math:`f` et n'est pas dans :math:`l`.

Réactive
--------

| Comme pour la recherche **taboue**, mais avec une table de hachage pour mémoriser les clefs des combinaisons visitées et pouvoir modifier la taille de la liste taboue en fonction.
| Peu de collision :math:`\rightarrow` rétrécissement de la liste et inversement pour beaucoup de collisions.

Recherche à voisinage variable (*Variable Neighborhood Search (VNS)*)
---------------------------------------------------------------------

| Soient :math:`V^{1}, V^{2}, ..., V^{k}` des voisinages de :math:`e`.
| :math:`V^{t}(e)` : voisins de :math:`e` dans le voisinage :math:`V^{t}`.
| En général : :math:`|V^{t}(e)| \gt |V^{t-1}(e)|`.

#.	:math:`t \; \leftarrow \; 1`
#.	Tant que :math:`max{\frac{f(e'')}{e''} \in V^{t}(e)} \; : \; t \; \leftarrow \; t+1`
#.	:math:`e'` :math:`\leftarrow` meilleure combinaison de :math:`V^{t}(e)`

Recherche à très grand voisinage (*Very Large Neighborhood Search (VLNS)*)
--------------------------------------------------------------------------

*	Définir un voisinage très large.
*	Utiliser une approche complète pour explorer ce voisinage.
*	Approche gloutonne :math:`\rightarrow` *intensification*.
*	Très grand voisinage :math:`\rightarrow` *diversification*.


PSO et GA
=========

Optimisation par essaim de particules (*Particle Swarm Optimization (PSO)*)
---------------------------------------------------------------------------

*	**Essaim initial** : Générer un ensemble :math:`P` de :math:`n` combinaisons et une vitesse initiale :math:`v_{i}` pour chaque combinaison :math:`e_{i} \in P`.
*	Tant que la qualité est insuffisante et le temps maximum n'est pas atteint :

	*	:math:`\forall e_{i} \in P` :

		#.	Modifier la vitesse de :math:`e_{i}` : :math:`v_{i} \leftarrow \omega v_{i}+c_{1}f_{1}(best_{i} - e_{i})+c_{2}f_{2}(best_{V(e_{i})} - e_{i})`

			*	:math:`\omega` : inertie.
			*	:math:`c_{1}, c_{2}` : accélération.
			*	:math:`f_{1}, f_{2}` : nombres aléatoires :math:`\in [0, 1]`.

		#.	Déplacer :math:`e_{i}` en fonction de :math:`v_{i}` (:math:`e_{i} \leftarrow e_{i} + v_{i}`).

Algorithmes génétiques (*Genetic Algorithms (GA)*)
--------------------------------------------------

*	**Population initiale** : Générer un ensemble :math:`P` de :math:`n` combinaisons.
*	Tant que la qualité est insuffisante et le temps maximum n'est pas atteint :

	#.	**Sélection** d'un ensemble :math:`P' \subseteq P` de combinaisons.
	#.	**Croisement** de :math:`P'` pour générer un ensemble :math:`P''` de combinaisons.
	#.	**Mutation** de :math:`P''` pour générer un ensemble :math:`P'''` de combinaisons.
	#.	**Mise à jour** de :math:`P` par :math:`P'''`.

Gloutons
========

.. admonition:: Principe général

	#.	:math:`e \; \leftarrow` combinaison vide.
	#.	:math:`Cand \; \leftarrow` ensemble des composants de combinaisons.
	#.	Tand que :math:`Cand \neq \varnothing` :

		#.	Choisir le meilleur composant :math:`c \in Cand` et l'ajouter à :math:`e`.
		#.	Mettre à jour :math:`Cand` en fonction de :math:`c`.

	#.	Retourner :math:`e`.

Comment concevoir un algorithme glouton ?
-----------------------------------------

| 3 points à définir :

*	Identifier les composants de combinaisons.
*	Définir une fonction mettant à jour l'ensemble des candidats par rapport à une combinaison partielle.
*	Définir une fonction heuristique évaluant la qualité d'un composant par rapport à une combinaison partielle.

.. note::
	| Ajouter un peu d'aléatoire pour diversifier la recherche.

Approche *1 parmi les meilleurs*
--------------------------------

*	Sélectionner les :math:`k` meilleurs composants.
*	Choisir aléatoirement l'un d'entre eux.

Approche *probabiliste*
-----------------------

*	Probabilité de choisir :math:`c_{i} \in Cand` : :math:`p(c_{i}) = \frac{h(c_{i})^{\alpha}}{\sum_{c_{k} \in Cand} h(c_{k})^{\alpha}}`.
*	Tirer un nombre aléatoire :math:`x \in [0, 1]`.
*	Choisir :math:`c_{i} \; tq \; \sum_{j \lt i}p(c_{j}) \lt x \leq \sum_{j \leq i}p(c_{j})`.

Algorithmes par estimation de distribution (*Estimation of Distribution Algorithms (EDA)*)
==========================================================================================

| Approche évolutionniste.

.. admonition:: Principe général

	#.	Génération d'une population initiale :math:`P(0)`.
	#.	:math:`t \; \leftarrow \; 0`
	#.	Tant que la solution optimale n'est pas trouvée et que :math:`t \lt t_{max}` :

		#.	Sélectionner :math:`S(t) /subseteq P(t)` de solutions *prometteuses*.
		#.	Construire un modèle probabiliste :math:`M(t)` à partir de :math:`S(t)`.
		#.	Générer de nouvelles solutions :math:`N(t)` à partir de :math:`M(t)`.
		#.	Créer une nouvelle population :math:`P(t+1) \subseteq S(t) \cup N(t)`.
		#.	:math:`t \; \leftarrow \; t+1`

| Compromis entre simplicité et qualité.

Ant Colony Optimization (ACO)
=============================

.. admonition:: Modélisation mathématique (Deneubourg et al., 1990)

	*	Modèle stochastique de la dynamique de la colonie.
	*	Identifier les mécanismes permettant aux fourmis de s'auto-organiser pour résoudre le problème de la recherche d'un plus court chemin.

		*	Le probabilité de choix d'un chemin dépend du taux de phéromone déposé sur ce chemin :math:`\rightsquigarrow` qui dépend du nombre de fourmis l'empruntant.
		*	Evaporation de la phéromone.

.. admonition:: Principe général

	#.	Initialisation des traces de phéromone.
	#.	Répéter jusqu'à trouver la solution optimale ou atteindre une stagnation :

		#.	Chaque fourmit fournit une solution.
		#.	Mise-à-jour des traces de phéromone.

Construction de la solution par une fourmi
------------------------------------------

*	Soit :math:`C` début de la solution et :math:`Cand` les candidats.
*	Choisir :math:`v_{j} \in Cand` selon la probabilité :math:`p(v_{j})`.

.. math::
	p(v_{j}) = \frac{[\tau_{C}(v_{j})]^{\alpha} \cdot [\eta_{C}(v_{j})]^{\beta}}{\sum_{v_{k} \in Cand}[ \tau_{C}(v_{k})]^{\alpha} \cdot [\eta_{C}(v_{k})]^{\beta}}

*	:math:`\tau_{C}(v_{j})` : facteur phéromonal.
*	:math:`\eta_{C}(v_{j})` : facteur heuristique.
*	:math:`\alpha, \beta` : poids des facteurs (*paramètres*).

Mise-à-jour des traces de phéromone
-----------------------------------

*	**Evaporer** : Multiplier les traces de phéromones par :math:`(1-\rho)` :math:`\rightsquigarrow` :math:`\rho` : taux d'évaporation.
*	**Récompenser** : Ajouter de la phéromone sur les composants des meilleurs solutions proportionnellement à la qualité.

Influence des paramètres
------------------------

*	:math:`\tau_{min}, \tau_{max}` : taux de phéromone minimum et maximum :math:`\rightsquigarrow` l'intensification augmente quand :math:`\tau_{max} - \tau_{min}` augmente.
*	:math:`nbAnts` : nombre de fourmis :math:`\rightsquigarrow` la diversification augmente quand :math:`nbAnts` augmente.
*	:math:`\alpha` : poids du facteur phéromonal :math:`\rightsquigarrow` l'intensification augmente quand :math:`\alpha` augmente.
*	:math:`\rho` : taux d'évaporation :math:`\rightsquigarrow` la diversification augmente quand :math:`\rho` augmente.

Indicateurs d'exploration/intensification
-----------------------------------------

Exploration :math:`\rightsquigarrow` Taux de ré-échantillonnage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. math::
	Taux = \frac{nb\;solutions\;calculées - nb\;solutions\;différentes}{nb\;solutions\;calculées}

*	Exploration maximale :math:`\Leftarrow 0 \leq` taux :math:`\leq 1 \Rightarrow` Stagnation

Intensification :math:`\rightsquigarrow` Taux de similarité
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. math::
	Taux = similarité\; moyenne\; des \; solutions \; calculées \; S
	
	\rightsquigarrow moyenne \; des \; similarites \; des \; paires \; de \; solutions \; de \; S

	\rightsquigarrow similarité \; de \; 2 \; solutions = taux \; de \;composants \; communs

*	Augmentation du Taux :math:`\rightsquigarrow` Intensification

Problèmes de la recherches de sous-ensembles
============================================

.. admonition:: Définition

	| Une **problème de sous-ensembles** (Subset problem *(ss-problem)*) est défini par :math:`(S, S_{C}, f)` tel que :

	*	:math:`S` : ensemble d'objets candidats.
	*	:math:`S_{C} \subseteq P(S)` : ensemble des sous-ensembles consistants.
	*	:math:`f : S_{C} \rightarrow \mathbb{R}` : fonction objectif.

	| Le but est de trouver :math:`S^{*} \in S_{C}` tel que :math:`f(S^{*})` soit maximale.

.. admonition:: Exemples

	*	Problème du sac à dos (*Knapsack problem (KP)*).
	*	Problème de la couverture par ensembles (*Set covering problem (SCP)*).
	*	Problème de satisfaction de contraintes (*Constraint satisfaction problem (CSP)*).
	*	Recherche de cliques maximales (*Maximum clique problem (MCP)*).

*	Stratégie **vertex** : Apprendre les bons objets. Phéromones associés aux objets :math:`\tau(i) \rightsquigarrow` intérêt de choisir :math:`i`.
*	Stratégie **clique** : Apprendre les bonnes paires d'objets. Phéromones associés aux paires :math:`\tau(i,j) \rightsquigarrow` intérêt de choisir :math:`i` avec :math:`j`.

Algorithme générique
--------------------

| Paramètré par :

*	Un problème à résoudre :math:`(S, S_{C}, f)`.
*	Une stratégie phéromonale :math:`\Phi \in {vertex, clique}`.

A chaque cycle
~~~~~~~~~~~~~~

| Chaque fourmi construit un sous-ensemble avec un probabilité :math:`p(i)` d'ajouter un objet :math:`o_{i} \in Candidats` au sous-ensemble :math:`S_{k}`.

.. math::
	p(i) = \frac{[\tau_{factor}(o_{i}, S_{k})]^{\alpha} \cdot [\eta_{factor}(o_{i}, S_{k})]^{\beta}}{\sum_{o_{j} \in Candidats}[\tau_{factor}(o_{j}, S_{k})]^{\alpha} \cdot [\eta_{factor}(o_{j}, S_{k})]^{\beta}}

*	:math:`\tau_{factor}(o_{i}, S_{k})` : Dépend de la stratégie :math:`\Phi`.

	*	:math:`\Phi = vertex` : :math:`\tau_{factor}(o_{i}, S_{k}) = \tau(o_{i})`.
	*	:math:`\Phi = clique` : :math:`\tau_{factor}(o_{i}, S_{k}) = \sum_{o_{j} \in S_{k}} \tau(o_{j}, o_{i})`.

*	:math:`\eta_{factor}(o_{i}, S_{k})` : Dépend du problème à résoudre.

A la fin de chaque cycle
~~~~~~~~~~~~~~~~~~~~~~~~

| Récompense des meilleurs sous-ensembles. Composants de :math:`S_{k}` récompensés suivant la stratégie :math:`\Phi`.

*	:math:`\Phi = vertex` : Dépôt sur les sommets.
*	:math:`\Phi = clique` : Dépôt sur les arêtes de la clique.