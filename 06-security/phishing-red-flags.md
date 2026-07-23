# Phishing — signaux d'alerte et réponse

## Objectif

Un technicien doit aider sans blâmer, préserver les preuves et réduire le risque. Aucun signe isolé ne prouve toujours une fraude; c'est la combinaison du contexte, de l'identité, du lien, de la demande et du comportement qui compte.

## Signaux d'alerte

- urgence ou menace inhabituelle;
- demande de secret, code MFA, carte-cadeau, virement ou modification bancaire;
- domaine ressemblant à un domaine légitime;
- nom d'affichage correct mais adresse différente;
- lien dont la destination ne correspond pas au texte;
- pièce jointe inattendue;
- ton ou processus inhabituel pour la personne;
- demande de contourner une procédure;
- formulaire de connexion externe inattendu;
- conversation détournée ou changement soudain de coordonnées;
- QR code qui cache la destination;
- demande MFA non sollicitée.

## Vérification sécuritaire

- ne clique pas sur le lien suspect;
- vérifie l'expéditeur par un canal connu et indépendant;
- ouvre le site via un favori ou l'adresse officielle saisie manuellement;
- compare le domaine caractère par caractère;
- utilise les outils de signalement de l'entreprise;
- transmets le message comme pièce jointe ou selon procédure pour conserver les en-têtes;
- ne réponds pas à l'expéditeur suspect.

## Si l'utilisateur n'a rien cliqué

1. rassure et remercie;
2. demande de ne pas interagir davantage;
3. recueille le message original;
4. signale à la sécurité;
5. vérifie si d'autres utilisateurs ont reçu le même message;
6. bloque ou retire seulement via les outils et autorisations appropriés;
7. documente.

## Si l'utilisateur a cliqué mais n'a rien saisi

- ferme la page;
- ne télécharge rien;
- recueille URL, heure, navigateur et comportement;
- lance les vérifications EDR approuvées;
- examine téléchargements et événements;
- escalade selon politique.

## Si des identifiants ont été saisis

Traite comme compromission potentielle :

- réinitialise le mot de passe depuis un appareil de confiance;
- révoque les sessions;
- vérifie méthodes MFA, règles de boîte, transferts et connexions;
- escalade immédiatement à la sécurité;
- recherche l'étendue et les actions après connexion;
- ne détruis pas les preuves.

## Si un fichier a été ouvert ou exécuté

- déconnecte du réseau selon procédure si l'activité est suspecte;
- ne redémarre pas aveuglément;
- note l'heure et les symptômes;
- contacte l'équipe sécurité;
- conserve l'appareil et les journaux;
- évite de copier le fichier sur d'autres systèmes.

## En-têtes utiles

Les en-têtes peuvent montrer le chemin, les résultats SPF/DKIM/DMARC et les serveurs. Ils doivent être analysés avec prudence : un message peut réussir certaines vérifications et rester malveillant.

## Communication

Ne dis pas « comment as-tu pu cliquer? ». Dis plutôt : « Merci de l'avoir signalé rapidement. Je vais sécuriser le compte et vérifier ce qui s'est passé. »

## Exercice

Crée trois exemples fictifs : fausse facture, demande de changement bancaire et fatigue MFA. Pour chacun, liste preuves à préserver, actions immédiates et équipe à contacter.
