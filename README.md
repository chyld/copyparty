# Copyparty

A Dockerized deployment of [copyparty](https://github.com/9001/copyparty), a portable file server with thumbnailing, search, and media playback.

## Overview

This runs copyparty inside a Debian Trixie container with ffmpeg and Python image processing libraries (Pillow, pyvips, rawpy, pillow-heif) for thumbnail generation and media handling. The server listens on port **3923**.

## Data Layout

| Path | Purpose |
|---|---|
| `~/data/copyparty/party` | Shared files |
| `~/data/copyparty/hist` | Database, thumbnails, metadata |

Both are bind-mounted into the container at `/data`.

## Accounts

Defined in `party.conf`:

- **u1** / p1 — no volume access by default
- **u2** / p2 — no volume access by default
- **u3** / p3 — read/write access to `/Party`

## Usage

```bash
# Build the image
./build.sh

# Start the server
./start.sh

# View logs
docker logs copyparty --follow

# Stop the server
./stop.sh
```

Access the UI at `https://localhost:3923` (HTTPS is recommended for speed).

## Configuration

Edit `party.conf` to add accounts, change permissions, or mount additional volumes. See the [copyparty docs](https://github.com/9001/copyparty#readme) for all available options.
