# Journal des leçons apprises

## Comment l'utiliser

Ajoute une entrée chaque fois qu'un projet casse, qu'une hypothèse est fausse ou qu'une amélioration fonctionne. Ce journal devient une source d'exemples pour les entrevues.

## Modèle d'entrée

### [Date] — [Titre court]

**Contexte**  
Quel système, quelle version et quel objectif?

**Symptôme**  
Qu'est-ce qui était visible? Message exact, heure, portée.

**Impact**  
Qu'est-ce qui ne fonctionnait plus?

**Changement récent**  
Qu'est-ce qui avait changé avant le problème?

**Hypothèses initiales**

1. 
2. 
3. 

**Tests et résultats**

```text
Commande/test 1 → résultat
Commande/test 2 → résultat
Commande/test 3 → résultat
```

**Cause confirmée**  
Quelle preuve confirme la cause?

**Correction**  
Qu'as-tu changé? Quelle sauvegarde ou quel retour arrière?

**Validation**  
Quels tests prouvent que le service fonctionne?

**Prévention**  
Monitoring, documentation, changement de configuration ou automatisation.

**Ce que j'ai appris**  
Concept technique et méthode.

**Version entrevue STAR**

- Situation :
- Tâche :
- Action :
- Résultat :

---

## Entrées suggérées

- Open WebUI ne rejoint pas Ollama;
- erreur de variable `OLLAMA_BASE_URL`;
- port Docker déjà utilisé;
- logs Docker trop volumineux;
- accès Tailscale fonctionne par IP mais pas par nom;
- mise à jour qui casse une dépendance;
- permission de volume;
- service qui ne repart pas après reboot;
- sauvegarde restaurée avec succès;
- diagnostic d'un problème DNS ou DHCP dans ton réseau.

## Règle de qualité

Ne transforme pas l'entrée en histoire parfaite. Mentionne les erreurs de raisonnement et ce qui t'a fait changer d'hypothèse. C'est souvent la partie la plus crédible en entrevue.
