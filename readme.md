# Configuración Docker Compose DNS


## Practica DNS

#### En el docker compose para tener un volumen con la configuracion tenemos que poner en el docker compose:
- dentro de la crecion del contenedor:
    volumes:
       -dns_conf:/etc/bind

- Y fuera de la creacion del contenedor esta parte (Si no existe el volumen quitamos la parte de external: true)
volumes:
  dns_conf:
    external: true

#### Para tener una red propia interna para todos los contenedores

- Creamos la red con: docker network create  --ubnet 10.1.0.0/24 --gateway 10.1.0.1 br02

- Dentro del docker compose tenemos que poner para meter los contenedores en la red:

- Al cliente que no queremos que tenga una ip fija:
networks:
      -rdns01
- Y al servidor que tendra ip fija:
    networks:
      rdns01:
        ipv4_address: 10.1.0.254

- y fuera de la crecion de los contenedores:
networks:
 rdns01:
  external: true
- Aqui el external: true no lo quitaremos en ningun caso ya que la red la crearemos por comandos antes.



