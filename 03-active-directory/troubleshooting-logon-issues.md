# Dépannage des problèmes d'ouverture de session AD

## Commencer par le message exact

« Mot de passe incorrect », « compte verrouillé », « aucun serveur d'ouverture de session disponible », « relation d'approbation échouée » et « profil temporaire » sont des problèmes différents. Ne les traite pas tous par une réinitialisation de mot de passe.

## Arbre rapide

1. L'utilisateur peut-il se connecter à un autre poste?
2. Un autre utilisateur peut-il se connecter au poste touché?
3. Le poste a-t-il une connectivité au réseau d'entreprise ou au VPN?
4. DNS pointe-t-il vers les serveurs AD prévus?
5. Date et heure sont-elles synchronisées?
6. Le compte est-il activé, non expiré et non verrouillé?
7. Le poste a-t-il une relation d'approbation valide?
8. Le profil local se charge-t-il correctement?

## Vérifier le compte

```powershell
Get-ADUser jdupont -Properties Enabled,LockedOut,AccountExpirationDate,PasswordExpired,PasswordLastSet
Search-ADAccount -LockedOut
```

## Vérifier le poste

```cmd
ipconfig /all
whoami
set logonserver
nltest /dsgetdc:contoso.local
w32tm /query /status
```

PowerShell :

```powershell
Test-ComputerSecureChannel -Verbose
Resolve-DnsName _ldap._tcp.dc._msdcs.contoso.local -Type SRV
```

Ne répare pas automatiquement le secure channel sans autorisation et sans comprendre l'effet sur le poste.

## Causes fréquentes

### Mot de passe récemment changé

Un téléphone, Outlook, un lecteur mappé, un service ou un VPN peut continuer d'utiliser l'ancien mot de passe et verrouiller le compte. Cherche la source du verrouillage au lieu de déverrouiller en boucle.

### Aucun serveur de connexion

- poste hors réseau et aucun cache valide;
- VPN non établi avant connexion;
- DNS externe au lieu du DNS AD;
- route/VLAN/pare-feu;
- DC ou service indisponible.

### Heure incorrecte

Kerberos dépend d'une heure suffisamment synchronisée. Vérifie la source de temps et ne règle pas manuellement l'heure comme solution permanente.

### Relation d'approbation

Peut survenir si le mot de passe du compte ordinateur et celui conservé localement ne correspondent plus, après restauration d'image ou longue désynchronisation.

### Profil temporaire

L'authentification peut réussir, mais le profil ne se charge pas. Vérifie espace disque, permissions, profil, antivirus, stockage et événements User Profile Service.

## Journaux utiles

- Security sur le poste et le DC;
- System;
- Microsoft-Windows-User Profile Service/Operational;
- GroupPolicy/Operational;
- événements de verrouillage sur le contrôleur de domaine.

## Informations à ne pas demander

Ne demande jamais à l'utilisateur de te donner son mot de passe. Tu peux lui demander d'essayer de le saisir lui-même et confirmer le message reçu.

## Exercice

Scénario : l'utilisateur peut se connecter au portail Microsoft 365, mais pas au poste du bureau après avoir changé son mot de passe à distance. Propose un ordre de tests qui distingue synchronisation, mot de passe AD, cache local, VPN et verrouillage.
