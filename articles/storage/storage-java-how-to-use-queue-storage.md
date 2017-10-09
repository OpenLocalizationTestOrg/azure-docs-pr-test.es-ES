---
title: aaaHow toouse almacenamiento de cola de Java | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate del servicio de cola de Azure de toouse hello y colas de delete y insert, obtener y eliminar mensajes. Ejemplos escritos en Java."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2d5211ec5b6454f7dbc126aad4ba9950df13661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a>¿Cómo toouse almacenamiento de cola en Java
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio de almacenamiento de cola de Azure. ejemplos de Hello están escritos en Java y usar hello [almacenamiento de Azure SDK para Java][Azure Storage SDK for Java]. Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear** y **eliminar** colas. Para obtener más información sobre las colas, vea hello [pasos siguientes](#Next-Steps) sección.

Nota: hay un SDK disponible para los desarrolladores que usen el almacenamiento de Azure en dispositivos Android. Para obtener más información, vea hello [SDK de almacenamiento de Azure para Android][Azure Storage SDK for Android].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Creación de una aplicación Java
En esta guía utilizará funciones del almacenamiento que puede ejecutar en una aplicación Java localmente o bien mediante código a través de un rol web o un rol de trabajo de Azure.

toodo por lo tanto, necesitará tooinstall Hola Java Development Kit (JDK) y crear una cuenta de almacenamiento de Azure en su suscripción de Azure. Una vez que lo ha hecho, necesitará tooverify que el sistema de desarrollo cumple los requisitos mínimos de Hola y dependencias que se enumeran en hello [almacenamiento de Azure SDK para Java] [ Azure Storage SDK for Java] repositorio en GitHub. Si su sistema cumple estos requisitos, puede seguir las instrucciones de Hola para descargar e instalar Hola bibliotecas de almacenamiento de Azure para Java en el sistema de ese repositorio. Una vez haya completado estas tareas, será capaz de toocreate una aplicación Java que utiliza los ejemplos de hello en este artículo.

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurar el almacenamiento de cola de aplicación tooaccess
Agregue Hola después de la parte superior de toohello de instrucciones de importación del archivo de Java de Hola donde desea que las colas tooaccess de las API de almacenamiento de Azure de toouse:

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configuración de una cadena de conexión de almacenamiento de Azure
Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos. Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, con nombre de hello de la cuenta de almacenamiento y Hola clave de acceso principal para cuenta de almacenamiento Hola Hola [Portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores. Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

En una aplicación en ejecución dentro de un rol en Microsoft Azure, esta cadena puede almacenarse en el archivo de configuración del servicio de hello *ServiceConfiguration.cscfg*y puede tener acceso mediante una llamada a toohello  **RoleEnvironment.getConfigurationSettings** método. Este es un ejemplo de obtención de la cadena de conexión de Hola desde una **configuración** elemento denominado *StorageConnectionString* en el archivo de configuración de servicio de hello:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.

## <a name="how-to-create-a-queue"></a>Creación de una cola
Los objetos **CloudQueueClient** le permiten obtener objetos de referencia para las colas. Hello código siguiente se crea un **CloudQueueClient** objeto. (Nota: hay otras formas toocreate **CloudStorageAccount** objetos; para obtener más información, vea **CloudStorageAccount** en hello [referencia de SDK de cliente de almacenamiento de Azure].)

Hola de uso **CloudQueueClient** tooget una cola de toohello de referencia que desee toouse del objeto. Puede crear la cola de hello si no existe.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a>Cómo: agregar una cola de mensajes tooa
tooinsert un mensaje en una cola existente, primero debe crear un nuevo **CloudQueueMessage**. A continuación, llame a hello **addMessage** método. Se puede crear un **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes. Este es el código que crea una cola (si no existe) y el mensaje de bienvenida de inserciones "¡Hello, World".

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a>Cómo: consultar mensajes de bienvenida del siguiente
Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de hello mediante una llamada a **peekMessage**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Cómo: cambiar Hola contenido de un mensaje en cola
Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola. Si el mensaje de Hola representa una tarea de trabajo, puede usar este estado de la característica tooupdate Hola de tarea de trabajo de hello. Hola siguiente código actualiza el mensaje de bienvenida de cola con nuevo contenido y conjuntos de Hola tooextend de tiempo de espera de visibilidad otro 60 segundos. Esto guarda el estado de Hola de trabajos asociados con el mensaje de bienvenida y proporciona a cliente hello otro toocontinue minuto trabajando en el mensaje de bienvenida. Puede utilizar este flujos de trabajo de varios pasos de tootrack técnica sobre los mensajes en cola, sin necesidad de toostart a través de hello principio si se produce un error en un paso de procesamiento debido a un error toohardware o software. Normalmente, se mantendría también un número de reintentos y si hello mensaje se vuelve a intentar más de  *n*  veces, debería eliminarla. Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.

siguiente Hola búsquedas de ejemplo a través de la cola de Hola de mensajes de código, busca Hola primer mensaje coincide con "¡Hello, World" para el contenido de hello, a continuación, modifica el contenido del mensaje de Hola y se cierra.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Como alternativa, hello ejemplo de código siguiente actualiza solo Hola primera visible mensaje en cola Hola.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a>Cómo: obtener la longitud de cola de Hola
Puede obtener una estimación del número de Hola de mensajes en una cola. Hola **downloadAttributes** método pide al servicio de cola de Hola para varios valores actuales, incluido un recuento de cuántos mensajes se encuentran en una cola. recuento de Hello solo es aproximado porque los mensajes se pueden agregar o quitar después de hello servicio cola responde tooyour solicitud. Hola **getApproximateMessageCount** método devuelve el valor última Hola recuperado por llamada de hello demasiado**downloadAttributes**, sin llamar al servicio de cola de Hola.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a>Cómo: eliminación de cola de mensajes de bienvenida del siguiente
El código extrae un mensaje de una cola en dos pasos. Cuando se llama a **retrieveMessage**, obtendrá el siguiente mensaje de Hola en una cola. Un mensaje devuelto de **retrieveMessage** se convierte en invisible tooany otro código que lee mensajes de esta cola. De forma predeterminada, este mensaje permanece invisible durante 30 segundos. toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **deleteMessage**. Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo. Las llamadas de código **deleteMessage** justo después de que se ha procesado el mensaje de bienvenida.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a>Opciones adicionales para quitar mensajes de la cola
Hay dos formas de personalizar la recuperación de mensajes de una cola. En primer lugar, puede obtener un lote de mensajes (arriba too32). En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.

ejemplo de código siguiente Hello usa Hola **retrieveMessages** tooget 20 mensajes de método en una llamada. A continuación, procesa cada mensaje con un bucle **for** . También establece Hola invisibilidad tiempo de espera toofive minutos (300 segundos para cada mensaje). Tenga en cuenta que Hola cinco minutos se inicia para todos los mensajes en hello mismo tiempo, por lo que cuando cinco minutos transcurridos desde la llamada de hello demasiado**retrieveMessages**, los mensajes que no se eliminaron estará visibles de nuevo.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a>Cómo: enumerar las colas de Hola
una lista de colas actuales de hello, llamada hello tooobtain **CloudQueueClient.listQueues()** método, que devuelve una colección de **CloudQueue** objetos.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a>Cómo eliminar una cola
toodelete una cola y todos los mensajes de Hola contenidas en ella, llamada hello **deleteIfExists** método en hello **CloudQueue** objeto.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento.

* [SDK de Azure Storage para Java][Azure Storage SDK for Java]
* [referencia de SDK de cliente de almacenamiento de Azure][referencia de SDK de cliente de almacenamiento de Azure]
* [API de REST de servicios de Azure Storage][Azure Storage Services REST API]
* [Blog del equipo de Azure Storage][Azure Storage Team Blog]

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referencia de SDK de cliente de almacenamiento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
