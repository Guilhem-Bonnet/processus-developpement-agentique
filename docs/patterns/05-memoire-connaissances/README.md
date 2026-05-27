# Patterns de mémoire et de connaissances

Ces patterns empêchent la mémoire agentique de devenir un vrac sémantique. Ils organisent rappel, vérité, rétention, désindexation et correction.

Ils distinguent trois plans qui sont souvent confondus :

| Plan | Rôle | Ce que ce n'est pas |
| --- | --- | --- |
| Base de connaissance indexée | Corpus externe gouverné, branché via repo, URL, API, MCP, base de données ou dossier, puis rendu recherchable. | Ce n'est pas la mémoire de l'agent. |
| Mémoire agentique | Ce que le système retient de ses missions, décisions, incidents et apprentissages. | Ce n'est pas une documentation métier exhaustive. |
| Contexte de session | Paquet minimal transmis à une tâche ou un subagent. | Ce n'est pas une base durable. |

La source Mermaid de cette famille est disponible dans [../../../diagrammes/patterns-memoire-connaissances.mmd](../../../diagrammes/patterns-memoire-connaissances.mmd).

## KNO-01 : Knowledge janitor

| Élément | Description |
| --- | --- |
| Intention | Empêcher la mémoire et les documents de devenir toxiques ou ingouvernables. |
| Problème | Les vieux rapports, traces et décisions remplacées polluent le contexte futur. |
| Solution | Classer artefacts en durable, archive, TTL, désindexation ou purge. |
| Contrôles | Pre-index, Scheduled-cleanup, registre de rétention, source registry. |
| Anti-pattern | Tout indexer parce que tout pourrait servir un jour. |

## KNO-02 : Mémoire hybride

| Élément | Description |
| --- | --- |
| Intention | Combiner rappel sémantique, relations et faits temporels. |
| Problème | Une vector DB seule rappelle des textes similaires sans comprendre validité ni dépendances. |
| Solution | Associer vectoriel, graphe, sidecar structuré, journal et sources de vérité. |
| Contrôles | Source registry, memory gate, valid_from/valid_to, désindexation. |
| Anti-pattern | Traiter le résultat vectoriel comme une vérité. |

## KNO-03 : Doc drift detector

| Élément | Description |
| --- | --- |
| Intention | Empêcher la divergence entre documentation, manifests, hooks, workflows et mémoire. |
| Problème | Le runtime évolue plus vite que le standard documentaire, ou inversement. |
| Solution | Comparer surfaces déclarées, fichiers réels, registres, sources actives et preuves de workflow. |
| Contrôles | Hook doc-drift-check, release gate, rapport de drift, owner de correction. |
| Anti-pattern | Considérer la documentation comme vraie sans vérifier le runtime. |

## KNO-04 : Knowledge promotion

| Élément | Description |
| --- | --- |
| Intention | Transformer une sortie temporaire en connaissance durable seulement si elle le mérite. |
| Problème | Les handoffs, rapports et notes temporaires sont souvent indexés trop tôt ou jamais capitalisés correctement. |
| Solution | Évaluer chaque candidat selon stabilité, source, réutilité, sensibilité, propriétaire et expiration, puis promouvoir, archiver ou purger. |
| Contrôles | Pre-memory-write, registre de rétention, evidence pack, source registry. |
| Anti-pattern | Tout indexer ou ne rien capitaliser. |

### Critères de promotion

| Critère | Seuil |
| --- | --- |
| Stabilité | Le fait ne dépend pas d'un état temporaire non figé. |
| Source | Une source active ou preuve vérifiée existe. |
| Réutilité | L'information servira probablement plusieurs missions. |
| Sensibilité | La donnée est non sensible ou minimisée. |
| Propriétaire | Un rôle peut corriger ou retirer la connaissance. |
| Expiration | TTL ou trigger de revue défini. |

## KNO-05 : Memory contamination response

| Élément | Description |
| --- | --- |
| Intention | Réparer une mémoire fausse, sensible ou obsolète déjà utilisée par le système. |
| Problème | Une mémoire contaminée peut influencer plusieurs tâches avant d'être détectée. |
| Solution | Déclarer incident, identifier portée, purger ou corriger la mémoire, invalider caches, réviser décisions impactées et ajouter une prévention. |
| Contrôles | Incident report, memory audit, désindexation, eval de prévention, doc drift detector. |
| Anti-pattern | Corriger seulement la réponse visible sans nettoyer la source contaminée. |

### Réponse minimale

| Étape | Action |
| --- | --- |
| Détection | Identifier signal, source et missions potentiellement touchées. |
| Containment | Réduire autonomie, bloquer réutilisation, invalider cache. |
| Correction | Corriger source, supprimer embedding, ajouter superseded_by si nécessaire. |
| Revalidation | Rejouer décisions ou tâches impactées si critique. |
| Prévention | Ajouter hook, eval, règle de promotion ou cleanup. |

## KNO-06 : Knowledge Base Indexer

| Élément | Description |
| --- | --- |
| Intention | Greffer une base documentaire externe au système agentique pour spécialiser un flow sur un domaine, produit, client ou entreprise. |
| Problème | Un agent générique ne connaît pas les spécifications internes, procédures, APIs, contraintes métier ou historiques de décision d'une organisation. Tout mettre en prompt ou en mémoire agentique mélange les responsabilités et devient ingouvernable. |
| Solution | Déclarer des sources de connaissance externes via connecteurs (repo, URL, API, MCP, base de données, dossier), les indexer avec métadonnées, ACL, fraîcheur et stratégie de réindexation, puis exposer la recherche à l'orchestrateur de contexte. |
| Contrôles | Pre-index, source owner, ACL, sensibilité, freshness check, réindexation, désindexation, source quarantine. |
| Anti-pattern | Appeler cette base “mémoire” ou injecter toute la documentation dans chaque prompt. |

### Connecteurs typiques

| Connecteur | Usage | Point de contrôle |
| --- | --- | --- |
| Repo Git | Code, docs, ADR, specs versionnées. | Branche, commit, owner, secret scan, fraîcheur. |
| URL / site docs | Documentation produit ou fournisseur. | Crawl scope, robots/politiques, date de capture, hash. |
| API | Référentiel métier, tickets, catalogue, CRM. | Auth, rate limit, champs sensibles, pagination. |
| MCP | Source exposée comme outil/serveur. | MCP Trust Gate, permissions, variables d'environnement. |
| Base de données | Données structurées ou catalogue interne. | Read-only, requêtes autorisées, masquage. |
| Dossier local | Documentation client, exports, procédures. | Classification, owner, indexable, TTL. |

### Pipeline d'indexation

| Étape | Sortie attendue |
| --- | --- |
| Déclaration | `knowledge-source-index` avec owner, type, périmètre, ACL et sensibilité. |
| Ingestion | Documents découpés avec source_id, version, hash et provenance. |
| Enrichissement | Métadonnées, langue, produit, domaine, validité, tags et relations. |
| Indexation | Index lexical, vectoriel et/ou graphe selon usage. |
| Recherche | Résultats candidats avec score, extrait, source, fraîcheur et restrictions. |
| Vérification | Retour à la source active pour décisions critiques. |
| Réindexation | Trigger par commit, webhook, calendrier, version ou incident. |

## KNO-07 : Memory integrity validator

| Élément | Description |
| --- | --- |
| Intention | Vérifier que les mémoires utilisées restent sourcées, fraîches et non contaminées. |
| Problème | Une mémoire durable peut devenir fausse, obsolète, sensible ou contradictoire avec une source active. |
| Solution | Auditer périodiquement les mémoires par provenance, validité, TTL, contradictions, usage récent et sensibilité. |
| Contrôles | Memory routing policy, source registry, contamination response, doc drift detector. |
| Anti-pattern | Réutiliser une mémoire ancienne parce qu'elle est souvent similaire aux demandes courantes. |

## KNO-08 : Doc-to-graph pipeline

| Élément | Description |
| --- | --- |
| Intention | Transformer un corpus documentaire en graphe de relations exploitable et vérifiable. |
| Problème | L'indexation vectorielle retrouve des passages mais ne représente pas dépendances, contradictions, supersessions ou preuves. |
| Solution | Extraire nœuds et relations depuis docs/code/ADR/tickets/API, avec provenance, confiance et statut de fraîcheur. |
| Contrôles | Source graph record, relation provenance, conflict resolver, freshness check. |
| Anti-pattern | Construire un graphe d'hypothèses non sourcées ou non révisables. |

## KNO-09 : Knowledge narrative packaging

| Élément | Description |
| --- | --- |
| Intention | Présenter une connaissance complexe sous une forme narrative exploitable par humains et agents. |
| Problème | Un graphe ou un index peut être correct mais trop fragmenté pour onboarding, audit ou décision. |
| Solution | Générer des packages narratifs sourcés : résumé, décisions, concepts, dépendances, risques, exemples et preuves. |
| Contrôles | Claim ledger, source graph, doc drift, owner, date de validité. |
| Anti-pattern | Produire une synthèse persuasive sans liens vers sources actives. |

## KNO-10 : Source Graph Resolver

| Élément | Description |
| --- | --- |
| Intention | Résoudre les relations entre sources pour éviter qu'une similarité soit prise pour une preuve. |
| Problème | Code, documentation, ADR, tickets, API et mémoire peuvent dépendre, se contredire ou se remplacer sans que le RAG le voie. |
| Solution | Interroger le graphe source pour retrouver dépendances, supersessions, contradictions, preuves et source active avant décision. |
| Contrôles | Source graph record, context conflict resolver, claim ledger, freshness check. |
| Anti-pattern | Utiliser seulement top-k vectoriel pour arbitrer une contradiction documentaire. |

## Relation avec l'orchestrateur de contexte avancé

La mémoire hybride fournit des couches de rappel et de vérité. L'orchestrateur de contexte avancé, défini dans [02-orchestration-contexte](../02-orchestration-contexte/README.md#orc-05--orchestrateur-de-contexte-avance), décide quelles couches utiliser, comment les pondérer, quoi exclure, quoi vérifier et quoi transmettre.

| Couche mémoire | Décision de l'orchestrateur |
| --- | --- |
| Fenêtre active | Conserver seulement l'objectif immédiat et le dernier état utile. |
| Contexte chaud | Utiliser si mission, TTL et version correspondent. |
| Vectoriel | Utiliser comme rappel candidat, jamais comme vérité. |
| Graphe | Utiliser pour dépendances, provenance et contradictions. |
| Sidecar structuré | Utiliser pour faits temporels, confiance et validité. |
| Journal append-only | Utiliser pour audit, reprise et causalité. |
| Source de vérité | Utiliser pour toute décision critique. |

## Interfaces liées

| Interface | Rôle |
| --- | --- |
| Source registry | Donne statut, propriétaire, sensibilité et validité. |
| Knowledge source index | Déclare les corpus externes indexables, leurs connecteurs, ACL et règles de réindexation. |
| Memory routing policy | Définit l'usage des couches mémoire/connaissance/source selon situation. |
| Source graph record | Décrit nœuds, relations, contradictions et provenance. |
| Source graph resolver | Résout dépendances, contradictions et supersessions avant décision. |
| Registre de rétention | Décide durable, archive, TTL, désindexation ou purge. |
| Memory gate | Contrôle lectures, écritures, indexation et invalidation. |
| Rapport de drift | Signale divergence entre documentation, runtime et mémoire. |
