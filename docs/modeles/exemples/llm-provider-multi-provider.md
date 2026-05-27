# Exemple rempli - LLM provider registry

> Statut : annexe informative. Cet exemple illustre un template ; il ne remplace pas une preuve active dans un projet réel.

```yaml
llm_providers:
  - provider_id: github-copilot
    access_mode: ide_integrated
    data_policy: internal_allowed
    models:
      - id: copilot-default
        capabilities: [code, chat, tool_use]
        status: active
  - provider_id: anthropic
    access_mode: api
    data_policy: no_sensitive_data
    models:
      - id: claude-sonnet
        capabilities: [reasoning, code, long_context, tool_use]
        status: active
  - provider_id: openai
    access_mode: api
    data_policy: no_sensitive_data
    models:
      - id: codex
        capabilities: [code, reasoning, tool_use]
        status: active
  - provider_id: local
    access_mode: local
    data_policy: sensitive_allowed
    models:
      - id: local-code
        capabilities: [code]
        status: restricted

routing:
  task_defaults:
    code_low_risk:
      primary: github-copilot/copilot-default
      fallback: openai/codex
    architecture_high_risk:
      primary: anthropic/claude-sonnet
      fallback: human_escalation
    sensitive_local:
      primary: local/local-code
      fallback: human_escalation
```
