<h1 align="center">dharmawebstudio/docker-opencart</h1>
<div align="center">
  <p>Dharma Web Studio's Docker Configuration for OpenCart</p>
  <img src="https://img.shields.io/badge/opencart-4.0.0.0-blue" alt="Supported OpenCart Versions" />
  <a href="https://opensource.org/licenses/MIT" target="_blank"><img src="https://img.shields.io/badge/license-MIT-blue.svg" /></a>
</div>

## Usage

This configuration is intended to be used as a Docker-based development environment for OpenCart 4.

## Prerequisites

This setup assumes you are running Docker on a computer with at least 2GB of RAM allocated to Docker, a dual-core, and an SSD hard drive. [Download & Install Docker Desktop](https://www.docker.com/products/docker-desktop).

This configuration has been tested on Mac & Linux.

## Custom CLI Commands

- `bin/bash`: Drop into the bash prompt of your Docker container. The `app` container should be mainly used to access the filesystem within Docker.
- `bin/cli`: Run any CLI command without going into the bash prompt.
- `bin/clinotty`: Run any CLI command with no TTY.
- `bin/copyfromcontainer`: Copy folders or files from container to host.
- `bin/copytocontainer`: Copy folders or files from host to container.
- `bin/fixowns`: This will fix filesystem ownerships within the container.
- `bin/restart`: Stop and then start all containers.
- `bin/root`: Run any CLI command as root without going into the bash prompt.
- `bin/rootnotty`: Run any CLI command as root with no TTY.
- `bin/setup`: Run the OpenCart setup process to build, create, starts containers, install OpenCart from the source code, with optional domain name. Defaults to `opencart.docker`.
- `bin/setup-domain`: Setup OpenCart domain name.
- `bin/setup-ssl`: Generate an SSL certificate for one or more domains.
- `bin/setup-ssl-ca`: Generate a certificate authority and copy it to the host.
- `bin/start`: Start all containers, good practice to use this instead of `docker-compose up -d`, as it may contain additional helpers.
- `bin/status`: Check the container status.
- `bin/stop`: Stop all project containers.
- `bin/up`: Builds, (re)creates, starts, and attaches to containers for a service. Good practice to use this instead of `docker-compose up -d`, as it may contain additional helpers.
- `bin/xdebug`: Disable or enable Xdebug. Accepts params `disable`, `enable`, `status`, or `toggle`.
