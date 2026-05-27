# Exemple rempli - browser tool contract

```yaml
browser_tool:
  id: BTW-ui-validation
  owner: qa-design
  status: active
  scope:
    allowed_urls:
      - http://localhost:3000/**
      - https://staging.example.com/**
    denied_urls:
      - https://prod.example.com/**
  auth:
    mode: test_account
    account_ref: qa-ui-test
  allowed_actions:
    - navigate
    - click
    - type
    - screenshot
    - snapshot
  denied_actions:
    - payment
    - delete_account
    - publish
  evidence:
    before_action:
      - dom_snapshot
    after_action:
      - screenshot
      - console_errors
      - network_errors
  controls:
    risky_action_requires: human_validation
    production_access: denied
```

