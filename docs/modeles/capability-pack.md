# Modèle de capability pack

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Pack ID | CAP-... |
| Nom | A renseigner |
| Owner | A renseigner |
| Version | A renseigner |
| Statut | draft / experimental / canary / enforced / deprecated / retired |

## Déclaration

| Élément | Valeur |
| --- | --- |
| Rôles fournis | A renseigner |
| Prompts / instructions | A renseigner |
| Skills incluses | A renseigner |
| Outils requis | A renseigner |
| Runtime compatible | local / workflow / k8s / IDE |
| Permissions | fichiers / réseau / modèle / MCP / shell |
| Données autorisées | public / interne / confidentiel / local_only |

## Tests de compétence

| Test | Critère de réussite | Preuve |
| --- | --- | --- |
| A renseigner | A renseigner | trace / verdict / capture |

## Lifecycle

| Transition | Condition |
| --- | --- |
| draft -> experimental | owner, usage cible et risques déclarés. |
| experimental -> canary | test de compétence passé. |
| canary -> enforced | preuve d'usage et faux positifs acceptables. |
| enforced -> deprecated | remplaçant ou risque identifié. |
| deprecated -> retired | migration faite et accès bloqué. |

