====================================
BIML - Bio-Inspired Machine Learning
====================================
Dispensé par : *Mathieu Lefort*, *Rémy Cazabet* et *Frédéric Armetta* (2023 - Sept.Nov)

Introduction aux réseaux de neurones
====================================
*Mathieu Lefort*

Principes généraux de l'apprentissage profond
---------------------------------------------

.. admonition:: Objectifs de l'apprentissage

	| Qu'attendre d'un système apprenant

	*	**Mémorisation** : Retrouver la réponse à une entrée déjà vue.
	*	**Généralisation** : Retrouver la réponse à une entrée jamais vue.
	*	**Hypothèses** : Fonction localement continue, rasoir d'Occam.
	*	**Techniques** : Ensemble d'apprentissage/validation/test, régularisation, ...

| Différents types d'apprentissage :

*	**Supervisé** : :math:`y = f(x)` avec :math:`x \in X` et :math:`y \in Y`.

	*	*Régression* : :math:`Y` continu, typiquement :math:`\mathbb{R}^{n}`.
	*	*Classification* : :math:`Y` discret.
	*	*En pratique* : :math:`f(x) = \sum_{i=1}^{n}(a_{i}^{T} \cdot x + b_{i})\phi (x, \theta_{i})` avec :math:`\phi` une fonction non linéaire paramétrée par :math:`\theta_{i}, b_{i} \in \mathbb{R}^{card(Y)}` et :math:`a_{i} \in \mathbb{R}^{card(Y)\times card(X)}`.

*	**Non supervisé** : :math:`f(x)` avec :math:`x \in X`.

	*	*Clustering* : Regroupement des entrées par groupes.
	*	*Génératif* : Apprentissage de la distribution :math:`p(x)` (par ex. :math:`x=f(\tilde{x})`).

*	Par renforcement, par imitation, ...

Neurone artificiel
~~~~~~~~~~~~~~~~~~

*	Inspiration biologique :

	.. math::
		y = \begin{cases}
			1 & \text{si } \sum_{i=1}^{n}w_{i}x_{i} - \theta > 0 \\
			0 & \text{sinon}
		\end{cases}

*	Le neurone en apprentissage automatique :

	.. math::
		y = \begin{cases}
			1 & \text{si } \sum_{i=0}^{n}w_{i}x_{i} - \theta > 0 = w^{T}x > 0 \\
			0 & \text{sinon}
		\end{cases}


Perceptron (Multi Couches)
--------------------------

Détailler dans le cours d'apprentissage profond : :ref:`PMC`.

.. admonition:: Propriétés du PMC

	*	Approximateur universel (avec fonction d'activation sigmoïde ou gaussienne entre autres).
	*	Convergence potentiellement peu efficace (non convexe, espace de haute dimension, gradient évanescent ou non borné, ...).

Réseaux Convolutionnels
-----------------------

| Pour les images, on utilise des réseaux convolutionnels.

.. figure:: img/biml-cnnConv.png
		:scale: 50 %

		Convolution (rappel)

.. figure:: img/biml-cnnConvNeuron.png
		:scale: 50 %

		Neurone de convolution

| Les différentes couches sont :

*	**Convolution** :

	.. figure:: img/biml-cnnConvLayer.png
		:scale: 50 %

		Couche de convolution

*	**Padding** :

	.. figure:: img/biml-cnnPadding.png
		:scale: 50 %

		Padding

*	**Stride** :

	.. figure:: img/biml-cnnStride.png
		:scale: 50 %

		Stride

*	**Pooling** :

	.. figure:: img/biml-cnnPool.png
		:scale: 50 %

		Pooling

Architectures
~~~~~~~~~~~~~

*	LeCun (1989) : LeNet-5

	.. figure:: img/biml-cnnLeNet5.png
		:scale: 50 %

		LeNet-5

*	Krizhevsky et al. (2012) : AlexNet

	.. figure:: img/biml-cnnAlexNet.png
		:scale: 50 %

		AlexNet

.. admonition:: Bilan des réseaux convolutionnels

	*	De la convolution pour son invariance à la translation et partage de poids.
	*	Du *pooling* pour réduire les dimensionnalités.
	*	Un perceptron à la fin car plus de structure spatiale en haut niveau.
	*	Architecture transposable à la 1D (audio), à la 3D (vidéo), aux graphes, ...

Panorama général du domaine et *Trucs & Astuces*
------------------------------------------------

`Le zoo des réseaux de neurones <https://www.asimovinstitute.org/neural-network-zoo/>`__.

*	Traitement des données :

	*	Equilibrage/représentativité des données *penser aux biais*.
	*	Augmentation des données.
	*	Données centées normées : :math:`\frac{x-\bar{x}}{\sigma(x)}`.
	*	Utilisation de mini batchs.

*	Choix du modèle :

	*	Type d'architecture suivant les données / le problème.
	*	Choix de la fonction d'activation.

*	Apprentissage :

	*	Fonction de coût :
	
		*	**Régression** : Erreur quadratique moyenne (MSE). :math:`\frac{1}{2}\sum_{x,i}(t_{i}-y_{i})^{2}`
		*	**Classification** : Entropie croisée. :math:`\sum_{x}-log\frac{e^{yt}}{\sum_{i}e^{yi}}`

	*	Régularisation : :math:`+||w||` dans la fonction de coût.
	*	Bruitage / *drop out* : mise à 0 de certaines valeurs.
	*	Choix de l'optimiseur :

		*	**SGD** : La base.
		*	**momentum** : Rajout d'inertie dans le gradient.
		*	**Adagrad** : Adaptation du taux d'apprentissage (en fonction du gradient).
		*	**Adam** : Combinaison des 2 points précédents.

*	Obtenir les meilleurs performance :

	*	**Hyperparamètrage** : on part d'un réglage *de base* ...

		*	pour le MLP : une grande 1ère couche, puis taille décroissante.
		*	pour le CNN : augmentation du nombre de canaux à chaque couche (qui *compense* la réduction de la taille de la carte de features).

	*	... et ensuite on cherche empiriquement (grid search, random search, ...) ce qui marche sur le jeu de validation.
	*	**Fine tuning** : on part d'un modèle *générique* pré appris et on l'adapte localement à nos données.

Limitations de l'apprentissage profond
--------------------------------------

*	Surapprentissage
*	Bruit
*	Biais
*	Oubli catastrophique (oubli des anciennes données)

Connexion résiduelle
~~~~~~~~~~~~~~~~~~~~

*	Activations sautes des couches.
*	Gradient important remonte via les connections résiduelles.
*	:math:`\rightarrow` réduit le *vanishing gradient problem*.

Couche de *Batch Norm*
~~~~~~~~~~~~~~~~~~~~~~

*	Normaliser les activations, puis change moyenne et variance à l'aide des paramètres apprenables.
*	Permet d'entraîner des réseaux plus profonds et plus rapidement.
*	Peut aider à stabiliser l'apprentissage.

`ResNet <https://fr.wikipedia.org/wiki/R%C3%A9seau_neuronal_r%C3%A9siduel#:~:text=Un%20r%C3%A9seau%20neuronal%20r%C3%A9siduel%20(%20ResNet,que%20les%20r%C3%A9seaux%20neuronaux%20pr%C3%A9c%C3%A9dents.>`__.

.. _GNN:

Graph Neural Network (GNN)
==========================
*Rémy Cazabet*

Intro
-----

| Les réseaux de neuronnes sont super efficaces sur les données structurées, et les graphes sont des données purement structurés.
| **GCN** : Graph Convolutional Network. Une adaption de la convolution sur les images pour les graphes.

Convolution
~~~~~~~~~~~

| Extrait des caractéristiques de "haut niveau".
| La convolution est définie par les poids de son noyau (qui peuvent être appris).
| La convolution d'une image peut être vu comme un cas spécial d'une opération de graphe.

.. admonition:: Différences entre image et graphe

	*	Dans les réseaux, il n'y a pas le même nombre de voisins pour chaque noeuds.
	*	La représentation matricielle : C'est le même objet mais l'interpretation change. La position d'un noeud (d'un graphe) dans la matrice n'a pas de signification.

	.. figure:: img/biml-gcnRepresentation.png
		:scale: 50 %

.. admonition:: Définition
	:class: myDefinition

	| L'interprétation du **message passing** est que tout les noeuds envoient leur informations à leur voisins.
	| La convolution combine les informations des voisins d'un noeud et de ses informations pour créer une nouvelle caractéristique.

Intuition sur les couches
~~~~~~~~~~~~~~~~~~~~~~~~~

*	Convolution dans les **images** :

	#.	Calcule une somme pondérée des valeurs des voisins.
	#.	Souvent suivi d'un pooling.

*	Convolution dans les **graphes** : Les poids ne peuvent pas être appris directement.

	#.	La moyenne des caractéristiques des voisins (comme un pooling).
	#.	Calcule la somme pondérée des caractéristiques des voisins.

Une convolution sur les graphes peut être vu comme une couche linéaire avec :

*	En entrée : La moyenne des caractéristiques des voisins.
*	En sortie : Une imbrication du nombre de dimensions.

.. warning::
	*	Les items d'un dataset d'image sont indépendentes les unes des autres.
	*	Pas les graphes. On peut traiter les noeuds indépendemment mais les caractéristiques ne doivent pas être cachés. Seulement les cibles peuvent être découpées en train/test.

Convolution de graphe
~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/biml-gcnGCN.png
	:scale: 50 %

	Stacking convolution layers

| Chaque couches de convolution permet de dépendre des noeuds plus loin dans le réseaux.

#.	Les résultats dépendent des voisins.
#.	Les résultats dépendent des voisins des voisins.
#.	...

.. note::
	Similaire aux convolutions dans les images.

GCN equation
------------

.. math::
	H^{(l+1)} = f(H^{(l)}, A) = \sigma(\hat{D}^{-\frac{1}{2}}\hat{A}\hat{D}^{-\frac{1}{2}}H^{(l)}W^{(l)})

*	:math:`H^{(l)}` : Matrice des caractéristiques des noeuds à la couche :math:`l`.
*	:math:`A` : Matrice d'adjacence du graphe. :math:`(\hat{A} = A + I)`
*	:math:`\hat{D}` : Matrice diagonale des degrés des noeuds.
*	:math:`W^{(l)}` : Matrice des poids de la couche :math:`l`.
*	:math:`\sigma` : Fonction d'activation (souvent relu).

.. figure:: img/biml-gcnKarataClub.png
	:scale: 50 %

	Graphe : Karate Club

.. figure:: img/biml-gcnAdj.png
	:scale: 50 %

	Matrice d'adjacence :math:`\hat{A}`

.. admonition:: Normalisation de la matrice d'adjacence

	.. figure:: img/biml-gcnDAdj.png
		:scale: 50 %

		Moyenne :math:`D^{-1}\hat{A}`

	.. figure:: img/biml-gcnDAdjD.png
		:scale: 50 %

		Moyenne par degrés :math:`\hat{D}^{-\frac{1}{2}}\hat{A}\hat{D}^{-\frac{1}{2}}`

Chaque imbrication est calculée comme :

.. math::
	h_{i}^{l+1} = \sum_{j \in N_{i}} \frac{1}{\sqrt{deg(i)}\sqrt{deg(j)}}h_{j}^{l}W^{T}

:math:`h_{j}^{l}` : Caractéristiques du noeud :math:`j` à l'ancienne couche.

GCN : step by step *(Sans caractéristiques : seulement stucture)*
-----------------------------------------------------------------

| Taille de la matrice :math:`W` par couches :

.. math::
	W_{0} : d_{0} \times d_{1} \\
	W_{1} : d_{1} \times d_{2} \\
	... \\
	W_{n} : d_{n} \times d_{n+1}

*	:math:`d_{0}` : Nombre de caractéristiques par noeuds dans le graphe d'origine.
*	:math:`d_{n+1}` : Nombre de caractéristiques voulues.

Phase avant
~~~~~~~~~~~

| On regarde ce qu'il se passe sans apprentissage des poids.
| On observe une structure gardée malgrés des poids aléatoires. Ceci grâce aux structures locales.

Phase arrière
~~~~~~~~~~~~~

| Pour apprendre les poids, on utilise de la **rétropropagation**.

.. admonition:: Résumé

	*	Une fonction de **perte** est définie pour comparer les valeurs calculées et les vrais labels.
	*	La **dérivée** de la fonction de perte est calculée par rapport aux poids.
	*	Les poids sont mis à jour en utilisant la **descente de gradient**.

| On définit un objectif semi-supervisé :

*	Les labels sont connus seulement pour quelques noeuds.
*	On choisit une fonction de perte pour de la classification binaire.

GAT
---

| **GAT** : Graph ATtention Network.
| Le principe des GAT et de permettre aux noeuds de choisir les noeuds voisins les plus importants.

.. math::
	h_{i}^{l+1} = \sum_{j \in N_{i}} \alpha_{ij}h_{j}^{l}W^{t}\\
	\alpha_{ij} attention from i to j.

#.	Une matrice d'attention apprenable qui convertit les imbrications de noeuds vers des nouvelles imbrications pour l'attention.

	*	:math:`z_{i} = Wh_{i}`
	*	:math:`W` : Matrice de poids apprenable.
	*	:math:`h_{i}` : Caractéristiques du noeud :math:`i`.

	On ne veut pas que les imbrications soient combinées avec la position dans le graphe ou la manière dont il se comporte pour l'attention des autres.

#.	Concaténer les deux imbrications.

	| :math:`z_{i} || z_{j}`
	| :math:`[a,b,c]||[f,e,d] = [a,b,c,f,e,d]`
	| :math:`e_{ij} = a^{T}[z_{i}||z_{j}]`

#.	Ajouter une fonction d'activation.

	*	:math:`e_{ij} = ReLu(a^{T}[z_{i}||z_{j}])`

#.	Normalisation softmax.

	*	On a des scores d'attention non normalisés.
	*	:math:`\alpha_{ij} = softmax(e_{ij}) = \frac{exp(e_{ij})}{\sum_{k \in N_{i}}exp(e_{ik})}`

| Une seule couche peut ne pas être assez performant. Nous venons de créer une tête d'attention.
| On combine plusieurs têtes d'attention pour créer une couche. On peut le voir comme les différents canaux d'une convolution.

Graph Autoencoder
-----------------

| **Autoencoder** : Un réseau de neuronne non-supervisé qui essaye de reconstruire son entrée. Composé d'un codeur et d'un décodeur. Au milieu, il y a une brique qui représente les données et on la contraint à être petite.

.. figure:: img/biml-gcnAE.png
	:scale: 50 %

	Autoencoder

| **Graph Autoencoder** : Un autoencoder pour les graphes.

.. admonition:: Architecture classique

	*	**Encodeur** : Des couches de GCN.
	*	**Décodeur** : Un *dot product* entre les embeddings, plus une activation.
	*	On minimise la *binary cross entropy* entre les matrices d'adjacences d'entrées et de sorties.

Variantes
~~~~~~~~~

| **VAE** : Variational Autoencoder. Une amélioration des AE.

.. admonition:: Limites des AE

	*	Pauvre continuité.
	*	Pauvre complétude.

| La solution des VAE et d'encoder les données dans un espace latent plutôt que sur un seul point.

.. figure:: img/biml-gcnVAE.png
	:scale: 50 %

	VAE

| Le modèle est entrainé comme suit :

#.	Les entrées sont encodées sur un espace latent comme une distribution gaussienne.
#.	Un point de l'espace latent est échantillonné.
#.	Le point est décodé pour reconstruire les entrées.
#.	La perte est calculée entre les entrées et les sorties.
#.	La perte est rétropropagée pour mettre à jour les poids.

| **VGAE** : Variational Graph Autoencoder. Une adaptation pour les graphes.

*	Couche 1 : Un GCN.
*	Couche 2 : 2 GCN en parallèle (un pour apprendre le *centroid* et un pour la *variance*).
*	Pour décoder : On prend un point aléatoire de la *multivariate gaussian*.

Link prediction
---------------

| Quels liens sont manquants ou vont apparaître dans le futur.
| Objectif binaire : lien ou pas lien.
| En utilisant un VGAE : dot product entre les embeddings des noeuds.
| Score de prédiction : le résultat du dot product sur le vecteurs de noeuds.

Transductive/Inductive
~~~~~~~~~~~~~~~~~~~~~~

*	**Transductive** : On a accès à tout le graphe. On cache une partie des labels.
*	**Inductive** : Entraînement sur un set de noeuds/graphes. Le résultat est appliqué sur des noeuds/graphes inconnus.

Graphe multi-partite
~~~~~~~~~~~~~~~~~~~~

| On ne peut pas apprendre un seul GCN sur des noeuds différents.
| On apprend plusieurs couches. Chacunes pour les noeuds spécifiques.

Deep Learning for Natural Language Processing (NLP)
===================================================
| *Frédéric Armetta*

.. note::
	| Beaucoup de screen de slides, pas forcément de notes

Introduction
------------

| Applications du NLP :

*	**Classification** : Analyse de sentiments ; classifications de textes ; détection de spam ; ...
*	**Génération** : Prédiction de mots ; Résumé de textes ; ...
*	**Tagging** : Part-of-speech tagging ; spell checking ; ...
*	étendus à la reconnaissance vocale, la reconnaissance de caractères, ...

#.	**Apprentissage auto-supervisé** : Un énorme dataset pour faire apprendre le réseau.
#.	**Fine tuning** : Spécialise pour une tâche spécifique, pour faire apprendre les dernières couches.

Word encoding
-------------

Première idée
~~~~~~~~~~~~~

| On encode chaque mots ou caractères entre 0 et 1.
| *Difficile de séparer 26 lettres, vraiment dur pour des milliers de mots.*

One-hot encoding (lettres)
~~~~~~~~~~~~~~~~~~~~~~~~~~

| On encode chaque lettre par un vecteur de 26 dimensions avec 0 de partout et 1 à la position de la lettre.

One-hot encoding (mots)
~~~~~~~~~~~~~~~~~~~~~~~

| On fait la même chose mais pour les mots.
| **Problème** : Ca ne garde aucune sémantique.

.. _BIML-WE:

Word embedding
~~~~~~~~~~~~~~

| Transforme les mots en vecteurs de k-dimensions.

.. math::
	h_{(k,1)} = W_{(k,n)}\cdot X_{(n,1)} \\
	h_{i} = \sum_{j=1}^{n}W_{ij}\cdot X_{j}

| **Word2Vec** pour apprendre :math:`W_{(k,n)}` : 

*	**CBOW** : Prédit un mot grâce à la proximité des mots.
*	**Skip-gram** : Prédit les mots voisins grâce à un mot.

| **GloVe** : Utilise les statistiques de co-occurence des mots.

.. admonition:: Propriétés du *Word Embedding*

	*	**Similarité** : Les mots similaires sont proches dans l'espace.
	*	**Translation** : Ex. on a un vecteur de roi vers homme, qui est le même que celui de reine vers femme.

RNN & NLP
---------

| **RNN** : Réseau de neurones récurrents.
| Comme encodeur : intègre une mémoire (*internal state*) qui permet de garder une trace des mots précédents. Comme décodeur : génère un mot à la fois grâce à la mémoire.
| Pour le NLP : l'encodeur construit une représentation pour une phrase/document et construit une représentation pour chaque mot dépendant du contexte ; le décodeur génère du texte.

.. figure:: img/biml-nlpRNN.png
	:scale: 50 %

	Recurrent Neural Network

.. figure:: img/biml-nlpLSTM.png
	:scale: 50 %

	Long Short Term Memory

*(Il présente plusieurs modèles mais bon OSEF...)*

Seq2Seq
-------

.. figure:: img/biml-nlpS2S.png
	:scale: 50 %

	Sequence 2 Sequence model

.. figure:: img/biml-nlpTeacherForcing.png
	:scale: 50 %

	Teacher Forcing

.. figure:: img/biml-nlpAM.png
	:scale: 50 %

	Attention Mechanism

.. figure:: img/biml-nlpAM2.png
	:scale: 50 %

	Attention function

Transformer
-----------

.. figure:: img/biml-nlpSA.png
	:scale: 50 %

	Self-Attention

.. figure:: img/biml-nlpQKV.png
	:scale: 50 %

	Queries, Keys, Values

.. figure:: img/biml-nlpTransformer.png
	:scale: 50 %

	Transformer

.. figure:: img/biml-nlpMH.png
	:scale: 50 %

	Multi-Head Attention

.. figure:: img/biml-nlpTransformerModel.png
	:scale: 50 %

	Transformer Model

.. figure:: img/biml-nlpLearning.png
	:scale: 50 %

	Learning