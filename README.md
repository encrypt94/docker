# nerdzeu/docker

# Develop

```sh
docker build -t nerdzeu/base .
docker run -d -p 8080:80 --name nerdz nerdzeu/base

```

Visit http://localhost:8080

# Open an interactive shell

```sh
docker exec -ti nerdz /bin/bash

```

# Reverse proxy

```sh
apt-get install nginx dnsmasq
```
Add in nginx.conf

```conf
resolver 127.0.0.1;
server {
listen 80;

server_name primary.nerdz.eu;
set $dn "local.nerdz.eu";
location / {
        proxy_pass http://$dn;
        }
}
```

Start dnsmasq and nginx.
