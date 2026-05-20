# Lifecycle et maturité des patterns

Cette page définit comment un pattern entre dans le référentiel, devient stable, puis peut être rendu normatif ou déprécié.

## Statuts de lifecycle

| Statut | Sens | Usage autorisé |
| --- | --- | --- |
| proposed | Idée utile mais non éprouvée. | discussion, expérimentation limitée. |
| experimental | Utilisé sur quelques missions avec suivi explicite. | usage encadré, preuve obligatoire. |
| stable | Pattern éprouvé et documenté. | usage recommandé. |
| normative | Pattern requis pour un niveau de conformité donné. | usage attendu, exception justifiée. |
| deprecated | Remplacé ou jugé insuffisant. | migration planifiée, pas de nouvel usage. |
| retired | Retiré du référentiel actif. | historique seulement. |

## Niveaux de maturité par pattern

| Niveau | Nom | Critère |
| --- | --- | --- |
| M0 | Absent | Le besoin couvert par le pattern n'est pas traité. |
| M1 | Minimal | Le pattern existe sous forme manuelle ou documentaire. |
| M2 | Contrôlé | Les entrées, sorties et responsables sont identifiés. |
| M3 | Gouverné | Des hooks, politiques ou validations empêchent les dérives. |
| M4 | Mesuré | Le pattern produit métriques, traces ou preuves exploitables. |
| M5 | Amélioré | Les incidents et evals modifient le pattern ou ses contrôles. |

## Grille d'évaluation

| Question | Maturité visée |
| --- | --- |
| Le pattern a-t-il une intention et un anti-pattern documentés ? | M1 |
| Les interfaces produites et consommées sont-elles définies ? | M2 |
| Les conditions de blocage ou d'escalade sont-elles explicites ? | M3 |
| Les preuves de bon fonctionnement sont-elles collectées ? | M4 |
| Les incidents entraînent-ils correction et prévention ? | M5 |

## Promotion d'un pattern

Un pattern peut passer à un statut supérieur seulement si :

1. son problème est récurrent ;
2. sa solution est formulée indépendamment d'un outil spécifique ;
3. ses interfaces sont vérifiables ;
4. ses contrôles sont proportionnés au risque ;
5. son anti-pattern est identifié ;
6. une preuve d'usage ou d'incident justifie sa présence.

## Dépréciation

Un pattern doit être déprécié si :

| Déclencheur | Action |
| --- | --- |
| Il est remplacé par un pattern plus précis. | marquer deprecated et pointer vers remplaçant. |
| Il encourage un comportement risqué. | ouvrir incident ou correction normative. |
| Il dépend d'un outil retiré. | séparer principe et implémentation, ou retirer. |
| Il n'est jamais utilisé. | archiver ou fusionner. |

## Métadonnées recommandées

| Champ | Usage |
| --- | --- |
| pattern_id | Identifiant stable. |
| family | Famille principale. |
| status | proposed, experimental, stable, normative, deprecated, retired. |
| maturity | M0 à M5. |
| owner | Rôle responsable. |
| related_requirements | Exigences AG-* couvertes. |
| evidence_refs | Preuves d'usage ou de validation. |
| superseded_by | Pattern de remplacement si applicable. |
| review_trigger | Incident, release, changement de modèle, changement de politique. |

## Règle finale

Un catalogue de patterns mature doit savoir promouvoir et retirer ses propres patterns. Sinon, il devient une mémoire normative obsolète.
