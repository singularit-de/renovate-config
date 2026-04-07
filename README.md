# renovate-config

Shareable [Renovate](https://docs.renovatebot.com/) config presets for singularIT.

## Usage

### Default preset

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>singularit-de/renovate-config#0.0.3"
  ]
}
```

### GitLab (self-hosted) preset

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>singularit-de/renovate-config:gitlab#0.0.3"
  ]
}
```

### Docker preset

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>singularit-de/renovate-config:docker#0.0.3"
  ]
}
```

## Presets

| Preset    | Description                                                                                                          |
|-----------|----------------------------------------------------------------------------------------------------------------------|
| `default` | Combines base, docker, python, and gitlab presets                                                                    |
| `base`    | Extends `config:best-practices`, `:rebaseStalePrs`, and `mergeConfidence:all-badges` with assignees from code owners |
| `docker`  | Enables `docker:pinDigests` and `docker:enableMajor`                                                                 |
| `python`  | Configures `pip_requirements` file matching                                                                          |
| `gitlab`  | Enables OSV vulnerability alerts for self-hosted GitLab                                                              |
| `node`    | Sets `rangeStrategy` to `bump` for Node.js projects                                                                 |

## Releasing

```bash
npm run release
```

Uses [bumpp](https://github.com/antfu-collective/bumpp) to interactively bump the version, create a git tag, and push to
origin. A GitHub Actions workflow then creates a GitHub Release.

Version pins in transitive config references (e.g. `github>singularit-de/renovate-config:base#0.0.3 in `default.json`)
are automatically updated to the new version during the bump.
