# Nginx Samples

This repository contains a collection of sample configurations for the Nginx web server.

## Generate Certs

Use the [mkcert](https://github.com/FiloSottile/mkcert) to generate the certificates.

```bash
# Install mkcert
$ mkcert -install

# Generate the certificates
$ mkcert -cert-file certs/local.test/cert.pem -key-file certs/local.test/key.pem local.dev "*.local.dev" local.test localhost 127.0.0.1 ::1
```

## Install Dnsmasq

Use the following commands to install and configure Dnsmasq.

```bash
$ brew install dnsmasq
$ mkdir -pv $(brew --prefix)/etc/
$ echo 'address=/.test/127.0.0.1' >> $(brew --prefix)/etc/dnsmasq.conf
$ echo 'port=53' >> $(brew --prefix)/etc/dnsmasq.conf
$ sudo brew services start dnsmasq
$ sudo mkdir -v /etc/resolver
$ sudo bash -c 'echo "nameserver 127.0.0.1" > /etc/resolver/test'
```

## Start Services

```shell
docker network create nginx
docker compose -f docker-compose.yml up -d
```
