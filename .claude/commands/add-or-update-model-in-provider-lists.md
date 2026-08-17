---
name: add-or-update-model-in-provider-lists
description: Workflow command scaffold for add-or-update-model-in-provider-lists in hermes-agent.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /add-or-update-model-in-provider-lists

Use this workflow when working on **add-or-update-model-in-provider-lists** in `hermes-agent`.

## Goal

Adds a new model to one or more provider lists, or updates model metadata (e.g., context length, fallback snapshot) for existing models.

## Common Files

- `hermes_cli/models.py`
- `agent/model_metadata.py`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit hermes_cli/models.py to add or update the model in provider lists.
- Edit agent/model_metadata.py to update context lengths or other metadata if needed.
- Optionally update fallback snapshots or default model selection logic.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.