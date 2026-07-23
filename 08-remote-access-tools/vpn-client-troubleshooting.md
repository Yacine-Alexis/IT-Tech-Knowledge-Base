# Dépannage d'un client VPN

## Déterminer le type d'échec

- application ne démarre pas;
- authentification échoue;
- MFA échoue;
- tunnel ne s'établit pas;
- tunnel établi mais ressources inaccessibles;
- Internet devient lent ou indisponible;
- déconnexions fréquentes;
- problème de certificat;
- conflit de sous-réseau local.

## Collecte

- client et version;
- OS;
- message/code exact;
- heure et fuseau;
- réseau utilisé;
- fonctionne depuis un autre réseau?
- autres utilisateurs touchés?
- changement de mot de passe ou téléphone?
- profil VPN, passerelle et groupe;
- journaux du client;
- adresse IP et routes avant/après connexion.

## Avant la connexion

```powershell
ipconfig /all
Get-NetRoute
Resolve-DnsName vpn.example.com
Test-NetConnection vpn.example.com -Port 443
```

Le port dépend du produit et du protocole.

## Tunnel établi, ressource inaccessible

1. vérifie l'adresse VPN attribuée;
2. compare routes avant/après;
3. vérifie DNS interne;
4. teste ressource par nom puis IP;
5. vérifie split tunneling;
6. vérifie pare-feu et ACL;
7. confirme autorisation utilisateur;
8. cherche chevauchement entre réseau local et réseau d'entreprise.

```powershell
route print
Get-NetIPConfiguration
Resolve-DnsName internalserver.corp
Test-NetConnection internalserver.corp -Port 445
```

## Conflit de sous-réseau

Si le domicile utilise `192.168.1.0/24` et l'entreprise aussi, le poste peut envoyer le trafic au routeur local au lieu du VPN. Un changement de réseau local temporaire peut confirmer l'hypothèse; la correction durable appartient à l'équipe réseau/VPN.

## DNS VPN

- serveurs DNS internes non appliqués;
- suffixe DNS absent;
- priorité d'interface;
- cache;
- split DNS mal configuré;
- client sécurisé qui intercepte DNS.

Vider le cache peut être un test :

```cmd
ipconfig /flushdns
```

Mais cela ne corrige pas une mauvaise politique DNS.

## MFA et certificats

- heure du poste;
- certificat expiré ou non approuvé;
- méthode MFA enregistrée;
- compte verrouillé;
- politique d'accès conditionnel;
- certificat machine ou utilisateur manquant.

Ne contourne pas un certificat en désactivant la validation TLS.

## Performance

- full tunnel;
- distance à la passerelle;
- réseau Wi-Fi;
- MTU;
- inspection de sécurité;
- saturation;
- transfert OneDrive ou mise à jour;
- débit du domicile.

## Escalade

Inclue journal client, heure, IP publique si autorisé, passerelle, code, utilisateur, réseau, routes, DNS, ressource testée et résultat. Masque les secrets.

## Exercice

Scénario : VPN connecté, accès web Internet fonctionne, mais `\\fileserver\share` échoue par nom et fonctionne par IP. Donne la cause probable et les tests.
