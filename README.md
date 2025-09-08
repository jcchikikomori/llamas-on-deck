# Llamas on Deck

This project provides a simple Docker Compose setup for running [Open WebUI](https://github.com/open-webui/open-webui) and [Portainer](https://www.portainer.io/) for easy web-based management of LLMs and Docker containers.

## Intended Purpose

Llamas on Deck is designed to help you set up and manage Large Language Models (LLMs) on your Steam Deck without replacing or modifying the default Steam OS. It leverages Docker to keep your system clean and isolated, making it easy to run LLMs alongside your existing setup.

## Services

- **Open WebUI**
  - A user-friendly web interface for interacting with LLMs.
  - Accessible at: <http://localhost:3000>
  - Data persists in Docker volume `open-webui`.

- **Ollama**
  - Local model runtime used by Open WebUI.
  - API exposed at: <http://localhost:11434>
  - Data persists in Docker volume `ollama_data`.

- **SearXNG**
  - Privacy‑respecting meta search engine used for Open WebUI web search.
  - Accessible at: <http://localhost:8888>
  - Public URL can be set via `.env` as `SEARXNG_PUBLIC_URL` (e.g., `https://search.example.com/`).
  - Open WebUI talks to it over the internal Docker network, independent of the public URL.

- **Portainer**
  - A lightweight management UI for Docker.
  - Accessible at: <https://localhost:9443>
  - Tunnel server available at port `8000`.
  - Requires access to the Docker socket (not rootless).

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed
- [Docker Compose](https://docs.docker.com/compose/install/) installed

> Note: This setup is not configured for Docker rootless mode. It requires access to `/var/run/docker.sock`.

## Usage

### Clone this repository

```sh
git clone <this-repo-url>
cd llamas-on-deck
```

### Clear existing ones

```sh
docker compose down --rmi=all --volumes
```

### Start the services

```sh
docker compose up -d
```

### Access the UIs

- Open WebUI: <http://localhost:3000>
- Portainer: <https://localhost:9443>
- SearXNG (public): <http://localhost:8888>

### Stop the services

```sh
docker compose down
```

## Volumes

- `open-webui`: Persists Open WebUI data
- `ollama_data`: Persists Ollama models and configs
- `searxng_data`: Persists SearXNG configuration
- `portainer_data`: Persists Portainer configuration

## Web Search (Open WebUI + SearXNG)

- Web search is enabled in Open WebUI (`ENABLE_WEB_SEARCH=True`).
- Open WebUI connects to SearXNG internally at `http://searxng:8080`.
- To expose SearXNG on the Internet, set a proper `SEARXNG_PUBLIC_URL` in `.env` to your domain (e.g., `https://search.example.com/`) and ensure port `8888` is reachable or place SearXNG behind your reverse proxy.

## Security

Portainer is exposed on HTTPS (9443) but uses self-signed certificates by default.
The Docker socket is mounted into the Portainer container, so only trusted users should have access.

## License

See individual project licenses for Open WebUI and Portainer.
