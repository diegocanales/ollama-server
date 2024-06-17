# Ollama - OpenWeb UI server

This project uses Docker Compose to manage two services: `ollama` and `open-webui`.

## Run

- Optional

```bash
mkdir -p services/ollama services/open-webui
```

```bash
docker compose up -d
```

If is first run

```bash
docker exec -it ollama bash
ollama pull llama3
```
