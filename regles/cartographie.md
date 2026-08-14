# Cartographie du cours

> Comprendre puis reconstruire les mécanismes qui relient un modèle de langage à
> un assistant agentique local. Chaque Parcours dépose une pièce générique dans
> **Praxis** et fait progresser **Mnémos**, l'assistant personnel qui l'emploie.

Ce fichier fixe l'ordre de construction, la couverture du cours et la
destination de chaque notion. Il ne fixe ni la forme d'une leçon ni les règles
de rédaction.

## Comment lire les tableaux

Chaque Parcours possède un tableau unique. Une ligne décrit une leçon :

- **Ordre · identifiant** — la position dans le Parcours et un identifiant
  stable. L'identifiant ne change plus une fois la leçon publiée ; une
  réorganisation documente sa migration.
- **Leçon** — le titre de travail.
- **Notions couvertes** — les connaissances attribuées **exclusivement** à cette
  leçon.

Une notion apparaît dans exactement une ligne. Elle ne peut pas disparaître
pendant la rédaction : elle reste attachée à sa leçon, devient une partie
explicitement rattachée à une autre, ou rejoint le glossaire. Élargir la
couverture d'une leçon demande de modifier ce fichier d'abord.

Une leçon peut nommer une notion voisine pour la situer, mais ne la réenseigne
pas.

## L'ordre du parcours

L'ordre suit la **construction du harnais**. Il est cognitif et pratique ; il ne
prétend pas décrire une pile logicielle strictement ascendante.

Un Parcours peut rouvrir une pièce rencontrée plus tôt lorsqu'il change de
niveau d'analyse. Le KV cache est ainsi expliqué pendant la génération, puis
mesuré pendant l'inférence locale.

Trois dépendances commandent l'ordre et méritent d'être énoncées :

1. rien ne se mesure avant de savoir ce qu'on mesure — l'inférence locale suit
   la génération ;
2. rien ne se reprend avant d'être observable — l'exécution durable suit
   l'observabilité ;
3. rien ne se sécurise avant d'exister — la sécurité consolide des frontières
   déjà construites, sans attendre le dernier Parcours pour être appliquée.

## La forme d'un Parcours

Chaque Parcours produit quatre résultats :

1. **Mécanismes** — les concepts et leurs relations, découpés en leçons ;
2. **Reconstruction** — une version minimale écrite ou manipulée à la main ;
3. **Cas pratique** — une situation vérifiable sur le matériel du projet ;
4. **Intégration** — une brique testée déposée dans Praxis, ou l'assemblage
   explicite d'une brique déjà acquise.

À partir du premier client utilisable, chaque Parcours fait aussi progresser un
fil rouge de Mnémos. Le produit ne doit pas attendre le dernier Parcours pour
commencer à fonctionner.

## Frontière avec la veille

Ce fichier contient les mécanismes durables. Les fonctions mouvantes d'un
produit ou d'un protocole vivent dans la veille. Une nouveauté ne devient une
leçon que si elle modifie un mécanisme, un contrat, une garantie, une menace ou
une décision mesurable.

---

## Préambule · Python pour construire Praxis

*La pièce : le langage et l'outillage nécessaires au reste du parcours.*

Ce Préambule ne reprend pas les bases communes à tous les langages. Il traduit
vers Python les compétences d'un développeur JavaScript ou Java.

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| P.1 · `py-environnements-dependances` | Environnements et dépendances | environnement virtuel, `pyproject.toml`, résolution des dépendances, packaging |
| P.2 · `py-modules-packages-imports` | Modules, packages et imports | modules, packages, mécanique d'import, layout `src/` |
| P.3 · `py-objets-contrats-types` | Modéliser des contrats | objets, `dataclass`, composition, protocoles structurels, annotations, génériques, unions |
| P.4 · `py-validation-donnees` | Valider les données | validation à la frontière, Pydantic, coercition et refus |
| P.5 · `py-exceptions-erreurs` | Représenter les échecs | exceptions, chaînage des causes, taxonomie d'erreurs |
| P.6 · `py-iterateurs-generateurs` | Produire un flux paresseux | itérateurs, générateurs, progression à la demande |
| P.7 · `py-coroutines-taches` | Coroutines et tâches | `async`, `await`, tâches, ordonnancement coopératif |
| P.8 · `py-iterateurs-asynchrones` | Flux asynchrones | itérateurs et générateurs asynchrones |
| P.9 · `py-annulation` | Annuler sans masquer | réception, propagation et limites de l'annulation |
| P.10 · `py-context-managers` | Durée de vie des ressources | context managers synchrones et asynchrones, nettoyage garanti |
| P.11 · `py-configuration-secrets` | Configurer sans état global | configuration, variables d'environnement, secrets |
| P.12 · `py-tests` | Tester les frontières | pytest, fixtures, doubles de test, tests asynchrones |
| P.13 · `py-logs-structures` | Produire des logs structurés | événement de log, contexte, corrélation |
| P.14 · `py-serialisation-schemas` | Sérialiser des contrats durables | formats sérialisables, version de schéma, compatibilité |

**Reconstruction** — un pipeline asynchrone typé qui produit, transforme et
annule un flux d'événements.

**Cas pratique** — empaqueter ce pipeline, le configurer sans constante globale
et le tester sans dépendre du réseau.

**Intégration** — `contracts`, `config` et l'infrastructure de tests de Praxis.

---

## 0 · De l'entrée textuelle au token suivant

*La pièce : le modèle comme fonction qui transforme une séquence en distribution
pour le prochain token.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 0.1 · `unicode-octets` | Texte, Unicode et octets | points de code, encodage, bytes, limites d'un caractère |
| 0.2 · `tokenisation-vocabulaire` | Tokenisation et vocabulaire | BPE, SentencePiece, vocabulaire, relation texte–identifiants |
| 0.3 · `tokens-controle` | Tokens de contrôle | BOS, EOS, fins de tour, portée des tokens spéciaux |
| 0.4 · `templates-chat` | Le texte réellement lu par le modèle | rôles, délimiteurs, Template de chat |
| 0.5 · `embeddings-tokens` | Embeddings de tokens | projection des identifiants dans le residual stream |
| 0.6 · `position-rope` | Représenter la position | position, portée de RoPE, variantes à ne pas confondre |
| 0.7 · `attention-causale` | L'attention causale | Q, K, V, masque causal, agrégation |
| 0.8 · `residual-normalisation` | Residual stream et normalisation | mises à jour résiduelles, pré-norm, propagation entre sous-blocs |
| 0.9 · `mlp-transformer` | Le MLP d'une couche | transformation par position, seconde mise à jour résiduelle |
| 0.10 · `projection-logits` | De la représentation aux logits | normalisation finale, projection vocabulaire, scores bruts |
| 0.11 · `logits-softmax` | Des logits à une distribution | softmax, normalisation numérique, interprétation probabiliste |
| 0.12 · `filtrage-distribution` | Transformer la distribution | température, top-k, top-p, min-p, pénalités de répétition, présence et fréquence, greedy |
| 0.13 · `sampling-reproductibilite` | Tirer le prochain token | échantillonnage, seed, sources d'aléa, portée réelle de la reproductibilité |
| 0.14 · `boucle-autoregressive` | Réinjecter le token choisi | autorégression, croissance de la séquence |
| 0.15 · `detokenisation-fragments` | Reconstruire le texte généré | détokenisation incrémentale, fragments UTF-8 incomplets |
| 0.16 · `conditions-arret` | Borner la génération | EOS, stop sequences, budget de sortie, raison d'arrêt |
| 0.17 · `prefill-decode-kv-cache` | Prefill, decode et cache KV | différence entre les phases, principe du cache, réutilisation |
| 0.18 · `fenetre-contexte-cout` | Fenêtre de contexte et coût | limite de contexte, croissance du coût, frontière de la mesure |

**Reconstruction** — suivre une entrée dans un petit modèle, observer les logits,
puis écrire le sampler et la condition d'arrêt.

**Cas pratique** — déformer une même distribution réglage par réglage, puis
reproduire une génération sous un environnement fixé.

**Intégration** — `generation` : tokenisation, Templates, comptage, sampling et
boucle autorégressive bornée.

---

## 1 · L'inférence locale

*La pièce : charger et servir le modèle sur le matériel disponible.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 1.1 · `poids-precision` | Poids, paramètres et précision | nombre de paramètres, précision numérique, modèle dense et mixture of experts |
| 1.2 · `formats-poids` | Formats de poids et chargement | Safetensors, GGUF, métadonnées, chargement, temps de chauffe |
| 1.3 · `quantification` | Quantifier un modèle | schémas de quantification, compromis mémoire, vitesse et qualité |
| 1.4 · `budget-memoire` | Calculer le budget mémoire | RAM et VRAM nécessaires, poids, activations, CPU, GPU, accélérateurs, offload |
| 1.5 · `kv-cache-memoire` | Le KV cache comme coût mémoire | taille et type du cache, pression mémoire, effet de la longueur de contexte |
| 1.6 · `attention-optimisee` | Réduire les mouvements mémoire | FlashAttention, PagedAttention, gestion paginée du cache |
| 1.7 · `batching` | Servir plusieurs requêtes | batching statique, batching continu, parallélisme, concurrence, saturation |
| 1.8 · `caches-et-speculation` | Éviter le travail redondant | cache de préfixe, décodage spéculatif |
| 1.9 · `metriques-service` | Mesurer un service d'inférence | TTFT, latence inter-token, débit, utilisation, mémoire, protocole séparant prefill et decode |
| 1.10 · `runtimes-locaux` | Choisir un runtime | Ollama comme première surface, llama.cpp, vLLM, SGLang, critères de choix pour le homelab |
| 1.11 · `adaptation-modele` | Adapter un modèle | quantification, distillation, LoRA, frontière avec le RAG |

**Reconstruction** — calculer le budget mémoire d'un modèle, observer prefill et
decode, puis relier chaque métrique au mécanisme correspondant.

**Cas pratique** — servir le même modèle avec deux runtimes sous une charge
identique et expliquer les différences mesurées.

**Intégration** — `inference` : description d'un runtime local, inventaire de ses
capacités, protocole de benchmark.

---

## 2 · Transport, modèles et providers

*La pièce : le modèle comme capacité accessible au bout d'une frontière.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 2.1 · `http-frontiere` | La requête brute | HTTP, headers, corps, authentification, conservation des secrets |
| 2.2 · `surfaces-api` | Les surfaces exposées | endpoints de complétion, chat, réponses et embeddings, API native contre surface compatible |
| 2.3 · `streaming-protocoles` | Recevoir en flux | requêtes synchrones et asynchrones, SSE, NDJSON, WebSocket |
| 2.4 · `evenements-flux` | Assembler un flux | événements de texte, raisonnement, outils, usage et fin, assemblage des deltas |
| 2.5 · `backpressure-annulation` | Consommateur lent et arrêt | backpressure, annulation, fermeture d'un flux |
| 2.6 · `timeouts-reprise` | Borner l'attente | timeout de connexion, de lecture et d'exécution, réponse partielle, absence de reprise |
| 2.7 · `taxonomie-erreurs` | Classer les échecs | erreurs réseau, protocole, fournisseur et modèle |
| 2.8 · `limites-debit` | Absorber une limite de débit | 429, `Retry-After`, backoff, jitter |
| 2.9 · `usage-finish-reason` | Ce que le fournisseur déclare | finish reason, comptage des tokens, écart avec le comptage local |
| 2.10 · `capacites-providers` | Découvrir les capacités | découverte, matrice de capacités, normalisation qui n'efface pas les différences |
| 2.11 · `contrats-par-capacite` | Un contrat par capacité | génération, embeddings, reranking, STT, TTS, vision, adaptateurs distincts pour le local et le cloud |

**Reconstruction** — écrire un client streaming sans SDK et rendre chaque
événement observable.

**Cas pratique** — employer successivement un endpoint natif, un endpoint
compatible et une API cloud, puis provoquer timeout, 429 et coupure de flux.

**Intégration** — `models` et `client` : contrats canoniques, adaptateurs,
streaming, taxonomie d'erreurs.

---

## 3 · Conversation, session et context engineering

*La pièce : construire la vue bornée que le modèle reçoit à chaque inférence.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 3.1 · `stateless-session` | Ce que le modèle ne retient pas | modèle stateless entre deux appels, contexte du modèle contre état de session |
| 3.2 · `messages-contenus` | Messages et contenus typés | rôles, texte, image, audio, appel et résultat d'outil |
| 3.3 · `journal-session` | Le journal d'une session | identité d'une session, ordre des événements, historique complet contre contexte matérialisé |
| 3.4 · `budget-contexte` | Un seul budget pour tout | instructions, outils, retrieval et historique dans le même budget, comptage exact, réserve de sortie, budgets par source |
| 3.5 · `selection-priorite` | Choisir ce qui entre | sélection, priorité, provenance des éléments retenus |
| 3.6 · `effets-position` | La position change la lecture | effets de position, « lost in the middle » |
| 3.7 · `troncature-fenetre` | Tenir dans la fenêtre | fenêtre glissante, troncature, messages épinglés |
| 3.8 · `compaction-resume` | Compacter sans mentir | compaction, résumé, information perdue et sa trace |
| 3.9 · `prefixe-cache` | Stabiliser le préfixe | cache de prompt, préfixe stable, coût d'une invalidation |
| 3.10 · `persistance-session` | Persister une session | stockage, format, version et migration |
| 3.11 · `retention-session` | Fin de vie d'une session | suppression, rétention, export |

**Reconstruction** — séparer un journal de session de la fonction qui compose le
prochain contexte.

**Cas pratique** — maintenir une conversation longue, redémarrer le processus,
inspecter exactement les tokens envoyés après reprise.

**Intégration** — `context` et `sessions` : composition, budget, compaction,
persistance conversationnelle.

---

## 4 · Diriger et contraindre le modèle

*La pièce : augmenter la probabilité d'une sortie utile sans modifier les poids.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 4.1 · `instruction-systeme` | L'instruction système | portée réelle d'une instruction, séparation entre instruction et donnée |
| 4.2 · `exemples-shots` | Montrer plutôt que décrire | zero-shot, one-shot, few-shot, exemples positifs, contre-exemples, effet de l'ordre |
| 4.3 · `templates-prompts` | Versionner un prompt | variables, Templates, versions |
| 4.4 · `raisonnement` | Le budget de raisonnement | modes de raisonnement, budget, raisonnement visible contre état interne non exposé |
| 4.5 · `prefill-reponse` | Amorcer la réponse | prefill de la réponse, contrôle de la forme initiale |
| 4.6 · `sortie-structuree` | Demander une structure | sortie libre, sortie structurée, outil, JSON Schema |
| 4.7 · `decodage-contraint` | Contraindre le décodage | grammaire, masquage des logits, `logit_bias` |
| 4.8 · `validation-reparation` | Valider puis réparer | validation syntaxique et métier, réparation, re-prompt, retry |
| 4.9 · `sortie-valide-fausse` | Valide mais faux | limites d'une contrainte de forme sur le fond |
| 4.10 · `candidats-multiples` | Plusieurs candidats | self-consistency, génération et sélection de candidats |
| 4.11 · `evaluer-un-prompt` | Prouver qu'un prompt est meilleur | protocole d'évaluation d'une modification de prompt |

**Reconstruction** — contraindre à la main les tokens autorisés pour une petite
grammaire, puis valider un invariant que la grammaire ne peut pas exprimer.

**Cas pratique** — produire le même objet par prompt seul, par validation avec
retry et par décodage contraint, puis comparer validité, contenu et coût.

**Intégration** — `control` : Templates, contraintes, validation, stratégie de
réparation.

---

## 5 · Outils, actions et approbations

*La pièce : transformer une proposition du modèle en effet contrôlé.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 5.1 · `function-calling` | Proposer n'est pas agir | function calling natif et émulé, le modèle propose, l'exécuteur décide |
| 5.2 · `schema-outil` | Décrire un outil | nom, description, schéma comme instruction adressée au modèle, `tool_choice` |
| 5.3 · `appels-correlation` | Appeler et corréler | parsing et validation des arguments, identifiant d'appel, corrélation du résultat, appels parallèles |
| 5.4 · `resultats-outils` | Rendre un résultat | résultat structuré, fichier, image, contenu volumineux, troncature, résumé |
| 5.5 · `erreurs-outils` | Échouer utilement | erreur de validation, erreur attendue, erreur interne, message exploitable par le modèle |
| 5.6 · `effets-de-bord` | Classer les effets | lecture, écriture, destruction, idempotence, clé d'idempotence |
| 5.7 · `resultat-incertain` | Ne pas savoir si l'effet a eu lieu | timeout, annulation, résultat incertain après coupure |
| 5.8 · `permissions` | Portée d'une capacité | permissions, moindre privilège, granularité |
| 5.9 · `approbations` | Faire décider un humain | approbation avant exécution, décision ponctuelle contre permission durable |
| 5.10 · `revalidation-effet` | Au moment de l'effet | revalidation des préconditions, compensation lorsqu'un effet ne peut pas être annulé |
| 5.11 · `journal-audit` | Tracer une action | journal d'audit d'un effet |

**Reconstruction** — un registre, un dispatcher et une politique qui séparent
proposition, autorisation, exécution et résultat.

**Cas pratique** — lire l'état d'un service du homelab, proposer une
modification, attendre l'approbation, exécuter, vérifier l'effet.

**Intégration** — `tools`, `permissions` et `approvals`.

---

## 6 · MCP

*La pièce : exposer et consommer des capacités distantes sans les confondre avec
le runtime de l'agent.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 6.1 · `jsonrpc` | JSON-RPC 2.0 | requêtes, réponses, erreurs, notifications |
| 6.2 · `roles-mcp` | Client, serveur et host | rôles, responsabilités, frontière du host |
| 6.3 · `handshake-capacites` | Ouvrir une connexion | initialisation, négociation de version, négociation des capacités |
| 6.4 · `primitives-mcp` | Tools, resources et prompts | inventaire, appel, changement de catalogue |
| 6.5 · `ressources-mcp` | Lire une ressource | URI, lecture, abonnement, pagination |
| 6.6 · `transports-mcp` | stdio et Streamable HTTP | transports, cycle de vie d'une connexion |
| 6.7 · `progression-annulation` | Travaux longs | annulation, progression, tâches longues et durables |
| 6.8 · `auth-mcp` | Authentifier un serveur distant | OAuth sur le transport HTTP, portée des credentials prêtés |
| 6.9 · `elicitation` | Demander à l'utilisateur | elicitation depuis un serveur |
| 6.10 · `versions-depreciation` | Vivre avec les versions | compatibilité, fonctions dépréciées, période de transition |
| 6.11 · `adaptateur-outils` | Un seul registre d'outils | adaptateur vers le registre du Parcours 5 |
| 6.12 · `menaces-mcp` | Frontière de confiance | serveur tiers, injection indirecte par une ressource ou un résultat, tool poisoning par la description, rug pull après approbation, validation et filtrage côté host |

**Reconstruction** — un serveur et un client minimaux, handshake, `tools/list` et
`tools/call` compris.

**Cas pratique** — exposer un outil natif en MCP, le consommer par le même
registre, puis simuler un changement de description et une coupure.

**Intégration** — `mcp` : client, serveur minimal, adaptateur vers `tools`.

---

## 7 · Retrieval et connaissance documentaire

*La pièce : retrouver des sources pertinentes avant de produire une réponse.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 7.1 · `unites-documentaires` | Source, document, fragment | unités documentaires, provenance |
| 7.2 · `ingestion-parsing` | Ingérer des documents réels | parsing, nettoyage, documents structurés, pages, tableaux, code |
| 7.3 · `chunking` | Découper un document | chunking fixe, sémantique et structurel, recouvrement, contexte parent |
| 7.4 · `embeddings-documents` | Représenter un fragment | dimension, normalisation, similarité cosinus |
| 7.5 · `recherche-vectorielle` | Recherche vectorielle | indexation, top-k, filtres de métadonnées |
| 7.6 · `recherche-lexicale` | Recherche lexicale | BM25, termes rares, ce que le vectoriel manque |
| 7.7 · `recherche-hybride` | Fusionner et reranker | fusion des rangs, reranking bi-encoder et cross-encoder |
| 7.8 · `index-ann` | Le coût d'un index | HNSW, compromis rappel, latence et mémoire, Qdrant comme store concret |
| 7.9 · `pipeline-rag` | Retrouver, composer, répondre | pipeline RAG, citations, rattachement de chaque affirmation à une source |
| 7.10 · `fraicheur-index` | Maintenir un index | fraîcheur, suppression, réindexation |
| 7.11 · `graphes-multi-hop` | Au-delà du top-k | GraphRAG, parcours multi-hop |
| 7.12 · `evaluer-retrieval` | Mesurer la récupération | rappel, précision, MRR, nDCG, fidélité, pertinence, séparation entre retrieval et génération |
| 7.13 · `rag-ou-autre` | Quand ne pas faire de RAG | RAG contre contexte direct, outil ou fine-tuning |

**Reconstruction** — un petit index lexical puis vectoriel sans framework RAG,
une fusion des résultats, une mesure de la récupération.

**Cas pratique** — interroger la documentation réelle du homelab avec citations,
puis diagnostiquer séparément une mauvaise récupération et une mauvaise réponse.

**Intégration** — `knowledge` et `retrieval` : ingestion, index, recherche,
reranking, provenance.

---

## 8 · La mémoire agentique

*La pièce : conserver une connaissance personnelle au-delà d'une session sans la
confondre avec l'état d'un workflow.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 8.1 · `natures-memoire` | Cinq mémoires distinctes | mémoire de travail, de session, épisodique, sémantique, procédurale |
| 8.2 · `supports-memoire` | Choisir un support | clé-valeur exact, index vectoriel, graphe d'entités et de relations, wiki auto-écrit et inspectable |
| 8.3 · `types-souvenir` | Ce qu'on écrit | événement, fait, préférence, procédure, observation |
| 8.4 · `decision-ecriture` | Décider de retenir | quoi retenir et pourquoi, extraction depuis une conversation ou un résultat d'outil |
| 8.5 · `provenance-confiance` | D'où vient un souvenir | provenance, niveau de confiance |
| 8.6 · `validite-temporelle` | Un fait qui change | validité temporelle, évolution, correction explicite par l'utilisateur |
| 8.7 · `conflits-memoire` | Deux souvenirs contradictoires | détection et arbitrage d'un conflit |
| 8.8 · `rappel-memoire` | Retrouver au bon moment | récupération selon la tâche, scoring, fréquence, récence, importance |
| 8.9 · `consolidation-oubli` | Consolider et oublier | consolidation, decay, déduplication |
| 8.10 · `isolation-memoire` | Cloisonner | isolation entre utilisateurs, agents et sources, contamination, empoisonnement |
| 8.11 · `sauvegarde-memoire` | Sauvegarder une mémoire | sauvegarde, export, restauration |
| 8.12 · `evaluer-memoire` | Mesurer une mémoire | évaluation de l'écriture, du rappel et de l'influence réelle sur la réponse |

**Reconstruction** — des contrats distincts pour un épisode, un fait et une
procédure, avec la trace de leur écriture et de leur rappel.

**Cas pratique** — apprendre une préférence, enregistrer un événement daté,
corriger un fait devenu faux, prouver que l'ancienne version n'est plus utilisée.

**Intégration** — `memory` : politiques d'écriture, stores spécialisés,
provenance, rappel, consolidation, oubli.

---

## 9 · La boucle mono-agent

*La pièce : transformer plusieurs appels isolés en une exécution bornée.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 9.1 · `workflow-ou-agent` | Workflow ou agent | workflow déterministe contre agent qui choisit la suite |
| 9.2 · `evenements-run` | L'état d'un run | état éphémère, événement utilisateur, événement modèle, événement outil |
| 9.3 · `boucle-oda` | Observer, décider, agir, intégrer | la boucle, l'étape et la transition explicites |
| 9.4 · `strategies-raisonnement` | Stratégies de conduite | ReAct, plan puis exécution, réflexion et critique, coût de chacune |
| 9.5 · `issues-d-un-tour` | Les issues d'un tour | outil, handoff, réponse finale |
| 9.6 · `conditions-arret-agent` | Arrêter la boucle | conditions d'arrêt, budget de tours, de tokens, de temps et d'outils |
| 9.7 · `erreurs-boucle` | Reprendre après une erreur | erreurs de transport, modèle, outil et politique, transitoire contre définitive, retry, backoff |
| 9.8 · `parallelisme-boucle` | Agir en parallèle | appels parallèles, collecte partielle, annulation propagée |
| 9.9 · `hooks` | Intervenir dans la boucle | hooks avant et après un appel |
| 9.10 · `trajectoire` | La trajectoire comme objet | journal d'événements, trajectoire inspectable |
| 9.11 · `declenchement` | Ce qui démarre un run | déclenchement par requête, événement ou horaire, limite d'une boucle vivant seulement en mémoire du processus |

**Reconstruction** — la boucle comme machine à états éphémère dont chaque
transition produit un événement inspectable.

**Cas pratique** — exécuter une tâche multi-étapes bornée, provoquer plusieurs
catégories d'erreurs, vérifier la condition d'arrêt.

**Intégration** — `loop` : runner mono-agent, budgets, transitions, hooks.

---

## 10 · Observabilité et évaluations

*La pièce : rendre une trajectoire explicable, comparable et reproductible.*

Ce Parcours précède l'exécution durable : une reprise, un replay ou un fork ne
se diagnostiquent pas sans trace ni rejeu.

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 10.1 · `signaux` | Événement, log, métrique, trace | span, hiérarchie, ce que chaque signal permet |
| 10.2 · `correlation` | Relier les signaux | corrélation session, run, agent, outil |
| 10.3 · `instrumenter-le-modele` | Instrumenter le client modèle | tokens d'entrée, de sortie, de cache et de raisonnement |
| 10.4 · `instrumenter-le-harnais` | Instrumenter le reste | outils, MCP, retrieval, mémoire |
| 10.5 · `couts-latences` | Latence et coût | TTFT, latence, durée d'outil, durée totale, coût cloud, coût matériel local |
| 10.6 · `donnees-sensibles-traces` | Ce qu'une trace ne doit pas contenir | données sensibles, rédaction, rétention |
| 10.7 · `format-de-trace` | Un format indépendant | OpenTelemetry, conventions GenAI, indépendance vis-à-vis d'un fournisseur |
| 10.8 · `replay-trajectoire` | Rejouer une trajectoire | replay d'une trajectoire enregistrée |
| 10.9 · `tests-deterministes` | Tester ce qui est déterministe | test unitaire, test de contrat, test d'intégration |
| 10.10 · `evals-sortie` | Évaluer une sortie | jeu de données, cas de non-régression, exact match, critères, score, distribution |
| 10.11 · `evals-composants` | Évaluer les composants | eval de retrieval, de mémoire, de trajectoire |
| 10.12 · `llm-as-judge` | Le modèle comme juge | LLM-as-judge, biais, ordre, calibration, juge différent du générateur, évaluation humaine |
| 10.13 · `comparer-et-decider` | Décider sur des mesures | comparaison de modèle, prompt, outil et architecture, diagnostic avant fine-tuning, alertes, tableaux de bord, SLO personnels |

**Reconstruction** — un format de trace indépendant d'un fournisseur, puis une
eval calculée à partir d'événements rejoués.

**Cas pratique** — retrouver la première décision fautive d'une trajectoire et
ajouter le cas de non-régression correspondant.

**Intégration** — `telemetry`, `evals` et `judge`.

---

## 11 · État agentique et exécution durable

*La pièce : survivre aux attentes, aux interruptions et aux redémarrages sans
perdre la position ni répéter aveuglément les effets.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 11.1 · `categories-etat` | Le mot « état » recouvre cinq choses | processus stateless contre agent logiquement stateful, contexte du modèle, session, run, workflow, mémoire |
| 11.2 · `identifiants` | Nommer une exécution | identifiants de session, run, workflow, étape, tâche et appel |
| 11.3 · `schema-etat` | Un état sérialisable | état éphémère contre durable, schéma typé, sérialisation sûre, version et migration |
| 11.4 · `etat-de-controle` | Où en est l'exécution | étape acquise, prochaine étape, statuts d'une tâche |
| 11.5 · `snapshot-ou-journal` | Snapshot ou journal | enregistrement d'état contre journal d'événements |
| 11.6 · `checkpoints` | Poser un checkpoint | frontière cohérente, fréquence et coût, écritures d'une branche parallèle, état et checkpoint dans une trace |
| 11.7 · `interruption-reprise` | Attendre sans rester vivant | interruption, attente d'approbation, pause sans processus vivant, reprise depuis le dernier checkpoint |
| 11.8 · `retry-replay` | Retry et replay | tentative d'une opération en échec, replay déterministe, enregistrement des résultats non déterministes, eval de reprise après panne |
| 11.9 · `fork-time-travel` | Explorer une autre trajectoire | fork d'un checkpoint, time travel pour le diagnostic |
| 11.10 · `activites-effets` | Ce qui ne se rejoue pas | appel modèle et outil comme activités, `at-least-once`, `at-most-once`, absence de garantie générale « exactly once » |
| 11.11 · `idempotence-effets` | Un effet, une fois | clé d'idempotence, journal d'effets, inbox et outbox, résultat inconnu après coupure, compensation |
| 11.12 · `planification-workers` | Faire avancer sans requête | timer durable, échéance, tâche planifiée, worker, file, lease, récupération d'un travail abandonné, concurrence sur un même workflow |
| 11.13 · `versions-en-vol` | Déployer avec des workflows ouverts | migration d'une version en cours d'exécution, approbation expirée, revalidation de l'autorité |
| 11.14 · `retention-etat` | Fin de vie d'un état | rétention, chiffrement, suppression |
| 11.15 · `moteurs-durables` | Confronter des moteurs | SQLite pour la reconstruction locale, Temporal, Restate, DBOS, Prefect |

**Reconstruction** — un checkpointer SQLite et un journal d'effets pour la boucle
du Parcours 9.

**Cas pratique** — arrêter le processus avant et après chaque frontière d'action,
reprendre le workflow, démontrer qu'aucun effet confirmé n'est répété, puis
forker un checkpoint sans modifier la trajectoire originale.

**Intégration** — `state`, `checkpoints`, `workflow` et `effects`.

---

## 12 · Workspace, sandbox et skills

*La pièce : donner à l'agent un environnement de travail sans lui donner la
machine entière.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 12.1 · `workspace` | Le workspace n'est pas le contexte | fichiers, répertoires, artefacts, cycle de vie d'un workspace |
| 12.2 · `montage-donnees` | Donner accès à des données | montage, copie de travail, chemins autorisés |
| 12.3 · `execution-code` | Exécuter du code | shell, exécution de code, processus enfant |
| 12.4 · `isolation` | Contenir l'exécution | conteneur, sandbox, limites CPU, mémoire, disque, temps et réseau |
| 12.5 · `credentials-isoles` | Ne pas prêter ses clés | séparation des credentials et du code généré |
| 12.6 · `artefacts` | Ce qui mérite d'être gardé | artefact produit contre fichier temporaire, snapshot et restauration d'un workspace |
| 12.7 · `skills` | Une procédure chargée à la demande | skill, ressources associées, divulgation progressive, description courte contre contenu complet |
| 12.8 · `instructions-en-couches` | Des instructions en couches | instructions globales, projet, agent et tâche, résolution des conflits |
| 12.9 · `hooks-outils` | Encadrer un outil | hooks avant et après outil |
| 12.10 · `cycle-dependances` | Installer et nettoyer | installation de dépendances, nettoyage, audit des fichiers et des commandes |

**Reconstruction** — un workspace local doté d'une liste explicite de capacités,
et une skill chargée sans placer tout son contenu dans le contexte.

**Cas pratique** — faire produire un artefact par un sous-processus isolé,
interrompre l'exécution, reprendre avec le même workspace restauré.

**Intégration** — `workspace`, `sandbox`, `skills`, `artifacts` et `hooks`.

---

## 13 · Sous-agents, délégation et état partagé

*La pièce : répartir un travail sans créer une mémoire globale implicite.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 13.1 · `quand-deleguer` | Quand un agent unique suffit | critères de délégation, coût d'un agent supplémentaire |
| 13.2 · `formes-de-delegation` | Trois formes | agent utilisé comme outil, handoff de contrôle, superviseur et ouvriers |
| 13.3 · `routage` | Router une demande | routeur déterministe contre routeur piloté par modèle |
| 13.4 · `contrat-de-resultat` | Déléguer sous contrat | contrat de résultat, contexte isolé d'un sous-agent |
| 13.5 · `etat-prive` | L'état privé par défaut | état privé par invocation, état par thread lorsqu'il est nécessaire, namespace de checkpoint |
| 13.6 · `champs-partages` | Partager un champ, pas un dictionnaire | état parent, champs publics, propriétaire et producteurs, mise à jour partielle |
| 13.7 · `reducers` | Fusionner des écritures | reducer, associativité, déterminisme d'une fusion |
| 13.8 · `concurrence-ecriture` | Écrire en concurrence | append-only, version, compare-and-swap, conflit entre branches |
| 13.9 · `fan-out-fan-in` | Ouvrir et refermer | fan-out, fan-in, limite de parallélisme, backpressure, annulation propagée |
| 13.10 · `echec-partiel` | Quand un ouvrier échoue | résultat partiel, boucle de délégation, décision de poursuite |
| 13.11 · `partage-d-observation` | Partager peu | partage d'une observation contre partage de tout l'historique, mémoire commune contre état de workflow partagé |
| 13.12 · `autorite-deleguee` | Ce qu'un sous-agent a le droit de faire | autorité déléguée, arbitrage qualité, délai, coût et confidentialité |
| 13.13 · `a2a` | Des agents indépendants | A2A comme protocole de culture |

**Reconstruction** — deux sous-agents en parallèle avec des états privés, dont
seuls les résultats publics fusionnent par un reducer défini.

**Cas pratique** — comparer un agent équipé de plusieurs skills à un superviseur
et plusieurs ouvriers sur les mêmes tâches, puis provoquer un conflit d'écriture
et un échec partiel.

**Intégration** — `agents`, `handoffs` et `router`, appuyés sur l'état durable du
Parcours 11.

---

## 14 · Sécurité du harnais

*La pièce : empêcher qu'une donnée non fiable acquière silencieusement une
autorité durable.*

Ce Parcours consolide et éprouve des barrières déjà posées. Il n'introduit pas
la sécurité : elle commence à la première frontière externe, au Parcours 2.

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 14.1 · `threat-model` | Modéliser la menace | actifs, adversaires, frontières de confiance, threat model propre au homelab |
| 14.2 · `donnee-et-autorite` | Quatre notions à ne pas confondre | donnée, instruction, capacité, autorité |
| 14.3 · `prompt-injection` | L'injection | injection directe, injection indirecte par page, document, outil ou mémoire, goal hijacking |
| 14.4 · `outils-non-fiables` | Un outil peut mentir | tool poisoning, résultat d'outil non fiable, excessive agency |
| 14.5 · `exfiltration` | Faire sortir une donnée | exfiltration de secrets, SSRF, traversée de chemins |
| 14.6 · `execution-non-fiable` | Exécuter du code non fiable | commande shell, exécution de code, dépendances et supply chain |
| 14.7 · `empoisonnement-durable` | Contaminer ce qui reste | serveur MCP malveillant ou compromis, empoisonnement du RAG, empoisonnement de mémoire persistant |
| 14.8 · `attaques-multi-agents` | Attaquer par la coordination | confusion entre agents, effet en cascade, état partagé comme canal, checkpoint contenant des secrets |
| 14.9 · `approbation-perimee` | Une autorisation périmée | approbation ancienne ou hors contexte, confirmation au moment de l'effet |
| 14.10 · `barrieres` | Les barrières qui tiennent | moindre privilège, séparation des credentials, sandbox, isolation réseau, allowlist, validation |
| 14.11 · `audit-chiffrement` | Garder une preuve | journal d'audit, chiffrement, sauvegarde, restauration |
| 14.12 · `reponse-incident` | Après l'incident | tests adversariaux, détection, révocation, réponse à incident, OWASP LLM et OWASP Agentic |

**Reconstruction** — tracer les flux de confiance depuis une donnée externe
jusqu'à un outil, une mémoire et un effet durable.

**Cas pratique** — attaquer Mnémos par un document, un outil MCP, une mémoire et
une commande, puis vérifier chaque barrière et la révocation d'un état contaminé.

**Intégration** — `security`, `policy` et `audit`.

---

## 15 · Voix, vision et temps réel

*La pièce : porter plusieurs modalités sans les réduire prématurément à du
texte.*

| Ordre · identifiant | Leçon | Notions couvertes |
|---|---|---|
| 15.1 · `contenu-multimodal` | Un contenu typé | contenu multimodal, budget de tokens visuels et audio |
| 15.2 · `vision` | Voir une image | image native contre OCR, préparation, redimensionnement, métadonnées, VLM local |
| 15.3 · `capture-consentement` | Capturer une image ou un son | caméra, consentement, durée de conservation, confidentialité des flux |
| 15.4 · `chaine-vocale` | Deux architectures vocales | STT puis LLM puis TTS, speech-to-speech |
| 15.5 · `audio-formats` | Transporter de l'audio | formats, échantillonnage, encodage, streaming audio |
| 15.6 · `tours-de-parole` | Savoir qui parle | détection d'activité vocale, tours de parole, echo cancellation |
| 15.7 · `barge-in` | Être interrompu | interruption par l'utilisateur pendant la réponse, barge-in |
| 15.8 · `session-temps-reel` | Une session en temps réel | événement temps réel, état de session, appel d'outil pendant une conversation vocale |
| 15.9 · `approbation-vocale` | Approuver à la voix | approbation vocale, risque d'ambiguïté |
| 15.10 · `latence-degrade` | Tenir la latence | latence de bout en bout, modèle local contre service cloud, mode dégradé sans voix ni vision |

**Reconstruction** — un flux d'événements commun au texte, à l'audio et à
l'image, qui ne perd pas le média source.

**Cas pratique** — parler à Mnémos, l'interrompre pendant sa réponse, lui faire
analyser une image, reprendre la même session après une coupure.

**Intégration** — `io` et `realtime`.

---

## 16 · Mnémos

*La pièce : assembler sans introduire un mécanisme encore inconnu.*

Ce Parcours n'ouvre aucun mécanisme neuf. Chaque décision pointe vers le
Parcours qui l'a rendue possible.

| Ordre · identifiant | Étape d'assemblage | Décisions à fixer |
|---|---|---|
| 16.1 · `mn-identite` | Identité et confidentialité | personnalité, instructions propres à Mnémos, contrats de confidentialité |
| 16.2 · `mn-topologie` | Topologie des agents | agents disponibles, choix entre skills et sous-agents |
| 16.3 · `mn-modeles` | Modèles et replis | modèles locaux, replis cloud autorisés, mise à jour des modèles et des dépendances |
| 16.4 · `mn-outils-homelab` | Outils réels | outils du homelab, API domotique, appareils |
| 16.5 · `mn-permissions` | Autorité | matrice des permissions et des approbations |
| 16.6 · `mn-sessions-workflows` | Continuité | sessions persistantes, workflows durables, état partagé explicitement limité |
| 16.7 · `mn-declencheurs` | Déclenchement | tâches déclenchées par requête, horaire ou événement |
| 16.8 · `mn-memoire` | Mémoire personnelle | sources de mémoire, procédures apprises |
| 16.9 · `mn-interfaces` | Surfaces d'usage | voix, vision, interface Web, mobile ou terminal |
| 16.10 · `mn-exploitation` | Exploitation | observabilité, evals, audit, runbook, sauvegarde, restauration, migration |
| 16.11 · `mn-acceptation` | Preuve d'usage | mode hors ligne et modes dégradés, critères d'acceptation quotidiens, conversion des échecs réels en evals de non-régression |

Mnémos n'est ni une plateforme multi-tenant, ni un produit commercial, ni un
prétexte pour distribuer prématurément chaque composant.

**Cas pratique** — utiliser Mnémos sur des tâches réelles du homelab, conserver
les trajectoires problématiques, fermer les régressions observées.

**Intégration** — Praxis atteint sa première version stable ; Mnémos devient
l'application qui l'éprouve chaque jour.

---

## Les briques de Praxis

Une brique est déposée à la fin du Parcours qui en ouvre les mécanismes.

| Brique | Rôle | Parcours |
|---|---|---|
| `contracts` · `config` | types communs, configuration, erreurs | Préambule |
| `generation` | tokeniser, rendre un Template, échantillonner, arrêter | 0 |
| `inference` | décrire et mesurer un runtime local | 1 |
| `models` · `client` | contrats par capacité, transport, streaming | 2 |
| `context` · `sessions` | composer le contexte, persister les sessions | 3 |
| `control` | prompts, sorties contraintes, validation | 4 |
| `tools` · `permissions` · `approvals` | enregistrer, autoriser et exécuter une action | 5 |
| `mcp` | adapter des outils et ressources distants | 6 |
| `knowledge` · `retrieval` | ingérer, rechercher, reranker, citer | 7 |
| `memory` | écrire, retrouver, consolider, oublier | 8 |
| `loop` | exécuter une boucle mono-agent bornée | 9 |
| `telemetry` · `evals` · `judge` | observer, rejouer, mesurer | 10 |
| `state` · `checkpoints` · `workflow` · `effects` | persister et reprendre une exécution | 11 |
| `workspace` · `sandbox` · `skills` · `artifacts` | fournir un environnement d'action isolé | 12 |
| `agents` · `handoffs` · `router` | déléguer et coordonner plusieurs agents | 13 |
| `security` · `policy` · `audit` | imposer les frontières de confiance | 14 |
| `io` · `realtime` | porter la voix, la vision, les interruptions | 15 |

## Veille transversale

La veille suit sans désorganiser le parcours : évolutions de MCP et de ses
extensions, A2A et autres protocoles inter-agents, computer use et nouveaux
environnements d'exécution, runtimes d'inférence et techniques de cache, modèles
de raisonnement et multimodal, moteurs d'exécution durable, stores de mémoire
temporelle et graphes, standards d'observabilité GenAI, nouvelles classes
d'attaques agentiques.
