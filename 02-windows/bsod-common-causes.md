# Écrans bleus Windows — causes et démarche

## Ce qu'est un BSOD

Un écran bleu survient lorsque Windows rencontre une erreur noyau qu'il ne peut pas gérer sans risque. Le code d'arrêt et le fichier de vidage sont des indices; ils ne suffisent pas toujours à identifier la cause exacte.

## Causes fréquentes

- pilote défectueux ou incompatible;
- mémoire vive instable;
- stockage ou système de fichiers endommagé;
- surchauffe ou alimentation instable;
- micrologiciel/BIOS et pilotes de chipset;
- logiciel de sécurité ou composant noyau;
- périphérique récemment ajouté;
- corruption système;
- overclocking ou paramètres matériels agressifs.

## Collecte avant correction

1. Note le code d'arrêt et tout pilote affiché.
2. Demande ce qui se passait au moment du crash.
3. Note les changements récents : pilote, mise à jour, matériel, logiciel.
4. Vérifie `C:\Windows\Minidump` et la date des fichiers.
5. Consulte le Moniteur de fiabilité et les événements juste avant le redémarrage.
6. Vérifie si le problème se reproduit selon une action précise.

## Vérifications prudentes

```powershell
Get-ComputerInfo
Get-WinEvent -FilterHashtable @{LogName='System'; StartTime=(Get-Date).AddDays(-2); Level=1,2,3}
Get-PnpDevice | Where-Object Status -ne 'OK'
```

Outils Windows :

- `perfmon /rel` pour la chronologie;
- Diagnostic de mémoire Windows, idéalement suivi d'un outil mémoire approuvé;
- `sfc /scannow` pour les fichiers système;
- `DISM /Online /Cleanup-Image /RestoreHealth` si l'image Windows est endommagée;
- `chkdsk /scan` pour une première vérification en ligne.

Les commandes de réparation doivent être utilisées après collecte et avec une sauvegarde adéquate.

## Stratégie d'isolation

- retire ou désactive temporairement uniquement le matériel récemment ajouté, si autorisé;
- reviens à un pilote précédent si le problème a commencé juste après une mise à jour;
- mets à jour depuis le fabricant ou le système de gestion d'entreprise;
- teste la mémoire et le stockage;
- vérifie températures et alimentation;
- compare avec un profil ou démarrage propre seulement si cela aide à isoler un logiciel.

## Codes d'arrêt — catégories courantes

- `IRQL_NOT_LESS_OR_EQUAL` : souvent pilote ou mémoire, mais analyse requise;
- `PAGE_FAULT_IN_NONPAGED_AREA` : mémoire, pilote ou stockage;
- `CRITICAL_PROCESS_DIED` : processus système critique terminé;
- `WHEA_UNCORRECTABLE_ERROR` : erreur matérielle signalée par l'architecture WHEA;
- `DPC_WATCHDOG_VIOLATION` : pilote, stockage ou opération bloquée;
- `INACCESSIBLE_BOOT_DEVICE` : Windows ne peut plus accéder au volume de démarrage.

Évite les conclusions automatiques à partir du nom du code.

## Quand escalader

- plusieurs postes touchés après une mise à jour;
- appareil sous garantie ou données critiques;
- suspicion de défaillance disque;
- vidage nécessitant analyse avancée;
- crash impliquant sécurité, chiffrement ou pilote d'entreprise;
- matériel gonflé, odeur, chaleur anormale ou risque électrique.

## Documentation de ticket

Inclue modèle, numéro d'actif, version Windows, code d'arrêt, fréquence, changement récent, fichiers de vidage, tests effectués, résultats et état des sauvegardes.

## Exercice

Construis un arbre de diagnostic pour : « le portable affiche un BSOD une fois par jour depuis l'installation d'une station d'accueil ».
