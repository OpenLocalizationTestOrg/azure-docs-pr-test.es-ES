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
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="fc460-104">¿Cómo toouse almacenamiento de cola de PHP</span><span class="sxs-lookup"><span data-stu-id="fc460-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="fc460-105">Información general</span><span class="sxs-lookup"><span data-stu-id="fc460-105">Overview</span></span>
<span data-ttu-id="fc460-106">Esta guía le mostrará cómo tooperform escenarios comunes al usar Hola servicio de almacenamiento de cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc460-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="fc460-107">ejemplos de Hola se escriben a través de las clases del SDK de Windows hello para PHP.</span><span class="sxs-lookup"><span data-stu-id="fc460-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="fc460-108">Hello cubiertos escenarios incluyen Insertar, inspeccionar, introducción y eliminar mensajes de la cola, así como la creación y eliminación de colas.</span><span class="sxs-lookup"><span data-stu-id="fc460-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="fc460-109">Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="fc460-109">Create a PHP application</span></span>
<span data-ttu-id="fc460-110">Hola solo requisito para crear una aplicación PHP que tiene acceso a almacenamiento de la cola de Azure es hello que hacen referencia a clases de hello Azure SDK para PHP desde dentro del código.</span><span class="sxs-lookup"><span data-stu-id="fc460-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="fc460-111">Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación, incluso el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="fc460-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="fc460-112">En esta guía, usará funciones del servicio Cola a las que se puede llamar desde una aplicación PHP localmente o bien mediante código a través de un rol web, rol de trabajo o sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc460-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="fc460-113">Obtener Hola bibliotecas de cliente de Azure</span><span class="sxs-lookup"><span data-stu-id="fc460-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="fc460-114">Configurar el almacenamiento de la cola de aplicación tooaccess</span><span class="sxs-lookup"><span data-stu-id="fc460-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="fc460-115">Hola toouse API para el almacenamiento de colas de Azure, necesita:</span><span class="sxs-lookup"><span data-stu-id="fc460-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="fc460-116">Archivo de cargador automático de hello de referencia mediante el uso de Hola [require_once] instrucción.</span><span class="sxs-lookup"><span data-stu-id="fc460-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="fc460-117">Hacer referencia a todas las clases que puede que use.</span><span class="sxs-lookup"><span data-stu-id="fc460-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="fc460-118">Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático **ServicesBuilder** clase.</span><span class="sxs-lookup"><span data-stu-id="fc460-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="fc460-119">En este ejemplo (y otros ejemplos de este artículo) se da por supuesto que ha instalado Hola PHP bibliotecas de cliente de Azure a través del compositor.</span><span class="sxs-lookup"><span data-stu-id="fc460-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="fc460-120">Si instala las bibliotecas de hello manualmente, tendrá hello tooreference `WindowsAzure.php` archivo cargador automático.</span><span class="sxs-lookup"><span data-stu-id="fc460-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="fc460-121">En los siguientes ejemplos de hello, Hola `require_once` instrucción se muestran siempre, pero solo las clases de Hola que son necesarias para tooexecute de ejemplo de Hola se hará referencia.</span><span class="sxs-lookup"><span data-stu-id="fc460-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="fc460-122">Configuración de una conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="fc460-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="fc460-123">tooinstantiate un cliente de almacenamiento de cola de Azure, primero debe tener una cadena de conexión válida.</span><span class="sxs-lookup"><span data-stu-id="fc460-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="fc460-124">formato de Hello para la cadena de conexión de servicio de cola de hello es el siguiente.</span><span class="sxs-lookup"><span data-stu-id="fc460-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="fc460-125">Para obtener acceso a un servicio en directo:</span><span class="sxs-lookup"><span data-stu-id="fc460-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="fc460-126">Para acceder al almacenamiento de emulador de hello:</span><span class="sxs-lookup"><span data-stu-id="fc460-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="fc460-127">toocreate cualquier cliente de servicio de Azure, necesita hello toouse **ServicesBuilder** clase.</span><span class="sxs-lookup"><span data-stu-id="fc460-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="fc460-128">Puede utilizar cualquiera de hello siguientes técnicas:</span><span class="sxs-lookup"><span data-stu-id="fc460-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="fc460-129">Pasar Hola conexión directamente cadena tooit.</span><span class="sxs-lookup"><span data-stu-id="fc460-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="fc460-130">Use **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="fc460-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="fc460-131">de manera predeterminada, admite un origen externo: variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="fc460-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="fc460-132">Puede agregar nuevos orígenes de extendiendo hello **ConnectionStringSource** clase.</span><span class="sxs-lookup"><span data-stu-id="fc460-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="fc460-133">Para obtener ejemplos de hello descritos a continuación, cadena de conexión de Hola se pasará directamente.</span><span class="sxs-lookup"><span data-stu-id="fc460-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="fc460-134">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="fc460-134">Create a queue</span></span>
<span data-ttu-id="fc460-135">A **QueueRestProxy** objeto le permite crear una cola mediante el uso de hello **createQueue** método.</span><span class="sxs-lookup"><span data-stu-id="fc460-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="fc460-136">Cuando se crea una cola, puede establecer opciones en cola hello, pero al hacerlo, por lo tanto, no es necesario.</span><span class="sxs-lookup"><span data-stu-id="fc460-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="fc460-137">(Hola el ejemplo siguiente se muestra cómo tooset metadatos en una cola.)</span><span class="sxs-lookup"><span data-stu-id="fc460-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="fc460-138">No debe confiar en la distinción entre minúsculas y mayúsculas para las claves de metadatos.</span><span class="sxs-lookup"><span data-stu-id="fc460-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="fc460-139">Todas las claves se leen desde el servicio de hello en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="fc460-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="fc460-140">Agregar una cola de mensajes tooa</span><span class="sxs-lookup"><span data-stu-id="fc460-140">Add a message tooa queue</span></span>
<span data-ttu-id="fc460-141">usar tooadd una cola de mensajes tooa, **QueueRestProxy -> createMessage**.</span><span class="sxs-lookup"><span data-stu-id="fc460-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="fc460-142">método Hello toma el nombre de la cola de hello, el texto del mensaje de Hola y opciones de mensaje (que son opcionales).</span><span class="sxs-lookup"><span data-stu-id="fc460-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="fc460-143">Consultar mensajes de bienvenida del siguiente</span><span class="sxs-lookup"><span data-stu-id="fc460-143">Peek at hello next message</span></span>
<span data-ttu-id="fc460-144">Puede inspeccionar en un mensaje (o mensajes) en la parte delantera de Hola de una cola sin quitarlo de la cola de hello mediante una llamada a **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="fc460-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="fc460-145">De forma predeterminada, Hola **peekMessage** método devuelve un único mensaje, pero puede cambiar ese valor mediante hello **PeekMessagesOptions -> setNumberOfMessages** método.</span><span class="sxs-lookup"><span data-stu-id="fc460-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="fc460-146">Eliminación de la cola mensajes de bienvenida del siguiente</span><span class="sxs-lookup"><span data-stu-id="fc460-146">De-queue hello next message</span></span>
<span data-ttu-id="fc460-147">El código borra un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="fc460-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="fc460-148">En primer lugar, se llama a **QueueRestProxy -> listMessages**, lo que hace tooany invisible de mensaje de Hola otro código que se está leyendo desde la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc460-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="fc460-149">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="fc460-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="fc460-150">(Si no se elimina el mensaje de bienvenida en este período de tiempo, dejará de estar visible en la cola de hello nuevo.) toofinish al quitar el mensaje de saludo de cola de hello, debe llamar a **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="fc460-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="fc460-151">Este proceso de dos pasos de la eliminación de un mensaje garantiza cuando los tooprocess se produce un error de código puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje e inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="fc460-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="fc460-152">Las llamadas de código **deleteMessage** justo después de que se ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="fc460-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="fc460-153">Cambiar el contenido de Hola de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="fc460-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="fc460-154">Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de hello mediante una llamada a **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="fc460-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="fc460-155">Si el mensaje de Hola representa una tarea de trabajo, puede usar este estado de la característica tooupdate Hola de tarea de trabajo de hello.</span><span class="sxs-lookup"><span data-stu-id="fc460-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="fc460-156">Hola siguiente código actualiza el mensaje de bienvenida de cola con nuevo contenido y establece tooextend de tiempo de espera de visibilidad de hello otro 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="fc460-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="fc460-157">Esto guarda el estado de Hola de trabajo que esté asociada con el mensaje de bienvenida y da a cliente hello otro toocontinue minuto trabajando en el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="fc460-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="fc460-158">Puede utilizar este flujos de trabajo de varios pasos de tootrack técnica sobre los mensajes en cola, sin necesidad de toostart a través de hello principio si se produce un error en un paso de procesamiento debido a un error toohardware o software.</span><span class="sxs-lookup"><span data-stu-id="fc460-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="fc460-159">Normalmente, se mantendría también un número de reintentos y si hello mensaje se vuelve a intentar más de  *n*  veces, debería eliminarla.</span><span class="sxs-lookup"><span data-stu-id="fc460-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="fc460-160">Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.</span><span class="sxs-lookup"><span data-stu-id="fc460-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="fc460-161">Opciones adicionales para quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="fc460-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="fc460-162">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="fc460-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="fc460-163">En primer lugar, puede obtener un lote de mensajes (arriba too32).</span><span class="sxs-lookup"><span data-stu-id="fc460-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="fc460-164">En segundo lugar, puede establecer un tiempo de espera de visibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="fc460-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="fc460-165">ejemplo de código siguiente Hello usa Hola **getMessages** mensajes tooget 16 de método en una llamada.</span><span class="sxs-lookup"><span data-stu-id="fc460-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="fc460-166">A continuación, procesa cada mensaje con un bucle **for** .</span><span class="sxs-lookup"><span data-stu-id="fc460-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="fc460-167">También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="fc460-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="fc460-168">longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="fc460-168">Get queue length</span></span>
<span data-ttu-id="fc460-169">Puede obtener una estimación del número de Hola de mensajes en una cola.</span><span class="sxs-lookup"><span data-stu-id="fc460-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="fc460-170">Hola **QueueRestProxy -> getQueueMetadata** método pide Hola cola servicio tooreturn metadatos acerca de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc460-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="fc460-171">Llamar a hello **getApproximateMessageCount** método en hello devolvió el objeto proporciona un recuento de cuántos mensajes se encuentran en la cola.</span><span class="sxs-lookup"><span data-stu-id="fc460-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="fc460-172">recuento de Hello solo es aproximado porque los mensajes se pueden agregar o quitar después de servicio de cola de hello responde tooyour solicitud.</span><span class="sxs-lookup"><span data-stu-id="fc460-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="fc460-173">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="fc460-173">Delete a queue</span></span>
<span data-ttu-id="fc460-174">toodelete una cola y todos los mensajes de Hola en ella, llame a hello **QueueRestProxy -> deleteQueue** método.</span><span class="sxs-lookup"><span data-stu-id="fc460-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fc460-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc460-175">Next steps</span></span>
<span data-ttu-id="fc460-176">Ahora que conoce los fundamentos de Hola de almacenamiento de la cola de Azure, siga estas toolearn vínculos acerca de las tareas más complejas de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="fc460-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="fc460-177">Visite hello [blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="fc460-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="fc460-178">Para obtener más información, vea también hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="fc460-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

