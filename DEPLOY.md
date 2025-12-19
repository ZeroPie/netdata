# Netdata Deployment Guide for Coolify

## Prerequisites
- Coolify instance running
- GitHub repository connected to Coolify
- Domain name (optional, can use Coolify's generated subdomain)

## Setup Steps

### 1. Push to GitHub
Push this repository (with `docker-compose.yaml` and `netdata/netdata.conf`) to your GitHub repo.

### 2. Create Service in Coolify
1. Go to your Coolify dashboard
2. Click "New Resource" → "Docker Compose"
3. Select your GitHub repository
4. Choose the branch with your netdata setup
5. Set build pack to "Docker Compose"

### 3. Configure Domain (Public Access)
1. In service settings, go to "Domains"
2. Either:
   - Use Coolify-generated domain (e.g., `netdata-xyz.coolify.io`)
   - Add your custom domain (e.g., `netdata.yourdomain.com`)
3. Coolify will automatically handle SSL certificates

### 4. Enable Basic Authentication
**IMPORTANT:** Do this before deploying!

1. In service settings, find "Basic Auth" or "Security" section
2. Toggle "Enable Basic Authentication"
3. Set username (e.g., `admin`)
4. Set a strong password
5. Save settings

### 5. Deploy
1. Click "Deploy" button
2. Wait for deployment to complete (check logs)
3. Visit your domain - you'll be prompted for username/password

## Accessing the Dashboard

Once deployed:
- Visit: `https://your-netdata-domain.com`
- Enter basic auth credentials
- You'll see the Netdata monitoring dashboard

## Security Notes

- ✅ Basic auth protects the dashboard from public access
- ✅ SSL/TLS enabled automatically via Coolify
- ✅ Netdata config optimized for minimal logging
- ⚠️  Monitor metrics may include sensitive server info - keep credentials secure

## Troubleshooting

**Dashboard not loading:**
- Check Coolify deployment logs
- Verify port 19999 is mapped correctly
- Check container is running: `docker ps`

**Can't access metrics:**
- Verify volume mounts for `/proc`, `/sys`, etc.
- Check container has required capabilities (`SYS_PTRACE`, `SYS_ADMIN`)

**High memory usage:**
- Adjust `page cache size` in `netdata/netdata.conf`
- Reduce `dbengine multihost disk space`
