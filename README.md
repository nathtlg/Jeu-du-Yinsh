# YINSH

Implémentation en **Java / JavaFX** du jeu de plateau abstrait **YINSH**, avec un adversaire contrôlé par une IA Minimax (élagage Alpha-Bêta).

Projet réalisé dans le cadre de la **SAÉ 2.2**, BUT Informatique, Université de Caen Normandie.

## Le jeu en bref

YINSH se joue à deux (Blancs et Noirs) sur un plateau hexagonal. Chaque joueur dispose de 5 anneaux.

1. À son tour, un joueur place un **pion** de sa couleur dans l'un de ses anneaux, puis **déplace cet anneau** en ligne droite.
2. Les pions franchis par l'anneau sont **retournés**.
3. Quand un joueur aligne **4 pions** de sa couleur, il retire cette ligne ainsi que l'un de ses anneaux.
4. Le premier joueur à retirer **3 anneaux** gagne la partie.

## Fonctionnalités

- **Deux modes de jeu** : Joueur vs Joueur et Joueur vs IA.
- **IA Minimax avec élagage Alpha-Bêta**, dont la profondeur de recherche est paramétrable.
- **Paramètres de l'IA** modifiables dans l'interface : poids d'un anneau retiré, d'un pion sur le plateau, d'une ligne de 4 pions, et score de victoire.
- **Aide au jeu** : bouton « Meilleur coup » et affichage de l'évaluation de la position.
- **Sauvegarde et chargement** des parties (fichiers `*.yinsh`).
- **Mode édition** : ajout et suppression de pions et d'anneaux directement sur le plateau (clic gauche pour ajouter, clic droit pour supprimer).
- **Informations de partie** : joueur courant, phase, nombre de pions et d'anneaux.
- **Affichage** : zoom, épaisseur des traits, affichage des coordonnées.

## Architecture

Le projet est un projet **Maven multi-modules** (Java 21, modules Java `module-info`).

```
.
├── pom.xml                      # POM parent (YINSH)
├── hexagonalCoordinate/         # Module de coordonnées hexagonales
│   └── src/main/java/coordinates/
│       ├── Coordinate           # Abstraction d'une coordonnée
│       ├── CoordinateCube       # Coordonnées cubiques
│       ├── CoordinateDoubled    # Coordonnées doublées
│       ├── Direction, Mode, Point, DifferentAxisException
└── application/                 # Application JavaFX
    └── src/main
        ├── java/but/info/sae2_12/
        │   ├── App.java         # Point d'entrée
        │   ├── model/           # Modèle du jeu
        │   │   ├── state/       # État de la partie (IState, State)
        │   │   ├── actions/     # Actions : Move, RemoveLine
        │   │   ├── tokens/      # Pièces : Pawn, Ring
        │   │   ├── factory/     # Génération de plateaux (vide, aléatoire, scénarios de test)
        │   │   └── Model, Team, GameMode, Utils
        │   ├── AI/              # IA : AI, MinimaxAI, MiniMax (Alpha-Bêta)
        │   └── ui/
        │       ├── controllers/ # Contrôleurs JavaFX (menus, partie, paramètres, IA...)
        │       ├── interaction/ # Modes d'interaction : jeu, édition, retrait de ligne
        │       └── objects/     # HexSquare, case hexagonale du plateau
        └── resources/but/info/sae2_12/   # Vues FXML
```

### Patrons de conception utilisés
- **Factory** (`IFactory`, `AbstractFactory`, `FactoryCube`, `FactoryDoubled`) : création des plateaux selon le système de coordonnées.
- **State** (`IState`, `State`) : état immuable de la partie, un nouvel état étant produit à chaque action.
- **Strategy / Mode d'interaction** (`InteractionMode`) : le comportement des clics change selon le mode (jeu, édition, retrait de ligne).

### Fonction d'évaluation de l'IA

| Élément | Poids par défaut |
|---|---|
| Anneau retiré par l'IA / l'adversaire | +1000 / −1000 |
| Pion sur le plateau | +10 / −10 |
| Ligne de 4 pions | +50 / −50 |
| Victoire / défaite | ±100 000 |

## Prérequis

- **JDK 21** ou supérieur
- **Maven 3.8** ou supérieur
- JavaFX 21 (téléchargé automatiquement par Maven)

## Compilation et lancement

```bash
git clone https://github.com/nathtlg/yinsh.git
cd yinsh

# Compiler
mvn clean install

# Lancer l'application
mvn clean javafx:run
```

La commande `javafx:run` est configurée sur la classe principale `but.info.sae2_12.App`.

## Documentation

Le code est documenté en **JavaDoc**. Pour la générer :

```bash
mvn javadoc:javadoc
```

## Équipe

Groupe 13 — SAÉ 2.2, BUT Informatique, Université de Caen Normandie.

| Membres |
|---|
| [COLLET Léo](https://github.com/leocollet07) |
| [DUTEURTRE Gabriel](https://github.com/gabidut) |
| LEGROS Ewenn |
| [TOULORGE Nathan](https://github.com/nathtlg) |

## Répartition du travail et origine du code

Ce dépôt regroupe plusieurs parties qui n'ont pas toutes été réalisées par l'équipe.

| Partie | Origine |
|--------|---------|
| **Module `hexagonalCoordinate`** (coordonnées cubiques et doublées, directions, etc.) | Fourni par l'enseignant |
| **Modèle du jeu et IA** (`model/`, `AI/`) | Fourni par l'enseignant |

> Seul le **front** a été développé par l'équipe dans le cadre de ce dépôt.

### 🔗 Projet d'origine

Le modèle du jeu et l'IA ainsi que le module `hexagonalCoordinate` où j'ai participé :
(ajout plus tard)

Les contributeurs de ce projet sont listés dans son propre README.
