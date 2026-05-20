# Patterns organisationnels

Les patterns organisationnels définissent la séparation des responsabilités entre l'utilisateur-client, l'entreprise-agent, les rôles spécialisés et les autorités de validation.

La source Mermaid de cette famille est disponible dans [../../../diagrammes/patterns-organisation.mmd](../../../diagrammes/patterns-organisation.mmd).

## ORG-01 : Entreprise-agent

| Élément | Description |
| --- | --- |
| Intention | Traiter l'agent comme une organisation opératrice plutôt que comme un simple assistant. |
| Problème | Un agent conversationnel mélange besoin, exécution, validation et mémoire. |
| Solution | Séparer rôles, responsabilités, validations, preuves et mémoire comme dans une entreprise. |
| Contrôles | RACI, Kanban, validateur final, contrats entre rôles, dossier d'acceptation. |
| Anti-pattern | Agent unique qui décide, exécute et valide seul. |

## ORG-02 : Validation authority

| Élément | Description |
| --- | --- |
| Intention | Savoir qui peut accepter, bloquer ou demander correction. |
| Problème | L'agent confond complétion technique et acceptation métier. |
| Solution | Définir les autorités par domaine : client, QA, sécurité, ops, design, architecture. |
| Contrôles | RACI, matrice de validation, dossier d'acceptation, verdict de vérification. |
| Anti-pattern | L'agent ferme une carte sensible sans validateur identifié. |

## Interfaces liées

| Interface | Rôle |
| --- | --- |
| Brief agentique | Formalise la demande et les contraintes client. |
| Carte Kanban | Porte le lot de travail, l'état, les risques et les validateurs. |
| Dossier d'acceptation | Permet au client ou validateur de décider en connaissance de cause. |
