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
