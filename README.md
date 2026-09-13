# Container Setup README

## Overview
This setup uses Docker Compose to manage media-related services, including torrent management, media organization, and indexing.

## Services
### 1. **Transmission**
- **Container**: `transmission`
- **Image**: [linuxserver/transmission](https://hub.docker.com/r/linuxserver/transmission)
- **Purpose**: BitTorrent client for downloading media.
- **Ports**: `9091`, `51413`, `51413/udp`
- **Volumes**: 
  - `/config` (logs, settings)
  - `/downloads` (downloaded files)
- **Environment**: `PUID`, `PGID`, `TZ`

### 2. **Plex**
- **Container**: `plex`
- **Image**: [linuxserver/plex](https://hub.docker.com/r/linuxserver/plex)
- **Purpose**: Media server for streaming movies, TV shows, and music.
- **Network**: `host` (direct access to host network)
- **Volumes**: 
  - `/config` (Plex settings)
  - `/media` (media library)
- **Environment**: `PUID`, `PGID`, `TZ`, `VERSION`

### 3. **Radarr**
- **Container**: `radarr`
- **Image**: [linuxserver/radarr](https://hub.docker.com/r/linuxserver/radarr)
- **Purpose**: Movie manager for automatic downloads and organization.
- **Ports**: `7878`
- **Volumes**: 
  - `/config` (Radarr settings)
  - `/movies` (movie library)
  - `/downloads` (incoming files)
- **Environment**: `PUID`, `PGID`, `TZ`

### 4. **Sonarr**
- **Container**: `sonarr`
- **Image**: [linuxserver/sonarr](https://hub.docker.com/r/linuxserver/sonarr)
- **Purpose**: TV show manager for automatic downloads and organization.
- **Ports**: `8989`
- **Volumes**: 
  - `/config` (Sonarr settings)
  - `/tv` (TV show library)
  - `/downloads` (incoming files)
- **Environment**: `PUID`, `PGID`, `TZ`

### 5. **Jackett**
- **Container**: `jackett`
- **Image**: [linuxserver/jackett](https://hub.docker.com/r/linuxserver/jackett)
- **Purpose**: Torrent indexer for searching and managing torrents.
- **Ports**: `9117`
- **Volumes**: 
  - `/config` (Jackett settings)
  - `/downloads` (incoming files)
- **Environment**: `PUID`, `PGID`, `TZ`

### 6. **Bazarr**
- **Container**: `bazarr`
- **Image**: [linuxserver/bazarr](https://hub.docker.com/r/linuxserver/bazarr)
- **Purpose**: Subtitle manager for automated subtitle downloads.
- **Ports**: `6767`
- **Volumes**: 
  - `/config` (Bazarr settings)
  - `/movies` (movie library)
  - `/tv` (TV show library)
- **Environment**: `PUID`, `PGID`, `TZ`

## Common Environment Variables
- `PUID`: User ID for container permissions.
- `PGID`: Group ID for container permissions.
- `TZ`: Time Zone (e.g., `Europe/Warsaw`).

## Notes
- All containers use `/config` for persistent settings.
- Media libraries are stored in `/media` (Plex), `/movies` (Radarr/Bazarr), and `/tv` (Sonarr/Bazarr).
- Ensure proper permissions for host directories before starting containers.