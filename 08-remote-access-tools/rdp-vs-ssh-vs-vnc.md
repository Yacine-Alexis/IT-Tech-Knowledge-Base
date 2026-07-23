# RDP, SSH et VNC — comparaison

## RDP

- bureau graphique Windows;
- port courant 3389;
- chiffrement et Network Level Authentication;
- peut créer ou reprendre une session selon configuration;
- adapté à l'administration Windows et aux utilisateurs distants.

Risques : exposition directe à Internet, mots de passe faibles, comptes privilégiés et règles de pare-feu trop larges. Préfère VPN, passerelle RDP, MFA et accès limité.

## SSH

- terminal distant, surtout Linux/Unix;
- port courant 22;
- tunnels, transfert SFTP/SCP et automatisation;
- authentification par clé recommandée;
- faible bande passante.

Bonnes pratiques : clés protégées, désactivation du login root direct selon politique, MFA ou bastion, journalisation et restriction réseau.

## VNC

- partage d'écran multi-plateforme;
- souvent port 5900 et suivants;
- montre généralement la session console;
- sécurité varie selon implémentation;
- doit souvent être encapsulé dans un VPN ou SSH.

## Tableau

| Critère | RDP | SSH | VNC |
|---|---|---|---|
| Interface | Graphique | Ligne de commande | Graphique |
| Plateforme cible typique | Windows | Linux/Unix | Multiple |
| Bande passante | Moyenne | Faible | Moyenne à élevée |
| Automatisation | Limitée | Excellente | Faible |
| Session console | Selon mode | Non graphique | Souvent oui |
| Sécurisation | NLA, TLS, VPN/gateway | Clés, bastion, MFA | Dépend du produit; tunnel recommandé |

## Diagnostic commun

1. résolution DNS;
2. connectivité et route;
3. port accessible;
4. service actif;
5. pare-feu;
6. identité et autorisation;
7. certificat ou clé;
8. politiques de session;
9. ressources de la machine distante.

Tests :

```powershell
Test-NetConnection server -Port 3389
Test-NetConnection server -Port 22
```

```bash
ssh -vvv user@server
nc -vz server 22
```

Les logs verbeux SSH peuvent contenir noms et chemins, mais ne devraient pas afficher la clé privée.

## Choisir l'outil

- administration Linux : SSH;
- bureau Windows d'entreprise : RDP via architecture sécurisée;
- assistance à l'utilisateur : outil de support interactif avec consentement;
- appareil sans RDP mais interface graphique : VNC sécurisé ou outil approuvé.

## Exercice

Explique pourquoi ouvrir 3389 directement sur un routeur domestique est moins sûr qu'utiliser Tailscale ou un VPN puis RDP.
