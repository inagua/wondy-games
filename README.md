# Wondy

> Wondy est une application mobile qui permet de centraliser les règles et autres outils comme des calculateurs de scores pour des jeux de société.

Ce site permet de recenser les jeux disponibles, et les explications pour vous permettre d'ajouter les votres pour les importer dans l'application.

Pour pouvoir importer votre jeu dans l'application mobile il vous faut créer un fichier texte avec un format particulier (JSON) et qu'il soit accessible depuis internet (ou ajouté sur ce site).

## Introduction

> Pour information, un fichier JSON est simplement un fichier texte particulier adapté pour décrire des données. On parle d'un format "clef / valeur" imbriqué délimité par des accolades. Voici un exemple simple d'une fiche contact :

```
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

Voici en détail la structure du fichier texte JSON.

- `schema` : la version de la structure du fichier utilisée (courante : `wondy-1.0`)
- `version` : la version de votre fichier, de son contenu (à gérer par l'auteur du fichier),
- `title` : le nom du jeu,
- `description` : un descriptif du jeu,
- `image` : l'URL d'une image qui sera utilisée sur la homepage du jeu (privilégier une image au format paysage)
