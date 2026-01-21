# PhotoPrism

PhotoPrism is an AI-powered photo management application for the decentralized web. It uses advanced machine learning to automatically tag and organize your photos, with support for browsing, searching, and sharing your personal photo collection.

## Features

- **AI-Powered Tagging**: Automatic classification and tagging using TensorFlow
- **Face Recognition**: Identify and group photos by people
- **Geolocation**: Browse photos on interactive maps
- **Timeline View**: Chronological browsing with smooth scrolling
- **Advanced Search**: Search by location, date, color, category, and more
- **RAW Support**: Full support for RAW image formats from major camera brands
- **Live Photos**: Support for Apple Live Photos and Google Motion Photos
- **WebDAV**: Access photos via WebDAV protocol
- **Multi-User**: Support for multiple user accounts (Plus edition)
- **Mobile Apps**: Progressive web app with offline support

## Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/photoprism/main/docker-compose.yaml" | docker compose -f - up -d
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

## Configuration

### Environment Variables

**Admin Account:**
- `APP_ADMIN_USER`: Admin username (default: admin)
- `APP_ADMIN_PASS`: Admin password (default: changeme_admin_password)

**Database:**
- `DB_USER_NAME`: Database username (default: photoprism)
- `DB_USER_PASS`: Database password (default: changeme_db_password)
- `DB_CREATE_DATABASE_NAME`: Database name (default: photoprism)

**Email (SMTP):**
- `EMAIL_SERVER_HOST`: SMTP server (default: 172.17.0.1)
- `EMAIL_SERVER_PORT`: SMTP port (default: 587)
- `EMAIL_SERVER_LOGIN_NAME`: SMTP username
- `EMAIL_SERVER_LOGIN_PASS`: SMTP password

### Photo Directories

- `./rootfs/data/photoprism/originals`: Your original photos (read-only recommended)
- `./rootfs/data/photoprism/import`: Import queue directory
- `./rootfs/data/photoprism/storage`: Sidecar files, thumbnails, cache

### Hardware Acceleration

**TensorFlow GPU Support:**
```yaml
photoprism:
  image: photoprism/photoprism:latest-gpu
  runtime: nvidia
  environment:
    - NVIDIA_VISIBLE_DEVICES=all
```

### Ports

- `2342`: Web interface

## Initial Setup

1. Access PhotoPrism at `http://localhost:2342`
2. Login with admin credentials
3. Go to Settings to configure:
   - Library settings and indexing options
   - Upload settings
   - Feature settings (face recognition, places)
4. Start initial indexing: Library > Index
5. Import photos from import folder if needed
6. Configure face recognition and review suggestions

## Photo Import Methods

### 1. Copy to Originals
Directly copy photos to `./rootfs/data/photoprism/originals` then index

### 2. Import Folder
Place photos in `./rootfs/data/photoprism/import` and use Import feature

### 3. WebDAV
Access via WebDAV at `http://localhost:2342/originals/` and upload

### 4. Web Upload
Upload directly through web interface

## Security Recommendations

- **Change Defaults**: Update admin password immediately
- **HTTPS**: Use reverse proxy with SSL/TLS
- **Read-Only Originals**: Mount originals as read-only after initial import
- **Network Access**: Restrict access with firewall rules
- **API Keys**: Protect any generated API keys
- **Backups**: Regular backups of database and storage
- **Updates**: Keep PhotoPrism updated for security patches

## Backup

Critical directories to backup:
- `./rootfs/db/mariadb/photoprism`: Database with metadata and tags
- `./rootfs/data/photoprism/storage`: Thumbnails and sidecar files
- `./rootfs/data/photoprism/originals`: Your original photos (primary backup)

## Advanced Features

### Face Recognition
1. Enable in Settings > Features
2. Go to People section
3. Review and name detected faces
4. PhotoPrism will learn and improve recognition

### Places
Browse photos by location on interactive maps. Requires photos with GPS data.

### Albums
Create albums manually or automatically based on:
- Date ranges
- Location
- Tags and keywords
- People

### Sharing
Share individual photos or entire albums with optional password protection.

## Troubleshooting

### Indexing Issues
- Check storage space availability
- Review logs: `docker compose logs photoprism`
- Verify file permissions
- Try re-indexing: Library > Index > Complete Rescan

### Face Recognition Not Working
- Enable feature in Settings > Features
- Allow time for initial processing
- Verify sufficient CPU/RAM resources

### Photos Not Appearing
- Ensure indexing has completed
- Check file formats are supported
- Verify originals directory permissions
- Review import logs

### Performance Issues
- Increase MariaDB buffer pool size
- Enable GPU acceleration if available
- Use SSD for storage directory
- Increase container memory limits

## Performance Optimization

- **Storage**: Use SSD for thumbnails and database
- **RAM**: Allocate at least 4GB for larger libraries
- **CPU**: More cores = faster indexing
- **GPU**: Enable for faster TensorFlow operations
- **Database**: Tune MariaDB settings for your workload

## Documentation

- Official Documentation: https://docs.photoprism.app/
- GitHub: https://github.com/photoprism/photoprism
- Community Forum: https://community.photoprism.app/
- Demo: https://demo.photoprism.app/

## License

PhotoPrism is licensed under the GNU AGPL v3. Plus features require a membership.
