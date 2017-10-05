---
title: Udo de Queue Storage (C++) | Microsoft Docs
description: "Aprenda a usar el servicio de almacenamiento de colas en Azure. Los ejemplos están escritos en C++."
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
ms.openlocfilehash: 5e81d5e0af9871099b7f921f355cf94249e4d30c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="d6926-104">Uso del almacenamiento de colas de C++</span><span class="sxs-lookup"><span data-stu-id="d6926-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="d6926-105">Información general</span><span class="sxs-lookup"><span data-stu-id="d6926-105">Overview</span></span>
<span data-ttu-id="d6926-106">Esta guía muestra cómo realizar algunas tareas comunes a través del servicio de almacenamiento en cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6926-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="d6926-107">Los ejemplos están escritos en C++ y usan la [biblioteca de cliente de almacenamiento de Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="d6926-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="d6926-108">Entre los escenarios descritos se incluyen **insertar**, **ojear**, **obtener** y **eliminar** mensajes de la cola, así como **crear y eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="d6926-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="d6926-109">Esta guía se destina a la biblioteca de cliente de almacenamiento de Azure para C++, versión 1.0.0 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="d6926-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="d6926-110">La versión recomendada es la biblioteca de cliente de almacenamiento 2.2.0, que se encuentra disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="d6926-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="d6926-111">Creación de una aplicación de C++</span><span class="sxs-lookup"><span data-stu-id="d6926-111">Create a C++ application</span></span>
<span data-ttu-id="d6926-112">En esta guía, usará las características de almacenamiento que se pueden ejecutar en una aplicación C++.</span><span class="sxs-lookup"><span data-stu-id="d6926-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="d6926-113">Para ello, deberá instalar la biblioteca de cliente de almacenamiento de Azure para C++ y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6926-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="d6926-114">Para instalar la biblioteca de cliente de almacenamiento de Azure para C++, puede usar los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d6926-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="d6926-115">**Linux:** siga las instrucciones indicadas en la página [Léame de la biblioteca de cliente de almacenamiento de Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="d6926-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="d6926-116">**Windows:** en Visual Studio, haga clic en **Herramientas > Administrador de paquetes de NuGet > Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="d6926-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="d6926-117">Escriba el siguiente comando en la [Consola del Administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="d6926-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="d6926-118">Configuración de la aplicación para obtener acceso al almacenamiento en cola</span><span class="sxs-lookup"><span data-stu-id="d6926-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="d6926-119">Agregue las siguientes instrucciones include en la parte superior del archivo C++ en el que desea usar las API de almacenamiento de Azure para obtener acceso a las colas:</span><span class="sxs-lookup"><span data-stu-id="d6926-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="d6926-120">Configuración de una cadena de conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d6926-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="d6926-121">Un cliente de almacenamiento de Azure utiliza una cadena de conexión de almacenamiento para almacenar extremos y credenciales con el fin de obtener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="d6926-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="d6926-122">Al ejecutarse en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento en el siguiente formato, usando el nombre de su cuenta de almacenamiento y la clave de acceso de almacenamiento de la cuenta de almacenamiento que se muestra en [Azure Portal](https://portal.azure.com) para los valores *AccountName* y *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="d6926-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="d6926-123">Para obtener información sobre las cuentas de almacenamiento y las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6926-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="d6926-124">En este ejemplo se muestra cómo puede declarar un campo estático para mantener la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="d6926-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="d6926-125">Para probar la aplicación en el equipo local de Windows, puede usar Microsoft Azure [Storage Emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) que se instala con [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d6926-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="d6926-126">El emulador de almacenamiento es una utilidad que simula los servicios Blob, Cola y Tabla disponibles en Azure en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="d6926-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="d6926-127">En el ejemplo siguiente se muestra cómo puede declarar un campo estático para mantener la cadena de conexión en el emulador de almacenamiento local:</span><span class="sxs-lookup"><span data-stu-id="d6926-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="d6926-128">Para iniciar Azure Storage Emulator, seleccione el botón **Inicio** o pulse la tecla **Windows**.</span><span class="sxs-lookup"><span data-stu-id="d6926-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="d6926-129">Comience a escribir **Azure Storage Emulator** y seleccione **Emulador de Microsoft Azure Storage** en la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d6926-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="d6926-130">En los ejemplos siguientes se supone que usó uno de estos dos métodos para obtener la cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d6926-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="d6926-131">Recuperación de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="d6926-131">Retrieve your connection string</span></span>
<span data-ttu-id="d6926-132">Puede usar la clase **cloud_storage_account** para representar la información de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d6926-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="d6926-133">Para recuperar la información de la cuenta de almacenamiento a partir de la cadena de conexión de almacenamiento, puede usar el método **parse** .</span><span class="sxs-lookup"><span data-stu-id="d6926-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="d6926-134">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="d6926-134">How to: Create a queue</span></span>
<span data-ttu-id="d6926-135">Los objetos **cloud_queue_client** le permiten obtener objetos de referencia para las colas.</span><span class="sxs-lookup"><span data-stu-id="d6926-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="d6926-136">El siguiente código crea un objeto **cloud_queue_client**.</span><span class="sxs-lookup"><span data-stu-id="d6926-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="d6926-137">Use el objeto **cloud_queue_client** para obtener una referencia a la cola que desea usar.</span><span class="sxs-lookup"><span data-stu-id="d6926-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="d6926-138">En caso de que la cola no exista todavía, es posible crearla.</span><span class="sxs-lookup"><span data-stu-id="d6926-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="d6926-139">Cómo insertar un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="d6926-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="d6926-140">Para insertar un mensaje en una cola existente, cree en primer lugar un nuevo **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="d6926-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="d6926-141">A continuación, llame al método **add_message**.</span><span class="sxs-lookup"><span data-stu-id="d6926-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="d6926-142">Se puede crear un **cloud_queue_message** a partir de una cadena o de una matriz de **byte**.</span><span class="sxs-lookup"><span data-stu-id="d6926-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="d6926-143">A continuación se muestra el código con el que se crea una cola (si no existe) y se inserta el mensaje "Hola, mundo":</span><span class="sxs-lookup"><span data-stu-id="d6926-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="d6926-144">Cómo ojear el siguiente mensaje</span><span class="sxs-lookup"><span data-stu-id="d6926-144">How to: Peek at the next message</span></span>
<span data-ttu-id="d6926-145">Puede ojear el mensaje situado en la parte delantera de una cola, sin quitarlo de la cola, llamando al método **peek_message**.</span><span class="sxs-lookup"><span data-stu-id="d6926-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="d6926-146">Cómo cambiar el contenido de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="d6926-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="d6926-147">Puede cambiar el contenido de un mensaje local en la cola.</span><span class="sxs-lookup"><span data-stu-id="d6926-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="d6926-148">Si el mensaje representa una tarea de trabajo, puede usar esta característica para actualizar el estado de la tarea de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d6926-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="d6926-149">El siguiente código actualiza el mensaje de la cola con contenido nuevo y amplía el tiempo de espera de la visibilidad en 60 segundos más.</span><span class="sxs-lookup"><span data-stu-id="d6926-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="d6926-150">De este modo, se guarda el estado de trabajo asociado al mensaje y se le proporciona al cliente un minuto más para que siga elaborando el mensaje.</span><span class="sxs-lookup"><span data-stu-id="d6926-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="d6926-151">Esta técnica se puede utilizar para realizar un seguimiento de los flujos de trabajo de varios pasos en los mensajes en cola, sin que sea necesario volver a empezar desde el principio si se produce un error en un paso del proceso a causa de un error de hardware o software.</span><span class="sxs-lookup"><span data-stu-id="d6926-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="d6926-152">Normalmente, también mantendría un número de reintentos y, si el mensaje se intentara más de n veces, lo eliminaría.</span><span class="sxs-lookup"><span data-stu-id="d6926-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="d6926-153">Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.</span><span class="sxs-lookup"><span data-stu-id="d6926-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="d6926-154">Cómo extraer el siguiente mensaje de la cola</span><span class="sxs-lookup"><span data-stu-id="d6926-154">How to: De-queue the next message</span></span>
<span data-ttu-id="d6926-155">El código quita un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="d6926-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="d6926-156">Si se llama a **get_message**, obtiene el siguiente mensaje de una cola.</span><span class="sxs-lookup"><span data-stu-id="d6926-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="d6926-157">Un mensaje devuelto por **get_message** se hace invisible a cualquier otro código que lea mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="d6926-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="d6926-158">Para terminar quitando el mensaje de la cola, también debe llamar a **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="d6926-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="d6926-159">Este proceso extracción de un mensaje que consta de dos pasos garantiza que si su código no puede procesar un mensaje a causa de un error de hardware o software, otra instancia de su código puede obtener el mismo mensaje e intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="d6926-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="d6926-160">El código llama a **delete_message** justo después de que se haya procesado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="d6926-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="d6926-161">Cómo usar las opciones adicionales para quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="d6926-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="d6926-162">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="d6926-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="d6926-163">En primer lugar, puede obtener un lote de mensajes (hasta 32).</span><span class="sxs-lookup"><span data-stu-id="d6926-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="d6926-164">En segundo lugar, puede establecer un tiempo de espera de la invisibilidad más largo o más corto para que el código disponga de más o menos tiempo para procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="d6926-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="d6926-165">El siguiente ejemplo de código utiliza el método **get_messages** para obtener 20 mensajes en una llamada.</span><span class="sxs-lookup"><span data-stu-id="d6926-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="d6926-166">A continuación, procesa cada mensaje con un bucle **for** .</span><span class="sxs-lookup"><span data-stu-id="d6926-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="d6926-167">También establece el tiempo de espera de la invisibilidad en cinco minutos para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="d6926-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="d6926-168">Tenga en cuenta que los 5 minutos empiezan a contar para todos los mensajes al mismo tiempo, por lo que después de que pasen los 5 minutos desde la llamada a **get_messages**, todos los mensajes que no se han eliminado volverán a estar visibles.</span><span class="sxs-lookup"><span data-stu-id="d6926-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="d6926-169">Cómo obtener la longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="d6926-169">How to: Get the queue length</span></span>
<span data-ttu-id="d6926-170">Puede obtener una estimación del número de mensajes existentes en una cola.</span><span class="sxs-lookup"><span data-stu-id="d6926-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="d6926-171">El método **download_attributes** solicita a Queue service la recuperación de los atributos de la cola, incluido el número de mensajes.</span><span class="sxs-lookup"><span data-stu-id="d6926-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="d6926-172">El método **approximate_message_count** obtiene el número aproximado de mensajes en la cola.</span><span class="sxs-lookup"><span data-stu-id="d6926-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="d6926-173">Cómo eliminar una cola</span><span class="sxs-lookup"><span data-stu-id="d6926-173">How to: Delete a queue</span></span>
<span data-ttu-id="d6926-174">Para eliminar una cola y todos los mensajes contenidos en ella, llame al método **delete_queue_if_exists** en el objeto de cola.</span><span class="sxs-lookup"><span data-stu-id="d6926-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="d6926-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6926-175">Next steps</span></span>
<span data-ttu-id="d6926-176">Ahora que está familiarizado con los aspectos básicos del almacenamiento de colas, siga estos vínculos para obtener más información sobre Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6926-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="d6926-177">Cómo usar el almacenamiento de blobs de C++</span><span class="sxs-lookup"><span data-stu-id="d6926-177">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="d6926-178">Cómo usar el almacenamiento de tablas de C++</span><span class="sxs-lookup"><span data-stu-id="d6926-178">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="d6926-179">Enumeración de los recursos de almacenamiento de Azure en C++</span><span class="sxs-lookup"><span data-stu-id="d6926-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="d6926-180">Referencia de la biblioteca de clientes de almacenamiento para C++</span><span class="sxs-lookup"><span data-stu-id="d6926-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="d6926-181">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d6926-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)