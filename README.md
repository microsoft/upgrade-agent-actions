# Copilot Coding Agent Setup

A GitHub Action that prepares the [GitHub Copilot Coding Agent](https://docs.github.com/en/copilot/using-github-copilot/using-copilot-coding-agent) development environment with the tools and SDKs it needs to build, test, and modernize .NET projects.

For instructions on running modernize-dotnet with the Copilot coding agent, see the [coding agent README](https://github.com/dotnet/modernize-dotnet/blob/main/coding-agent/README.md).

## Usage

Add this action as a step inside your repository's `copilot-setup-steps.yml` workflow:

```yaml
name: "Copilot Setup Steps"

on:
  workflow_dispatch:
  pull_request:
    paths:
      - .github/workflows/copilot-setup-steps.yml

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - uses: dotnet/modernize-dotnet-actions@main
```

### .NET Framework / Windows desktop workloads

Use a Windows runner and enable the targeting pack installer:

```yaml
jobs:
  copilot-setup-steps:
    runs-on: windows-latest
    permissions:
      contents: read
    steps:
      - uses: dotnet/modernize-dotnet-actions@main
        with:
          install-framework-targeting-packs: 'true'
```

> **Note:** When using Windows runners, you must also disable the integrated firewall in your repository settings under **Settings → Copilot → Coding agent**. See the [coding-agent README](coding-agent/README.md) for details.

## Inputs

| Input | Description | Default |
|---|---|---|
| `dotnet-version` | .NET SDK version to install | `10.0.x` |
| `node-version` | Node.js version to install | `20` |
| `install-framework-targeting-packs` | Install .NET Framework 4.7.1–4.8.1 SDK and targeting packs (Windows only) | `false` |

## License

See [LICENSE](LICENSE) for details.
