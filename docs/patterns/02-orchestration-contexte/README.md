# Patterns d'orchestration et de contexte

Ces patterns structurent le passage d'une intention client vers des lots exécutables par des agents spécialisés, sans perte de contrôle ni saturation de contexte.

La source Mermaid de cette famille est disponible dans [../../../diagrammes/patterns-orchestration-contexte.mmd](../../../diagrammes/patterns-orchestration-contexte.mmd).

## ORC-01 : Orchestrateur et subagents spécialisés

| Élément | Description |
| --- | --- |
| Intention | Déléguer sans perdre le contrôle. |
| Problème | Un agent généraliste sature en contexte et oublie les contraintes. |
| Solution | L'orchestrateur découpe le travail et transmet des task envelopes à des subagents spécialisés. |
| Contrôles | WIP limité, outils par rôle, handoff packet, revue croisée. |
| Anti-pattern | Subagents autonomes qui explorent librement sans contrat de sortie. |

## ORC-02 : Task envelope

| Élément | Description |
| --- | --- |
| Intention | Donner à un agent exactement ce qu'il doit faire. |
| Problème | Les prompts longs et flous produisent dérive, coûts et faux Done. |
| Solution | Encapsuler mission, rôle, contexte minimal, outils, contraintes, critères et format de sortie. |
| Contrôles | Pre-delegation, budget de contexte, policy engine, modèle autorisé. |
| Anti-pattern | Coller tout l'historique de conversation à chaque agent. |

## ORC-03 : Handoff packet

| Élément | Description |
| --- | --- |
| Intention | Passer le relais sans recharger toute la mission. |
| Problème | Les étapes suivantes perdent les décisions ou héritent de bruit inutile. |
| Solution | Résumer résultat, preuves, hypothèses, risques, changements et prochain déclencheur. |
| Contrôles | Post-subagent, claim ledger, journal de preuves, transition d'étape. |
| Anti-pattern | Rapport narratif long sans action suivante ni preuve. |

## ORC-04 : Context router

| Élément | Description |
| --- | --- |
| Intention | Fournir un contexte utile, frais et proportionné. |
| Problème | Trop peu de contexte crée hallucination ; trop de contexte crée confusion. |
| Solution | Sélectionner sources par rôle, étape, risque, budget, fraîcheur et statut de connaissance. |
| Contrôles | Pre-context-load, Post-context-load, Pre-context-reuse, source registry. |
| Anti-pattern | RAG large sans filtres ni métadonnées. |

## ORC-05 : Orchestrateur de contexte avancé

| Élément | Description |
| --- | --- |
| Intention | Piloter le contexte comme un plan de contrôle au-dessus des mémoires, modèles, outils et transitions. |
| Problème | Des couches mémoire séparées restent utiles mais insuffisantes : elles rappellent, stockent ou relient, sans décider quoi exposer, à qui, quand, ni avec quel niveau de preuve. |
| Solution | Ajouter un orchestrateur de contexte qui classe la tâche, choisit un profil, arbitre les sources, calcule un budget, critique les contradictions, produit un context pack, puis décide persistance, invalidation ou escalade. |
| Contrôles | Context scorecard, provenance obligatoire, budget tokens/coût, policy engine, memory gate, pre-stage-transition, ledger des décisions de contexte. |
| Anti-pattern | Laisser chaque subagent récupérer son propre contexte sans coordination globale. |

L'orchestrateur de contexte avancé ne remplace pas Redis, la vector DB, le graphe ou le sidecar. Il les gouverne comme des fournisseurs de signaux. Sa sortie n'est pas une mémoire supplémentaire, mais un paquet de contexte vérifié et limité.

### Décisions prises par l'orchestrateur de contexte

| Décision | Critères |
| --- | --- |
| Profil de contexte | étape, rôle, complexité, risque, livrable attendu. |
| Niveau de mémoire | fenêtre active, contexte chaud, vectoriel, graphe, sidecar, source de vérité. |
| Budget | tiny, small, medium, deep, avec justification si augmentation. |
| Source prioritaire | vérité active avant mémoire ; mémoire comme rappel ou indice. |
| Compression | résumé sourcé, extraction ciblée, découpage ou refus si perte critique. |
| Délégation | subagent autorisé, outils permis, format de restitution. |
| Persistance | Redis, mémoire durable, archive, désindexation ou purge. |
| Escalade | question client, validation humaine, critique indépendante ou blocage. |

### Context pack minimal

Un context pack est le livrable interne envoyé à un subagent ou à une étape.

```yaml
context_pack:
  mission_id: "MIS-001"
  stage: "architecture"
  role: "architecte"
  context_profile: "architecture"
  budget: "deep"
  objective: "Comparer deux options d'orchestration de contexte"
  sources:
    - id: "SRC-adr-12"
      status: "active"
      reason: "decision architecture actuelle"
      confidence: "high"
    - id: "SRC-incident-04"
      status: "active"
      reason: "risque deja observe"
      confidence: "medium"
  excluded_sources:
    - id: "SRC-old-report"
      reason: "superseded"
  constraints:
    - "ne pas utiliser de source sensitive non minimisee"
    - "citer les preuves pour toute decision durable"
  expected_handoff:
    - summary
    - options
    - risks
    - evidence
    - memory_updates
    - next_trigger
```

## Interfaces liées

| Interface | Rôle |
| --- | --- |
| Task envelope | Contrat d'exécution envoyé au subagent. |
| Context pack | Sous-ensemble contrôlé du contexte utile pour la tâche. |
| Handoff packet | Retour structuré permettant transition, preuve et mémoire. |
| Source registry | Statut et validité des sources récupérables. |
| Memory gate | Contrôle lecture, écriture, indexation et invalidation mémoire. |
| Workflow state manifest | États, transitions, guards, interruptions et preuves. |
| Flow DSL minimal | Description compacte de flows exportables. |

## ORC-06 : Context constitution

| Élément | Description |
| --- | --- |
| Intention | Définir l'ordre d'autorité des informations utilisées par l'agent. |
| Problème | L'agent peut traiter une mémoire, une similarité ou une hypothèse comme équivalente à une source de vérité. |
| Solution | Établir une constitution du contexte : source active > preuve vérifiée > décision validée > mémoire durable > handoff récent > hypothèse > similarité vectorielle. |
| Contrôles | Source registry, claim ledger, memory gate, vérification de provenance, marquage des hypothèses. |
| Anti-pattern | RAG aveugle ou mémoire autoritaire. |

### Ordre d'autorité

| Rang | Type d'information | Usage |
| --- | --- | --- |
| 1 | Source de vérité active | Décision critique ou durable. |
| 2 | Preuve vérifiée | Fermeture, validation, audit. |
| 3 | Décision validée | Arbitrage métier, architecture, sécurité ou ops. |
| 4 | Mémoire durable sourcée | Rappel réutilisable, jamais seule pour décision critique. |
| 5 | Handoff récent | Passage de relais limité à la mission. |
| 6 | Hypothèse déclarée | Travail exploratoire, pas fermeture. |
| 7 | Similarité vectorielle | Candidat à vérifier. |

## ORC-07 : Context conflict resolver

| Élément | Description |
| --- | --- |
| Intention | Résoudre ou exposer les contradictions de contexte avant action. |
| Problème | Code, documentation, tickets, mémoire, ADR et demande client peuvent se contredire. |
| Solution | Détecter les conflits, classer leur gravité, appliquer l'ordre d'autorité, puis décider : source gagnante, hypothèse, question client, tâche d'analyse ou blocage. |
| Contrôles | Context scorecard, claim ledger, validation authority, incident si mémoire contaminée. |
| Anti-pattern | Choisir la source la plus récente ou la plus similaire sans justification. |

### Décisions de conflit

| Conflit | Décision attendue |
| --- | --- |
| Documentation contre code | Vérifier tests, CI et comportement réel ; escalader si règle métier. |
| Mémoire contre source active | Invalider ou rétrograder la mémoire. |
| ADR contre implémentation | Créer analyse architecture ou incident de drift. |
| Client contre charte validée | Demander arbitrage ou exception explicite. |
| Deux sources actives incompatibles | Bloquer décision durable jusqu'à clarification. |

## ORC-08 : Context budget escalation

| Élément | Description |
| --- | --- |
| Intention | Augmenter le contexte seulement quand une preuve montre que le budget courant est insuffisant. |
| Problème | Le contexte grossit par confort, ou reste trop petit par économie, ce qui crée hallucinations et coûts inutiles. |
| Solution | Définir des déclencheurs d'escalade de tiny vers small, medium ou deep, avec justification, durée et retour au budget inférieur après synthèse. |
| Contrôles | Logs tokens/coût, context scorecard, pre-context-load, validation si dépassement de seuil. |
| Anti-pattern | Prompt-cargo : ajouter toujours plus de contexte sans diagnostic. |

### Escalade de budget

| Passage | Déclencheur valide | Sortie attendue |
| --- | --- | --- |
| tiny -> small | Objectif ou état insuffisant pour agir. | bref contexte ciblé. |
| small -> medium | Plusieurs sources ou contraintes doivent être comparées. | synthèse sourcée. |
| medium -> deep | Décision architecture, incident, sécurité ou arbitrage durable. | options, preuves, risques. |
| deep -> medium/small | Analyse terminée. | handoff compressé et sources clés. |

## ORC-09 : Workflow State Engine

| Élément | Description |
| --- | --- |
| Intention | Rendre les workflows agentiques explicites, reprenables et auditables. |
| Problème | Les agents enchaînent souvent étapes, interruptions et reprises dans une logique cachée au prompt ou au runtime. |
| Solution | Déclarer un manifeste d'états, transitions, guards, retries, interruptions, compensations et preuves minimales. |
| Contrôles | Workflow state manifest, mission ledger append-only, evidence-driven transition, telemetry events. |
| Anti-pattern | Décrire un process dans un prompt sans état machine ni preuve de transition. |

### États minimaux recommandés

| État | Rôle |
| --- | --- |
| intake | qualifier intention, contraintes et ambiguïtés critiques. |
| discovery | charger sources, connaissances et risques. |
| decision | choisir option, modèle, capacité ou escalade. |
| execution | produire action, artefact ou changement. |
| verification | relier preuves aux critères. |
| capitalization | décider rétention, mémoire, archive ou purge. |

## ORC-10 : Flow DSL minimal

| Élément | Description |
| --- | --- |
| Intention | Décrire des flows réutilisables sans créer un langage complexe prématuré. |
| Problème | Les workflows restent dispersés entre prompts, scripts et documentation, ou deviennent un DSL trop riche et fragile. |
| Solution | Définir un DSL minimal : états, transitions, guards, preuves et export Mermaid/manifest. |
| Contrôles | Flow DSL minimal, workflow state manifest, validation syntaxique, dry-run de flow. |
| Anti-pattern | Encoder la logique métier dangereuse directement dans le DSL au lieu de la garder dans les policies/outils. |
