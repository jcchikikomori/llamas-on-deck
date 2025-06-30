# Llamas on Deck

This project provides a simple Docker Compose setup for running [Open WebUI](https://github.com/open-webui/open-webui) and [Portainer](https://www.portainer.io/) for easy web-based management of LLMs and Docker containers.

**Intended Purpose:**  
Llamas on Deck is designed to help you set up and manage Large Language Models (LLMs) on your Steam Deck without replacing or modifying the default Steam OS. It leverages Docker to keep your system clean and isolated, making it easy to run LLMs alongside your existing setup.

## Services

- **Open WebUI**  
  A user-friendly web interface for interacting with LLMs.  
  - Accessible at: [http://localhost:3000](http://localhost:3000)
  - Data is persisted in a Docker volume (`open-webui`).

- **Portainer**  
  A lightweight management UI for Docker.  
  - Accessible at: [https://localhost:9443](https://localhost:9443)  
  - Tunnel server available at port 8000.
  - Requires access to the Docker socket (runs in privileged mode, not rootless).

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed
- [Docker Compose](https://docs.docker.com/compose/install/) installed

> **Note:** This setup is not configured for Docker rootless mode. It requires access to `/var/run/docker.sock`.

## Usage

### Clone this repository

```sh
git clone <this-repo-url>
cd llamas-on-deck
```

### Start the services

```sh
docker compose up -d
```

### Access the UIs

Open WebUI: http://localhost:3000

Portainer: https://localhost:9443

### Stop the services

```sh
docker compose down
```

## Volumes

open-webui: Persists Open WebUI data
portainer_data: Persists Portainer configuration

## Security

Portainer is exposed on HTTPS (9443) but uses self-signed certificates by default.
The Docker socket is mounted into the Portainer container, so only trusted users should have access.

## License

See individual project licenses for Open WebUI and Portainer.
