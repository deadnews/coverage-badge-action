# action-coverage-badge

> Push a [shields.io](https://shields.io) coverage badge to an orphan branch

[![GitHub: Release](https://img.shields.io/github/v/release/deadnews/action-coverage-badge?logo=github&logoColor=white)](https://github.com/deadnews/action-coverage-badge/releases/latest)
[![CI: Main](https://img.shields.io/github/actions/workflow/status/deadnews/action-coverage-badge/main.yml?branch=main&logo=github&logoColor=white&label=main)](https://github.com/deadnews/action-coverage-badge/actions/workflows/main.yml)

## Usage

```yml
permissions:
  contents: write

steps:
  - uses: deadnews/action-coverage-badge@v1
    with:
      file: coverage.txt
      type: go
```

Badge link:

```md
![Coverage](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/USER/REPO/badges/coverage.json)
```

### Inputs

| Input    | Required | Default  | Description           |
| -------- | -------- | -------- | --------------------- |
| `file`   | yes      | —        | Path to coverage file |
| `type`   | yes      | —        | `go` or `lcov`        |
| `branch` | no       | `badges` | Orphan branch name    |

### Outputs

| Output     | Description         |
| ---------- | ------------------- |
| `coverage` | Coverage percentage |

## Examples

### Go

```yaml
- run: go test -coverprofile=coverage.txt ./...
- uses: deadnews/action-coverage-badge@v1
  with:
    file: coverage.txt
    type: go
```

### Rust

```yml
- run: cargo llvm-cov --lcov --output-path lcov.info
- uses: deadnews/action-coverage-badge@v1
  with:
    file: lcov.info
    type: lcov
```

### Python

```yml
- run: pytest --cov --cov-report=lcov
- uses: deadnews/action-coverage-badge@v1
  with:
    file: coverage.lcov
    type: lcov
```
