# Nginx multi websites Production-Ready Setup Project

## Project Overview
This project implements a complete nginx setup with:
- Multiple websites
- Load-balanced backend services
- Security configurations
- Monitoring setup
- SSL/TLS configuration

### Components:
1. **Main Corporate Website** - example.com
2. **API Gateway** - api.example.com
3. **Admin Interface** - admin.example.com (or dashboard.example.com)
4. **Load-Balanced Backend Servers** - app.example.com
5. **Monitoring Dashboard** - monitor.example.com

## Configuration Files

| File Path | Purpose |
|-----------|---------|
| `/etc/nginx/sites-available/example.com` | Main corporate website config |
| `/etc/nginx/sites-available/api.example.com` | API gateway configuration |
| `/etc/nginx/sites-available/admin.example.com` | Admin interface config |
| `/etc/nginx/conf.d/load-balancer.conf` | Load balancing configuration |
| `/etc/nginx/conf.d/security.conf` | Security headers and rate limiting |

## Troubleshooting Guide

### Common Issues

**502 Bad Gateway**
- Check if backend servers are running: `systemctl status backend-service`
- Verify ports in nginx config match backend ports

**403 Forbidden**
- Check directory permissions: `chmod -R 755 /var/www`
- Verify ownership: `chown -R www-data:www-data /var/www`

**404 Not Found**
- Check root directory path in nginx config
- Verify files exist in the specified directory

## Maintenance Procedures

### Adding New Sites
1. Create site directory in `/var/www/`
2. Create config file in `/etc/nginx/sites-available/`
3. Enable site: `ln -s /etc/nginx/sites-available/newsite /etc/nginx/sites-enabled/`
4. Test and reload: `nginx -t && systemctl reload nginx`

### Updating SSL Certificates
```bash
sudo certbot renew --dry-run
sudo systemctl reload nginx
