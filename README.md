# Docker Deployments

This repository contains a collection of sample configurations for apps and services, you can quickly setup services on
your local machine. **Only works on MacOS for now, but can be easily adapted to other Unix-based systems.**

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
$ ./service nginx start
```

Visit [https://local.test](https://local.test) to see the Dashboard.

## Supported Services

- Jenkins
- Gitea
- Minio
- MySQL
- Mongo

## Starting Other Services

```shell
# service name should be lowercase
$ ./service [service_name] start
```

Visit [https://[service_name].local.test](https://local.test) to see the service page if it's available.
