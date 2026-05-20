# Contrats formels agentiques

Cette page formalise les schémas minimaux des interfaces agentiques. Les templates complets peuvent rester en Markdown, YAML ou JSON, mais les champs ci-dessous définissent la structure vérifiable attendue.

## Niveaux d'obligation

| Niveau | Sens |
| --- | --- |
| required | Champ obligatoire pour que le contrat soit valide. |
| recommended | Champ attendu sauf justification. |
| conditional | Champ obligatoire dans certains profils de risque. |
| optional | Champ utile mais non requis. |

## Task envelope

| Champ | Obligation | Rôle |
| --- | --- | --- |
| mission_id | required | Relier la tâche à la mission. |
| task_id | required | Identifier le lot délégué. |
| stage | required | Situer l'étape du processus. |
| role | required | Définir le subagent ou rôle attendu. |
| objective | required | Décrire le résultat attendu. |
| scope | required | Délimiter fichiers, domaines ou actions incluses. |
| out_of_scope | recommended | Bloquer les dérives connues. |
| context_pack_ref | conditional | Relier la tâche au contexte vérifié. |
| allowed_tools | required | Limiter les outils. |
| denied_tools | recommended | Rendre explicites les interdictions. |
| model_policy | conditional | Définir modèle, fallback et contraintes. |
| success_criteria | required | Rendre le Done testable. |
| expected_handoff | required | Imposer la sortie structurée. |
| validation_authority | conditional | Identifier qui peut accepter ou bloquer. |

## Context pack

| Champ | Obligation | Rôle |
| --- | --- | --- |
| mission_id | required | Relier le contexte à la mission. |
| context_profile | required | Intake, discovery, architecture, QA, sécurité, etc. |
| budget | required | tiny, small, medium ou deep. |
| objective | required | Expliquer pourquoi ce contexte est composé. |
| included_sources | required | Sources transmises avec statut, raison et confiance. |
| excluded_sources | recommended | Sources volontairement rejetées et raison. |
| constraints | required | Contraintes de vérité, sécurité, confidentialité. |
| scorecard | conditional | Suffisance, provenance, fraîcheur, sensibilité, cohérence. |
| open_questions | recommended | Ambiguïtés non résolues. |
| expiry | recommended | TTL ou déclencheur d'invalidation. |

## Handoff packet

| Champ | Obligation | Rôle |
| --- | --- | --- |
| task_id | required | Relier la sortie à la tâche. |
| summary | required | Résumer ce qui a été produit. |
| changes | recommended | Décrire artefacts ou décisions modifiés. |
| evidence | required | Relier aux preuves disponibles ou manquantes. |
| assumptions | required | Séparer hypothèses et faits. |
| risks | required | Lister risques nouveaux ou résiduels. |
| claims | conditional | Alimenter le claim ledger si affirmation critique. |
| memory_candidates | recommended | Proposer ce qui peut être promu, archivé ou purgé. |
| next_trigger | required | Indiquer étape suivante, correction ou escalade. |

## Evidence pack

| Champ | Obligation | Rôle |
| --- | --- | --- |
| evidence_pack_id | required | Identifier le paquet de preuves. |
| task_id | required | Relier à la carte ou tâche. |
| profile | required | light, standard, strict, security_critical ou release. |
| criteria_coverage | required | Mapper critères et preuves. |
| evidence_items | required | Tests, logs, traces, captures, diff, rapports. |
| digests | conditional | Vérifier intégrité des preuves critiques. |
| limitations | required | Rendre visibles les limites de validation. |
| proposed_decision | required | passed, failed, skipped ou error. |

## Verification verdict

| Champ | Obligation | Rôle |
| --- | --- | --- |
| verdict_id | required | Identifier le verdict. |
| evidence_pack_id | required | Relier au paquet de preuves. |
| validator | required | Identifier l'autorité de validation. |
| checks | required | Contrôles effectués et résultats. |
| global_result | required | passed, failed, skipped ou error. |
| decision | required | close_task, reopen_task, create_incident ou escalate. |
| residual_risks | required | Risques acceptés ou non. |
| closure_conditions | conditional | Conditions si fermeture différée. |

## Memory record

| Champ | Obligation | Rôle |
| --- | --- | --- |
| memory_id | required | Identifier la mémoire. |
| source_id | required | Relier à une source vérifiable. |
| type | required | fait, décision, préférence, incident, apprentissage. |
| scope | required | mission, projet, produit, organisation, utilisateur. |
| subject | required | Sujet filtrable. |
| content | required | Contenu minimal. |
| status | required | candidate, active, durable_memory, archived, superseded, obsolete, sensitive. |
| confidence | required | Niveau de confiance. |
| sensitivity | required | Classification de sensibilité. |
| valid_from | recommended | Début de validité. |
| valid_until | recommended | Fin ou revue prévue. |
| retention_class | required | durable, projet, mission, court terme, purge. |
| indexable | required | oui/non et raison. |

## Incident record

| Champ | Obligation | Rôle |
| --- | --- | --- |
| incident_id | required | Identifier l'incident. |
| trigger | required | Décrire le signal de détection. |
| impact | required | Décrire périmètre touché. |
| severity | required | Classer gravité. |
| contaminated_memory | conditional | Identifier mémoires à purger ou corriger. |
| containment | required | Décrire réduction d'autonomie ou blocage. |
| correction | required | Décrire correction. |
| prevention | required | Hook, eval, règle ou documentation à ajouter. |

## Pattern record

| Champ | Obligation | Rôle |
| --- | --- | --- |
| pattern_id | required | Identifier le pattern. |
| family | required | Classer la responsabilité principale. |
| status | required | proposed, experimental, stable, normative, deprecated ou retired. |
| maturity | required | M0 à M5. |
| definition | required | Intention, problème, solution, contrôles, anti-pattern. |
| related_requirements | required | Exigences AG-* couvertes. |
| expected_evidence | required | Preuves attendues. |
| relations | recommended | Dépendances, contrôles, corrections. |
| owner | recommended | Rôle responsable. |
| review_trigger | recommended | Événement de revue. |

## Règle finale

Les contrats peuvent être enrichis, mais leurs champs requis ne doivent pas disparaître. Une interface agentique non structurée devient rapidement impossible à auditer.
