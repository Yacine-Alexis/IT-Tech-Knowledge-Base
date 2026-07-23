# Gestion des paquets Linux selon les distributions

## Familles principales

| Famille | Format | Outil courant | Exemples |
|---|---|---|---|
| Debian | `.deb` | `apt`, `dpkg` | Debian, Ubuntu |
| Red Hat | `.rpm` | `dnf`, `rpm` | RHEL, Fedora, Rocky, AlmaLinux |
| SUSE | `.rpm` | `zypper` | openSUSE, SLES |
| Arch | `.pkg.tar.*` | `pacman` | Arch Linux |

Des formats applicatifs comme Snap, Flatpak et conteneurs peuvent coexister avec le gestionnaire système.

## Debian/Ubuntu

```bash
sudo apt update
apt list --upgradable
sudo apt upgrade
apt search nginx
apt show nginx
dpkg -l | grep nginx
sudo apt install nginx
sudo apt remove nginx
sudo apt purge nginx
```

`update` rafraîchit les métadonnées; `upgrade` installe les versions disponibles. `purge` supprime aussi les fichiers de configuration gérés par le paquet, donc utilise-le prudemment.

## RHEL/Fedora et dérivés

```bash
sudo dnf check-update
dnf search nginx
dnf info nginx
rpm -qa | grep nginx
sudo dnf install nginx
sudo dnf upgrade
sudo dnf remove nginx
```

## SUSE

```bash
sudo zypper refresh
zypper search nginx
zypper info nginx
sudo zypper install nginx
sudo zypper update
```

## Arch

```bash
sudo pacman -Syu
pacman -Ss nginx
pacman -Qi nginx
sudo pacman -S nginx
sudo pacman -R nginx
```

Ne mélange pas des instructions d'une distribution avec une autre.

## Vérifier l'origine d'un fichier

Debian :

```bash
dpkg -S /usr/bin/curl
```

RPM :

```bash
rpm -qf /usr/bin/curl
```

## Avant une mise à jour

- confirme la distribution et la version;
- lis les notes de version pour un serveur critique;
- vérifie les dépôts configurés;
- contrôle l'espace disque;
- sauvegarde configuration et données;
- prévois interruption et retour arrière;
- teste sur un environnement pilote;
- vérifie après redémarrage si un nouveau noyau est installé.

## Dépôts et clés

N'ajoute pas un dépôt tiers ou une clé de signature parce qu'un tutoriel le demande. Valide l'éditeur, l'URL, la clé, la compatibilité et la politique de l'entreprise.

## Dépendances et paquets retenus

Les gestionnaires résolvent les dépendances, mais un conflit peut bloquer une mise à jour. Ne force pas une suppression de dépendance critique sans analyse.

Debian :

```bash
apt-mark showhold
apt-cache policy package-name
```

RHEL-like :

```bash
dnf repolist
dnf history
```

## Après installation

- vérifie le fichier de configuration;
- démarre et active le service seulement si nécessaire;
- ouvre uniquement les ports requis;
- consulte les journaux;
- teste l'application;
- documente la version.

## Exercice

Sur ta distribution, trouve la version installée de Docker ou Nginx, le dépôt d'origine, les fichiers fournis par le paquet et l'historique de la dernière mise à jour.
