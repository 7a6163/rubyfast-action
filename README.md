# RubyFast GitHub Action

A GitHub Action for [RubyFast](https://github.com/7a6163/rubyfast) — a blazing-fast Ruby performance linter written in Rust.

## Usage

```yaml
- uses: 7a6163/rubyfast-action@v1
  with:
    path: "."
```

### Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `path` | Path to scan (file or directory) | `.` |
| `version` | RubyFast version (e.g. `1.0.0`) | `latest` |
| `args` | Additional arguments passed to rubyfast | |
| `reviewdog` | Enable reviewdog inline PR comments | `false` |
| `github-token` | GitHub token for reviewdog API access | `${{ github.token }}` |
| `reviewdog-reporter` | reviewdog reporter | `github-pr-review` |
| `reviewdog-filter-mode` | reviewdog filter mode | `added` |

### Outputs

| Output | Description |
|--------|-------------|
| `exit-code` | Exit code from rubyfast (0=clean, 1=offenses found) |

### Example: Basic

```yaml
name: Lint
on: [push, pull_request]

jobs:
  rubyfast:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: 7a6163/rubyfast-action@v1
```

### Example: With reviewdog

```yaml
name: Lint
on: [pull_request]

jobs:
  rubyfast:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      checks: write
      pull-requests: write
    steps:
      - uses: actions/checkout@v4
      - uses: 7a6163/rubyfast-action@v1
        with:
          reviewdog: "true"
          github-token: ${{ secrets.GITHUB_TOKEN }}
          reviewdog-reporter: github-pr-review
```

### Example: Scan specific directory

```yaml
- uses: 7a6163/rubyfast-action@v1
  with:
    path: "app/models"
```

### Example: Pin version

```yaml
- uses: 7a6163/rubyfast-action@v1
  with:
    version: "1.0.0"
```

## License

MIT
