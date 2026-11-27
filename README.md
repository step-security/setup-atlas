[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

# setup-action

A GitHub Action for installing [Atlas](https://github.com/ariga/atlas).

## Usage

Add `.github/workflows/deploy-schema.yaml` to your repo with the following contents:

```yaml
name: Deploy schema changes
run-name: I'm using Atlas 🚀
on: [push]
jobs:
  use-atlas:
    runs-on: ubuntu-latest
    steps:
      - uses: step-security/setup-atlas@v0
      - run: atlas version
      # - run: atlas schema apply ... 
```

## Inputs

### Version

By default, the `latest` version of Atlas is being used. If you want to lock a specific version of Atlas, you can do so by specifying the `version` parameter.

```yaml
- uses: step-security/setup-atlas@v0
  with:
    version: "vX.Y.Z"
```

### Flavor

If you want to install a specific driver flavor of Atlas, you can do so by specifying the `flavor` parameter.

```yaml
- uses: step-security/setup-atlas@v0
  with:
    flavor: "snowflake"
```

### cloud-token

The Atlas Cloud token to use for authentication. Must be passed as a secret.
```yaml
- uses: step-security/setup-atlas@v0
  with:
    cloud-token: ${{ secrets.ATLAS_CLOUD_TOKEN }}
```

## Caching

On Linux and macOS the binary is installed to `~/.atlas-bin` and cached between runs with
[actions/cache](https://github.com/actions/cache), keyed by OS, architecture, requested version and the installed build.
When the cached binary is already up to date, the download is skipped. `latest` always checks for a newer
release, and a new cache entry is saved only when the binary has changed.

## Legal

The source code for this GitHub Action is released under the Apache 2.0
License, see [LICENSE](LICENSE).

This action downloads a binary version of [Atlas](https://atlasgo.io) which
is distributed under the [Ariga EULA](https://ariga.io/legal/atlas/eula).
