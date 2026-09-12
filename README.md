# RepoKit

This repository manages repositories for development across both local and
remote environments.

| Management area | Tool | Path |
| --- | --- | --- |
| Remote GitHub settings | [gh-infra](https://github.com/babarot/gh-infra) | [`./infra.yaml`](./infra.yaml) |
| Local Go repository templates | [gonew](https://pkg.go.dev/golang.org/x/tools/cmd/gonew) | [`./templates/cli`](./templates/cli), [`./templates/pkg`](./templates/pkg) |

## Requirements

Install gh-infra as a GitHub CLI extension.

```sh
gh extension install babarot/gh-infra
```

Install gonew.

```sh
go install golang.org/x/tools/cmd/gonew@latest
```

## GitHub repository settings

Repository settings are defined in `infra.yaml`. Validate the manifest and
review the planned changes before applying them.

```sh
gh infra validate infra.yaml
gh infra plan infra.yaml
gh infra apply infra.yaml
```

Set `HOMEBREW_TAP_GITHUB_TOKEN` before applying changes that manage the
corresponding repository secret.

## Go repository templates

Create a CLI repository from `templates/cli`.

```sh
gonew github.com/nekrassov01/repokit/templates/cli \
  github.com/nekrassov01/my-cli
```

Create a package repository from `templates/pkg`.

```sh
gonew github.com/nekrassov01/repokit/templates/pkg \
  github.com/nekrassov01/my-package
```

gonew rewrites the module path in `go.mod` and Go source files. It does not
rewrite other files. After creating a repository, replace `DUMMY` with the
repository or command name in these files:

- CLI: `README.md`, `Makefile`, and `.goreleaser.yml`
- Package: `README.md`

For a CLI repository, also set the Homebrew description in `.goreleaser.yml`.

## Structure

```text
.
├── infra.yaml
└── templates
    ├── cli
    │   └── go.mod
    └── pkg
        └── go.mod
```
