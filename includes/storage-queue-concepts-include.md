## <a name="what-is-queue-storage"></a>¿Qué es el almacenamiento en cola?
Almacenamiento de la cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS. Un mensaje de la cola solo puede estar too64 KB de tamaño y una cola puede contener millones de mensajes, seguridad toohello límite de capacidad total de una cuenta de almacenamiento.

El almacenamiento en cola suele usarse para realizar las siguientes tareas:

* Crear un trabajo pendiente de tooprocess de trabajo de forma asincrónica
* Pasar mensajes de un rol de trabajador de Azure de tooan de rol web de Azure

## <a name="queue-service-concepts"></a>Conceptos del servicio Cola
Hola servicio cola contiene Hola de los componentes siguientes:

![Cola1](./media/storage-queue-concepts-include/queue1.png)

* **Formato de dirección URL:** las colas son direccionables mediante Hola siguiendo el formato de dirección URL:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Hola después de la dirección URL de direcciones una cola en el diagrama de hello:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Cuenta de almacenamiento:** todos los accesos tooAzure almacenamiento se realiza a través de una cuenta de almacenamiento. Consulte [Objetivos de escalabilidad y rendimiento del almacenamiento de Azure](../articles/storage/common/storage-scalability-targets.md) para obtener información sobre la capacidad de la cuenta de almacenamiento.
* **Cola:** una cola contiene un conjunto de mensajes. Todos los mensajes deben encontrarse en una cola. Tenga en cuenta que ese nombre de cola de hello debe estar en minúsculas. Para más información, consulte [Asignar nombres a colas y metadatos](https://msdn.microsoft.com/library/azure/dd179349.aspx).
* **Mensaje:** un mensaje, en cualquier formato, de seguridad too64 KB. tiempo máximo de Hola que un mensaje puede permanecer en la cola de hello es 7 días.

