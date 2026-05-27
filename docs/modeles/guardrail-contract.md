# Modèle de guardrail contract

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Guardrail ID | GRD-... |
| Nom | A renseigner |
| Type | input / output / tool / model / memory / runtime |
| Owner | A renseigner |
| Mode | shadow / canary / enforced / retired |

## Déclenchement

| Champ | Valeur |
| --- | --- |
| Moment | pre-model / post-model / pre-tool / post-tool / pre-memory / pre-release |
| Scope | mission / projet / organisation |
| Entrées | A renseigner |
| Données sensibles | oui / non / possible |

## Décisions

| Décision | Effet |
| --- | --- |
| allow | Continuer. |
| block | Stopper et produire preuve. |
| escalate | Demander validation authority. |
| modify | Masquer, réduire ou rediriger. |
| observe | Tracer sans bloquer. |

## Preuves et télémétrie

| Élément | Valeur |
| --- | --- |
| Evidence | control record, event, log, verdict |
| Metrics | blocks, false positives, bypass attempts |
| Incident requis | oui / non / selon sévérité |

