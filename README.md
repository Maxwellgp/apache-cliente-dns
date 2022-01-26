# Practica Servidor WEB

## Servidor Apache
~~~
 apache:
   image: httpd:latest
   ports:
      - 8000:80
   volumes:
     - confapache:/usr/local/apache2/conf
     - htdocs:/usr/local/apache2/htdocs
   networks:
      red:
        ipv4_address: 10.5.0.5 
~~~
* Su puerto será el 8000:80.
* Le asignamos dos volumenes conf, htdocs.
* Le asignamos la ip 10.5.0.5 de la red.

## Cliente
~~~
 apache-cliente:
   image: kasmweb/desktop:1.10.0
   ports:
      - 6901:6901
   stdin_open: true  
   tty: true         
   environment:
    - VNC_PASSWORD=password 
   networks:
      red:
        ipv4_address: 10.5.0.3 
~~~
* Su puerto será el 6901:6901.
* Asignamos una contraseña que será 'password' en string.
* Le asignamos la ip 10.5.0.3 de la red.

## DNS
~~~
 bind9:
    container_name: bind9_server
    image: internetsystemsconsortium/bind9:9.16
    networks:
      red:
        ipv4_address: 10.5.0.2
    ports:
      - 801:801
    volumes:
      - bind:/etc/bind
~~~
* Su puerto será el 801:801.
* Le asignamos le volumen bind.
* Le asignamos la ip 10.5.0.2

## Red
~~~
networks:
  red:
    driver: bridge
    ipam:
     config:
       - subnet: 10.5.0.0/16
         gateway: 10.5.0.1
~~~
Creamos la red en modo bridge, con subnet: 10.5.0.0 y gateway: 10.5.0.1

### Volumenes
~~~
volumes:
  bind:
    external: true
  confapache:
    external: true
  htdocs:
    external: true
~~~
Todos los volumenes serán creados de manera externa e independiente.

## Autor
* **Samuel Gardón** - [Samuel Gardón](https://github.com/Maxwellgp)