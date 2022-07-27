# Ejercicio 07 #

Para este ejercicio necesitas docker-compose, si estas usando Docker Desktop ya lo tienes instalados, sino deberás instalarlo aparte. Crea un archivo llamado "docker-compose-jobvacancy.yml" y pon dentro el contenido de este link: https://gitlab.com/-/snippets/2088421/raw/master/docker-compose-jobvacancy.yml.
A continuación ejecuta este comando en una terminal: docker-compose -f docker-compose-jobvacancy.yml up.
Espera unos minutos hasta que dejen de aparecer mensaje en la terminal. Luego navega localhost:3000 para verificar que la aplicación levantó correctamente.
Finalmente contesta:

¿Cuántos contenedores se están ejecutando? (pueden verlo en el archivo docker-compose-jobvacancy.yml y también ejecutando docker ps)
¿Cuales son las imágenes en las que están basados los mencionados contenedores?
¿Puedes leer el docker-compose-jobvacancy.yml y describir lo que hace cada una de sus lineas?
Dado que cada contenedor corre en forma aislada ¿Cómo es posible que esos contenedores se vean entre sí?

Escribe tus respuestas ejercicio07/README.md en tu repositorio github y entrega el link directo al archivo.

* ¿Cuántos contenedores se están ejecutando? (pueden verlo en el archivo docker-compose-jobvacancy.yml y también ejecutando docker ps)

Se estan ejecutando 2 contenedores. En el archivo yml se distinguen 2 servicios el web y la db. Cuando ejecuto el comando docker ps se listan los 2 contenedores:

```bash
$ docker ps
CONTAINER ID   IMAGE                            COMMAND                  CREATED        STATUS          PORTS                    NAMES
c54f4db96a0f   nicopaez/jobvacancy-ruby:1.3.0   "/jobvacancy/start_a…"   25 hours ago   Up 16 seconds   0.0.0.0:3000->3000/tcp   ejercicio07_web_1
35e5d8cc9b1c   postgres:14.4-alpine             "docker-entrypoint.s…"   25 hours ago   Up 17 seconds   5432/tcp                 ejercicio07_db_1
```

* ¿Cuales son las imágenes en las que están basados los mencionados contenedores?

- nicopaez/jobvacancy-ruby:1.3.0
- postgres:14.4-alpine

* ¿Puedes leer el docker-compose-jobvacancy.yml y describir lo que hace cada una de sus lineas?

Segun la documentacion: [https://docs.docker.com/compose/compose-file/](https://docs.docker.com/compose/compose-file/)

```docker
services: => servicios que componen
  web: => alias del servicio
    image: nicopaez/jobvacancy-ruby:1.3.0 => imagen para iniciar el contenedor
    links: => define enlace a otro contenedor, tambien indica dependencia, por lo que determina el orden de inicio
      - db => ser requiere servicio db.
    ports: => puertos que se exponen.
      - "3000:3000"
    environment: => Definicion de variables de ambientes utilizadas por el servicio
      PORT: "3000"
      RACK_ENV: "production"
      DATABASE_URL: "postgres://postgres:Passw0rd!@db:5432/postgres"
    depends_on: => determina comienzo y fin de dependencias entre servicios.
      - db => debe iniciar primero db
  db:
    image: postgres:14.4-alpine
    environment:
      POSTGRES_PASSWORD: Passw0rd!
```

* Dado que cada contenedor corre en forma aislada ¿Cómo es posible que esos contenedores se vean entre sí?

Los servicios se comunica por medio de una network. En este caso la creada por defecto ejercicio07_default

```bash
$ docker network ls
NETWORK ID     NAME                     DRIVER    SCOPE
c54ab3968360   bridge                   bridge    local
bdc8c1b5c25f   ejercicio07_default      bridge    local
4d9ec7151e2d   host                     host      local
e5e23892139b   jv1                      bridge    local
ccfca9fa2386   none                     null      local
40a035c21d5c   webapi-example_default   bridge    local
b98777c58e6b   workshop03_default       bridge    local
```
