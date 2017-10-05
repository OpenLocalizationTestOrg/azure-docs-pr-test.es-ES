---
title: Uso de Queue Storage en Java | Microsoft Docs
description: Aprenda a utilizar el servicio Cola de Azure para crear y eliminar colas e insertar, obtener y eliminar mensajes. Ejemplos escritos en Java.
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
ms.openlocfilehash: a56b345c5efb4ce9c8ee2da91b798d09d44e42be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-java"></a><span data-ttu-id="18413-104">Uso del almacenamiento de colas de Java</span><span class="sxs-lookup"><span data-stu-id="18413-104">How to use Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="18413-105">Información general</span><span class="sxs-lookup"><span data-stu-id="18413-105">Overview</span></span>
<span data-ttu-id="18413-106">Esta guía muestra cómo realizar algunas tareas comunes a través del servicio de almacenamiento en cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="18413-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="18413-107">Los ejemplos están escritos en Java y utilizan el [SDK de Azure Storage para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="18413-107">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="18413-108">Entre los escenarios descritos se incluyen **insertar**, **ojear**, **obtener** y **eliminar** mensajes de la cola, así como **crear** y **eliminar** colas.</span><span class="sxs-lookup"><span data-stu-id="18413-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="18413-109">Para obtener más información sobre las colas, consulte la sección [Pasos siguientes](#Next-Steps) .</span><span class="sxs-lookup"><span data-stu-id="18413-109">For more information on queues, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="18413-110">Nota: hay un SDK disponible para los desarrolladores que usen el almacenamiento de Azure en dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="18413-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="18413-111">Para obtener más información, vea el [SDK de Azure Storage para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="18413-111">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="18413-112">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="18413-112">Create a Java application</span></span>
<span data-ttu-id="18413-113">En esta guía utilizará funciones del almacenamiento que puede ejecutar en una aplicación Java localmente o bien mediante código a través de un rol web o un rol de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="18413-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="18413-114">Para ello, deberá instalar el Kit de desarrollo de Java (JDK) y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="18413-114">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="18413-115">Después, deberá verificar que su sistema de desarrollo satisface los requisitos mínimos y las dependencias que se indican en el repositorio del [SDK de Azure Storage para Java][Azure Storage SDK for Java] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="18413-115">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="18413-116">Si su sistema cumple esos requisitos, puede seguir las instrucciones para descargar e instalar las bibliotecas de almacenamiento de Azure para Java en su sistema desde ese repositorio.</span><span class="sxs-lookup"><span data-stu-id="18413-116">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="18413-117">Cuando haya completado esas tareas, podrá crear una aplicación Java que use los ejemplos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="18413-117">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="18413-118">Configuración de la aplicación para obtener acceso al almacenamiento en cola</span><span class="sxs-lookup"><span data-stu-id="18413-118">Configure your application to access queue storage</span></span>
<span data-ttu-id="18413-119">Agregue las siguientes instrucciones de importación en la parte superior del archivo Java en el que desea utilizar las API de almacenamiento de Azure para obtener acceso a las colas:</span><span class="sxs-lookup"><span data-stu-id="18413-119">Add the following import statements to the top of the Java file where you want to use Azure storage APIs to access queues:</span></span>

```java
// Include the following imports to use queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="18413-120">Configuración de una cadena de conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="18413-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="18413-121">Un cliente de almacenamiento de Azure utiliza una cadena de conexión de almacenamiento para almacenar extremos y credenciales con el fin de obtener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="18413-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="18413-122">Al ejecutarse en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento en el siguiente formato, usando el nombre de su cuenta de almacenamiento y la clave de acceso principal de la cuenta de almacenamiento que se muestra en [Azure Portal](https://portal.azure.com) para los valores *AccountName* y *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="18413-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="18413-123">En este ejemplo se muestra cómo puede declarar un campo estático para mantener la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="18413-123">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="18413-124">En una aplicación que se esté ejecutando en un rol de Microsoft Azure, esta cadena se puede almacenar en el archivo de configuración de servicio, *ServiceConfiguration.cscfg*, y se puede obtener acceso a él con una llamada al método **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="18413-124">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="18413-125">A continuación se muestra un ejemplo de cómo obtener la cadena de conexión desde un elemento de **configuración** denominado *StorageConnectionString* en el archivo de configuración del servicio:</span><span class="sxs-lookup"><span data-stu-id="18413-125">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="18413-126">En los ejemplos siguientes se supone que usó uno de estos dos métodos para obtener la cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18413-126">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="18413-127">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="18413-127">How to: Create a queue</span></span>
<span data-ttu-id="18413-128">Los objetos **CloudQueueClient** le permiten obtener objetos de referencia para las colas.</span><span class="sxs-lookup"><span data-stu-id="18413-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="18413-129">El siguiente código crea un objeto **CloudQueueClient**.</span><span class="sxs-lookup"><span data-stu-id="18413-129">The following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="18413-130">(Nota: Hay otras maneras de crear objetos **CloudStorageAccount**. Para más información, consulte **CloudStorageAccount** en la [Referencia del SDK del cliente de Azure Storage]).</span><span class="sxs-lookup"><span data-stu-id="18413-130">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="18413-131">Use el objeto **CloudQueueClient** para obtener una referencia a la cola que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="18413-131">Use the **CloudQueueClient** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="18413-132">En caso de que la cola no exista todavía, es posible crearla.</span><span class="sxs-lookup"><span data-stu-id="18413-132">You can create the queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create the queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference to a queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create the queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-to-a-queue"></a><span data-ttu-id="18413-133">Incorporación de un mensaje a una cola</span><span class="sxs-lookup"><span data-stu-id="18413-133">How to: Add a message to a queue</span></span>
<span data-ttu-id="18413-134">Para insertar un mensaje en una cola existente, cree en primer lugar un nuevo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="18413-134">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="18413-135">A continuación, llame al método **addMessage** .</span><span class="sxs-lookup"><span data-stu-id="18413-135">Next, call the **addMessage** method.</span></span> <span data-ttu-id="18413-136">Se puede crear un **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="18413-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="18413-137">A continuación se muestra el código con el que se crea una cola (si no existe) y se inserta el mensaje "Hola, mundo".</span><span class="sxs-lookup"><span data-stu-id="18413-137">Here is code which creates a queue (if it doesn't exist) and inserts the message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create the queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="18413-138">Cómo ojear el siguiente mensaje</span><span class="sxs-lookup"><span data-stu-id="18413-138">How to: Peek at the next message</span></span>
<span data-ttu-id="18413-139">Puede inspeccionar el mensaje situado en la parte delantera de una cola, sin quitarlo de la cola, mediante una llamada al método **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="18413-139">You can peek at the message in the front of a queue without removing it from the queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at the next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output the message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="18413-140">Cómo cambiar el contenido de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="18413-140">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="18413-141">Puede cambiar el contenido de un mensaje local en la cola.</span><span class="sxs-lookup"><span data-stu-id="18413-141">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="18413-142">Si el mensaje representa una tarea de trabajo, puede usar esta característica para actualizar el estado de la tarea de trabajo.</span><span class="sxs-lookup"><span data-stu-id="18413-142">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="18413-143">El siguiente código actualiza el mensaje de la cola con contenido nuevo y amplía el tiempo de espera de la visibilidad en 60 segundos más.</span><span class="sxs-lookup"><span data-stu-id="18413-143">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="18413-144">De este modo, se guarda el estado de trabajo asociado al mensaje y se le proporciona al cliente un minuto más para que siga elaborando el mensaje.</span><span class="sxs-lookup"><span data-stu-id="18413-144">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="18413-145">Esta técnica se puede utilizar para realizar un seguimiento de los flujos de trabajo de varios pasos en los mensajes en cola, sin que sea necesario volver a empezar desde el principio si se produce un error en un paso del proceso a causa de un error de hardware o software.</span><span class="sxs-lookup"><span data-stu-id="18413-145">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="18413-146">Normalmente, también mantendría un número de reintentos y, si el mensaje se intentara más de *n* veces, lo eliminaría.</span><span class="sxs-lookup"><span data-stu-id="18413-146">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="18413-147">Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.</span><span class="sxs-lookup"><span data-stu-id="18413-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="18413-148">El siguiente código de ejemplo busca en la cola de mensajes, encuentra el primer mensaje cuyo contenido coincide con "Hola, mundo" y luego modifica el contenido del mensaje "Hola mundo" y se cierra.</span><span class="sxs-lookup"><span data-stu-id="18413-148">The following code sample searches through the queue of messages, locates the first message that matches "Hello, World" for the content, then modifies the message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // The maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through the messages in the queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify the content of the first matching message.
            message.setMessageContent("Updated contents.");
            // Set it to be visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update the message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="18413-149">Como alternativa, el siguiente código de ejemplo actualiza únicamente el primer mensaje visible de la cola.</span><span class="sxs-lookup"><span data-stu-id="18413-149">Alternatively, the following code sample updates just the first visible message on the queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify the message content.
        message.setMessageContent("Updated contents.");
        // Set it to be visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update the message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="18413-150">Cómo obtener la longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="18413-150">How to: Get the queue length</span></span>
<span data-ttu-id="18413-151">Puede obtener una estimación del número de mensajes existentes en una cola.</span><span class="sxs-lookup"><span data-stu-id="18413-151">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="18413-152">El método **downloadAttributes** pide al servicio de cola varios valores actuales, incluido un conteo de cuántos mensajes están en la cola.</span><span class="sxs-lookup"><span data-stu-id="18413-152">The **downloadAttributes** method asks the Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="18413-153">El recuento solo es aproximado, ya que se pueden agregar o borrar mensajes después de que el servicio de cola haya respondido su solicitud.</span><span class="sxs-lookup"><span data-stu-id="18413-153">The count is only approximate because messages can be added or removed after the Queue service responds to your request.</span></span> <span data-ttu-id="18413-154">El método **getApproximateMethodCount** devuelve el último valor recuperado por la llamada a **downloadAttributes**, sin llamar a Queue service.</span><span class="sxs-lookup"><span data-stu-id="18413-154">The **getApproximateMessageCount** method returns the last value retrieved by the call to **downloadAttributes**, without calling the Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download the approximate message count from the server.
    queue.downloadAttributes();

    // Retrieve the newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display the queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="18413-155">Extracción del siguiente mensaje de la cola</span><span class="sxs-lookup"><span data-stu-id="18413-155">How to: Dequeue the next message</span></span>
<span data-ttu-id="18413-156">El código extrae un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="18413-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="18413-157">Al llamar a **retrieveMessage**, obtiene el siguiente mensaje de una cola.</span><span class="sxs-lookup"><span data-stu-id="18413-157">When you call **retrieveMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="18413-158">Un mensaje devuelto por **retrieveMessage** se hace invisible a cualquier otro código de lectura de mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="18413-158">A message returned from **retrieveMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="18413-159">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="18413-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="18413-160">Para terminar de quitar el mensaje de la cola, también debe llamar a **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="18413-160">To finish removing the message from the queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="18413-161">Este proceso de extracción de un mensaje que consta de dos pasos garantiza que si su código no puede procesar un mensaje a causa de un error de hardware o software, otra instancia de su código puede obtener el mismo mensaje e intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="18413-161">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="18413-162">Su código llama a **deleteMessage** justo después de que se haya procesado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="18413-162">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process the message in less than 30 seconds, and then delete the message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="18413-163">Opciones adicionales para quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="18413-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="18413-164">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="18413-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="18413-165">En primer lugar, puede obtener un lote de mensajes (hasta 32).</span><span class="sxs-lookup"><span data-stu-id="18413-165">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="18413-166">En segundo lugar, puede establecer un tiempo de espera de la invisibilidad más largo o más corto para que el código disponga de más o menos tiempo para procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="18413-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="18413-167">El siguiente ejemplo de código utiliza el método **retrieveMessage** para obtener 20 mensajes en una llamada.</span><span class="sxs-lookup"><span data-stu-id="18413-167">The following code example uses the **retrieveMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="18413-168">A continuación, procesa cada mensaje con un bucle **for** .</span><span class="sxs-lookup"><span data-stu-id="18413-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="18413-169">También establece el tiempo de espera de la invisibilidad en cinco minutos (300 segundos) para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="18413-169">It also sets the invisibility timeout to five minutes (300 seconds) for each message.</span></span> <span data-ttu-id="18413-170">Tenga en cuenta que los cinco minutos empiezan a contar para todos los mensajes al mismo tiempo, por lo que después de pasar los cinco minutos desde la llamada a **retrieveMessage**, todos los mensajes que no se han eliminado volverán a estar visibles.</span><span class="sxs-lookup"><span data-stu-id="18413-170">Note that the five minutes starts for all messages at the same time, so when five minutes have passed since the call to **retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-queues"></a><span data-ttu-id="18413-171">Enumeración de las colas</span><span class="sxs-lookup"><span data-stu-id="18413-171">How to: List the queues</span></span>
<span data-ttu-id="18413-172">Para obtener una lista de las colas actuales, llame al método **CloudQueueClient.listQueues()**, el cual devolverá una colección de objetos **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="18413-172">To obtain a list of the current queues, call the **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through the collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="18413-173">Cómo eliminar una cola</span><span class="sxs-lookup"><span data-stu-id="18413-173">How to: Delete a queue</span></span>
<span data-ttu-id="18413-174">Para eliminar una cola y todos los mensajes contenidos en ella, llame al método **deleteIfExists** en el objeto de cola **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="18413-174">To delete a queue and all the messages contained in it, call the **deleteIfExists** method on the **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete the queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="18413-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18413-175">Next steps</span></span>
<span data-ttu-id="18413-176">Ahora que está familiarizado con los aspectos básicos del almacenamiento de colas, utilice estos vínculos para obtener más información acerca de tareas de almacenamiento más complejas.</span><span class="sxs-lookup"><span data-stu-id="18413-176">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="18413-177">[SDK de Azure Storage para Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="18413-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="18413-178">[Referencia del SDK del cliente de Azure Storage][Referencia del SDK del cliente de Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="18413-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="18413-179">[API de REST de servicios de Azure Storage][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="18413-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="18413-180">[Blog del equipo de Azure Storage][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="18413-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Referencia del SDK del cliente de Azure Storage]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
