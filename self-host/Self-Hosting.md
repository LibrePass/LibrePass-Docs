# Self-hosting LibrePass

LibrePass is an open source project and allows anyone to create their own server for their own needs.

## Dependencies

- [Docker and docker compose](https://docs.docker.com/engine/install/)

## Steps

### 1. Setup environment variables

Create a `.env` file using the following [template](https://github.com/LibrePass/LibrePass-Server/blob/main/.env.schema)

### 2. Setup docker configuration

Create a `docker-compose.yml` file using the following [template](https://github.com/LibrePass/LibrePass-Server/blob/main/docker-compose.yml)

### 3. Start the server

```bash
sudo docker compose up

# or if you using an older docker version, use the `docker-compose` command instead
sudo docker-compose up
```

### 4. Update the server version

> [!NOTE]
> Do not forget to update the server version regularly.

```bash
# Download the latest version
sudo docker compose pull
# Restart the server
sudo docker compose up

# or if you using an older docker version, use the `docker-compose` command instead
sudo docker-compose pull
sudo docker-compose up
```
