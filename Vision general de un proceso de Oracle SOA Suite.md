##Retos de negocio y Oracle SOA Suite##

###Retos de negocio de la _Compañia X_###

>Este capítulo describe los retos de negocio a los que se enfrenta la _Compañia X_ y como **Oracle SOA Suite** provee una solución de negocio para estos retos.

La Compañia X debe mejorar su sistema de procesamiento de pedidos para acomodar el crecimiento de varios canales con los socios de negocios en línea, se ha previsto una expansion agresiva de tiendas. Lo sistemas deben ser consolidados para proporcionar una mejor visibilidad del proceso de extremo a extremo, de inicio al fin del mismo.

Requerimientos para la mejora del sistema de procesamiento de pedidos:
+ El sistema de procesamiento de pedidos debe ser accesible a través de multiples protocolos, formato de datos, y tipos de clientes, incluyendo dispositivos móviles:
    * Las tendencias de negocio indican que la compañia debe lanzar proximamente una aplicacion móvil y el servicio de pedidos debe soportar el acceso atraves de API RESTful.
    * En complemento a la tienda directa en linea, la compañia planea lanzar un servicio en el cual los pedidos son recibidos a traves de diferentes canales (como archivos de valores batch comandos-separados (CSV) sobre FTP). 
    * La compañia debe interactuar con los socios comerciales y proporcionar la interfaz de datos electronicos de apoyo (EDI).
    * Para pedidos grandes, el historial de credito del cliente debe ser comprobado antes de enviar el pedido, de otra manera el pedido es rechazado. Inicialmente, el credito es revisado por el departamento interno, pero despues debe ser integrado con paypal. El cambio de los provedores de credito no debe interrumpir las operaciones de pedidos.
    * El sistema de pedidos debe proporcionar integracion directa con el departamento de embalaje para enviar los pedidos con los proveedores de envio preferidos en funcion al tipo de servicio de envio.
    * El proceso de entrega debe funcionar de acuerdo con un horario de recogida predefinido.
    * Tras el proceso de entrega que se envia al departamento de empaquetado, un mensaje debe ser enviado al cliente.

###Soluciones de negocio de la _Compañia X_###

>Este capitulo describe como la _compañia X_ usas las capacidades de Oracle SOA Suite para hacer frente a sus retos de negocio.

Frente a los desafios de negocio:  
1. La _compañia X_ diseña un compuesto de validacion de tarjeta de credito, para validar pagos y retornar el estatus del pago. Si el pago es rechazado, una orden no es procesada. **Oracle Service Bus** es integrado con el compuesto para proporcionar inscripcion y seguridad.  
2. La _compañia X_ diseña una aplicacion compuesta para aceptar nuevas ordenes de compra, autorizar o denegarlas, y remitir los pedidos autorizados a otro compuesto de manejo de pedidos. **Oracle Service Bus** hace el compuesto de procesamiento de pedidos disponible sobre varios protocolos y formato de datos, y valida el pedido.  
3. La _compañia X_ diseña un pipeline de **Oracle Service Bus** para conectar un servicio proxy a un canal de archivos de pedido. El proxy maneja los pedidos entrantes por archivo.  
4. La _compañia X_ diseña un proceso **BPEL** que establece el estado de un pedido a enviar, notifica al cliente que el pedido ha sido enviado y actualiza el estatus del pedido en la base de datos. Este proceso esta conectado a un servicio con interfaz **REST** de entrada que define un recurso de envio.  
5. La _compañia X_ diseña un compuesto para el procesamiento de pedidos para escuchar los pedidos a procesar, selecciona un provedor de envio e invoca el servicio de empaquetado y en vio diseñado en _empaquetado y envio de pedidos_.  
6. La _compañia X_ diseña un compuesto de consulta de inventario para identificar el total de elementos para cada producto ordenado  para una categoria. **Oracle Enterprise Scheduler** es usado para definir una tarea de un servicio web para el compuesto de consulta de inventario y entonces enviar la tarea con una planificacion para ejecutar en un momento determinado.  
7. La _compañia X_ diseña un flujo de transferencia de archivos de **Oracle Manage File Transfer** para recibir archivos y escribirlos a un archivo de sistema usando el servidor FTP integrado de gestion de transferencia de archivos. **Oracle Manage File Transfer** invoca un servicio de transferencia de archivos en un compuesto y dinamicamente decide basado en el tamaño del archivo si pasa el contenido en linea o por referencia.  
8. La _compañia X_ usa la consola de **Oracle B2B** para construir un documento de flujo que acepta una orden _EDI XML_ de un socio comercial remoto.  
9. La _compañia X_ desina una aplicacion **Oracle Event Processing** para proporcionar analisis en tiempo real de los pedidos (eventos) de clientes reconocidos especificamente por una direccion asociada de email.  
10. Como cada pedido (evento) se pasa al servidor de **Oracle Event Processing**, se accede de forma dinamica para detectar una posible actividad fraudulenta, mediante la observacion de patrones de eventos con una cantidad en dolares acumulados por pedido que supere los $1000 en cualquier periodo de 24 hrs.  
