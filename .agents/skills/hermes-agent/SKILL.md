```markdown
# hermes-agent Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the established development patterns, coding conventions, and common workflows for contributing to the `hermes-agent` repository. The project is primarily written in TypeScript, with a focus on CLI, desktop, and Dockerized environments. It uses conventional commits, kebab-case file naming, and a modular, test-driven approach. You'll learn how to update model providers, add models, manage Docker permissions, enhance the desktop app, sync CLI skills, and handle environment secrets.

## Coding Conventions

- **File Naming:**  
  Use kebab-case for all file names.  
  _Example:_  
  ```
  model-provider-list.ts
  agent-config.ts
  ```

- **Import Style:**  
  Use alias imports for modules.  
  _Example:_  
  ```typescript
  import { getModelList } from '@/models/model-list';
  ```

- **Export Style:**  
  Use named exports.  
  _Example:_  
  ```typescript
  export function syncSkills() { ... }
  export const DEFAULT_UID = 34107;
  ```

- **Commit Messages:**  
  Follow [Conventional Commits](https://www.conventionalcommits.org/) with prefixes: `fix`, `feat`, `chore`, `docs`.  
  _Example:_  
  ```
  feat: add support for new model provider grouping
  fix: correct UID/GID handling in Docker containers
  ```

## Workflows

### Model Provider Label and Description Update
**Trigger:** When updating how model providers are presented to users (labels, descriptions, groupings).  
**Command:** `/update-model-provider-labels`

1. Edit `hermes_cli/models.py` to update `PROVIDER_GROUPS`, labels, or descriptions.
2. Update UI logic in `hermes_cli/main.py` and/or `gateway/platforms/telegram.py` to reflect new grouping/description logic.
3. Update or add tests in `tests/hermes_cli/test_provider_groups.py` to assert new grouping/description logic.
4. Optionally update provider plugin `__init__.py` files for provider-specific copy.

_Code Example:_
```python
# hermes_cli/models.py
PROVIDER_GROUPS = {
    "OpenAI": {"label": "OpenAI", "description": "High-quality GPT models"},
    # ...
}
```

---

### Add or Update Model in Provider Lists
**Trigger:** When adding a new model or updating model metadata for a provider.  
**Command:** `/add-model`

1. Edit `hermes_cli/models.py` to add or update the model in provider lists.
2. Edit `agent/model_metadata.py` to update context lengths or other metadata if needed.
3. Optionally update fallback snapshots or default model selection logic.

_Code Example:_
```python
# hermes_cli/models.py
PROVIDERS["openai"]["models"].append("gpt-4o")
```

---

### Docker UID/GID Chown Fix
**Trigger:** When fixing or hardening file/directory permissions in Dockerized deployments.  
**Command:** `/fix-docker-chown`

1. Edit `docker/stage2-hook.sh` to validate or fix UID/GID handling.
2. Edit `hermes_cli/config.py` or `hermes_cli/container_boot.py` to ensure chown logic is correct.
3. Add or update tests in `tests/hermes_cli/test_container_boot.py` or `tests/hermes_cli/test_ensure_hermes_home_uid_34107.py`.

_Code Example:_
```bash
# docker/stage2-hook.sh
chown -R $HERMS_UID:$HERMS_GID /app/data
```

---

### Desktop App Feature or Fix
**Trigger:** When adding a desktop feature, fixing a bug, or refactoring an existing flow.  
**Command:** `/desktop-feature`

1. Edit or add files in `apps/desktop/src/app/` for UI changes.
2. Edit `apps/desktop/electron/main.cjs` and related Electron scripts for backend/bootstrapping logic.
3. Edit `apps/desktop/scripts/` for build or runtime support.
4. Update `apps/desktop/README.md` or documentation as needed.
5. Optionally update or add tests in `apps/desktop/src/app/` or scripts.

_Code Example:_
```tsx
// apps/desktop/src/app/NewFeature.tsx
export function NewFeature() {
  return <div>New Desktop Feature</div>;
}
```

---

### Update or Fix CLI Skill Sync
**Trigger:** When fixing missing skills in new installs or ensuring skills are always available.  
**Command:** `/sync-skills`

1. Refactor or add helper in `hermes_cli/main.py` to centralize skill sync logic.
2. Call the helper from multiple CLI entrypoints (`cmd_chat`, `cmd_dashboard`, `cmd_gateway`).
3. Optionally update or add tests for skill sync behavior.

_Code Example:_
```python
# hermes_cli/main.py
def sync_skills():
    # logic to sync bundled skills
```

---

### Fix or Harden Env Secret Forwarding
**Trigger:** When fixing or hardening how environment variables and secrets are forwarded to Docker containers or sandboxes.  
**Command:** `/fix-docker-env`

1. Edit `tools/environments/docker.py` to fix secret forwarding logic.
2. Update or add tests in `tests/tools/test_docker_environment.py`.
3. Optionally update `scripts/release.py` for attribution if needed.

_Code Example:_
```python
# tools/environments/docker.py
if secret_value:
    env_vars[secret_name] = secret_value
```

## Testing Patterns

- **Framework:**  
  Uses [vitest](https://vitest.dev/) for testing.

- **Test File Pattern:**  
  All test files use the `*.test.ts` naming convention.

- **Example Test:**
  ```typescript
  // agent-config.test.ts
  import { getConfig } from './agent-config';

  test('returns default config', () => {
    expect(getConfig()).toHaveProperty('uid', 34107);
  });
  ```

## Commands

| Command                       | Purpose                                                        |
|-------------------------------|----------------------------------------------------------------|
| /update-model-provider-labels  | Update model provider labels, descriptions, and groupings      |
| /add-model                    | Add or update a model in provider lists                        |
| /fix-docker-chown             | Fix UID/GID ownership and permissions in Docker containers      |
| /desktop-feature              | Add, fix, or refactor a desktop app feature                    |
| /sync-skills                  | Sync bundled skills for CLI, dashboard, and gateway            |
| /fix-docker-env               | Fix or harden environment secret forwarding in Docker           |
```
