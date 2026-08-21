# Eddy IA Lab — agent à idées de vidéos

Agent autonome qui alimente en continu la base Notion "Eddy IA Lab → Idées de vidéos" avec des idées de vidéos prêtes à publier, sans intervention manuelle.

## Comment ça marche

Un unique routine cloud Claude Code (`claude.ai/code/routines`) clone ce repo et exécute le skill `eddy-idee` 6 fois par jour. Chaque run produit 4 idées de vidéos (une par pilier en général), les fait juger par un sous-agent en contexte vierge, et écrit dans Notion celles qui passent le seuil de qualité.

Voir [ROUTINE_SETUP.md](./ROUTINE_SETUP.md) pour la configuration exacte du routine.

## Structure

```
BRIEF.md          identité de la chaîne, les 4 piliers, interdits, matrice de démarrage
VOICE.md          ton et règles de copywriting (copié depuis Agence IA)
AUDIENCE.md       cible et langage de l'audience (copié depuis Agence IA)
SOURCES.md        requêtes de veille et chaînes de calibrage
ROTATION.md       répartition des piliers par créneau horaire
signaux.json      cache de veille, régénéré automatiquement toutes les ~20h

.claude/skills/
  eddy-idee/       orchestrateur principal, appelé à chaque run
  eddy-radar/       instructions de veille, déclenchées si signaux.json est périmé
  eddy-titre/       règles de copywriting des titres
  eddy-juge/        grille de notation
  eddy-notion/      lecture/écriture Notion, dédoublonnage

.claude/agents/
  veilleur-yt.md      benchmark YouTube FR/EN
  veilleur-actu.md    changelog Anthropic, Reddit, X, Hacker News
  juge-editorial.md   note chaque idée en contexte vierge
```

## Ce que l'agent ne fait jamais

- N'utilise aucun MCP tiers de recherche YouTube — uniquement WebSearch/WebFetch (refus explicite du propriétaire)
- N'écrit jamais une idée sous le seuil de qualité de 70/100
- Ne propose jamais de sujet supposant une équipe, un plateau ou un budget — la chaîne est tenue en solo

Voir [BRIEF.md](./BRIEF.md) pour le détail complet.
