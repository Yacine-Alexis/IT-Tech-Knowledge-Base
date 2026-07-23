# Observateur d'événements Windows — guide pratique

## Objectif

Utiliser les journaux pour établir une chronologie et confirmer une hypothèse. Un identifiant d'événement isolé n'est pas une preuve complète : sa source, son niveau, son texte, son heure et les événements voisins comptent.

## Journaux principaux

- **Application** : erreurs d'applications et composants.
- **Security** : authentification, audits et accès, selon la stratégie d'audit.
- **System** : pilotes, services, démarrage, alimentation et matériel.
- **Setup** : installation de rôles, mises à jour et configuration.
- **Applications and Services Logs** : journaux détaillés par produit, par exemple PowerShell, Windows Update, GroupPolicy et Defender.

## Méthode efficace

1. Reproduis ou note l'heure exacte du problème.
2. Ouvre `eventvwr.msc`.
3. Filtre sur une fenêtre de temps courte.
4. Commence par Critical, Error et Warning, sans ignorer les événements Information liés.
5. Lis le message complet et l'onglet Details.
6. Corrèle plusieurs événements et le symptôme utilisateur.
7. Recherche la source et l'identifiant dans la documentation officielle si nécessaire.
8. Exporte les événements pertinents avant un changement important.

## Événements fréquemment utiles

| Zone | Événement ou source | Interprétation générale |
|---|---|---|
| Démarrage | Kernel-Power 41 | Arrêt inattendu; ne donne pas à lui seul la cause |
| Arrêt | EventLog 6008 | Arrêt précédent inattendu |
| Service | Service Control Manager 7000–7099 | Échec de démarrage, délai ou configuration de service |
| Disque | Disk, Ntfs, StorPort | Erreurs d'E/S, système de fichiers, stockage |
| Connexion | Security 4624 | Ouverture de session réussie |
| Connexion | Security 4625 | Échec d'ouverture de session; lire le type et le code |
| Verrouillage | Security 4740 sur DC | Compte AD verrouillé, si audit activé |
| Groupe | GroupPolicy 1058/1030 et journal opérationnel | Accès ou traitement GPO problématique |
| Mise à jour | WindowsUpdateClient | Installation, échec ou redémarrage requis |
| Défense | Microsoft-Windows-Windows Defender/Operational | Détections et actions de protection |

Les identifiants peuvent varier selon version et composant. Utilise-les comme points de départ, pas comme liste absolue.

## PowerShell

```powershell
Get-WinEvent -LogName System -MaxEvents 50
Get-WinEvent -FilterHashtable @{LogName='System'; Level=1,2,3; StartTime=(Get-Date).AddHours(-2)}
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625; StartTime=(Get-Date).AddDays(-1)}
Get-WinEvent -ListLog * | Sort-Object RecordCount -Descending | Select-Object -First 20
```

Exporter :

```powershell
wevtutil epl System C:\Temp\System.evtx
```

## Exemple de raisonnement

Symptôme : le PC redémarre seul à 14 h 32.

- Kernel-Power 41 à 14 h 33 confirme un arrêt non propre.
- Cherche juste avant : erreur thermique, pilote, stockage, bugcheck ou événement de mise à jour.
- Vérifie aussi `C:\Windows\Minidump`, l'historique de fiabilité et les journaux matériels.
- Ne conclus pas « alimentation défectueuse » uniquement à partir de l'événement 41.

## Outils complémentaires

- `perfmon /rel` : Moniteur de fiabilité, excellent pour une chronologie visuelle.
- `msinfo32` : informations système.
- `services.msc` : état et dépendances des services.
- `Get-CimInstance Win32_ReliabilityRecords` : historique de fiabilité par PowerShell.

## Erreurs à éviter

- effacer les journaux;
- filtrer seulement les erreurs et manquer le contexte;
- rechercher un événement générique sur Internet et appliquer une correction non liée;
- changer plusieurs services avant d'avoir exporté les données;
- ignorer le fuseau horaire et l'heure réelle du symptôme.

## Exercice

Provoque une erreur bénigne dans un laboratoire, note l'heure, retrouve-la dans les journaux, exporte l'événement et rédige une conclusion qui distingue fait, hypothèse et prochaine vérification.
