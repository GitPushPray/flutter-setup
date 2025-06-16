# Setup Flutter

A GitHub Action to install the Flutter SDK on Linux, macOS, or Windows runners.  
Easily specify the Flutter version, architecture, and release channel (stable or beta).

## Usage

Add the following step to your workflow:

```yaml
- name: Setup Flutter
  uses: GitPushPray/flutter-setup@v1
  with:
    os: linux           # Optional: linux, macos, or windows (default: linux)
    arch: x64           # Optional: x64 or arm64 (default: x64)
    version: stable     # Optional: Flutter version (e.g., 3.29.3, 3.32.0-0.2.pre, default: stable)
    is-beta: "false"    # Optional: "true" for beta channel, "false" for stable (default: "false")
```

### Example Workflow

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Flutter
        uses: GitPushPray/flutter-setup@v1
        with:
          os: linux
          arch: x64
          version: 3.29.3
          is-beta: "false"
      - run: flutter --version
      - run: flutter doctor -v
```

## Inputs

| Name      | Description                                 | Default   |
|-----------|---------------------------------------------|-----------|
| os        | Target OS (`linux`, `macos`, `windows`)     | linux     |
| arch      | CPU architecture (`x64`, `arm64`)           | x64       |
| version   | Flutter version (e.g., `3.29.3`)            | stable    |
| is-beta   | Use beta channel (`"true"` or `"false"`)    | "false"   |

## How it works

- Downloads the specified Flutter SDK release for your OS and architecture.
- Extracts the SDK and adds `flutter/bin` to the PATH.
- Runs `flutter doctor -v` to verify the installation.

## License

MIT

---

**Marketplace Keywords:** flutter, dart, setup, install, github-action, ci, cd, mobile, cross-platform
