# nginx-sites-config
nginx ayarları ile iki sitenin farklı dizinlerde çalıştırılması

```
version: "2"

services:
  nginx:
    container_name: nginx-deneme
    image: nginx:latest
    ports:
      - 1080:80
      - 1088:88
    volumes:
      - ./www/server80:/usr/share/nginx/server80
      - ./www/changelogs:/usr/share/nginx/changelogs
      - ./nginx.conf:/etc/nginx/conf/nginx.conf
      - ./conf.d:/etc/nginx/conf.d
```

Nginx ayarları:

```
$ tail conf.d/*
==> conf.d/changelog.conf <==
server {
    listen 88;
#    server_name subdomain.example.com;
    root /usr/share/nginx/changelogs;

#    autoindex on;
#    index index.html;
    # Diğer yapılandırma ayarları
}


==> conf.d/default.conf <==
server {
    listen 80;
    server_name example.com;
    root /usr/share/nginx/server80;

    # Diğer yapılandırma ayarları
}
```
