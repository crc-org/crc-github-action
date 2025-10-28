# CRC GitHub Action

The CRC GitHub Action is a custom GitHub Action designed to integrate CRC into your CI/CD workflows.
This action facilitates the setup, start, and management of CRC instances directly within your GitHub
Actions pipelines, enabling seamless testing and development of your workload on OpenShift/MicroShift.


## Features

- **Automated CRC Setup**: Installs and configures CRC on the runner.
- **Cluster Management**: Starts CRC cluster.
- **Environment Configuration**: Sets up necessary environment variables for cluster access.

## Usage

To incorporate the CRC GitHub Action into your workflow, include the following steps in your GitHub Actions YAML file:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Remove unwanted stuff
        run: |
          # According to your needs
          #sudo rm -rf /usr/share/dotnet
          #sudo rm -rf /usr/local/lib/android

      - name: Set up CRC
        uses: crc-org/crc-github-action@v1
        with:
          pull-secret: ${{ secrets.CRC_PULL_SECRET }}
          preset: openshift/microshift/okd (default is microshift)
          memory: <In MiB, if you want to change from default>
          cpus: < int, if you want to change from default>
          disk: <In GiB, if you want to change from default>

      # Additional steps for your workflow
```

> [!NOTE]
> You are advised to maximize available diskspace using a third-party action.


### Inputs

| Name          | Description                                                   | Required | Default           |
|---------------|---------------------------------------------------------------|----------|-------------------|
| `pull-secret` | The pull secret for CRC, typically stored as a GitHub secret. | No       | dummy             |
| `preset`      | Available preset (openshift/microshift/okd).                  | No       | `'microshift'`    |
| `cpus`        | Number of cpus (default as per preset) (integer value)        | No       | `'as per preset'` |
| `memory`      | Memory in MiB (default as per preset) (integer value)         | No       | `'as per preset'` |
| `disk`        | disk size in GiB (default as per preset) (integer value)      | No       | `'as per preset'` |
| `version`     | crc version (default latest) (string value)                   | No       | `'latest'`        |

#### Example
- https://github.com/praveenkumar/simple-go-server/blob/main/.github/workflows/crc_linux.yaml
