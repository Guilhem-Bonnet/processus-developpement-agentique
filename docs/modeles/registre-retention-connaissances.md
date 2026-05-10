# Modèle de registre de rétention des connaissances

## Inventaire

| ID | Artefact | Type | Statut | Owner | Sensibilité | Indexable | Rétention | Expiration | Remplacé par |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| K-001 | A renseigner | ADR / rapport / handoff / log / charte / API / incident | active / archived / superseded / obsolete / sensitive | A renseigner | public / interne / confidentiel / secret / données personnelles | oui / non | durable / projet / mission / court terme / purge | A renseigner | A renseigner |

## Décision de nettoyage

| ID | Décision | Justification | Action | Validation |
| --- | --- | --- | --- | --- |
| K-001 | conserver / archiver / désindexer / purger / résumer | A renseigner | A renseigner | A renseigner |

## Contrôle d'indexation

| ID | Source active ? | Métadonnées complètes ? | Embedding à jour ? | Risque |
| --- | --- | --- | --- | --- |
| K-001 | oui / non | oui / non | oui / non | aucun / obsolète / sensible / contradictoire |

## Nettoyage périodique

| Date | Périmètre | Éléments revus | Actions | Prochaine revue |
| --- | --- | --- | --- | --- |
| A renseigner | docs / vector DB / Redis / rapports / handoffs | A renseigner | A renseigner | A renseigner |

## Règles rapides

- Une source `active` peut être utilisée pour décision.
- Une source `archived` ne sert qu'à l'historique.
- Une source `superseded` doit pointer vers sa remplaçante.
- Une source `obsolete` doit être désindexée.
- Une source `sensitive` ne doit pas être indexée sans procédure dédiée.
- Un handoff temporaire doit expirer ou être synthétisé en mémoire durable.
