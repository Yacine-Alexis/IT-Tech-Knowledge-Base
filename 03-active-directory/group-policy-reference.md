# Group Policy — référence de soutien

## Rôle d'une GPO

Une stratégie de groupe applique des paramètres aux ordinateurs ou utilisateurs d'un domaine. Une GPO est liée à un site, un domaine ou une OU. Son effet dépend du lien, de l'ordre, du filtrage de sécurité, des filtres WMI, de l'héritage et du traitement côté client.

## Ordre d'application simplifié

**L**ocal → **S**ite → **D**omain → **OU** : LSDOU. Les GPO plus proches de l'objet peuvent remplacer des paramètres antérieurs, sauf règles particulières comme Enforced ou Block Inheritance.

## Configuration ordinateur vs utilisateur

- **Computer Configuration** : dépend de l'objet ordinateur; appliquée au démarrage et rafraîchie périodiquement.
- **User Configuration** : dépend de l'objet utilisateur; appliquée à l'ouverture de session et périodiquement.

## Tâches de soutien courantes

- vérifier quelle GPO a défini un paramètre;
- forcer une actualisation contrôlée;c c 
- diagnostiquer un lecteur mappé ou une imprimante;
- vérifier filtrage et appartenance aux groupes;
- confirmer que l'objet se trouve dans la bonne OU;
- lire le journal GroupPolicy/Operational.

## Commandes

```cmd
gpupdate /force
gpresult /r
gpresult /h C:\Temp\gpresult.html
rsop.msc
```

PowerShell :

```powershell
Get-GPResultantSetOfPolicy -ReportType Html -Path C:\Temp\rsop.html
Get-WinEvent -LogName 'Microsoft-Windows-GroupPolicy/Operational' -MaxEvents 100
```

`gpupdate /force` ne corrige pas une mauvaise portée ou un problème DNS. Il peut aussi demander une fermeture de session ou un redémarrage.

## Pourquoi une GPO ne s'applique pas

1. objet dans la mauvaise OU;
2. lien désactivé;
3. filtrage de sécurité incorrect;
4. utilisateur ou ordinateur non membre du bon groupe;
5. filtre WMI faux ou lent;
6. problème DNS vers les DC;
7. accès à SYSVOL impossible;
8. réplication incomplète;
9. conflit ou priorité d'une autre GPO;
10. paramètre côté utilisateur alors qu'on attend côté ordinateur, ou inversement;
11. extension côté client et redémarrage requis;
12. loopback processing dans un contexte de kiosque/RDS.

## Préférences vs stratégies

Les Group Policy Preferences configurent souvent lecteurs, imprimantes, fichiers et registres. Selon l'option, elles peuvent rester après que la GPO ne s'applique plus. Comprends les actions Create, Replace, Update et Delete avant de modifier.

## Bonnes pratiques d'administration

- une GPO claire par objectif plutôt qu'un objet énorme;
- nom descriptif, propriétaire, date et but;
- test dans une OU pilote;
- sauvegarde avant modification;
- changement via processus approuvé;
- ne modifie pas les Default Domain Policy et Default Domain Controllers Policy sauf paramètres réellement appropriés;
- évite les filtres WMI complexes lorsque le ciblage par groupe suffit.

## Scénario

Un lecteur réseau n'apparaît que pour certains employés.

- compare leurs OU et groupes;
- génère `gpresult` pour un utilisateur fonctionnel et un utilisateur touché;
- vérifie la préférence de lecteur, son ciblage et l'accessibilité du partage;
- vérifie les permissions indépendamment de la GPO;
- n'ajoute pas manuellement le lecteur comme solution permanente avant d'avoir identifié la cause.

## Exercice

Dans un laboratoire, crée une GPO qui verrouille l'écran après une durée raisonnable et une préférence qui mappe un lecteur pour un groupe test. Produis un rapport `gpresult` et démontre pourquoi un utilisateur hors groupe ne reçoit pas le lecteur.
