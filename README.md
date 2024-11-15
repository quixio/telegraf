# Custom Telegraf Docker Image for quix-samples

This Docker image is used primarily in the [quix-samples](https://github.com/quixio/quix-samples) repository. It is a custom build of [Telegraf](https://github.com/influxdata/telegraf), a popular server agent for collecting and reporting metrics. This image extends the official Telegraf image by adding a custom output plugin and configuration tailored to publish to [Quix Cloud](https://quix.io).

## Image Details

### Build Process

The Dockerfile defines a multi-stage build process to compile a custom version of Telegraf with additional plugins.

1. **Builder Stage**:
    - Starts with a Golang Alpine image for a lightweight, compatible build environment.
    - Installs required dependencies (`git` and `make`).
    - Clones the official Telegraf repository from GitHub.
    - Copies custom plugin code into the `outputs` directory within Telegraf’s source.
    - Builds Telegraf, creating an executable with the added plugin.

2. **Final Stage**:
    - Starts with the official Telegraf image.
    - Copies the Telegraf binary with the custom plugin from the builder stage.
    - Adds a custom Telegraf configuration file (`telegraf.conf`).
    - Sets the default command to run Telegraf with the specified configuration.

### Key Components

- **Custom Plugin**: The `outputs` plugin added to Telegraf enables it to export metrics in ways specific to the requirements of the `quix-samples` environment.
- **Configuration**: `telegraf.conf` defines how metrics are collected, processed, and outputted. Modify this file to change data collection sources or output behaviors.