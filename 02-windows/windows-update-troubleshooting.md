# Dépannage de Windows Update

## Avant de commencer

Détermine si le poste est géré par Windows Update for Business, Intune, WSUS ou un autre outil. Une politique d'entreprise peut expliquer un comportement qui semble anormal sur un poste personnel.

## Collecte

- version et build de Windows;
- code d'erreur exact;
- mise à jour concernée et numéro KB;
- date du dernier succès;
- espace disque disponible;
- redémarrage en attente;
- VPN, proxy ou réseau utilisé;
- étendue : un poste ou plusieurs.

Commandes :

```powershell
Get-ComputerInfo | Select-Object WindowsProductName, WindowsVersion, OsBuildNumber
Get-HotFix | Sort-Object InstalledOn -Descending | Select-Object -First 20
Get-Volume
```

## Ordre de dépannage

1. Confirme l'heure, la date et la connectivité.
2. Vérifie l'espace libre.
3. Redémarre si une installation est en attente et que cela est autorisé.
4. Consulte l'historique de Windows Update et le code d'erreur.
5. Vérifie les services BITS, Windows Update et Cryptographic Services.
6. Consulte les journaux Windows Update.
7. Vérifie la santé de l'image et les fichiers système.
8. Réinitialise les composants seulement selon une procédure approuvée.
9. Si plusieurs postes sont touchés, enquête sur la plateforme de gestion ou la mise à jour elle-même.

## Services

```powershell
Get-Service wuauserv,bits,cryptsvc
```

Ne change pas leur type de démarrage arbitrairement sur un poste géré.

## Réparation système

```cmd
DISM /Online /Cleanup-Image /ScanHealth
DISM /Online /Cleanup-Image /RestoreHealth
sfc /scannow
```

Exécute DISM avant SFC lorsque l'image de composants est suspecte. Ces opérations peuvent prendre du temps et nécessitent une connexion ou une source appropriée.

## Journaux

```powershell
Get-WindowsUpdateLog
Get-WinEvent -LogName 'Microsoft-Windows-WindowsUpdateClient/Operational' -MaxEvents 100
```

`Get-WindowsUpdateLog` produit un fichier lisible à partir des traces ETL; il peut être utile, mais commence par l'historique et le journal opérationnel.

## Symptômes fréquents

| Symptôme | Vérifications |
|---|---|
| Téléchargement bloqué | BITS, réseau, proxy, espace, cache, service de gestion |
| Installation échoue | code KB, image de composants, antivirus/EDR, pilote, incompatibilité |
| Redémarrage en boucle | état de maintenance, mise à jour défectueuse, récupération |
| « Votre organisation gère… » | MDM, GPO, WSUS, compte professionnel |
| Plusieurs postes échouent | déploiement central, anneau, approbation, incident fournisseur |

## Réinitialisation des composants

Cette action modifie le cache de mises à jour et doit suivre la procédure interne. Avant de le faire : capture le code d'erreur, exporte les journaux, confirme qu'aucune tâche de déploiement n'est en cours et prépare un retour arrière.

## Escalade

Escalade si :

- mise à jour de sécurité critique échoue sur plusieurs machines;
- BitLocker ou le démarrage est affecté;
- le poste ne démarre plus;
- la politique MDM/WSUS semble incorrecte;
- une désinstallation de mise à jour est envisagée en production.

## Exercice

Rédige un ticket pour un échec de mise à jour avec le code, le KB, la build, l'espace libre, les services, les journaux consultés et la prochaine action.
