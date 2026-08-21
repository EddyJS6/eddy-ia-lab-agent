---
name: eddy-radar
description: Instructions de veille pour les sous-agents veilleur-yt et veilleur-actu. Utilisée uniquement quand signaux.json est absent ou daté de plus de 20h.
---

# eddy-radar

## Quand cette veille se déclenche

L'orchestrateur (eddy-idee) vérifie en début de run si `signaux.json` existe à la racine du repo et si son champ `generated_at` a moins de 20 heures. Si oui, réutilise le fichier tel quel, ignore ce skill. Si non (absent, ou plus de 20h), lance ce skill avant de produire des idées — c'est la veille qui alimente les runs suivants pour les prochaines ~20h.

Ce mécanisme remplace un déclenchement par horaire fixe : il est robuste même si un run est en retard ou sauté.

## Répartition du travail

Lance en parallèle les deux sous-agents `veilleur-yt` et `veilleur-actu` (voir .claude/agents/). Chacun revient avec une liste de signaux structurés. N'exécute jamais cette veille dans l'agent principal — c'est volumineux et ça doit rester isolé.

## Format attendu de signaux.json

```json
{
  "generated_at": "2026-08-21T05:23:00Z",
  "signaux": [
    {
      "pilier_suggere": "Actu Claude",
      "resume": "une phrase décrivant le signal",
      "source_url": "https://...",
      "pourquoi_maintenant": "ce qui rend ce signal périssable",
      "force": "fort | moyen"
    }
  ]
}
```

Vise 15 à 25 signaux par génération, répartis sur les 4 piliers, pour couvrir les runs suivants jusqu'à la prochaine veille.

## Après génération

Écris le fichier `signaux.json` à la racine du repo et commit-le (le routine doit committer ses changements de fichiers pour que le run suivant les retrouve au clone). Message de commit : `chore: refresh signaux.json`.
