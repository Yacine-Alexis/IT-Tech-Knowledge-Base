# Ports et protocoles courants

## Comprendre un port

Une adresse IP identifie un appareil ou une interface; un port identifie un service réseau sur cet appareil. TCP et UDP ont chacun leurs propres espaces de ports. Le fait qu'un port soit « courant » ne garantit pas qu'il soit ouvert ou utilisé de cette façon dans un environnement donné.

## Ports à connaître

| Port | Transport | Service | Utilité et note de dépannage |
|---:|---|---|---|
| 20/21 | TCP | FTP | Transfert de fichiers ancien; non chiffré par défaut |
| 22 | TCP | SSH / SFTP | Administration Linux sécurisée et transfert chiffré |
| 23 | TCP | Telnet | Non chiffré; à éviter |
| 25 | TCP | SMTP | Relais de courriel entre serveurs |
| 53 | UDP/TCP | DNS | UDP pour la plupart des requêtes; TCP pour réponses volumineuses et transferts de zone |
| 67/68 | UDP | DHCP | Serveur 67, client 68 |
| 80 | TCP | HTTP | Web non chiffré, souvent redirigé vers HTTPS |
| 88 | TCP/UDP | Kerberos | Authentification Active Directory |
| 110 | TCP | POP3 | Récupération de courriel, souvent remplacée ou chiffrée |
| 123 | UDP | NTP | Synchronisation de l'heure |
| 135 | TCP | RPC Endpoint Mapper | Services Windows et administration distante |
| 137–139 | TCP/UDP | NetBIOS | Anciennes fonctions de noms et partage Windows |
| 143 | TCP | IMAP | Accès aux courriels côté serveur |
| 161/162 | UDP | SNMP | Supervision et alertes d'équipements |
| 389 | TCP/UDP | LDAP | Annuaire, non chiffré par défaut |
| 443 | TCP | HTTPS | Web chiffré; plusieurs VPN SSL l'utilisent aussi |
| 445 | TCP | SMB | Partages de fichiers, imprimantes et fonctions AD |
| 464 | TCP/UDP | Kerberos password | Changement de mot de passe Kerberos |
| 465/587 | TCP | SMTP sécurisé / soumission | Envoi authentifié depuis les clients |
| 514 | UDP/TCP | Syslog | Centralisation de journaux |
| 636 | TCP | LDAPS | LDAP sur TLS |
| 993 | TCP | IMAPS | IMAP chiffré |
| 995 | TCP | POP3S | POP3 chiffré |
| 1433 | TCP | Microsoft SQL Server | Base de données SQL Server |
| 3306 | TCP | MySQL/MariaDB | Base de données |
| 3389 | TCP/UDP | RDP | Bureau à distance Windows |
| 5432 | TCP | PostgreSQL | Base de données |
| 5900 | TCP | VNC | Contrôle d'écran à distance |
| 8080 | TCP | HTTP alternatif | Applications web, proxys, consoles |

## Protocoles importants sans port fixe unique

- **ICMP** : diagnostics et messages réseau, utilisé par `ping`; ce n'est pas TCP ou UDP.
- **ARP** : associe une IPv4 locale à une adresse MAC.
- **IPsec** : ensemble de protocoles pour VPN; peut utiliser ESP, AH et IKE.
- **SMB dynamique/RPC** : certaines fonctions Windows utilisent des ports dynamiques en plus de 135.

## Tester un port

Windows PowerShell :

```powershell
Test-NetConnection server01 -Port 445
Test-NetConnection 192.168.1.20 -Port 3389 -InformationLevel Detailed
```

Linux :

```bash
nc -vz server01 22
curl -I https://example.com
ss -tulpn
```

Interprétation :

- résolution de nom échouée : commence par DNS;
- hôte injoignable : vérifie route, pare-feu, VLAN et connectivité;
- connexion refusée : l'hôte répond, mais aucun service n'écoute ou le service rejette;
- délai expiré : filtrage réseau, pare-feu ou chemin interrompu possible;
- port ouvert : cela confirme seulement l'écoute réseau, pas le bon fonctionnement complet de l'application.

## Approche de dépannage

1. Confirme le nom ou l'IP de destination.
2. Vérifie la résolution DNS.
3. Vérifie la route et la connectivité.
4. Teste le port précis.
5. Vérifie le service côté serveur.
6. Examine les pare-feu locaux et réseau.
7. Valide l'application et l'authentification.

## Sécurité

N'ouvre jamais un port « pour essayer » sans connaître le flux requis, la source, la destination et le risque. Préfère une règle minimale : protocole, port, adresses autorisées et durée nécessaires.

## Exercices

- Pourquoi un partage `\\serveur\commun` peut-il échouer même si `ping serveur` fonctionne?
- Pourquoi un service HTTPS peut-il fonctionner alors que le port 80 est fermé?
- Quel test ferais-tu pour savoir si un serveur RDP répond sur le réseau?
