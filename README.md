# proxy_docker

Docker web proxy for the different docker web services of Queerreferat Aachen

## usage

for any web service that is to be added to the infrastructure, create a docker-compose.yml file and add the proxy network.

```
networks:
    proxy:
        external: true
        name: shared-proxy
```

Besides possibly needed other services, create ONE (proxied server) service that connects to the proxy network and specify the virtual host domain as an environment variable. Also specify host and email for Let's Encrypt if you want TLS encryption.

```
services:
    ...
    server:
        environment:
            - VIRTUAL_HOST=<SUBDOMAIN>.queerreferat.ac
            - LETSENCRYPT_HOST=<SUBDOMAIN>.queerreferat.ac
            - LETSENCRYPT_EMAIL=<EMAIL>
        networks:
            - proxy
            - default
```
