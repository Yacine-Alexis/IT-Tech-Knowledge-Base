# Projet portfolio — Homelab Ollama et Open WebUI

## But du document

Transforme ton projet personnel en preuve d'expérience technique. Remplace les éléments entre crochets par tes informations réelles et conserve uniquement ce que tu peux démontrer.

## Résumé en 30 secondes

« J'ai déployé un serveur Linux personnel qui exécute Ollama et Open WebUI avec Docker Compose. J'ai configuré les volumes persistants, le redémarrage des services, la journalisation et l'accès réseau. J'utilise Tailscale pour l'administration à distance sans exposer directement les services au public. Ce projet m'a permis de pratiquer Linux, Docker, réseau, sécurité, diagnostic et documentation. »

## Architecture

```text
[Portable/PC client]
        |
   Tailscale/WireGuard
        |
[Serveur Ubuntu]
  ├─ Docker Engine
  ├─ Ollama :11434
  └─ Open WebUI :8080
       └─ volume persistant
```

Ajoute : matériel, OS, adresse locale, stockage, GPU, réseau et sauvegarde, sans publier de secrets.

## Compétences démontrées

- installation et mises à jour Linux;
- gestion des utilisateurs et permissions;
- Docker Compose;
- variables d'environnement;
- volumes persistants;
- ports et liaisons réseau;
- logs et redémarrage de services;
- accès distant sécurisé;
- surveillance CPU, RAM, GPU et disque;
- sauvegarde et restauration;
- diagnostic couche par couche.

## Checklist technique

### Système

```bash
uname -a
lsb_release -a
uptime
free -h
df -h
```

### Docker

```bash
docker compose ps
docker compose logs --tail=100
docker stats
docker inspect ollama
```

### Réseau

```bash
ss -tulpn
curl -I http://127.0.0.1:8080
curl http://127.0.0.1:11434/api/tags
```

### Santé

- conteneurs redémarrent après reboot;
- Open WebUI rejoint Ollama par le réseau Docker;
- données persistent après recréation;
- logs ne remplissent pas le disque;
- accès limité aux interfaces prévues;
- sauvegarde testée.

## Scénarios à documenter

1. Open WebUI démarre mais ne voit pas Ollama.
2. Un port est déjà utilisé.
3. Le GPU n'est pas visible dans le conteneur.
4. Le volume n'a pas les bonnes permissions.
5. Le disque se remplit à cause des modèles ou logs.
6. Une mise à jour d'image introduit une incompatibilité.

Pour chacun : symptôme, hypothèses, commandes, cause, correction, validation et prévention.

## Sécurité

- ne publie pas les ports sur Internet sans besoin;
- utilise Tailscale ou un reverse proxy correctement sécurisé;
- protège les comptes et secrets;
- mets à jour les images après test;
- fixe des limites de logs;
- sauvegarde les données importantes;
- vérifie les images et dépôts officiels;
- applique le moindre privilège.

## Présentation d'entrevue en deux minutes

1. problème ou objectif;
2. architecture;
3. ton rôle;
4. incident réel et diagnostic;
5. amélioration de sécurité;
6. ce que tu ferais ensuite.

## À compléter

- date de début :
- matériel :
- OS :
- versions :
- sauvegarde :
- monitoring :
- incident le plus intéressant :
- amélioration future :
