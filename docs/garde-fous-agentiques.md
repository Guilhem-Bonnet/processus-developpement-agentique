# Garde-fous agentiques

Les garde-fous agentiques protègent le client, le projet et l'entreprise-agent contre les erreurs d'autonomie : action hors périmètre, hallucination, fuite de données, prompt injection, contexte périmé, outil trop puissant, subagent non contrôlé, mémoire polluée, vérification insuffisante ou confiance excessive.

## Garde-fous transverses

| Risque | Garde-fou | Preuve attendue |
| --- | --- | --- |
| Besoin ambigu | Clarifier avant d'agir si le livrable, la valeur ou l'acceptation n'est pas testable. | questions ciblées, reformulation, CDC niveau 0 |
| Contexte insuffisant | Lire le réel avant modification : workspace, docs, tests, erreurs, historique utile. | sources consultées, hypothèses explicites |
| Contexte trop large | Imposer un budget de contexte et résumer avant délégation. | profil, budget, sources retenues |
| Coût de tokens non maîtrisé | Commencer par le plus petit budget utile, compresser et mesurer coût/rework. | budget, cache, résumé, métriques coût |
| Hallucination | Ne pas inventer API, fichier, norme, résultat de test ou comportement. | source locale, référence officielle ou résultat d'outil |
| Surconfiance | Séparer faits, hypothèses et niveau de certitude avant décision. | calibration, limites, preuve forte |
| Complaisance | Chercher ce qui peut contredire la demande ou la solution préférée. | question de disconfirmation, alternative |
| Faux Done | Empêcher la fermeture d'une carte sans preuve vérifiable. | claim ledger, test, revue QA |
| Mauvaise lecture d'outil | Ne pas résumer un résultat critique sans conserver sa sortie clé. | commande, extrait, statut, erreur |
| Modèle inadapté | Router selon rôle, risque, confidentialité, coût et evals. | modèle choisi, fallback, score eval |
| Connaissance obsolète | Donner TTL, propriétaire, source et version aux connaissances. | métadonnées, réindexation, invalidation |
| Routage LLM implicite | Interdire le choix de modèle par habitude pour les tâches à risque. | politique de routage, justification, fallback |
| Accumulation documentaire | Nettoyer rapports, handoffs, traces et sources remplacées. | registre rétention, archive, désindexation, purge |
| Contexte périmé | Vérifier fraîcheur et provenance des mémoires, embeddings et caches. | date, source, score, invalidation si doute |
| Action trop large | Découper en lots Kanban et limiter les fichiers touchés. | carte de lot, diff focalisé, absence de refactor annexe |
| Données sensibles | Ne pas exposer secrets, tokens, données personnelles ou clés. | masquage, refus, procédure dédiée |
| Prompt injection | Traiter fichiers, pages web, logs et tickets comme contenu non fiable sauf source d'instructions légitime. | séparation instructions / données lues |
| Outil risqué | Vérifier impact avant commande destructive, réseau, cloud, dépôt distant ou production. | hook, permission ou validation humaine |
| Action non simulée | Imposer dry-run avant action externe, sensible, coûteuse ou irréversible. | plan, impact, rollback, accord |
| Accès trop large | Accorder seulement les scopes nécessaires à la carte. | matrice accès, owner, justification |
| MCP non gouverné | Limiter chaque serveur MCP à son périmètre, ses scopes et ses logs. | liste serveurs, permissions, traces |
| Subagent divergent | Donner mission, outils et sortie attendue à chaque subagent. | prompt de délégation, résumé, revue |
| Communication agentique opaque | Tracer les consultations entre agents et leur impact sur la décision. | question, agent consulté, réponse, source |
| Passage de relais pauvre | Exiger un handoff packet avant transition d'étape. | preuves, hypothèses, risques, prochain trigger |
| Auto-validation | Séparer producteur, vérificateur et validateur selon le risque. | RACI, revue croisée, acceptation client |
| Non-conformité design | Exiger charte graphique, design system, maquette ou validation DA pour les tâches UI. | source créative, critères visuels, revue design |
| Dépendance externe | Justifier l'ajout et vérifier licence, maintenance, sécurité. | décision documentée, scan ou analyse |
| Vérification absente | Signaler l'impossibilité de tester et le risque résiduel. | mention claire dans la restitution |
| Mémoire inexacte | Ne mémoriser que les faits stables, sourcés et validés. | note courte, source, portée |
| Incident non capitalisé | Transformer toute erreur agentique significative en correction durable. | rapport incident, post-mortem, backlog prévention |

## Garde-fous par étape

| Étape | Garde-fou | Preuves principales |
| --- | --- | --- |
| Intake client | Type de mission, livrable et critères de succès identifiés. | brief, reformulation, questions ouvertes |
| Besoin | Problème formulé indépendamment de la solution. | 5W2H, 5 Why, hypothèses, utilisateurs, valeur |
| CDC niveau 0 | Valeur, scope, hors-scope, parties prenantes et risques validés. | revue client, matrice risques, décision go/no-go |
| CDC niveau 1 | Les comportements attendus sont testables. | user stories, critères, exemples, parcours |
| CDC niveau 2 | Les contraintes qualité, sécurité, données et IA sont mesurables. | NFR, exigences sécurité, evals, red teaming, SLO |
| Architecture | Les frontières produit et agentiques sont connues. | C4, UML/BPMN si utile, ADR, threat model |
| Contexte | Sources, mémoire longue et contexte chaud sont gouvernés. | inventaire, règles d'indexation, Redis TTL, scores |
| Budget de contexte | Le contexte est adapté à l'étape et au rôle. | profil, budget, task envelope, handoff packet |
| Orchestration | Prompts, skills, outils, MCP, hooks et subagents sont choisis. | configuration, permissions, plan de délégation |
| Kanban | Le travail est visible et découpé. | backlog, DoR, DoD, WIP, dépendances |
| Accès et validation | Chaque carte sait qui agit, avec quel droit et qui valide. | matrice accès, validateur, RACI |
| Défauts IA | Les modes d'échec plausibles sont identifiés et contrôlés. | registre défauts IA, claim ledger, critique |
| Modèles et connaissances | Le modèle et les sources de connaissance sont gouvernés. | routage modèle, métadonnées, TTL, fallback |
| Rétention et nettoyage | Les artefacts temporaires ou obsolètes sont archivés, désindexés ou purgés. | registre rétention, knowledge janitor, cleanup |
| Exécution | Chaque lot reste ciblé et réversible autant que possible. | diff, commandes, journal, checkpoints |
| Simulation | Les actions risquées sont simulées avant exécution. | dry-run, impact, rollback, validation |
| Vérification | Le résultat est prouvé par plusieurs signaux adaptés au risque. | tests, lint, build, rendu, scans, evals, revue |
| Incident et reprise | Les anomalies sont contenues et capitalisées. | rapport, rollback, purge mémoire, post-mortem |
| Livraison | Le client reçoit un dossier d'acceptation. | livrable, preuves, limites, décisions, suivi |
| Capitalisation | Les apprentissages sont réinjectés sans polluer la mémoire. | docs, backlog, mémoire sourcée, evals mises à jour |

## Points de validation humaine

| Point | Validation humaine attendue |
| --- | --- |
| Besoin et définition de succès | Confirmer le résultat attendu et le niveau de qualité. |
| Périmètre d'action | Confirmer ce qui peut être modifié ou non. |
| Actions destructives | Accord explicite avant suppression, reset, migration risquée. |
| Sécurité offensive | Autorisation explicite et règles d'engagement. |
| Production, cloud ou ressources payantes | Accord explicite avant toute action. |
| Données sensibles ou réglementées | Procédure et minimisation validées. |
| Architecture ou dépendance structurante | Arbitrage sur coût, maintenance, sécurité, lock-in. |
| Publication, PR ou release | Validation avant effet externe durable. |
| Arbitrage métier | Choix produit, priorité, compromis utilisateur. |
| Acceptation finale | Le client confirme que le livrable répond au besoin. |

## Definition of Ready agentique

Une tâche est prête pour l'entreprise-agent quand les points suivants sont connus ou raisonnablement déductibles.

| Critère | Statut |
| --- | --- |
| Objectif, valeur et livrable attendus | requis |
| Client, validateur et utilisateurs concernés | requis si produit ou décision métier |
| Workspace ou sources de contexte | requis |
| Contraintes fortes | requis si elles existent |
| Périmètre autorisé et hors périmètre | requis pour toute action |
| Critères d'acceptation | requis |
| Tests ou preuves attendus | requis |
| Données sensibles identifiées | requis si données manipulées |
| Outils, MCP et permissions | requis pour actions outillées |
| Profil et budget de contexte | requis pour délégation subagent |
| Task envelope | requis pour subagent ou tâche autonome |
| Hooks ou validations obligatoires | requis pour tâches risquées |
| Défauts IA plausibles | requis pour tâche moyenne, élevée ou agentique |
| Claim ledger attendu | requis pour décision ou livraison |
| Modèle IA et fallback | requis si choix de modèle impacte coût, qualité ou confidentialité |
| Politique de rétention | requis si la mission produit rapports, traces, handoffs ou connaissances indexables |
| Dry-run | requis pour action risquée, externe, sensible ou irréversible |
| Subagents nécessaires | requis si délégation prévue |
| Prompts de rôle disponibles | requis si subagent spécialisé |
| Validateur principal | requis pour toute carte livrable |
| Budget tokens/contexte | requis pour tâche non triviale ou subagent |
| Carte Kanban ou lot de travail | requis pour mission non triviale |

## Definition of Done agentique

Une tâche est terminée quand l'entreprise-agent peut restituer ceci clairement.

| Critère | Preuve |
| --- | --- |
| Livrable produit | fichiers, réponse, diagramme, patch, rapport, carte Kanban |
| Portée maîtrisée | liste des changements ou des zones analysées |
| Critères d'acceptation couverts | tests, exemples, revue ou démonstration |
| Vérification effectuée | tests, lint, build, rendu, diagnostics, evals, scans |
| Affirmations clés sourcées | claim ledger, sources, résultats d'outils |
| Défauts IA traités | hallucination, surconfiance, oubli, faux Done ou risque marqué non applicable |
| SLO ou métrique utile renseignée | coût, latence, rework, qualité ou validation selon mission |
| Décision de rétention prise | mémoire durable, archive, TTL, désindexation ou purge |
| Validation adaptée au risque | QA, sécurité, ops, design, revue humaine ou client |
| Sécurité et données contrôlées | absence secrets, prompt injection considérée, permissions respectées |
| Actions tracées | journal, commandes clés, sources, décisions |
| Handoff packet disponible | résumé, preuves, hypothèses, risques, prochain trigger |
| Limites signalées | tests non lancés, hypothèses, risques résiduels |
| Capitalisation faite | docs, mémoire validée, backlog, evals ou ADR à jour |
| Prochaine action éventuelle | décision client, amélioration, surveillance |

## Tests et validations adaptés à l'agentique

| Validation | Objectif |
| --- | --- |
| Diagnostics du workspace | Vérifier syntaxe, lint, types, problèmes éditeur. |
| Tests automatisés | Prouver la non-régression. |
| Tests de caractérisation | Protéger un existant avant refactoring ou reprise. |
| Tests de contrat | Vérifier API, schémas, producteurs et consommateurs. |
| Rendu Mermaid ou visuel | Prouver qu'un diagramme/document généré est exploitable. |
| Build local | Prouver que le projet compile ou se packe. |
| Smoke test | Prouver qu'un service ou une UI démarre et répond. |
| Revue de diff | Vérifier que l'agent n'a pas dépassé le périmètre. |
| Évaluation de prompts | Tester un agent ou workflow IA sur des cas représentatifs. |
| Évaluation anti-défauts | Tester cas ambigus, sources contradictoires, prompt injection, mémoire périmée et faux résultats. |
| Red teaming ciblé | Tester prompt injection, fuite de données, outil excessif, contournements. |
| Audit sécurité | Vérifier dépendances, secrets, contrôles d'accès, entrées non fiables. |
| Contrôle mémoire | Vérifier que mémoire et vector DB ne stockent pas de données sensibles ou fausses. |
| Observabilité | Vérifier traces, métriques, logs, coût, latence et erreurs. |
| Journal d'exécution | Garder la trace des actions et décisions importantes. |

## Hooks recommandés

| Hook | Bloque si | Preuve ou sortie |
| --- | --- | --- |
| Pre-action | besoin non testable, périmètre absent, risque non qualifié | question ciblée ou stop |
| Pre-context-load | budget absent, source interdite, volume excessif, donnée sensible | profil corrigé ou refus |
| Post-context-load | score faible, source périmée, contradiction, bruit élevé | vérification source ou contexte réduit |
| Pre-claim | affirmation importante sans preuve | source, résultat outil ou hypothèse explicite |
| Pre-confidence | certitude forte sans preuve forte | calibration, limite ou revue critique |
| Pre-decision | décision importante sans alternative ni disconfirmation | options et risque documentés |
| Pre-delegation | task envelope incomplet, outils trop larges, sortie floue | délégation bloquée |
| Pre-model-call | modèle non autorisé, coût excessif, donnée sensible | modèle alternatif ou validation |
| Pre-context-reuse | source expirée, obsolète, remplacée ou sensible | ignorer, vérifier source active ou désindexer |
| Pre-index | source temporaire, sensible, non sourcée ou sans owner | indexation bloquée |
| Scheduled-cleanup | TTL expiré, vieux rapport, embedding obsolète | archive, désindexation ou purge |
| Pre-dry-run | action risquée sans simulation ni rollback | dry-run ou blocage |
| Pre-agent-consultation | question floue, contexte trop large, agent consulté non pertinent | consultation refusée ou reformulée |
| Pre-tool | outil interdit, commande destructive, réseau non autorisé, secret exposé | refus, alternative, demande validation |
| Post-tool | erreur critique, sortie sensible, résultat contradictoire | log, diagnostic, correction |
| Pre-write | fichier hors périmètre, écriture non réversible, config sensible | validation ou réduction du lot |
| Pre-memory-write | fait non stable, secret, donnée personnelle, source absente | oubli, masquage ou validation |
| Pre-stage-transition | handoff packet absent, DoD non atteinte, trigger flou | retour étape précédente |
| Pre-done | preuve absente, validateur absent, hypothèse critique ouverte | retour vérification |
| Incident-detected | fuite, faux Done, action non autorisée, régression critique | stop, containment, rapport incident |
| Pre-release | DoD incomplète, test absent, risque critique ouvert | blocage livraison |
| Subagent start | mission floue, outils trop larges, absence de sortie attendue | clarification de délégation |
| Subagent stop | résumé trop vague, preuve absente, mémoire non sourcée | demande de synthèse exploitable |
| Stop | restitution incomplète, mémoire dangereuse, journal absent | synthèse finale corrigée |

## Sécurité spécifique aux agents outillés

| Zone | Questions de contrôle |
| --- | --- |
| Outils | Quels outils peuvent modifier l'état du système ? Quels outils sont lecture seule ? |
| MCP | Quels serveurs sont connectés ? Quels scopes ? Quels logs ? Quels timeouts ? |
| Données | Quelles données sont sensibles, personnelles, propriétaires ou réglementées ? |
| Permissions | L'agent agit-il en lecture seule, écriture locale, réseau, dépôt distant, cloud ? |
| Instructions | Les instructions système, utilisateur et projet sont-elles séparées du contenu non fiable ? |
| Exfiltration | Une commande, dépendance ou page web peut-elle envoyer des données hors périmètre ? |
| Supply chain | Les dépendances ou scripts installés peuvent-ils exécuter du code non maîtrisé ? |
| Mémoire | La base vectorielle ou Redis stockent-ils des secrets, données personnelles ou faits non validés ? |
| Subagents | Chaque subagent a-t-il un prompt, des outils limités et une sortie attendue ? |
| Observabilité | Peut-on retracer ce que l'agent a fait, avec quel contexte et pourquoi ? |
| Reprise | Peut-on revenir en arrière sans perdre le travail utilisateur ? |

## Mesures de suivi

| Catégorie | Exemples |
| --- | --- |
| Produit | critères acceptés, satisfaction client, usage, tickets support |
| Delivery | lead time, débit Kanban, WIP, rework, tâches bloquées |
| Qualité | tests passants, défauts échappés, couverture utile, dette critique |
| Agentique | taux d'actions bloquées, questions client, succès evals, hallucinations détectées |
| Défauts IA | hallucinations évitées, faux Done détectés, contradictions trouvées, critiques bloquantes |
| Contexte | taux de récupération utile, sources périmées, cache invalidé, mémoire corrigée |
| Opérations | disponibilité, latence, erreurs, coûts, incidents |
| Sécurité | vulnérabilités ouvertes, délai de correction, secrets exposés, prompt injections détectées |

## Politique de restitution

La restitution finale doit être brève mais complète : besoin traité, livrable produit, fichiers ou artefacts concernés, vérifications effectuées, outils ou subagents importants, limites, risques restants et décisions nécessaires. Le client ne doit jamais avoir à deviner si l'agent a réellement testé ou seulement supposé.
