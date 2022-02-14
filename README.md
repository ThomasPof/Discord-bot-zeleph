# Bot pour serveur Discord de parapente FFVL

Ce bot est conçu pour intéragir de manière automatique via certaines commandes avec les utilisateurs. Il permet notamment de valider les licences des membres afin de vérifier qu'ils sont bien membre du club.

## Installation

Node.js 16.9.0 or newer is required.

Install the app : `npm i`

Run the app : `node .`

## Prérequis

Il est nécessaire de créer un fichier config.json à la racine, ayant cette forme :

```
{
  "Token": "le token du bot Discord",
  "mainRoleId": "l'ID du rôle 'membre du club' du serveur",
  "newMemberRoleId": "un ID de rôle donné aux nouveaux membres n'ayant pas validé leur licence",
  "welcomeChannelId": "ID du salon de bienvenue"
}
```

## Fonctionnement

1. Un nouveau membre Discord se connecte au serveur, il obtient automatiquement le rôle de `newMemberRoleId`. Un message de bienvenue est envoyé par le bot (à personnaliser dans `Events/Clients/newMember.js`)
2. Il peut lancer la commande `/licence XXXX` (XXXX = numéro FFVL) afin de valider sa licence. Si la licence est dans la liste des licences du fichier `Validation/Licences.js` alors sa licence est validée. Il obtient alors les rôles de `mainRoleId` et un rôle "Licencié 2021" (année en cours)
3. Au début de chaque année, la licence doit être renouvelée. Ainsi, les **administrateurs** peuvent lancer une discussion pour pousser au renouvellement. Les membres doivent donc de nouveau lancer la commande `/licence XXXX` pour obtenir le nouveau rôle "Licencié 2022" et perdre "Licencié 2021".
5. On peut imaginer qu'au mois de Mars, un membre n'ayant pas renouvelé sa licence n'est plus membre. L'admin peut donc lancer la commande `/licences_clean_all` qui aura pour effet de supprimer le rôle `mainRoleId` à toutes les personnes n'ayant pas le rôle "Licencié 2022"

## Commandes disponibles

- `/licence XXXXX`: lancée par un membre pour valider sa licence et obtenir les rôles de `mainRoleId` et "Licencié 2022" (année en cours)
- `/licences_clean_all` : lancée par un admin. Supprime les rôles "Licencié 2021" (année précédente) et `mainRoleId` aux personnes n'ayant pas le rôle "Licencié 2022" (année en cours)
- `/licence_validate_all` : lancée par un admin. Commande de test. Permet de donner à tous le rôle "Licencié 2022" (année en cours)
- `/emitadd`: permet de tester le message de bienvenue (trigger l'ajout d'un nouveau membre Discord)
- `/verel`: permet de générer un rapide aperçu des balises utiles autour de Verel + la dernière image webcam


