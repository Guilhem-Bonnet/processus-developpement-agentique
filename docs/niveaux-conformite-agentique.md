# Niveaux de conformité agentique

Cette page propose une échelle de conformité pour évaluer une structure agentique. Elle permet de savoir si le système est seulement assisté par IA, réellement orchestré, ou suffisamment gouverné pour fonctionner comme base d'entreprise-agent.

## Vue d'ensemble

| Niveau | Nom | Description courte |
| --- | --- | --- |
| 0 | Conversationnel | L'IA aide ponctuellement, sans structure opérable. |
| 1 | Minimal | Les missions, cartes, preuves et validations existent. |
| 2 | Contrôlé | Les accès, outils, hooks et risques sont gouvernés. |
| 3 | Orchestré | Les subagents, contextes, modèles et handoffs sont structurés. |
| 4 | Gouverné | Les evals, SLO, incidents, rétention et autorités sont formalisés. |
| 5 | Mature | Le système est observable, auditable, prouvé et améliorable en continu. |

## Niveau 0 : conversationnel

| Critère | État |
| --- | --- |
| Mission | demande informelle. |
| Orchestration | agent unique ou conversation libre. |
| Contexte | fourni manuellement, non qualifié. |
| Preuves | occasionnelles. |
| Conformité | non conforme au standard de structure agentique. |

## Niveau 1 : minimal

| Exigence | Attendu |
| --- | --- |
| Mission | brief ou demande structurée avec objectif, scope et critères. |
| Kanban | cartes avec statut, owner, risques et preuves attendues. |
| Délégation | task envelope pour travaux non triviaux. |
| Handoff | résumé structuré avec preuves et limites. |
| Preuves | evidence pack simple ou preuve équivalente pour les fermetures. |
| Validation | client ou validateur identifié. |

## Niveau 2 : contrôlé

| Exigence | Attendu |
| --- | --- |
| Permissions | registre d'outils et droits par carte. |
| Hooks | contrôles avant outil, écriture, mémoire et livraison. |
| Hook lifecycle | modes shadow, canary, enforced ou équivalent pour les hooks nouveaux. |
| Risques IA | registre défauts IA et contrôles associés. |
| Claim ledger | obligatoire pour affirmations critiques. |
| Sécurité | règles pour secrets, données sensibles et réseau. |

## Niveau 3 : orchestré

| Exigence | Attendu |
| --- | --- |
| Subagents | rôles spécialisés avec prompts, outils et sorties. |
| Contexte | context router, budgets et sources par rôle. |
| Modèles | model router, fallback, coûts et confidentialité. |
| Communication | consultations inter-agents tracées. |
| Ledger | événements de mission et transitions critiques tracés. |
| Handoffs | passage d'étape basé sur preuves et DoD. |

## Niveau 4 : gouverné

| Exigence | Attendu |
| --- | --- |
| Evals | jeux de cas pour prompts, modèles ou workflows critiques. |
| SLO | coût, latence, qualité, faux Done, rework ou validation. |
| Incidents | détection, containment, rollback, purge mémoire et post-mortem. |
| Rétention | politique durable/archive/TTL/désindexation/purge. |
| Surfaces runtime | registre des prompts, agents, skills, hooks, workflows et artefacts de sortie. |
| Autorités | RACI et validateurs par domaine. |

## Niveau 5 : mature

| Exigence | Attendu |
| --- | --- |
| Observabilité | traces bout en bout des décisions, outils, coûts et validations. |
| Auditabilité | capacité à reconstruire pourquoi une décision a été prise. |
| Conformité prouvée | matrice reliant exigences, preuves, owners et risques résiduels. |
| Amélioration | incidents et métriques alimentent evals, hooks, prompts et patterns. |
| Résilience | fallback modèles/outils, modes dégradés, reprise contrôlée. |
| Hygiène mémoire | audits périodiques du corpus, embeddings, graphe, sources et connaissances durables. |
| Drift documentaire | détection entre docs, manifests, runtime, workflows et mémoire. |

## Règles de conformité

- Un niveau est atteint seulement si toutes ses exigences obligatoires sont satisfaites.
- Un niveau supérieur implique les exigences des niveaux précédents.
- Une exception doit être documentée avec justification, risque, propriétaire et date de revue.
- Une conformité déclarative sans preuve est non conforme.
- Un système peut être conforme sur un périmètre limité, par exemple documentation, code local ou mission sans production.

## Matrice de vérification rapide

| Domaine | N1 | N2 | N3 | N4 | N5 |
| --- | --- | --- | --- | --- | --- |
| Mission structurée | oui | oui | oui | oui | oui |
| Kanban agentique | oui | oui | oui | oui | oui |
| Task envelope | oui | oui | oui | oui | oui |
| Evidence pack/verdict | partiel | partiel | oui | oui | oui |
| Mission ledger | non requis | partiel | oui | oui | oui |
| Permissions outils | non requis | oui | oui | oui | oui |
| Hooks | non requis | oui | oui | oui | oui |
| Hook lifecycle | non requis | partiel | oui | oui | oui |
| Subagents spécialisés | non requis | partiel | oui | oui | oui |
| Context router | non requis | partiel | oui | oui | oui |
| Mémoire hybride | non requis | non requis | partiel | oui | oui |
| Model router | non requis | partiel | oui | oui | oui |
| Evals et SLO | non requis | non requis | partiel | oui | oui |
| Incidents et rollback | non requis | partiel | partiel | oui | oui |
| Rétention et nettoyage | non requis | partiel | partiel | oui | oui |
| Surfaces runtime gouvernées | non requis | partiel | partiel | oui | oui |
| Matrice preuves/conformité | non requis | non requis | partiel | oui | oui |
| Doc drift detector | non requis | non requis | non requis | partiel | oui |
| Observabilité complète | non requis | non requis | partiel | partiel | oui |
