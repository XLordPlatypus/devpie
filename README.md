# Configuration for Raspberry Homeserver

## Readme
This is a setup running purely in Docker Containers.
The only real application running is OneDev. 
The rest is for managing the containers or security of the raspberry.
I recommend you to buy a domain for connecting from the outside, I used cloudflare.

## Software
* Portainer
* Nginx Proxy Manager
* Fail2Ban
* OneDev

Step:
1. Set up the Raspi (I recommend a clean installation to start of)
2. Clone this repository where you want to run the docker containers
3. Setup Nginx Proxy Manager
4. get a domain (Cloudflare or similar)
5. Domain should point to the Router public IP
6. Install Port forwarding in your router to your device
7. Fail2ban setup [Fail2Ban](https://blog.lrvt.de/fail2ban-with-nginx-proxy-manager/)

Recommendations:
* Configure Nginx to whitelist only [Cloudflare IPs](https://www.cloudflare.com/de-de/ips/) (Or other provider)]
* Ufw firewall activated [Link](https://pimylifeup.com/raspberry-pi-ufw/)
* [DynDNS setup for router](https://github.com/L480/cloudflare-dyndns) or just use CName

## Fail2Ban:
[source](https://github.com/crazy-max/docker-fail2ban)
```
services:
  fail2ban:
    container_name: fail2ban
    hostname: fail2ban
    cap_add:
      - NET_ADMIN
      - NET_RAW
    environment:
      - TZ=Europe/Berlin
      - F2B_DB_PURGE_AGE=14d
    image: crazymax/fail2ban:latest
    network_mode: host
    restart: unless-stopped
    volumes:
      - <path/to/containers>/containers/fail2ban/data:/data
      - <path/to/containers>/containers/nginx/data/logs:/var/log/npm:ro
```

## Nginx Proxy Manager
[source](https://nginxproxymanager.com/setup/)
```
networks:
  nginx_default:
   external: true

services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    container_name: nginx
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - '80:80' # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81' # Admin Web Port
    volumes:
      - <path/to/containers>/containers/nginx/data:/data
      - <path/to/containers>/containers/nginx/letsencrypt:/etc/letsencrypt
    networks:
      - nginx_default
```

## One Dev
[source](https://robinshen.medium.com/five-minutes-tutorial-to-onedev-23c1ad380aec)
```
networks:
  nginx_default:
    external: true

services:
  onedev:
    image: 1dev/server:latest
    container_name: onedev
    restart: always
    ports:
      - '6610:6610'
      - '6611:6611'
      - '22:22'
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - <path/to/containers>/containers/onedev/data:/opt/onedev
    networks:
      - nginx_default
```

## Portainer
[source](https://docs.portainer.io/advanced/reverse-proxy/nginx)
```
networks:
  nginx_default:
    external: true

services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: unless-stopped
    security_opt:
      - no-new-privileges:true
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - <path/to/containers>/containers/portainer/portainer-data:/data
    networks:
      - nginx_default
    ports:
      - '9000:9000'
      - '9443:9443'
```