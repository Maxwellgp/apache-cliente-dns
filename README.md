# Practica Servidor WEB

~~~
 apache:
   image: apache2:latest
   ports:
      - 800:800
   volumes:
     - conf: /usr/local/apache2/conf
     - htdocs: /usr/local/apache2/htdocs
   networks:
      red:
        ipv4_address: 10.5.0.5
~~~