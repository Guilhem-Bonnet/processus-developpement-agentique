# Modèle de memory record

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Memory ID | MEM-... |
| Source ID | SRC-... |
| Mission ID | MIS-... |
| Type | fait / décision / préférence / incident / apprentissage / contrainte |
| Portée | mission / projet / produit / organisation / utilisateur |
| Propriétaire | A renseigner |

## Contenu

| Champ | Valeur |
| --- | --- |
| Sujet | A renseigner |
| Contenu minimal | A renseigner |
| Confiance | low / medium / high |
| Statut | candidate / active / durable_memory / archived / superseded / obsolete / sensitive |
| Sensibilité | public / interne / confidentiel / secret / données personnelles |

## Validité et rétention

| Champ | Valeur |
| --- | --- |
| valid_from | A renseigner |
| valid_until | A renseigner |
| retention_class | durable / projet / mission / court terme / purge |
| indexable | oui / non |
| raison indexation | A renseigner |
| superseded_by | A renseigner si applicable |

## Contrôle

| Contrôle | Résultat |
| --- | --- |
| Source active vérifiée | oui / non |
| Données sensibles minimisées | oui / non |
| Hypothèse séparée du fait | oui / non |
| TTL ou trigger défini | oui / non |
