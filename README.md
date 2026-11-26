# .github

Configuración compartida de la organización Waypoint Studio.

- `profile/README.md`: perfil público de la organización.
- `.github/ISSUE_TEMPLATE` y `pull_request_template.md`: plantillas por defecto para todos los repos.
- `CONTRIBUTING.md` y `SECURITY.md`: políticas por defecto.

## Workflows reutilizables

### `node-ci.yml`

Format, lint, typecheck, tests con cobertura, e2e opcional, build y SonarCloud opcional.

```yaml
jobs:
  ci:
    uses: Waypoint-Studio/.github/.github/workflows/node-ci.yml@main
    with:
      run-e2e: true
      sonar: false
    secrets: inherit
```

### `docker-publish.yml`

Build y push de la imagen a GHCR con tags `sha`, `latest` y semver.

```yaml
jobs:
  docker:
    permissions:
      contents: read
      packages: write
    uses: Waypoint-Studio/.github/.github/workflows/docker-publish.yml@main
    secrets: inherit
```

### `deploy-ssh.yml`

Despliega una app en el droplet por SSH ejecutando `scripts/deploy.sh` del repo `infra`. Por defecto usa el tag `sha-<commit>` que publica `docker-publish.yml`.

```yaml
jobs:
  deploy:
    needs: docker
    uses: Waypoint-Studio/.github/.github/workflows/deploy-ssh.yml@main
    with:
      app: mi-app
    secrets: inherit
```

Secretos en el repo de la app: `DEPLOY_HOST`, `DEPLOY_USER`, `DEPLOY_SSH_KEY` y `DEPLOY_KNOWN_HOSTS` (salida de `ssh-keyscan <host>`).
