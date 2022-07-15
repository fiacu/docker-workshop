# Ejercicio 02 #

1. Descarga la imagen nicopaez/pingapp:3.0.0

```bash
docker pull nicopaez/pingapp:3.0.0
```

2. Crear un repositorio en dockerhub

Lo hice desde la página. [Link](https://hub.docker.com/repository/docker/fiacu/ejercicio02)

3. Sube la imagen descargada al repositorio creado

Hago un tag de la imagen descargada en el paso anterior.

```bash
docker tag 5021b0410677 fiacu/ejercicio02:v1.0
```

Pusheo el tag a mi repo.

```bash
docker push fiacu/ejercicio02:v1.0
```

6. Incluye al final de las instrucciones la sentencia docker pull exacta para descargar tu imagen.

```bash
$ docker pull fiacu/ejercicio02:v1.0
v1.0: Pulling from fiacu/ejercicio02
Digest: sha256:b3ccc9984deb6eb1dfd9ce172f29c38651902ece467c666f6e585ddf9ba4adb5
Status: Image is up to date for fiacu/ejercicio02:v1.0
docker.io/fiacu/ejercicio02:v1.0
```
