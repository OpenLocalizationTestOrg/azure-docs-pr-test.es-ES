---
title: almacenamiento (C++) en la cola toouse aaaHow | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola servicio de almacenamiento de cola en Azure. Los ejemplos están escritos en C++."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: b0cddf017878e9fab87f47d24b2906e40c9f4ad5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a>¿Cómo toouse almacenamiento de cola desde C++
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio de almacenamiento de cola de Azure. ejemplos de Hello están escritos en C++ y usar hello [biblioteca de cliente de almacenamiento de Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear y eliminar colas**.

> [!NOTE]
> Destinos de esta guía Hola biblioteca de cliente de almacenamiento de Azure para C++ versión 1.0.0 y versiones posteriores. Hola recomienda versión es la biblioteca de cliente de almacenamiento 2.2.0, que está disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](http://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Creación de una aplicación de C++
En esta guía, usará las características de almacenamiento que se pueden ejecutar en una aplicación C++.

toodo por lo tanto, necesitará tooinstall Hola biblioteca de cliente de almacenamiento de Azure para C++ y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.

Hola tooinstall biblioteca de cliente de almacenamiento de Azure para C++, puede usar Hola siguientes métodos:

* **Linux:** seguir instrucciones Hola de hello [biblioteca de cliente de almacenamiento de Azure para C++ Léame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.
* **Windows:** en Visual Studio, haga clic en **Herramientas &gt; Administrador de paquetes de NuGet &gt; Consola del Administrador de paquetes**. Escriba lo siguiente Hola de comandos en hello [consola de administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione **ENTRAR**.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurar el almacenamiento de la cola de aplicación tooaccess
Agregue la siguiente Hola incluye la parte superior de toohello de las instrucciones del archivo de C++ de Hola donde desea que las colas tooaccess de las API de toouse Hola almacenamiento de Azure:  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configuración de una cadena de conexión de Almacenamiento de Azure
Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos. Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, utilizando el nombre de Hola de su clave de acceso almacenamiento hello y cuenta de almacenamiento para cuenta de almacenamiento Hola Hola [Portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores. Para obtener información sobre las cuentas de almacenamiento y las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json). Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest la aplicación en el equipo local de Windows, puede usar Microsoft Azure hello [emulador de almacenamiento](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) que se instala con hello [Azure SDK](https://azure.microsoft.com/downloads/). emulador de almacenamiento de Hello es una utilidad que simula los servicios de Blob, cola y tabla de hello disponibles en Azure en su equipo de desarrollo local. Hello en el ejemplo siguiente se muestra cómo se puede declarar un emulador de almacenamiento local de campo estático toohold Hola conexión cadena tooyour:  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

emulador de almacenamiento de Azure de hello toostart, seleccione hello **iniciar** Hola o presionen **Windows** clave. Comience a escribir **emulador de almacenamiento de Azure**y seleccione **emulador de almacenamiento de Microsoft Azure** de lista de Hola de aplicaciones.

Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.

## <a name="retrieve-your-connection-string"></a>Recuperación de la cadena de conexión
Puede usar hello **cloud_storage_account** clase toorepresent información de su cuenta de almacenamiento. tooretrieve información de cadena de conexión de almacenamiento de hello de la cuenta de almacenamiento, puede utilizar hello **analizar** método.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>Creación de una cola
Los objetos **cloud_queue_client** le permiten obtener objetos de referencia para las colas. Hello código siguiente se crea un **cloud_queue_client** objeto.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

Hola de uso **cloud_queue_client** tooget una cola de toohello de referencia que desee toouse del objeto. Puede crear la cola de hello si no existe.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Cómo insertar un mensaje en una cola
tooinsert un mensaje en una cola existente, primero debe crear un nuevo **cloud_queue_message**. A continuación, llame a hello **add_message** método. Se puede crear un **cloud_queue_message** a partir de una cadena o de una matriz de **byte**. Este es el código que crea una cola (si no existe) y el mensaje de bienvenida de inserciones "¡Hello, World":

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a>Cómo: consultar mensajes de bienvenida del siguiente
Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **peek_message** método.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Cómo: cambiar Hola contenido de un mensaje en cola
Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola. Si el mensaje de Hola representa una tarea de trabajo, puede usar este estado de la característica tooupdate Hola de tarea de trabajo de hello. Hola siguiente código actualiza el mensaje de bienvenida de cola con nuevo contenido y conjuntos de Hola tooextend de tiempo de espera de visibilidad otro 60 segundos. Esto guarda el estado de Hola de trabajos asociados con el mensaje de bienvenida y proporciona a cliente hello otro toocontinue minuto trabajando en el mensaje de bienvenida. Puede utilizar este flujos de trabajo de varios pasos de tootrack técnica sobre los mensajes en cola, sin necesidad de toostart a través de hello principio si se produce un error en un paso de procesamiento debido a un error toohardware o software. Por lo general, puede hacer que un número de reintentos así y si el mensaje de bienvenida se vuelve a intentar más de n veces, debería eliminarla. Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a>Cómo: eliminación de la cola mensajes de bienvenida del siguiente
El código quita un mensaje de una cola en dos pasos. Cuando se llama a **get_message**, obtendrá el siguiente mensaje de Hola en una cola. Un mensaje devuelto de **get_message** se convierte en invisible tooany otro código que lee mensajes de esta cola. toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **delete_message**. Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo. Las llamadas de código **delete_message** justo después de que se ha procesado el mensaje de bienvenida.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>Cómo usar las opciones adicionales para quitar mensajes de la cola
Hay dos formas de personalizar la recuperación de mensajes de una cola. En primer lugar, puede obtener un lote de mensajes (arriba too32). En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje. ejemplo de código siguiente Hello usa Hola **get_messages** tooget 20 mensajes de método en una llamada. A continuación, procesa cada mensaje con un bucle **for** . También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje. Tenga en cuenta que Hola 5 minutos se inicia para todos los mensajes en hello mismo tiempo, por lo que tras 5 minutos transcurridos desde la llamada de hello demasiado**get_messages**, los mensajes que no se eliminaron estará visibles de nuevo.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a>Cómo: obtener la longitud de cola de Hola
Puede obtener una estimación del número de Hola de mensajes en una cola. Hola **download_attributes** método pide tooretrieve de servicio de cola de hello atributos de la cola de hello, incluido el número de mensajes de Hola. Hola **approximate_message_count** método obtiene el número aproximado de Hola de mensajes en cola de Hola.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a>Cómo eliminar una cola
toodelete una cola y todos los mensajes de Hola contenidos en él, llamada hello **delete_queue_if_exists** método hello en objetos de cola.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn de vínculos más sobre el almacenamiento de Azure.

* [¿Cómo toouse almacenamiento de blobs de C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de tablas de C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Enumeración de los recursos de almacenamiento de Azure en C++](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Referencia de la biblioteca de clientes de almacenamiento para C++](http://azure.github.io/azure-storage-cpp)
* [Documentación de Almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/)