My friend helps me in more ways than I care to share but alas I cannot avoid. I have always taken notes on my contacts. There's a portion in your mobile devices that has "Notes" normally thats where I would store information. What I realized is that often times the information here would be deleted on accident, the space is open on my mobile phone and can be wiped easily. It's happened where I had extensive information on someone and it was gone. 

Talking with my friend I they mentioned Monica which is a personal CRM - or a contact management system.

Installation:

SSHd into server, created a new directory, created the docker file using

```
version: "3.4"

services:
  app:
    image: monica
    depends_on:
      - db
    ports:
      - 8080:80
    environment:
      - APP_KEY=
      - DB_HOST=db
      - DB_USERNAME=monica
      - DB_PASSWORD=secret
    volumes:
      - data:/var/www/html/storage
    restart: always

  db:
    image: mysql:5.7
    environment:
      - MYSQL_RANDOM_ROOT_PASSWORD=true
      - MYSQL_DATABASE=monica
      - MYSQL_USER=monica
      - MYSQL_PASSWORD=secret
    volumes:
      - mysql:/var/lib/mysql
    restart: always

volumes:
  data:
    name: data
  mysql:
    name: mysql
```
Note that the `APP_KEY=` variable has to be 32 characters long, no special symbols. 

When I ran `docker-compose up` initially I was using this:

```
version: "3.4"

services:
  app:
    image: monica:fpm
    depends_on:
      - db
    environment:
      - DB_HOST=db
      - DB_USERNAME=monica
      - DB_PASSWORD=secret
    volumes:
      - data:/var/www/html/storage
    restart: always
  
  web:
    build: ./web
    ports:
      - 80:80
    depends_on:
      - app
    volumes:
      - data:/var/www/html/storage:ro
    restart: always

  db:
    image: mysql:5.7
    environment:
      - MYSQL_RANDOM_ROOT_PASSWORD=true
      - MYSQL_DATABASE=monica
      - MYSQL_USER=monica
      - MYSQL_PASSWORD=secret
    volumes:
      - mysql:/var/lib/mysql
    restart: always

volumes:
  data:
    name: data
  mysql:
    name: mysql
```

note that this had a web variable that I could not use - it as I was not in need of a reverse proxy. Once I got the right docker I did not have the `APP_KEY=` variable set and I needed to go back into my `docker-compose.yml` to set and restart the service. But when I tried to close my docker containers I was getting an error message permission was denied and they could not be closed down. I tried to remove images, contains, prune nothing worked. I checked several Stock overflows and I found that by running `sudo aa-remove-unknown` I was then able to run `docker-compose down`. Once docker was down I was able to remove the container. I made the changes to the docker compose file and ran `docker-compose up`and the service was rendering at localhost:[PORT]
