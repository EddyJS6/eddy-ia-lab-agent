# Configuration du routine cloud

Cette étape se fait à la main sur `claude.ai/code/routines` — je n'ai pas d'outil pour créer un routine cloud directement, seulement pour préparer ce qu'il contient.

## 1. Créer le routine

Sur `claude.ai/code/routines` → New Routine.

- **Nom** : `eddy-ia-lab-idees`
- **Dépôt connecté** : `EddyJS6/eddy-ia-lab-agent` (branche `main`)
- **Connecteur** : Notion (celui déjà actif sur ton compte — l'agent l'utilise directement, aucun token à saisir)
- **Déclencheur** : Scheduled → cron expression personnalisée

## 2. Cron

```
23 1,5,9,13,17,21 * * *
```

6 déclenchements par jour, décalés à la minute 23 pour éviter l'engorgement des créneaux ronds.

**Point à vérifier à la création** : confirme dans l'interface si ce cron s'évalue en UTC ou dans ton fuseau local. Si c'est en UTC et que tu es en France (UTC+1 ou +2 selon la saison), décale les heures en conséquence pour que le créneau ~5h (celui qui déclenche la veille) tombe bien tôt le matin heure de Paris — sinon la logique de "premier sur l'actu de la nuit" dans BRIEF.md perd son intérêt.

## 3. Prompt du routine

Colle exactement ceci dans le champ prompt du routine :

```
Applique le skill eddy-idee défini dans .claude/skills/eddy-idee/SKILL.md à la racine de ce repo. Suis-le à la lettre, dans l'ordre. Committe et pousse tout fichier modifié (notamment signaux.json si la veille a été relancée) à la fin du run avec un message de commit clair. Termine par le résumé de fin de run prévu par le skill.
```

## 4. Vérifications avant premier run automatique

- Lance le routine manuellement une fois depuis l'interface ("Run now") et vérifie le résumé de fin de run.
- Va voir la base Notion : les propriétés doivent être remplies proprement, le Statut doit être "Nouvelle".
- Une ligne de test "Test de connexion — à supprimer" a été ajoutée pendant la mise en place pour vérifier l'accès en écriture — supprime-la à la main, ce n'est pas une vraie idée.
- Vérifie que le nombre de pages dans Notion après ce premier run correspond à ce qui est attendu pour le mode amorçage (compteur < 30, voir BRIEF.md).

## 5. Si le plafond de runs quotidiens du plan est dépassé

Passe le cron à 3 créneaux au lieu de 6 (`23 5,13,21 * * *`) et double la répartition par pilier dans ROTATION.md pour chaque créneau — 8 idées par run au lieu de 4. Non recommandé au-delà de 6 idées d'affilée dans un même run, la qualité de fin de liste baisse.
