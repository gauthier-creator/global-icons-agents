# Workflow : Newsletter Hebdomadaire

## Declencheur
- Automatique : lundi (apres validation du draft LinkedIn)
- Manuel : "newsletter", "newsletter lundi", "rediger la newsletter"

## Pre-requis
- Draft LinkedIn du lundi valide (`outputs/daily_post_draft.json`)
- Plan de la semaine si disponible
- Config : `config/brand-voice.json`
- Memoire : `memory/posts-history.json`, `memory/topics-used.json`

## Specifications

- **Longueur** : 600-1000 mots
- **Envoi** : Lundi 8h
- **Phase 1** : Aucune mention de Global Icons
- **Ton** : Plus approfondi que LinkedIn, valeur ajoutee exclusive

## Structure de la newsletter

### 1. Objet du mail (Subject line)
- Court, percutant, suscite la curiosite
- Patterns efficaces :
  - Chiffre + contexte : "SCPI : -40% de collecte, et maintenant ?"
  - Question : "La dette privee va-t-elle remplacer le fonds euros ?"
  - Constat : "Ce que les CGP ignorent sur le secondaire PE"
- Longueur max : 60 caracteres
- Eviter : "Newsletter #12", "Actu de la semaine"

### 2. Edito (100 mots)
- Introduction personnelle et editoriale
- Donne le ton de la semaine
- Pose la problematique centrale
- Voix : "nous" ou impersonnel
- Transition vers les analyses

### 3. Analyse principale (250-350 mots)
- Reprend et APPROFONDIT le post LinkedIn du lundi
- Ajoute des donnees supplementaires
- Developpe l'argumentation
- Cite des sources complementaires
- Inclut au moins 2 donnees chiffrees

### 4. Analyse secondaire (200-300 mots)
- Sujet complementaire (pas de redite)
- Peut etre :
  - Un decryptage d'une publication recente
  - Une tendance de fond sous-estimee
  - Un comparatif sectoriel
- Au moins 1 donnee chiffree

### 5. Donnee cle de la semaine (50-100 mots)
- Un chiffre marquant presente visuellement
- Contexte en 2-3 phrases
- Pourquoi c'est important pour un CGP/FO
- Format :
  ```
  📊 LE CHIFFRE : {chiffre}
  {contexte et implication}
  ```

### 6. CTA final (50 mots)
- Deux options en rotation :
  - **CTA partage** : "Si cette analyse vous a ete utile, partagez-la a un confrere."
  - **CTA engagement** : question ouverte invitant a repondre au mail
- Jamais de CTA commercial (Phase 1)

## Template de sortie

```
Objet : {subject_line}

---

{edito — 100 mots}

---

## {titre_analyse_1}

{analyse_principale — 250-350 mots}

---

## {titre_analyse_2}

{analyse_secondaire — 200-300 mots}

---

📊 LE CHIFFRE DE LA SEMAINE

{donnee_cle — chiffre en gros + contexte}

---

{cta_final}

---

L'Allocateur — L'essentiel des investissements alternatifs, chaque lundi.
```

## Checklist qualite

- [ ] Objet < 60 caracteres, accrocheur
- [ ] Edito : 100 mots, pose la problematique
- [ ] Analyse 1 : approfondit le post LinkedIn, 250-350 mots
- [ ] Analyse 2 : sujet different, 200-300 mots
- [ ] Au moins 3 donnees chiffrees au total
- [ ] Sources citees
- [ ] Donnee cle percutante
- [ ] CTA non commercial
- [ ] ZERO mention Global Icons
- [ ] Ton expert, independant, pas promotionnel
- [ ] Total : 600-1000 mots
- [ ] Preview-text optimise (40 premiers mots)
