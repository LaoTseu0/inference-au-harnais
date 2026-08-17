# Point d'entrée des instructions

Ce fichier fixe les règles qui valent pour toute intervention dans le dépôt :
langue, rigueur et méthode. Il doit être lu entièrement avant d'écrire.

## Ce qu'on charge

@regles/lecon.md

La cartographie ne se charge pas entièrement. On y lit la rubrique du Parcours
concerné :

| Ce qu'on écrit | Ce qu'on lit en plus |
|---|---|
| une leçon | la rubrique de son Parcours dans [regles/cartographie.md](regles/cartographie.md) |
| une entrée de glossaire | la section `Termes techniques et glossaire` de [regles/lecon.md](regles/lecon.md) |
| une modification de la couverture ou de l'ordre | [regles/cartographie.md](regles/cartographie.md) en entier |

Réduire le contexte ne dispense jamais de lire entièrement les règles
applicables.

Les leçons vivent dans `cours/<parcours>/`, les définitions dans `glossaire/`.

## Langue

- Écrire comme un humain français natif.
- Écarter les calques, faux-amis et collocations étrangères au français.
- Ne pas traduire en français les mots-clés techniques essentiels. Conserver la
  forme d'origine des mots-clés techniques essentiels lorsqu'ils nomment un
  concept, un contrat, une primitive, un champ ou une opération consacrée par
  l'écosystème.
- Conserver le jargon technique anglais lorsqu'il évite une traduction
  artificielle ou ambiguë.
- Employer notamment `Template`, `Frontmatter`, `Input` et `Output` dans leur
  sens technique.
- Garder un registre écrit et précis. Écarter les béquilles de l'oral et
  l'emphase commerciale.
- Supprimer le jargon corporatif et les transitions trop formelles.

## Rigueur

- Distinguer un fait observé, une déduction, une hypothèse et une décision de
  conception.
- Pour un sujet qui évolue, vérifier la documentation ou la spécification
  primaire actuelle. Nommer la version ou la date lorsqu'elle change la portée
  de l'affirmation.
- Privilégier les spécifications, documentations officielles, dépôts sources et
  articles de recherche. Une source secondaire sert à découvrir une piste, pas à
  fixer un mécanisme.
- Une mesure mentionne son protocole, son environnement et ce qu'elle permet
  réellement de conclure.
- Signaler une incertitude restante au lieu de la combler par une formulation
  vraisemblable.

## Méthode de travail

- Lire entièrement les instructions applicables avant d'agir.
- Préserver les modifications existantes et les fichiers hors du périmètre de la
  demande.
- Vérifier les liens et les commandes concernés avant d'annoncer leur validité.
- Ne jamais déclarer qu'un contrôle passe sans l'avoir exécuté.
- Une refonte conserve les informations encore justes ou explique pourquoi elles
  disparaissent.
- Les messages de commit ne contiennent aucune mention de co-auteur généré par
  une IA.
