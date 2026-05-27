# Profils de preuves par type de tâche

Cette page indique quelles preuves sont attendues selon le type de travail agentique. Elle évite d'exiger les mêmes preuves pour une recherche documentaire, une action infra, une UI ou une modification de code.

## Matrice des profils

| Type de tâche | Preuves minimales | Preuves renforcées si risque élevé |
| --- | --- | --- |
| Recherche / analyse | sources consultées, claim ledger, hypothèses explicites. | contradiction report, source graph query, validation humaine. |
| Documentation | diff documentaire, sources, liens internes, absence de drift. | audit de cohérence, rendu diagramme, revue owner. |
| Code | diff ciblé, tests ou justification, lint/build si existants. | tests de non-régression, scan secret/sécurité, review indépendante. |
| UI / design | screenshot, DOM snapshot, critères visuels. | visual evidence pack, console/network logs, validation design authority. |
| Infra / cluster | dry-run, impact report, rollback plan. | server-side dry-run, RBAC utilisé, policy decision, go/no-go humain. |
| Données / connaissance | knowledge source index, ACL, fraîcheur, provenance. | source active vérifiée, réindexation, désindexation ou quarantine. |
| Modèle / prompt | provider/model, prompt version, eval dataset. | canary, rollback, coût, régression par version. |
| Runtime / agent | runtime provider contract, logs, health, cleanup. | trajectory log, crash/unhealthy rate, workspace isolation evidence. |
| Sécurité | menace, contrôle appliqué, décision allow/block/escalate. | incident record, containment, post-mortem, eval de prévention. |

## Règle d'escalade

Si une tâche touche production, secrets, données personnelles, coût significatif, client externe ou décision durable, le profil de preuve passe au niveau renforcé.

## Sortie attendue

Chaque evidence pack DOIT mentionner :

- le type de tâche ;
- le profil de preuve choisi ;
- les preuves présentes ;
- les preuves absentes et la justification ;
- le verdict de fermeture, réouverture, incident ou escalade.

