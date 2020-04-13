# Traefik 2 + Let’s Encrypt + Docker Compose 

## Testing on Local PC

### Step 1: Make Sure You Have Required Dependencies

- Git
- Docker
- Docker Compose


### Step 2: Clone the Repository

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
```

### Step 4: Set Your Own Password

If you're curious about HTTP basic auth and how it can be used with Traefik, you can read [the full post](https://bubelov.com/blog/basic-auth-reverse-proxy/). Here is the excerpt and it assumes you already installed `htpasswd`:

```bash
htpasswd -nBC 10 admin

New password:
Re-type new password:

admin:$2y$10$zi5n43jq9S63gBqSJwHTH.nCai2vB0SW/ABPGg2jSGmJBVRo0A.ni
```

The resulting format is quite straighforward: `username`:`hashedPassword`. The username doesn't have to be `admin`, feel free to change it.

You can paste the username into the `TRAEFIK_USER` environment variable. The other part, `hashedPassword`, should be assigned to `TRAEFIK_PASSWORD_HASH`. Now you have your own `username`:`password` pair.

### Step 5: Launch Your Deployment

```bash
cd ~/traefik-letsencrypt-compose
docker-compose up -d
```

### Step 6: Test Your Deployment

```bash
sudo nano /etc/hosts
```

```
127.0.0.1       example.local
127.0.0.1       traefik.example.local
```

## Deploying on a Public Server With Real Domain

Let's say you have a domain `example.com` and it's DNS records point to your production server. Just repeat the local deployment steps but don't forget to set the `DOMAIN` environment variable with your real domain. In case of `example.com`, your `.env` file should have the following line:

```bash
DOMAIN=example.com
```

You should also uncomment the following lines inside `docker-compose.yml` in order to use Let’s Encrypt to generate a trusted certificate instead of self-signed one that we used for local deployment:

```bash
#traefik.http.routers.traefik-https.tls.certresolver=letsencrypt
```
