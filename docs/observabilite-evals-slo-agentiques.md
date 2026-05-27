# Observabilité, evals et SLO agentiques

Cette page transforme la fiabilité agentique en système mesurable. Une entreprise-agent doit pouvoir répondre à quatre questions : que s'est-il passé, pourquoi, à quel coût et avec quel niveau de confiance. Le modèle détaillé de traces, métriques, logs et événements est défini dans [observabilite-telemetrie-agentique.md](observabilite-telemetrie-agentique.md).

## Objectifs

| Objectif | Pourquoi |
| --- | --- |
| Rendre les runs auditables | Reconstituer contexte, outils, subagents, décisions et preuves. |
| Mesurer la qualité | Suivre acceptation, rework, faux Done, hallucinations et validations. |
| Piloter le coût | Mesurer tokens, latence, cache, escalades et modèles utilisés. |
| Améliorer les agents | Alimenter evals, prompts, skills, garde-fous et backlog. |
| Détecter les dérives | Identifier mémoire périmée, outil instable, subagent faible ou coût anormal. |

## Traces agentiques

| Segment de trace | Contenu minimal |
| --- | --- |
| Mission | id, client, type, risque, validateur, statut Kanban. |
| Contexte | profil, budget, sources retenues, sources rejetées, scores, fraîcheur. |
| Prompt | version, rôle, instructions projet, task envelope, capability pack, skill. |
| Outil | nom, paramètres sensibles masqués, durée, résultat, erreur. |
| Subagent | rôle, budget, outils, sortie, handoff, critique. |
| Décision | options, preuve, hypothèse, validateur, décision. |
| Ledger | événement mission, transition, actor, raison, tâche et preuve liée. |
| Vérification | evidence pack, verdict, tests, lint, scans, rendu, evals, revue, go/no-go. |
| Surface runtime | prompt, skill, agent, hook, workflow ou artefact créé, modifié, promu ou purgé. |
| Workflow | état, transition, guard, interruption, preuve requise. |
| Trajectoire | intention, contexte, décision, action, observation, correction, verdict. |
| Browser | URL scope, action, DOM snapshot, screenshot, logs console/réseau. |
| Coût | tokens entrée/sortie, provider, modèle, cache hit, latence, coût estimé. |

La trace ne doit pas stocker de secrets ni de données personnelles inutiles. Elle doit stocker assez pour expliquer une décision.

## Métriques principales

| Famille | Métriques |
| --- | --- |
| Delivery | lead time, cycle time, débit Kanban, WIP, cartes bloquées. |
| Qualité | taux d'acceptation premier passage, rework, défauts échappés, tests passants. |
| Agentique | hallucinations détectées, faux Done évités, actions bloquées, questions client. |
| Contexte | budget moyen, taux de récupération utile, cache hit Redis, sources périmées. |
| Coût | tokens par carte, coût par livrable, latence, escalades vers modèle profond. |
| Sécurité | prompt injections détectées, secrets bloqués, accès refusés, MCP en erreur. |
| Validation | temps d'attente humain, décisions en suspens, revues critiques bloquantes. |
| Modèles | succès par modèle, coût par modèle, taux d'erreur, fallback, variance. |
| Providers LLM | appels par provider, rejets hors registry, fallback provider, conformité data policy. |
| Runtime | surfaces créées, promues, retirées, drifts détectés, hooks en shadow/canary/enforced. |
| Sessions | crashs, quarantaines, idle kills, unhealthy rate par model/prompt/rig. |

## SLO agentiques

Les SLO doivent être adaptés au contexte. Ils ne sont pas des promesses universelles, mais des objectifs de pilotage.

| SLO | Exemple de cible | Signal d'alerte |
| --- | --- | --- |
| Acceptation premier passage | 80 % des cartes faibles risques acceptées sans rework majeur. | chute sous 65 %. |
| Faux Done | 0 faux Done critique accepté. | 1 faux Done critique. |
| Preuve de fermeture | 95 % des cartes livrées avec preuve vérifiable. | carte livrée sans preuve. |
| Coût de contexte | 90 % des tâches ciblées restent en budget small ou medium. | dérive fréquente en deep. |
| Latence de vérification | QA automatique sous seuil projet. | validation trop lente ou non lancée. |
| Sécurité | 100 % des actions sensibles passent par validation. | action sensible non validée. |
| Mémoire | 0 secret ou donnée personnelle inutile mémorisée. | fuite ou mémoire non sourcée. |
| Evals critiques | 100 % des evals bloquantes passent avant release agentique. | eval critique échouée. |
| Verdicts critiques | 100 % des tâches à risque ont un verification verdict. | fermeture sans verdict. |
| Drift documentaire | 0 drift bloquant avant release. | manifest, hook ou doc incohérent. |
| Runtime session health | CrashRate et UnhealthyRate sous seuil projet. | session quarantined, idle kill ou crash répété. |
| Prompt/version regression | 0 régression critique non rollbackée. | baisse eval ou hausse faux Done par version. |

## Evals agentiques

Les evals testent un comportement d'agent, pas seulement une sortie textuelle. Elles doivent couvrir les cas normaux, limites et adversariaux.

| Type d'eval | Ce qu'elle vérifie |
| --- | --- |
| Cadrage ambigu | L'agent questionne au lieu d'inventer. |
| Source contradictoire | L'agent détecte le conflit et baisse sa confiance. |
| Outil en erreur | L'agent ne transforme pas un échec en succès. |
| Prompt injection | L'agent sépare instructions et contenu non fiable. |
| Contexte absent | L'agent demande la source plutôt que de produire au hasard. |
| Design sans charte | L'agent exige validation DA ou propose une direction à valider. |
| Sécurité sensible | L'agent bloque ou escalade avant action. |
| Handoff incomplet | L'agent refuse le passage d'étape. |
| Mémoire périmée | L'agent vérifie la source originale. |
| Coût excessif | L'agent compresse ou réduit le contexte. |
| Evidence pack incomplet | L'agent refuse la fermeture ou demande preuve manquante. |
| Modèle retiré | L'agent applique fallback ou suspension. |
| Provider non déclaré | L'agent bloque l'appel ou route vers provider autorisé. |
| Prompt régressif | L'agent détecte la version fautive et rollback/canary. |
| Browser risqué | L'agent refuse action hors scope ou exige preuve visuelle. |
| Transition sans preuve | L'agent bloque le changement d'état. |
| Drift runtime/doc | L'agent détecte la divergence et crée une carte de correction. |

## Scorecard de run

| Dimension | Score attendu |
| --- | --- |
| Besoin | clair / ambigu / bloqué. |
| Contexte | suffisant / incomplet / contradictoire / périmé. |
| Preuves | fortes / partielles / absentes. |
| Sécurité | conforme / risque résiduel / bloquant. |
| Coût | normal / élevé justifié / dérive. |
| Qualité | validée / à reprendre / non vérifiée. |
| Critique | non requise / passée / bloquante. |
| Client | accepté / décision attendue / refusé. |

## Tableau de bord minimal

Un tableau de bord opérationnel doit afficher :

- cartes en cours, bloquées, en validation et livrées ;
- coûts tokens par mission, rôle et modèle ;
- taux de cache Redis et escalades de contexte ;
- hallucinations, faux Done et contradictions détectées ;
- actions bloquées par hook ;
- hooks en shadow, canary, enforced et retired ;
- evidence packs et verification verdicts par release ;
- drifts entre docs, manifests, runtime et mémoire ;
- evals passantes et échouées ;
- délais de validation humaine ;
- incidents ouverts et post-mortems en attente.

## Boucle d'amélioration

1. Collecter traces, métriques, logs et résultats d'evals.
2. Identifier les dérives : coût, qualité, sécurité, contexte ou modèle.
3. Créer une carte Kanban d'amélioration.
4. Mettre à jour prompt, skill, garde-fou, eval ou documentation.
5. Vérifier que la métrique s'améliore sur les runs suivants.

## Règle finale

Ce qui n'est pas observé ne peut pas être gouverné. Une entreprise-agent fiable mesure autant ses hésitations, blocages et erreurs évitées que ses livraisons réussies.
