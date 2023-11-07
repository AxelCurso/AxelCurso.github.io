============================================
TAA - Techniques d'apprentissage automatique
============================================

TAA à partir de données
=======================
| Les données ne sont pas des informations.

.. admonition:: Définitions
	:class: myDefinition

	*	**Donnée** : Description élémentaire d'un objet. (une observation, une transaction, un signal, un graphe, ...)
	*	**Information** : Représente le moyen pour un individu de comprendre son environnement.
	*	**Connaissance** : Etat de transition de la donnée.

.. figure:: img/taa-triangle.png
   :scale: 50%

Prise de recul
==============
| Préparation du terrain
| Avant de commencer à coder : analyser et préparer le jeu de données.

#.	Pré-traitement + codage :
	
	:math:`\Rightarrow` Data engeenering

	*	Il faut traiter les données nuisibles/aberantes d'abord.
	*	Codage : faire une vectorisation de la donnée brute.
#.	Sélection de variables : 
	
	:math:`\Rightarrow` Fisher engeenering
	Réduire le nombre de dimensions matricielles.

	*	Détecter les variables ayant des valeurs trés proches pour tout les individus.
	*	Détecter les fortes corrélations entre les variables.
	*	Imputation des données manquantes.
#.	Normatiser les données :

	*	Centrer et réduire les données.

Apprentissage automatique (Machine Learning)
============================================
| Discipline de l'IA qui consiste à modéliser une fonction statistique pour résoudre les problèmes complexes, linéairement ou non séparables.
| :math:`y=f(x)` avec :math:`x\in\rm I\!R^{p}` et :math:`y` la valeur cible.

.. figure:: img/taa-separation.png
   :scale: 50%

| Chercher le minimum global entre tous les minimums locaux.

Types d'apprentissage
---------------------
.. figure:: img/taa-diffTypes.png
	:scale: 50%

.. note::
	*	**Statistique** : Mathématiques appliquées.
	*	**Probabiliste** : Génératif.
	*	**Supervisé** : y est totalement connu.
	*	**Semi-supervisé** : y est partiellement connu.
	*	**Non-supervisé** : y est totalement inconnu.

*	A base de distance : KNN, K-means, ...
*	Connexioniste : Réseaux de neurones, ...
*	A base de densité : SVM, ...
*	Modèle probabiliste : BN (Bayesian Network), ...
*	A base d'induction : Arbre de décision, ...
*	A base de régression : Régression linéaire, régression logistique, ...

.. admonition:: Définition
	
	**Neurone formel (artificiel)** : Unité de traitement qui prend en entrée des données sous forme de vecteur :math:`x=(x_{1},x_{2},...,x_{n})` et qui produit en sortie une valeur réel :math:`s` en fonction de poids de connexion :math:`w=(w_{1},w_{2},...,w_{n})`.

Le neurone formel passe par 2 fonctions :

*	Une linéaire :math:`F(x,w)` pour calculer son activation :math:`a`.
*	La deuxième fonction est non-linéaire :math:`f(a)` pour calculer sa décision :math:`s`.

.. figure:: img/taa-neuroneFormel.png
	:scale: 50%

Il existe 2 types de neurones formels :

*	**Neurone produit scalaire** : :math:`F(x,w)=<x,w>=\sum_{i=1}^{n}x_{i}w_{i}`
*	**Neurone distance** : :math:`F(x,w)=||x-w||^{2}`

| Si les poids sont normalisés, alors il existe un lien entre les 2 types.
| :math:`||x-w||^{2}=||x||^{2}+||w||-2<x,w>`

Différents modèles
==================
1er modèle : ADALINE
--------------------
| **ADALINE** : ADAptive LInear NEuron
| On suppose des données en entrée :math:`x=(x_{1},x_{2},...,x_{n})` avec :math:`x\in\rm I\!R^{p}` et les sorties désirées :math:`d=(d_{1},d_{2},...,d_{n})`.

.. note::
	ADALINE est un modèle adaptatif qui consiste à calculer une sortie :math:`y` en fonction d'un vecteur de poids :math:`w` tel que \:

	.. math::
		y = w_{0}+<x,w>\\
		  = w_{0}+\sum_{i=1}^{n}x_{i}w_{i}

.. admonition:: Algorithme

	#.	Initialiser aléatoirement les poids :math:`w`.
	#.	Boucle jusqu'à convergence :

		#.	Présenter une donnée :math:`x^{k}` avec sa sortie :math:`d^{k}`.
		#.	Calculer l'écart : :math:`e=d^{k}-<x^{k},w^{k}>`.
		#.	Calucler l'approximation : :math:`\Delta = -2\epsilon x^{k}`.
		#.	Mettre à jour les poids : :math:`w(t+1)=w(t)-\epsilon \Delta`.

| Comment trouver les formules ?
| L'erreur est : :math:`err(w)=(d^{k}-x^{k}w)^{2}` `erreur quadratique`.
| On cherche à minimiser l'erreur : :math:`\frac{\partial err(w)}{\partial w}=0`.
| On obtient : :math:`-2(d^{k}-x^{k}w)x^{k}=0` `équation normale`.

2ème modèle : MADALINE
----------------------
| **MADALINE** : Multiple ADALINE
| Modèle connexioniste à 2 couches :

#.	Plusieurs ADALINEs en parallèle.
#.	Une couche logique pour aggéger les sorties des ADALINEs.

.. figure:: img/taa-madaline.png
	:scale: 50%

.. _PMC:

3ème modèle : Perceptron
------------------------
| Modèle connexioniste à 3 couches :

#.	Capter les variables.
#.	Coder les variables.
#.	Décision.

.. figure:: img/taa-perceptron.png
	:scale: 50%

.. admonition:: Algorithme

	#.	Initialiser aléatoirement les poids :math:`w`.
	#.	Boucle jusqu'à convergence :

		#.	Présenter une donnée :math:`x^{k}` avec sa sortie :math:`d^{k}`.
		#.	Calculer la sortie du modèle : :math:`y^{k}=f(<w,\varphi (x^{k})>)`.
		#.	| Si la donnée est bien classée (:math:`d^{k}=y^{k}`) : :math:`w(t+1)=w(t)`.
			| Sinon : :math:`w(t+1)=w(t)+\epsilon \varphi (x^{k})d^{k}`.

.. note::
	**Perceptron** est plus rapide mais moins robuste que **ADALINE**.

	*	**ADALINE** : cherche la bonne frontière de séparation.
	*	**Perceptron** : cherche à tout bien classifier.

4ème modèle : Perceptron multi-classes
--------------------------------------
| Variante du perceptron pour séparer entre plusieurs classe :math:`C=(C_{1},C_{2},...,C_{p})`.
| Le principe consiste à apprendre plusieurs vecteurs de poids de connexion :math:`W=(W_{1},W_{2},...,W_{p})`, avec :math:`W_{i}=(w_{i1},w_{i2},...,w_{in})` tel que :

.. math::
	\forall i \in [1,p]\;si\;x\in C_{i}\;alors\;\forall j\neq i\;|\,<x,W_{i}>\;>\;<x,W_{j}>

.. figure:: img/taa-perceptronmcouches.png
	:scale: 50%

.. admonition:: Algorithme

	#.	Initialiser aléatoirement les poids :math:`W_{i}`.
	#.	Boucle jusqu'à convergence :

		#.	Présenter une donnée :math:`x^{k}\in C_{i}` avec :math:`i\in [1,p]`.
		#.	Calculer la sortie du modèle : :math:`C_{j}=ArgMax_{i}(<W_{i},x^{k}>)`.
		#.	| Si la donnée est bien classée (:math:`C_{j}=C_{i}`) : :math:`W(t+1)=W(t)`.
			| Sinon :

			*	:math:`W_{i}(t+1)=W_{i}(t)+\epsilon x^{k}`.
			*	:math:`W_{j}(t+1)=W_{j}(t)-\epsilon x^{k}`.
			*	:math:`W_{l}(t+1)=W_{l}(t)` avec :math:`l\neq j` et :math:`l\neq i`.