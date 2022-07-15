# Ejercicio 01 #

## Construir imagen ##

```bash
docker build -t fmoran-01-nginx .
```

## Ejecutar imagen ##

```bash
docker run -d -p 8080:80 fmoran-01-nginx
```