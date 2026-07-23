# Gestion des services avec systemd

## Concepts

- **unit** : ressource gérée par systemd;
- **service unit** : processus ou application;
- **target** : groupe logique d'unités;
- **enabled** : configuré pour démarrer selon ses dépendances;
- **active** : actuellement en cours d'exécution;
- **failed** : état d'échec enregistré.

Un service peut être enabled mais inactif, ou active sans être enabled.

## Commandes essentielles

```bash
systemctl status nginx
systemctl is-active nginx
systemctl is-enabled nginx
systemctl list-units --type=service
systemctl list-units --type=service --state=failed
```

Actions, avec autorisation :

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
sudo systemctl enable nginx
sudo systemctl disable nginx
```

Préférer `reload` à `restart` si le service le supporte et si une interruption doit être évitée. Vérifie toujours la documentation du service.

## Dépannage structuré

1. `systemctl status service` pour l'état, le code de sortie et les dernières lignes.
2. `journalctl -u service` pour la chronologie.
3. Valide la configuration avant redémarrage avec l'outil de l'application.
4. Vérifie utilisateur, permissions, ports, fichiers et dépendances.
5. Compare l'état avant et après.
6. Teste le service depuis le client ou avec `curl`, `nc` ou un test applicatif.

Exemples de validation :

```bash
sudo nginx -t
sudo sshd -t
sudo apachectl configtest
```

## Journaux

```bash
journalctl -u nginx --since today
journalctl -u nginx --since '2026-07-13 08:00' --until '2026-07-13 09:00'
journalctl -u nginx -f
journalctl -xeu nginx
```

`-f` suit le journal en direct. Quitte avec `Ctrl+C`.

## Inspecter une unité

```bash
systemctl cat nginx
systemctl show nginx
systemctl list-dependencies nginx
```

Les fichiers fournis par un paquet ne devraient pas être modifiés directement si un override suffit.

## Créer un override

```bash
sudo systemctl edit nginx
```

Puis :

```bash
sudo systemctl daemon-reload
sudo systemctl restart nginx
```

Sauvegarde le contenu et prépare un retour arrière :

```bash
sudo systemctl revert nginx
```

Utilise `revert` seulement si tu comprends quels overrides seront supprimés.

## Service qui redémarre en boucle

Vérifie :

- `Restart=` et `RestartSec=`;
- code de sortie;
- fichier de configuration;
- dépendances réseau et stockage;
- secret ou variable d'environnement manquant;
- port déjà occupé;
- permission du répertoire de travail;
- limite de redémarrage atteinte.

```bash
systemctl show app.service -p Restart -p NRestarts -p ExecMainStatus
ss -ltnp
```

## Service masqué

Une unité masked ne peut pas être démarrée :

```bash
systemctl is-enabled service
```

Ne fais pas `unmask` sans connaître la raison du masquage.

## Documentation de ticket

Note unité, état, PID, code de sortie, heure, configuration testée, journal pertinent, action appliquée, interruption causée et validation.

## Exercice

Dans une VM, crée un service simple ou utilise un service non critique. Provoque une erreur de chemin, diagnostique-la avec `status` et `journalctl`, corrige-la, puis documente la cause.
