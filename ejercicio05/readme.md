# Ejercicio 05 #

Investigar que hacen y para que se usan los siguientes comandos dentro de un Dockerfile:

* HEALTHCHECK
* ONBUILD
* VOLUME

Escribir la respuesta en el repositorio personal en ejercicio05/README.md, entregar el link director al archivo.

## HEALTHCHECK ##

La instruccion HEALTHCHECK le indica a Docker como probar un contender para veririficar que continua funcionando correctamente. Sirve para detectar comportamientos inesperados, como ser un loop infinito de un web server.

Cuando se utiliza, el contenedor pasa a tener un estado adicional, el health status. El estado inicial es *starting*, luego de pasar la primer revisión de estado pasa a estado *healthy*, si comienzan a fallar las revisiones pasará a estado *unhealthy*.

Se pueden especificar distintas opciones de revisión. Intervalo de repeticion (--interval), timeout (--timeout), delay inicial (start-period) y reintento (--retries).

La utilidad de los healthchecks se aprecia en los orquestadores, por ejemplo, docker swarm tiene en cuenta este estado para reiniciar contenedores que estan en estado unhealthy para garantizar una cierta cantidad de contenedores en servicio.

[https://docs.docker.com/engine/reference/builder/#healthcheck](https://docs.docker.com/engine/reference/builder/#healthcheck)


## ONBUILD ##

Esta instrucción agrega a la imagen un trigger que se ejecutará en un momento posterior, cuando la imagen se use como base para otra compilación. El trigger se ejecutará en el contexto de la compilación descendente, como si se hubiera insertado inmediatamente después del *FROM* en el Dockerfile.

Este instruccion puede utilizarse para desarrollar una imagen generalizada base, de la cual un desarrollador no va a necesitar volver a especificar los comandos precedidos pore el ONBUILD y solo deberá ocuparse de comandos especificos de su proyecto. Ejemplo:

```docker
FROM openjdk:8
ONBUILD WORKDIR /
ONBUILD COPY passwordapi.jar passwordapi.jar
EXPOSE 8080
CMD java -jar passwordapi.jar
```

Al construir una imagen "base" segun el dockerfile anterior, no se va a ejecutar el WORKDIR y el COPY. Estos comandos se ejecutaron cuando se construya la imagen que tenga como origen la imagen base creada.

[https://docs.docker.com/engine/reference/builder/#onbuild](https://docs.docker.com/engine/reference/builder/#onbuild)

## VOLUME ##

Este comando permite crear un *mount point* y que lo monte un volumen de Docker. Adicionalmente incluye el nombre del mount point y lo marca como elemento que cuenta con volúmenes que fueron montados de manera externa a partir de un host nativo o desde otros contenedores.

```docker
FROM ubuntu
RUN mkdir /myvol
RUN echo "hello world" > /myvol/greeting
VOLUME /myvol
```

El ejemplo anterior crear un *mount point* en /myvol y copiara el archivo greeting en ese volumen.

Un volumne, no es mas que una carpeta en el sistema de archivos. 

[https://docs.docker.com/engine/reference/builder/#volume](https://docs.docker.com/engine/reference/builder/#volume)