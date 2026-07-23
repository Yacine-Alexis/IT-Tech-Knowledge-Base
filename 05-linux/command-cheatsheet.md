# Commandes Linux pour technicien IT

## Principe de travail

Commence par observer, puis modifie. Lis l'aide avec `man`, `--help` ou `info`. Évite d'exécuter une commande avec `sudo` tant que tu ne comprends pas exactement sa cible et son effet.

## Navigation et fichiers

```bash
pwd                         # dossier actuel
ls -lah                     # contenu détaillé, y compris caché
cd /var/log                 # changer de dossier
find /etc -name '*.conf'    # rechercher par nom
locate sshd_config          # recherche via index, si disponible
file myfile                 # type de fichier
stat myfile                 # métadonnées
```

Lire et filtrer :

```bash
cat file.txt
less file.txt
tail -n 50 /var/log/syslog
tail -f /var/log/syslog
head -n 20 file.txt
grep -i 'error' file.txt
grep -Rin 'listen' /etc/nginx
```

## Création, copie et suppression

```bash
touch notes.txt
mkdir -p lab/logs
cp source.txt destination.txt
cp -a source-dir backup-dir
mv oldname newname
rm file.txt
rmdir empty-dir
```

`rm -rf` peut supprimer récursivement sans confirmation. Ne l'utilise pas par habitude. Vérifie `pwd`, utilise un chemin précis et liste la cible avant toute suppression.

## Utilisateurs et identité

```bash
whoami
id
getent passwd username
getent group groupname
who
w
last
sudo -l
```

Administration, si autorisée :

```bash
sudo adduser username
sudo passwd username
sudo usermod -aG groupname username
```

Le `-a` est important avec `usermod -aG`; sans lui, tu peux remplacer les groupes secondaires existants.

## Permissions

```bash
ls -l
namei -l /path/to/file
chmod u+x script.sh
chmod 640 secret.txt
chown user:group file.txt
getfacl /path
setfacl -m u:username:r-- /path/file
```

Lecture de `rwxr-x---` : propriétaire `rwx`, groupe `r-x`, autres `---`.

## Processus et ressources

```bash
ps aux
ps -ef
top
htop
pgrep -a nginx
free -h
df -h
du -sh /var/* 2>/dev/null
uptime
```

Terminer un processus :

```bash
kill PID
kill -TERM PID
kill -KILL PID
```

Utilise d'abord `TERM` pour permettre un arrêt propre. `KILL` est un dernier recours.

## Réseau

```bash
ip address
ip route
ip neigh
ping -c 4 gateway
traceroute example.com
ss -tulpn
resolvectl status
getent hosts example.com
dig example.com
curl -I https://example.com
nc -vz server 443
```

## Services et journaux

```bash
systemctl status ssh
systemctl is-enabled ssh
journalctl -u ssh --since '1 hour ago'
journalctl -p err..alert -b
```

## Stockage et montage

```bash
lsblk -f
findmnt
mount | column -t
blkid
```

Ne monte, démonte ou repartitionne pas un disque sans sauvegarde et sans identifier précisément le périphérique.

## Archives et transferts

```bash
tar -czf logs.tar.gz /var/log/app
tar -xzf logs.tar.gz
scp file.txt user@server:/tmp/
rsync -avh --dry-run source/ user@server:/backup/
```

Fais d'abord un `--dry-run` avec `rsync` lorsqu'une suppression ou synchronisation importante est possible.

## Aide et historique

```bash
man systemctl
systemctl --help
history
history | grep ssh
```

L'historique peut contenir des secrets si quelqu'un les a saisis en ligne de commande. Ne le partage pas aveuglément.

## Exercices

1. Trouve les cinq dossiers les plus volumineux sous `/var` sans modifier le système.
2. Vérifie quelle application écoute sur le port 8080.
3. Trouve les erreurs du service SSH depuis le dernier démarrage.
4. Explique la différence entre `df` et `du`.
