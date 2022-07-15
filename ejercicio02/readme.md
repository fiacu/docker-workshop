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

