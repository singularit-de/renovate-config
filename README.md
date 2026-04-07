# renovate-config

Shareable [Renovate](https://docs.renovatebot.com/) config presets for singularIT.

## Usage

### Default preset

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>singularit-de/renovate-config"]
}
```

### GitLab (self-hosted) preset

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>singularit-de/renovate-config:gitlab"]
}
```

### Docker preset

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>singularit-de/renovate-config:docker"]
}
```

### Pin to a version

```json
{
  "extends": ["github>singularit-de/renovate-config#1.0.0"]
}
```

## Presets

| Preset | Description |
|--------|-------------|
| `default` | Base config extending `config:best-practices` with automerge, scheduling, and labels |
| `gitlab` | Self-hosted GitLab config with auto-approve and merge strategy |
| `docker` | Docker-specific grouping, pinning, and automerge rules |

## Releasing

```bash
npm run release
```

Uses [bumpp](https://github.com/antfu-collective/bumpp) to interactively bump the version, create a git tag, and push to origin. A GitHub Actions workflow then creates a GitHub Release.
