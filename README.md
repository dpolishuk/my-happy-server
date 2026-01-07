# Happy Server

Minimal backend for open-source end-to-end encrypted Claude Code clients.

## What is Happy?

Happy Server is the synchronization backbone for secure Claude Code clients. It enables multiple devices to share encrypted conversations while maintaining complete privacy - the server never sees your messages, only encrypted blobs it cannot read.

## Features

- 🔐 **Zero Knowledge** - The server stores encrypted data but has no ability to decrypt it
- 🎯 **Minimal Surface** - Only essential features for secure sync, nothing more  
- 🕵️ **Privacy First** - No analytics, no tracking, no data mining
- 📖 **Open Source** - Transparent implementation you can audit and self-host
- 🔑 **Cryptographic Auth** - No passwords stored, only public key signatures
- ⚡ **Real-time Sync** - WebSocket-based synchronization across all your devices
- 📱 **Multi-device** - Seamless session management across phones, tablets, and computers
- 🔔 **Push Notifications** - Notify when Claude Code finishes tasks or needs permissions (encrypted, we can't see the content)
- 🌐 **Distributed Ready** - Built to scale horizontally when needed

## How It Works

Your Claude Code clients generate encryption keys locally and use Happy Server as a secure relay. Messages are end-to-end encrypted before leaving your device. The server's job is simple: store encrypted blobs and sync them between your devices in real-time.

## Hosting

**You don't need to self-host!** Our free cloud Happy Server at `happy-api.slopus.com` is just as secure as running your own. Since all data is end-to-end encrypted before it reaches our servers, we literally cannot read your messages even if we wanted to. The encryption happens on your device, and only you have the keys.

That said, Happy Server is open source and self-hostable if you prefer running your own infrastructure. The security model is identical whether you use our servers or your own.

## Self-Hosting

### Requirements

- Linux server (Ubuntu 22.04+ recommended)
- Docker and Docker Compose
- Domain name with DNS pointing to your server
- Caddy (for HTTPS) - or bring your own reverse proxy

### Quick Deploy

```bash
git clone https://github.com/slopus/happy-server.git
cd happy-server
./deploy.sh
```

The interactive script will:
1. Detect your environment (Docker, Caddy, existing data)
2. Prompt for your domain name
3. Configure PostgreSQL, Redis, and MinIO
4. Build and start the application
5. Set up HTTPS via Caddy
6. Verify the deployment

### What Gets Deployed

- **App** - Node.js server on port 3005
- **PostgreSQL** - Database for user data and sessions
- **Redis** - Event bus and caching
- **MinIO** - S3-compatible storage for encrypted blobs
- **Caddy** - Automatic HTTPS with Let's Encrypt

### Environment Variables

The deploy script creates a `.env` file automatically. Key settings:

| Variable | Description |
|----------|-------------|
| `DOMAIN` | Your domain name |
| `DATABASE_URL` | PostgreSQL connection string |
| `REDIS_URL` | Redis connection string |
| `MINIO_ENDPOINT` | MinIO S3 endpoint |

### Manual Operations

```bash
# View logs
docker compose logs -f app

# Restart services
docker compose restart app

# Stop everything
docker compose down

# Update and redeploy
git pull && ./deploy.sh
```

## License

MIT - Use it, modify it, deploy it anywhere.