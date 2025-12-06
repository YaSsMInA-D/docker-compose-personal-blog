# Personal Blog 

##  Overview
This project demonstrates the evolution of a Django blog development through 3 stages:
1. **Development** → Django runserver
2. **Production Stage 1** → Gunicorn only  
3. **Production Stage 2** → Gunicorn + Nginx

---

## Stage 1: Development Environment

### Configuration:
- **Server**: Django development server (`runserver`)
- **Port**: 8000
- **DEBUG**: Enabled (DEBUG=1)


### Files:
```yaml
# docker-compose.yml (Development)
services:
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    ports:
      - "8000:8000"
    environment:
      - DEBUG=1



### Problems Encountered:

 - No worker processes - Can't handle concurrent requests
 - No security features 



  *** Stage 2: Production Stage 1 - Gunicorn Only

Changes from Development:

---Removed django-browser-reload (development dependency)

---Replaced runserver with gunicorn

---Disabled DEBUG (DEBUG=0)

 ---Added collectstatic to Dockerfile


*** Configuration:

Server: Gunicorn WSGI 

Files Changed:

# Dockerfile changes
CMD ["gunicorn", "personalblog.wsgi:application", "--bind", "0.0.0.0:8000"]

### Problems Encountered:

-Direct exposure to internet - No reverse proxy for security

- Error during build: ModuleNotFoundError: No module named 'django_browser_reload'

   Solution Applied:
--- Removed django-browser-reload from requirements.txt and INSTALLED_APPS



***Stage 3: Production Stage 2 - Gunicorn + Nginx

Changes from Production Stage 1:

 - Added Nginx as reverse proxy

 -Nginx serves static files directly

- Port 80 for external access



**Benefits Achieved:

--- Efficient static file serving - Nginx is optimized for static content

--- Reverse proxy security - Application not directly exposed

---Load balancing ready - Can add more workers

---Better performance with caching

-- Port 80 standard - No need to specify port in URL


### Commands That i used:**

docker-compose down
docker-compose build
docker-compose up

