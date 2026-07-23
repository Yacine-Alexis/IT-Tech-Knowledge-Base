# Problèmes d'écran et d'affichage

## Isoler la chaîne

Source → GPU/pilote → port → câble/adaptateur → écran → entrée sélectionnée.

Teste chaque maillon plutôt que de remplacer l'écran immédiatement.

## Aucun signal

1. écran alimenté et bonne entrée;
2. luminosité et menu de l'écran visibles;
3. câble correctement connecté;
4. autre câble ou port connu fonctionnel;
5. écran testé avec une autre source;
6. poste testé avec un autre écran;
7. station d'accueil retirée;
8. détection Windows;
9. pilote graphique et événements;
10. démarrage/BIOS visible ou non.

Si le BIOS n'apparaît jamais sur aucun écran, le problème peut être matériel ou de démarrage, pas Windows.

## Commandes et raccourcis

- `Win + P` : mode d'affichage;
- `Win + Ctrl + Shift + B` : réinitialise le pilote graphique;
- Paramètres → Système → Affichage;
- Gestionnaire de périphériques → cartes graphiques et moniteurs.

PowerShell :

```powershell
Get-PnpDevice -Class Display
Get-CimInstance Win32_VideoController | Select-Object Name,DriverVersion,CurrentHorizontalResolution,CurrentVerticalResolution
```

## Résolution ou mise à l'échelle

- utilise la résolution native;
- vérifie mise à l'échelle par écran;
- certaines applications anciennes gèrent mal le DPI;
- une session distante peut modifier les dimensions;
- un adaptateur peut limiter la résolution ou fréquence.

## Plusieurs écrans

- capacité du GPU et du dock;
- bande passante USB-C/Thunderbolt;
- DisplayPort MST;
- câbles et adaptateurs actifs/passifs;
- fréquence et résolution combinées;
- ordre et écran principal;
- firmware du dock.

## Scintillement ou artefacts

- câble ou connecteur;
- fréquence de rafraîchissement;
- pilote;
- application avec accélération matérielle;
- GPU ou mémoire vidéo;
- surchauffe;
- écran défectueux.

Teste une capture d'écran : si l'artefact apparaît dans la capture, la cause est probablement avant l'écran; s'il n'apparaît pas, le câble ou l'écran devient plus suspect. Ce test n'est pas absolu, mais utile.

## Couleur ou luminosité

- mode nuit/HDR;
- profil de couleur;
- luminosité adaptative;
- réglages de l'écran;
- câble;
- pilote;
- calibration.

## Exercice

Scénario : deux écrans fonctionnent directement sur le portable, mais un seul via la station d'accueil. Liste les limites de dock, câble, firmware et bande passante à vérifier.
