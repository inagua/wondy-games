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
    { name: "Robin" },
    { name: "Catwoman" }
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

Un item est une instrusction.

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
