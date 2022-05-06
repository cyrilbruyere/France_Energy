**Objectif :**

Au niveau national, l'objectif est de faire une prédiction de la balance énergétique, différence entre la consommation et la production. On s'intéresse particulièrement au risque de balance négative pouvant conduire à une situation de black-out : rupture d'approvisionnement en énergie pour les utilisateurs.

**Méthodologie :**

1. Deux approches pour prédire la balance :
   - Prédiction directe
   - Prédiction indirecte (consolidation de prédictions)
2. Modèles utilisées :
   - SARIMAX
   - Régression linéaire
3. Pas temporels modélisés :
   - 3h : 3 heures
   - D : 24 heures
   - W : semaine
4. Etat des signaux donnés aux modèles :
   - Signaux originaux
   - Signaux filtrés par transformation de Fourier
5. Variables explicatives ajoutées aux modèles :
   - Sinusoïdales de périodes les saisons
   - Données métiers
     - variables utilisées pour la prédiction directe
     - variables utilisées pour la prédiction de la consommatioin
     - principes de construction pour les variables utilisées pour les productions 

**Environnement de programmation :**

Le répertoire ./environnement/ contient le fichier requirements.txt correspondant aux versions de package utilisées.
NB : les développements ont été réalisés au sein de l'environnement **Base** de la distribution Anaconda.

**Données d'étude :**

Le fichier source provient de RTE France sous forme de données publiques : [eco2mix](https://opendata.reseaux-energies.fr/explore/dataset/eco2mix-regional-cons-def/information/?disjunctive.libelle_region&disjunctive.nature&sort=-date_heure)
NB : ce fichier de grande taille n'est pas stocké sur GitHub.

Les notebooks JuPyTer de l'arborescence proposée : **0x** et **2x** permettent de nettoyer les données et de les structurer pour les obtenir sous les différentes formes qui seront utilisés pour les modèles de prédiction : différents pas de temps et filtration du signal par transformée de Fourier.

Ces notebooks produisent des fichiers au format csv qui sont stockés dans le répertoire **.dataset/**

La période de l'étude est du **1/1/2013** au **31/10/2021**.

**Données métier :**

Les fichiers sources se trouvent dans le répertoire **./datasource/**

Les fichiers de capacité pour les différentes filières de production ont été construit à partir de Wikipédia.

Le fichier [SYNOP](https://public.opendatasoft.com/explore/dataset/donnees-synop-essentielles-omm/table/?flg=fr&sort=date) des observations météorologiques n'est pas stocké sur GitHub du fait de sa taille (1 Go).

**Variables explicatives :**

A partir des données métiers, nous avons construit les variables explicatives qui auront pour objectif d'aider les différents modèles à améliorer leurs prédictions. Ces **régresseurs exogènes** ont été développés avec les notebooks JuPyTer **3x** de l'arborescence de fichier fournie.

Ces variables sont stockées dans le répertoire **./exog/** sous forme de fichiers au format csv.

PS : différentes visualisations de ces étapes sont disponibles dans le répertoire **./png/**

**Résultats et interprétabilité :**

Les résultats sont stockés dans le répertoire **./results/**.

Ils sont triés suivants 3 répertoires en fonction du pas temporel de modélisation : 3h, D (24h) ou W (semaine).

On y trouve les tableaux des erreurs absolues pour l'ensemble des modèles testés, ainsi que les graphiques de prédictions permettant de visualiser les différences de comportement des modèles.

L'arborescence des notebooks JuPyter est structurée de la manière suivante :
* Les notebooks **4x** servent à la prédiction de la balance directe
* les notebooks **5x** servent à la prédiction de la balance indirecte (recomposition à partir de la prédiction des énergies)

NB : concernant le pas temporel :
* les notebooks **x1** correspondent au pas 3h
* les notebooks **x2** correspondent au pas D (24h)
* les notebooks **x3** correspondent au pas W (semaine)
