# tarea_docker
# Andres Mauricio Ramirez Rengifo 192987-3743
# andres.ramirez.rengifo@correounivalle.edu.co
# Enlace del video : https://youtu.be/NpYCGPYkvH4

docker volume create pg_db : volumen donde se va guardar los datos

docker network create pg_network : donde se va conectar el servidor y el cliente

docker run  --name pg_server --network pg_network -v pg_db:/var/lib/postgresql/data -e POSTGRES_PASSWORD=contrasena -d postgres:15-bookworm : se crea el contenedor

docker logs pg_server : para ver si el servidor esta corriendo de forma correcta

docker exec -it pg_server bash: para entrar en pg_server

psql -U postgres : para acceder a la base de datos

CREATE DATABASE tarea_db; : se crea la base de datos con el nombre

\c tarea_db : se accede a la base de datos

CREATE TABLE pg_tabla(id SERIAL PRIMARY KEY, mensaje TEXT); : se crea la tabla

SELECT*FROM pg_tabla; : vemos que esta creada la tabla

\q : salimos de la base de datos

exit

docker run - - name pg_client - - network pg_network -it postgres:15-bookworm psql 
-h pg_server -U postgres : se crea el cliente

\c tarea_db : ingresamos a tarea

SELECT*FROM pg_tabla; vemos que la tabla todavia esta creada

INSERT INTO pg_tabla(mensaje) VALUES(‘hola’); para ingresar un registro cuyo valor sera hola

SELECT*FROM pg_tabla; : verificamos que se haya insertado el registro

\q : nos salimos

docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q) : detemos el contenedor

docker network rm pg_network : borramos el contenedor 
