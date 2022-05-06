
# NextJS + Strapi + MongoDB + NGINX + Docker Starter

This boilerplate includes :

- 🖼 NextJS
- 🛠 Strapi
- 🌱 MongoDB
- 🔗 NGINX
- ⛴ Docker

## Configuration

Rename .env.example to .env :
```bash
  cp .env.example .env
```

You can modify 3 environment variables :
- MONGODB_DBNAME : Database name for Strapi on MongoDB
- MONGODB_ROOT_USERNAME : Root username for MongoDB
- MONGODB_ROOT_PASSWORD : Root password for MongoDB

You can also modify the NGINX config for custom domain :

```
  # NextJS
  server {
    listen 80;
    server_name localhost; # Modify this line
    include server.conf;

    # Cache (jsx, css)
    location /_next/static {
      proxy_cache STATIC;
      proxy_pass http://nextjs_upstream;
    }

    # Cache (...static)
    location ~* ^/.*\\.(?:jpg|jpeg|gif|png|ico|cur|gz|svg|ttf)$ {
      proxy_cache STATIC;
      proxy_ignore_headers Cache-Control;
      proxy_cache_valid 60m;
      proxy_pass http://nextjs_upstream;
    }

    location / {
      proxy_pass          http://nextjs_upstream;
    }
  }


  # Strapi
  server {
    listen 80;
    server_name cms.localhost; # Modify this line
    include server.conf;
    
    location / {
      proxy_pass          http://strapi_upstream;
    }
  }
}
```

**Disclaimer : SSL AND HTTPS isn't configured on this boilerplate**

## Deployment

To deploy this project run

```bash
  docker-compose up -d
```

You have to wait till Strapi is fully built and ready to be used (deps installation can take some times)

With the default configuration **and with Strapi fully installed** :
 - Strapi : [http://cms.localhost](http://cms.localhost)
 - NextJS : [http://localhost](http://localhost)
 - MongoDB : [mongodb://strapi:strapi@127.0.0.1:27017/](mongodb://strapi:strapi@127.0.0.1:27017/)



