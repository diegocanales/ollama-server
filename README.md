# Project Documentation

This project uses Docker Compose to manage two services: `ollama` and `open-webui`.

## Docker Compose File

The `docker-compose.yaml` file defines the configuration for the services.

### Ollama Service

The `ollama` service uses the `ollama/ollama` Docker image. The Docker tag can be specified using the `OLLAMA_DOCKER_TAG` environment variable, defaulting to `latest` if not set. The service has access to all available GPUs on the host machine. The service uses a volume named `ollama` for persistent storage, mounted at `/root/.ollama` in the container. The service is always restarted unless manually stopped.

### Open-WebUI Service

The `open-webui` service uses the `ghcr.io/open-webui/open-webui` Docker image with a specific tag (`v0.1.123-cuda`). The service depends on the `ollama` service. It exposes port 8080 inside the container as port 3000 on the host machine, but the host port can be changed using the `OPEN_WEBUI_PORT` environment variable. The service has two environment variables: `OLLAMA_BASE_URL`, which is set to `http://ollama:11434`, and `WEBUI_SECRET_KEY`, which is left empty. The service also defines an extra host `host.docker.internal` that resolves to `host-gateway`. The service uses a volume named `open-webui` for persistent storage, mounted at `/app/backend/data` in the container. The service is always restarted unless manually stopped. It also has access to all available GPUs on the host machine.

## Volumes

Two volumes are defined for persistent storage: `ollama` and `open-webui`. These volumes are used by the `ollama` and `open-webui` services, respectively.

## Running the Services

To start the services, run `docker-compose up` in the directory containing the `docker-compose.yaml` file. To stop the services, run `docker-compose down`.