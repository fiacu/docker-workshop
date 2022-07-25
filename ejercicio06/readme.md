# Ejercicio 06 #

Crear un contenedor para la aplicación PasswordApi (del ejercicio 4) que esté basada en la imagen redhat-openjdk-18/openjdk18-openshift
disponible en la registry de Red Hat (https://catalog.redhat.com/software/containers/redhat-openjdk-18/openjdk18-openshift/58ada5701fbe981673cd6b10).


1. Escribe el dockerfile
2. Genera la imagen (docker build)
3. Publica la imagen en tu cuenta de Dockerhub


Pon el dockerfile en un repositorio Github en una carpeta ejercicio06. Agregar también en esa carpeta un archivo readme con el link a la imagen generada en dockerhub.
Entrega el link a la carpeta en el repositorio Github.

## Pasos ##

1. Me registre en redhat
2. configure archivo de autorizacion en .docker/config.json
3. Descargue la imagen: docker pull registry.redhat.io/redhat-openjdk-18/openjdk18-openshift:1.12-1.1655301789

```bash
$ docker pull registry.redhat.io/redhat-openjdk-18/openjdk18-openshift:1.12-1.1655301789

docker build -t fiacu/passwordapi-redhat .
docker run -d -p 8080:8080 fiacu/passwordapi-redhat

docker exec -it 1c6de6bfbffb bash
[jboss@1c6de6bfbffb /]$ cat /etc/redhat-release
Red Hat Enterprise Linux Server release 7.9 (Maipo)
[jboss@1c6de6bfbffb /]$
```

## GITHUB Repo ##

[https://hub.docker.com/repository/docker/fiacu/passwordapi-redhat](https://hub.docker.com/repository/docker/fiacu/passwordapi-redhat)
