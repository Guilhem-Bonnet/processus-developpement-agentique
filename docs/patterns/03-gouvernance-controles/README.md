# Patterns de gouvernance et de contrôles

Ces patterns empêchent les actions non autorisées, les choix implicites de modèle et les changements risqués sans simulation ni validation.

La source Mermaid de cette famille est disponible dans [../../../diagrammes/patterns-gouvernance-controles.mmd](../../../diagrammes/patterns-gouvernance-controles.mmd).

## GOV-01 : Policy engine et hooks

| Élément | Description |
| --- | --- |
| Intention | Prévenir les actions non autorisées avant qu'elles se produisent. |
| Problème | Les agents peuvent appeler outils, écrire, pousser ou supprimer au mauvais moment. |
| Solution | Intercepter les moments critiques avec règles allow, block ou escalate. |
| Contrôles | Pre-tool, Pre-write, Pre-release, Pre-dry-run, Incident-detected. |
| Anti-pattern | Revue seulement après exécution. |

## GOV-02 : Dry-run avant action risquée

| Élément | Description |
| --- | --- |
| Intention | Simuler avant d'agir sur un système externe, coûteux ou irréversible. |
| Problème | Un agent peut produire un changement correct localement mais dangereux en contexte réel. |
| Solution | Décrire impact, permissions, coût, rollback, validation et critères de go/no-go. |
| Contrôles | Pre-dry-run, validation humaine, rollback, evidence pack. |
| Anti-pattern | Déploiement, suppression ou appel externe sans simulation. |

## GOV-03 : Hook lifecycle progressif

| Élément | Description |
| --- | --- |
| Intention | Déployer les garde-fous sans casser le flux de travail. |
| Problème | Un hook nouveau peut bloquer trop large ou manquer des cas critiques. |
| Solution | Promouvoir les hooks par modes `shadow`, `canary`, puis `enforced`. |
| Contrôles | Registre des hooks, digest de validation, faux positifs, procédure de retrait. |
| Anti-pattern | Activer un blocage global sans période d'observation. |

## MOD-01 : Model router

| Élément | Description |
| --- | --- |
| Intention | Utiliser le bon modèle pour la bonne tâche. |
| Problème | Le modèle par défaut peut être trop faible, trop cher ou non autorisé. |
| Solution | Router selon tâche, rôle, risque, confidentialité, coût, modalité et evals. |
| Contrôles | Pre-model-route, fallback, evals, logs coût/latence, statut modèle. |
| Anti-pattern | Choix implicite du modèle pour toutes les tâches. |

## GOV-04 : Autonomie gouvernée

| Élément | Description |
| --- | --- |
| Intention | Adapter le niveau d'autonomie de l'agent au risque, aux preuves et aux autorités de validation. |
| Problème | Une autonomie uniforme donne trop de pouvoir aux tâches risquées ou bloque inutilement les tâches simples. |
| Solution | Définir des niveaux d'autonomie par tâche : proposer, préparer, exécuter sous contrôle, exécuter automatiquement, ou bloquer. |
| Contrôles | Policy engine, validation authority, evidence pack, dry-run, incident stop. |
| Anti-pattern | Autonomie maximale par défaut. |

### Niveaux d'autonomie

| Niveau | Comportement | Conditions |
| --- | --- | --- |
| A0 bloqué | L'agent ne peut pas agir. | politique interdite, secret, risque critique non couvert. |
| A1 conseiller | L'agent propose seulement. | besoin flou, décision métier ou sécurité. |
| A2 préparer | L'agent prépare artefacts sans effet externe. | dry-run ou brouillon requis. |
| A3 exécuter avec validation | L'agent agit après accord ou gate. | risque moyen, preuve disponible. |
| A4 exécuter automatiquement | L'agent agit sans validation préalable. | tâche réversible, faible risque, contrôles actifs. |
| A5 auto-améliorer | L'agent peut proposer évolution de règles ou capacités. | gouvernance mature, promotion séparée. |

## MOD-02 : Model retirement guard

| Élément | Description |
| --- | --- |
| Intention | Retirer ou restreindre un modèle sans casser l'orchestration. |
| Problème | Un modèle obsolète peut rester utilisé par habitude ou fallback implicite. |
| Solution | Maintenir statuts active, restricted, deprecated, disallowed et local_only avec fallback explicite. |
| Contrôles | Politique de routage, pre-model-route, eval de remplacement, journal d'appel. |
| Anti-pattern | Laisser un modèle interdit accessible parce qu'il fonctionne encore. |

## GOV-05 : Agent privilege boundary

| Élément | Description |
| --- | --- |
| Intention | Empêcher qu'un agent hérite des permissions d'infrastructure du controller. |
| Problème | Un agent lancé avec les mêmes variables d'environnement que l'orchestrateur peut écrire des clés réservées, modifier l'état de convergence ou escalader ses droits. |
| Solution | Séparer les clés controller et agent, protéger les champs d'infrastructure et scrubber les tokens avant spawn de toute session agent. |
| Contrôles | Pre-spawn env scrub, liste de clés protégées, audit des écritures `convergence.*`/`var.*`, rotation de token controller. |
| Anti-pattern | Donner au worker le même token que le scheduler parce qu'ils tournent sur la même machine. |

## GOV-06 : Merge lane fault classifier

| Élément | Description |
| --- | --- |
| Intention | Relancer seulement les échecs réellement transitoires et escalader les échecs durables. |
| Problème | Les workflows de review/merge peuvent rester bloqués par des retries infinis ou échouer trop tôt sur un timeout provider. |
| Solution | Classifier chaque échec en transient ou hard avant retry : rate limit, timeout et indisponibilité provider sont retryables ; violation durable, conflit logique ou verdict critique escaladent. |
| Contrôles | Budget de retry, raison normalisée, journal de classification, escalade si seuil dépassé. |
| Anti-pattern | Retry automatique sans type d'erreur ni limite. |

## GOV-07 : Tool blast-radius limiter

| Élément | Description |
| --- | --- |
| Intention | Limiter l'impact maximal d'un appel outil avant exécution. |
| Problème | Un outil autorisé peut quand même toucher trop de fichiers, domaines, environnements, coûts ou données sensibles. |
| Solution | Déclarer pour chaque tool call un périmètre fichiers/réseau/shell/browser/MCP/coût/environnement, puis appliquer allow, dry-run, escalate ou block. |
| Contrôles | Pre-tool policy, allowlist, dry-run, budget, workspace isolation, evidence pack. |
| Anti-pattern | Autoriser un outil globalement parce que son usage précédent était sûr. |

## GOV-08 : Guardrail contract

| Élément | Description |
| --- | --- |
| Intention | Rendre les garde-fous explicites, testables et versionnés. |
| Problème | Les règles de sécurité, qualité ou conformité restent souvent implicites dans prompts, hooks ou habitudes. |
| Solution | Décrire chaque guardrail par type, scope, mode, point de déclenchement, décisions possibles, preuves et métriques. |
| Contrôles | Guardrail contract, hook lifecycle, faux positifs, incident si bypass ou dérive. |
| Anti-pattern | Ajouter une règle bloquante sans owner, mode shadow/canary ni mesure d'impact. |

## GOV-09 : MCP Trust Gate

| Élément | Description |
| --- | --- |
| Intention | Autoriser les serveurs MCP comme capacités externes seulement après qualification. |
| Problème | Un MCP peut exposer réseau, fichiers, secrets ou actions métier sans frontière claire. |
| Solution | Enregistrer serveur, outils, variables, scopes, données accessibles, owner et mode de confiance avant usage. |
| Contrôles | Registre MCP, secret minimization, allowlist tool, sandbox, telemetry, blast-radius. |
| Anti-pattern | Brancher un MCP parce qu'il fonctionne localement sans examiner ses permissions. |

## GOV-10 : Policy by environment

| Élément | Description |
| --- | --- |
| Intention | Adapter l'autonomie et les outils au niveau de risque de l'environnement. |
| Problème | Les règles local, staging, prod et client peuvent être confondues ou appliquées uniformément. |
| Solution | Déclarer des profils d'environnement avec actions permises, dry-run requis, validation authority et secrets accessibles. |
| Contrôles | Environment policy, runtime provider, blast-radius, audit prod, emergency stop. |
| Anti-pattern | Tester une action en staging puis l'exécuter en production avec le même niveau d'autonomie. |

## GOV-11 : Cluster action dry-run

| Élément | Description |
| --- | --- |
| Intention | Simuler toute action cluster ou infra avant effet réel. |
| Problème | Une commande Kubernetes ou cloud peut dégrader plusieurs workloads même si elle est syntaxiquement correcte. |
| Solution | Produire plan d'impact, ressources touchées, RBAC utilisé, diff attendu, rollback et preuve de policy avant apply. |
| Contrôles | Server-side dry-run, diff, admission policy, quota, service account minimal, rollback plan. |
| Anti-pattern | Laisser un agent appliquer directement sur cluster parce que la CI est verte. |

## GOV-12 : Prompt Injection Firewall

| Élément | Description |
| --- | --- |
| Intention | Empêcher qu'un contenu externe devienne une instruction de contrôle. |
| Problème | Pages web, tickets, logs, docs ou sorties outil peuvent contenir des instructions adverses ou hors périmètre. |
| Solution | Séparer instructions de contrôle et contenu lu, marquer les sources non fiables, refuser toute instruction provenant d'un corpus externe. |
| Contrôles | Source trust label, pre-context-load, pre-tool, redaction, incident si tentative critique. |
| Anti-pattern | Coller du contenu web ou ticket dans le prompt comme s'il était une instruction système. |

## GOV-13 : Remote Hygiene Guard

| Élément | Description |
| --- | --- |
| Intention | Vérifier la fraîcheur et la sûreté d'une source distante avant audit ou indexation. |
| Problème | Une analyse peut s'appuyer sur une branche obsolète, un remote inaccessible, des tags massifs ou un worktree sale. |
| Solution | Contrôler remote, branche, ref, tags, dirty state, pull/fetch safe et statut de fraîcheur avant de conclure. |
| Contrôles | Remote audit, dirty-skip-pull, source freshness, quarantine si remote incohérent. |
| Anti-pattern | Auditer ou indexer un dépôt sans savoir si la ref locale représente encore la source active. |

## GOV-14 : Decision Council Gate

| Élément | Description |
| --- | --- |
| Intention | Escalader les décisions critiques vers un quorum contrôlé. |
| Problème | Une seule réponse modèle peut être insuffisante pour architecture, sécurité, production ou arbitrage irréversible. |
| Solution | Définir conseil, quorum, veto, budget, modèles/providers autorisés, synthèse des désaccords et verdict final. |
| Contrôles | Council record, validation authority, cost cap, dissent log, evidence pack. |
| Anti-pattern | Multiplier les modèles pour toute décision ou accepter un consensus non sourcé. |

## Interfaces liées

| Interface | Rôle |
| --- | --- |
| Policy manifest | Déclare règles, permissions, seuils et escalades. |
| Registre des hooks | Trace mode, propriétaire, statut, portée et preuves de validation. |
| Politique de routage LLM | Définit modèle principal, fallback et restrictions par tâche. |
| Controller-agent privilege contract | Définit clés protégées, tokens autorisés et scrub d'environnement avant spawn. |
| Failure classification contract | Normalise transient/hard, raison, budget de retry et escalade. |
| Tool policy | Déclare surface, budget, environnement, données et limites d'impact. |
| Guardrail contract | Versionne règles, modes, décisions et preuves. |
| MCP trust record | Déclare serveur, outils, scopes, secrets et confiance. |
| Environment policy | Sépare local, staging, prod, client et sandbox. |
| Remote audit record | Trace remote, branche, ref, dirty state et fraîcheur. |
| Council record | Trace participants, quorum, veto, coût, désaccords et verdict. |
