# Wondy

> Wondy est une application mobile qui permet de centraliser les règles et autres outils comme des calculateurs de scores pour des jeux de société.

Ce site permet de recenser les jeux disponibles, et les explications pour vous permettre d'ajouter les votres pour les importer dans l'application.

Pour pouvoir importer votre jeu dans l'application mobile il vous faut créer un fichier texte avec un format particulier (JSON) et qu'il soit accessible depuis internet (ou ajouté sur ce site).

## Introduction

> Pour information, un fichier JSON est simplement un fichier texte particulier adapté pour décrire des données. On parle d'un format "clef / valeur" imbriqué délimité par des accolades. Voici un exemple simple d'une fiche contact :

```json
{
  "firstName": "Bruce",
  "lastName": "Wayne",
  "city": "Gotham",
  "rate": 99,
  "cars": ["Batmobile 1", "Batmobile 2"],
  "friends": [
    { "name": "Robin" },
    { "name": "Catwoman" }
  ]
}
``` 

Dans cet exemple :
- `firstName` est une clef et `Bruce` sa valeur (du texte)
- la valeur `99` pour `rate` est elle un nombre
- la valeur associée à la clef `rate` est un tableau... de chaines de texte
- alors que pour `friends` c'est un tableau d'objets... qui eux aussi contiennent des clef / valeur (imbriqué)


## Structure

```json
{
  "schema": "wondy-1.0",
  "version": "1.0",
  "title": "7 Wonders Duel",
  "description": "Développez votre science et ...",
  "image": "assets/7w2/images/header.jpg",
  "authors": [...],
  "sections": [...],
  "cards": [...],
  "scores": ,
}
```

Voici en détail la structure du fichier texte JSON.

- `schema` : la version de la structure du fichier utilisée (courante : `wondy-1.0`)
- `version` : la version de votre fichier, de son contenu (à gérer par l'auteur du fichier)
- `title` : le nom du jeu, qui sera affiché à l'écran
- `description` : un descriptif du jeu, qui sera affiché à l'écran
- `image` : l'URL d'une image qui sera utilisée sur la homepage du jeu (privilégier une image au format paysage)
- `autors` : tableau des auteurs du document, voir plus bas
- `sections` : tableau des sections, voir plus bas
- `cards` : tableau de cartes, voir plus bas

### Authors

```json
{ "firstName": "", "lastName": "", "email": "", "site": "", "by": "" }
```

### Sections

#### Section

Une section est un ensemble d'instructions, par exemple pour mettre en place le jeu ou les actions à mener lors d'un tour.

```json
{
  "id": "SetupSection",
  "icon": "bonfire",
  "title": "Mise en place",
  "description": "Préparation d'une nouvelle partie.",
  "groups": [...]
}
```

- `id` : identifiant de la section. Il sa'git d'un texte libre avec uniquement des lettres et des chiffres, mais chaque section doit avoir un id unique 
- `icon` : icône de la section, à choisir parmi ceux disponible dans le framework Ionic utilisé sur https://ionicons.com/
- `title` : le nom de la section, qui sera affiché à l'écran
- `description` : un descriptif de la section, qui sera affiché à l'écran
- `groups` : tableau de groupes d'instructions, voir ci-dessous


#### Group

Un groupe est un ensemble d'instructions.

- `title` : le nom du groupe, qui sera affiché à l'écran
- `description` : un descriptif du groupe, qui sera affiché à l'écran
- `items` : tableau d'instrucions, voir ci-dessous

```json
{
  "title": "Air de jeu",
  "items": [...]
}
```


#### Item

Un item est une instruction.

- `fr` : le libellé de l'instruction en français
- `image` : l'URL d'une image qui sera affichée en plein écran lorsque l'utilisateur clique sur l'instruction
- `document` : l'URL d'un document (par exemple un PDF) qui sera affiché en plein écran lorsque l'utilisateur clique sur l'instruction

NB : Si à la fois `image` et `document` sont renseignés, seule `image` sera considéré.

```json
{
  "fr": "Placez le pion Conflit sur la case neutre au milieu du plateau.",
  "image": "https://mon.site.com/assets/7w2/images/supremacie-militaire.png",
  "document": "https://mon.site.com/assets/7w2/pdfs/7-Wonders-Duel-Rules-FR.pdf"
}
```

### Cards

Il est possible d'afficher des cartes, avec une image et leurs détails

- `icon` : icône de la section des cartes, à choisir parmi ceux disponible dans le framework Ionic utilisé sur https://ionicons.com/
- `title` : le nom de la section, qui sera affiché à l'écran
- `description` : un descriptif de la section, qui sera affiché à l'écran
- `items` : tableau des cartes, voir ci-dessous

#### Item

Un item est une carte.

- `title` : le libellé de la carte
- `category` : groupe auquel appartient la carte
- `image` : l'URL d'une image qui sera affichée en plein écran

```json
{
    "title": "La Palace",
    "category": "Bâtiment Civil",
    "image": "assets/7w2/images/cards/batiments-civils.jpg"
}
```

### Scores

Un des principaux intéret de l'application mobile est d'aider à calculer les scores finaux car, n'en déplaise à Pierre de Coubertin, 
l'important est quand même de faire la misère à l'adversaire ;)

Le calculateur de scores est affiché comme un tableaur, à savoir des lignes de scores (`row`) et de colonnes pour chaque joueurs (`players`). Le calculateur 
calcule alors le total par joueur.
La première colonne indique l'icône de la ligne de score et lorsque l'on clique dessus s'affiche le détail de la ligne de score (image, titre, description...).

```json
{
    "players": 2,
    "icon": "calculator",
    "title": "Calculateur de scores",
    "description": "",
    "rows": [...]
}
```

- `icon` : icône de la section des scores, à choisir parmi ceux disponible dans le framework Ionic utilisé sur https://ionicons.com/
- `title` : le nom de la section, qui sera affiché à l'écran
- `description` : un descriptif de la section, qui sera affiché à l'écran
- `players` : nombre de joueurs maximum
- `rows` : liste des lignes de scores, voir ci-dessous

#### Row

Une `row` est une ligne de score, par exemple "Le nombre de pièces d'or" et "Le nombre de points de victoire".

- `icon` : icône de la section des cartes, à choisir parmi ceux disponible dans le framework Ionic utilisé sur https://ionicons.com
- `color` : couleur de l'icône, [au format CSS](https://developer.mozilla.org/fr/docs/Web/CSS/Couleurs_CSS/S%C3%A9lecteur_de_couleurs) comme par exemple `#FF0000` pour un rouge moche ;)
- `avatar` : URL de l'image qui servira d'icone de la ligne (si `icon` et `avatar` sont renseignés, ce dernier sera utilisé)
- `title` : le libellé de la ligne de score
- `subtitle` : sous titre de la ligne de score
- `description` : un descriptif de la section, qui sera affiché à l'écran
- `image` : l'URL d'une image qui sera affichée au dessus du détail

```json
{
    "icon": "",
    "color": "#D8272E",
    "avatar": "assets/7w2/images/icons/ico-armee.png",
    "title": "Militaire",
    "subtitle": "Pion Conflit",
    "description": "0, 2, 5 ou 10 en fonction de la position du pion Conflit",
    "image": "assets/7w2/images/supremacie-militaire.png"
}
```
