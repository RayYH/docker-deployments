# Deployments 101

This repository contains a collection of sample configurations for apps and services, you can quickly setup services on
your local machine. **Only works on MacOS**.

## Generate Certs

Use the [mkcert](https://github.com/FiloSottile/mkcert) to generate the certificates.

```bash
# Install mkcert
$ mkcert -install

# Generate the certificates
$ mkcert -cert-file certs/local.test/cert.pem -key-file certs/local.test/key.pem local.test "*.local.test" local.test localhost 127.0.0.1 ::1
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

## Start Dashboard

```shell
$ docker network create nginx
$ docker compose -f services/dashy-compose.yml up -d
$ docker compose -f docker-compose.yml up -d
```

Visit [https://local.test](https://local.test) to see the Dashboard.

## Starting Other Services

First, you need to uncomment the line for configuring proxy inside `nginx/nginx.conf`:

```nginx
# include /etc/nginx/conf.d/minio.local.test.conf;
```

Now, start the service and reload nginx service:

```shell
docker compose -f services/minio-compose.yml up -d
docker restart nginx
```

Visit [https://minio.local.test](https://minio.local.test) to see the Minio welcome page.
