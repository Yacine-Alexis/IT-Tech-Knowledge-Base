# Guide de préparation — Entrevue Technicien(ne) IT

*Prépare-toi domaine par domaine. Chaque section a : les concepts clés, ce qu'on te demandera concrètement, et des questions d'entrevue types avec réponses courtes.*

---

## 1. TCP/IP

**Les bases**
- TCP/IP = la pile de protocoles qui fait fonctionner Internet et les réseaux locaux.
- 4 couches pratiques à connaître : **Accès réseau** (Ethernet/Wi-Fi) → **Internet** (IP) → **Transport** (TCP/UDP) → **Application** (HTTP, DNS, etc.).
- **Adresse IP** : identifiant unique d'un appareil sur un réseau (ex. `192.168.1.10`).
- **Masque de sous-réseau** : détermine quelle partie de l'IP est le réseau vs l'hôte (ex. `255.255.255.0` = /24).
- **Passerelle par défaut (gateway)** : la porte de sortie vers d'autres réseaux/Internet.
- **IP privée vs publique** : privées (10.x, 172.16-31.x, 192.168.x) ne sont pas routables sur Internet directement.
- **TCP vs UDP** : TCP = fiable, avec accusé de réception (poignée de main à 3 temps) — utilisé pour HTTP, email, transferts de fichiers. UDP = rapide, sans garantie — utilisé pour streaming, VoIP, jeux.
- **Ports courants à mémoriser** : 20/21 FTP, 22 SSH, 23 Telnet, 25 SMTP, 53 DNS, 67/68 DHCP, 80 HTTP, 110 POP3, 143 IMAP, 443 HTTPS, 445 SMB, 3389 RDP.

**Ce qu'on te demandera de faire**
- Expliquer ce qu'est une adresse IP, un masque, une passerelle.
- Utiliser `ipconfig` (Windows) / `ip addr` (Linux) pour voir la config réseau d'un poste.
- Faire un `ping` et un `tracert`/`traceroute` pour diagnostiquer une panne.
- Comprendre pourquoi deux appareils sur des sous-réseaux différents ne se voient pas sans routeur.

**Questions type**
- *Quelle est la différence entre TCP et UDP ?*
- *Comment fais-tu pour vérifier si un poste a une connexion réseau fonctionnelle ?* → `ping` la passerelle, puis un site externe, puis `ipconfig /all`.
- *Un utilisateur ne peut pas accéder à Internet mais peut accéder aux fichiers partagés du bureau — par où commences-tu ?* → Vérifier DNS d'abord (le partage local peut fonctionner sans DNS si résolu par nom NetBIOS/cache, mais Internet dépend fortement du DNS).

---

## 2. DNS (Domain Name System)

**Les bases**
- DNS traduit les noms de domaine (`google.com`) en adresses IP.
- **Serveur DNS** : répond aux requêtes de résolution de noms.
- Types d'enregistrements clés : **A** (nom → IPv4), **AAAA** (nom → IPv6), **CNAME** (alias), **MX** (serveur de courriel), **PTR** (IP → nom, résolution inverse), **TXT** (vérification/SPF).
- Dans un environnement AD, le DNS est presque toujours hébergé sur le contrôleur de domaine — AD *dépend* du DNS pour localiser les autres DC et pour l'authentification Kerberos.
- **Cache DNS** : Windows garde les résolutions en mémoire (`ipconfig /displaydns`) ; on le vide avec `ipconfig /flushdns`.

**Ce qu'on te demandera de faire**
- Diagnostiquer "je ne peux pas ouvrir de sites web" vs "je ne peux pas pinger une IP mais pas un nom" (= problème DNS).
- Utiliser `nslookup` ou `dig` pour tester la résolution.
- Vider le cache DNS pour régler des problèmes de résolution périmée.

**Questions type**
- *Un utilisateur dit "Internet ne fonctionne pas" mais peut pinger 8.8.8.8. Quelle est la cause probable ?* → Problème DNS. Ping par IP fonctionne, donc la connectivité est bonne ; c'est la résolution de noms qui échoue.
- *Que fait un enregistrement MX ?* → Indique quel serveur reçoit les courriels pour un domaine.

---

## 3. DHCP (Dynamic Host Configuration Protocol)

**Les bases**
- DHCP attribue automatiquement une IP, un masque, une passerelle et des serveurs DNS aux appareils qui se connectent au réseau.
- Processus **DORA** : **D**iscover (le client cherche un serveur DHCP) → **O**ffer (le serveur propose une IP) → **R**equest (le client la demande) → **A**cknowledge (le serveur confirme).
- **Bail (lease)** : durée pendant laquelle l'IP est réservée à l'appareil ; se renouvelle automatiquement.
- **Réservation DHCP** : on fixe une IP précise pour une adresse MAC donnée (utile pour imprimantes, serveurs).
- **Étendue (scope)** : la plage d'IP que le serveur DHCP peut distribuer.
- Sans DHCP, il faut configurer chaque poste manuellement (IP statique) — impensable à grande échelle.

**Ce qu'on te demandera de faire**
- Reconnaître une IP en `169.254.x.x` (APIPA) = le poste n'a pas pu contacter de serveur DHCP.
- Faire `ipconfig /release` puis `ipconfig /renew` pour forcer une nouvelle demande d'IP.
- Créer une réservation DHCP pour un appareil qui doit toujours avoir la même IP.

**Questions type**
- *Un poste a une adresse 169.254.x.x, que se passe-t-il ?* → Le DHCP n'est pas accessible ; le poste s'est auto-attribué une adresse APIPA.
- *Quelle est la différence entre une IP statique et une IP dynamique ?*

---

## 4. VPN (Virtual Private Network)

**Les bases**
- Un VPN crée un tunnel chiffré entre un appareil et un réseau distant, comme si l'appareil était physiquement sur ce réseau.
- Utilisé pour le télétravail (accès sécurisé aux ressources de l'entreprise) et pour relier deux sites (site-à-site).
- Protocoles courants : **IPsec**, **SSL/TLS VPN** (souvent via un portail web ou client comme AnyConnect/FortiClient), **WireGuard** (plus récent, léger).
- **Split tunneling** : seul le trafic destiné au réseau de l'entreprise passe par le VPN ; le reste (Netflix, etc.) sort directement par Internet.
- **Full tunneling** : tout le trafic passe par le VPN.

**Ce qu'on te demandera de faire**
- Aider un utilisateur à se connecter/dépanner un client VPN (identifiants, certificat expiré, MFA).
- Comprendre pourquoi un utilisateur en VPN peut avoir un accès plus lent ou ne pas voir l'imprimante locale (à cause du split/full tunneling).

**Questions type**
- *Pourquoi une entreprise utiliserait-elle un VPN pour ses employés en télétravail ?*
- *Qu'est-ce que le split tunneling ?*

*(Note : tu as déjà de l'expérience concrète ici — ton serveur Linux personnel avec accès distant sécurisé via Tailscale. Tailscale utilise WireGuard. C'est un excellent exemple à donner en entrevue : "j'ai mis en place un accès distant sécurisé chez moi avec Tailscale/WireGuard.")*

---

## 5. Réseaux LAN

**Les bases**
- **LAN** (Local Area Network) : réseau local, un bureau, un bâtiment.
- **Switch** : relie les appareils d'un même réseau, opère au niveau 2 (adresses MAC).
- **Routeur** : relie des réseaux différents entre eux, opère au niveau 3 (IP).
- **VLAN** (Virtual LAN) : segmente un réseau physique en plusieurs réseaux logiques séparés (ex. VLAN pour les employés, VLAN pour les invités) — améliore la sécurité et la gestion du trafic.
- **Topologies** : étoile (la plus commune aujourd'hui, tout passe par un switch central).
- **Adresse MAC** : identifiant physique unique d'une carte réseau.
- **Collision domain vs broadcast domain** : les switches réduisent les collisions ; les VLAN/routeurs limitent les domaines de diffusion.

**Ce qu'on te demandera de faire**
- Brancher/dépanner un poste sur le réseau (câble, port switch, voyants).
- Comprendre un plan d'adressage IP simple d'une petite entreprise.
- Identifier un problème physique (câble débranché) vs logique (config IP).

**Questions type**
- *Quelle est la différence entre un switch et un routeur ?*
- *Pourquoi utiliser des VLAN ?*

---

## 6. Active Directory (voir aussi ton guide précédent)

**Rappel condensé**
- Domaine, contrôleur de domaine (DC), OU, objets, groupes de sécurité, GPO, Kerberos, LDAP.
- Tâches courantes : réinitialiser mot de passe, débloquer un compte, ajouter à un groupe, créer/désactiver un utilisateur via **ADUC**.
- GPO = règles poussées automatiquement (verrouillage écran, restrictions USB, lecteurs réseau mappés).

**Lien avec le reste du guide**
- AD dépend du **DNS** pour fonctionner (localiser les DC).
- AD distribue souvent la config réseau via **DHCP** en complément.
- Les utilisateurs AD se connectent souvent à **Microsoft 365** via la synchronisation Azure AD Connect (identité hybride).

---

## 7. Microsoft 365

**Les bases**
- Suite infonuagique de Microsoft : Outlook (courriel), Teams, SharePoint, OneDrive, Word/Excel/PowerPoint en ligne.
- **Centre d'administration Microsoft 365** : où un technicien gère les comptes, licences, mots de passe, boîtes courriel.
- **Azure AD (Microsoft Entra ID)** : l'annuaire "cloud" équivalent à Active Directory, souvent synchronisé avec l'AD on-premise via **Azure AD Connect**.
- **Licences** : chaque utilisateur a besoin d'une licence (E1, E3, Business Standard, etc.) pour accéder aux services.
- **MFA (authentification multifacteur)** : quasi systématique en entreprise aujourd'hui — un technicien doit savoir réinitialiser/reconfigurer le MFA d'un utilisateur.
- **OneDrive/SharePoint** : stockage et partage de fichiers dans le nuage, remplace de plus en plus les partages réseau locaux.

**Ce qu'on te demandera de faire**
- Créer un utilisateur, assigner une licence, réinitialiser un mot de passe dans le portail admin M365.
- Dépanner Outlook (profil corrompu, synchronisation, cache).
- Aider un utilisateur bloqué par le MFA (nouveau téléphone, code perdu).

**Questions type**
- *Quelle est la différence entre Active Directory et Azure AD / Entra ID ?* → AD est on-premise (contrôleur de domaine local), Azure AD/Entra ID est dans le nuage ; beaucoup d'entreprises ont les deux, synchronisés.
- *Comment gères-tu un utilisateur qui a perdu l'accès à son MFA ?*

---

## 8. Soutien technique

**Diagnostic de problèmes**
- Méthode structurée à connaître par cœur (on te la demandera presque certainement) :
  1. **Identifier** le problème (poser des questions précises, reproduire si possible)
  2. **Établir une théorie** de la cause probable
  3. **Tester** la théorie
  4. **Établir un plan d'action** et l'exécuter
  5. **Vérifier** que le problème est résolu et prévenir la récurrence
  6. **Documenter** la solution

**Soutien aux utilisateurs**
- Communication claire, patience, éviter le jargon avec un utilisateur non-technique.
- Prise de contrôle à distance (TeamViewer, AnyDesk, Assistance rapide Windows, Intune).
- Gestion des tickets (souvent via un système comme ServiceNow, Jira Service Desk, Freshservice — mentionne que tu es à l'aise d'apprendre n'importe lequel).

**Installation de logiciels**
- Installation manuelle vs déploiement automatisé (via GPO, Intune, SCCM).
- Vérifier les prérequis, compatibilité, licences.

**Configuration de postes de travail**
- Imagerie/déploiement d'un nouveau poste, jonction au domaine, profils utilisateurs, pilotes, mises à jour Windows.
- Configuration de l'accès aux imprimantes, lecteurs réseau, VPN.

**Documentation technique**
- Rédiger des procédures claires (comment réinitialiser tel système, comment configurer tel logiciel).
- Tenir à jour une base de connaissances (wiki interne) pour que d'autres techniciens puissent réutiliser tes solutions.

**Questions type**
- *Décris ta méthode pour résoudre un problème technique que tu ne connais pas.*
- *Un utilisateur frustré t'appelle parce que son imprimante ne fonctionne pas — comment gères-tu l'appel ?*
- *Pourquoi la documentation est-elle importante dans un rôle de soutien technique ?*

---

## 9. Serveurs et sécurité

**Administration Linux**
- Commandes de base : `ls`, `cd`, `cat`, `grep`, `chmod`/`chown` (permissions), `systemctl` (gérer les services), `top`/`htop` (surveiller les ressources), `apt`/`yum` (gestion de paquets), `ssh` (accès distant).
- Gestion des utilisateurs (`useradd`, `passwd`), des services, des logs (`/var/log`).
- *Tu as un net avantage ici* : ton serveur Ollama/OpenWebUI est de l'admin Linux concrète — mentionne-le.

**Accès distant sécurisé**
- **SSH** (Linux) et **RDP** (Windows) pour l'accès distant.
- Bonnes pratiques : authentification par clé plutôt que mot de passe (SSH), MFA, VPN pour restreindre l'accès, désactiver les comptes/ports inutilisés.
- Ton expérience avec **Tailscale** est directement pertinente ici — accès distant sans exposer de ports publiquement (zero-trust mesh VPN).

**Gestion des mises à jour**
- Windows Update / WSUS en entreprise pour contrôler le déploiement des correctifs (patch management).
- Sur Linux : `apt update && apt upgrade`, ou gestion via des outils comme Ansible pour plusieurs serveurs.
- Importance des mises à jour de sécurité (correctifs pour vulnérabilités connues).

**Surveillance de services**
- Vérifier qu'un service tourne (`systemctl status`, Gestionnaire des tâches/Services sur Windows).
- Outils de monitoring (Zabbix, Nagios, PRTG, ou simplement les journaux d'événements Windows / `/var/log` sur Linux).
- Alertes en cas de panne (espace disque plein, service arrêté, CPU élevé).

**Notions de sécurité réseau**
- **Pare-feu (firewall)** : filtre le trafic entrant/sortant selon des règles.
- **Antivirus/EDR** : protection des postes contre les logiciels malveillants.
- **Principe du moindre privilège** : donner seulement les accès nécessaires à chaque utilisateur.
- **Phishing** : reconnaître et signaler les courriels suspects — souvent la première ligne de défense en soutien technique.
- **Chiffrement** : HTTPS, VPN, BitLocker (chiffrement de disque Windows).
- **Sauvegardes** : règle 3-2-1 (3 copies, 2 supports différents, 1 hors site).

**Questions type**
- *Comment sécurises-tu un accès distant à un serveur ?*
- *Que fais-tu si tu reçois un courriel qui ressemble à du phishing ?*
- *Pourquoi les mises à jour de sécurité sont-elles importantes, et quel est le risque de trop attendre avant de les appliquer ?*
- *Parle-moi d'un projet technique personnel.* → **C'est ta question en or.** Décris ton serveur Linux (Ollama/OpenWebUI) avec accès distant sécurisé via Tailscale : ça touche admin Linux, sécurité réseau, accès distant, et gestion de service — presque toute la section 9 en un seul projet concret.

---

## 10. Plan d'étude suggéré (avant l'entrevue)

1. **Jour 1-2** — Réseaux (TCP/IP, DNS, DHCP, LAN) : revois les concepts, pratique `ipconfig`, `ping`, `nslookup`, `tracert` sur ton propre poste.
2. **Jour 3** — Active Directory : si possible, monte le labo Windows Server suggéré précédemment (VM + AD DS + quelques utilisateurs/OU/GPO).
3. **Jour 4** — Microsoft 365 : explore un compte d'essai ou le centre d'admin si tu y as accès ; comprends la différence AD vs Azure AD.
4. **Jour 5** — Soutien technique : mémorise la méthode de diagnostic en 6 étapes, prépare 2-3 histoires concrètes (même scolaires ou personnelles) où tu as résolu un problème.
5. **Jour 6** — Serveurs et sécurité : révise ton projet Linux/Tailscale en détail — sois capable de l'expliquer techniquement en 2 minutes.
6. **Veille de l'entrevue** — Relis ce guide au complet, prépare 3-4 questions à poser à l'employeur (sur l'équipe, les outils utilisés, le type de tickets).

---

## Astuce générale pour l'entrevue

Pour presque chaque sujet technique, ramène la conversation vers ton projet personnel (serveur Linux + Ollama + Tailscale) quand c'est pertinent — ça prouve une expérience pratique réelle, même sans emploi IT antérieur. Les employeurs pour un poste d'entrée valorisent souvent la curiosité démontrée autant que les connaissances mémorisées.