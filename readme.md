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

- Creamos la red con: docker network create  --subnet 10.1.0.0/24 --gateway 10.1.0.1 br02

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

#### Creacion de servicios

- Al crear el contenedor de bind el servicio dns se crea con el ya que el contenedor es el servicio mismo

#### Modificaciones a la configuracion de bind

- Lo primero cambiado fue los forwarders, puse el primero de google y el segundo el dns secundario de google 
	 forwarders {
	 	8.8.8.8;
		 8.8.4.4;
	 };

- para crear el servicio: docker-compose up
- Para iniciar el servicio: docker-compose start
- Para parar el servicio: docker-compose stop
- Para eliminar el servicio: docker-compose down

- Si solo quieres que afecte al servidor y no a los creados con el compose todos utiliza docker "Opcion" "Nombre del contenedor"

- Nota: despues de tocar cualquier configuración hay que reiniciar el servicio/contenedor




