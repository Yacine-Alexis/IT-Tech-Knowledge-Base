# Permissions NTFS et permissions de partage

## Deux couches distinctes

Lorsqu'un dossier est accédé par SMB, les permissions de partage et les permissions NTFS s'appliquent ensemble. L'accès effectif est le résultat le plus restrictif entre les deux couches, puis des règles NTFS détaillées.

Pour un accès local au serveur, seules les permissions NTFS s'appliquent.

## Permissions de partage

- Read;
- Change;
- Full Control.

Une approche fréquente consiste à donner un accès de partage relativement large à des groupes authentifiés appropriés, puis à contrôler précisément avec NTFS. Suis toutefois la norme de l'entreprise.

## Permissions NTFS

Permissions de base :

- Full control;
- Modify;
- Read & execute;
- List folder contents;
- Read;
- Write.

Les permissions avancées permettent un contrôle plus fin sur création, suppression, attributs, sous-dossiers et héritage.

## Règles importantes

- les permissions explicites ont priorité sur les héritées dans plusieurs cas;
- un Deny explicite peut bloquer un Allow, donc utilise Deny avec prudence;
- les appartenances à plusieurs groupes se cumulent généralement;
- le propriétaire peut modifier les permissions selon ses droits;
- le jeton de sécurité est créé à la connexion; un nouvel accès de groupe peut nécessiter une nouvelle session;
- le partage et NTFS doivent tous deux permettre l'action.

## Modèle AGDLP

- **A**ccounts : utilisateurs;
- **G**lobal groups : regroupent les utilisateurs par rôle;
- **D**omain **L**ocal groups : représentent l'accès à une ressource;
- **P**ermissions : attribuées au groupe local de domaine.

Exemple : Julie → `GG-Finance` → `DL-Files-Finance-Modify` → permission Modify sur le dossier.

## Diagnostic d'un accès refusé

1. Confirme le chemin exact et l'action tentée.
2. Vérifie l'identité réelle : `whoami`.
3. Vérifie groupes : `whoami /groups`.
4. Vérifie les permissions du partage.
5. Vérifie ACL NTFS et héritage.
6. Recherche un Deny explicite.
7. Vérifie si l'utilisateur utilise d'anciennes informations d'identification SMB.
8. Ferme la session ou purge les connexions seulement selon procédure.
9. Teste avec un fichier de test non sensible.

Commandes :

```powershell
Get-Acl 'D:\Shares\Finance' | Format-List
Get-SmbShareAccess -Name Finance
Get-SmbSession
Get-SmbOpenFile
```

## Propriété et déplacement

- déplacer un fichier dans le même volume conserve généralement les permissions;
- copier ou déplacer vers un autre volume hérite généralement des permissions de destination;
- vérifie les comportements réels en laboratoire, surtout avec outils de synchronisation.

## Mauvaises solutions

- ajouter Everyone: Full Control pour faire disparaître l'erreur;
- donner l'accès directement à chaque utilisateur;
- prendre possession sans justification;
- utiliser Deny pour gérer des exceptions complexes;
- tester avec un compte administrateur et conclure que les droits sont bons.

## Exercice

Crée un dossier avec groupes Read et Modify. Teste création, modification et suppression. Ajoute ensuite un conflit contrôlé dans le laboratoire et explique l'accès effectif avant de vérifier.
