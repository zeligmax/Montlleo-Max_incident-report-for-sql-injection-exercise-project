#  Informe de gestión de incidentes que cumple con la norma ISO 27001
<!-- hide -->

> By [@rosinni](https://github.com/rosinni) and [other contributors](https://github.com/4GeeksAcademy/deploying-wordpress-debian/graphs/contributors) at [4Geeks Academy](https://4geeksacademy.co/)

[![build by developers](https://img.shields.io/badge/build_by-Developers-blue)](https://4geeks.com)
[![build by developers](https://img.shields.io/twitter/follow/4geeksacademy?style=social&logo=twitter)](https://twitter.com/4geeksacademy)

*These instructions are [available in english](https://github.com/breatheco-de/incident-report-management-exercise-project/blob/main/README.md)*
<!-- endhide -->


<!-- hide -->


### Antes de empezar...

> ¡Te necesitamos! Estos ejercicios se crean y mantienen en colaboración con personas como tú. Si encuentras algún error o falta de ortografía, contribuye y/o repórtalo.

<!-- endhide -->

## 🌱 ¿Cómo empezar este proyecto?

¡No clones este repositorio! solo sigue las intrucciones.

Este ejercicio tiene como objetivo enseñar a los estudiantes cómo identificar y reportar una vulnerabilidad de inyección SQL utilizando la aplicación web Damn Vulnerable Web Application (DVWA). El reporte se debe realizar de acuerdo a las normas ISO 27001 para la gestión de incidentes de seguridad de la información.

### Requisitos

* VirtualBox instalado en tu computadora.
* Una máquina virtual Debian instalada en VirtualBox. Para efectos del tutorial, utilizaremos Debian.

#### Beneficios de Usar una Máquina Virtual

*Aislamiento: Mantiene el entorno de pruebas separado de tu sistema operativo principal, protegiéndolo de posibles daños.

*Facilidad de Restauración: Puedes crear instantáneas (snapshots) de tu máquina virtual y restaurarlas fácilmente si algo sale mal.

*Portabilidad: Puedes mover y compartir la máquina virtual fácilmente con otros.

## 📝 Instrucciones

### Paso 1: Crear una Máquina Virtual:
- [ ] Abre VirtualBox y haz clic en "Nuevo".
- [ ] Asigna un nombre a tu VM (por ejemplo, "Debian-DVWA").
- [ ] Selecciona "Linux" como tipo de sistema operativo y "Debian (64-bit)" como versión.
- [ ] Asigna al menos 2 GB de RAM (recomendado).
- [ ] Crear un disco duro virtual con al menos 20 GB de espacio (VDI, reservado dinámicamente).
- [ ] Descarga la imagen ISO de Debian desde Debian.
- [ ] Inicia la VM y selecciona la imagen ISO de Debian descargada para arrancar desde ella.
- [ ] Sigue las instrucciones en pantalla para instalar Debian en la máquina virtual.
- [ ] En la sección "Red", selecciona "Adaptador Puente" (Bridge Adapter) para que la VM esté en la misma red que tu host.

### Paso 2: Configuración de Entorno de Desarrollo.  MySQL(MariaDB) Apache, y PHP (LAMP Stack):
- [ ] Actualizar el índice de paquetes
```sh
sudo apt-get update
```
- [ ] Instalar MariaDB
```sh
sudo apt-get install mariadb-server
```
- [ ] Iniciar y habilitar el servicio de MariaDB
```sh
sudo systemctl start mariadb 
sudo systemctl enable mariadb
```
- [ ] Asegurar la instalación de MariaDB
```sh
sudo mysql_secure_installation
```
- [ ] Sigue las instrucciones para establecer la contraseña del root de MariaDB y configurar la seguridad básica.


### Paso 3: Configuración de Apache y PHP:
- [ ] Instalar Apache y PHP
```sh
sudo apt-get install apache2 
sudo apt-get install php libapache2-mod-php php-mysql
```
- [ ] Iniciar y habilitar el servicio de Apache
```sh
sudo systemctl start apache2 
sudo systemctl enable apache2
```

### Paso 4: Instalación y Configuración de DVWA:
- [ ] Descargar DVWA
```sh
cd /var/www/html 

```
- [ ] Configurar DVWA
Cambia al directorio DVWA y renombra el archivo de configuración
```sh
cd DVWA/config 
sudo cp config.inc.php.dist config.inc.php
```
- [ ] Edita el archivo de configuración `config.inc.php` para configurar las credenciales de MariaDB:
```ssh
sudo nano config.inc.php
```
> 💡 IMPORTANTE: Asegúrate de que las siguientes líneas tengan las credenciales correctas:
* $_DVWA[ 'db_user' ] = 'root';
* $_DVWA[ 'db_password' ] = 'tu_contraseña_de_root'; 
* $_DVWA[ 'db_database' ] = 'dvwa';

- [ ] Configurar la Base de Datos
Inicia sesión en MariaDB y crea la base de datos DVWA
```sh
sudo mysql -u root -p 
CREATE DATABASE dvwa; 
EXIT;
```
- [ ] Ajustar Permisos
```sh
sudo chown -R www-data:www-data /var/www/html/DVWA/
sudo chmod -R 755 /var/www/html/DVWA/
```
- [ ] Abre un navegador en tu VM y ve a http://localhost/DVWA/setup.php
- [ ] Revisa la configuración y Haz clic en "Create / Reset Database".


### Paso 5: Realización del Ataque SQL Injection
- [ ] Abre un navegador en la VM y accede a http://localhost/DVWA.
- [ ] Iniciar sesión en DVWA:
```
*Usuario: admin
*Contraseña: password
```
- [ ] Configurar el Nivel de Seguridad
Ve a la pestaña "DVWA Security" y selecciona el nivel "Low" para facilitar la explotación

- [ ] Ejecutar SQL Injection
Ve a la sección "SQL Injection" en DVWA
Ingresa un ataque de inyección SQL simple en el campo proporcionado de "User ID", por ejemplo:
```sh
1' OR '1'='1
```
Haz clic en "Submit" y observa cómo DVWA procesa la inyección y muestra los resultados de la base de datos. 
> 💡 NOTA: Deberías ver una lista de todos los usuarios extraída de la base de datos, indicando una inyección SQL exitosa.

### Paso 6: Reporte del Incidente
- [ ] Cumple la Estructura del Reporte
  * Título del Reporte
  * Introducción
  * Descripción del Incidente
  * Proceso de Reproducción
  * Impacto del Incidente
  * Recomendaciones
  * Conclusión

 ¡Buena suerte con tu ejercicio!
