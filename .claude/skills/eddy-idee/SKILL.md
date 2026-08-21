---
name: eddy-idee
description: Orchestrateur principal du run. Produit 4 idées de vidéos par pilier, les fait juger, écrit celles qui passent dans Notion.
---

# eddy-idee

Tu es l'orchestrateur unique appelé à chaque déclenchement du routine "eddy-ia-lab-idees". Ce run n'a aucune mémoire d'un run précédent — tout ce dont tu as besoin vient soit du repo (BRIEF.md, ROTATION.md, SOURCES.md, VOICE.md, AUDIENCE.md, signaux.json), soit de Notion (voir eddy-notion/SKILL.md).

## Étapes, dans l'ordre

### 1. État de la base

Applique eddy-notion/SKILL.md, section "Lire l'état de la base". Récupère le compte total de pages et l'historique des 15 derniers jours. Détermine si tu es en mode amorçage (< 30 pages).

### 2. Fraîcheur des signaux

Vérifie `signaux.json` à la racine du repo. S'il est absent ou vieux de plus de 20h, applique eddy-radar/SKILL.md avant de continuer. Sinon, charge-le directement.

### 3. Répartition du run

Ouvre ROTATION.md, trouve le créneau le plus proche de l'heure locale actuelle, note combien d'idées produire par pilier pour ce run (total 4, sauf créneaux à 4 piliers représentés différemment — suis le tableau exactement).

### 4. Génération par pilier

Pour chaque idée à produire dans ce run :
- Si mode amorçage : pioche un sujet non encore utilisé dans BRIEF.md → Matrice de démarrage, pour le pilier concerné.
- Sinon : pioche un signal non encore exploité dans `signaux.json` correspondant au pilier concerné, en priorisant les signaux "force: fort".
- Compare au préalable à l'historique 15 jours (étape 1) pour écarter tout ce qui redite un angle déjà traité.
- Transforme le signal ou le sujet d'amorçage en angle concret (une phrase : de quoi parle la vidéo, quel problème elle résout ou quel fait elle montre).
- Applique eddy-titre/SKILL.md pour produire le titre final.

### 5. Jugement

Pour chaque idée produite à l'étape 4, invoque le sous-agent `juge-editorial` (voir .claude/agents/juge-editorial.md) avec eddy-juge/SKILL.md comme grille. Lance les jugements en parallèle si plusieurs idées sont prêtes en même temps.

### 6. Écriture

Pour chaque idée qui passe le seuil de 70, applique eddy-notion/SKILL.md pour l'écrire. Les idées rejetées ne sont ni écrites ni loggées ailleurs que dans le résumé de fin de run.

### 7. Résumé de fin de run

Termine par un résumé court : nombre d'idées produites, nombre retenues, nombre rejetées et pourquoi en une ligne chacune, mode (amorçage ou normal), et si la veille a été relancée ce run.

## Règle de repli

Si à un moment une étape échoue (signal introuvable, Notion indisponible), ne bloque jamais tout le run : passe à l'idée suivante et note l'échec dans le résumé final.
