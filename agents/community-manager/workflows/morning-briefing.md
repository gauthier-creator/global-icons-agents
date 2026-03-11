# Workflow : Morning Briefing

## Declencheur
- Automatique : tous les jours a 7h30
- Manuel : "morning briefing", "validation du post", "valider le draft"

## Pre-requis
- Draft genere : `outputs/daily_post_draft.json` (doit exister et etre au statut "draft")

## Etapes

### Etape 1 — Lire le draft du jour

1. Charger `outputs/daily_post_draft.json`
2. Verifier que le statut est "draft"
3. Si pas de draft disponible, generer une alerte

### Etape 2 — Generer le message de validation

Composer un message court pour validation (format Telegram / chat) :

```
📋 DRAFT DU JOUR — {date} ({jour})

📌 Format : {format} — {format_nom}
📰 Source : {source}

🔹 Hook :
"{hook}"

🔹 CTA :
"{cta}"

🔹 Longueur : {nombre_mots} mots
🔹 Hashtags : {hashtags}

🐦 Twitter :
"{twitter_version}"

---
✅ Valider (oui)
✏️ Modifier (non + feedback)
❌ Refuser (refuser + raison)
```

### Etape 3 — Attendre la reponse

Trois reponses possibles :

#### Reponse : "oui" / "valide" / "ok"
1. Mettre a jour `outputs/daily_post_draft.json` → statut: "valide"
2. Ajouter le post a `outputs/linkedin_queue.json`
3. Ajouter le sujet a `memory/topics-used.json` si pas deja fait
4. Confirmer : "Post valide et ajoute a la queue de publication."

#### Reponse : "non" / "modifier" + feedback
1. Prendre en compte le feedback
2. Re-generer le draft avec les modifications
3. Mettre a jour `outputs/daily_post_draft.json`
4. Renvoyer le nouveau message de validation
5. Retourner a l'etape 3

#### Reponse : "refuser" + raison
1. Mettre a jour `outputs/daily_post_draft.json` → statut: "refuse"
2. Logger la raison dans `memory/posts-history.json`
3. Proposer un draft alternatif avec un angle different
4. Retourner a l'etape 2

### Etape 4 — Mise a jour de la queue

Si le post est valide, l'ajouter a `outputs/linkedin_queue.json` :

```json
{
  "posts": [
    {
      "date": "2024-01-15",
      "canal": "linkedin",
      "contenu_complet": "...",
      "hashtags": ["..."],
      "statut": "planifie",
      "heure_publication": "08:30",
      "valide_a": "07:45",
      "twitter_version": "..."
    }
  ]
}
```

## Notes
- Le briefing doit etre envoye meme si aucun draft n'a ete genere (message d'alerte)
- Garder un historique des modifications demandees pour ameliorer les futurs drafts
- Maximum 2 rounds de modification avant de proposer un angle completement different
