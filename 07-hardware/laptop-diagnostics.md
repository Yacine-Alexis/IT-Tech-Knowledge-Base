# Diagnostic d'un ordinateur portable

## Sécurité physique

Arrête l'utilisation et escalade si tu observes :

- batterie gonflée;
- odeur de brûlé;
- chaleur extrême;
- liquide;
- étincelle ou dommage électrique;
- chargeur endommagé;
- bruit mécanique anormal d'un disque.

Ne perce jamais une batterie et ne continue pas à charger un appareil gonflé.

## Collecte

- modèle, numéro d'actif et garantie;
- symptôme exact;
- fréquence et contexte;
- changement récent;
- chargeur, station d'accueil et périphériques;
- état batterie;
- espace disque;
- températures et ventilateurs;
- journaux et diagnostics fabricant;
- sauvegarde des données.

## Ne démarre pas

1. vérifie prise, adaptateur et câble;
2. observe voyants et sons;
3. retire les périphériques non essentiels;
4. teste une alimentation approuvée compatible;
5. effectue une décharge électrique ou procédure fabricant;
6. vérifie affichage externe;
7. consulte codes LED/bips;
8. escalade sous garantie avant démontage non autorisé.

## Lent ou gelé

- Gestionnaire des tâches : CPU, mémoire, disque et réseau;
- espace libre;
- mises à jour;
- processus de synchronisation;
- température et throttling;
- santé du stockage;
- mémoire;
- logiciel au démarrage;
- journaux et Moniteur de fiabilité.

PowerShell :

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-Volume
Get-PhysicalDisk
Get-CimInstance Win32_Battery
```

## Batterie

```cmd
powercfg /batteryreport
powercfg /energy
```

Compare capacité de conception et capacité de charge complète. Une estimation varie selon usage et calibration; ne remplace pas la batterie sur un seul chiffre sans symptômes et politique.

## Surchauffe

- ventilation bloquée;
- poussière;
- charge CPU prolongée;
- profil d'alimentation;
- ventilateur défaillant;
- pâte thermique ou dissipateur, selon niveau de réparation;
- environnement trop chaud.

## Stockage

Signes : erreurs, lenteurs, fichiers corrompus, bruit, BSOD. Vérifie SMART via outils approuvés, journaux Disk/Ntfs, diagnostics fabricant et sauvegarde. Évite de lancer des tests intensifs sur un disque en panne avant de sécuriser les données.

## Mémoire

Crashes aléatoires, erreurs d'application et BSOD peuvent venir de la RAM. Teste selon procédure et, si matériel accessible, isole les modules seulement si autorisé et ESD contrôlé.

## Après réparation

- test de démarrage;
- batterie et charge;
- Wi-Fi, audio, caméra, clavier, pavé tactile;
- ports et station d'accueil;
- mises à jour;
- chiffrement;
- test utilisateur;
- documentation des pièces et numéros de série.

## Exercice

Crée une fiche de diagnostic pour « portable s'éteint après 20 minutes sur batterie mais fonctionne sur secteur ».
