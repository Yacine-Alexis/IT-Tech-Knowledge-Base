# Journaux Linux — emplacements et méthode

## Deux modèles principaux

- **systemd journal** : consulté avec `journalctl`;
- **fichiers texte** : souvent dans `/var/log`.

Selon la distribution et l'application, un événement peut être dans l'un, l'autre ou les deux.

## Emplacements fréquents

| Emplacement | Contenu typique |
|---|---|
| `/var/log/syslog` | messages généraux sur Debian/Ubuntu |
| `/var/log/messages` | messages généraux sur RHEL-like |
| `/var/log/auth.log` | authentification Debian/Ubuntu |
| `/var/log/secure` | authentification RHEL-like |
| `/var/log/kern.log` | noyau, selon distribution |
| `/var/log/dmesg` | messages de démarrage, selon système |
| `/var/log/apt/` | opérations APT |
| `/var/log/dnf.log` | opérations DNF |
| `/var/log/nginx/` | accès et erreurs Nginx |
| `/var/log/apache2/` ou `/var/log/httpd/` | Apache |
| `/var/log/audit/audit.log` | auditd, si activé |
| `/var/log/cron` | tâches cron, selon distribution |
| `/var/log/containers/` | certains environnements de conteneurs |

## Journal systemd

```bash
journalctl -b                     # depuis le démarrage courant
journalctl -b -1                  # démarrage précédent
journalctl -p warning..alert      # niveaux élevés
journalctl -u ssh --since today
journalctl --since '30 min ago'
journalctl -k                     # noyau
journalctl -f                     # suivi en direct
```

## Chercher efficacement

```bash
grep -iE 'error|fail|denied' /var/log/app.log
zgrep -i 'error' /var/log/app.log*.gz
awk '$1 == "ERROR" {print}' app.log
```

Ne te limite pas au mot « error ». Cherche l'heure exacte, l'identifiant de requête, le nom utilisateur, l'adresse IP et les événements juste avant et après.

## Rotation

`logrotate` archive, compresse et supprime les anciens fichiers selon une politique. Les fichiers peuvent devenir `.1`, `.2.gz`, etc.

```bash
ls -lh /var/log/app*
cat /etc/logrotate.conf
ls /etc/logrotate.d/
```

Ne modifie pas la rétention sans comprendre les besoins de conformité et d'espace disque.

## Permissions et données sensibles

Les journaux peuvent contenir : noms, adresses IP, chemins, jetons, URL et données personnelles. Ne copie pas un journal complet dans un ticket public. Extrais le minimum utile et masque les secrets.

## Disque plein à cause des journaux

1. vérifie `df -h` et `du`;
2. identifie le fichier qui grossit;
3. détermine pourquoi l'application écrit autant;
4. sauvegarde l'extrait utile;
5. corrige la cause ou la rotation;
6. libère l'espace selon une procédure approuvée;
7. vérifie si un processus garde un fichier supprimé ouvert.

```bash
sudo lsof +L1
journalctl --disk-usage
```

Évite de vider un journal avec `> file.log` sans validation, surtout lors d'un incident.

## Construire une chronologie

- normalise le fuseau horaire;
- relève heure système avec `timedatectl`;
- combine application, proxy, authentification, système et réseau;
- distingue première erreur et erreurs secondaires;
- conserve les lignes originales avec contexte.

## Exercice

Trouve le dernier échec de connexion SSH dans une VM, note l'heure, l'adresse source, la méthode et les lignes voisines. Explique ce qui est un fait et ce qui reste une hypothèse.
