Oracle Fusion Middleware  
===
Software para la instalación de SOA
---
**OFM** : Oracle Fusion Middleware

| Software | Archivo | Version |
| :------- | -----: | -----: |
| JDK 8.65 linux x64|jdk-8u65-linux-x64.tar.gz| **8.65** |
| OFM Infrastructure | fmw_12.2.1.0.0\_infrastructure\_Disk1\_1of1.zip | **12.2.1.0.0**
| OFM 12c SOA Suite and Business Process Management | V78169-01.zip | **12.2.1.0.0** |
|OFM 12c WebLogic Server and Coherence| V78153-01.zip | **12.2.1.0.0** |
| OFM 12c Service Bus | V78173-01.zip | **12.2.1.0.0** |
|Oracle JDeveloper 12c and Oracle Application Development Framework 12c | V78168-01_1of2.zip -  V78168-01_2of2.zip | **12.2.1.0.0**|

Topología de Instalación Estandar de Oracle Fusion Middleware
---  
Es importante definir la estructura estandar de la topologia de directorios de OFM, ya que permitira en un futuro extender esta topología para que sea altamente disponible y seguro, de forma que es adecuada para un sistema de producción.

1. Entendiendo los permisos:
El usuario que instala OFM debe ser propietario de los archivos y tener los siguientes permisos:
  + Permisos de lectura y escritura en todos los archivos **no-ejecutables** por ejemplo .jar, .properties o .xml.  Todos los usuarios en el mismo grupo como propietarios de los archivos solo tienen permisos de lectura.
  + Permisos de lecutra, escritura y ejecucion en todos los archivos **ejecutables** por ejemplo .exe, .sh o .cmd. Todos los usuarios en el mismo grupo como propietarios del archivo solo tiene permisos de lectura y ejecucion.

Esto significa que alguien mas que la persona que instalo el software, puede usar los instaladores binarios en el Oracle Home (**Oracle_Home**) para configurar un dominio o grupo de Productos de Oracle Fusion Middleware.

**Topología de Instalacion Estandar de OFM.**
```
/home
----- /oracle
---------- /product
--------------- /Oracle Home
                (Oracle_Home)
---------- /config
--------------- /Domain Home
                (domains)
--------------- /Application Home
                (applications)
```

>El directorio Oracle Home (Oracle_Home) se debe establecer este directorio base en tu sistema y desde aqui, dos ramas deben ser creadas. El directorio **product** debera contener los archivos binarios de los productos y todos directorios de inicio de Oracle. El directorio **config** debera contener los datos de dominio y datos de la aplicacion.

Acerca del directorio **Oracle Home (_Oracle\_Home_)**.  

Cuando instalas cualquier producto de OFM, se le pedira que especifique un directorio _Oracle Home_. Este directorio funciona como un repositorio para archivos comunes que son usados por multiples productos de OFM instalados en la misma maquina. Por esta razon, el directorio _Oracle Home_ puede ser considerado como un directorio de soporte central para todos los productos de OFM instalados.  
El directorio _Oracle Home_ es referenciado como **_ORACLE\_HOME_** en la documentacion de OFM.

Acerca del directorio **Domain Home (_domains_)**.  

El _Domain Home_ es el directorio donde seran creados los dominios configurados. La ubicacion default del _Domain Home_ es _ORACLE\_HOME/user\_projects/domains/domain\_name_.  
El directorio _Domain Home_ es referenciado como **_DOMAIN\_HOME_** en la documentacion de OFM e incluye todos los directorios incluyendo el nombre del dominio. Por ejemplo si tu nombres tu dominio como _exampledomain_ y tu ubicas los datos de tu dominio en _/home/oracle/config/domains_, _DOMAIN\_HOME_ sera usado en la documentacion para referirse a _/home/oracle/config/domains_.  

Acerca del directorio **Application Home (_applications_)**.  

_Application Home_ es el directorio donde se crearan las aplicaciones relacionadas con los dominios que configuraste. La ubicacion default del _Application Home_ es _ORACLE\_HOME/user\_projects/applications/domain\_name_. Oracle recomienda ubicar tu _Application Home_ fuera del directorio _Oracle\_Home_  


>##NOTAS

####Archivos ~/.bashrc, ~/bash_profile, /etc/bashrc, /etc/profile####

---
Son shell scripts (archivos por lotes). Son ficheros que el sistema operativo ejecuta de forma automática cuando se da una cierta condición.
En el forndo lo que hace el sistema operativo es mandar a bash (el programa interprete de comandos más usual de Linux) ejecutar los archivos.
Podemos incluir en ellos cualquier orden de la linea de comandos.

+ Solo existe una sola copia de los archivos **/etc/profile** y **/etc/bashrc**.
+ Cada usuario tiene su propia copia de los archivos **.bashrc** y **.bash_profile**. (Estos archivos se encuentran en el directorio personal de cada usuario (**~**). El punto hace que estos archivos sean ocultos. Para ver si los tiene pruebe:
```shell
$ ls -a ~ 
```
+ Los archivos **/etc/profile** y **/etc/bashrc** afectan a todos los usuarios.Por tanto son gestionados por el administrador del sistema (**root**).

**Cual de ellos utilizar:**

Podemos clasificar estos cuatro archivos en función de si _los comandos que contienen_ afectan a un solo usuario o contrariamente todos los usuarios del sistema se ven afectados.

**Para todos los usuarios**: (Se necesita permisos de root para editar/modificar estos archivos)

**/etc/profile**: Se ejecuta cuando qualquier usuario inicia la sesión.
**/etc/bashrc**: Se ejecuta cada vez que qualquier usuario ejecuta el programa bash.

**Para nuestro usuario**:

**~/.bash_profile**: Se ejecuta el .bash_profile de juanito cuando juanito inicia su sesión.
**~/.bashrc**: Se ejecuta el .bashrc de juanito cuando juanito ejecuta el programa bash.

####Desinstalacion del BEA JRockit SKD####

--------

1. Colocarse un directorio antes al directorio que contiene el JRockit.
2. Ejecutar el siguiente comando.
```shell
$ rm -rf jrockit-24.5.0-j2sdk1.4.2_<version>
```
>Esto removerà el jdk del equipo

####Instalacion JDK (_Pendiente_)####

---------

1. Colocarse en el directorio de descarga del archivo de instalación. (user:soaadmin)

```shell
(soaadmin)$ tar zxvf jdk-8u<version>-linux-x64.tar.gz
```

Instalación de Oracle WebLogic y Oracle Coherence.
---  

Topologia estandar de Oracle Weblogic y Coherence.  

![Con titulo](http://drive.google.com/uc?export=view&id=0B43TL8clFj-nb2hUdl9iaWpORjQ "Topologia estandar Oracle Weblogic y Coherence")

+ **APPHOST**: Termino estandar en la documentacion de Oracle para la maquina que hospeda la capa de aplicacion.  
+ **WebLogic Domain**: Grupo de componentes java logicamente relacionados. En este caso _Administration Server_, _Managed Server_ y otros componentes de software relacionados.  
+ **Administration Server**: Entidad de control central de dominio. Mantiene la configuracion de los objetos del dominio y distribuye cambios de configuraciones a los _Managed Servers_.
+ **Cluster**: Coleccion de multiples instancias de WebLogic Servers corriendo simultaneamente y trabajando juntos.
+ **Machine**: Representacion logica de la computadora que hospeda uno o mas instancias de Weblogic Server (_servers_). Las maquinas tambien son el enlace logico entre los _Managed Servers_ y _Node Manager_; para empezar y detener un _Managed Server_ con Node Manager, el _Managed Server_ debe estar asociado con una maquina.
+ **Managed Server**: Hospeda tus aplicaciones, componentes de aplicaciones, servicios web y sus recursos asociados.

Pasos Instalacion de Oracle Weblogic y Coherence:
1.
2.
3.


Instalación de Oracle Fusion Middleware Infrastructure.
---  

Pasos Instalacion de Oracle Fusion Middleware Infrastructure:
1.
2.
3.