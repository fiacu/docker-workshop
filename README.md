# docker-workshop
Docker Balanz workshop


## Crear una network - clase 3
#!/bin/bash

docker network create jv1

docker container run --name=db -e POSTGRES_PASSWORD=Passw0rd! --network=jv1 postgres:14.4-alpine

docker container run -d --name=web -e PORT=3000 -e RACK_ENV=production -e DATABASE_URL='postgres://postgres:Passw0rd!@db:5432/postgres' -p3000:3000 --network=jv1 nicopaez/jobvacancy-ruby:1.3.0

### Docker compose 

https://github.com/docker/awesome-compose

- Copio :
https://gitlab.com/-/snippets/2088421/raw/master/docker-compose-jobvacancy.yml
- ejecuto:
docker-compose -f docker-compose-jobvacancy.yml up

doker-compose up

docker-compose exec webapp /bin/bash
