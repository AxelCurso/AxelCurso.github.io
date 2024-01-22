.. raw:: html

    <style> .green {color:#60aa00; font-weight:bold; font-size:16px} </style>
	<style> .red {color:#aa0060; font-weight:bold; font-size:16px} </style>

.. role:: green
.. role:: red

====================================================================
AI4IoTR - Artifical Intelligence for Internet of Things and Robotics
====================================================================
| Dispensé par : *Lionel Médini* et *Laeticia Matignon* (2023 - Nov.Jan)

IoT & IA
========
| *Lionel Médini*

IoT, késako ?
-------------

.. admonition:: Définition **IoT**

	| L’**internet des objets** est un ensemble d’objets connectés et de technologies de réseaux qui, à l’exclusion des stations de travail, des tablettes, des téléphones portables et des smartphones, se conjuguent en associant :
	
	*	des objets physiques qui possèdent des capteurs connectés, éventuellement dotés de capacités de calcul et qui sont en mesure d’interagir avec leur environnement ;
	*	des réseaux de communication numériques filaires ou non filaires qui permettent de communiquer les données issues de ces objets ;
	*	des espaces de stockage distants pour les données recueillies ;
	*	des applications de traitement des données qui engagent des processus décisionnels à même de rétroagir sur des objets physiques inanimés ou vivants.

.. admonition:: Quelques définitions

	*	**Système observé** : Any real world entity from which a property is measured.
	*	**Grandeur physique** : An aspect of a feature of interest that can be measured and is intrinsic to and cannot exist without the feature.
	*	**Phénomène physique** : In scientific usage, a phenomenon is any event that is observable, including the use of instrumentation to observe, record, or compile data. Especially in physics, the study of a phenomenon may be described as measurements related to matter, energy, or time.
	*	**Observation** : Act of carrying out an (Observation) Procedure to estimate or calculate a value of a property of a FeatureOfInterest.
	*	**Action** : Carries out an (Actuation) Procedure to change the state of the world.

| On utilise des capteurs et actionneurs pour interagir avec le monde.
| Un **Système Cyber-Physique** (CPS) interagit avec son environnement dans lequel il prend des données, les traite et au travers d’une boucle de rétroaction, contrôle ou influence le processus auquel il est associé.
| Un **jumeau virtuel** (Digital Twin, DT) est un modèle virtuel pour représenter l'objet physique. Sert à lancer des simulations ou étudier des erreurs de performances. On peut mettre dans l'objet physique ce que nous avons appris.

| 2 typologies d'objets :

*	Objets **chipless** : Reconnus à l'aide de tag RFID, QR codes, analyse d'image, ... Modèle de comportement déporté.
*	Objets **smart** : Communicants et/ou intelligents. Modèle de comportement (partiellement) embarqué. Intégrés à un ensemble plus vaste.

| Un écosystème IoT d'objets dans la vie de tous les jours :

*	Quatified self
*	E-santé, médecine préventive, confort
*	Maison connectée
*	Animaux de compagnie, plantes
*	Jouets, loisirs, ...
*	Le coin des geeks/projets open-source
*	...

| De nombreux domaines applicatifs :

*	Industrie
*	E-commerce
*	Agriculture
*	Transport
*	Santé
*	Energie
*	Smart city/smart building

.. admonition:: Différents modèles d'IoT

	*	**Embarqué** sur l'objet
	*	**Edge/Fog** : intelligence répartie
	*	**Cloud** : intelligence déportée

IoT & IA
--------

| **Intelligence ambiante** consiste en essayant de rendre invisible l'interface entre l'homme et la machine.
| Par **smart-** on entend un avancement technologique, une conscience environnementale et de l'interactivité.
| Le but du **machine learning** est de prédire l'évolution d'un paramètre, ou la réponse à une question.
| L'**intelligence distribuée** est le fait de contrôler un grand nombre d'objets interconnectés.

IoT & Ethique 
-------------

#.	Action humaine et contrôle humain

	*	Droits fondamentaux
	*	Action humaine
	*	Contrôle humain

#.	Robustesse technique et fiabilité

	*	Prévention de toute atteinte aux données ou aux services dans le monde *cyber* :math:`\rightarrow` IA.
	*	Prévention de toute atteinte aux humains et à l’environnement *physique* :math:`\rightarrow` IoT.

#.	Respect de la vie privée et gouvernance des données

	*	Respect de la vie privée et protection des données
	*	Qualité et intégrité des données
	*	Accès aux données

#.	Transparence

	*	Traçabilité
	*	Explicabilité
	*	Communication

#.	Diversité, non-discrimination et équité

	*	Lutte contre les biais
	*	Accessibilité
	*	Conception universelle
	*	Intégration des parties prenantes

#.	Bien-être sociétal et environnemental

	*	IA durable et respectueuse de l’environnement
	*	Incidences sociales
	*	Société et démocratie

#.	Responsabilité

	*	Auditabilité
	*	Réduction au minimum et documentation des incidences négatives
	*	Arbitrages
	*	Recours

Tendances et défis
------------------

| De nouvelles applications et défis :

*	Miniaturisation et passage à l'échelle
*	Communication : 5g ?
*	Interface Humain-Objet (IHO)

| Vers le **Web des Objets** (WoT) : standardisation des protocoles et interfaces, découvrabilité des objets, coopération entre objets hétérogènes.

Objets communicants
===================
| *Lionel Médini*

| Le but est de se placer dans une démarche de conception au niveau applicatif et de comprendre les différences avec une démarche de conception logicielle.

Anatomie d'un objet communicant
-------------------------------


Quelle démarche de conception ?
-------------------------------


Analyse des besoins
-------------------


Processus de développement
--------------------------


Validation
----------
