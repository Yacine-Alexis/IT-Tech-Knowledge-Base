# Arbres de dépannage réseau

## Principe

Un bon diagnostic avance du plus local au plus distant et du plus simple au plus complexe. À chaque étape, note le résultat avant de continuer.

## « Je n'ai pas Internet »

```text
1. Le problème touche-t-il un seul appareil?
   ├─ Non → vérifier panne générale, routeur, commutateur, FAI, DHCP/DNS central.
   └─ Oui
      2. L'interface est-elle connectée?
         ├─ Non → câble, Wi-Fi activé, mode avion, port de commutateur, pilote.
         └─ Oui
            3. L'adresse IP est-elle valide?
               ├─ 169.254.x.x → échec DHCP; tester câble/VLAN/DHCP, renouveler le bail.
               ├─ aucune adresse → interface/pilote/configuration.
               └─ adresse attendue
                  4. Ping de la boucle locale et de sa propre IP.
                  5. Ping de la passerelle.
                     ├─ échec → couche locale, masque, VLAN, Wi-Fi, pare-feu.
                     └─ succès
                        6. Ping d'une IP externe autorisée.
                           ├─ échec → route, pare-feu, passerelle, FAI.
                           └─ succès
                              7. Résolution d'un nom avec nslookup.
                                 ├─ échec → DNS.
                                 └─ succès → navigateur, proxy, certificat, application.
```

Commandes :

```powershell
ipconfig /all
ping 127.0.0.1
ping <adresse_du_poste>
ping <passerelle>
nslookup example.com
tracert example.com
Test-NetConnection example.com -Port 443
```

## « Le partage réseau ne fonctionne pas »

```text
1. Le nom du partage et les droits sont-ils exacts?
2. Le serveur se résout-il par DNS?
3. Le serveur répond-il sur le réseau?
4. Le port SMB 445 est-il accessible?
5. Le service de partage est-il disponible?
6. L'utilisateur est-il authentifié avec le bon compte?
7. Permissions de partage ET NTFS permettent-elles l'accès?
8. Le lecteur mappé utilise-t-il d'anciennes informations d'identification?
```

Tests :

```powershell
Resolve-DnsName server01
Test-NetConnection server01 -Port 445
Get-SmbConnection
net use
whoami /groups
```

## « Un site web précis ne fonctionne pas »

1. Teste un autre site.
2. Teste le site depuis un autre appareil ou réseau autorisé.
3. Résous son nom avec `nslookup`.
4. Teste le port 443.
5. Vérifie date et heure du poste.
6. Essaie une fenêtre privée pour éliminer cache et extensions.
7. Vérifie proxy, filtrage DNS, pare-feu et certificat.
8. Consulte l'état du fournisseur si l'accès Internet général fonctionne.

## « L'appareil est lent sur le réseau »

- compare filaire et Wi-Fi;
- mesure latence, pertes et débit, sans conclure avec un seul test;
- vérifie utilisation CPU/disque, synchronisation OneDrive et mises à jour;
- vérifie duplex/vitesse du lien et signal Wi-Fi;
- cherche un transfert important ou une saturation;
- compare avec un autre appareil au même endroit.

## « Deux postes ne communiquent pas »

1. Confirme les adresses et masques.
2. Détermine s'ils sont dans le même sous-réseau.
3. S'ils sont séparés, vérifie passerelles et routage inter-VLAN.
4. Vérifie le pare-feu du poste de destination.
5. Teste le port réel plutôt que seulement `ping`.
6. Vérifie que le service écoute sur la bonne interface.

## Ce qu'il faut documenter

- heure et étendue de la panne;
- configuration IP;
- résultats des tests;
- chemin ou équipement où le test commence à échouer;
- changement effectué;
- validation utilisateur.

## Scénarios de pratique

1. Le poste reçoit `169.254.12.8`.
2. `ping 1.1.1.1` fonctionne mais `nslookup example.com` échoue.
3. Un nom se résout, mais `Test-NetConnection serveur -Port 445` expire.
4. Tout fonctionne sur câble, mais pas sur Wi-Fi.

Pour chacun, écris trois hypothèses, un test par hypothèse et un critère d'escalade.
