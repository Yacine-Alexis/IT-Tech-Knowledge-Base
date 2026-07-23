# PowerShell pour technicien IT — par tâche

## Principes de base

PowerShell manipule des objets, pas seulement du texte. Utilise d'abord les commandes en lecture seule. Avant un changement, comprends les paramètres, teste sur un poste de laboratoire et utilise `-WhatIf` lorsque disponible.

## Obtenir de l'aide

```powershell
Get-Help Get-Service
Get-Help Get-Service -Examples
Get-Command *printer*
Get-Member
```

## Inventaire du poste

```powershell
Get-ComputerInfo
Get-CimInstance Win32_ComputerSystem
Get-CimInstance Win32_OperatingSystem
Get-CimInstance Win32_BIOS
Get-CimInstance Win32_LogicalDisk
Get-PhysicalDisk
Get-Volume
```

## Réseau

```powershell
Get-NetAdapter
Get-NetIPConfiguration
Get-NetIPAddress
Get-DnsClientServerAddress
Get-NetRoute
Resolve-DnsName example.com
Test-NetConnection example.com -Port 443
Get-NetTCPConnection -State Listen
```

## Processus et performance

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 10
Get-Counter '\Processor(_Total)\% Processor Time'
Get-Counter '\LogicalDisk(_Total)\% Free Space'
```

## Services

```powershell
Get-Service
Get-Service -Name Spooler
Get-Service | Where-Object Status -eq 'Stopped'
Restart-Service -Name Spooler
```

Avant un redémarrage, vérifie l'impact et les dépendances :

```powershell
Get-Service -Name Spooler -DependentServices
Get-Service -Name Spooler -RequiredServices
```

## Utilisateurs, groupes et sessions locales

```powershell
Get-LocalUser
Get-LocalGroup
Get-LocalGroupMember -Group Administrators
whoami
whoami /groups
quser
```

## Fichiers et permissions

```powershell
Get-ChildItem C:\Temp -Recurse -ErrorAction SilentlyContinue
Get-Item C:\Path\file.txt | Select-Object *
Get-Acl C:\Data | Format-List
Test-Path C:\Data
Get-FileHash C:\Temp\file.iso
```

## Logiciels et pilotes

```powershell
Get-PnpDevice | Where-Object Status -ne 'OK'
Get-CimInstance Win32_PnPSignedDriver | Select-Object DeviceName, DriverVersion, Manufacturer
Get-AppxPackage
winget list
```

Évite `Win32_Product` pour un simple inventaire : cette classe peut déclencher une vérification/réparation MSI et être lente.

## Journaux

```powershell
Get-WinEvent -LogName System -MaxEvents 100
Get-WinEvent -FilterHashtable @{LogName='System'; Level=1,2; StartTime=(Get-Date).AddHours(-4)}
```

## Impression

```powershell
Get-Printer
Get-PrintJob
Get-PrinterPort
Get-Service Spooler
```

## Active Directory, si le module est installé et autorisé

```powershell
Get-ADUser -Identity jdupont -Properties Enabled,LockedOut,PasswordLastSet
Get-ADGroupMember -Identity 'GG-Finance-Read'
Search-ADAccount -LockedOut
```

## Export et documentation

```powershell
Get-ComputerInfo | Out-File C:\Temp\computer-info.txt
Get-Service | Export-Csv C:\Temp\services.csv -NoTypeInformation -Encoding UTF8
Start-Transcript -Path C:\Temp\session.txt
Stop-Transcript
```

Attention : un transcript peut contenir des renseignements sensibles. Stocke-le et partage-le selon les règles de l'entreprise.

## Pipeline utile

```powershell
Get-Service |
  Where-Object Status -eq 'Running' |
  Sort-Object DisplayName |
  Select-Object Name, DisplayName, Status
```

## Bonnes pratiques

- précise la cible plutôt que d'agir sur tous les objets;
- capture l'état avant et après;
- utilise des noms de variables clairs;
- gère les erreurs avec `-ErrorAction` et `try/catch` dans les scripts;
- ne place jamais de mots de passe en clair dans un script;
- signe ou contrôle les scripts selon la politique de l'organisation.

## Exercices

1. Exporte les dix processus utilisant le plus de mémoire.
2. Vérifie le DNS, la route par défaut et l'accès au port 443 d'un site.
3. Trouve les périphériques dont l'état n'est pas OK.
4. Crée un rapport texte contenant le nom du poste, l'OS, l'espace disque et l'adresse IP.
