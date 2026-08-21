---
name: eddy-notion
description: Écrit une idée de vidéo validée dans la base Notion Eddy IA Lab, avec dédoublonnage et lecture de l'historique récent.
---

# eddy-notion

## Identifiants fixes

- Data source Notion : `collection://58e7a55f-1788-43c9-82b3-b1d288dd6361`
- Titre de la base : "Idées de vidéos", sous la page "Eddy IA Lab"

Ne jamais rechercher cette base par recherche à chaque run — utilise directement cet ID pour économiser des appels.

## Lire l'état de la base (à faire en tout début de run)

Utilise l'outil de requête Notion en mode SQL sur la data source ci-dessus pour récupérer en une seule fois :
1. Le nombre total de pages (`SELECT COUNT(*) FROM "collection://58e7a55f-1788-43c9-82b3-b1d288dd6361"`) — détermine si on est encore en mode amorçage (< 30, voir BRIEF.md).
2. Les titres, piliers et angles des pages créées dans les 15 derniers jours (`WHERE datetime("Date d'ajout") > datetime('now', '-15 days')`) — sert de base anti-doublon pour eddy-idee et eddy-titre.

## Écrire une idée validée

Une seule page par idée retenue par le juge (score au-dessus du seuil, voir eddy-juge/SKILL.md). N'écris jamais une idée rejetée.

Propriétés à remplir, toutes obligatoires sauf Source :
- **Titre** — le titre final choisi par eddy-titre, prêt à publier tel quel
- **Statut** — toujours "Nouvelle" à la création
- **Pilier** — un des 4 piliers exacts de BRIEF.md
- **Format** — "Long" ou "Short"
- **Angle** — une phrase, l'angle qui rend ce titre différent d'un titre générique
- **Pourquoi maintenant** — ce qui rend l'idée périssable ou urgente (une actu qui vient de sortir, un signal détecté) ; si l'idée vient du mode amorçage, écrire "Idée de lancement — positionnement de chaîne"
- **Source** — l'URL de la vidéo ou de la page qui a inspiré le signal, si applicable ; laisser vide en mode amorçage
- **Score** — la note du juge sur 100

## Dédoublonnage

Avant d'écrire, compare le titre et l'angle proposés à l'historique des 15 derniers jours récupéré plus haut. Si un titre ou un angle est trop proche (même sujet, même angle, formulation différente), ne l'écris pas — redemande une idée différente à eddy-idee plutôt que d'insérer un quasi-doublon.

## En cas d'échec d'écriture

Si l'appel Notion échoue, réessaie une fois. Si l'échec persiste, ne bloque pas le reste du run : log l'échec dans la sortie du run et continue avec l'idée suivante.
