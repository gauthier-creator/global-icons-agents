# Workflow : Performance Review Hebdomadaire

## Declencheur
- Automatique : vendredi 17h00
- Manuel : "analyse resultats", "performance review", "metriques", "comment ca performe"

## Pre-requis
- Memoire : `memory/performance-log.json`, `memory/posts-history.json`
- Config : `config/targets.json`
- Les metriques doivent etre alimentees (manuellement ou via API)

## Etapes

### Etape 1 — Collecter les metriques de la semaine

Pour chaque post publie cette semaine, collecter :

**LinkedIn** :
- Impressions
- Reactions (likes, celebrates, etc.)
- Commentaires
- Partages
- Taux d'engagement = (reactions + commentaires + partages) / impressions
- Clics sur le profil
- Nouveaux followers (delta semaine)

**Newsletter** :
- Nombre d'envois
- Taux d'ouverture
- Taux de clic
- Taux de desabonnement
- Nouveaux abonnes (delta semaine)

**Twitter** :
- Impressions par tweet
- Engagements (likes, RT, replies)
- Nouveaux followers (delta semaine)

**Instagram** :
- Reach par post
- Engagement (likes, commentaires, saves)
- Croissance followers

### Etape 2 — Comparer aux objectifs

Charger `config/targets.json` et comparer :

```
📊 TABLEAU DE BORD — Semaine du {date}

LINKEDIN
├── Engagement rate : {taux}% (cible: 3%) {✅/⚠️/❌}
├── Impressions moy. : {nombre} (cible: 2000) {✅/⚠️/❌}
├── Commentaires moy. : {nombre} (cible: 5) {✅/⚠️/❌}
└── Nouveaux followers : +{nombre} (cible: +50/semaine) {✅/⚠️/❌}

NEWSLETTER
├── Taux ouverture : {taux}% (cible: 45%) {✅/⚠️/❌}
├── Taux clic : {taux}% (cible: 8%) {✅/⚠️/❌}
├── Desabonnements : {taux}% (max: 2%) {✅/⚠️/❌}
└── Total abonnes : {nombre} (objectif M3: 300) {✅/⚠️/❌}

TWITTER
├── Engagement rate : {taux}% (cible: 1.5%) {✅/⚠️/❌}
└── Nouveaux followers : +{nombre} (cible: +12/semaine) {✅/⚠️/❌}

INSTAGRAM
├── Engagement rate : {taux}% (cible: 4%) {✅/⚠️/❌}
└── Reach evolution : {tendance} {✅/⚠️/❌}
```

Legende : ✅ = au-dessus de la cible / ⚠️ = entre plancher et cible / ❌ = sous le plancher

### Etape 3 — Analyser les tendances

1. **Top 3 posts de la semaine** : quels formats et sujets ont le mieux performe
2. **Flop 3 posts** : quels formats et sujets ont sous-performe
3. **Patterns identifies** :
   - Les hooks qui fonctionnent (type de hook_pattern)
   - Les sujets qui resonnent (thematiques)
   - Les jours/heures optimaux
   - La longueur optimale
4. **Tendance sur 4 semaines** : l'engagement progresse, stagne ou decline

### Etape 4 — Recommandations

Generer 3-5 recommandations actionnables :

```
🎯 RECOMMANDATIONS SEMAINE PROCHAINE

1. {recommandation — ex: "Privilegier les hooks chiffres, +40% d'engagement vs questions"}
2. {recommandation — ex: "Les posts Format B performent 2x mieux le mercredi, maintenir"}
3. {recommandation — ex: "Augmenter les posts SCPI, forte resonance aupres des CGP"}
4. {recommandation — ex: "Tester un carrousel Instagram sur la dette privee"}
5. {recommandation — ex: "Newsletter : raccourcir l'edito, les clics viennent de l'analyse 1"}
```

### Etape 5 — Mettre a jour la memoire

1. Ajouter les metriques de la semaine dans `memory/performance-log.json` :
```json
{
  "semaine": "2024-W03",
  "date_debut": "2024-01-15",
  "date_fin": "2024-01-19",
  "linkedin": {
    "posts": 3,
    "engagement_moyen": 0.034,
    "impressions_moyennes": 2400,
    "meilleur_post": { "date": "...", "sujet": "...", "format": "B", "engagement": 0.052 },
    "nouveaux_followers": 48
  },
  "newsletter": {
    "envois": 1,
    "taux_ouverture": 0.47,
    "taux_clic": 0.09,
    "nouveaux_abonnes": 23,
    "total_abonnes": 156
  },
  "twitter": {
    "tweets": 5,
    "engagement_moyen": 0.018,
    "nouveaux_followers": 14
  },
  "instagram": {
    "posts": 2,
    "engagement_moyen": 0.045,
    "reach_moyen": 340
  },
  "recommandations": ["..."],
  "alertes": ["..."]
}
```

2. Mettre a jour `config/editorial-calendar.json` si des ajustements strategiques sont necessaires

### Etape 6 — Rapport de synthese

Generer un rapport court (200 mots max) a envoyer via Telegram :

```
📊 BILAN SEMAINE {numero}

LinkedIn : {engagement}% engagement (cible 3%) {emoji}
Newsletter : {ouverture}% ouverture, +{abonnes} abonnes {emoji}
Twitter : +{followers} followers {emoji}
Instagram : {engagement}% engagement {emoji}

🏆 Best : "{sujet meilleur post}" — {engagement}%
📉 Flop : "{sujet pire post}" — {engagement}%

🎯 Actions S+1 :
1. {action}
2. {action}
3. {action}
```

## Declenchement des alertes

Si un KPI passe sous le plancher defini dans `targets.json`, generer une alerte immediate :

```
⚠️ ALERTE PERFORMANCE

{kpi} est passe sous le plancher ({valeur} vs {plancher}).

Cause probable : {analyse}
Action recommandee : {action}
```
