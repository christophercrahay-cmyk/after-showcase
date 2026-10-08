# AFTER

> Prototype de jeu systémique sous Godot : survie technique, récupération, fabrication, automatisation et robotique dans un monde rural sous pression d'une IA hostile.

**Statut : vitrine technique.** Le dépôt de développement, les assets et les systèmes de simulation restent privés. Ce dépôt présente l'intention, l'architecture générale et la méthode de construction du projet.

> **Technical review:** [Architecture evidence and limitations](AUDIT.md) — simulation logic and visual presentation.

## Le concept

AFTER part d'une règle de progression simple :

> **Faire manuellement → comprendre → construire l'outil → automatiser.**

Le joueur ne débloque donc pas seulement des capacités dans un menu. Il transforme progressivement son environnement en remettant en état des machines, en récupérant des ressources et en construisant une chaîne technique.

Le point de départ est un **atelier civil en Franche-Comté**. Une IA hostile exploite des machines et robots civils détournés. Le joueur dispose de sa propre IA locale, mais ses capacités physiques dépendent des systèmes qu'il parvient réellement à construire.

## Boucle de progression

```text
Explorer
   ↓
Récupérer une ressource
   ↓
Manipuler / réparer
   ↓
Transformer
   ↓
Fabriquer une pièce
   ↓
Assembler un nouvel outil
   ↓
Automatiser une tâche
   ↓
Accéder à de nouvelles possibilités
```

Les déblocages sont liés à l'état du monde : machines disponibles, objets réparés, ressources obtenues et capacités effectivement construites.

## Exemple : première chaîne technique

Le premier chapitre sert à enseigner les systèmes par leur utilisation :

```text
Métal
  ↓
remise en service d'un robot de manutention
  ↓
Polymère
  ↓
réparation d'un recycleur
  ↓
Filament
  ↓
impression 3D
  ↓
premières pièces techniques
```

L'objectif est de faire comprendre au joueur **pourquoi** une machine est utile avant qu'elle devienne une couche d'automatisation.

# Architecture

AFTER est développé avec **Godot**.

Un choix important du projet consiste à séparer autant que possible la **simulation** de sa **présentation**.

```text
                ┌─────────────────────────┐
                │       Simulation        │
                │                         │
                │ état du monde           │
                │ entités                 │
                │ ressources              │
                │ tâches / interactions   │
                │ navigation              │
                └────────────┬────────────┘
                             │
                      état / événements
                             │
                ┌────────────v────────────┐
                │      Présentation       │
                │                         │
                │ scènes Godot            │
                │ modèles / animations    │
                │ effets / audio          │
                │ interface joueur        │
                └─────────────────────────┘
```

Cette séparation permet de tester une partie importante des règles sans dépendre du rendu 3D.

## Simulation déterminée par l'état

Les systèmes ne sont pas pensés comme une succession de scripts de scénario indépendants.

Ils s'appuient autant que possible sur des états et capacités explicites :

```text
Ressource trouvée
      +
Station disponible
      +
Préconditions satisfaites
      ↓
Nouvelle action possible
      ↓
État du monde modifié
```

Cette approche facilite l'ajout de nouvelles chaînes de production et limite les dépendances cachées entre progression, interface et environnement.

## Navigation et agents

Le prototype utilise une navigation calculée pour permettre aux entités de se déplacer et d'exécuter des tâches dans l'espace simulé.

Les robots ne sont pas uniquement des éléments décoratifs : leur forme et leur rôle découlent d'une fonction dans le monde.

Parmi les familles explorées :

- drone d'observation ;
- rover d'inspection ;
- quadrupède de pistage ;
- robot de récupération ;
- unité de sabotage ;
- unité de brouillage ;
- robot de construction / réparation.

La logique détaillée de comportement reste dans le projet privé.

# Machines et fabrication

L'atelier est progressivement équipé de stations techniques.

Exemples :

**Robot de manutention**  
Permet de déplacer ou manipuler des éléments que le joueur ne peut pas traiter efficacement seul.

**Recycleur de filament**  
Transforme des ressources polymères récupérées en matière utilisable.

**Imprimante 3D**  
Produit des pièces et kits. Les objets complexes ne sortent pas nécessairement terminés de l'imprimante : ils peuvent nécessiter un assemblage sur une autre station.

**Stockage**  
Fait partie de la logique physique de ressources plutôt que d'un inventaire abstrait illimité.

## Crafting volontairement lisible

L'objectif n'est pas d'accumuler des centaines de recettes presque identiques.

Une ressource doit idéalement ouvrir quelques choix compréhensibles, avec des chaînes suffisamment courtes pour que le joueur puisse raisonner sur le système.

Cela permet de conserver une profondeur systémique sans transformer l'expérience en tableur.

# Direction du monde

AFTER vise une ambiance **rurale / péri-industrielle de l'est de la France**, plutôt qu'un décor post-apocalyptique générique.

Le premier environnement se concentre autour d'un atelier et de ses abords :

- asphalte fissuré et gravier ;
- herbes hautes et végétation irrégulière ;
- bouleaux et feuillus ;
- bâtiments et équipements civils ;
- machines récupérées, réparées ou détournées.

La technologie avancée doit émerger progressivement d'un environnement crédible et matériel.

# IA dans l'univers

Deux formes d'IA structurent le contexte du jeu :

**IA hostile** — utilise et détourne des infrastructures et robots civils.

**IA locale du joueur** — apporte des capacités d'analyse et d'assistance, mais reste dépendante des moyens physiques disponibles dans l'atelier.

Cette dépendance est importante : une intelligence logicielle ne peut pas fabriquer, déplacer ou réparer quelque chose sans capteurs, énergie, machines et actionneurs adaptés.

Cela permet de faire de la robotique et de l'automatisation des éléments de gameplay plutôt que de simples éléments narratifs.

# Méthode de développement

Le projet est construit par incréments courts :

```text
Spécification
    ↓
Implémentation minimale
    ↓
Tests de simulation
    ↓
Validation
    ↓
Intégration visuelle
    ↓
Itération suivante
```

Les étapes importantes disposent de tests de non-régression. Les chiffres internes évoluent rapidement et ne sont volontairement pas utilisés ici comme argument marketing.

L'objectif est plutôt de démontrer une méthode : **stabiliser les règles avant d'empiler du contenu**.

# Pipeline d'assets

Le projet combine plusieurs sources et étapes :

- modèles 3D ;
- personnages et vêtements ;
- animations ;
- machines et robots ;
- végétation et environnement ;
- préparation / organisation des assets ;
- intégration dans Godot.

Les assets entrants passent par une étape de staging avant intégration afin d'éviter que le projet principal devienne un dépôt désorganisé de fichiers bruts.

# Ce que le projet démontre

AFTER est aussi un projet d'ingénierie de systèmes.

Il demande de faire travailler ensemble :

| Domaine | Travail |
| --- | --- |
| Moteur | Godot |
| Simulation | état du monde, entités, interactions |
| Navigation | déplacement d'agents |
| Gameplay | progression systémique |
| Production | ressources, machines, crafting |
| Robotique fictive | fonctions, capacités, contraintes |
| 3D | modèles, rig, animations, intégration |
| Validation | tests et non-régression |
| Architecture | séparation simulation / présentation |

Ce projet complète mes travaux orientés applications et agents IA : le problème reste le même à une autre échelle — **faire coopérer beaucoup de composants sans perdre la maîtrise du système**.

## Ce qui reste privé

Cette vitrine ne publie pas :

- le code source du jeu ;
- les scènes et scripts Godot ;
- les tests internes et leurs fixtures ;
- les assets sous licence ou propriétaires ;
- les modèles 3D et animations ;
- les règles détaillées de simulation ;
- les paramètres d'équilibrage ;
- les documents internes de conception et d'audit ;
- les pipelines et outils internes complets.

Des captures et vidéos pourront être ajoutées ici au fur et à mesure de la présentation publique du projet.

---

**Christopher Crahay**  
AI Builder — Intégrateur de systèmes IA


<!-- audit-sequence: 03 | architecture survives when presentation is removed -->
