# Projet portfolio — Accès distant avec Tailscale

## Résumé

Tailscale crée un réseau privé maillé basé sur WireGuard et une gestion d'identité. Dans ton portfolio, explique l'objectif, la configuration, les contrôles d'accès, les tests et les choix de sécurité sans publier de clés ou d'informations sensibles.

## Objectif

Accéder à ton serveur Linux depuis tes appareils autorisés sans redirection de port publique et sans exposer SSH, Open WebUI ou d'autres services directement sur Internet.

## Architecture à documenter

```text
[Mac/PC/iPhone autorisé]
          |
   réseau Tailscale chiffré
          |
[Serveur Ubuntu : IP Tailscale]
  ├─ SSH
  └─ services internes autorisés
```

## Installation et état

Selon le système et la procédure officielle :

```bash
tailscale status
tailscale ip -4
tailscale ping <device-name>
```

Évite d'inscrire une auth key dans un script, une capture ou un dépôt Git.

## Tests

1. confirmer appareil visible dans la console;
2. vérifier IP Tailscale;
3. tester `tailscale ping`;
4. tester SSH par nom MagicDNS ou IP;
5. tester le port du service;
6. confirmer que le port n'est pas exposé publiquement;
7. tester depuis un autre réseau, par exemple cellulaire;
8. vérifier comportement après redémarrage.

## Contrôles de sécurité

- comptes protégés par MFA;
- appareils approuvés;
- clés et appareils expirés ou révoqués lorsque nécessaire;
- ACL ou grants limitant les flux;
- tags gérés correctement;
- SSH Tailscale ou SSH classique choisi consciemment;
- mises à jour du client;
- journalisation et revue des appareils;
- pas d'accès plus large que nécessaire.

## Concepts à expliquer

### Pas de port forwarding

Le service n'a pas besoin d'être publié sur l'adresse publique du routeur. Cela réduit l'exposition directe, mais ne remplace pas la sécurité du service, des comptes et des appareils.

### MagicDNS

Permet de résoudre les noms des appareils du tailnet. Un problème par nom mais pas par IP peut orienter vers DNS ou configuration de nom.

### Subnet router

Un appareil peut annoncer des routes vers un réseau derrière lui. Cela élargit l'accès et doit être contrôlé par routes et ACL. N'annonce pas un sous-réseau sans comprendre qui pourra l'atteindre.

### Exit node

Peut acheminer le trafic Internet d'un client via un appareil. Cela diffère de l'accès à un service interne et peut affecter performance, géolocalisation et politiques.

## Scénarios de dépannage

- appareil offline;
- connexion directe impossible, relais utilisé;
- ACL refuse le flux;
- service écoute seulement sur localhost;
- firewall local bloque l'interface Tailscale;
- MagicDNS échoue;
- route de sous-réseau non approuvée;
- compte ou appareil expiré.

## Histoire d'entrevue

« Je voulais accéder à mon serveur sans ouvrir SSH sur Internet. J'ai déployé Tailscale, vérifié les flux avec `tailscale ping`, SSH et les ports applicatifs, puis limité l'accès aux appareils autorisés. J'ai appris à distinguer disponibilité du tunnel, résolution de noms, pare-feu et service d'application. »

## À compléter

- appareils autorisés :
- règles d'accès :
- services accessibles :
- méthode SSH :
- test de non-exposition publique :
- incident rencontré :
- amélioration future :
