# Protection des postes — antivirus, EDR et durcissement

## Définitions

- **Antivirus** : détecte et bloque des fichiers ou comportements malveillants.
- **EDR** : collecte davantage de télémétrie, détecte des comportements et permet investigation/réponse.
- **Pare-feu hôte** : filtre les connexions du poste.
- **Chiffrement disque** : protège les données au repos, par exemple BitLocker.
- **Application control** : limite les applications autorisées.
- **Patch management** : maintient OS et logiciels à jour.

Aucun outil ne remplace les autres. La sécurité repose sur plusieurs couches.

## Vérifications de premier niveau

- agent présent et sain;
- signatures ou moteur à jour;
- dernier scan et dernières alertes;
- appareil visible dans la console;
- pare-feu actif;
- chiffrement actif et clé de récupération gérée;
- OS et applications supportés;
- utilisateur sans privilèges administratifs permanents.

PowerShell, selon environnement :

```powershell
Get-MpComputerStatus
Get-MpThreatDetection
Get-NetFirewallProfile
Get-BitLockerVolume
```

Ces commandes donnent un état local, mais la console centrale reste souvent la source principale.

## Détection sur un poste

1. ne supprime pas manuellement le fichier avant collecte;
2. note heure, utilisateur, nom de détection et action;
3. isole l'appareil avec l'outil approuvé si le risque le justifie;
4. contacte la sécurité;
5. recueille les détails sans exécuter le fichier;
6. vérifie étendue : autres machines, utilisateurs, courriels;
7. suit le playbook de réponse;
8. ne réactive pas l'appareil avant validation.

## Faux positif possible

Un faux positif doit être démontré et approuvé. Ne crée pas une exclusion permanente parce qu'une application est bloquée. Recueille hash, éditeur, signature, chemin, version, comportement et besoin métier.

## Exclusions

Une exclusion réduit la visibilité. Elle doit être :

- minimale;
- justifiée;
- approuvée;
- limitée à un chemin, processus ou durée;
- revue périodiquement;
- documentée.

## Pare-feu

Ouvre uniquement les flux requis. Une règle devrait préciser direction, protocole, port, programme, profil et sources/destinations.

```powershell
Get-NetFirewallRule -Enabled True
Get-NetFirewallProfile
```

## Chiffrement

Avant une opération de BIOS, carte mère, TPM ou récupération système, confirme que la clé BitLocker est sauvegardée dans l'emplacement approuvé. Ne désactive pas le chiffrement pour contourner un problème sans autorisation.

## Exercice

Scénario : l'EDR bloque un outil interne après une mise à jour. Rédige les informations à recueillir et une réponse qui ne consiste pas à désactiver l'EDR.
