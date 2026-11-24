# OWASP Juice Shop – Lab 01: Reconocimiento de rutas y control de acceso

## Objetivo
Desplegar Juice Shop de forma aislada, descubrir rutas ocultas de un SPA y comprobar si el control de acceso está en el frontend o en el backend
## Entorno
Docker en macOS M2
imagen bkimminich/juice-shop
expuesto solo en 127.0.0.1
safari browser

## Despliegue
```
docker run -d --name juice-shop -p 127.0.0.1:3000:3000 bkimminich/juice-shop
```
## Reto: Score Board
curl descarga el archivo main.js en la memoria con grep buscamos algo, en este caso path:` , y las comillas simples de afuera evitan que zsh interprete las comillas invertidas como un comando. sort -u, ordena y quita repetidos
```
curl -s http://127.0.0.1:3000/main.js | grep -o 'path:`[^`]*`' | sort -u
```
## Hallazgo: frontend vs backend
el frontend no protege nada, todo el trabajo de seguridad es del backend, la que autoriza una acceso de administrador es el servidor mediante una llamada de la api, si no se hace esta fallando el top 1 de OWASP( A01: Broken Access Control.), 403 es una ruta del frontend y en la pestaña Red no hubo ninguna petición de administración (llamada de api como /api/, /rest/)
## Lecciones aprendidas
(pull access denied): la imagen no existe, no tengo autorización para la imagen, verificar imágenes en Docker Hub: puede que use una imagen falsa, security through obscurity: unico metodo de seguridad ocultar paginas 

## Aviso
Laboratorio ejecutado solo en entorno local propio.