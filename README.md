# AWS Mgmt

## Running the application locally

### Requirements

A Docker environment is provided and requires you to have these tools available:

 * Docker
 * pipenv (see [these instructions](https://pipenv.readthedocs.io/en/latest/install/) for how to install)

Install and run `pipenv` to install the required tools:

```bash
pipenv install
```

You can configure your current shell to be able to use fabric commands directly
(without having to prefix everything by `pipenv run`)

```bash
pipenv shell
```

### Docker environment

The Docker infrastructure provides a web stack with:
 - NGINX
 - PostgreSQL
 - PHP
 - Traefik
 - A container with some tooling:
   - Composer
   - Node
   - Yarn / NPM

### Domain configuration (first time only)

Before running the application for the first time, ensure your domain names
point the IP of your Docker daemon by editing your `/etc/hosts` file.

This IP is probably `127.0.0.1` unless you run Docker in a special VM (docker-machine, dinghy, etc).

Note: The router binds port 80 and 443, that's why it will work with `127.0.0.1`

```
echo '127.0.0.1 <your hostnames>' | sudo tee -a /etc/hosts
```

Using dinghy? Run `dinghy ip` to get the IP of the VM.

### Starting the stack

Launch the stack by running this command:

```bash
fab start
```

> Note: the first start of the stack should take a few minutes.

The site is now accessible at the hostnames your have configured over HTTPS
(you may need to accept self-signed SSL certificate).

### Builder

Having some composer, yarn or another modifications to make on the project?
Start the builder which will give you access to a container with all these
tools available:

```bash
fab builder
```

Note: You can add as many fabric command as you want. But the command should be
ran by the builder, don't forget to add `@with_builder` annotation to the
function.

### Other tasks

Checkout `fab -l` to have the list of available fabric tasks.
