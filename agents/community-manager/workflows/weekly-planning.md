# Workflow : Planification Hebdomadaire

## Declencheur
- Automatique : dimanche 20h00
- Manuel : "planification semaine", "contenu semaine", "plan editorial", "que poster cette semaine"

## Pre-requis
- Config : `config/editorial-calendar.json`, `config/sources.json`, `config/brand-voice.json`
- Memoire : `memory/topics-used.json`, `memory/performance-log.json`

## Etapes

### Etape 1 — Analyser le contexte

1. Determiner les dates de la semaine a venir (lundi a vendredi)
2. Charger `memory/topics-used.json` : lister les sujets des 30 derniers jours
3. Charger `memory/performance-log.json` : identifier les formats/sujets les plus performants
4. Scanner les sources hebdomadaires pour les tendances a venir :
   - Agenda economique de la semaine (BCE, Fed, publications)
   - Evenements sectoriels (conferences, publications rapports)
   - Tendances de fond identifiees

### Etape 2 — Attribuer les formats

Selon `config/editorial-calendar.json` :

| Jour      | Format LinkedIn | Newsletter | Twitter        | Instagram |
|-----------|-----------------|------------|----------------|-----------|
| Lundi     | A               | Oui        | Condensed-A    | Non       |
| Mardi     | C               | Non        | Condensed-C    | Oui       |
| Mercredi  | B               | Non        | Condensed-B    | Non       |
| Jeudi     | B ou C          | Non        | Reactif        | Oui       |
| Vendredi  | A ou B          | Non        | Condense       | Non       |

Pour jeudi et vendredi, choisir le format selon :
- L'actualite prevue (resultats, publications)
- L'equilibre de la semaine (eviter 2x le meme format consecutif)
- Les performances passees des formats

### Etape 3 — Proposer les angles

Pour chaque jour, proposer :
- **Sujet principal** : angle precis et differentiant
- **Source probable** : quelle source alimentera le contenu
- **Hook envisage** : premiere ligne d'accroche
- **Lien avec la newsletter** (si lundi) : comment le post s'articule avec la NL

Verifications :
- [ ] Aucun sujet deja traite dans les 15 derniers jours
- [ ] Diversite des themes (pas que dette privee, pas que SCPI)
- [ ] Au moins 1 post avec donnee chiffree inedite
- [ ] Au moins 1 post avec angle contre-intuitif
- [ ] Coherence d'ensemble de la semaine

### Etape 4 — Planifier la newsletter

Structure de la newsletter du lundi :
1. **Edito** (100 mots) : sujet principal de la semaine, angle editorial
2. **Analyse 1** : approfondissement du post LinkedIn du lundi
3. **Analyse 2** : deuxieme sujet complementaire
4. **Donnee cle** : chiffre marquant de la semaine avec contexte
5. **CTA** : abonnement ou partage

### Etape 5 — Generer le plan

Output format :

```
📅 PLAN EDITORIAL — Semaine du {date_lundi} au {date_vendredi}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📌 LUNDI — Format A (Chronique marche) + Newsletter
Sujet : {sujet}
Angle : {angle}
Hook : "{hook}"
Source : {source}
Newsletter : {lien avec NL}

📌 MARDI — Format C (Decryptage pratique) + Instagram
Sujet : {sujet}
Angle : {angle}
Hook : "{hook}"
Instagram : {description visuel}

📌 MERCREDI — Format B (Insight contre-intuitif)
Sujet : {sujet}
Angle : {angle}
Hook : "{hook}"
Idee recue ciblee : {idee recue}

📌 JEUDI — Format {B/C} + Instagram
Sujet : {sujet}
Angle : {angle}
Hook : "{hook}"
Instagram : {description visuel}

📌 VENDREDI — Format {A/B}
Sujet : {sujet}
Angle : {angle}
Hook : "{hook}"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📰 NEWSLETTER — Lundi 8h
Edito : {sujet edito}
Analyse 1 : {sujet}
Analyse 2 : {sujet}
Donnee cle : {chiffre}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Etape 6 — Validation et ajustements

1. Presenter le plan pour validation
2. Accepter les modifications demandees
3. Une fois valide, le plan sert de reference pour les daily-drafts de la semaine
