# Modèle de contrat MCP

## Identification

| Champ | Valeur |
| --- | --- |
| Nom du serveur MCP | A renseigner |
| Propriétaire | A renseigner |
| Usage métier | A renseigner |
| Environnement | local / staging / production / externe |
| Niveau de risque | faible / moyen / élevé / critique |

## Scopes et permissions

| Scope | Lecture | Écriture | Conditions |
| --- | --- | --- | --- |
| A renseigner | oui / non | oui / non | A renseigner |

## Données

| Question | Réponse |
| --- | --- |
| Données sensibles traitées ? | oui / non |
| Données personnelles ? | oui / non |
| Secrets nécessaires ? | oui / non |
| Rétention côté serveur | A renseigner |
| Masquage dans les logs | A renseigner |

## Contrôles

| Contrôle | Règle |
| --- | --- |
| Authentification | A renseigner |
| Autorisation | scopes minimaux, allowlist, denylist |
| Timeout | A renseigner |
| Rate limit | A renseigner |
| Journalisation | requêtes, erreurs, décisions, masquage secrets |
| Validation humaine | requise pour écriture, production ou données sensibles |
| Rollback | A renseigner |

## Modes d'échec

| Échec | Réponse attendue |
| --- | --- |
| serveur indisponible | fallback ou blocage |
| permission refusée | demander validation ou réduire action |
| sortie contradictoire | vérifier source ou escalader |
| donnée sensible détectée | stop, masquage, procédure sécurité |
| effet externe inattendu | incident agentique |

## Acceptation

| Validateur | Date | Décision |
| --- | --- | --- |
| A renseigner | A renseigner | accepté / refusé / conditions |
