# ejemploDAGSS
Proyecto Java EE 8 de ejemplo para DAGSS 2020/21

# ESQUEMA
![Esquema del ejemplo](doc/esquema.jpg?raw=true "Esquema del proyecto JSF + JAX-RS")


# PREVIO

* Instalación del servidor de aplicaciones Payara 5 
  
    * Web Payara Server: https://www.payara.fish/
* Enlaces descarga (Community Edition): https://www.payara.fish/downloads/payara-platform-community-edition/
    * Seleccionar la versión `Payara Server 5.XXXX.X (Full)`
  
  ```
  unzip payara-5.XXXX.X.zip
  export PAYARA_HOME=$PWD/payara5
  ```
  
  **Nota 1:**  En el caso de usar el IDE Netbeans 12.x es posible descargar, instalar y vincular el IDE con el servidor desde la opción `Tools > Server > AddServer` del propio IDE (detalles en [Creación del proyecto con Netbeans paso a paso](/doc/pasos_netbeans.md))
  
  **Nota 2:**  Para otros IDEs (Eclipse, Visual Studio Code, Intelli J) existen plugins específicos para integrar el servidor con el IDE (detalles en https://docs.payara.fish/enterprise/docs/5.23.0/documentation/ecosystem/ecosystem.html) 
  
  El servidor Payara5 puede gestionarse desde línea de comandos con la herramienta `asadmin` ubicada en `$PAYARA_HOME/bin` ([resumen comandos `asadmin`](https://docs.payara.fish/community/docs/5.2020.6/documentation/payara-server/asadmin-commands/server-management-commands.html))
  
  ```
  $PAYARA_HOME/bin/asadmin start-domains domain1   # arranca el dominio por defecto (domain1) del servidor
  $PAYARA_HOME/bin/asadmin stop-domains domain1   # detiene el dominio por defecto (domain1) del servidor
  ```
  
  Con el servidor de aplicaciones arrancado está disponible la consola web de administración enla URL http://localhost:4848
  
* Descargar driver JDBC de MySQL y copiarlo en el directorio de librerias de Payara5
  
  ```
  cd /tmp
  wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-8.0.22.zip
  unzip mysql-connector-java-8.0.22.zip
     
  cp /tmp/mysql-connector-java-8.0.22/mysql-connector-java-8.0.22.jar \
        $PAYARA_HOME/glassfish/domains/domain1/lib
  ```
  
  **Nota:** También puede registrarse el driver de MySQL empleando el comando `asdmin` de Payara5
  
  ```
  $PAYARA_HOME/bin/asadmin add-library /tmp/mysql-connector-java-8.0.22/mysql-connector-java-8.0.22.jar
  ```
  
   
  
* Crear BD `pruebas_dagss` en MySQL
   ```
   $ mysql -u root -p    [pedirá la contraseña de MySQL]

   mysql> create user dagss@localhost identified by "dagss";
   mysql> create database pruebas_dagss;
   mysql> grant all privileges on pruebas_dagss.* to dagss@localhost;
   ```

# DESCARGA Y EJECUCION DEL PROYECTO

* Descargar copia del proyecto desde GitHub
   ```
   git clone https://github.com/esei-si-dagss/ejemploDAGSS-20.git
   ```

* Abrir el proyecto en el IDE seleccionado y desplegarlo en el servidor (la aplicación estará accesible en la URL http://localhost:8080/ejemploDAGSS-20)

* Otra alternativa es empaquetarlo con `maven` en un archivo `.war`y desplegarlo manualmente en el servidor.

    * Desde el directorio del proyecto `ejemploDAGSS`

    ```
    cd ejemploDAGSS-20
    mvn install
    $PAYARA_HOME/bin/asadmin deploy target/ejemploDAGSS-1.0.war
    ```


# DOCUMENTACION
 
* [Creación del proyecto con Netbeans paso a paso](/doc/pasos_netbeans.md)

# TAREAS FUTURAS
1. Añadir las vistas para la visualización y gestión de los anuncios 
2. Añadir un API REST empleando JAX-RS
