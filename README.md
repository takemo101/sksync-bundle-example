# sksync-bundle-example

Example [sksync](https://github.com/takemo101/sksync) bundle manifest.

This repository contains a `sksync.bundle.json` at the repository root, so it can be installed directly from the GitHub tree URL. It also includes a local `sksync` helper skill that teaches agents how to find, add, remove, and audit Agent Skills with `sksync` and `npx skills find`.

## Inspect

```sh
sksync bundle inspect https://github.com/takemo101/sksync-bundle-example/tree/main
```

## Install

Choose the agents you want to link the bundle entries into:

```sh
sksync bundle add https://github.com/takemo101/sksync-bundle-example/tree/main --agent pi --agent claude-code
```

Preview first:

```sh
sksync bundle add https://github.com/takemo101/sksync-bundle-example/tree/main --agent pi --dry-run
```

## Notes

- Bundle manifests do not choose agents. Pass `--agent` at install time.
- Most entries point to existing upstream skill sources.
- The `sksync` entry is local to this repository at `./skills/sksync`.
- Many entries use `HEAD`, which tracks upstream changes. Pin refs to tags or commit SHAs when strict reproducibility matters.
