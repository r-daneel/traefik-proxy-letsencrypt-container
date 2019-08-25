# traefik-proxy-letsencrypt-container
Traefik Proxy + Letsencrypt Container setup

This Ansible Role starts a traefik container.\
The traefik configuration is setup to listen on http (port 80/tcp) and https (port 443/tcp).\
The traefik acme module is enabled so any container running on the docker host will automatically get an SSL certificate from letsencrypt.org.\
The traefic proxy will automatically pick up any existing container as a destination.

Any http traffic will be automatically be redirected to https.

## Parameters
Following parameters must be provided in order for the playbook to run properly:
- The domain name is used to build the FQDN for each detected container\
  > Ex: If the container name is `web_srv`, the FQDN becomes `web_srv.{your_domain}`\
  >     The traefik proxy will automatically request and setup an SSL certificate for web_srv.{your_domain}
- The e-mail address is used to request new certificates from letencrypt.org
- The userrname & password for the traefik dashboard interface

## Playbook
The example playbook `traefik-proxy-letsencrypt-container.yaml` run agains a host setup with a working docker setup will turn your containers into publicly accessible sites with https enabled.

## Dashboard
The container itself will run as a container named 'traefik' and will thus automatically generate an SSL certificate and respond to https://traefik.{your_domain}.
