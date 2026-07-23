# Dépannage des imprimantes

## Première question

Le problème vient-il :

- d'une seule application;
- d'un seul utilisateur;
- d'un seul poste;
- d'une file d'impression;
- d'une imprimante physique;
- de tout un site?

Cette portée évite de redémarrer le spooler alors que l'imprimante manque simplement de papier.

## Vérifications physiques

- alimentation et écran;
- papier, bourrage et capots;
- toner/encre;
- message ou code exact;
- câble réseau/USB;
- étiquettes, format et bac;
- travaux bloqués sur l'appareil;
- adresse IP et page de configuration.

## Vérifications Windows

```powershell
Get-Printer
Get-PrintJob
Get-PrinterPort
Get-Service Spooler
```

1. confirme l'imprimante sélectionnée;
2. vérifie si elle est en pause ou hors connexion;
3. imprime une page de test Windows;
4. teste une autre application;
5. vérifie file et serveur d'impression;
6. teste le port réseau;
7. vérifie pilote et préférences;
8. redémarre le spooler seulement si nécessaire et autorisé.

## Imprimante réseau

```powershell
Test-NetConnection printer01 -Port 9100
Test-NetConnection printserver -Port 445
Resolve-DnsName printer01
```

Le port dépend du protocole : RAW 9100, IPP, LPR ou partage via serveur. Ne suppose pas 9100 dans tous les cas.

## File bloquée

Un document corrompu peut bloquer la file.

1. identifie le travail;
2. annule le travail depuis la file;
3. si impossible, arrête le spooler selon procédure;
4. supprime seulement les fichiers de file prévus;
5. redémarre le service;
6. teste avec une page simple;
7. vérifie le document d'origine.

Évite d'effacer toutes les files sur un serveur d'impression partagé pendant les heures de pointe.

## Pilotes

- utilise le pilote validé par l'entreprise ou le fabricant;
- distingue pilote universel et spécifique;
- architecture et version Windows;
- Type 3 vs Type 4 selon environnement;
- ne télécharge pas depuis un site tiers;
- une mise à jour de pilote sur serveur peut affecter plusieurs utilisateurs.

## Qualité d'impression

- lignes ou taches : consommable, tambour, tête, rouleau;
- couleurs incorrectes : calibration, profil, consommable;
- pages pâles : toner/encre, économie, matériel;
- format incorrect : bac, taille papier, pilote;
- impression de caractères : mauvais pilote ou langage.

## Scan

Le scan peut utiliser un autre chemin : SMB vers dossier, courriel SMTP, application locale ou service cloud. Vérifie DNS, authentification, certificat, permissions et destination.

## Ticket complet

Modèle, numéro d'actif, emplacement, IP, code d'erreur, consommables, portée, file, pilote, tests, page de configuration et résultat final.

## Exercice

Scénario : tous les utilisateurs peuvent imprimer sauf une personne, qui reçoit « Access denied » sur la file partagée. Distingue réseau, file, pilote et permission.
