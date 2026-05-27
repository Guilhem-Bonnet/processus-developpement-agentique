# Exemple rempli - workflow state manifest

```yaml
workflow:
  id: WF-feature-simple
  owner: orchestration
  version: "1.0"
  profile: orchestre
  states:
    - id: intake
      output: brief_agentique
      evidence: brief-agentique.md
    - id: discovery
      input: brief_agentique
      output: context_scorecard
      evidence: context-pack.md
    - id: implementation
      input: task_envelope
      output: patch
      evidence: diff + tests
    - id: verification
      input: evidence_pack
      output: verification_verdict
      evidence: verification-verdict.md
  transitions:
    - from: intake
      to: discovery
      guard: brief.scope_defined == true
    - from: discovery
      to: implementation
      guard: context_scorecard.sufficiency in ["medium", "high"]
    - from: implementation
      to: verification
      guard: evidence_pack.exists == true
    - from: verification
      to: done
      guard: verification_verdict.decision == "close"
  interrupts:
    - id: human_required
      trigger: risk_level in ["high", "critical"]
      resume_state: discovery
```

