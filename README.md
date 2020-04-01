# Wondy

> Wondy est une application mobile qui permet de centraliser les règles et autres outils pour des jeux de société, comme 
> des calculateurs de scores ou des cartes du jeu.
>
> Il s'agit d'un service ouvert : vous pouvez créer vos propres règles, soit pour vos jeux préférés, soit créer votre jeu.

Il vous suffit de créer un fichier texte (dans un format particulier JSON [expliqué plus bas](#introduction)) puis :
 - soit vous hébergez ce fichier sur votre site (pour qu'il puisse être téléchargé depsuis l'application mobile)
 - soit il est possible de l'héberger ici gratuitement
 
Dans les 2 cas, il pourra être référencé dans [le fichier central](https://raw.githubusercontent.com/inagua/wondy-games/master/games/games.json), 
permettant ainsi d'être facilement accessible depuis l'application mobile. Dans le cas contraire, il faudra explicitement
indiquer son URL dans l'écran d'import de l'application mobile.


## Exemples

Il y a deux fichiers d'exemple:

1. [Le fichier partiel](https://raw.githubusercontent.com/inagua/wondy-games/master/games/7-wonders-duel/game.json) qui est une partie de celui qui sert pour le jeu fournit avec l'application "7 Wonders - Duel"  
1. [Le fichier explicatif](https://raw.githubusercontent.com/inagua/wondy-games/master/games/game.json) qui reprend un élément de tout ce qui est disponible avec l'explication à la place des valeurs  

## Introduction à JSON

> Le format des fichiers Wondy est JSON.
>
> Pour information, un fichier JSON est simplement un fichier texte particulier adapté pour décrire des données. On parle 
> d'un format "clef / valeur" (ou propriété) imbriqué délimité par des accolades. Voici un exemple simple d'une fiche contact :

```json
{
  "firstName": "Bruce",
  "lastName": "Wayne",
  "city": "Gotham",
  "rate": 99,
  "vehicles": ["Batmobile", "Tumbler", "Knightcrawler"],
  "friends": [
    { "name": "Robin" },
    { "name": "Catwoman" }
  ]
}
``` 

Dans cet exemple :
- `firstName` est une clef et `"Bruce"` sa valeur (du texte), la paire formant une "propriété"
- la valeur `99` pour `rate` est elle un nombre
- la valeur associée à la clef `rate` est un tableau... de chaines de texte
- alors que pour `friends` c'est un tableau d'objets... qui eux aussi contiennent des clef / valeur (imbriqué)

### Edition

Pour créer et éditer un fichier JSON, vous pouvez :

- soit utiliser votre éditeur de texte préféré
- soit utiliser un des editeurs en ligne qui existent (voir ci-dessous)

Edition en ligne :

- Utiliser par exemple : https://jsonformatter.org/json-editor
- Dans les boutons au milieu cliquer sur "Load Data"
- Renseigner l'URL du fichier de référence : https://raw.githubusercontent.com/inagua/wondy-games/master/games/7-wonders-duel/game.json
- Puis cliquer sur "Close"

Vous pouvez alors au choix éditer dans la partie gauche (texte brut), ou la partie droite (édition élaborée), et synchroniser 
l'une et l'autre via les boutons flèche gauche et flèche droite qui se trouvent au milieu.

L'intérêt de la partie droite est notamment de faciliter la duplication de blocs. Par exemple, si vous voulez ajouter un second auteur
dans la balise `authors`, aller dans la marge de gauche à hauteur du `0 {5}` ligne 8 (`0` signifie que c'est le premier 
élément (en informatique on commence à compter à partir de 0, le second est 1, le troisième est 2...), et le `5` signifie
que l'objet contient 5 propriétés) et cliquer sur le second icone en forme de carré pour faire apparaitre le menu d'option : 
il est notamment possible de dupliquer ou supprimer tout le bloc `author` en un clic et sans erreur.

Une fois terminé cliquer sur le bouton Download au milieu pour obtenir le fichier JSON à publier (penser à le faire souvent 
pour ne pas perdre votre travail).

## Structure

```json
{
  "schema": "wondy-1.0",
  "version": "1.0",
  "title": "7 Wonders Duel",
  "description": "Développez votre science et ...",
  "image": "http://mon.site.com/assets/images/header.jpg",
  "authors": [...],
  "sections": [...],
  "cards": {...},
  "scores": {...},
  "library": {...},
}
```

Voici en détail la structure du fichier texte JSON.

- `schema` : la version de la structure du fichier utilisée (courante : `wondy-1.0`)
- `version` : la version de votre fichier, de son contenu (à gérer par l'auteur du fichier, par exemple 1.0, puis 1.1 en cas de modification)
- `title` : le nom du jeu, qui sera affiché à l'écran
- `description` : un descriptif du jeu, qui sera affiché à l'écran
- `image` : l'URL d'une image qui sera utilisée sur la homepage du jeu (privilégier une image au format paysage) [facultatif]
- `authors` : tableau des auteurs du document, voir plus bas [facultatif]
- `sections` : tableau des sections, voir plus bas
- `cards` : liste de cartes, voir plus bas [facultatif]
- `library` : liste de ressources, voir plus bas [facultatif]

### Authors

Tableau des auteurs du document. Facultatif. 

```json
{ 
    "firstName": "", 
    "lastName": "", 
    "email": "", 
    "site": "", 
    "by": "" 
}
```

- `firstName` :  prénom
- `lastName` : nom
- `email` : adresse email
- `site` : URL d'un site internet
- `by` : cette valeur pour le premier auteur sera affichée en bas de l'écran d'accueil du jeu dans l'application mobile

### Sections

#### Section

Une section est un ensemble d'instructions, par exemple pour mettre en place le jeu ou les actions à mener lors d'un tour.
Chaque section apparait distinctement sur l'écran d'accueil du jeu dans l'application mobile.

```json
{
  "id": "SetupSection",
  "icon": "bonfire",
  "title": "Mise en place",
  "description": "Préparation d'une nouvelle partie.",
  "groups": [...]
}
```

- `id` : Identifiant de la section. Il s'agit d'un texte libre (avec uniquement des lettres et des chiffres) mais chaque section doit avoir un id unique 
- `icon` : icône de la section, à choisir parmi ceux disponible dans le framework Ionic utilisé sur https://ionicons.com/
- `title` : le nom de la section, qui sera affiché à l'écran sur la page d'accueil du jeu
- `description` : un descriptif de la section, qui sera affiché à l'écran sur la page d'accueil du jeu
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
- `image` : l'URL d'une image qui sera affichée en plein écran lorsque l'utilisateur clique sur l'instruction [facultatif]
- `document` : l'URL d'un document (par exemple un PDF) qui sera affiché en plein écran lorsque l'utilisateur clique sur l'instruction [facultatif]

NB : Si à la fois `image` et `document` sont renseignés, seule `image` sera considéré.

```json
{
  "fr": "Placez le pion Conflit sur la case neutre au milieu du plateau.",
  "image": "https://mon.site.com/assets/images/supremacie-militaire.png",
  "document": "https://mon.site.com/assets/pdfs/7-Wonders-Duel-Rules-FR.pdf"
}
```

### Cards

Il est possible d'afficher des cartes, avec une image et leurs détails. Facultatif.

- `icon` : icône de la section des cartes, à choisir parmi ceux disponible dans le framework Ionic utilisé sur https://ionicons.com/
- `title` : le nom de la section des cartes, qui sera affiché à l'écran sur la page d'accueil du jeu
- `description` : un descriptif de la section, qui sera affiché à l'écran sur la page d'accueil du jeu
- `items` : tableau des cartes, voir ci-dessous

#### Item

Un item est une carte.

- `title` : le libellé de la carte, qui sera affiché sur l'écran de la carte [facultatif]
- `category` : groupe auquel appartient la carte [facultatif]
- `image` : l'URL d'une image qui sera affichée en plein écran

```json
{
    "title": "La Palace",
    "category": "Bâtiment Civil",
    "image": "http://mon.site.com/assets/images/cards/batiments-civils.jpg"
}
```

### Scores

Un des principaux intéret de l'application mobile est d'aider à calculer les scores finaux car, n'en déplaise à Pierre de Coubertin, 
l'important est quand même de faire la misère à l'adversaire ;)

Le calculateur de scores est affiché comme un tableaur, à savoir des lignes de scores (`row`) et de colonnes pour chaque 
joueurs (`players`). Le calculateur  calcule alors le total par joueur.
La première colonne indique l'icône de la ligne de score et lorsque l'on clique dessus s'affiche le détail de la ligne de 
score (image, titre, description...).

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
- `title` : le nom de la section, qui sera affiché à l'écran sur la page d'accueil du jeu
- `description` : un descriptif de la section, qui sera affiché à l'écran sur la page d'accueil du jeu
- `players` : nombre de joueurs maximum qui deternmine le nombre de colonnes à remplir qui s'afficheront 
- `rows` : liste des lignes de scores, voir ci-dessous

#### Row

Une `row` est une ligne de score, par exemple "Le nombre de pièces d'or" et "Le nombre de points de victoire".

- `icon` : icône de la section des cartes, à choisir parmi ceux disponible dans le framework Ionic utilisé sur https://ionicons.com
- `color` : couleur de l'icône, [au format CSS](https://developer.mozilla.org/fr/docs/Web/CSS/Couleurs_CSS/S%C3%A9lecteur_de_couleurs) comme par exemple `#FF0000` pour un rouge moche ;)
- `avatar` : URL de l'image qui servira d'icone de la ligne (si `icon` et `avatar` sont renseignés, ce dernier sera utilisé)
- `title` : le libellé de la ligne de score qui est affiché dans le détail quand on clique sur l'icone
- `subtitle` : sous titre de la ligne de score qui est affiché dans le détail quand on clique sur l'icone
- `description` : un descriptif de la section qui est affiché dans le détail quand on clique sur l'icone
- `image` : l'URL d'une image qui sera affichée au dessus du détail

```json
{
    "icon": "",
    "color": "#D8272E",
    "avatar": "http://mon.site.com/assets/images/icons/ico-armee.png",
    "title": "Militaire",
    "subtitle": "Pion Conflit",
    "description": "0, 2, 5 ou 10 en fonction de la position du pion Conflit",
    "image": "http://mon.site.com/assets/images/supremacie-militaire.png"
}
```

### Library

Ensemble de ressources à consulter, comme par exemple les PDF des règles du jeu ou d'aide de jeu.

- `documents` : tableau des documents, voir ci-dessous

#### Document

Un document correspond à une ressource, par exemple un PDF.

- `title` : le libellé du document, qui sera affiché sur l'écran d'accueil de la section
- `path` : l'URL où le document sera téléchargé pour être consulté en plein écran

```json
{
    "title": "Règles du jeu",
    "path": "http://mon.site.com/assets/pdfs/7-Wonders-Duel-Rules-FR.pdf"
}
```
