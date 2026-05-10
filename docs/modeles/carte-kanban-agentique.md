# Modèle de carte Kanban agentique

## Métadonnées

| Champ | Valeur |
| --- | --- |
| ID carte | A renseigner |
| Titre | A renseigner |
| Type | feature / bug / refactor / sécurité / design / ops / doc / agentique |
| Statut | signal / cadrage / prêt / en cours / consultation / vérification / validation / livré / capitalisé |
| Priorité | basse / moyenne / haute / critique |
| Niveau de risque | faible / moyen / élevé / critique |
| Demandeur | A renseigner |
| Validateur final | A renseigner |
| Owner agentique | orchestrateur / analyste / architecte / dev / design / QA / sécurité / ops / doc |

## Besoin et portée

| Champ | Valeur |
| --- | --- |
| Problème | A renseigner |
| Valeur attendue | A renseigner |
| Scope | A renseigner |
| Hors-scope | A renseigner |
| Critères d'acceptation | A renseigner |
| Décisions ouvertes | A renseigner |

## Contexte et défauts IA

| Champ | Valeur |
| --- | --- |
| Sources de vérité | A renseigner |
| Profil de contexte | intake / discovery / architecture / implémentation / QA / sécurité / livraison |
| Budget contexte | tiny / small / medium / deep |
| Routage LLM | modèle principal, fallback, justification, eval requise |
| Rétention des sources | active / archive / superseded / obsolete, TTL, indexable |
| Défauts IA plausibles | hallucination / oubli / surconfiance / faux Done / mémoire polluée |
| Claim ledger requis | oui / non |
| Critique requise | non / checklist / subagent critique / revue humaine |

## Permissions

| Action | Autorisée | Conditions |
| --- | --- | --- |
| Lecture workspace | oui / non | A renseigner |
| Écriture locale | oui / non | A renseigner |
| Tests / build / lint | oui / non | A renseigner |
| Réseau | oui / non | A renseigner |
| MCP | oui / non | A renseigner |
| Dépôt distant | oui / non | A renseigner |
| Production | non par défaut | validation explicite |

## Orchestration

| Élément | Valeur |
| --- | --- |
| Subagents impliqués | A renseigner |
| Task envelope | A renseigner ou lien |
| Consultations inter-agents | A renseigner |
| Handoff attendu | résumé, preuves, hypothèses, risques, prochain trigger |
| Dry-run requis | oui / non |
| Rollback | A renseigner |

## Rétention et nettoyage

| Champ | Valeur |
| --- | --- |
| Artefacts durables | A renseigner |
| Artefacts temporaires | A renseigner |
| Sources à désindexer | A renseigner |
| Sources à archiver | A renseigner |
| Sources à purger | A renseigner |
| Mémoire durable candidate | A renseigner |

## Preuves de fermeture

| Preuve | Résultat |
| --- | --- |
| Tests | A renseigner |
| Lint / build | A renseigner |
| Scan sécurité | A renseigner |
| Revue design / QA | A renseigner |
| Claim ledger | A renseigner |
| Validation client | A renseigner |

## Handoff final

| Champ | Valeur |
| --- | --- |
| Résumé | A renseigner |
| Fichiers ou artefacts | A renseigner |
| Risques résiduels | A renseigner |
| Mémoire à écrire ou invalider | A renseigner |
| Rétention décidée | durable / archive / TTL / désindexation / purge |
| Prochain trigger | A renseigner |
