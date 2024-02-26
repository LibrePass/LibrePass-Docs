# Self-hosting LibrePass

LibrePass is an open source project and allows anyone to create their own server for their own needs.

## Dependencies

- [Docker and Docker Compose](https://docs.docker.com/engine/install/)

## Steps

### 1. Setup environment variables

Create a `.env` file using the following [template](https://github.com/LibrePass/LibrePass-Server/blob/main/.env.schema)

#### Variables

- `PORT` - The port number on which the application listens for incoming requests.
- `API_DOMAIN` - The domain on which the API is hosted (e.g. api.librepass.org).
- `CORS_ALLOWED_ORIGINS` - The domains from which requests to the API can be called (required for the website), separated by a comma (e.g. https://librepass.org,https://example.librepass.org).
- `RATE_LIMIT_ENABLED` - Whether to rate-limit requests to the API (default true).
- `HTTP_IP_HEADER` -Header with the user's IP address if a proxy is used. (e.g. `CF-Connecting-IP` for cloudflare proxy, `X-Forwarded-For` for nginx, caddy, etc.)
- `LOG_FILE` - The filename of the server logs file.
- `WEB_URL` - The URL of the LibrePass website. (e.g. https://librepass.org)
- `POSTGRES_HOST` - The hostname or IP address of the PostgreSQL database server. The default is postgres if using docker-compose.
- `POSTGRES_PORT` - The port number on which the PostgreSQL database server listens for connections. The default is 5432.
- `POSTGRES_DB` - The name of the database used by LibrePass within the PostgreSQL server.
- `POSTGRES_USER` - The username for accessing the LibrePass database in PostgreSQL.
- `POSTGRES_PASSWORD` - The password for the POSTGRES_USER to connect to the LibrePass database.
- `DATABASE_URI` - A connection string constructed dynamically from the previous database settings. This string is used by the application to connect to the PostgreSQL database.
- `MAIL_SMTP` - The hostname or IP address of the SMTP server used for sending email notifications. The default value is example.com (replace with your actual server).
- `MAIL_SMTP_PORT` - The port number on which the SMTP server accepts connections. The default is 465.
- `MAIL_SMTP_AUTH` - Whether authentication is required to connect to the SMTP server. Set it to true if your server requires authentication.
- `MAIL_SMTP_USERNAME` - The username to authenticate with the SMTP server if MAIL_SMTP_AUTH is set to true.
- `MAIL_SMTP_PASSWORD` - The password to authenticate with the SMTP server if MAIL_SMTP_AUTH is set to true.
- `MAIL_SMTP_TLS_ENABLED` - Whether to use TLS encryption for communication with the SMTP server. Set it to true for secure email delivery.
- `SMTP_EMAIL_ADDRESS` - The email address used as the "from" address for sending email notifications from the application.

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
