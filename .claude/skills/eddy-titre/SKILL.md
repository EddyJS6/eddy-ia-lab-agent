---
name: eddy-titre
description: Transforme un angle de vidéo en un titre français accrocheur, prêt à publier, dans la voix de Tom.
---

# eddy-titre

## Avant de générer quoi que ce soit

Lis intégralement VOICE.md et AUDIENCE.md à la racine du repo. Ce ne sont pas des références facultatives — un titre qui ne colle pas à VOICE.md doit être rejeté avant même d'atteindre le juge.

## Contraintes dures

- 45 à 60 caractères. En dessous, le titre est vague. Au-dessus, YouTube le coupe.
- Une promesse concrète et vérifiable, jamais une promesse vague ("tout comprendre", "le guide ultime")
- Aucun mot de la liste interdite de VOICE.md section "Jamais" : "boostez", "révolutionnez", "game changer", "disruptif", "débloquez votre potentiel", "transformez votre vie", et toute variante évidente de ces formules
- Pas de point d'exclamation en rafale, pas plus d'un par titre
- Pas de "tout comprendre X" ni "guide complet X" — voir BRIEF.md, Constat de marché
- Le titre doit être publiable tel quel, sans édition — pas de crochets, pas de placeholder, pas de "[insérer X]"

## Processus

1. Génère 5 variantes du titre à partir de l'angle fourni par eddy-idee.
2. Élimine celles qui violent une contrainte dure.
3. Parmi les survivantes, garde celle qui est la plus directe et la plus concrète — pas la plus putaclic. VOICE.md dit "cash" et "tranchant", pas "racoleur".
4. Vérifie une dernière fois la longueur en caractères avant de renvoyer le titre final.

## Exemples de calibrage (ton, pas sujet à copier)

Ce que le ton Tom donnerait sur ce type de sujet, à partir de VOICE.md :
- Direct, sujet-verbe-complément, pas d'adjectif en rab
- Une affirmation ou un résultat concret annoncé frontalement, jamais enrobé
- Jamais de tournure "vendeur de rêve"

Renvoie uniquement le titre final et l'angle en une phrase qui l'accompagne — c'est ce qui va dans la propriété Angle de Notion.
