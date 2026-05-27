# Modèle de flow DSL minimal

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Flow ID | FLOW-... |
| Nom | A renseigner |
| Owner | A renseigner |
| Version | A renseigner |
| Statut | draft / active / deprecated |

## Exemple

```yaml
flow:
  id: FLOW-001
  states:
    - id: intake
      next: discovery
      evidence: brief
    - id: discovery
      next: decision
      guard: context_scorecard.passed
    - id: decision
      next: done
      guard: verification_verdict.accepted
```

## Règles

| Règle | Description |
| --- | --- |
| États explicites | Aucun état implicite. |
| Transitions gardées | Chaque transition a guard ou preuve. |
| Exportable | Le flow doit pouvoir être rendu en Mermaid ou manifest. |
| Pas de logique cachée | Les actions dangereuses restent dans policies/tools, pas dans le DSL. |

