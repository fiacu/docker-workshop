# Ejercicio 08 #

Utilizando docker compose generar una configuración para correr dos instancias de passwordapi (nicopaez/password-api) balanceadas por Nginx.
La aplicación tiene un endpoint /health que indica la ip/host de la instancia que atendió el pedido, se puede usar esto para verificar el correcto balanceo.
Poner la solución en un carpeta ejercicio08, incluyendo

* la configuración de compose
* el README.md con la forma correrlo y cualquier explicación que consideres relevante. 

Entregar el link directo a la carpeta en el repositorio.

## Respuesta ##

Para resolver este ejercicio cree el archivo `docker-compose-nginx.yml` donde defini dos servicios que ejecutan la imagen nicopaez/password-api como app1 y app2, tambien agregue un servicio con la imagen nginx.

Utilice la version latest, a pesar de no ser una buena práctica, ya que no se especificaba alguna.

Para los servicios app1 y app2 expuse puertos diferentes mapeados sobre el 3000 y de esta fomar poder rutear el trafico en nginx basandome en estos puertos.

Por último, configuré un volumen en el servicio nginx para poder utilizar los templates segun su documentacion: 
[https://hub.docker.com/_/nginx?tab=description](https://hub.docker.com/_/nginx?tab=description)

Para poder correrlo debe ejecutarse:

```bash
docker-compose -f docker-compose-nginx.yml up -d
```

Una vez en ejecución, se puede acceder a [http://localhost:8080/health] repetidas veces y ver como se modifican los valores retornados, especificamente el host:

Request 1: 

```json
{
    "host": "bd5cdf5a067d",
    "loadavg": [
        0,
        0,
        0
    ],
    "freemem": 209403904,
    "appversion": "1.0.0"
}
```

Request 2:

```json
{
    "host": "26efcd88bb86",
    "loadavg": [
        0,
        0,
        0
    ],
    "freemem": 209195008,
    "appversion": "1.0.0"
}
```