# Exemple rempli - capability pack

```yaml
capability_pack:
  id: CAP-code-reviewer
  name: Code Reviewer Agentique
  owner: quality
  version: "1.0"
  status: canary
  roles:
    - code_reviewer
  skills:
    - SKL-diff-risk-review
    - SKL-test-gap-analysis
  permissions:
    files: read
    shell: denied
    network: denied
    model_providers:
      - github-copilot
      - anthropic
  runtime:
    compatible:
      - local-worker
      - ide-integrated
  tests:
    - id: detects-secret-risk
      expected: flags_secret_or_sensitive_diff
    - id: avoids-style-only-comments
      expected: only_material_findings
  telemetry:
    required_spans:
      - agent.capability.resolve
      - agent.subagent.run
      - agent.evidence.pack
```

