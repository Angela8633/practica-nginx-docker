# Practica: Nginx con Docker, Docker Hub y Render

Este proyecto levanta un servidor web Nginx local usando Docker Compose. Tambien incluye un workflow de GitHub Actions para crear la imagen Docker, subirla a Docker Hub y desplegarla en Render.

## Ejecutar

```bash
docker compose up -d --build
```

Luego abrir:

```text
http://localhost:8080
```

## Detener

```bash
docker compose down
```

## GitHub Actions

El archivo `.github/workflows/deploy.yml` automatiza:

- Crear la imagen Docker de la aplicacion.
- Subir la imagen a Docker Hub.
- Ejecutar un despliegue en Render usando la API.

## Secretos requeridos en GitHub

En GitHub, entrar a `Settings > Secrets and variables > Actions > New repository secret` y crear:

```text
DOCKERHUB_USERNAME
DOCKERHUB_TOKEN
RENDER_API_KEY
RENDER_SERVICE_ID
```

`DOCKERHUB_TOKEN` se crea en Docker Hub como Access Token.

`RENDER_API_KEY` se crea en Render desde Account Settings.

`RENDER_SERVICE_ID` es el ID del servicio web en Render, por ejemplo `srv-xxxxxxxx`.

## Imagen Docker Hub

El workflow publica la imagen con este formato:

```text
docker.io/DOCKERHUB_USERNAME/practica-nginx-docker:latest
```

En Render, el servicio debe estar configurado como Docker/Image service usando esa misma imagen.
