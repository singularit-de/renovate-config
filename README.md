# renovate-config

Shareable [Renovate](https://docs.renovatebot.com/) config presets for singularIT.

## Usage

### Default preset

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>singularit-de/renovate-config#0.0.7"
  ]
}
```

### GitLab (self-hosted) preset

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>singularit-de/renovate-config:gitlab#0.0.7"
  ]
}
```

### Docker preset

Includes all Docker sub-presets (base + versions).

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>singularit-de/renovate-config:docker#0.0.7"
  ]
}
```

Sub-presets can also be used individually:

- `:docker/base` — digest pinning and major updates
- `:docker/envVersions` — detects `_VERSION` variables in Dockerfiles via `# renovate:` comments

Example Dockerfile usage for `docker/envVersions`:

```dockerfile
# renovate: datasource=docker depName=node versioning=docker
ENV NODE_VERSION=18.17.0

# renovate: datasource=docker depName=php versioning=docker
ARG PHP_VERSION=8.2
```

> [!WARNING]
> Do not use `# renovate:` comments for variables that are used in a `FROM` directive. Renovate has native support for detecting and updating Docker image references in `FROM` lines. Adding a `# renovate:` comment in this case will override the native handling and **disable digest pinning** for that image.
>
> ```dockerfile
> # Bad – unnecessary, Renovate already handles this natively
> # renovate: datasource=docker depName=node versioning=docker
> ARG NODE_VERSION=18.17.0
> FROM node:${NODE_VERSION}
>
> # Good – Renovate updates the FROM reference automatically
> ARG NODE_VERSION=18.17.0
> FROM node:${NODE_VERSION}
> ```


## Presets

| Preset    | Description                                                                                                          |
|-----------|----------------------------------------------------------------------------------------------------------------------|
| `default` | Combines base, docker, python, and gitlab presets                                                                    |
| `base`    | Extends `config:best-practices`, `:rebaseStalePrs`, and `mergeConfidence:all-badges` with assignees from code owners |
| `docker`  | Combines `docker/base` and `docker/envVersions`                                                                         |
| `docker/base` | Enables `docker:pinDigests` and `docker:enableMajor`                                                             |
| `docker/envVersions` | Detects and updates `_VERSION` variables (ENV/ARG) in Dockerfiles via `# renovate:` comments              |
| `python`  | Configures `pip_requirements` file matching                                                                          |
| `gitlab`  | Enables OSV vulnerability alerts for self-hosted GitLab                                                              |
| `node`    | Sets `rangeStrategy` to `bump` for Node.js projects                                                                 |

## Releasing

```bash
npm run release
```

Uses [bumpp](https://github.com/antfu-collective/bumpp) to interactively bump the version, create a git tag, and push to
origin. A GitHub Actions workflow then creates a GitHub Release.

Version pins in transitive config references (e.g. `github>singularit-de/renovate-config:base#0.0.7 in `default.json`)
are automatically updated to the new version during the bump.
