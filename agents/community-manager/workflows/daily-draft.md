# Workflow : Daily Draft

## Declencheur
- Automatique : tous les jours a 5h00
- Manuel : "post du jour", "draft LinkedIn", "que poster aujourd'hui"

## Pre-requis
- Acces aux fichiers : `config/editorial-calendar.json`, `config/brand-voice.json`, `config/sources.json`
- Memoire : `memory/topics-used.json`, `memory/posts-history.json`

## Etapes

### Etape 1 — Determiner le format du jour

1. Lire la date du jour (YYYY-MM-DD)
2. Determiner le jour de la semaine
3. Consulter `config/editorial-calendar.json` pour identifier :
   - Le format LinkedIn (A, B, C, ou B_or_C / A_or_B)
   - Si c'est un jour newsletter
   - Le format Twitter associe
   - Si c'est un jour Instagram
4. Si le format est `B_or_C` ou `A_or_B`, choisir en fonction de l'actualite

### Etape 2 — Scanner les sources editoriales

1. Charger `config/sources.json`
2. Pour chaque source quotidienne :
   - Identifier les 3-5 actualites les plus pertinentes
   - Filtrer selon les mots-cles definis
   - Evaluer la pertinence pour la cible CGP/FO
3. Classer les actualites par potentiel editorial :
   - Priorite 1 : Donnee chiffree nouvelle + impact direct alternatifs
   - Priorite 2 : Tendance de fond confirmee par plusieurs sources
   - Priorite 3 : Evenement marche notable

### Etape 3 — Verifier l'anti-repetition

1. Charger `memory/topics-used.json`
2. Lister les sujets traites sur les 15 derniers jours
3. Eliminer tout angle deja couvert recemment
4. Si l'actualite du jour recoupe un sujet recent, trouver un angle differentiant

### Etape 4 — Rediger le draft

1. Charger `config/brand-voice.json`
2. Charger le template du format du jour (`templates/format-A.md`, `format-B.md`, ou `format-C.md`)
3. Rediger le post en respectant :
   - La structure du format choisi
   - Le ton et le style definis dans brand-voice
   - La longueur : 150-400 mots pour LinkedIn
   - Un hook fort sur la premiere ligne (utiliser les hook_patterns)
   - Une terminaison par question ou CTA engageant
   - 3-5 hashtags pertinents
4. Generer la version Twitter condensee (280 chars max)

### Etape 5 — Generer l'output

Ecrire le draft dans `outputs/daily_post_draft.json` au format :

```json
{
  "date": "2024-01-15",
  "jour": "lundi",
  "canal": "linkedin",
  "format": "A",
  "format_nom": "Chronique marche",
  "hook": "La premiere ligne accrocheuse du post",
  "contenu": "Le corps complet du post LinkedIn, avec paragraphes structures...",
  "cta": "La question ou le CTA final",
  "hashtags": ["#Alternatives", "#CGP", "#DettePrivee"],
  "source": "Boursorama — collecte SCPI T3 2024",
  "source_url": "https://...",
  "twitter_version": "Version condensee en 280 chars max avec lien",
  "newsletter_jour": false,
  "instagram_jour": false,
  "statut": "draft",
  "genere_a": "05:00"
}
```

### Etape 6 — Mettre a jour la memoire

1. Ajouter le sujet du jour a `memory/topics-used.json` :
```json
{
  "date": "2024-01-15",
  "sujet": "Collecte SCPI en baisse de 40% au T3",
  "format": "A",
  "angle": "Comparaison avec la dette privee immobiliere",
  "source": "ASPIM"
}
```

## Criteres de qualite du draft

- [ ] Hook fort et accrocheur sur la 1ere ligne
- [ ] Au moins 1 donnee chiffree sourcee
- [ ] Aucune mention de Global Icons
- [ ] Ton expert et independant (pas commercial)
- [ ] Longueur entre 150 et 400 mots
- [ ] Se termine par une question ou un CTA
- [ ] 3-5 hashtags pertinents
- [ ] Sujet non traite dans les 15 derniers jours
- [ ] Version Twitter generee (< 280 chars)
