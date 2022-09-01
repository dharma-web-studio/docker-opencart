<h1 align="center">dharmawebstudio/docker-opencart</h1>
<div align="center">
  <p>Dharma Web Studio's Docker Configuration for OpenCart 4, intended to be used only as a Docker-based development environment</p>
  <img src="https://img.shields.io/badge/opencart-4.0.1.0-blue" alt="Supported OpenCart Versions" />
  <a href="https://opensource.org/licenses/MIT" target="_blank"><img src="https://img.shields.io/badge/license-MIT-blue.svg" /></a>
</div>

## Prerequisites

This setup assumes you are running Docker on a computer with at least 2GB of RAM allocated to Docker, a dual-core, and an SSD hard drive. [Download & Install Docker Desktop](https://www.docker.com/products/docker-desktop).

This configuration has been tested on Mac & Linux.

## Usage

### Quick Setup
```
git clone https://github.com/dharmawebstudio/docker-opencart.git ./
bin/install
open https://opencart.docker
```

### Extension Development

- Create a directory in "extension"
```
mkdir extension/name-of-the-extension
```
- In docker-compose.yml, remove the comment in the line, and replace the string 'name-of-the-extension', with the recently created directory name 
```
# - ./extension/name-of-extension:/var/www/html/extension/name-of-extension
```
- Recreates the container to mount a volume in the container, which will contain the extension directory in localhost
```
bin/up
```

## Testing Suite and Quality Control

### Detect and fix violations according [OpenCart Coding Standards](https://github.com/opencart/opencart/wiki/Coding-standards) using [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)

PHP_CodeSniffer tokenizes PHP, JavaScript and CSS files to detect and fix violations of a defined set of coding standards.

In order to execute these tests in the container, first is required to install via [Composer](https://getcomposer.org/) some development dependencies:
```
bin/install-composer-dev-dependencies
```

There is a file, which contains an example of coding standard based on [this document](https://github.com/opencart/opencart/wiki/Coding-standards) from OpenCart documentation.  
```
mv tests/phpcs/phpcs.xml.example tests/phpcs/phpcs.xml
```

Execute bin over the files of your extension 
```
bin/phpcs extension/tabs-with-products
```



## Custom CLI Commands

- `bin/bash`: Drop into the bash prompt of your Docker container. The `app` container should be mainly used to access the filesystem within Docker.
- `bin/cli`: Run any CLI command without going into the bash prompt.
- `bin/clinotty`: Run any CLI command with no TTY.
- `bin/composer`: Allow an user modify the compose file, which is located in storage/ directory from OpenCart.
- `bin/copyfromcontainer`: Copy folders or files from container to host.
- `bin/copytocontainer`: Copy folders or files from host to container.
- `bin/fixowns`: This will fix filesystem ownerships within the container.
- `bin/install`: This will run all actions need it to build, start containers the first time, and install OpenCart in them.
- `bin/install-composer-dev-dependencies`: This will install in the container development dependencies
- `bin/mv-admin`: Move, rename and update admin directory constant in config file
- `bin/mv-storage`: Move, rename and update storage directory constant in config file
- `bin/restart`: Stop and then start all containers.
- `bin/root`: Run any CLI command as root without going into the bash prompt.
- `bin/rootnotty`: Run any CLI command as root with no TTY.
- `bin/setup-domain`: Setup OpenCart domain name.
- `bin/setup-ssl`: Generate an SSL certificate for one or more domains.
- `bin/setup-ssl-ca`: Generate a certificate authority and copy it to the host.
- `bin/start`: Start all containers, good practice to use this instead of `docker-compose up -d`, as it may contain additional helpers.
- `bin/status`: Check the container status.
- `bin/stop`: Stop all project containers.
- `bin/up`: Builds, (re)creates, starts, and attaches to containers for a service. Good practice to use this instead of `docker-compose up -d`, as it may contain additional helpers.
- `bin/xdebug`: Disable or enable Xdebug. Accepts params `disable`, `enable`, `status`, or `toggle`.
