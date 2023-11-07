.. raw:: html

    <style> .green {color:#60aa00; font-weight:bold; font-size:16px} </style>
	<style> .red {color:#aa0060; font-weight:bold; font-size:16px} </style>

.. role:: green
.. role:: red

=======================
IA - intelligent Agents
=======================
| Dispensé par : *Laëtition Matignon* et *Nadia Kabachi* (2023 - Sept.Nov)

MDP et Planification sous incertitudes
======================================
*Laëtitia Matignon*

Notion d'agent
--------------

| Un agent est une entité autonome évoluant dans un environnement avec des capteurs et des actionneurs. Il prend des décisions pour atteindre son objectif.

.. admonition:: Boucle perception/action

	| L'agent possède une fonction de décision :math:`f_{d}:(O_{n} \rightarrow A)`

	*	:math:`O` : Unité élémentaire de perception *(via des capteurs)*.
	*	:math:`A` : Un ensemble d'actions *(via des actionneurs)*.

| Un agent rationnel doit sélectionner une action qui maximise sa mesure de performance.

.. admonition:: Environnement de la tâche *(PEAS)*

	*	Définir la mesure de performance.
	*	Définir l'environnement.
	*	Définir les capteurs.
	*	Définir les effecteurs.

| L'environnement peut être entièrement ou partiellement observable.
| Il peut être déterministe ou stochastique.
| Il peut être épisodique ou séquentiel.
| Il peut être statique ou dynamique *(un environnement dynamique change pendant la délibération de l'agent)*.
| Il peut être discret ou continu.
| Il peut être mono-agent ou multi-agent.

| Un agent est la combinaison d'une architecture et d'un programme. Il existe 5 types de programmes :

*	**Agents réflexes simples** : Sélection des actions en fonction de la perception courante.
*	**Agents réflexes fondés sur des modèles** : L'agent maintient un état interne qui dépend de la perception courante et de l'historique des perceptions. Il possède un modèle de l'environnement.
*	**Agents fondés sur les buts** : L'agent possède une information sur le but qui décrit les situations désirables. Combinaison de cette information avec l'information sur les résultats des actions possibles afin de choisir l'action qui satisfait le but.
*	**Agents fondés sur l'utilité** : L'agent possède une fonction d'utlité qui mesure le degré de satisfaction associé à l'état. Choisit la meilleure manière de réaliser le but.
*	**Agents évolués capables d'apprentissage** : 

	*	Elément de performance : Décide de l'action en fonction des perceptions.
	*	Critic : Evalue le comportement de l'agent selon une mesure de performance.
	*	Learning element : Utilise l'évaluation du critic pour déterminer comment modifier l'élément de performance.
	*	Problem generator : Suggère des actions d'exploration.

Introduction à la décision séquentielle
---------------------------------------

| Trouver un plan ou une séquence d'actions pour aller d'un état initial à un état but en respectant certains objectifs.
| 2 phases en planification : planification *(calcul d'un plan)* et exécution du plan.

Formalisation mathématique
--------------------------

| On se base sur un environnement stochastique.

Problème : Modèle MDP *(Markov Decision Process)*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. admonition:: Chaîne de Markov

	*	Ensemble fini d'états : :math:`S`.
	*	Fonction de transition : :math:`T:S\times S \rightarrow [0;1]`.

	.. math::
		T(s,s') = P(s_{t+1}=s'|s_{t}=s)

.. admonition:: Processus Décisionnel Markovien (MDP)

	*	Ensemble fini d'états : :math:`S`.
	*	Ensemble fini d'actions : :math:`A`.
	*	Fonction de transition : :math:`T:S\times A \times S \rightarrow [0;1]`.
	*	Fonction de récompense : :math:`R:S\times A \times S \rightarrow \mathbb{R}`.

	.. math::
		T(s,a,s') = P(s_{t+1}=s'|s_{t}=s,a_{t}=a)

.. admonition:: Propriété de Markov

	| Les conséquences d'un action :math:`a_{t}` dans un état :math:`s_{t}` ne dépendent que de l'état courant :math:`s_{t}`.

.. figure:: img/ia-loop.png
	:scale: 50 %

	Boucle perception/action

| Un épisode : :math:`s_{0}, a_{0}, r_{1}, s_{1}, a_{1}, r_{2}, s_{2}, a_{2}, ...`

Solution : Politique
~~~~~~~~~~~~~~~~~~~~

.. admonition:: Politique :math:`\pi`

	| L'agent doit déterminer quelle action faire dans chaque état : politique :math:`\pi:S \rightarrow A` associe une (ou plusieurs) action(s) à exécuter dans chaque état.

| Si le choix de la meilleure décision dépend de l'instant :math:`t` alors la politique est *non-stationnaire* :math:`\pi_{t}`. Sinon elle est *stationnaire* :math:`\forall t, \pi_{t}=\pi`.
| L'**horizon** est le nombre de pas de temps sur lesquels l'agent raisonne pour prendre ses décisions *(peut être fini ou infini)*.

.. note::
	| On se base sur une politique stationnaire et un horizon infini.

Objectif : Politique optimale
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. admonition:: Politique optimale :math:`\pi^{*}`

	| Résoudre un MDP consiste à trouver une politique optimale :math:`\pi^{*}` qui donne pour tout état l'action permettant de maximiser l'espérance de récompenses cumulées.

	.. math::
		G = \sum_{t=0}^{\infty} \gamma^{t}r_{t+1}

| Compromis nécessaire entre récompenses immédiates et futures. Pondération des récompenses selon leur éloignement dans le futur.

.. math::
	G^{\gamma} = \sum_{t=0}^{\infty} \gamma^{t}r_{t+1}

Fonction de valeur
------------------

.. admonition:: Fonction de valeur :math:`V^{\pi}`

	| La fonction de valeur :math:`V^{\pi}(s)` d'un état :math:`s` est l'espérance de récompenses cumulées à partir de :math:`s` en suivant la politique :math:`\pi`.

	.. math::
		V^{\pi}(s) = \mathbb{E}_{\pi}[\sum_{t=0}^{\infty} \gamma^{t}r_{t+1}|s_{0}=s]

| :math:`\pi^{'} \geq \pi` ssi :math:`V_{\pi^{'}}(s) \geq V_{\pi}(s) \forall s \in S`.

.. math::
	V^{*} = V^{\pi^{*}} = \max_{\pi} V^{\pi}

.. admonition:: Equation de Bellman

	.. math::
		V^{\pi}(s) = \sum_{s' \in S} T(s,\pi(s),s')[R(s,\pi(s),s') + \gamma V^{\pi}(s')]

	| Optimalité d'optimalité de Bellman :

	.. math::
		V^{*}(s) = \max_{a \in A} \sum_{s' \in S} T(s,a,s')[R(s,a,s') + \gamma V^{*}(s')]

Résolution d'un MDP
-------------------

.. admonition:: Value Iteration *(Bellman, 1957)*

	#.	Initialisation arbitraire de :math:`V_{0}(s) \forall s \in S`.
	#.	:math:`V_{k+1}(s) = \max_{a \in A} \sum_{s' \in S} T(s,a,s')[R(s,a,s') + \gamma V_{k}(s')]`
	#.	Répète jusqu'à convergence. Critère d'arrêt : :math:`\max_{s \in S} |V_{k+1}(s) - V_{k}(s)| \lt \epsilon`.

| Extraction de la politique optimale : :math:`\pi^{*}(s) = \arg\max_{a \in A} \sum_{s' \in S} T(s,a,s')[R(s,a,s') + \gamma V^{*}(s')]`.

.. admonition:: Policy iteration *(Howard, 1960)*

	*	Evaluation d'un politique :math:`\pi` : calcul de :math:`V^{\pi}`.

	.. math::
		V_{k+1}^{\pi}(s) = \sum_{s' \in S} T(s,\pi(s),s')[R(s,\pi(s),s') + \gamma V_{k}^{\pi}(s')]

	*	Amélioration d'une politique.

	.. math::
		\forall s \in S, \pi^{'}(s) \leftarrow \arg\max_{a \in A} \sum_{s' \in S} T(s,a,s')[R(s,a,s') + \gamma V^{\pi}(s')]

Extensions des MDP
------------------

| Pour un MDP partiellement observable, l'agent n'agit qu'en fonction de son observation immédiate :math:`\pi : S\rightarrow A`.

.. admonition:: Syst§mes Multi-Agent *(SMA)*

	*	:math:`n` nombre de robots.
	*	:math:`s \in S` état joint du SMA.
	*	:math:`a \in A` action jointe.
	*	:math:`T : S\times A \times S \rightarrow [0;1]` fonction de transition des :math:`n` robots d'un état joint :math:`s` à un état joint :math:`s'` en suivant une action jointe :math:`a`.
	*	:math:`R : S \rightarrow \mathbb{R}` fonction de récompense sur l'état joint :math:`s`.

Apprentissage par renforcement
==============================
*Laëtitia Matignon*

| **Apprentissage par renforcement** (AR) : L'apprentissage est basé sur l'interaction avec l'environnement : l'apprenant est actif.

Notions de base
---------------

| Nouvelles hypothèses : :math:`T` et :math:`R` sont inconnues. L'agent doit les apprendre en interagissant avec l'environnement.
| Nous n'avons plus de planification hors-ligne.

| 2 types d'AR :

*	**AR indirect** (model-based) : L'agent apprend :math:`T` et :math:`R` par interactions. Il s'appuie sur cette connaissnace pour calculer une politique optimale avec des méthodes de planifications.
*	**AR direct** (model-free) : Construit une politique optimale en apprenant des fonctions spécifiques mais sans apprentissage direct de :math:`T` et :math:`R`.

AR passif
---------

.. math::
	\forall s \in S, V^{\pi}(s) = \mathbb{E}_{\pi}[\sum_{t=0}^{\infty} \gamma^{t}r_{t+1}|s_{0}=s]

| L'agent réalise plusieurs épisodes en suivant la politique fixée :math:`\pi`.
| Il existe 3 algorithmes pour évaluer :math:`V^{\pi}` à partir des épisodes :

*	**Monte-Carlo Prediction** : La valeur d'un état :math:`s` est la moyenne des récompenses obtenues sur tous les épisodes en partant de :math:`s` et en suivant la politique :math:`\pi`.

	.. admonition:: Avantages

		*	Apprentissage en ligne, sans modèle.
		*	Pas de biais : les valeurs proviennent d'une interaction avec l'environnement.

	.. admonition:: Inconvénients

		*	On doit conserver les épisodes.
		*	Convergence très lente.
		*	Problème pour tout les épisodes de taille infinie.
		*	Forte variance : les valeurs d'un état peuvent être très différentes d'un épisode à l'autre.

*	**Incremental Monte-Carlo Prediction** : On réalise des épisodes complets réalisés dans l'environnement en suivant la politique :math:`\pi`. A chaque fin d'épisode, on met à jour les états visités pendant l'épisode.

	.. math::
		V^{\pi}(s) = V^{\pi}(s) + \alpha (v(s) - V^{\pi}(s))
	
	| Avec :math:`v(s) = r_{1} + \gamma r_{2} + \gamma^{2} r_{3} + ...` et :math:`\alpha \in [0;1]` le pas d'apprentissage.

	.. admonition:: Avantages

		*	Apprentissage en ligne, sans modèle.
		*	Pas de biais : les valeurs proviennent d'une interaction avec l'environnement.
		*	:green:`On doit conserver un seul épisode.`

	.. admonition:: Inconvénients

		*	Convergence très lente.
		*	Problème pour tout les épisodes de taille infinie.
		*	Forte variance : les valeurs d'un état peuvent être très différentes d'un épisode à l'autre.

*	**Temporal Difference Prediction** : On réalise des épisodes complets réalisés dans l'environnement en suivant la politique :math:`\pi`. Après chaque action exécutée par l'agent dans un état :math:`s`, on applique la mise à jour suivante à l'état :math:`s` :

	.. math::
		V^{\pi}(s) = (1 - \alpha) V^{\pi}(s) + \alpha (r + \gamma V^{\pi}(s'))

	.. admonition:: Avantages

		*	Apprentissage en ligne, sans modèle.
		*	:green:`Pas besoin de conserver tout l'épisode, mise à jour à chaque étape.`
		*	:green:`Convergence plus rapide avec le bootstrap.`
		*	:green:`Faible variance avec le bootstrap.`

	.. admonition:: Inconvénients

		*	:red:`Biais : Les valeurs ne sont pas toujours justes car on utilise le bootstrap pour l'échantillon.`

AR actif
--------

| :math:`\pi` n'est plus figée.
| Il évolue un politique :math:`\pi` puis met à jour :math:`V^{\pi}(s)` selon *TD prediction*. Apreès chaque évaluation, il améliore la politique :math:`\pi` suivie.

.. admonition:: Fonction de valeur d'action :math:`Q`

	| :math:`Q:S\times A \rightarrow \mathbb{R}`.
	| :math:`Q(s, a)` est la valeur de l'action :math:`a` dans l'état :math:`s`.
	| :math:`Q^{\pi}(s, a)` évalue le retour espéré lorsque l'on effecture l'action :math:`a` dans l'état :math:`s` puis on suit la politique :math:`\pi` : :math:`Q^{\pi}(s, a) = \mathbb{E}[\sum_{t=0}^{\infty} \gamma^{t}r_{t+1}|\pi, s_{t}=s, a_{t}=a]`.
	| Liens entre :math:`V` et :math:`Q` : :math:`\forall s \in S, V(s) = \max_{a \in A} Q(s, a)`.

Agent glouton
~~~~~~~~~~~~~

| A chaque étape :math:`<s,a,s',r>` : 

#.	L'agent dans :math:`s` suit sa politique :math:`a=\pi(s)`.
#.	Il évalue cette politique avec mise à jour *TD prediction* :

	.. math::
		Q(s,a) \leftarrow (1 - \alpha) Q(s,a) + \alpha (r + \gamma \max_{b \in A} Q(s',b))

#.	Après chaque mise à jour, il améliore sa politique :

	.. math::
		\pi(s) = greedy(Q(s, .)) = \arg\max_{a \in A} Q(s,a)

.. note::
	| Manque d'exploration.

Politique :math:`\epsilon`-greedy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| Explorer avec probabilité :math:`\epsilon` et exploiter avec probabilité :math:`1 - \epsilon`.

.. admonition:: Algorithme du Q-learning

	| Construire une table des Q-valeurs et répéter pour chaque épisode : 

	#.	:math:`s \leftarrow` état initial.
	#.	Répéter pour chaque étape dans l'épisode :

		#.	Choisir :math:`a` selon une stratégie d'exploration.
		#.	Exécuter :math:`a` et observer :math:`r` et :math:`s'`.
		#.	:math:`Q(s,a) \leftarrow (1 - \alpha_{k}) Q(s,a) + \alpha_{k} (r + \gamma \max_{b \in A} Q(s',b))`
		#.	:math:`s \leftarrow s'`

	| La suite :math:`\alpha_{k}(s,a)` doit décroitre à chaque nouvelle visite de :math:`(s,a)`.

Généralisation
--------------

| Problème d'espace de mémoire pour les méthodes tabulaires ; de lenteur d'apprentissage ; et de discétisation.

Fusion d'états
~~~~~~~~~~~~~~

| Si des situations se ressemblent, on considère qu'elles correspondent au même état discret.
| La politique définie sur l'espace des états fusionnés doit permettre à l'agent de prendre une décision markovienne *(qui ne dépend pas de l'état courant)*.

| Discrétisation de l'espace d'états experte, difficile à trouver.

Généralisation
~~~~~~~~~~~~~~

| Le principe est d'utiliser une fonction de Q-valeurs continue plutôt qu'une table.

Approximate Q-learning
~~~~~~~~~~~~~~~~~~~~~~

| La fonction de valeur :math:`Q` est approximée par une fonction linéaire :

.. math::
	Q_{w}(s,a) = \sum_{i=1}^{n} w_{i} f_{i}(s,a)

*	:math:`n` features ou fonctions caractéristiques :math:`f_{i}:S\times A \rightarrow \mathbb{R}` choisies.
*	:math:`n` paramètres/poids :math:`w_{i}` appris pour avoir la meilleure approximation de la fonction :math:`Q`.

.. note::
	| On stocke :math:`n` poids au lieu des Q-valeurs (:math:`n \lt\lt |S| \times |A|`).

.. figure:: img/ia-algoApproxQ.png
	:scale: 50 %

	Algorithme Approximate Q-learning

Apprentissage profond par renforcement *(Deep RL)*
==================================================
*Laëtitia Matignon*

Deep Q Learning
---------------

QLearning avec NN naïf
~~~~~~~~~~~~~~~~~~~~~~

| Approximation non-linéaire de la Q fonction :math:`Q_{\omega}` avec :math:`\omega` les poids d'un réseau de neurones.

*	Action **Value** Approximation : :math:`Q_{\omega} : S \times A \rightarrow \mathbb{R}`.
*	Action **Vector** Approximation : :math:`Q_{\omega} : S \rightarrow \mathbb{R}^{A}`. Autant de sortie que d'actions.

| On veut minimiser l'erreur sur les Q-valeurs. A chaque interaction :math:`(s,a,s',r)` : 

#.	Prédiction pour la valeur de :math:`(s,a)` (forward pass) : :math:`\hat{y} = q_{\omega}(s,a)`.
#.	Label/valeur cible de :math:`(s,a)` *inconnue* : estimation par amorçage (2nd forward pass) : :math:`y = r + \gamma \max_{b \in A} q_{\omega}(s',b)`.
#.	Une itération de la descente de gradient :

	#.	Fonction de perte *MST loss* : :math:`J_{\omega} = (y-\hat{y})^{2}`.
	#.	Calcul du gradient de la fonction MSE par rapport à :math:`\omega` : :math:`\nabla_{\omega} J_{\omega} = -2(y-\hat{y})\nabla_{\omega}\hat{y}`.
	#.	Mise à jour des poids selon descente de gradient, :math:`\alpha \in [0;1]` le pas d'apprentissage : :math:`\omega = \omega - \alpha \nabla_{\omega} J_{\omega}`.

Experience Replay
~~~~~~~~~~~~~~~~~

.. admonition:: Replay Buffer

	*	Mémorise les interactions rencontrées en suivant la politique courante.
	*	Tire aléatoirement un mini-batch d'interactions dans le buffer pour la mise à jour des poids du NN.

*	Réduite la corrélation entre interactions successives.
*	Accélère l'apprentissage car mini-batch et chaque interation est potentiellement utilisée plusieurs fois.
*	Réduction de l'oubli : réutilise des interactions rares ou anciennes.

Réseau cible
~~~~~~~~~~~~

| Figer la cible : Découpler les paramètres utilisés pour calculer la cible :math:`\omega^{-}` et ceux mis à jour :math:`\omega` : 

.. math::
	\omega = \omega + \alpha (r + \gamma \max_{b \in A} q_{\omega^{-}}(s',b) - q_{\omega}(s,a))\nabla_{\omega}q_{\omega}(s,a)

Deep Q-Network (DQN)
~~~~~~~~~~~~~~~~~~~~

*	Fonction d'approximation non-linéaire pour fonction Q, avec autant de sorties du NN que d'actions.
*	Apprentissage supervisée avec cible mouvante.
*	Experience replay pour réduire la corrélation entre interactions successives dans un même épisode.
*	Réseau cible pour réduire les corrélations dues à la cible :math:`y` mouvante.

Recherche de politique
----------------------

:math:`V`-based vs :math:`\pi`-based
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| Avantages de :math:`\pi`-based :

*	Simplicité.
*	Pas de stratégies d'exploration/exploitation.
*	Convergence : changement lisse des probabilités d'action.
*	Possibilité d'avoir :math:`A` continu.

| Inconvénients :math:`\pi`-based :

*	Risque de convergence vers un optimum local plutôt que global.
*	Evaluation de la politique inefficace *(variance élevée, convergence lente)*.
*	Pas sample-efficient : on policy, replay-buffer non utilisable.

Formalisation du problème
~~~~~~~~~~~~~~~~~~~~~~~~~

*	:math:`\pi_{\theta}` : politique paramétrique.
*	:math:`\tau_{i}` : une trajectoire *(séquence d'états-actions sur un horizon)*. :math:`H:\tau = s_{0}, a_{0}, s_{1}, ..., s_{H}, a_{H}, s_{H+1}`
*	:math:`R(\tau_{i})` : somme des récompenses obtenues sur la trajectoire :math:`\tau_{i}`. :math:`R(\tau) = \sum_{t=0}^{\infty} \gamma^{t}r_{t}`
*	**Objectif** : maximiser la fonction objectif.

	.. math::
		J(\theta) = \mathbb{E}_{\tau \sim \pi_{\theta}}[R(\tau)] = \sum_{\tau} P(\tau|\theta) R(\tau)

*	Les actions choisies par la politique :math:`\pi_{\theta}` influencent les récompenses reçues par l'agent.
*	Trouver les paramètres :math:`\theta^{*}` qui maximisent la fonction objectif.

	.. math::
		\theta^{*} = \arg\max_{\theta} J(\theta) = \arg\max_{\theta} \sum_{\tau} P(\tau|\theta) R(\tau)

.. note::
	| :math:`P(\tau|\theta)` est la probabilité de prendre la trajectoire :math:`\tau` en suivant la politique :math:`\pi_{\theta}`.

Recherche stochastique de :math:`\pi`
-------------------------------------

.. admonition:: Algorithme *Hill Climbing*

	#.	Intialiser :math:`\theta` aléatoirement.
	#.	Collecter un épisode avec :math:`\theta`, et enregistre le retour :math:`G`.
	#.	:math:`\theta_{best} \leftarrow \theta`.
	#.	:math:`G_{best} \leftarrow G`.
	#.	Répéter jusqu'à que l'environnement soit résolu :

		#.	Ajouter un peu de bruit aléatoire à :math:`\theta_{best}` pour avoir des nouveaux poids :math:`\theta_{new}`.
		#.	Collecter un épisode avec :math:`\theta_{new}`, et enregistre le retour :math:`G_{new}`.
		#.	Si :math:`G_{new} \gt G_{best}` alors :
			
			#.	:math:`\theta_{best} \leftarrow \theta_{new}`.
			#.	:math:`G_{best} \leftarrow G_{new}`.

Approches par gradient de :math:`\pi`
-------------------------------------

*	**Objectif** : Trouver les paramètres :math:`\theta^{*}` qui maximisent la fonction objectif.

	.. math::
		\theta^{*} = \arg\max_{\theta} J(\theta) = \arg\max_{\theta} \sum_{\tau} P(\tau|\theta) R(\tau)

*	**Moyen** : Amélioration directe de la politique avec remontée de gradient.

	.. math::
		\theta_{k+1} = \theta_{k} + \alpha \nabla_{\theta} J(\theta)

*	**Idée** : Augmenter la probabilité des trajectoires qui ont un retour élevée.

.. note::
	Nécessite de calculer :math:`\nabla_{\theta} J(\theta) \rightarrow` Policy Gradient Theorem.

Policy Gradient Theorem
~~~~~~~~~~~~~~~~~~~~~~~

| Reformule le calcul du gradient sur des probabilités de trajectoires en gradient sur la politique.

.. math::
	\nabla_{\theta} J(\theta) = \mathbb{E}_{\tau}[\nabla_{\theta} \log P(\tau|\theta) R(\tau)]

	| Peut être réécrite :

.. math::
	\nabla_{\theta} J(\theta) = \mathbb{E}_{\tau}[\sum_{t=0}^{H} \nabla_{\theta} \log \pi_{\theta}(a_{t}|s_{t}) R(\tau)]

| Calcul du gradient = calcul de l'espérance : on réalise :math:`m` trajectoires avec un agent qui suit :math:`\pi_{\theta}`.

.. math::
	\nabla_{\theta} J(\theta) = \frac{1}{m} \sum_{i=1}^{m} \sum_{t=1}^{H} \nabla_{\theta} \log \pi_{\theta}(a_{t}^{(i)}|s_{t}^{(i)}) R(\tau^{(i)})

Algorithme REINFORCE
~~~~~~~~~~~~~~~~~~~~

| Application directe du *Policy Gradient Theorem* : estimation du gradient ave :math:`m` trajectoires.

.. admonition:: Algorithme

	#.	Initialiser :math:`\theta` aléatoirement.
	#.	Initailiser :math:`b` : baseline.
	#.	Pour les itération=1,2,.. :

		#.	Collecteur un set de trajectoires suivant la politique courante.
		#.	Pour chaque étape dans chaque trajectoire, calculer :

			#.	Le retour :math:`R_{t} = \sum_{t^{'}=t}^{T-1} \gamma^{t^{'}-t} r_{t^{'}}`.
			#.	L'avantage estimé :math:`\hat{A}_{t} = R_{t} - b(s_{t})`.

		#.	Re-fit la baseline, en minimisant :math:`||b(s_{t}) - R_{t}||^{2}`.
		#.	Mettre à jour la politique.

On-policy vs Off-policy
~~~~~~~~~~~~~~~~~~~~~~~

*	:math:`\pi_{target}` : politique que l'agent essaie d'apprendre (:math:`\pi_{target} \approx \pi^{*}`).
*	:math:`\pi_{behavior}` : politique utilisée pour collecter les trajectoires.

.. admonition:: Off-policy *(Q-learning/DQN)*

	*	:math:`\pi_{target} \neq \pi_{behavior}`.
	*	On peut même avoir :math:`\pi_{behavior}` complètement aléatoire, le Q-learning apprendra une *target policy* optimale.
	*	*Replay buffer*

.. admonition:: On-policy *(REINFORCE)*

	*	:math:`\pi_{target} = \pi_{behavior}`.
	*	*Replay buffer* impossible.

Actor-Critic
~~~~~~~~~~~~

*	**Policy-based** (Actor :math:`\pi`) : Apprend à agir.
*	**Value-based** (Critic :math:`Q, V`) : Apprend à évaluer les valeurs des états/états-actions.
*	**Actor-Critic** : Combine les 2. Ajuste les probabilités des actions comme l'acteur, mais utilise un critic pour évaluer les bonnes et mauvaises actions prises plus rapidement.

.. figure:: img/ia-acAlgo.png
	:scale: 50 %

	Algorithme Actor-Critic vanilla

Approche BDI (Belief Desire Intention)
======================================
*Nadia Kabachi*

| Pourquoi utiliser des systèmes multi-agents *(SMA)* ?

*	Résoudre un problème de manière distribué.
*	Simulation de systèmes complexes.
*	Gérer un maintenir un environnement de travail.

| SMA est un système :math:`<O,E,A>` où :

*	:math:`O` est un ensemble d'objets.
*	:math:`A` est un ensemble d'agents.
*	:math:`O` et :math:`A` sont immergés dans un environnement :math:`E`.

| :math:`SMA = Agents + Environnement + Interactions + Organisations` *(AEIO - Y. Demazeau, 1995)*

Agents
------

.. list-table:: Cognitif vs Réactif
	:widths: 50 50
	:header-rows: 1

	* - Agent cognitif
	  - Agent réactif
	* - Représentation explicite de l'environnement
	  - Pas de représentation explicite
	* - Peut tenir compte de son passé
	  - Pas de mémoire locale
	* - Agents complexes
	  - Fonctionnement stimulus/action
	* - Nombre d'agents réduit
	  - Nombre d'agents élevé
	
.. admonition:: Quelques propriétés

	*	**Agence faible** :

		*	*Autonomie* : Opère sans intervention externe.
		*	*Sociabilité* : Interactions avec d'autres agents ou humains.
		*	*Réactivitié* : Perception de l'environnement et réaction en conséquence.
		*	*Pro-attitude* : Initiative d'actions.
	
	*	**Agence forte** : Agent doté d’un *état mental* :math:`\rightarrow` Connaissances, Croyances, Intentions,  Désirs, Obligations, Engagements..(Emotions) (Agents BDI).
	*	Autres : Mobilité, Dévouement, Rationalité, Adaptabilité, ...

Architectures et fonctionnement des agents
------------------------------------------

*	Les **agents réactifs** : Fonctionnement basé sur une simple correspondance entre les situations et les actions.

	*	Interagissent simplement avec leur environnement plutôt que de se le représenter et de raisonner dessus.
	*	Basés sur des règles de type (situation, action).
	*	Plusieurs comportements peuvent être lancés.
	*	Sélection de comportements non contradictoires.
	* 	...


*	Les **agents logiques** : Fonctionnement basé sur des déductions.

	*	Modèlisation de l'environnement.
	*	Actions.
	*	Règles de comportement.

*	Les **agents BDI** : L’agent décide des actions à entreprendre à partir de ses états internes qui sont exprimés sous la forme de BDI.

	*	*Believes* : Informations (faits) courantes qu’un agent possède à propos de l’environnement.
	*	*Desires* : Buts à réaliser si possible.
	*	*Plans* : connaissances qui déterminent comment certaines séquences de tests et d’actions permettent d’atteindre des buts ou bien réagir à certaines situations. :math:`Plan=(condition d’invocation, condition sur le contexte, plan : when event if condition then action)`
	*	*Intentions* : Plans (et donc but) instanciés choisis pour une (éventuelle) exécution.

	.. admonition:: Algorithme

		| Fonction :math:`agir(p:P):A`
		| Début
		
		#.	:math:`B := réviser\_les\_croyances(B, p)`
		#.	:math:`D := déterminer\_de\_nouveaux_buts(B, D, I)`
		#.	:math:`I := sélectionner\_les\_buts\_à\_tenter(B, D, I)`
		#.	:math:`renvoyer(action(un\_plan(I)))`
	
		| Fin

*	Les **agents ACA** : Agents Conversationnels Animés. Vers la prise en compte des émotions.

	*	Capables d’interactions multimodales avec un usagé.
	*	Dotés d’une apparence effective face à l’usagé.
	*	Nécessite des capacité de raisonnement et des interaction multi-modale anthropocentrées.
	*	Vers les agents émotionnels : Modélisation interne de l’état émotionnel d’un agent ; les agents animés traduisent et montrent leur état émotionnel.

Architecture BDI
----------------

.. figure:: img/ia-bdi.png
	:scale: 50 %

	Architecture BDI

| Différetntes fonctions :

*	:math:`revc : B x P \rightarrow B` est la fonction de révision des croyances de l'agent  lorsqu'il reçoit de nouvelles perceptions sur l’environnement, où P représente l'ensemble des perceptions de l'agent; elle est réalisée par la composante Révision des croyances.
*	:math:`options : D x I \rightarrow I` est la fonction qui représente le processus de décision de l'agent prenant en compte ses désirs et ses intentions courantes; cette fonction est réalisée par la composante Processus de décision.
*	:math:`des : B x D x I \rightarrow D` est la fonction qui peut changer les désirs d'un agent si ses croyances ou intentions changent, pour maintenir la consistance des désirs de l'agent; cette fonction est également réalisée par la composante Processus de décision
*	:math:`filtre : B x D x I \rightarrow I` est la fonction la plus importante car elle décide des intentions à poursuivre; elle est réalisée par la composante Filtre.
*	:math:`plan : B x I \rightarrow PE` est la fonction qui transforme les plans partiels en plans exécutables, PE étant l'ensemble de ces plans ; elle peut utiliser, par exemple, une bibliothèque de plans, représentée par le module LibP dans la figure.
*	:math:`Un plan` est une séquence d'actions à exécuter dans le temps

.. admonition:: Algorithme de contrôle d'agent BDI

	| Soient B0, D0 et I0 les croyances, désirs et intentions initiales de l'agent.

	#.	:math:`B := B0`
	#.	:math:`D := D0`
	#.	:math:`I := I0`
	#.	Répéter jusqu'à ce que l'agent soit arrêté :

		#.	Obtenir nouvelle perception :math:`p`
		#.	:math:`B := revc(B, P)`
		#.	:math:`I := options(D, I)`
		#.	:math:`D := des(B, D, I)`
		#.	:math:`I := filtre(B, D, I)`
		#.	:math:`PE := plan(B, I)`
		#.	:math:`executer(PE)`

Stratégies d'obligation :

*	**Obligation aveugle** : Un agent suivant cette stratégie va maintenir ses intentions jusqu'à ce qu'elles soient réalisées, plus précisément jusqu'à ce qu'il croie qu'elles sont réalisées.
*	**Obligation limitée** : Cette stratégie dit que l'agent va maintenir ses intentions ou bien jusqu'à ce qu’elles soient réalisées ou bien jusqu'à ce qu’il croie qu’elles ne sont plus  réalisables.
*	**Obligation ouverte** : Un agent ayant une stratégie d'obligation ouverte maintient ses intentions tant que ces intentions sont aussi ses désirs; une fois que l'agent a conclu que ses intentions ne sont plus réalisables, il ne les considère plus parmi ses désirs.