# Exemple rempli - knowledge source index

> Statut : annexe informative. Cet exemple illustre un template ; il ne remplace pas une preuve active dans un projet réel.

```yaml
knowledge_source:
  id: KSI-product-docs
  type: git_repo
  owner: documentation
  source_uri: https://github.com/example/product-docs
  scope:
    include:
      - docs/**
      - adr/**
      - api/**
    exclude:
      - secrets/**
      - drafts/private/**
  access:
    mode: read_only
    acl: internal
    sensitive: possible
  indexing:
    lexical: true
    vector: true
    graph: true
    chunking: heading_aware
    metadata:
      - commit_sha
      - path
      - owner
      - valid_from
      - superseded_by
  freshness:
    trigger: webhook_or_daily
    stale_after_days: 14
  retrieval_policy:
    max_results: 8
    require_source_link: true
    critical_decision_requires_active_source: true
```
