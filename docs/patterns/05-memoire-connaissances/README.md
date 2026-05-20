# Patterns de mémoire et de connaissances

Ces patterns empêchent la mémoire agentique de devenir un vrac sémantique. Ils organisent rappel, vérité, rétention, désindexation et correction.

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
| Registre de rétention | Décide durable, archive, TTL, désindexation ou purge. |
| Memory gate | Contrôle lectures, écritures, indexation et invalidation. |
| Rapport de drift | Signale divergence entre documentation, runtime et mémoire. |
