# coverage-badge-action

> Push a [shields.io](https://shields.io) coverage badge to an orphan branch or gist

[![GitHub: Release](https://img.shields.io/github/v/release/deadnews/coverage-badge-action?logo=github&logoColor=white)](https://github.com/deadnews/coverage-badge-action/releases/latest)
[![CI: Main](https://img.shields.io/github/actions/workflow/status/deadnews/coverage-badge-action/main.yml?branch=main&logo=github&logoColor=white&label=main)](https://github.com/deadnews/coverage-badge-action/actions/workflows/main.yml)
![Coverage: branch](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/deadnews/coverage-badge-action/badges/coverage.json)
![Coverage: gist](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/deadnews/eb0c3af607cb0c996bdcd7a5acc43b98/raw/coverage-badge-action-coverage.json)

## Usage

### Orphan branch (default)

Pushes `coverage.json` to an orphan branch in the same repo. Works with the default `GITHUB_TOKEN`.

```yml
permissions:
  contents: write

steps:
  - name: Upload coverage
    uses: deadnews/coverage-badge-action@v1
    with:
      file: coverage.txt
      type: go
```

```md
![Coverage](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/USER/REPO/badges/coverage.json)
```

### Gist

Pushes `REPO-coverage.json` to a gist. One gist can store badges for all your repos. Requires a PAT with `gist` scope.

```yml
steps:
  - name: Upload coverage
    uses: deadnews/coverage-badge-action@v1
    with:
      file: coverage.txt
      type: go
      gist-id: ${{ vars.GIST_ID }}
      gist-token: ${{ secrets.GIST_TOKEN }}
```

```md
![Coverage](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/USER/GIST_ID/raw/REPO-coverage.json)
```

### Inputs

| Input        | Required | Default  | Description                   |
| ------------ | -------- | -------- | ----------------------------- |
| `file`       | yes      | —        | Path to coverage file         |
| `type`       | yes      | —        | `go` or `lcov`                |
| `branch`     | no       | `badges` | Orphan branch name            |
| `gist-id`    | no       | —        | Gist ID (enables `gist` mode) |
| `gist-token` | no       | —        | PAT with `gist` scope         |

## Examples

### Go

```yml
- run: go test -coverprofile=coverage.txt ./...
- uses: deadnews/coverage-badge-action@v1
  with:
    file: coverage.txt
    type: go
```

### Rust

```yml
- run: cargo llvm-cov --lcov --output-path lcov.info
- uses: deadnews/coverage-badge-action@v1
  with:
    file: lcov.info
    type: lcov
```

### Python

```yml
- run: pytest --cov --cov-report=lcov
- uses: deadnews/coverage-badge-action@v1
  with:
    file: coverage.lcov
    type: lcov
```
