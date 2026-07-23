# Registre Windows — modifications sécuritaires

## Avertissement

Le registre contient des paramètres critiques. Une mauvaise modification peut empêcher une application, un profil ou Windows de fonctionner. Utilise une GPO, un paramètre d'application ou un outil de gestion officiel lorsqu'ils existent.

## Structure

- `HKEY_LOCAL_MACHINE` : paramètres du poste;
- `HKEY_CURRENT_USER` : profil de l'utilisateur actuel;
- `HKEY_USERS` : profils chargés;
- `HKEY_CLASSES_ROOT` : associations et classes;
- `HKEY_CURRENT_CONFIG` : configuration matérielle courante.

Valeurs fréquentes : String, Expandable String, DWORD 32-bit, QWORD 64-bit, Multi-String et Binary.

## Procédure avant modification

1. Confirme la source officielle de la clé et la version concernée.
2. Vérifie si la clé est contrôlée par GPO ou MDM.
3. Note le chemin, le nom, le type et la valeur actuels.
4. Exporte la clé ciblée, pas nécessairement tout le registre.
5. Crée un point de restauration ou une sauvegarde selon la politique.
6. Teste sur un appareil de laboratoire.
7. Prépare la commande de retour arrière.
8. Applique le changement avec autorisation.
9. Redémarre seulement si requis.
10. Valide et documente.

## Lecture avec PowerShell

```powershell
Get-Item 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion'
Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion'
Test-Path 'HKCU:\Software\Contoso'
```

## Sauvegarde ciblée

```cmd
reg export "HKCU\Software\Contoso" "C:\Temp\Contoso-backup.reg" /y
```

## Exemple de modification contrôlée

```powershell
$path = 'HKCU:\Software\Contoso'
New-Item -Path $path -Force
New-ItemProperty -Path $path -Name 'ExampleSetting' -PropertyType DWord -Value 1 -Force
Get-ItemProperty -Path $path -Name 'ExampleSetting'
```

Pour annuler :

```powershell
Remove-ItemProperty -Path $path -Name 'ExampleSetting'
```

L'exemple utilise une clé fictive. Ne copie pas une modification de registre trouvée sur un forum sans validation.

## Registre 32 bits vs 64 bits

Sur Windows 64 bits, certaines applications 32 bits utilisent une vue différente, souvent visible sous `WOW6432Node`. Vérifie l'architecture de l'application et l'outil utilisé.

## Problèmes de profil

Évite de supprimer des clés de profil pour « réparer » une session sans sauvegarder les données, vérifier le SID et comprendre les conséquences. Les profils temporaires peuvent provenir du stockage, des permissions, d'un antivirus, d'une corruption ou d'une indisponibilité réseau.

## Indices qu'une politique écrase la valeur

- la valeur revient après `gpupdate` ou redémarrage;
- l'interface indique « géré par votre organisation »;
- la clé se trouve dans une branche Policies;
- le rapport `gpresult` montre une stratégie correspondante.

## Commandes de vérification GPO

```cmd
gpresult /h C:\Temp\gpresult.html
gpupdate /force
```

N'exécute pas `gpupdate /force` en boucle; lis d'abord le résultat et les journaux.

## Validation

Tu maîtrises ce fichier si tu peux expliquer pourquoi exporter une clé n'est pas la même chose qu'une sauvegarde complète et comment revenir exactement à l'état précédent.
