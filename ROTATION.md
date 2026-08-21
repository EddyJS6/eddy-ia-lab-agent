# ROTATION — répartition des 4 idées par run

Le routine tourne 6 fois par jour, une seule expression cron avec 6 heures : `23 1,5,9,13,17,21 * * *`. Chaque run produit exactement 4 idées, une par pilier sauf sur les créneaux marqués.

À chaque run, prends l'heure locale courante et choisis le créneau le plus proche dans le tableau ci-dessous. Ne bloque jamais un run parce que l'heure ne tombe pas pile — le créneau le plus proche suffit.

| Créneau | Actu Claude | Astuces/tutos | Builds perso | Builds en direct |
|---|---|---|---|---|
| ~1h | 1 | 1 | 1 | 1 |
| ~5h | 2 | 1 | 1 | 0 |
| ~9h | 1 | 2 | 1 | 0 |
| ~13h | 1 | 1 | 1 | 1 |
| ~17h | 1 | 2 | 1 | 0 |
| ~21h | 1 | 1 | 2 | 0 |

Total quotidien approximatif : Actu 7, Astuces/tutos 8, Builds perso 6, Builds en direct 2. C'est volontaire — l'actu et les astuces sont le volume de fond, les builds en direct sont un format lourd qui n'a pas besoin de sortir tous les jours.

Le créneau ~5h porte aussi la veille complète (voir eddy-radar/SKILL.md) car c'est le moment où l'actu US de la nuit est fraîche et où aucune chaîne FR n'a encore réagi.

## Mode amorçage

Cette rotation ne s'applique qu'une fois sortie du mode amorçage (30+ pages en base). En amorçage, applique quand même la répartition par pilier de ce tableau, mais pioche dans BRIEF.md → Matrice de démarrage au lieu des signaux du radar.
