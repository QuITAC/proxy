# proxy_docker

Traefik web proxy for the different docker web services of Queerreferat Aachen

## setup

1. replace `<ref_mail>` with our mail address
2. launch the proxy server using `docker compose up -`

## usage

for any web service that is to be added to the infrastructure, create a docker-compose.yml file and add the proxy network.

```yml
networks:
  proxy:
    external: true
    name: shared-proxy
```

Besides possibly needed other services, create ONE (proxied server) service that connects to the proxy network and specify the virtual host domain as an environment variable. Also specify host and email for Let's Encrypt if you want TLS encryption.

```yml
services:
  server:
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.<uniquearbitraryroutername>.rule=Host('<Hostname>')"
    networks:
      - proxy
      - default
```
