# Traefik 2 + Let’s Encrypt + Docker Compose 

## Deployment Instructions

### Step 1: Make Sure You Have Required Dependencies

- Git
- Docker
- Docker Compose


### Step 2: Clone the Repo

```bash
git clone git@github.com:bubelov/traefik-letsencrypt-compose.git
```

### Step 3: Add Environment Variables

```bash
nano traefik-letsencrypt-compose/.env
```

```bash
DOMAIN=example.local
EMAIL=admin@example.local
TRAEFIK_USER=admin
TRAEFIK_PASSWORD_HASH=$2y$10$zi5n43jq9S63gBqSJwHTH.nCai2vB0SW/ABPGg2jSGmJBVRo0A.ni # admin

# Uncomment to get a trusted certificate in production
# HTPPS_CERTIFICATE_RESOLVER=letsencrypt
```

### Step 4: Launch Your Deployment

```bash
cd ~/traefik-letsencrypt-compose
docker-compose up -d
```

## Testing Deployment on Local PC

```bash
sudo nano /etc/hosts
```

```
127.0.0.1       example.local
127.0.0.1       traefik.example.local
```
