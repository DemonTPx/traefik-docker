# Traefik reverse docker proxy

## Setup

- Run `docker-compose up -d` to start the traefik reverse proxy
- Copy `dnsmasq.d/docker.conf` to `/etc/dnsmasq.d/docker.conf`
- Install `dnsmasq` using `apt install dnsmasq`
- Uncomment `prepend domain-name-servers 127.0.0.1;` in `/etc/dhcp/dhclient.conf` 

## Configure in the `docker-compose.yml` of your project
 
 
```yaml
services:
    nginx:
        # ...
        labels:
            - "traefik.frontend.rule=Host:my-project.i"
            - "traefik.docker.network=traefik_gateway"
        networks:
            - my_project
            - web
    
    private_service:
        # ...
        labels:
            - "traefik.enable=false"
        networks:
            - my_project

networks:
    web:
        external:
            name: traefik_gateway
    my_project:
```
