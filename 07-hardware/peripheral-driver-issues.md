# Périphériques et pilotes

## Symptômes

- périphérique absent;
- point d'exclamation dans le Gestionnaire de périphériques;
- déconnexion aléatoire;
- fonction partielle;
- code d'erreur;
- problème après mise à jour;
- fonctionne sur un autre port ou poste.

## Méthode

1. identifie exactement le périphérique et son modèle;
2. vérifie alimentation, câble, port et adaptateur;
3. teste un autre port ou câble connu fonctionnel;
4. teste le périphérique sur un autre poste si possible;
5. vérifie Gestionnaire de périphériques et événements;
6. relève Hardware IDs et version du pilote;
7. installe ou restaure un pilote approuvé;
8. vérifie micrologiciel et compatibilité;
9. teste la fonction réelle.

## PowerShell

```powershell
Get-PnpDevice
Get-PnpDevice | Where-Object Status -ne 'OK'
Get-PnpDeviceProperty -InstanceId '<instance-id>'
Get-CimInstance Win32_PnPSignedDriver | Select-Object DeviceName, DriverVersion, Manufacturer
```

## Codes fréquents

Le Gestionnaire de périphériques peut afficher des codes comme 10, 28 ou 43. Le code oriente le diagnostic, mais lis toujours le texte et le contexte : pilote absent, périphérique impossible à démarrer, erreur signalée par le matériel, etc.

## USB

- puissance insuffisante;
- concentrateur ou station d'accueil;
- câble charge seulement;
- économie d'énergie;
- contrôleur USB;
- périphérique trop ancien;
- conflit après veille.

Teste directement sur le poste avant de conclure que le périphérique est défectueux.

## Bluetooth

- radio activée;
- mode appairage;
- ancien jumelage;
- batterie;
- interférences;
- service Bluetooth;
- pilote;
- profil supporté, par exemple audio ou HID.

## Stations d'accueil

Un problème de dock peut toucher affichage, réseau, USB et charge. Vérifie alimentation du dock, câble hôte, firmware, pilote graphique, compatibilité USB-C/Thunderbolt et tests sans dock.

## Pilote après mise à jour

- compare date et version;
- cherche un rollback disponible;
- utilise le package fabricant/entreprise;
- évite les outils automatiques de pilotes non approuvés;
- documente si le problème touche plusieurs modèles.

## Firmware

Une mise à jour de firmware comporte plus de risque qu'un pilote. Assure alimentation stable, chiffrement/clé de récupération, sauvegarde et procédure fabricant.

## Exercice

Scénario : une webcam USB fonctionne sur un autre poste, mais apparaît avec code 10 sur le poste de l'utilisateur. Écris les tests du moins risqué au plus intrusif.
