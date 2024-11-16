# Configuration for my Raspberry Homeserver

This is a setup running purely in Docker Containers.

## Software
* Portainer
* Nginx Proxy Manager
* Fail2Ban
* Flame
* Docmost
* OneDev
* Pydio

Docker Setup:
1. Clone repo
2. Cut containers dir into your home
3. Create & edit .env
4. Start Nginx first and the rest
5. Fail2ban needs special configuration linked in sources

## Sources & Installation guides
* [Fail2Ban](https://github.com/crazy-max/docker-fail2ban)
* [Nginx Proxy Manager](https://nginxproxymanager.com/setup/)
* [One Dev](https://robinshen.medium.com/five-minutes-tutorial-to-onedev-23c1ad380aec)
* [Portainer](https://docs.portainer.io/advanced/reverse-proxy/nginx)
* [Flame](https://github.com/pawelmalak/flame)
* [Docmost](https://docmost.com/docs/installation/)
* [Pydio](https://pydio.com/en/docs/cells/v3/docker)