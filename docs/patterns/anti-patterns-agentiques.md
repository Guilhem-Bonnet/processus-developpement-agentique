# Anti-patterns agentiques

Les anti-patterns décrivent les formes dangereuses ou immatures des systèmes agentiques. Ils servent à diagnostiquer les dérives et à choisir les patterns correctifs.

## Catalogue

| Anti-pattern | Symptôme | Risque | Correction |
| --- | --- | --- | --- |
| Agent omniscient | Un seul agent reçoit tout, décide tout et valide tout. | faux Done, dérive de contexte, absence de responsabilité. | ORG-01, ORC-01, ORG-02. |
| RAG aveugle | La similarité vectorielle est traitée comme vérité. | décisions basées sur documents obsolètes ou mauvais projet. | ORC-06, ORC-07, KNO-02. |
| Mémoire autoritaire | Une mémoire ancienne contredit la source active mais reste utilisée. | reproduction d'erreurs et dette documentaire. | KNO-01, KNO-05, ORC-06. |
| Subagent sans contrat | Un subagent explore librement sans sortie imposée. | coût élevé, résultats incomparables, impossibilité d'audit. | ORC-02, ORC-03, GOV-01. |
| Prompt-cargo | Le système compense l'incertitude par un prompt de plus en plus long. | saturation, contradictions, perte de focus. | ORC-05, ORC-08. |
| Faux Done | Une tâche est fermée parce que l'agent affirme qu'elle est terminée. | défaut livré, perte de confiance. | QUA-01, QUA-04, QUA-05. |
| Validation circulaire | L'agent qui produit valide sa propre sortie critique. | acceptation non indépendante. | ORG-02, GOV-04. |
| Hook marteau | Un hook bloque tout sans phase d'observation. | workflow cassé, contournements humains. | GOV-03. |
| Fallback fantôme | Un modèle interdit reste accessible par alias ou fallback implicite. | fuite de données, non-conformité. | MOD-02, GOV-01. |
| Tout indexer | Chaque trace, brouillon ou handoff devient mémoire durable. | corpus ingouvernable, rappel toxique. | KNO-01, KNO-04, RUN-02. |
| Drift documentaire | La documentation affirme une gouvernance que le runtime n'applique plus. | conformité fictive. | KNO-03, RUN-02. |
| Autonomie maximale par défaut | L'agent agit avec le niveau d'autonomie le plus élevé sauf blocage. | actions irréversibles ou non autorisées. | GOV-04, GOV-01, GOV-02. |

## Diagnostic rapide

| Question | Anti-pattern probable |
| --- | --- |
| La sortie cite-t-elle des sources actives ? | RAG aveugle ou mémoire autoritaire. |
| Le Done a-t-il un verdict indépendant ? | Faux Done ou validation circulaire. |
| Le contexte transmis est-il plus gros que le besoin ? | Prompt-cargo. |
| Les agents peuvent-ils créer des artefacts permanents seuls ? | Tout indexer ou dynamic factory incontrôlée. |
| Un incident permet-il d'identifier quelle mémoire purger ? | Mémoire autoritaire ou observabilité insuffisante. |

## Règle finale

Un anti-pattern doit toujours pointer vers un pattern correctif. Sinon il reste une critique générale et ne permet pas d'améliorer le système.
