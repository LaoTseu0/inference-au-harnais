# La forme d'une leçon

Ce fichier fixe ce qu'est une leçon et comment elle s'écrit. Il ne fixe ni
l'ordre du cours ni la couverture des notions : c'est le rôle de
[cartographie.md](cartographie.md).

## Finalité et public

Le cours s'adresse à un développeur full stack expérimenté en JavaScript, avec
des bases en Java et une pratique récente de Python.

Il poursuit un seul résultat : comprendre les mécanismes qui relient un modèle de
langage à un harnais agentique.

Le cours n'est pas une démonstration jetable. Chaque Parcours produit une
connaissance vérifiable.

## Ce que « maîtriser » veut dire

Le cours ouvre toute boîte noire dont le mécanisme change une décision de
conception, une limite ou un risque.

Lorsqu'un mécanisme est hors de portée — pilote GPU, pile TLS, moteur de base de
données — la leçon ouvre le contrat et les garanties de la dépendance, puis
**marque explicitement la frontière**. Elle ne fait pas semblant de l'expliquer.

Un outil ne tient jamais lieu de concept. Ollama, llama.cpp, vLLM, LangGraph,
Temporal ou Qdrant servent d'études de cas **après** l'explication du mécanisme
qu'ils matérialisent.

## Un seul concept

Une leçon ouvre une seule pièce. Elle peut montrer ses relations, mais ne
réenseigne pas les pièces voisines. Une notion majeure possède sa propre leçon.
Une notion secondaire tient en quelques lignes ou rejoint le glossaire.

La cartographie fixe ce que chaque leçon doit couvrir. Une notion ne peut pas
disparaître pendant la rédaction : elle reste attachée à sa leçon, devient une
partie explicitement rattachée à une autre, ou devient une entrée de glossaire.

## Termes techniques et glossaire

Un terme ou un mot-clé technique qui exige une définition pour comprendre le
cours possède une entrée dans `glossaire/`. Cette entrée conserve le terme
consacré et donne sa définition en français simple.

Dans le corps de chaque leçon :

1. la première occurrence du terme porte un lien vers son entrée de glossaire ;
2. les occurrences suivantes dans cette même leçon sont en gras, sans lien.

La règle recommence dans chaque leçon. Elle rend la définition accessible au
premier emploi sans multiplier les liens dans le reste du texte.

## Frontmatter

```yaml
---
id: logits-softmax
type: leçon
titre: Des logits à une distribution
parcours: 0-generation
statut: brouillon
tags: [generation, sampling]
created: 2026-08-17
updated: 2026-08-17
verified: 2026-08-17
---
```

- `id` est stable et unique. Il est repris de la cartographie et ne change plus
  une fois la leçon publiée ;
- `parcours` correspond à une rubrique de la cartographie ;
- `statut` vaut `brouillon`, `en-revue` ou `validé` ;
- `updated` change à chaque modification éditoriale ;
- `verified` date la dernière vérification des sources mouvantes.

## Squelette

```markdown
---
<Frontmatter complet>
---

# Titre

## Prérequis

## Savoir le situer

## Connaissances

## Références
```

Les quatre rubriques sont obligatoires.

Dans une leçon destinée à Obsidian, une formule intégrée à une phrase utilise
`$...$` et une formule en bloc utilise `$$...$$`. Les délimiteurs `\(...\)` et
`\[...\]` ne sont pas utilisés.

## Prérequis

Cette rubrique contient seulement les notions réellement nécessaires, sous forme
de liens courts.

Une dépendance non liée est soit posée sur place, soit ajoutée au glossaire, soit
reconnue comme lacune de la cartographie.

Les suites ne sont pas maintenues à la main. Elles sont la relation inverse des
prérequis et se consultent par les backlinks d'Obsidian.

## Savoir le situer

Cette rubrique applique à petite échelle la progression
holistique → analytique → holistique : voir l'ensemble, ouvrir une pièce,
replacer cette pièce dans l'ensemble. Elle contient quatre éléments :

- **Ensemble** — nomme l'ensemble auquel la pièce appartient, son Input global,
  son Output global et ses grandes parties, sans rouvrir leurs mécanismes ;
- **Pièce ouverte** — place la pièce dans la chaîne
  `ce qui précède → la pièce → ce qui suit`, puis donne son Input, son Output et
  la frontière exacte de sa responsabilité ;
- **L'essentiel** — énonce en une à trois phrases le mécanisme central qui
  explique la transformation de l'Input en Output ;
- **Recomposer** — précise ce que la pièce reçoit de l'amont, ce qu'elle garantit
  à l'aval, et comment une modification ou une défaillance locale se propage.

La rubrique situe ; elle ne redécrit pas tout l'ensemble. Lorsque la pièce
n'appartient pas à une chaîne ordonnée, `Pièce ouverte` nomme ses relations
directes au lieu de son amont et de son aval.

## Connaissances

Cette rubrique décompose les notions attribuées à la leçon par la cartographie.
Elle n'ajoute pas un panorama voisin pour donner une impression de complétude.

Pour chaque point important, elle précise :

- où il agit ;
- quand et à quelle fréquence il agit ;
- ce qu'il modifie ou propage ;
- ce qui le rend inopérant ;
- son coût et sa limite lorsqu'ils influencent une décision.

Un nom d'outil apparaît après le mécanisme qu'il implémente.

## Références

Les références pointent au plus près de l'affirmation qu'elles soutiennent. Pour
un protocole ou une API, la version est indiquée. Pour un comportement observé,
le dépôt, la version du logiciel et le protocole de reproduction sont conservés.

Une leçon sur un sujet mouvant ne passe pas la relecture si ses sources primaires
n'ont pas été vérifiées récemment.

## Liste de contrôle

Une leçon ne rejoint le cours que si chaque réponse est positive :

1. Le Frontmatter est-il complet et cohérent ?
2. La leçon tient-elle sur un concept ?
3. Ses prérequis sont-ils disponibles et liés ?
4. Toutes les notions que la cartographie lui attribue sont-elles traitées ?
5. Chaque propriété importante porte-t-elle son mécanisme, et non sa seule
   description ?
6. Chaque levier porte-t-il sa portée et ses limites ?
7. Les sources sont-elles primaires, actuelles et précisément rattachées ?
8. La langue respecte-t-elle [AGENTS.md](../AGENTS.md) ?

Le contrôle est une relecture. Aucun script ne le remplace.
