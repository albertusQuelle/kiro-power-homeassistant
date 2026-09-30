---
inclusion: manual
---

# Commit Message Standards

This project uses [Conventional Commits](https://www.conventionalcommits.org/). Release notes are generated automatically from commit messages by [git-cliff](https://git-cliff.org/) (see `.github/cliff.toml`), so the type prefix matters.

## Format

```
<type>(<optional scope>): <description>

<optional body>

<optional footer>
```

- Use the imperative mood in the description ("add", not "added" or "adds").
- Keep the description concise (about 72 characters or fewer).
- Do not end the description with a period.
- Use lowercase for the type and scope.

## Allowed Types

These map to the changelog groups defined in `.github/cliff.toml`:

| Type       | Changelog group   | Use for                                        |
|------------|-------------------|------------------------------------------------|
| `feat`     | 🚀 New Features    | A new feature or capability                    |
| `fix`      | 🐛 Bug Fixes       | A bug fix                                       |
| `perf`     | ⚡ Performance     | A performance improvement                       |
| `refactor` | ✨ Refactoring     | A code change that neither fixes nor adds       |
| `test`     | 🧪 Tests           | Adding or correcting tests                      |
| `docs`     | 📚 Documentation   | Documentation only changes                      |
| `style`    | 🎨 Styling         | Formatting, whitespace (no behavior change)     |
| `build`    | 📦 Build           | Build system or dependency changes              |
| `ci`       | ⚙️ CI/CD           | CI configuration and scripts                    |
| `chore`    | 🔧 Maintenance     | Routine maintenance not covered above           |

## Scopes

Use an optional scope to indicate the affected area, for example:

- `feat(power): ...` — changes to `POWER.md`
- `feat(mcp): ...` — changes to `power-homeassistant/mcp.json`
- `feat(steering): ...` — changes to steering guides
- `docs: ...` — README and general docs

## Notes on Release Automation

- `chore: bump version ...` and `chore(release): ...` commits are intentionally skipped in the changelog.
- Unconventional commits are filtered out of release notes, so always use a valid type.

## Examples

```
feat(mcp): update autoApprove list for ha-mcp 8.x tools
fix(steering): correct dead tool names in advanced workflows
docs: document HACS in-process install method
chore: bump version to 0.4.0
```
