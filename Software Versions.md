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

Topología de Instalacion Estandar de OFM
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


Desinstalacion del BEA JRockit SKD
---
1. Colocarse un directorio antes al directorio que contiene el JRockit.
2. Ejecutar el siguiente comando.
```shell
$ rm -rf jrockit-24.5.0-j2sdk1.4.2_<version>
```
>Esto removerà el jdk del equipo

Instalacion JDK
---

1. Colocarse en el directorio de descarga del archivo de instalación. (user:soaadmin)

```shell
$
```
