===========================================
AIC - Artificial Intelligence and Cognition
===========================================
| Dispensé par : *Marie Lfevre* et *Olivier Georgeon* (2023 - Sept.Nov)

IA et Cognition
===============
Marie Lefevre

CM1 - IA Cognition
------------------

Qu'est-ce que l'IA ?
~~~~~~~~~~~~~~~~~~~~

.. admonition:: Une définition (pas la seule)

	**L’Intelligence Artificielle** : Doter une machine (ordinateur, robot, dispositif informatique...) de capacités ⟪dites intelligentes⟫, en mimant / s’inspirant des humains ou plus généralement de la nature.

.. figure:: img/aic-approches.png
	:width: 80 %

	Approches de l'IA

*	**IA forte** : La machine développe sa propre intelligence (ses propres capacités cognitives).
*	**IA faible** : La machine exécute un modèle d’une forme d’intelligence (inspiré d’une intelligence naturelle).
*	**IA générale** : L’intelligence n’est pas spécifique à un(e) (type de) tâche donné(e).

| Congrès de Darmouth (USA - 1956) : Définit le périmètre d'investigation de l'IA.

| Quelques dates:

*	1950 : Test de turing *(Test permettant de déterminer si une intelligence artificielle est similaire ou impossible à distinguer d’une intelligence humaine. Aujourd’hui, le programme ALICE est sans doute la référence dans ce domaine, mais aucun logiciel n’a pour l’instant passé le test.)*
*	1951 : Jeux de dames *(Premier logiciel fonctionnel démontrant une intelligence artificielle. Un programme permettant de jouer aux échecs a aussi été conçu durant cette période, mais la machine était trop lente et le jeu se limitait à un échec et mat en 2 coups.)*
*	1956 : Logic Theorist *(Programme informatique conçu pour reproduire les compétences de résolution de problèmes d’un être humain et est considéré comme le premier programme d'intelligence artificielle. Il a été capable de prouver 38 des 52 théorèmes des Principia Mathematica.)*
*	1956 : Satificing *(Principe du seuil de satisfaction de l’individu : l’homme est incapable de maximiser ou optimiser ses ressources, car il peut rarement évaluer toutes les probabilités d’une situation avec précision.)*
*	1958 : LISP
*	1963 : ANALOGY
*	1968 : SHRDLU
*	1972 : Prolog
*	1983 : SOAR *(State Operator and Result ou architecture cognitive)*
*	1989 : Smart Truck
*	1991 : DART
*	1997 : Deep Blue

| Aujourd'hui :

*	**Biais des données** : Diversification et représentativité des données ; manque de ⟪bon sens⟫, dérapage des IA (Étique) ; pistes : auto-génération de données / simulation.
*	**Apprentissage en continu /(Internet /corpus)** : Mise en situation / expérience / appropriation ? ; transfert d’Apprentissage (Transfer Learning) ; généralisation et adaptation.
*	**Boite noire : non intelligibilité** : Pouvoir explicatif ; contrôlabilité , Acceptabilité;

Cognition
~~~~~~~~~

| Regarder ce qu'il se passe dans le/notre/un monde.
| La **cognition** signifie *savoir*, *connaitre*. Réfère à la capacité de raisonner, percevoir, décider et résoudre des problèmes.
| Les sciences cognitives étudient la façon dont un système construit des représentations et les utilise rationnellement pour raisonner, faire des inférences.

.. admonition:: Deux types de systèmes capables de réaliser des processus cognitifs

	*	Les **systèmes naturels** : un neurone, un réseau de neurones, un cerveau (humain ou animal), un groupe d'individus (poissons, fourmis), etc. :math:`\rightarrow` approches bio-inspirées.
	*	Les **systèmes artificiels** : réseau de neurones artificiels, système expert, etc.

CM2 - Approches cognitivistes
-----------------------------

Processus cognitif
~~~~~~~~~~~~~~~~~~

| La **cognition** est un processus par lequel un organisme acquiert de la consciencees des évènements et objets de son environnement.
| Les **processus cognitifs** sont les différents modes à travers lesquels un système traite l'information en y répondant par une action. Il est analysé selon le mode de traitement et le niveau d'élaboration.
| Le **traitement de l’information** se définit comme étant le processus par lequel l’information perçue est analysée et intégrée dans la structure de connaissances de la personne / l’agent.

Cybernétique
~~~~~~~~~~~~

.. admonition:: Quelques défintions

	*	The science of control and communication.
	*	The art of steersmanship *(l’art du pilotage d'une machine par rétroaction)*.
	*	Cybernetics is the study of systems and processes that interact with themselves and produce themselves from themselves.

| La **closed-loop control** est un système de contrôle qui utilise la rétroaction d'un système pour contrôler le comportement d'un système et provoque un changement dans son environnement.

General Problem Solver (GPS)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| *(Simon, Shaw et Newell - 1957)*
| N'importe quel problème formalisé peut en principe être résolu par GPS.
| Sépare sa base de données (faits) de sa stratégie de résolution.
| GPS exploite les heuristiques par une ⟪confrontation moyens/fins⟫ (means-ends analysis).
| Pour les problèmes plus réalistes il est confronté à l'explosion combinatoire.
| Le paradigme GPS a évolué vers l'architecture SOAR.

.. figure:: img/aic-gps.png
	:scale: 50 %

	GPS : a means-ends search process

.. admonition:: Modélisation du problème

	*	Décrire ce qu’est un **état du problème**.
	*	Décrire **l’état initial**.
	*	Définir les **opérateurs** permettant de passer d’un état à un autre.
	*	Disposer d’un test permettant de savoir si on a trouvé un **état but final**.
	*	Construire l’espace des états : L’ensemble des états atteignables depuis l’état initial.
	*	Construire un chemin de l’état initial à l’état final : Une séquence d’états dans l’espace des états.
	*	Disposer d’une fonction de coût sur le chemin : Cette fonction associe un coût au chemin (coût calculé comme la somme des coûts individuels des actions le long du chemin).

Physical Symbol System
~~~~~~~~~~~~~~~~~~~~~~

| *(Newell et Simon - 1975)*
| Les symboles sont des entités abstraites qui peuvent être instanciées.
| Un système symbolique physique a :

*	Une **mémoire** : Pour contenir les informations symboliques.
*	Des **symboles** : Pour fournir un modèle pour faire correspondre ou indexer d'autres symboles.
*	Des **interprétations** : Pour permettre aux symboles de spécifier les opérations.
*	Des capacités de composition, d’interprétabilité, de mémoire suffisante.

.. figure:: img/aic-pss.png
	:width: 80 %

	Physical Symbol System

| Principes sous-jacents :

*	**Principe de rationalité** (Newell 82) : si un agent sait qu'une de ses actions conduira à l'un de ces buts, alors l'agent sélectionnera cette action.
*	**Analyse rationnelle** (Anderson 89) : le système cognitif optimise l'adaptation du comportement de l'organisme.
*	**Théorie unifiée de la cognition** (Newell 90) : nécessité d'un ensemble d'hypothèses générales pour les modèles cognitifs qui tiennent compte de toute la cognition *(SOAR)*.
*	Un système de connaissances : peut apporter toutes ses connaissances à chaque problème :

	*	Connaissance parfaite > utilisation complète des connaissances
	*	Les humains n'en sont pas encore là !

Systèmes cognitivistes
~~~~~~~~~~~~~~~~~~~~~~

.. admonition:: Problèmes

	*	La représentation est dépendante du programmeur : Biaise le système.
	*	Fosser sémantique : Symbol Grounding problem ; problème d'enracinement des symboles.

| Combler le fossé sémantique :

*	Apprentissage automatique
*	Modélisation probabiliste
*	Meilleurs modèles
*	Meilleures logiques
*	... bref, en améliorant tout ...

| Il reste le **frame problem** *(McCarty et Hayes - 1969)* : En utilisant la logique mathématique, comment est-il possible d'écrire des formules qui décrivent les effets des actions sans avoir à écrire un grand nombre de formules d'accompagnement qui décrivent les non-effets banals et évidents de ces actions ?

CM3 - Approches émergeantes
---------------------------

| La **cognition** est le processus par lequel un système autonome devient viable et efficace dans son environnement par le biais de processus d'**auto-organisation**.

Co-détermination
~~~~~~~~~~~~~~~~

| Le processus cognitif détermine ce qui est réel ou significatif pour l'agent.
| Le système construit sa réalité. La perception fournit des données sensotielles pour permettre une action efficace, mais toujours en conséquence des actions du système.
| La cognition et la perception dépendent fonctionnellement de la richesse de l'interface d'actions.

Cognition & perception
~~~~~~~~~~~~~~~~~~~~~~

| La cognition est le complément de la perception : la perception traite de l'immédiat ; la cognition traite des délais plus longs.
| Le point de départ de l'intelligence est d'agir efficacement, d'anticiper la nécessité d'agir et de faire évoluer ses possibilités d'action.

Auto-organisation
~~~~~~~~~~~~~~~~~

| La structure du monde provient uniquement des interactions entre les composants de niveau inférieur du système.
| Les règles spécifiant les interactions entre les composants du système ne sont exécutées qu'à l'aide d'informations locales, sans référence à une représentation globale du système.

*	Structures collectives décrites par 1 (ou +) variable collective :math:`X_{t}`.

	.. math::
		X_{t+1} = f(X_{t})

	| :math:`f` est une fonction non-linéaire.

*	:math:`X_{t}` : caractérise les relations spatio-temporelles entre composants. *Indicateur macroscopique de coordination.*
*	**Variabilité des comportements micro** : Reflète des fluctuations au niveau macro de la variable collective.
*	**Perturbation de la structure collective** : Fluctuations de la variable collective.

.. admonition:: Stabilité, Equilibre, Transition de phase

	*	Si :math:`X_{t} = k`, k étant une constante : **état d'équilibre**.
	*	2 états d'équilibre :

		*	**Attracteur** : Etat dans lequel converge le système quelque soit les conditions de départ.
		*	**Répulsif** : Etat dans lequel le système ne peut pas se maintenir.

	*	**Transition de phase** : Passage d'un état stable à un autre sous la variation d'un paramètre de contrôle ou sous l'influence des fluctuations inhérentes du système.

Emergence
~~~~~~~~~

| L'**émergence** est un processus par lequel un système d'éléments en interaction acquiert un modèle et une structure qualitativement nouveaux qui ne peuvent être compris simplement comme la superposition des contributions individuelles.

Système connexionniste
~~~~~~~~~~~~~~~~~~~~~~

.. admonition:: Définition

	| Le **connexionnisme** modèlise les phénomènes mentaux ou comportementaux comme des processus émergents des réseaux d'unités simples interconnectées.

| Les phénomènes mentaux peuvent être décrits à l'aide de réseaux d'unités simples interconnectées.
| Traitement parallèle de l'information. Modèle d'activation distribué non symbolique.
| Chaque état mental peut être représenté comme un vecteur à n dimensions représentant les valeurs d'activation des unités neuronales. Le réseau peut apprendre en modifiant les poids des connexions entre ses unités.

Système dynamique
~~~~~~~~~~~~~~~~~

.. admonition:: Définition

	| Un **système dynamique** est un système dissipatif ouvert, non-linéaire et non-équilibré.

*	**Système** : Un grand nombre de composants en interaction et un grand nombre de degrés de liberté.
*	**Dissipatif** : Energie diffuse (i.e. l'énergie diminue au cours du temps).
*	**Non-linéaire** : La dissipation d'énergie n'est pas uniforme.
*	**Non-équilibré** : Incapable de maintenir la structure sans sources externes d'énergie, matériel, information *(donc ouvert)*.

Enaction
~~~~~~~~

.. admonition:: Définition

	| L'**énaction** est une approche de la cognition qui met l'accent sur la manière dont les organismes et esprits humains s'organisent eux-mêmes en interaction avec l'environnement.

| 5 éléments cléfs : 

*	**Autonomie** : Auto-entretien du système, non contrôlé pas des entités extérieures.
*	**Incarnation** : Existe en tant qu'entité physique, interargit directement avec son environnement.
*	**Emergence** : Le comportement cognitif découle d'un jeu dynamique entre les composants.
*	**Expérience** : Histoire de l'interactiona vec le monde.
*	**Création de sens** : La connaissance est générée par le système lui-même, acquisistion autogénique profressive des capacités anticipatoires.

| Le sens peut émerger d'une expérienc consensuelle partagée médiée par l'interaction.

CM4 - Cognition & Perception
----------------------------

| La cognition dans l'approche **cognitiviste** n'a pas besoin d'incarnation.
| La cognition dans l'approche **enactive** est incarnée.

Ancrage symbolique
~~~~~~~~~~~~~~~~~~

| Les symboles ne sont pas liés à l'expérimentation du monde physique : question de *sens*.
| Reprénsetation définie par le concepteur, non contruite par le système lui-même : question d'*embodiment*.

.. admonition:: Paradoxe de Moravec *(1988)*

	| Le plus difficile en robotique est souvent ce qui est le plus facile pour l'homme.
	| Le raisonnement de haut niveau est beaucoup plus facile à reproduire et simuler par un programme informatique que les aptitudes sensorimotrices humaines.

Corps dans la cognition *(dans la création du sens)*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| La cognition incarnée en dépend et repose sur 3 hypothèses :

*	**Hypothèse de conceptualisation** : Les caractéristiques du corps d'un agent déterminent les concepts qu'il peut acquérir. Le corps conditionne et limite donc la cognition.
*	**Hypothèse de constitution** : Le corps est lui-même une partie intégrante de la cognition.
*	**Hypothèse de remplacement** : Le corps d'un agent en interaction en temps réel avec son environnement remplace le besoin de processus de représentation via des associations *perception/action* basées sur des systèmes dynamiques. Le corps agit comme un régulateur de l'activité cognitive.

.. admonition:: Définition

	| L'**affordance** est la capacité d'un objet ou d'un système à évoquer sa fonction.

Biais cognitifs
~~~~~~~~~~~~~~~

.. admonition:: Définition

	| Un **biais cognitif** est une déviation dans le traitement cognitif d'une information.

| Comment les expliquer ? (Hypothèses)

*	La rationalité limitée de l'individu.
*	Se donner des repères dans la société et justifier nos prises de décisions.

| Le plus connu est le **biais de confirmation** : Nous pousse à privilégier tous les arguments qui iraient dans notre sens et à rejeter ceux qui tendent à invalider nos hypothèses.
| Il y a aussi le **biais de disponibilité** qui fait qu'on se contente des informations disponibles immédiatement. Ou encore la **pensée de groupe** qui fait que l'on se fait *convaincre* par la pensée majoritaire.

| Différents biais cognitifs :

*	**Biais sensori-moteurs** : Relatifs aux processus sensori-moteurs, on parle plutôt d'*illusions*.
*	**Biais attentionnels** : Avoir ses perceptions influencées par ses propres centres d'intérêts.
*	**Biais mnésique** :

	*	*Effet de récence* : Mieux se souvenir des dernières informations auxquelles on a été confronté.
	*	*Effet de simple exposition* : Avoir préalablement été exposé à quelqu'un ou à une situation le/la rend plus positive.
	*	*Effet de primauté* : Mieux se souvenir des premiers éléments d'une liste mémoréisée.
	*	...

*	**Biais de jugement** :

	*	*Biais de confirmation*.
	*	*Biais de normalimité* : Tendance à penser que tout ca se passer comme d'habitude.
	*	*Biais de présentéisme* : Privilégier les facteurs présents est plus économique cognitivement à modéliser que les facteurs absents.
	*	*Effet Stroop* : Incapacité d'ignore une information non pertinente.
	*	...

*	**Biais de raisonnement** : 

	*	*Biais de confirmation d'hypothèse* : Préférer les éléments qui confirment plutôt que ceux qui infirment une hypothèse.
	*	*Biais de représentativité* : Considérer un ou certains éléments comme représentatifs d'une population.
	*	*Biais de disponibilité* : Ne pas chercher d'autres informations que celles immédiatement disponibles.
	*	*Effet rebond* : Une pensée que l'on cherche à inhiber devient plus saillante.
	*	*Perception sélective* : Interpréter des manière sélective des infromations en fonction de sa propre expérience.
	*	...

Défis de l'IA
~~~~~~~~~~~~~

| 4 questions fondamentales :

*	Problème de **catégorisation** et d'**abstraction** de l'information : Comment structurer les informations que l'agent reçoit du monde ?
*	Problème d'**ancrage symbolique - embodiment** : Comment lier au monde cette infromation structurée, ou, comment construire le *sens* pour l'agent ?
*	Problème de la **socialisation** et du **partage de la culture** : Comment synchroniser ce sens avec celui que perçoivent et élaborent les autres agents ?
*	Problème d'**autonomie** et **pro-activité** : Comment faire en sorte que *(de façon autonome)* l'agent agisse au lieu de ne rien faire *(sauf si cela a du sens : donner du sens à son action ?)* ?

Ateliers
--------

Chinese Room
~~~~~~~~~~~~
| *BERTOLONE--LOPEZ-SERRANO, MAHAMADOU KONA, NAOUZ et SAIDOUNI*

| Expérience posant la question de savoir si un programme informatique, aussi complexe soit-il, peut-il donner un esprit à un système ?
| Montrer qu'une IA ne peut être qu'une intelligence faible, plutôt que de posséder d'authentiques états mentaux de conscience et d'intentionnalité.
| Montrer que le test de Turing est insuffisant pour déterminer si une IA possède ou non ces états mentaux.

| La syntaxe se base sur la machine de Turing.
| La syntaxe seule ne permet pas de déterminer le sens. Problème de sémantique *(signification des symboles)*.
| La sémantique dépend de l'observateur.

The Symbol Grounding Problem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
| *CONRAD, DAKHLI, MARTINEZ et SALAZAR*

.. admonition:: Définition

	| Comment faire en sorte que l'interprétation sémantique d'un système de symboles formels soit intrinsèque à ce système, plutôt que d'être parasitée par les significations que nous avons dans notre tête ?
	| Harnad *(1990)*

.. figure:: img/aic-atelierT.png
	:width: 80 %

	Triangle sémiotique (Ogden & Richards, *1923*)

| Un symbole est ancré quand la méthode liant l'objet désigné et son concept est définie.
| Il y a une grande importance de la notion d'intrinsèque.

The Frame Problem
~~~~~~~~~~~~~~~~~
| *BESSY, BOUAMRA et LERAY*

| **On a bosser dessus les gueux**

State Operator and Result
~~~~~~~~~~~~~~~~~~~~~~~~~
| *AZOURI, BOUCHARD, COLIN et DEGUT*

| 1981 - Nouvelle architecture cognitive (par Allen Newell et Paul Rosenbloom et John Laird).
| Objectif : apprendre des connaissances sous formes d'états. Ces connaissances sont ensuite utilisées pour résoudre des problèmes. Nouvelles méthodes pour la perception, mémorisation et décision.

*	Système à base de connaissances - State englobant des données
*	Règles - actions suivants des règles
*	Modularité - Facilité de développement
*	Opérateurs - sur les States
*	Apprentissage continu - Connaissances abondantes et expériences
*	Flexibilité - S'adapte à ses expériences et agit en conséquence

| Essayer de représenter symboliquement la mémoire humaine.

*	Semantic or Declarative Memory (SM) : What things are
*	Procedural Memory (PM) : How to do things
*	Episodic Memory (EM) : What happened when
*	Symbolic Working Memory (SM) : What is being thought about now

.. admonition:: Cycle de traitement du Soar

	#.	Sélection d'un objectif
	#.	Sélection des règles produites
	#.	Application des règles produites
	#.	Mise à jour de la mémoire de travail
	#.	Evaluation des résultats
	#.	Apprentissage et adaptation

| Par rapport à ACT-R :

*	Même structure pour les données
*	Soar a un nombre de buffer variable
*	Nombre de chunks illimités
*	Dit quand il est bloqué
*	Même cycle
*	Soar applique sur plusieurs règles en même temps
*	Episodic Memory

| Common Model of Cognition : Un modèle abstrait d’une architrecutre cognitive semblable à celle de l’humain.

.. admonition:: Avantages

	*	Versatilité
	*	Prise en charge de la perception
	*	Apprentissage par instruction
	*	Mimer le raisonnement humain

| Marge de progession :

*	Amélioration des capacités actuelles
*	Insertion de connaissances innées
*	Auto-entrainement
*	Apprentissage par l'instructions

.. admonition:: Inconvénients

	*	Dense et complexe
	*	Apprentissage limité
	*	Dépend du matériel actuel pour la perception
	*	Modèle complet et long à développer
	*	Problèmes métaphysiques

Métacognition
~~~~~~~~~~~~~
| *BONHOURE, LEFEBVRE, RAVELLA et SOMNY*

.. admonition:: Définition

	*	La **métacognition** est la capacité d'une entité à gérer ses propres processus cognitifs, comme la prise de décision, la résolution de problèmes, l'apprentissage, ou la mémoire. Sert à savoir quel raisonnement choisir.
	*	La **métaconnaissance** est une liste non exhaustives sur les connaissances sur une connaissance.

| On a de la réflexivité sur nos métaconnaissances (métaconnaissance de métaconnaissance de connaissance).
| La metacognition permettrait d'avoir des connaissances sur les classes, amélioration de nos modèles. 
| Sans metacogition, on peut faire des différenciations qui n'ont pas de sens. Alors qu'avec on peut avoir une auto-amélioration de notre base de connaissances. Modèle capable de douter et dire qu'il ne sait pas.
| Il pourrait expliquer pourquoi on arrive à un résultat et avoir des connaissances plus précises sur les méthodes.
| Très utilisé en IA symbolique.

.. admonition:: Piste de recherche : Amorçage de l'IA

	#.	On donne des connaissances à une IA qui produit des métaconnaissances.
	#.	Ces métaconnaissances sont données à une autre IA qui produit des métaconnaissances de métaconnaissances.
	#.	...

Motivation intrinsèque
~~~~~~~~~~~~~~~~~~~~~~
| *MABROUK, NGUYEN, FAUGIER*

| Le but est de permettre à des machines de se développer de manière autonome. Ce base sur l'IA développementale. L'acquisition de nouvelles capacités via des séquences de développement.
| 2 machines : 

*	Machine **M** : prédire les résultats d'actions.
*	Machine **metaM** : prédire les erreurs de M (mesurant l'intérêt des situations)
*	Module additionnel **KGA** : prédit le taux d'erreur moyen de M dans un futur proche.

.. admonition:: Modèle IAC (Intelligent Adaptative Curiosity)

	#.	IAC repose sur une mémoire stockant les expériences sous dorme d'exemplaires vectoriels.
	#.	L'espace sensorimoteur est divisé en régions, chacune ayant ses propres exemplaires exclusifs et un expert associé.
	#.	Les erreurs de prédiction des experts sont stockées et utilisées pour évaluer le potentiel d'apprentissage.
	#.	Le robot sélectionne les actions maximisant le progrès d'apprentissage attendu.

	| Régions :

		*	Un ensemble exclusif d'exemplaires.
		*	Critères de division basés sur le nombre d'exemplaires et minimisation de la variance dans les composants.

	| Experts :

		*	Chaque région est associée à un expert.
		*	Experts conçus sous forme de réseaux neuronaux.
		*	Intégration facile de nouveaux exemplaires pour l'apprentissage.

Robots sociaux
~~~~~~~~~~~~~~
| *BAGNOL, BILLOD, BOURNIER et GEILLON*

.. admonition:: Définition

	*	Un agent incarné et autonome
	*	Des interactions au niveau émotionnel
	*	Des interactions sociales
	*	De l'apprentissage par interaction

| Pour comprendre les signaux humains, il doit comprendre son environnement, faire du traitement naturel du langage (NLP), et de la reconnaissance des expressions faciales et vocales.
| Pour faire du raisonnement il fait preuve d'utilisation de l'intelligence artificielle, interprétation des informations, et de la prise de décisions adaptées.
| Les actions qu'il doit faire sont les interactions physiques, la manipulation d'objets, la capacité motrice et exécuter des tâches.
| Pour intérargir il faut des modèles de communication efficaces et une adaptation du comportement en fonction de la situation.

| Très important de développer des comportements sociaux.
| Une approche robotique développementale peut permettre aux robots d'acquérir des compétences sociales plus complexe (comme l'empathie).
| Des robots moins scénarisés.

.. admonition:: Différentes études empiriques sur la perception sociale humaines

	*	Utilisation d’irm pour voir quelles parties sont stimulées par les intéractions.
	*	Envoie de stimulus au cerveau.

| Etudier un robot dans deux contions : le sujet humain devait regarder deux objets en face du robot. Le robot doit suivre le regard soit à 80% soit à 20% (celui de 20% était moins aimé parce que moins humain)

| Interdisciplinarité avec la partie des sciences sociales et les sciences humaines. Cela permet une grade diversification des types de données et permet d'avoir une compréhension plus générale et en profondeur.

| Critique sur l'aspect éthique. *e.g. le robot AIBO pour les personnes agées isolées.*
| Enjeux sociaux : population vieillissante et avoir une aide physique et psychologique. Pour le moment on accepte seulement le physique.
| Traiter les démences en les stimulant, en communiquant les émotions, réduire l'anxiété et améliorer leurs humeurs.

IA développementale
===================
Olivier Georgeon

CM1
---
Qu'est-ce que l'IA développementale ?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Faire des robots capables d'apprendre comme des bébés.

Des termes voisins :

*	`Motivation intrinsèque <https://ieeexplore.ieee.org/document/4141061>`__ : La conception de systèmes qui sont motivés par des objectifs internes plutôt que par des récompenses externes.
*	`Apprentissage constructiviste <https://www.researchgate.net/publication/233842691_A_New_Constructivist_AI_From_Manual_Methods_to_Self-Constructive_Systems>`__ : Des modèles qui apprennent de manière interactive, en construisant progressivement leur compréhension du monde à partir de l'expérience.
*	`Self-supervised learning <https://ai.meta.com/blog/self-supervised-learning-the-dark-matter-of-intelligence/>`__ : C'est une technique d'apprentissage automatique où un modèle est capable d'apprendre à partir de données non étiquetées en créant ses propres étiquettes à partir de la structure inhérente aux données.
*	`Enactive artificial intelligence <https://www.sciencedirect.com/science/article/pii/S0004370208002105?via%3Dihub>`__ : L'intelligence artificielle énactive s'inspire de la théorie de l'esprit énactif, qui considère l'interaction entre un agent et son environnement comme fondamentale pour la cognition. Dans le contexte de l'IA, cela pourrait se référer à des systèmes qui n'apprennent pas seulement à partir de données statiques, mais qui sont également capables d'interagir dynamiquement avec leur environnement pour acquérir des connaissances.
*	`Self-programming <https://www.sciencedirect.com/science/article/abs/pii/S1389041719304644?via%3Dihub>`__ : La capacité d'un système d'apprentissage automatique à améliorer son propre code ou sa propre structure au fil du temps.

Les vieux rêves de l'IA : Simuler le cerveau d'un enfant. En pensant qu'il y a si peu de méchanismes dans le cerveau d'un enfant que l'on pourrait le simuler [#]_.

Critique de l'IA actuelle
~~~~~~~~~~~~~~~~~~~~~~~~~
*	Pas une question de puissance de calcul : ⟪On peut multiplier la puissance des ordinateurs d'un facteur 1000 ou davantage, rien ne permet de penser qu'il en sera autrement.⟫ [#]_
*	Critique ontologique : 

	.. note::
		**Ontologie** : Partie de la philosophie qui traite de l'être indépendamment de ses déterminations particulières.

	| Opère sur une ontologie prédéfinie : Présupposition des états et des transitions ; très efficace en domaines fermés ; impossible (à priori) de modéliser le monde réel.
	| Pour dépasser cela : IA capable de créer sa propre ontologie ; robots sans modèle du monde coder en dur ; nouveaux algorithmes à partir d'interactions.
*	Critique téléologique :

	.. note::
		**Téléologie** : Étude de la finalité.

	| Atteindre des *états-solution* par exploration d'un espace d'états prédéfinis. Pas de motivation propre.
	| Pour dépasser cela : Ne pas fixer d'objectifs concrets (activité atélique plutôt que télique).

Intelligence artificielle dans un domaine non modélisé a priori
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. topic:: Inverstion du cycle d'interactions

	*	⟪build agents that receive percepts from the environment and perform actions⟫ [#]_
	*	⟪By observing the structure of the changes that occur when they press various buttons and levers⟫ [#]_

	.. figure:: img/aic-dTradModel.png
		:scale: 50 %

		Modèle traditionnel

	.. figure:: img/aic-dInvModel.png
		:scale: 50 %

		Modèle inversé
	
	| La complexité des données d'entrée n'a pas besoin d'être proportionnelle à celle du monde.

.. topic:: Deux hypothèses en concurrence

	*	**Représentationaliste** ou **réaliste** : Les données d'entrée représente des aspects de la réalité.
	*	**Constructiviste** ou **interactionaliste** : Les données d’entrées informent sur les possibilités d’interaction.

CM2
---
Déterminisme et cognition
~~~~~~~~~~~~~~~~~~~~~~~~~

*	**Déterministe** : Chaque état du système découle de manière univoque de l’état précédent.
*	**Prédictibilité** : Possibilité de prévoir l’état futur d’un système.

.. topic:: Sources d'imprédictibilité

	*	Indéterminisme
	*	Incertitude
	*	Complexité
	*	Irréductibilité computationnelle : L’algorithme qui simule le système ne peut pas être court-circuité pour prédire directement le résultat à l’étape n.

Idées clés
~~~~~~~~~~

*	L'humain est peut être déterministe mais néanmoins libre [#]_.
*	Système déterministe peut être imprédictible [#]_. Inutile d’utiliser la Fonction Random() pour générer des comportements imprédictibles.
*	Un système déterministe peut ⟪s’individualiser⟫ [#]_. En fonction des conditions initiales, d'expériences individuelles.
*	Emergence de ⟪macro-propriétés⟫. Souvent non démontrable mais observable depuis un niveau d'observation supérieur

CM3
---
Théorie du développement
~~~~~~~~~~~~~~~~~~~~~~~~
.. figure:: img/aic-dPhyloOnto.png
	:scale: 50 %

	IA développementale :math:`\rightarrow` ontogenèse.

.. admonition:: Définition

	*	**Phylogenèse** : La phylogenèse fait référence à l'évolution d'une intelligence artificielle sur des générations successives.
	*	**Ontologie** : L'ontogenèse désigne le développement et la croissance d'une intelligence artificielle au cours de sa vie ou de son expérience.

| On parle de **couplage structurel** chaque fois que survient une histoire d'interactions récurrentes responsables d’une congruence structurelle entre deux systèmes ou plus [#]_.
| **Théories de Piaget** (apprentissage développementale) : Capacité d’un sujet a développer individuellement sa structure interne et son couplage avec son environnement.
| Dans un système artificiel : différencier *couplage cognitif* et *couplage physique*.
| Construire des connaissances à partir de régularités d'interactions.

Formalisation
~~~~~~~~~~~~~

.. figure:: img/aic-dbu.png
	:scale: 50 %

	Bottom up interaction chaining

| Un syst§me **auto-programmant** est un système capable d'apprendre du code qu'il peut ré-exécuter.

| Pose quelques question :

*	Quel jeu d'instructions ?
*	Quel moteur d'exécution ?
*	Quelle finalité ? Pourquoi apprendre un programme plutôt qu'un autre ?




.. [#] Alan Turing, 1950, Mind, philosophy journal
.. [#] Dessalles, Des intelligences très artificielles, Odile Jacob, 2019, p. 10-11
.. [#] Russell et Norvig, 2003, p.iv
.. [#] O’Regan & Noë 2001, p. 940
.. [#] Théorie évolutionniste de la liberté (Dennett 2003)
.. [#] Computatinal irreductibility (Stehen Wolfram)
.. [#] Autonomie constitutive (Froese & Ziemke 2009)
.. [#] Maturana & Varela,1989, p. 78