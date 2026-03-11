# Community Manager Agent — L'Allocateur

Agent IA autonome pour la gestion editoriale de **L'Allocateur**, le media de reference sur les investissements alternatifs pour CGP et Family Offices.

## Deploiement rapide

### 1. Installer comme skill Claude Code

Copier le dossier dans votre projet Claude Code :
```bash
cp -r community-manager-agent/ ~/.claude/skills/community-manager-allocateur/
```

Ou ajouter le skill dans votre configuration Claude Code en pointant vers `SKILL.md`.

### 2. Deployer sur le repo Global Icons

```bash
cd global-icons-agents
cp -r community-manager-agent/ agents/community-manager/
git add agents/community-manager/
git commit -m "feat: add community manager agent for L'Allocateur"
git push origin main
```

## Utilisation

### Commandes principales

| Commande | Description |
|----------|-------------|
| `post du jour` | Genere le draft LinkedIn du jour selon le calendrier |
| `morning briefing` | Affiche le draft pour validation |
| `planification semaine` | Genere le plan editorial de la semaine |
| `newsletter` | Redige la newsletter du lundi |
| `analyse resultats` | Bilan de performance hebdomadaire |
| `que poster aujourd'hui` | Identifie le format et propose un sujet |
| `contenu semaine` | Equivalent a `planification semaine` |

### Workflow quotidien type

1. **5h00** — `daily-draft` : l'agent scanne les sources et genere un draft
2. **7h30** — `morning-briefing` : l'agent envoie le draft pour validation
3. **Validation** : repondre "oui", "modifier + feedback", ou "refuser"
4. **Publication** : le post valide est ajoute a la queue

### Workflow hebdomadaire

1. **Dimanche 20h** — `weekly-planning` : plan de la semaine generee
2. **Lundi** — Newsletter + Post LinkedIn Format A
3. **Mardi a Vendredi** — Posts selon le calendrier
4. **Vendredi 17h** — `performance-review` : bilan hebdomadaire

## Architecture

```
community-manager-agent/
├── SKILL.md                          # Skill principal
├── config/
│   ├── editorial-calendar.json       # Rotation formats par jour
│   ├── brand-voice.json              # Ton, style, contraintes
│   ├── sources.json                  # Sources editoriales
│   └── targets.json                  # KPIs et objectifs
├── workflows/
│   ├── daily-draft.md                # Generation draft quotidien
│   ├── morning-briefing.md           # Validation Telegram
│   ├── weekly-planning.md            # Planification hebdo
│   ├── newsletter.md                 # Newsletter lundi
│   └── performance-review.md         # Analyse hebdo
├── templates/
│   ├── format-A.md                   # Chronique marche
│   ├── format-B.md                   # Insight contre-intuitif
│   └── format-C.md                   # Decryptage pratique
├── memory/
│   ├── posts-history.json            # Historique posts
│   ├── performance-log.json          # Metriques
│   └── topics-used.json              # Anti-repetition
└── outputs/
    ├── daily_post_draft.json         # Draft du jour
    └── linkedin_queue.json           # Queue planifiee
```

## Calendrier editorial

| Jour | LinkedIn | Newsletter | Twitter | Instagram |
|------|----------|------------|---------|-----------|
| Lundi | Format A | Oui | Condense-A | Non |
| Mardi | Format C | Non | Condense-C | Oui |
| Mercredi | Format B | Non | Condense-B | Non |
| Jeudi | B ou C | Non | Reactif | Oui |
| Vendredi | A ou B | Non | Condense | Non |

## Formats de contenu

- **Format A** (Chronique marche) : analyse macro, tendances alternatives, donnees
- **Format B** (Insight contre-intuitif) : idee recue deconstruite, donnees surprenantes
- **Format C** (Decryptage pratique) : guide, methodologie, explication pour CGP/FO

## Contraintes Phase 1

- ZERO mention de Global Icons
- Ton independant et analytique
- Cible exclusive : CGP et Family Offices
- Objectif : credibilite et audience avant monetisation

## KPIs

| Canal | Metrique | M+3 | M+6 | M+12 |
|-------|----------|-----|-----|------|
| Newsletter | Abonnes | 300 | 1000 | 3000 |
| LinkedIn | Engagement | >3% | >3% | >3% |
| Twitter | Followers/mois | +50 | +100 | +200 |

## Personnalisation

### Ajouter une source editoriale
Editer `config/sources.json` et ajouter l'entree dans la section appropriee.

### Modifier le ton
Editer `config/brand-voice.json` — les listes `a_eviter` et `a_privilegier`.

### Ajuster les KPIs
Editer `config/targets.json` — modifier les cibles et planchers par canal.

### Passer en Phase 2 (mention Global Icons)
Quand le moment sera venu :
1. Retirer "Global Icons" de la liste `a_eviter` dans `brand-voice.json`
2. Ajouter des templates de contenu sponsorise
3. Definir les regles de frequence de mention
