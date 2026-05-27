# Modèle d'événement télémétrique agentique

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Event ID | TEL-... |
| Event name | A renseigner |
| Trace ID | A renseigner |
| Span ID | A renseigner |
| Mission ID | MIS-... |
| Task ID | TASK-... |
| Timestamp | A renseigner |

## Classification

| Champ | Valeur |
| --- | --- |
| Type | trace / metric / log / event |
| Domaine | mission / contexte / modèle / outil / preuve / mémoire / sécurité / conformité |
| Sévérité | debug / info / warning / error / critical |
| Sensibilité | public / interne / confidentiel / secret / données personnelles |

## Payload minimisé

| Champ | Valeur |
| --- | --- |
| Résumé | A renseigner |
| Attributs | A renseigner |
| Données masquées | oui / non / non applicable |
| Digest | sha256-... |

## Corrélation

| Référence | Valeur |
| --- | --- |
| Control ID | CTRL-... |
| Evidence ID | EVI-... |
| Verdict ID | VER-... |
| Incident ID | INC-... |
| Exception ID | EXC-... |
