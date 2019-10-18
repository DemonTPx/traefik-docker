# Traefik reverse docker proxy

## Setup

- Run `docker-compose up -d` to start the traefik reverse proxy

## Configure in the `docker-compose.yml` of your project
 
 
```yaml
services:
    nginx:
        # ...
        labels:
            - traefik.http.routers.traefik.rule=Host(`my-project.localhost`)
            - traefik.http.services.traefik.loadbalancer.server.port=80 # defaults to 80
            - traefik.docker.network=traefik_gateway
        networks:
            - web
            - default
    
    private_service:
        # ...
        labels:
            - traefik.enable=false
        networks:
            - my_project

networks:
    web:
        external:
            name: traefik_gateway
```
