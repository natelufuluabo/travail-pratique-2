# Travail Pratique 2

## But

Rédiger une documentation qui explique l'implementation d'une nouvelle fonctionnalité pour une application web qui sera utilisée par des bibliothécaires.

## Problème

Les bibliothécaires aimeraient être en mesure de sauvegarder des nouveaux livres dans le système de gestion eux-mêmes.

## Contraintes

- Tous les livres sauvergadés dans le système doivent être identifiés avec un code ISBN valide sauf dans les cas des livres publiés avant 1972. Dans ce cas-là, le titre du livre sera utilisé comme identifiant principal du livre.

- Le système ne peut pas sauvegardés deux livres avec le même code ISBN.

- Chaque bibliothécaire doit être identifié avant de pouvoir ajouter un nouveau livre dans le système.

## Solution

Créer et sauvegarder dans la base de données un identifiant (nom d'utilisateur + mot de passe) pour chaque bibliothécaire.

Créer un formulaire dans le front-end qui exigéra au bibliothécaire de rentrer ces identifiants. Ce formulaire enverra une requête HTTPS vers le serveur express dans le backend.

Implementer un chemin (route) dans le serveur express qui sera utilisé pour valider les identifiants dans le backend avec la base de données avant de permettre au bibliothécaire d'ajouter un nouveau livre dans le système. Le serveur renverra une réponse au front-end qui dependra de la validité des identifiants reçus.

Dans le cas d'une réponse négative, le bibliothécaire aura 2 autres essais avant que son compte soit verrouillé et requiert l'intervention d'un administrateur du système qui va créer un nouveau mot de passe pour le bibliothécaire.

Dans le cas d'une réponse positive, le bibliothécaire sera redirigé vers une nouvelle page dans le front-end qui va lui demander la date de publication du livre.

Si le livre a été publiée avant 1972, le bibliothécaire sera redirigé vers le formulaire dans lequel il pourra rentrer le titre du livre et les autres informations concernant le livre puis soumettre le formulaire. La soumission du formulaire dans le frontend enverra une requête HTTPS au serveur express dans le backend qui va créer un nouveau document dans la base de données MongoDB contenant toutes les informations du livre ajouté.

Note: Le formulaire dans le frontend ne pourras pas être soumis s'il manque le titre du livre donc il va falloir implementer un mecanisme de vérification dans le frontend afin de s'assurer de ne pas ajouter un livre sans titre.

Si le livre n'a pas été publié avant 1972, le bibliothécaire sera redirigé vers un formulaire dans le frontend qui va lui demander de rentrer le code ISBN du livre puis faire une demande de vérification du code ISBN. Cette vérification sera effectuée dans le frontend. Si le code ISBN est valide, le bibliothécaire sera redirigé vers un formulaire dans lequel il va rentrer les autres informations concernant le livre puis soumettre le formulaire. La soumission du formulaire dans le frontend enverra une requête HTTPS au serveur express dans le backend qui va créer un nouveau document dans la base de données MongoDB contenant toutes les informations du livre ajouté.

Note: Si le code ISBN est valide, ce dernier doit être conservé et pre-remplis pour le bibliothécaire dans le formulaire qui sera soumis au serveur express dans le backend.
