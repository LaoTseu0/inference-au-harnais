# Cartographie du cours

> Comprendre puis reconstruire les mécanismes qui relient un modèle de langage à
> un assistant agentique local. Chaque Parcours dépose une pièce générique dans
> **Praxis** et fait progresser **Mnémos**, l'assistant personnel qui l'emploie.

Ce fichier fixe l'ordre de construction, la couverture du cours et la
destination de chaque notion. Il ne fixe ni la forme d'une leçon ni les règles
de rédaction.

## Conventions

- Une leçon porte un ordre et un identifiant stable. L'identifiant ne change
  plus une fois la leçon publiée ; une réorganisation documente sa migration.
- Les notions listées sous une leçon lui sont attribuées **exclusivement**.
- Une notion ne disparaît pas pendant la rédaction : elle reste attachée à sa
  leçon, devient une partie explicitement rattachée à une autre, ou rejoint le
  glossaire.
- Élargir la couverture d'une leçon demande de modifier ce fichier d'abord.
- Une leçon peut nommer une notion voisine pour la situer, mais ne la
  réenseigne pas.

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

- **P.1 · `py-environnements-dependances`** — Environnements et dépendances
  - environnement virtuel, `pyproject.toml`
  - résolution des dépendances, packaging
- **P.2 · `py-modules-packages-imports`** — Modules, packages et imports
  - modules, packages, mécanique d'import
  - layout `src/`
- **P.3 · `py-objets-contrats-types`** — Modéliser des contrats
  - objets, `dataclass`, composition, protocoles structurels
  - annotations de types, génériques, unions
- **P.4 · `py-validation-donnees`** — Valider les données
  - validation à la frontière, Pydantic
  - coercition et refus
- **P.5 · `py-exceptions-erreurs`** — Représenter les échecs
  - exceptions, chaînage des causes
  - taxonomie d'erreurs
- **P.6 · `py-iterateurs-generateurs`** — Produire un flux paresseux
  - itérateurs, générateurs
  - progression à la demande
- **P.7 · `py-coroutines-taches`** — Coroutines et tâches
  - `async`, `await`, tâches
  - ordonnancement coopératif
- **P.8 · `py-iterateurs-asynchrones`** — Flux asynchrones
  - itérateurs et générateurs asynchrones
- **P.9 · `py-annulation`** — Annuler sans masquer
  - réception, propagation et limites de l'annulation
- **P.10 · `py-context-managers`** — Durée de vie des ressources
  - context managers synchrones et asynchrones
  - nettoyage garanti
- **P.11 · `py-configuration-secrets`** — Configurer sans état global
  - configuration, variables d'environnement, secrets
- **P.12 · `py-tests`** — Tester les frontières
  - pytest, fixtures, doubles de test
  - tests asynchrones
- **P.13 · `py-logs-structures`** — Produire des logs structurés
  - événement de log, contexte, corrélation
- **P.14 · `py-serialisation-schemas`** — Sérialiser des contrats durables
  - formats sérialisables
  - version de schéma, compatibilité

**Reconstruction** — un pipeline asynchrone typé qui produit, transforme et
annule un flux d'événements.

**Cas pratique** — empaqueter ce pipeline, le configurer sans constante globale
et le tester sans dépendre du réseau.

**Intégration** — `contracts`, `config` et l'infrastructure de tests de Praxis.

---

## 0 · De l'entrée textuelle au token suivant

*La pièce : le modèle comme fonction qui transforme une séquence en distribution
pour le prochain token.*

- **0.1 · `unicode-octets`** — Texte, Unicode et octets
  - points de code, encodage, bytes
  - limites d'un caractère
- **0.2 · `tokenisation-vocabulaire`** — Tokenisation et vocabulaire
  - BPE, SentencePiece, vocabulaire
  - relation texte–identifiants
- **0.3 · `tokens-controle`** — Tokens de contrôle
  - BOS, EOS, fins de tour
  - portée des tokens spéciaux
- **0.4 · `templates-chat`** — Le texte réellement lu par le modèle
  - rôles, délimiteurs, Template de chat
- **0.5 · `embeddings-tokens`** — Embeddings de tokens
  - projection des identifiants dans le residual stream
- **0.6 · `position-rope`** — Représenter la position
  - position, portée de RoPE
  - variantes à ne pas confondre
- **0.7 · `attention-causale`** — L'attention causale
  - Q, K, V
  - masque causal, agrégation
- **0.8 · `residual-normalisation`** — Residual stream et normalisation
  - mises à jour résiduelles, pré-norm
  - propagation entre sous-blocs
- **0.9 · `mlp-transformer`** — Le MLP d'une couche
  - transformation par position
  - seconde mise à jour résiduelle
- **0.10 · `projection-logits`** — De la représentation aux logits
  - normalisation finale, projection vocabulaire
  - scores bruts
- **0.11 · `logits-softmax`** — Des logits à une distribution
  - softmax, normalisation numérique
  - interprétation probabiliste
- **0.12 · `filtrage-distribution`** — Transformer la distribution
  - température, top-k, top-p, min-p
  - pénalités de répétition, de présence et de fréquence
  - argmax et génération greedy
- **0.13 · `sampling-reproductibilite`** — Tirer le prochain token
  - échantillonnage, seed, sources d'aléa
  - portée réelle de la reproductibilité
- **0.14 · `boucle-autoregressive`** — Réinjecter le token choisi
  - autorégression, croissance de la séquence
- **0.15 · `detokenisation-fragments`** — Reconstruire le texte généré
  - détokenisation incrémentale
  - fragments UTF-8 incomplets
- **0.16 · `conditions-arret`** — Borner la génération
  - EOS, stop sequences, budget de sortie
  - raison d'arrêt
- **0.17 · `prefill-decode-kv-cache`** — Prefill, decode et cache KV
  - différence entre les phases
  - principe du cache, réutilisation
- **0.18 · `fenetre-contexte-cout`** — Fenêtre de contexte et coût
  - limite de contexte, croissance du coût
  - frontière de la mesure

**Reconstruction** — suivre une entrée dans un petit modèle, observer les logits,
puis écrire le sampler et la condition d'arrêt.

**Cas pratique** — déformer une même distribution réglage par réglage, puis
reproduire une génération sous un environnement fixé.

**Intégration** — `generation` : tokenisation, Templates, comptage, sampling et
boucle autorégressive bornée.

---

## 1 · L'inférence locale

*La pièce : charger et servir le modèle sur le matériel disponible.*

- **1.1 · `poids-formats`** — Ce qu'est un modèle sur disque et en mémoire
  - nombre de paramètres, précision numérique
  - modèle dense et mixture of experts
  - Safetensors, GGUF, métadonnées, chargement, temps de chauffe
- **1.2 · `quantification`** — Quantifier un modèle
  - schémas de quantification
  - compromis mémoire, vitesse et qualité
- **1.3 · `budget-memoire`** — Calculer le budget mémoire
  - RAM et VRAM nécessaires, poids et activations
  - CPU, GPU, accélérateurs, offload
- **1.4 · `kv-cache-memoire`** — Le KV cache comme coût mémoire
  - taille et type du cache, pression mémoire
  - effet de la longueur de contexte
- **1.5 · `attention-optimisee`** — Réduire les mouvements mémoire
  - FlashAttention
  - PagedAttention, gestion paginée du cache
- **1.6 · `batching`** — Servir plusieurs requêtes
  - batching statique, batching continu
  - parallélisme, concurrence, saturation
- **1.7 · `caches-et-speculation`** — Éviter le travail redondant
  - cache de préfixe
  - décodage spéculatif
- **1.8 · `metriques-service`** — Mesurer un service d'inférence
  - TTFT, latence inter-token, débit, utilisation, mémoire
  - protocole séparant prefill et decode
- **1.9 · `runtimes-locaux`** — Choisir un runtime
  - Ollama comme première surface locale
  - llama.cpp, vLLM, SGLang
  - critères de choix selon la charge du homelab
- **1.10 · `adaptation-modele`** — Adapter un modèle
  - quantification, distillation, LoRA
  - frontière avec le RAG

**Reconstruction** — calculer le budget mémoire d'un modèle, observer prefill et
decode, puis relier chaque métrique au mécanisme correspondant.

**Cas pratique** — servir le même modèle avec deux runtimes sous une charge
identique et expliquer les différences mesurées.

**Intégration** — `inference` : description d'un runtime local, inventaire de ses
capacités, protocole de benchmark.

---

## 2 · Transport, modèles et providers

*La pièce : le modèle comme capacité accessible au bout d'une frontière.*

- **2.1 · `http-frontiere`** — La requête brute
  - HTTP, headers, corps
  - authentification, conservation des secrets
- **2.2 · `surfaces-api`** — Les surfaces exposées
  - endpoints de complétion, chat, réponses et embeddings
  - API native contre surface compatible
- **2.3 · `streaming-protocoles`** — Recevoir en flux
  - requêtes synchrones et asynchrones
  - SSE, NDJSON, WebSocket
- **2.4 · `evenements-flux`** — Assembler un flux
  - événements de texte, raisonnement, outils, usage et fin
  - assemblage des deltas
- **2.5 · `flux-interrompu`** — Quand le flux ne va pas au bout
  - timeout de connexion, de lecture et d'exécution
  - backpressure et consommateur lent
  - annulation, fermeture, réponse partielle, absence de reprise
- **2.6 · `taxonomie-erreurs`** — Classer les échecs
  - erreurs réseau, protocole, fournisseur et modèle
- **2.7 · `limites-debit`** — Absorber une limite de débit
  - 429, `Retry-After`
  - backoff, jitter
- **2.8 · `usage-finish-reason`** — Ce que le fournisseur déclare
  - finish reason, comptage des tokens
  - écart avec le comptage local
- **2.9 · `capacites-providers`** — Découvrir les capacités
  - découverte, matrice de capacités
  - normalisation qui n'efface pas les différences
- **2.10 · `contrats-par-capacite`** — Un contrat par capacité
  - génération, embeddings, reranking, STT, TTS, vision
  - adaptateurs distincts pour le runtime local et le service cloud

**Reconstruction** — écrire un client streaming sans SDK et rendre chaque
événement observable.

**Cas pratique** — employer successivement un endpoint natif, un endpoint
compatible et une API cloud, puis provoquer timeout, 429 et coupure de flux.

**Intégration** — `models` et `client` : contrats canoniques, adaptateurs,
streaming, taxonomie d'erreurs.

---

## 3 · Conversation, session et context engineering

*La pièce : construire la vue bornée que le modèle reçoit à chaque inférence.*

- **3.1 · `stateless-session`** — Ce que le modèle ne retient pas
  - modèle stateless entre deux appels
  - contexte du modèle contre état de session
- **3.2 · `messages-contenus`** — Messages et contenus typés
  - rôles
  - texte, image, audio, appel et résultat d'outil
- **3.3 · `journal-session`** — Le journal d'une session
  - identité d'une session, ordre des événements
  - historique complet contre contexte matérialisé
- **3.4 · `budget-contexte`** — Un seul budget pour tout
  - instructions, outils, retrieval et historique dans le même budget
  - comptage exact, réserve de sortie, budgets par source
- **3.5 · `selection-placement`** — Choisir ce qui entre et où
  - sélection, priorité, provenance des éléments retenus
  - effets de position, « lost in the middle »
- **3.6 · `troncature-fenetre`** — Tenir dans la fenêtre
  - fenêtre glissante, troncature
  - messages épinglés
- **3.7 · `compaction-resume`** — Compacter sans mentir
  - compaction, résumé
  - information perdue et sa trace
- **3.8 · `prefixe-cache`** — Stabiliser le préfixe
  - cache de prompt, préfixe stable
  - coût d'une invalidation
- **3.9 · `persistance-session`** — Persister, migrer, supprimer
  - stockage d'une session, format, version et migration
  - suppression, rétention, export

**Reconstruction** — séparer un journal de session de la fonction qui compose le
prochain contexte.

**Cas pratique** — maintenir une conversation longue, redémarrer le processus,
inspecter exactement les tokens envoyés après reprise.

**Intégration** — `context` et `sessions` : composition, budget, compaction,
persistance conversationnelle.

---

## 4 · Diriger et contraindre le modèle

*La pièce : augmenter la probabilité d'une sortie utile sans modifier les poids.*

- **4.1 · `instruction-systeme`** — L'instruction système
  - portée réelle d'une instruction
  - séparation entre instruction et donnée
- **4.2 · `exemples-shots`** — Montrer plutôt que décrire
  - zero-shot, one-shot, few-shot
  - exemples positifs, contre-exemples, effet de l'ordre
- **4.3 · `templates-prompts`** — Versionner un prompt
  - variables, Templates
  - versions de prompts
- **4.4 · `raisonnement`** — Le budget de raisonnement
  - modes de raisonnement, budget
  - raisonnement visible contre état interne non exposé
- **4.5 · `sortie-structuree`** — Demander une forme
  - sortie libre, sortie structurée, outil
  - JSON Schema
  - prefill de la réponse
- **4.6 · `decodage-contraint`** — Contraindre le décodage
  - décodage contraint par grammaire
  - masquage des logits, `logit_bias`
- **4.7 · `validation-reparation`** — Valider, réparer, douter
  - validation syntaxique et validation métier
  - réparation, re-prompt, retry
  - cas où une sortie valide reste sémantiquement fausse
- **4.8 · `candidats-multiples`** — Plusieurs candidats
  - self-consistency
  - génération et sélection de candidats
- **4.9 · `evaluer-un-prompt`** — Prouver qu'un prompt est meilleur
  - protocole d'évaluation d'une modification de prompt

**Reconstruction** — contraindre à la main les tokens autorisés pour une petite
grammaire, puis valider un invariant que la grammaire ne peut pas exprimer.

**Cas pratique** — produire le même objet par prompt seul, par validation avec
retry et par décodage contraint, puis comparer validité, contenu et coût.

**Intégration** — `control` : Templates, contraintes, validation, stratégie de
réparation.

---

## 5 · Outils, actions et approbations

*La pièce : transformer une proposition du modèle en effet contrôlé.*

- **5.1 · `function-calling`** — Proposer n'est pas agir
  - function calling natif et émulé
  - le modèle propose un appel, l'exécuteur décide de l'action
- **5.2 · `schema-outil`** — Décrire un outil
  - nom, description, schéma
  - le schéma comme instruction adressée au modèle
  - `tool_choice`
- **5.3 · `appels-correlation`** — Appeler et corréler
  - parsing et validation des arguments
  - identifiant d'appel, corrélation du résultat
  - appels parallèles
- **5.4 · `resultats-outils`** — Rendre un résultat
  - résultat structuré, fichier, image, contenu volumineux
  - troncature et résumé d'un résultat
- **5.5 · `erreurs-outils`** — Échouer utilement
  - erreur de validation, erreur attendue, erreur interne
  - message d'erreur exploitable par le modèle
- **5.6 · `effets-de-bord`** — Classer les effets et leur incertitude
  - lecture, écriture, destruction
  - idempotence, clé d'idempotence
  - timeout, annulation, résultat incertain après coupure
- **5.7 · `permissions`** — Portée d'une capacité
  - permissions, granularité
  - moindre privilège
- **5.8 · `approbations`** — Faire décider un humain
  - approbation humaine avant exécution
  - décision ponctuelle contre permission durable
- **5.9 · `revalidation-audit`** — Au moment de l'effet
  - revalidation des préconditions
  - compensation lorsqu'un effet ne peut pas être annulé
  - journal d'audit

**Reconstruction** — un registre, un dispatcher et une politique qui séparent
proposition, autorisation, exécution et résultat.

**Cas pratique** — lire l'état d'un service du homelab, proposer une
modification, attendre l'approbation, exécuter, vérifier l'effet.

**Intégration** — `tools`, `permissions` et `approvals`.

---

## 6 · MCP

*La pièce : exposer et consommer des capacités distantes sans les confondre avec
le runtime de l'agent.*

- **6.1 · `jsonrpc-roles`** — Le substrat
  - JSON-RPC 2.0 : requêtes, réponses, erreurs, notifications
  - client, serveur, host et leurs responsabilités
- **6.2 · `handshake-versions`** — Ouvrir une connexion
  - initialisation, négociation de version, négociation des capacités
  - compatibilité, fonctions dépréciées, période de transition
- **6.3 · `primitives-mcp`** — Tools, resources et prompts
  - inventaire, appel
  - changement de catalogue
- **6.4 · `ressources-mcp`** — Lire une ressource
  - URI, lecture, abonnement
  - pagination
- **6.5 · `transports-mcp`** — stdio et Streamable HTTP
  - transports
  - cycle de vie d'une connexion
- **6.6 · `interactions-serveur`** — Ce qui remonte pendant un appel
  - annulation, progression
  - tâches longues et extension de tâches durables
  - elicitation et demande d'information à l'utilisateur
- **6.7 · `auth-mcp`** — Authentifier un serveur distant
  - authentification et OAuth pour le transport HTTP
  - portée des credentials prêtés au serveur
- **6.8 · `adaptateur-outils`** — Un seul registre d'outils
  - adaptateur vers le registre du Parcours 5
- **6.9 · `menaces-mcp`** — Frontière de confiance
  - serveur tiers, injection indirecte par une ressource ou un résultat
  - tool poisoning par la description, rug pull après approbation
  - validation, filtrage et approbation côté host

**Reconstruction** — un serveur et un client minimaux, handshake, `tools/list` et
`tools/call` compris.

**Cas pratique** — exposer un outil natif en MCP, le consommer par le même
registre, puis simuler un changement de description et une coupure.

**Intégration** — `mcp` : client, serveur minimal, adaptateur vers `tools`.

---

## 7 · Retrieval et connaissance documentaire

*La pièce : retrouver des sources pertinentes avant de produire une réponse.*

- **7.1 · `ingestion`** — Ingérer des documents réels
  - source, document, fragment, provenance
  - parsing, nettoyage
  - documents structurés, pages, tableaux, code
- **7.2 · `chunking`** — Découper un document
  - chunking fixe, sémantique et structurel
  - recouvrement, contexte parent
- **7.3 · `embeddings-documents`** — Représenter un fragment
  - dimension, normalisation
  - similarité cosinus
- **7.4 · `deux-recherches`** — Vectorielle et lexicale
  - indexation, recherche vectorielle top-k, filtres de métadonnées
  - BM25 et recherche lexicale
  - ce que chacune manque
- **7.5 · `recherche-hybride`** — Fusionner et reranker
  - fusion des rangs
  - reranking bi-encoder et cross-encoder
- **7.6 · `index-ann`** — Le coût d'un index
  - HNSW, compromis rappel, latence et mémoire
  - Qdrant comme store vectoriel concret
- **7.7 · `pipeline-rag`** — Retrouver, composer, répondre
  - pipeline RAG
  - citations, rattachement de chaque affirmation à une source
- **7.8 · `fraicheur-index`** — Maintenir un index
  - fraîcheur, suppression, réindexation
- **7.9 · `graphes-multi-hop`** — Au-delà du top-k
  - GraphRAG, parcours multi-hop
- **7.10 · `evaluer-retrieval`** — Mesurer la récupération
  - rappel, précision, MRR, nDCG, fidélité, pertinence
  - séparation entre évaluation du retrieval et de la génération
- **7.11 · `rag-ou-autre`** — Quand ne pas faire de RAG
  - RAG contre contexte direct, outil ou fine-tuning

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

- **8.1 · `natures-memoire`** — Cinq mémoires distinctes
  - mémoire de travail, mémoire de session
  - mémoire épisodique, sémantique, procédurale
- **8.2 · `supports-memoire`** — Choisir un support
  - clé-valeur pour l'état exact, index vectoriel pour le sens proche
  - graphe pour les entités, relations et parcours
  - wiki auto-écrit pour la connaissance inspectable
- **8.3 · `decision-ecriture`** — Décider de retenir
  - événement, fait, préférence, procédure, observation
  - quoi retenir et pourquoi
  - extraction depuis une conversation ou un résultat d'outil
- **8.4 · `provenance-confiance`** — D'où vient un souvenir
  - provenance, niveau de confiance
- **8.5 · `validite-conflits`** — Un fait qui change
  - validité temporelle, évolution d'un fait
  - correction explicite par l'utilisateur
  - conflit entre souvenirs et arbitrage
- **8.6 · `rappel-memoire`** — Retrouver au bon moment
  - récupération selon la tâche
  - scoring, fréquence, récence, importance
- **8.7 · `consolidation-oubli`** — Consolider et oublier
  - consolidation, decay
  - déduplication
- **8.8 · `isolation-memoire`** — Cloisonner
  - isolation entre utilisateurs, agents et sources
  - contamination, empoisonnement de mémoire
- **8.9 · `sauvegarde-memoire`** — Sauvegarder une mémoire
  - sauvegarde, export, restauration
- **8.10 · `evaluer-memoire`** — Mesurer une mémoire
  - évaluation de l'écriture, du rappel
  - influence réelle sur la réponse

**Reconstruction** — des contrats distincts pour un épisode, un fait et une
procédure, avec la trace de leur écriture et de leur rappel.

**Cas pratique** — apprendre une préférence, enregistrer un événement daté,
corriger un fait devenu faux, prouver que l'ancienne version n'est plus utilisée.

**Intégration** — `memory` : politiques d'écriture, stores spécialisés,
provenance, rappel, consolidation, oubli.

---

## 9 · La boucle mono-agent

*La pièce : transformer plusieurs appels isolés en une exécution bornée.*

- **9.1 · `workflow-ou-agent`** — Workflow ou agent
  - workflow déterministe contre agent qui choisit la suite
- **9.2 · `evenements-run`** — L'état d'un run
  - état éphémère d'un run
  - événement utilisateur, événement modèle, événement outil
- **9.3 · `boucle-oda`** — Observer, décider, agir, intégrer
  - la boucle, l'étape et la transition explicites
  - issues d'un tour : outil, handoff, réponse finale
  - hooks avant et après un appel
- **9.4 · `strategies-raisonnement`** — Stratégies de conduite
  - ReAct, plan puis exécution
  - réflexion et critique, avec leur coût
- **9.5 · `conditions-arret-agent`** — Arrêter la boucle
  - conditions d'arrêt
  - budget de tours, de tokens, de temps et d'outils
- **9.6 · `erreurs-boucle`** — Reprendre après une erreur
  - erreurs de transport, modèle, outil et politique
  - erreur transitoire contre erreur définitive
  - retry, backoff
- **9.7 · `parallelisme-boucle`** — Agir en parallèle
  - appels parallèles, collecte partielle
  - annulation propagée
- **9.8 · `trajectoire`** — La trajectoire comme objet
  - journal d'événements, trajectoire inspectable
- **9.9 · `declenchement`** — Ce qui démarre un run
  - déclenchement par requête, événement ou horaire
  - limite d'une boucle vivant seulement en mémoire du processus

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

- **10.1 · `signaux-correlation`** — Les signaux et leur corrélation
  - événement, log, métrique, trace, span
  - corrélation session, run, agent, outil
- **10.2 · `instrumentation`** — Instrumenter le harnais
  - client modèle : tokens d'entrée, de sortie, de cache et de raisonnement
  - outils, MCP, retrieval, mémoire
- **10.3 · `couts-latences`** — Latence et coût
  - TTFT, latence, durée d'outil, durée totale
  - coût cloud et coût matériel local
- **10.4 · `format-de-trace`** — Un format qui survit au fournisseur
  - OpenTelemetry, conventions GenAI
  - données sensibles, rédaction, rétention
- **10.5 · `replay-trajectoire`** — Rejouer une trajectoire
  - replay d'une trajectoire enregistrée
- **10.6 · `tests-deterministes`** — Tester ce qui est déterministe
  - test unitaire, test de contrat, test d'intégration
- **10.7 · `evals-sortie`** — Évaluer une sortie
  - jeu de données, cas de non-régression
  - exact match, critères, score, distribution
- **10.8 · `evals-composants`** — Évaluer les composants
  - eval de retrieval, de mémoire, de trajectoire
- **10.9 · `llm-as-judge`** — Le modèle comme juge
  - LLM-as-judge, biais, ordre, calibration
  - juge différent du générateur
  - évaluation humaine
- **10.10 · `comparer-et-decider`** — Décider sur des mesures
  - comparaison de modèle, prompt, outil et architecture
  - diagnostic avant fine-tuning
  - alertes, tableaux de bord, SLO personnels

**Reconstruction** — un format de trace indépendant d'un fournisseur, puis une
eval calculée à partir d'événements rejoués.

**Cas pratique** — retrouver la première décision fautive d'une trajectoire et
ajouter le cas de non-régression correspondant.

**Intégration** — `telemetry`, `evals` et `judge`.

---

## 11 · État agentique et exécution durable

*La pièce : survivre aux attentes, aux interruptions et aux redémarrages sans
perdre la position ni répéter aveuglément les effets.*

- **11.1 · `etats-identifiants`** — Le mot « état » recouvre cinq choses
  - processus stateless contre agent logiquement stateful
  - contexte du modèle, session, run, workflow, mémoire
  - identifiants de session, run, workflow, étape, tâche et appel
- **11.2 · `schema-etat`** — Un état sérialisable
  - état éphémère contre état durable
  - schéma typé, sérialisation sûre
  - version de schéma et migration
- **11.3 · `etat-de-controle`** — Où en est l'exécution
  - étape acquise, prochaine étape
  - statuts d'une tâche
- **11.4 · `checkpoints`** — Poser un checkpoint
  - snapshot contre journal d'événements
  - frontière cohérente, fréquence et coût
  - écritures intermédiaires d'une branche parallèle
  - état et checkpoint dans une trace
- **11.5 · `interruption-reprise`** — Attendre sans rester vivant
  - interruption, attente d'une approbation
  - pause sans conserver le processus vivant
  - reprise depuis le dernier checkpoint
- **11.6 · `retry-replay`** — Retry et replay
  - retry d'une opération en échec
  - replay déterministe, enregistrement des résultats non déterministes
  - eval de reprise après panne
- **11.7 · `fork-time-travel`** — Explorer une autre trajectoire
  - fork depuis un checkpoint antérieur
  - time travel pour le diagnostic
- **11.8 · `activites-effets`** — Ce qui ne se rejoue pas
  - appel modèle et appel outil comme activités
  - `at-least-once`, `at-most-once`
  - absence de garantie générale « exactly once »
- **11.9 · `idempotence-effets`** — Un effet, une fois
  - clé d'idempotence
  - journal d'effets, inbox et outbox
  - résultat inconnu après coupure, compensation
- **11.10 · `planification-workers`** — Avancer sans requête
  - timer durable, échéance, tâche planifiée
  - worker, file, lease, récupération d'un travail abandonné
  - concurrence sur un même workflow
- **11.11 · `exploitation-etat`** — Vivre avec un état durable
  - déploiement d'une nouvelle version avec workflows ouverts
  - approbation expirée, revalidation de l'autorité
  - rétention, chiffrement, suppression
- **11.12 · `moteurs-durables`** — Confronter des moteurs
  - SQLite pour la reconstruction locale
  - Temporal, Restate, DBOS, Prefect

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

- **12.1 · `workspace`** — Le workspace n'est pas le contexte
  - fichiers, répertoires, artefacts, cycle de vie d'un workspace
  - montage de données, copie de travail, chemins autorisés
- **12.2 · `execution-code`** — Exécuter du code
  - shell, exécution de code
  - processus enfant
- **12.3 · `isolation`** — Contenir l'exécution
  - conteneur, sandbox
  - limites CPU, mémoire, disque, temps et réseau
- **12.4 · `credentials-isoles`** — Ne pas prêter ses clés
  - séparation des credentials et du code généré
- **12.5 · `artefacts`** — Ce qui mérite d'être gardé
  - artefact produit contre fichier temporaire
  - snapshot et restauration d'un workspace
- **12.6 · `skills`** — Une procédure chargée à la demande
  - skill, procédure et ressources associées
  - divulgation progressive
  - description courte contre contenu complet
- **12.7 · `instructions-en-couches`** — Des instructions en couches
  - instructions globales, projet, agent et tâche
  - résolution des conflits entre couches
- **12.8 · `encadrer-nettoyer`** — Encadrer, installer, nettoyer
  - hooks avant et après outil
  - installation de dépendances, nettoyage
  - audit des fichiers et des commandes

**Reconstruction** — un workspace local doté d'une liste explicite de capacités,
et une skill chargée sans placer tout son contenu dans le contexte.

**Cas pratique** — faire produire un artefact par un sous-processus isolé,
interrompre l'exécution, reprendre avec le même workspace restauré.

**Intégration** — `workspace`, `sandbox`, `skills`, `artifacts` et `hooks`.

---

## 13 · Sous-agents, délégation et état partagé

*La pièce : répartir un travail sans créer une mémoire globale implicite.*

- **13.1 · `quand-et-comment-deleguer`** — Déléguer ou non
  - déterminer quand un agent unique suffit
  - agent utilisé comme outil, handoff de contrôle, superviseur et ouvriers
- **13.2 · `routage`** — Router une demande
  - routeur déterministe contre routeur piloté par modèle
- **13.3 · `contrat-de-resultat`** — Déléguer sous contrat
  - contrat de résultat
  - contexte isolé d'un sous-agent
- **13.4 · `etat-prive`** — L'état privé par défaut
  - état privé par invocation
  - état conservé par thread seulement lorsqu'il est nécessaire
  - namespace de checkpoint par agent et par invocation
- **13.5 · `champs-partages`** — Partager un champ, pas un dictionnaire
  - état parent, champs publics, propriétaire et producteurs autorisés
  - mise à jour partielle
  - reducer, associativité, déterminisme d'une fusion
- **13.6 · `concurrence-ecriture`** — Écrire en concurrence
  - append-only, version, compare-and-swap
  - conflit entre branches
- **13.7 · `fan-out-fan-in`** — Ouvrir, refermer, échouer partiellement
  - fan-out, fan-in, limite de parallélisme
  - backpressure, annulation propagée
  - résultat partiel, échec d'un ouvrier, boucle de délégation
- **13.8 · `partage-d-observation`** — Partager peu
  - partage d'une observation contre partage de tout l'historique
  - mémoire commune contre état de workflow partagé
- **13.9 · `autorite-deleguee`** — Ce qu'un sous-agent a le droit de faire
  - autorité déléguée
  - arbitrage qualité, délai, coût et confidentialité
- **13.10 · `a2a`** — Des agents indépendants
  - A2A comme protocole de culture

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

- **14.1 · `threat-model`** — Modéliser la menace
  - actifs, adversaires, frontières de confiance
  - threat model propre au homelab
  - donnée, instruction, capacité, autorité
- **14.2 · `prompt-injection`** — L'injection
  - injection directe
  - injection indirecte par page, document, outil ou mémoire
  - goal hijacking
- **14.3 · `outils-non-fiables`** — Un outil peut mentir
  - tool poisoning
  - résultat d'outil non fiable
  - excessive agency
- **14.4 · `exfiltration`** — Faire sortir une donnée
  - exfiltration de secrets
  - SSRF, traversée de chemins
- **14.5 · `execution-non-fiable`** — Exécuter du code non fiable
  - commande shell, exécution de code
  - dépendances et supply chain
- **14.6 · `empoisonnement-durable`** — Contaminer ce qui reste
  - serveur MCP malveillant ou compromis
  - empoisonnement du RAG
  - empoisonnement de mémoire persistant
- **14.7 · `attaques-multi-agents`** — Attaquer par la coordination
  - confusion entre agents, effet en cascade
  - état partagé comme canal d'attaque
  - checkpoint contenant des secrets
- **14.8 · `barrieres`** — Les barrières qui tiennent
  - moindre privilège, séparation des credentials
  - sandbox, isolation réseau, allowlist, validation
  - approbation ancienne ou hors contexte, confirmation au moment de l'effet
- **14.9 · `audit-chiffrement`** — Garder une preuve
  - journal d'audit
  - chiffrement, sauvegarde, restauration
- **14.10 · `reponse-incident`** — Après l'incident
  - tests adversariaux
  - détection, révocation, réponse à incident
  - OWASP LLM et OWASP Agentic comme référentiels

**Reconstruction** — tracer les flux de confiance depuis une donnée externe
jusqu'à un outil, une mémoire et un effet durable.

**Cas pratique** — attaquer Mnémos par un document, un outil MCP, une mémoire et
une commande, puis vérifier chaque barrière et la révocation d'un état contaminé.

**Intégration** — `security`, `policy` et `audit`.

---

## 15 · Voix, vision et temps réel

*La pièce : porter plusieurs modalités sans les réduire prématurément à du
texte.*

- **15.1 · `contenu-multimodal`** — Un contenu typé
  - contenu multimodal
  - budget de tokens visuels et audio
- **15.2 · `vision`** — Voir
  - image native contre OCR
  - préparation, redimensionnement, métadonnées, VLM local
  - caméra, consentement, durée de conservation, confidentialité des flux
- **15.3 · `chaine-vocale`** — Deux architectures vocales
  - STT puis LLM puis TTS
  - speech-to-speech
  - formats audio, échantillonnage, encodage, streaming audio
- **15.4 · `tours-de-parole`** — Savoir qui parle
  - détection d'activité vocale, tours de parole
  - echo cancellation
- **15.5 · `barge-in`** — Être interrompu
  - interruption par l'utilisateur pendant la réponse
- **15.6 · `session-temps-reel`** — Une session en temps réel
  - événement temps réel, état de session
  - appel d'outil pendant une conversation vocale
  - approbation vocale et risque d'ambiguïté
- **15.7 · `latence-degrade`** — Tenir la latence
  - latence de bout en bout
  - modèle local contre service cloud
  - mode dégradé sans voix ni vision

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

- **16.1 · `mn-identite`** — Identité et confidentialité
  - personnalité et instructions propres à Mnémos
  - contrats de confidentialité
- **16.2 · `mn-topologie`** — Topologie des agents
  - agents disponibles
  - choix entre skills et sous-agents
- **16.3 · `mn-modeles`** — Modèles et replis
  - modèles locaux, replis cloud autorisés
  - mise à jour des modèles et des dépendances
- **16.4 · `mn-outils-homelab`** — Outils réels
  - outils du homelab
  - API domotique et appareils
- **16.5 · `mn-permissions`** — Autorité
  - matrice des permissions et des approbations
- **16.6 · `mn-sessions-workflows`** — Continuité
  - sessions persistantes, workflows durables
  - état partagé explicitement limité
- **16.7 · `mn-declencheurs`** — Déclenchement
  - tâches déclenchées par requête, horaire ou événement
- **16.8 · `mn-memoire`** — Mémoire personnelle
  - sources de mémoire
  - procédures apprises
- **16.9 · `mn-interfaces`** — Surfaces d'usage
  - voix, vision
  - interface Web, mobile ou terminal
- **16.10 · `mn-exploitation`** — Exploitation
  - observabilité, evals, audit
  - runbook, sauvegarde, restauration, migration
- **16.11 · `mn-acceptation`** — Preuve d'usage
  - mode hors ligne et modes dégradés
  - critères d'acceptation quotidiens
  - conversion des échecs réels en evals de non-régression

Mnémos n'est ni une plateforme multi-tenant, ni un produit commercial, ni un
prétexte pour distribuer prématurément chaque composant.

**Cas pratique** — utiliser Mnémos sur des tâches réelles du homelab, conserver
les trajectoires problématiques, fermer les régressions observées.

**Intégration** — Praxis atteint sa première version stable ; Mnémos devient
l'application qui l'éprouve chaque jour.

---

## Les briques de Praxis

Une brique est déposée à la fin du Parcours qui en ouvre les mécanismes.

- **Préambule** — `contracts`, `config` : types communs, configuration, erreurs
- **0** — `generation` : tokeniser, rendre un Template, échantillonner, arrêter
- **1** — `inference` : décrire et mesurer un runtime local
- **2** — `models`, `client` : contrats par capacité, transport, streaming
- **3** — `context`, `sessions` : composer le contexte, persister les sessions
- **4** — `control` : prompts, sorties contraintes, validation
- **5** — `tools`, `permissions`, `approvals` : enregistrer, autoriser et
  exécuter une action
- **6** — `mcp` : adapter des outils et ressources distants
- **7** — `knowledge`, `retrieval` : ingérer, rechercher, reranker, citer
- **8** — `memory` : écrire, retrouver, consolider, oublier
- **9** — `loop` : exécuter une boucle mono-agent bornée
- **10** — `telemetry`, `evals`, `judge` : observer, rejouer, mesurer
- **11** — `state`, `checkpoints`, `workflow`, `effects` : persister et reprendre
  une exécution
- **12** — `workspace`, `sandbox`, `skills`, `artifacts` : fournir un
  environnement d'action isolé
- **13** — `agents`, `handoffs`, `router` : déléguer et coordonner plusieurs
  agents
- **14** — `security`, `policy`, `audit` : imposer les frontières de confiance
- **15** — `io`, `realtime` : porter la voix, la vision, les interruptions

## Veille transversale

La veille suit sans désorganiser le parcours :

- évolutions de MCP et de ses extensions ;
- A2A et autres protocoles inter-agents ;
- computer use et nouveaux environnements d'exécution ;
- runtimes d'inférence et techniques de cache ;
- modèles de raisonnement, outils et multimodal ;
- moteurs d'exécution durable ;
- stores de mémoire temporelle et graphes ;
- standards d'observabilité GenAI ;
- nouvelles classes d'attaques agentiques.
