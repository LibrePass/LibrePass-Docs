# Self-Hosting Server

LibrePass, an open-source password manager, empowers you to take charge of your data by self-hosting it on your own server.
This approach grants you complete privacy and eliminates dependence on third-party services.

## Before you begin

- **Technical knowledge**: This guide assumes some familiarity with Docker and terminal commands.
- **Security**: Self-hosting requires managing your server's security. Ensure you understand the risks and how to mitigate them.


## Requirements

- A server running Linux (amd64 or arm64)
- [Docker and Docker Compose](https://docs.docker.com/engine/install/) installed on your server

## Steps

### Prepare Environment Variables

Create a file named `.env` in your LibrePass directory. You can use the following [template](https://github.com/LibrePass/LibrePass-Server/blob/main/.env.schema).
 
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

### Set Up Docker Configuration

Create a file named `docker-compose.yml` in your LibrePass directory. Use the following [template](https://github.com/LibrePass/LibrePass-Server/blob/main/docker-compose.yml).

### Launch Server

```bash
sudo docker compose up -d

# or if you using an older docker version, use the `docker-compose` command instead
sudo docker-compose up -d
```

The `-d` flag runs the container in detached mode, allowing you to exit the terminal without stopping LibrePass.

### Update Server

!!! note
    Do not forget to update the server version regularly.

To keep your server secure, it's crucial to update LibrePass regularly. Run these commands in your terminal:

```bash
# Download the latest version
sudo docker compose pull
# Restart the server
sudo docker compose up -d

# or if you using an older docker version, use the `docker-compose` command instead
sudo docker-compose pull
sudo docker-compose up -d
```

## Addional Tips

- **Backups** - Regularly back up your LibrePass database for disaster recovery.
- **Security** - Consider implementing additional security measures like firewalls for your server.

By following these steps, you'll have a self-hosted LibrePass server up and running, giving you complete control over your passwords!
