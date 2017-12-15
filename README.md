# Tiny Tiny RSS Docker Image

Example docker-compose.yml
```
version: '2'

secrets:
  ttrss_pgsql_pw:
    external: 'true'

volumes:
  data:
    driver: local
  db:
    driver: local

services:
  app:
    image: ptrunk/docker-ttrss
    volumes:
    - data:/var/www/html
    depends_on:
    - db

  updatedaemon:
    image: ptrunk/docker-ttrss
    volumes:
    - data:/var/www/html
    user: apache
    entrypoint: php
    command: /var/www/html/update_daemon2.php
    depends_on:
      - app
      - db
   
  db:
    image: postgres:10.1
    environment:
      POSTGRES_USER: ttrss
      POSTGRES_DB: ttrss
      POSTGRES_PASSWORD_FILE: /run/secrets/ttrss_pgsql_pw
    volumes:
    - db:/var/lib/postgresql/data
    secrets:
    - ttrss_pgsql_pw
```
