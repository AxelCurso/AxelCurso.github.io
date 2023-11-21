.. raw:: html

    <style> .green {color:#60aa00; font-weight:bold; font-size:16px} </style>
	<style> .red {color:#aa0060; font-weight:bold; font-size:16px} </style>

.. role:: green
.. role:: red

=======================
DV - Data Visualization
=======================
| Dispensé par : *Aurélien Tabard* (2023 - Nov.Jan)

Introduction à la visualisation de données
==========================================

Pourquoi visualiser ?
---------------------

| Il y a une explosion de la quantité de données.
| Le défi est de transformer les données en connaissance pour qu'elles deviennent utiles.

+------------------------------------------------------+------------------------------------------------------------------------------------+
| Ordinateur plus efficace                             | Humain plus efficace                                                               |
+======================================================+====================================================================================+
| Question bien définie, sur les données connues       | Quand les questions ne sont pas bien définies                                      |
|                                                      |                                                                                    |
| * Quel est le taux de chômage ?                      | * Quelle combinaison de gènes peut être associée à un cancer ?                     |
| * Quel gène mute fréquemment ?                       |                                                                                    |
+------------------------------------------------------+------------------------------------------------------------------------------------+
| Décision doivent être faites en un mimum de temps    | Quand les résultats peuvent donner lieu à plusieurs interprétations                |
|                                                      |                                                                                    |
| * High frequency trading                             | * Quelle est la relation entre l'emploi et la ploitique industrielle du pays ?     |
| * Détection de défaut sur une chaîne    d'assemblage |                                                                                    |
+------------------------------------------------------+------------------------------------------------------------------------------------+

| Nous n'utilisons pas que l'analyse de données puisque pour plusieurs données différentes on peut avoir les mêmes statistiques. `(i.e. Anscombe quartet) <https://en.wikipedia.org/wiki/Anscombe%27s_quartet>`__

| Les 3 raisons de la visualisation :

#.	Enregistrer de l'information.

	*	Plan, photo

#.	Faciliter le raisonnemennt sur de l'information.

	*	Analyser et calculer
	*	Raisonner sur les données
	*	Feedback et interaction

#.	Transmettre de l'information.

	*	Partager et persuader
	*	Collaborer et itérer
	*	Mettre en avant un aspect des données

Qu'est-ce que la visualisation ?
--------------------------------

| Les différents types de visualisation :

*	Infographics
*	Storytelling
*	Cartographie
*	Visualisation scientifique
*	Visualisation d'information
*	Visual analytics

.. admonition:: Définition *(Card, Mackinla, & Shneidermann - 1999)*

	| L'utilisation de représentation visuelles, interactives et informatique de données abstraites pour amplifier la cognition.

Type de données
---------------

| On doit connaître :

*	Les propriétés des données
*	Les méta-données associées
*	Ce que les gens veulent tirer des données

| Les types de jeux de données :

*	Tableaux
*	Arbres
*	Graphes
*	Données spatiales (geometry)
*	Fields (continuous)
*	Tables multidimensionnelles

.. admonition:: Quelques définitions

	*	**Eléments** : Entité individuelle, discrète.
	*	**Attributs** : Propriété mesurée ou observée.
	*	**Lien** : Relation entre deux éléments.
	*	**Position** : Données spatiales (en 2D ou 3D).
	*	**Grille** : Stratégie d'échantillonnage pour données continues.

| Les types d'échelles :

*	**Nominale** : Catégoriel (Opérations : :math:`=, \neq`)
*	**Ordinale** : Ordonnée (Opérations : :math:`=, \neq, <, >`)
*	**Intervalle** : Zéro arbitraire (Opérations : :math:`=, \neq, <, >, +, -`)
*	**Ratio** : Zéro fixé (Opérations : :math:`=, \neq, <, >, +, -, \times, \div`)

| **Modèle de données** : description de bas niveau *(i.e. flottants)*
| **Modèle conceptuel** : construction mentale *(i.e. température)*

Variables graphiques
--------------------

| Marques simples :

*	Points
*	Lignes
*	Surface

| Canaux visuels :

*	Position
*	Couleur
*	Forme
*	Angle
*	Taille
*	Aire
*	Volume

Mapping + visualisation pipeline
--------------------------------

| Le travail de mapping consiste à mapper des données à des marques graphiques et propriétés.
| Ensuite rajouter de l'interaction pour naviguer dans et manipuler les données.

.. figure:: img/dv-humanPercept.png
	:scale: 50 %

	Efficacité de la perception humaine

.. figure:: img/dv-channelEff.png
	:scale: 50 %

	Efficacité des canaux visuels

.. figure:: img/dv-channelErr.png
	:scale: 50 %

	Erreurs des canaux visuels

.. figure:: img/dv-hi.png
	:scale: 50 %

	Intéraction humaine

Visualiser le temps
===================

.. admonition:: Modèle de temps de Aigner

	*	**Scale** : Ordinal, discrete, continuous
	*	**Scope** : Point-based, interval-based
	*	**Arrangement** : Linear, cyclic
	*	**Viewpoint** : Ordered, branching, multiple perspectives

| Les différentes tâches :

#.	Existence d'un élément de donée.
#.	Localisation temporelle
#.	Interval temporel
#.	Texture temporelle (i.e. fréquence)

| On peut faire des opérations entre les séquences temporelles : égalité ; avant/après ; touche ; chevauche ; pendant ; démarre ; termine.

.. note::
	| Faire attention aux échelles (i.e. logarithmique, linéaire).

