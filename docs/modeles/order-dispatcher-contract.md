# Modèle de contrat order dispatcher

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Order ID | ORD-... |
| Nom | A renseigner |
| Type | exec / formula |
| Owner | A renseigner |
| Statut | draft / active / deprecated / retired |

## Classification

| Champ | exec | formula |
| --- | --- | --- |
| Session agent | non | oui |
| Usage attendu | commande déterministe, script, inspection | workflow agentique, raisonnement, multi-étapes |
| Budget token | none / faible | A renseigner |
| Blast radius | fichiers, réseau, shell | outils, fichiers, modèle, sous-agents |
| Preuves minimales | sortie commande, exit code | trace workflow, evidence pack, verdict |

## Contrôles

| Contrôle | Règle |
| --- | --- |
| Policy tool | Autoriser seulement outils déclarés. |
| Budget | Bloquer ou escalader si budget dépassé. |
| Dry-run | Requis si impact externe, production ou suppression. |
| Evidence | L'ordre ne peut pas être marqué Done sans preuve liée. |

## Télémétrie

| Event | Quand |
| --- | --- |
| order.dispatched | ordre routé vers exec ou formula. |
| order.blocked | policy, budget ou blast-radius refuse l'ordre. |
| order.completed | ordre terminé avec preuve et verdict. |

