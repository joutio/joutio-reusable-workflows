# AGENTS.md — joutio-reusable-workflows

GitHub Actions communes à tous les dépôts Joutio : workflows réutilisables (`.github/workflows/`),
actions composites (`actions/`), Dockerfiles (`docker/`), configuration Maven, npm et
semantic-release partagée. Hors architecture hexagonale.

Lire : `../../AGENTS.md`, puis **[`docs/ops/ci.md`](../../docs/ops/ci.md)** (workflows, actions,
release, secrets des dépôts, rétention du stockage).

## Règles

- Les wrappers des dépôts appellent `…@main` : toute modification ici touche immédiatement toutes
  les CI. Garder les entrées rétrocompatibles ou mettre à jour tous les wrappers dans le même lot.
- Un secret ne s'écrit jamais en clair : seuls `JOUTIO_GITHUB_USERNAME` (variable) et
  `JOUTIO_GITHUB_TOKEN` (secret) sont attendus des dépôts (le mobile ajoute les siens à son propre `release.yml`).
- `prune-packages.yml` ne supprime jamais un tag déployé ni une version de `joutio-parent`.
- Images en `linux/arm64` (cluster de Raspberry Pi).

## Structure

```
actions/{build-push-docker,semantic-release,setup-java-maven,setup-node-npm,prune-packages}/action.yml
.github/workflows/{service,lib,frontend}-{ci,release}.yml, domain-bootstrap.yml, prune-packages.yml
docker/Dockerfile.service, docker/Dockerfile.frontend
maven/settings.xml, npm/.npmrc, semantic-release/release.{maven,npm}.config.cjs
```
