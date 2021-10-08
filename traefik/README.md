Directories store dynamic configuration with routes to dev and production environments


Generate default http passwords for both Traefik and Portainer dashboards:
```
docker run --rm httpd:2.4-alpine htpasswd -nbB USERNAME 'PASSWORD' | cut -d ":" -f 2
# for deploying with docker-compose:
    # escape all $ characters with $$
    # example: "$$2y$$05$$dxmqV2oF3HNHkQYwFldjUuuos6MHgYjJ8fEU8pBK9G9MSIf2hckRm" 

# for deploying with docker swarm:
    # escape all $ characters with \$
    # example: "\$2y\$05\$dxmqV2oF3HNHkQYwFldjUuuos6MHgYjJ8fEU8pBK9G9MSIf2hckRm" 
```
Save the password in the .env file.


#----------------------------------------------------------------------------------
# traefik configuration example 
#----------------------------------------------------------------------------------
  # example1:
  #   image: containous/whoami
  #   environment:
  #     WHOAMI_NAME: "example1"
  #   labels:
  #       - "traefik.enable=true"
  #       - "traefik.http.routers.example1.rule=Host(`localhost`) || Host(`exp.localhost`)"
  #       - "traefik.http.routers.example1.entrypoints=web"
  #   networks:
  #       - net_traefik

  # example2_path:
  #   image: containous/whoami
  #   environment:
  #     WHOAMI_NAME: "example2_path"
  #   labels:
  #       - "traefik.enable=true"
  #       - "traefik.http.routers.example2_path.rule=(Host(`localhost`) && PathPrefix(`/a`)) || (Host(`exp.localhost`) && PathPrefix(`/a`))"
  #       - "traefik.http.routers.example2_path.entrypoints=web"
  #   networks:
  #       - net_traefik

  # sub:
  #   image: containous/whoami
  #   environment:
  #     WHOAMI_NAME: "sub"
  #   labels:
  #       - "traefik.enable=true"
  #       - "traefik.http.routers.sub.entrypoints=web"
  #       - "traefik.http.routers.sub.rule=Host(`subdomain.localhost`)"
  #   networks:
  #       - net_traefik