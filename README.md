## 👋 Welcome to photoprism 🚀

AI-powered photo management with face recognition

## 📋 Description

AI-powered photo management with face recognition

## 🚀 Services

- **photoprism**: photoprism/photoprism:latest

### Infrastructure Components

- **photoprism-db**: Mariadb database


## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/photoprism/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/photoprism" ~/.local/srv/docker/photoprism
cd ~/.local/srv/docker/photoprism
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install photoprism
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_ADMIN_USER=admin
APP_ADMIN_PASS=changeme_admin_password
DB_CREATE_DATABASE_NAME=photoprism
DB_USER_NAME=photoprism
DB_USER_PASS=changeme_db_password
EMAIL_SERVER_HOST=172.17.0.1
EMAIL_SERVER_PORT=587
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:2342

## 📂 Volumes

- `./rootfs/data/photoprism/originals` - Data storage
- `./rootfs/data/photoprism/storage` - Data storage
- `./rootfs/data/photoprism/import` - Data storage
- `./rootfs/data/db/mariadb/photoprism` - Data storage

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose logs -f photoprism
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
