---
title: aaaHow toouse almacenamiento de cola desde PHP | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate de servicio de almacenamiento de toouse Hola cola de Azure y colas de delete y insert, obtener y eliminar mensajes. Los ejemplos están escritos en C++."
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 8daabcc9b3b4de121a309f21bb3325242cff06f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a>¿Cómo toouse almacenamiento de cola de PHP
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes al usar Hola servicio de almacenamiento de cola de Azure. ejemplos de Hola se escriben a través de las clases del SDK de Windows hello para PHP. Hello cubiertos escenarios incluyen Insertar, inspeccionar, introducción y eliminar mensajes de la cola, así como la creación y eliminación de colas.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Creación de una aplicación PHP
Hola solo requisito para crear una aplicación PHP que tiene acceso a almacenamiento de la cola de Azure es hello que hacen referencia a clases de hello Azure SDK para PHP desde dentro del código. Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación, incluso el Bloc de notas.

En esta guía, usará funciones del servicio Cola a las que se puede llamar desde una aplicación PHP localmente o bien mediante código a través de un rol web, rol de trabajo o sitio web de Azure.

## <a name="get-hello-azure-client-libraries"></a>Obtener Hola bibliotecas de cliente de Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurar el almacenamiento de la cola de aplicación tooaccess
Hola toouse API para el almacenamiento de colas de Azure, necesita:

1. Archivo de cargador automático de hello de referencia mediante el uso de Hola [require_once] instrucción.
2. Hacer referencia a todas las clases que puede que use.

Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático **ServicesBuilder** clase.

> [!NOTE]
> En este ejemplo (y otros ejemplos de este artículo) se da por supuesto que ha instalado Hola PHP bibliotecas de cliente de Azure a través del compositor. Si instala las bibliotecas de hello manualmente, tendrá hello tooreference `WindowsAzure.php` archivo cargador automático.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

En los siguientes ejemplos de hello, Hola `require_once` instrucción se muestran siempre, pero solo las clases de Hola que son necesarias para tooexecute de ejemplo de Hola se hará referencia.

## <a name="set-up-an-azure-storage-connection"></a>Configuración de una conexión de Almacenamiento de Azure
tooinstantiate un cliente de almacenamiento de cola de Azure, primero debe tener una cadena de conexión válida. formato de Hello para la cadena de conexión de servicio de cola de hello es el siguiente.

Para obtener acceso a un servicio en directo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Para acceder al almacenamiento de emulador de hello:

```php
UseDevelopmentStorage=true
```

toocreate cualquier cliente de servicio de Azure, necesita hello toouse **ServicesBuilder** clase. Puede utilizar cualquiera de hello siguientes técnicas:

* Pasar Hola conexión directamente cadena tooit.
* Use **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:
  * de manera predeterminada, admite un origen externo: variables de entorno.
  * Puede agregar nuevos orígenes de extendiendo hello **ConnectionStringSource** clase.

Para obtener ejemplos de hello descritos a continuación, cadena de conexión de Hola se pasará directamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Creación de una cola
A **QueueRestProxy** objeto le permite crear una cola mediante el uso de hello **createQueue** método. Cuando se crea una cola, puede establecer opciones en cola hello, pero al hacerlo, por lo tanto, no es necesario. (Hola el ejemplo siguiente se muestra cómo tooset metadatos en una cola.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> No debe confiar en la distinción entre minúsculas y mayúsculas para las claves de metadatos. Todas las claves se leen desde el servicio de hello en minúsculas.
> 
> 

## <a name="add-a-message-tooa-queue"></a>Agregar una cola de mensajes tooa
usar tooadd una cola de mensajes tooa, **QueueRestProxy -> createMessage**. método Hello toma el nombre de la cola de hello, el texto del mensaje de Hola y opciones de mensaje (que son opcionales).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-hello-next-message"></a>Consultar mensajes de bienvenida del siguiente
Puede inspeccionar en un mensaje (o mensajes) en la parte delantera de Hola de una cola sin quitarlo de la cola de hello mediante una llamada a **QueueRestProxy -> peekMessages**. De forma predeterminada, Hola **peekMessage** método devuelve un único mensaje, pero puede cambiar ese valor mediante hello **PeekMessagesOptions -> setNumberOfMessages** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-hello-next-message"></a>Eliminación de la cola mensajes de bienvenida del siguiente
El código borra un mensaje de una cola en dos pasos. En primer lugar, se llama a **QueueRestProxy -> listMessages**, lo que hace tooany invisible de mensaje de Hola otro código que se está leyendo desde la cola de Hola. De forma predeterminada, este mensaje permanece invisible durante 30 segundos. (Si no se elimina el mensaje de bienvenida en este período de tiempo, dejará de estar visible en la cola de hello nuevo.) toofinish al quitar el mensaje de saludo de cola de hello, debe llamar a **QueueRestProxy -> deleteMessage**. Este proceso de dos pasos de la eliminación de un mensaje garantiza cuando los tooprocess se produce un error de código puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje e inténtelo de nuevo. Las llamadas de código **deleteMessage** justo después de que se ha procesado el mensaje de bienvenida.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-hello-contents-of-a-queued-message"></a>Cambiar el contenido de Hola de un mensaje en cola
Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de hello mediante una llamada a **QueueRestProxy -> updateMessage**. Si el mensaje de Hola representa una tarea de trabajo, puede usar este estado de la característica tooupdate Hola de tarea de trabajo de hello. Hola siguiente código actualiza el mensaje de bienvenida de cola con nuevo contenido y establece tooextend de tiempo de espera de visibilidad de hello otro 60 segundos. Esto guarda el estado de Hola de trabajo que esté asociada con el mensaje de bienvenida y da a cliente hello otro toocontinue minuto trabajando en el mensaje de bienvenida. Puede utilizar este flujos de trabajo de varios pasos de tootrack técnica sobre los mensajes en cola, sin necesidad de toostart a través de hello principio si se produce un error en un paso de procesamiento debido a un error toohardware o software. Normalmente, se mantendría también un número de reintentos y si hello mensaje se vuelve a intentar más de  *n*  veces, debería eliminarla. Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a>Opciones adicionales para quitar mensajes de la cola
Hay dos formas de personalizar la recuperación de mensajes de una cola. En primer lugar, puede obtener un lote de mensajes (arriba too32). En segundo lugar, puede establecer un tiempo de espera de visibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje. ejemplo de código siguiente Hello usa Hola **getMessages** mensajes tooget 16 de método en una llamada. A continuación, procesa cada mensaje con un bucle **for** . También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a>longitud de la cola
Puede obtener una estimación del número de Hola de mensajes en una cola. Hola **QueueRestProxy -> getQueueMetadata** método pide Hola cola servicio tooreturn metadatos acerca de la cola de Hola. Llamar a hello **getApproximateMessageCount** método en hello devolvió el objeto proporciona un recuento de cuántos mensajes se encuentran en la cola. recuento de Hello solo es aproximado porque los mensajes se pueden agregar o quitar después de servicio de cola de hello responde tooyour solicitud.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a>Eliminación de una cola
toodelete una cola y todos los mensajes de Hola en ella, llame a hello **QueueRestProxy -> deleteQueue** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de almacenamiento de la cola de Azure, siga estas toolearn vínculos acerca de las tareas más complejas de almacenamiento:

* Visite hello [blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/).

Para obtener más información, vea también hello [Centro para desarrolladores de PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

