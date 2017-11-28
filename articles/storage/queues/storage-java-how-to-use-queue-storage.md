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
ms.openlocfilehash: 297f89c9d21a38d2b4a5f4346f66f59f9d487010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="c3e6d-104">¿Cómo toouse almacenamiento de cola en Java</span><span class="sxs-lookup"><span data-stu-id="c3e6d-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="c3e6d-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c3e6d-105">Overview</span></span>
<span data-ttu-id="c3e6d-106">Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio de almacenamiento de cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="c3e6d-107">ejemplos de Hello están escritos en Java y usar hello [almacenamiento de Azure SDK para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="c3e6d-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="c3e6d-108">Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear** y **eliminar** colas.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="c3e6d-109">Para obtener más información sobre las colas, vea hello [pasos siguientes](#Next-Steps) sección.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="c3e6d-110">Nota: hay un SDK disponible para los desarrolladores que usen el almacenamiento de Azure en dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="c3e6d-111">Para obtener más información, vea hello [SDK de almacenamiento de Azure para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="c3e6d-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="c3e6d-112">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="c3e6d-112">Create a Java application</span></span>
<span data-ttu-id="c3e6d-113">En esta guía utilizará funciones del almacenamiento que puede ejecutar en una aplicación Java localmente o bien mediante código a través de un rol web o un rol de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="c3e6d-114">toodo por lo tanto, necesitará tooinstall Hola Java Development Kit (JDK) y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="c3e6d-115">Una vez que lo ha hecho, necesitará tooverify que el sistema de desarrollo cumple los requisitos mínimos de Hola y dependencias que se enumeran en hello [almacenamiento de Azure SDK para Java] [ Azure Storage SDK for Java] repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="c3e6d-116">Si su sistema cumple estos requisitos, puede seguir las instrucciones de Hola para descargar e instalar Hola bibliotecas de almacenamiento de Azure para Java en el sistema de ese repositorio.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="c3e6d-117">Una vez haya completado estas tareas, será capaz de toocreate una aplicación Java que utiliza los ejemplos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="c3e6d-118">Configurar el almacenamiento de cola de aplicación tooaccess</span><span class="sxs-lookup"><span data-stu-id="c3e6d-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="c3e6d-119">Agregue Hola después de la parte superior de toohello de instrucciones de importación del archivo de Java de Hola donde desea que las colas tooaccess de las API de almacenamiento de Azure de toouse:</span><span class="sxs-lookup"><span data-stu-id="c3e6d-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="c3e6d-120">Configuración de una cadena de conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c3e6d-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="c3e6d-121">Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="c3e6d-122">Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, con nombre de hello de la cuenta de almacenamiento y Hola clave de acceso principal para cuenta de almacenamiento Hola Hola [Portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="c3e6d-123">Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="c3e6d-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="c3e6d-124">En una aplicación en ejecución dentro de un rol en Microsoft Azure, esta cadena puede almacenarse en el archivo de configuración del servicio de hello *ServiceConfiguration.cscfg*y puede tener acceso mediante una llamada a toohello  **RoleEnvironment.getConfigurationSettings** método.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="c3e6d-125">Este es un ejemplo de obtención de la cadena de conexión de Hola desde una **configuración** elemento denominado *StorageConnectionString* en el archivo de configuración de servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="c3e6d-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="c3e6d-126">Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="c3e6d-127">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="c3e6d-127">How to: Create a queue</span></span>
<span data-ttu-id="c3e6d-128">Los objetos **CloudQueueClient** le permiten obtener objetos de referencia para las colas.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="c3e6d-129">Hello código siguiente se crea un **CloudQueueClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="c3e6d-130">(Nota: hay otras formas toocreate **CloudStorageAccount** objetos; para obtener más información, vea **CloudStorageAccount** en hello [referencia de SDK de cliente de almacenamiento de Azure].)</span><span class="sxs-lookup"><span data-stu-id="c3e6d-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="c3e6d-131">Hola de uso **CloudQueueClient** tooget una cola de toohello de referencia que desee toouse del objeto.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="c3e6d-132">Puede crear la cola de hello si no existe.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-132">You can create hello queue if it doesn't exist.</span></span>

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

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="c3e6d-133">Cómo: agregar una cola de mensajes tooa</span><span class="sxs-lookup"><span data-stu-id="c3e6d-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="c3e6d-134">tooinsert un mensaje en una cola existente, primero debe crear un nuevo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="c3e6d-135">A continuación, llame a hello **addMessage** método.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="c3e6d-136">Se puede crear un **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="c3e6d-137">Este es el código que crea una cola (si no existe) y el mensaje de bienvenida de inserciones "¡Hello, World".</span><span class="sxs-lookup"><span data-stu-id="c3e6d-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

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

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="c3e6d-138">Cómo: consultar mensajes de bienvenida del siguiente</span><span class="sxs-lookup"><span data-stu-id="c3e6d-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="c3e6d-139">Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de hello mediante una llamada a **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="c3e6d-140">Cómo: cambiar Hola contenido de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="c3e6d-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="c3e6d-141">Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="c3e6d-142">Si el mensaje de Hola representa una tarea de trabajo, puede usar este estado de la característica tooupdate Hola de tarea de trabajo de hello.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="c3e6d-143">Hola siguiente código actualiza el mensaje de bienvenida de cola con nuevo contenido y conjuntos de Hola tooextend de tiempo de espera de visibilidad otro 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="c3e6d-144">Esto guarda el estado de Hola de trabajos asociados con el mensaje de bienvenida y proporciona a cliente hello otro toocontinue minuto trabajando en el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="c3e6d-145">Puede utilizar este flujos de trabajo de varios pasos de tootrack técnica sobre los mensajes en cola, sin necesidad de toostart a través de hello principio si se produce un error en un paso de procesamiento debido a un error toohardware o software.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="c3e6d-146">Normalmente, se mantendría también un número de reintentos y si hello mensaje se vuelve a intentar más de  *n*  veces, debería eliminarla.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="c3e6d-147">Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="c3e6d-148">siguiente Hola búsquedas de ejemplo a través de la cola de Hola de mensajes de código, busca Hola primer mensaje coincide con "¡Hello, World" para el contenido de hello, a continuación, modifica el contenido del mensaje de Hola y se cierra.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

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

<span data-ttu-id="c3e6d-149">Como alternativa, hello ejemplo de código siguiente actualiza solo Hola primera visible mensaje en cola Hola.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="c3e6d-150">Cómo: obtener la longitud de cola de Hola</span><span class="sxs-lookup"><span data-stu-id="c3e6d-150">How to: Get hello queue length</span></span>
<span data-ttu-id="c3e6d-151">Puede obtener una estimación del número de Hola de mensajes en una cola.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="c3e6d-152">Hola **downloadAttributes** método pide al servicio de cola de Hola para varios valores actuales, incluido un recuento de cuántos mensajes se encuentran en una cola.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="c3e6d-153">recuento de Hello solo es aproximado porque los mensajes se pueden agregar o quitar después de hello servicio cola responde tooyour solicitud.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="c3e6d-154">Hola **getApproximateMessageCount** método devuelve el valor última Hola recuperado por llamada de hello demasiado**downloadAttributes**, sin llamar al servicio de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

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

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="c3e6d-155">Cómo: eliminación de cola de mensajes de bienvenida del siguiente</span><span class="sxs-lookup"><span data-stu-id="c3e6d-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="c3e6d-156">El código extrae un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="c3e6d-157">Cuando se llama a **retrieveMessage**, obtendrá el siguiente mensaje de Hola en una cola.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="c3e6d-158">Un mensaje devuelto de **retrieveMessage** se convierte en invisible tooany otro código que lee mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="c3e6d-159">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="c3e6d-160">toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="c3e6d-161">Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="c3e6d-162">Las llamadas de código **deleteMessage** justo después de que se ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="c3e6d-163">Opciones adicionales para quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="c3e6d-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="c3e6d-164">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="c3e6d-165">En primer lugar, puede obtener un lote de mensajes (arriba too32).</span><span class="sxs-lookup"><span data-stu-id="c3e6d-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="c3e6d-166">En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="c3e6d-167">ejemplo de código siguiente Hello usa Hola **retrieveMessages** tooget 20 mensajes de método en una llamada.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="c3e6d-168">A continuación, procesa cada mensaje con un bucle **for** .</span><span class="sxs-lookup"><span data-stu-id="c3e6d-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="c3e6d-169">También establece Hola invisibilidad tiempo de espera toofive minutos (300 segundos para cada mensaje).</span><span class="sxs-lookup"><span data-stu-id="c3e6d-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="c3e6d-170">Tenga en cuenta que Hola cinco minutos se inicia para todos los mensajes en hello mismo tiempo, por lo que cuando cinco minutos transcurridos desde la llamada de hello demasiado**retrieveMessages**, los mensajes que no se eliminaron estará visibles de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

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

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="c3e6d-171">Cómo: enumerar las colas de Hola</span><span class="sxs-lookup"><span data-stu-id="c3e6d-171">How to: List hello queues</span></span>
<span data-ttu-id="c3e6d-172">una lista de colas actuales de hello, llamada hello tooobtain **CloudQueueClient.listQueues()** método, que devuelve una colección de **CloudQueue** objetos.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

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

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="c3e6d-173">Cómo eliminar una cola</span><span class="sxs-lookup"><span data-stu-id="c3e6d-173">How to: Delete a queue</span></span>
<span data-ttu-id="c3e6d-174">toodelete una cola y todos los mensajes de Hola contenidas en ella, llamada hello **deleteIfExists** método en hello **CloudQueue** objeto.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c3e6d-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3e6d-175">Next steps</span></span>
<span data-ttu-id="c3e6d-176">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c3e6d-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="c3e6d-177">[SDK de Azure Storage para Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="c3e6d-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="c3e6d-178">[referencia de SDK de cliente de almacenamiento de Azure][referencia de SDK de cliente de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="c3e6d-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="c3e6d-179">[API de REST de servicios de Azure Storage][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="c3e6d-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="c3e6d-180">[Blog del equipo de Azure Storage][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="c3e6d-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referencia de SDK de cliente de almacenamiento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
