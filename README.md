# Example of prebuilt Codespace using Docker Compose

This is a minimal example showing one way to set up GitHub Codespaces for a web app project that uses [a custom Dockerfile](web/Dockerfile) and [a Docker Compose configuration](docker-compose.yml).

## Setup

In the [Dev Container configuration](.devcontainer/devcontainer.json), key things to note are:

* Specifying a path to the docker-compose.yml file relative to the `.devcontainer` directory:

```json
  "dockerComposeFile": "../docker-compose.yml",
```

* Setting the `service` property to [the name of the service in the `docker-compose.yml` file that you want to use as the development container](docker-compose.yml#L24):

```json
  "service": "dev",
```

* Setting the `workspaceFolder` property to the same path used in the [`Dockerfile`](web/Dockerfile#L3) and in [`docker-compose.yml`]() as the root of the project:

```json
  "workspaceFolder": "/app",
```

* Specifying a port to forward:

```json
  "forwardPorts": [5000],
```

* Using the ["Docker outside of Docker" feature](https://github.com/devcontainers/features/blob/main/src/docker-outside-of-docker/README.md) to allow the development container to run Docker commands connected to the host machine's Docker daemon:

```json
"features": {
  "ghcr.io/devcontainers/features/docker-outside-of-docker": {}
}
```

## Developer experience

When a developer opens this repository in a Codespace:

1. All the services specified in the Docker Compose config will be started up (using a prebuilt Codespace snapshot if available).
2. VS Code will connect to the `dev` service.
3. The forwarded port will automatically appear in the Ports view in VS Code.
