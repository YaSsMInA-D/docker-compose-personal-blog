

# Development Stage - Docker Compose Personal Blog

## Configuration
- **Web Server**: Django development server (runserver)

## Files:
- `Dockerfile` - Python with development dependencies
- `docker-compose.yml` - Single service configuration
- `requirements.txt` - Django + development packages

## How to run:

docker-compose build
docker-compose up


### PROD STAGE 1 

## Objective
Upgrade from development server to production WSGI server (Gunicorn)

## Changes from Development:
-  Removed django-browser-reload (development only)
-  Replaced `runserver` with `gunicorn`
-  Set DEBUG=0 for production
-  Static files collected during build

## Configuration:
- **Web Server**: Gunicorn WSGI server
- **Port**: 8000
- **Workers**: Default Gunicorn configuration

## Files changed:
- `requirements.txt` - Removed development packages
- `Dockerfile` - Added collectstatic, changed CMD to gunicorn
- `docker-compose.yml` - Updated command and environment

## How to run:

docker-compose build
docker-compose up


### For PROD STAGE 2 

## Objective
Full production deployment with reverse proxy and static file serving

1. **Nginx Container** (port 80)
   - Reverse proxy
   - Static file serving
   - Security headers

2. **Django Container** (port 8000 internal)
   - Gunicorn WSGI server
   - Application logic

## Configuration:
 **External Access**: Port 80 via Nginx
 **Static Files**: Served directly by Nginx
 **Media Files**: Served by Nginx
 **Application**: Proxied to Gunicorn

## New Files:
- `default.conf` - Nginx configuration
- Updated `docker-compose.yml` with nginx service

## How to run:

docker-compose build
docker-compose up

