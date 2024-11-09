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

## Nginx Proxy Manager
[source](https://nginxproxymanager.com/setup/)

## One Dev
[source](https://robinshen.medium.com/five-minutes-tutorial-to-onedev-23c1ad380aec)

## Portainer
[source](https://docs.portainer.io/advanced/reverse-proxy/nginx)

## Flame
[source](https://github.com/pawelmalak/flame)