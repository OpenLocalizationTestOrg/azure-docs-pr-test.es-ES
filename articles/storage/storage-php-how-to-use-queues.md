---
title: Uso de Queue Storage en PHP | Microsoft Docs
description: "Aprenda a usar el servicio Cola de Azure para crear y eliminar colas e insertar, obtener y eliminar mensajes. Los ejemplos están escritos en C++."
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
ms.openlocfilehash: 3c8f799a917cfc9d74412d90f27f2ea8c21265d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="dd963-104">Uso del almacenamiento de colas de PHP</span><span class="sxs-lookup"><span data-stu-id="dd963-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="dd963-105">Información general</span><span class="sxs-lookup"><span data-stu-id="dd963-105">Overview</span></span>
<span data-ttu-id="dd963-106">Esta guía muestra cómo realizar algunas tareas comunes a través del servicio de almacenamiento Cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd963-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="dd963-107">Los ejemplos están escritos con las clases del SDK de Windows para PHP.</span><span class="sxs-lookup"><span data-stu-id="dd963-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="dd963-108">Entre los escenarios descritos se incluyen insertar, ojear, obtener y eliminar mensajes de la cola, así como crear y eliminar colas.</span><span class="sxs-lookup"><span data-stu-id="dd963-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="dd963-109">Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="dd963-109">Create a PHP application</span></span>
<span data-ttu-id="dd963-110">El único requisito a la hora de crear una aplicación PHP para obtener acceso al servicio Cola de Azure es que el código haga referencia a clases del SDK de Azure para PHP desde el código.</span><span class="sxs-lookup"><span data-stu-id="dd963-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="dd963-111">Puede utilizar cualquier herramienta de desarrollo para crear la aplicación, incluido el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="dd963-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="dd963-112">En esta guía, usará funciones del servicio Cola a las que se puede llamar desde una aplicación PHP localmente o bien mediante código a través de un rol web, rol de trabajo o sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd963-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="dd963-113">Obtención de las bibliotecas de clientes de Azure</span><span class="sxs-lookup"><span data-stu-id="dd963-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="dd963-114">Configuración de la aplicación para obtener acceso al almacenamiento en cola</span><span class="sxs-lookup"><span data-stu-id="dd963-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="dd963-115">Para usar las API de almacenamiento en cola de Azure, necesitará:</span><span class="sxs-lookup"><span data-stu-id="dd963-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="dd963-116">Hacer referencia al archivo autocargador mediante la instrucción [require_once].</span><span class="sxs-lookup"><span data-stu-id="dd963-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="dd963-117">Hacer referencia a todas las clases que puede que use.</span><span class="sxs-lookup"><span data-stu-id="dd963-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="dd963-118">En el siguiente ejemplo se muestra cómo incluir el archivo autocargador y hacer referencia a la clase **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="dd963-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="dd963-119">En este ejemplo (así como en otros ejemplos de este artículo), se asume que ha instalado las bibliotecas de clientes PHP para Azure mediante el Compositor.</span><span class="sxs-lookup"><span data-stu-id="dd963-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="dd963-120">Si las instaló manualmente, deberá hacer referencia al archivo del cargador automático `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="dd963-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="dd963-121">En los ejemplos que aparecen a continuación, la instrucción `require_once` aparecerá siempre, pero solo se hará referencia a las clases necesarias para la ejecución del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="dd963-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="dd963-122">Configuración de una conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="dd963-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="dd963-123">Para crear una instancia de un cliente de almacenamiento en cola de Azure, primero debe disponer de una cadena de conexión válida.</span><span class="sxs-lookup"><span data-stu-id="dd963-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="dd963-124">El formato de las cadenas de conexión del servicio Cola es:</span><span class="sxs-lookup"><span data-stu-id="dd963-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="dd963-125">Para obtener acceso a un servicio en directo:</span><span class="sxs-lookup"><span data-stu-id="dd963-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="dd963-126">Para obtener acceso al emulador de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="dd963-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="dd963-127">Para crear un cliente de cualquier servicio de Azure, debe usar la clase **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="dd963-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="dd963-128">Puede usar cualquiera de las técnicas siguientes:</span><span class="sxs-lookup"><span data-stu-id="dd963-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="dd963-129">pasarle directamente la cadena de conexión, o bien</span><span class="sxs-lookup"><span data-stu-id="dd963-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="dd963-130">usar **CloudConfigurationManager (CCM)** para buscar la cadena de conexión en varios orígenes externos:</span><span class="sxs-lookup"><span data-stu-id="dd963-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="dd963-131">de manera predeterminada, admite un origen externo: variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="dd963-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="dd963-132">para agregar nuevos orígenes, amplíe la clase **ConnectionStringSource**</span><span class="sxs-lookup"><span data-stu-id="dd963-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="dd963-133">En los ejemplos descritos aquí, la cadena de conexión se pasará directamente.</span><span class="sxs-lookup"><span data-stu-id="dd963-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="dd963-134">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="dd963-134">Create a queue</span></span>
<span data-ttu-id="dd963-135">Un objeto **QueueRestProxy** le permite crear una cola con el método **createQueue**.</span><span class="sxs-lookup"><span data-stu-id="dd963-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="dd963-136">Al crear una cola, puede establecer opciones en ella, aunque no es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="dd963-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="dd963-137">El ejemplo siguiente muestra cómo configurar metadatos en una cola.</span><span class="sxs-lookup"><span data-stu-id="dd963-137">(The example below shows how to set metadata on a queue.)</span></span>

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
> <span data-ttu-id="dd963-138">No debe confiar en la distinción entre minúsculas y mayúsculas para las claves de metadatos.</span><span class="sxs-lookup"><span data-stu-id="dd963-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="dd963-139">Todas las claves se leen en el servicio en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="dd963-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="dd963-140">un mensaje a una cola</span><span class="sxs-lookup"><span data-stu-id="dd963-140">Add a message to a queue</span></span>
<span data-ttu-id="dd963-141">Para agregar un mensaje a una cola, use **QueueRestProxy->createMessage**.</span><span class="sxs-lookup"><span data-stu-id="dd963-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="dd963-142">El método toma el nombre de la cola, el texto del mensaje y las opciones de mensaje (que son opcionales).</span><span class="sxs-lookup"><span data-stu-id="dd963-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-the-next-message"></a><span data-ttu-id="dd963-143">siguiente mensaje</span><span class="sxs-lookup"><span data-stu-id="dd963-143">Peek at the next message</span></span>
<span data-ttu-id="dd963-144">Puede ojear uno o varios mensajes en la parte delantera de una cola, sin quitarlos de la cola, mediante una llamada a **QueueRestProxy->peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="dd963-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="dd963-145">De forma predeterminada, el método **peekMessage** devuelve un único mensaje, pero puede cambiar el valor con el método **PeekMessagesOptions->setNumberOfMessages**.</span><span class="sxs-lookup"><span data-stu-id="dd963-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-the-next-message"></a><span data-ttu-id="dd963-146">siguiente mensaje de la cola</span><span class="sxs-lookup"><span data-stu-id="dd963-146">De-queue the next message</span></span>
<span data-ttu-id="dd963-147">El código borra un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="dd963-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="dd963-148">Primero llama a **QueueRestProxy->listMessages**, que hace que el mensaje sea invisible a cualquier otro código que esté leyendo de la cola.</span><span class="sxs-lookup"><span data-stu-id="dd963-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="dd963-149">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="dd963-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="dd963-150">(si el mensaje no se elimina en este período, volverá a estar visible de nuevo en la cola). Para terminar de quitar el mensaje de la cola, debe llamar a **QueueRestProxy->deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="dd963-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="dd963-151">Este proceso de extracción de un mensaje que consta de dos pasos garantiza que si su código no puede procesar un mensaje a causa de un error de hardware o software, otra instancia de su código puede obtener el mismo mensaje e intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="dd963-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="dd963-152">Su código llama a **deleteMessage** justo después de que se haya procesado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="dd963-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

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

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="dd963-153">contenido de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="dd963-153">Change the contents of a queued message</span></span>
<span data-ttu-id="dd963-154">Puede cambiar el contenido de un mensaje local en la cola llamando a **QueueRestProxy->updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="dd963-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="dd963-155">Si el mensaje representa una tarea de trabajo, puede usar esta característica para actualizar el estado de la tarea de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dd963-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="dd963-156">El siguiente código actualiza el mensaje de la cola con contenido nuevo y amplía el tiempo de espera de la visibilidad en 60 segundos más.</span><span class="sxs-lookup"><span data-stu-id="dd963-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="dd963-157">De este modo, se guarda el estado de trabajo asociado al mensaje y se le proporciona al cliente un minuto más para que siga elaborando el mensaje.</span><span class="sxs-lookup"><span data-stu-id="dd963-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="dd963-158">Esta técnica se puede utilizar para realizar un seguimiento de los flujos de trabajo de varios pasos en los mensajes en cola, sin que sea necesario volver a empezar desde el principio si se produce un error en un paso del proceso a causa de un error de hardware o software.</span><span class="sxs-lookup"><span data-stu-id="dd963-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="dd963-159">Normalmente, también mantendría un número de reintentos y, si el mensaje se intentara más de *n* veces, lo eliminaría.</span><span class="sxs-lookup"><span data-stu-id="dd963-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="dd963-160">Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.</span><span class="sxs-lookup"><span data-stu-id="dd963-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="dd963-161">Opciones adicionales para quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="dd963-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="dd963-162">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="dd963-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="dd963-163">En primer lugar, puede obtener un lote de mensajes (hasta 32).</span><span class="sxs-lookup"><span data-stu-id="dd963-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="dd963-164">En segundo lugar, puede establecer un tiempo de espera de la visibilidad más largo o más corto para que el código disponga de más o menos tiempo para procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="dd963-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="dd963-165">El siguiente ejemplo de código utiliza el método **getMessages** para obtener 16 mensajes en una llamada.</span><span class="sxs-lookup"><span data-stu-id="dd963-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="dd963-166">A continuación, procesa cada mensaje con un bucle **for** .</span><span class="sxs-lookup"><span data-stu-id="dd963-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="dd963-167">También establece el tiempo de espera de la invisibilidad en cinco minutos para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="dd963-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="dd963-168">longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="dd963-168">Get queue length</span></span>
<span data-ttu-id="dd963-169">Puede obtener una estimación del número de mensajes existentes en una cola.</span><span class="sxs-lookup"><span data-stu-id="dd963-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="dd963-170">El método **QueueRestProxy->getQueueMetadata** solicita a Queue service que devuelva los metadatos sobre la cola.</span><span class="sxs-lookup"><span data-stu-id="dd963-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="dd963-171">Si llama al método **getApproximateMessageCount** en el objeto devuelto, se ofrece un recuento de la cantidad de mensajes que hay en una cola.</span><span class="sxs-lookup"><span data-stu-id="dd963-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="dd963-172">El recuento solo es aproximado, ya que se pueden agregar o borrar mensajes después de que el servicio de cola haya respondido su solicitud.</span><span class="sxs-lookup"><span data-stu-id="dd963-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="dd963-173">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="dd963-173">Delete a queue</span></span>
<span data-ttu-id="dd963-174">Para eliminar una cola y todos los mensajes contenidos en ella, llame al método **QueueRestProxy->deleteQueue**.</span><span class="sxs-lookup"><span data-stu-id="dd963-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dd963-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd963-175">Next steps</span></span>
<span data-ttu-id="dd963-176">Ahora que está familiarizado con los aspectos básicos del almacenamiento en cola de Azure, use estos vínculos para obtener más información acerca de tareas de almacenamiento más complejas.</span><span class="sxs-lookup"><span data-stu-id="dd963-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="dd963-177">Visite el [Blog del equipo de Almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="dd963-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="dd963-178">Para obtener más información, consulte también el [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="dd963-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
<span data-ttu-id="dd963-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span><span class="sxs-lookup"><span data-stu-id="dd963-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span></span>
[Azure Portal]: https://portal.azure.com

