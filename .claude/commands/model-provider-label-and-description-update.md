---
name: model-provider-label-and-description-update
description: Workflow command scaffold for model-provider-label-and-description-update in hermes-agent.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /model-provider-label-and-description-update

Use this workflow when working on **model-provider-label-and-description-update** in `hermes-agent`.

## Goal

Refreshes or restructures the model provider labels, descriptions, and groupings in the model picker UI and related tests.

## Common Files

- `hermes_cli/models.py`
- `hermes_cli/main.py`
- `gateway/platforms/telegram.py`
- `tests/hermes_cli/test_provider_groups.py`
- `plugins/model-providers/*/__init__.py`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit hermes_cli/models.py to update PROVIDER_GROUPS, labels, or descriptions.
- Update UI logic in hermes_cli/main.py and/or gateway/platforms/telegram.py to reflect new grouping/description logic.
- Update or add tests in tests/hermes_cli/test_provider_groups.py to assert new grouping/description logic.
- Optionally update provider plugin __init__.py files for provider-specific copy.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.