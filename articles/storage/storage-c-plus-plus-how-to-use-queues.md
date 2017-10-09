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
ms.openlocfilehash: 755380824890ad83774e14d258975915e10cfede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="4adc7-104">¿Cómo toouse almacenamiento de cola desde C++</span><span class="sxs-lookup"><span data-stu-id="4adc7-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="4adc7-105">Información general</span><span class="sxs-lookup"><span data-stu-id="4adc7-105">Overview</span></span>
<span data-ttu-id="4adc7-106">Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio de almacenamiento de cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="4adc7-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="4adc7-107">ejemplos de Hello están escritos en C++ y usar hello [biblioteca de cliente de almacenamiento de Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="4adc7-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="4adc7-108">Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear y eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="4adc7-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="4adc7-109">Destinos de esta guía Hola biblioteca de cliente de almacenamiento de Azure para C++ versión 1.0.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="4adc7-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="4adc7-110">Hola recomienda versión es la biblioteca de cliente de almacenamiento 2.2.0, que está disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="4adc7-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="4adc7-111">Creación de una aplicación de C++</span><span class="sxs-lookup"><span data-stu-id="4adc7-111">Create a C++ application</span></span>
<span data-ttu-id="4adc7-112">En esta guía, usará las características de almacenamiento que se pueden ejecutar en una aplicación C++.</span><span class="sxs-lookup"><span data-stu-id="4adc7-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="4adc7-113">toodo por lo tanto, necesitará tooinstall Hola biblioteca de cliente de almacenamiento de Azure para C++ y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4adc7-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="4adc7-114">Hola tooinstall biblioteca de cliente de almacenamiento de Azure para C++, puede usar Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="4adc7-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="4adc7-115">**Linux:** seguir instrucciones Hola de hello [biblioteca de cliente de almacenamiento de Azure para C++ Léame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="4adc7-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="4adc7-116">**Windows:** en Visual Studio, haga clic en **Herramientas &gt; Administrador de paquetes de NuGet &gt; Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="4adc7-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="4adc7-117">Escriba lo siguiente Hola de comandos en hello [consola de administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="4adc7-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="4adc7-118">Configurar el almacenamiento de la cola de aplicación tooaccess</span><span class="sxs-lookup"><span data-stu-id="4adc7-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="4adc7-119">Agregue la siguiente Hola incluye la parte superior de toohello de las instrucciones del archivo de C++ de Hola donde desea que las colas tooaccess de las API de toouse Hola almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="4adc7-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="4adc7-120">Configuración de una cadena de conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="4adc7-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="4adc7-121">Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="4adc7-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="4adc7-122">Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, utilizando el nombre de Hola de su clave de acceso almacenamiento hello y cuenta de almacenamiento para cuenta de almacenamiento Hola Hola [Portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="4adc7-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="4adc7-123">Para obtener información sobre las cuentas de almacenamiento y las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="4adc7-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="4adc7-124">Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="4adc7-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="4adc7-125">tootest la aplicación en el equipo local de Windows, puede usar Microsoft Azure hello [emulador de almacenamiento](storage-use-emulator.md) que se instala con hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4adc7-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="4adc7-126">emulador de almacenamiento de Hello es una utilidad que simula los servicios de Blob, cola y tabla de hello disponibles en Azure en su equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="4adc7-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="4adc7-127">Hello en el ejemplo siguiente se muestra cómo se puede declarar un emulador de almacenamiento local de campo estático toohold Hola conexión cadena tooyour:</span><span class="sxs-lookup"><span data-stu-id="4adc7-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="4adc7-128">emulador de almacenamiento de Azure de hello toostart, seleccione hello **iniciar** Hola o presionen **Windows** clave.</span><span class="sxs-lookup"><span data-stu-id="4adc7-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="4adc7-129">Comience a escribir **emulador de almacenamiento de Azure**y seleccione **emulador de almacenamiento de Microsoft Azure** de lista de Hola de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4adc7-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="4adc7-130">Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="4adc7-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="4adc7-131">Recuperación de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="4adc7-131">Retrieve your connection string</span></span>
<span data-ttu-id="4adc7-132">Puede usar hello **cloud_storage_account** clase toorepresent información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4adc7-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="4adc7-133">tooretrieve información de cadena de conexión de almacenamiento de hello de la cuenta de almacenamiento, puede utilizar hello **analizar** método.</span><span class="sxs-lookup"><span data-stu-id="4adc7-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="4adc7-134">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="4adc7-134">How to: Create a queue</span></span>
<span data-ttu-id="4adc7-135">Los objetos **cloud_queue_client** le permiten obtener objetos de referencia para las colas.</span><span class="sxs-lookup"><span data-stu-id="4adc7-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="4adc7-136">Hello código siguiente se crea un **cloud_queue_client** objeto.</span><span class="sxs-lookup"><span data-stu-id="4adc7-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="4adc7-137">Hola de uso **cloud_queue_client** tooget una cola de toohello de referencia que desee toouse del objeto.</span><span class="sxs-lookup"><span data-stu-id="4adc7-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="4adc7-138">Puede crear la cola de hello si no existe.</span><span class="sxs-lookup"><span data-stu-id="4adc7-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="4adc7-139">Cómo insertar un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="4adc7-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="4adc7-140">tooinsert un mensaje en una cola existente, primero debe crear un nuevo **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="4adc7-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="4adc7-141">A continuación, llame a hello **add_message** método.</span><span class="sxs-lookup"><span data-stu-id="4adc7-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="4adc7-142">Se puede crear un **cloud_queue_message** a partir de una cadena o de una matriz de **byte**.</span><span class="sxs-lookup"><span data-stu-id="4adc7-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="4adc7-143">Este es el código que crea una cola (si no existe) y el mensaje de bienvenida de inserciones "¡Hello, World":</span><span class="sxs-lookup"><span data-stu-id="4adc7-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

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

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="4adc7-144">Cómo: consultar mensajes de bienvenida del siguiente</span><span class="sxs-lookup"><span data-stu-id="4adc7-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="4adc7-145">Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **peek_message** método.</span><span class="sxs-lookup"><span data-stu-id="4adc7-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="4adc7-146">Cómo: cambiar Hola contenido de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="4adc7-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="4adc7-147">Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="4adc7-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="4adc7-148">Si el mensaje de Hola representa una tarea de trabajo, puede usar este estado de la característica tooupdate Hola de tarea de trabajo de hello.</span><span class="sxs-lookup"><span data-stu-id="4adc7-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="4adc7-149">Hola siguiente código actualiza el mensaje de bienvenida de cola con nuevo contenido y conjuntos de Hola tooextend de tiempo de espera de visibilidad otro 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="4adc7-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="4adc7-150">Esto guarda el estado de Hola de trabajos asociados con el mensaje de bienvenida y proporciona a cliente hello otro toocontinue minuto trabajando en el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="4adc7-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="4adc7-151">Puede utilizar este flujos de trabajo de varios pasos de tootrack técnica sobre los mensajes en cola, sin necesidad de toostart a través de hello principio si se produce un error en un paso de procesamiento debido a un error toohardware o software.</span><span class="sxs-lookup"><span data-stu-id="4adc7-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="4adc7-152">Por lo general, puede hacer que un número de reintentos así y si el mensaje de bienvenida se vuelve a intentar más de n veces, debería eliminarla.</span><span class="sxs-lookup"><span data-stu-id="4adc7-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="4adc7-153">Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.</span><span class="sxs-lookup"><span data-stu-id="4adc7-153">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="4adc7-154">Cómo: eliminación de la cola mensajes de bienvenida del siguiente</span><span class="sxs-lookup"><span data-stu-id="4adc7-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="4adc7-155">El código quita un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="4adc7-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="4adc7-156">Cuando se llama a **get_message**, obtendrá el siguiente mensaje de Hola en una cola.</span><span class="sxs-lookup"><span data-stu-id="4adc7-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="4adc7-157">Un mensaje devuelto de **get_message** se convierte en invisible tooany otro código que lee mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="4adc7-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="4adc7-158">toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="4adc7-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="4adc7-159">Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="4adc7-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="4adc7-160">Las llamadas de código **delete_message** justo después de que se ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="4adc7-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

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

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="4adc7-161">Cómo usar las opciones adicionales para quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="4adc7-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="4adc7-162">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="4adc7-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="4adc7-163">En primer lugar, puede obtener un lote de mensajes (arriba too32).</span><span class="sxs-lookup"><span data-stu-id="4adc7-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="4adc7-164">En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="4adc7-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="4adc7-165">ejemplo de código siguiente Hello usa Hola **get_messages** tooget 20 mensajes de método en una llamada.</span><span class="sxs-lookup"><span data-stu-id="4adc7-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="4adc7-166">A continuación, procesa cada mensaje con un bucle **for** .</span><span class="sxs-lookup"><span data-stu-id="4adc7-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="4adc7-167">También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="4adc7-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="4adc7-168">Tenga en cuenta que Hola 5 minutos se inicia para todos los mensajes en hello mismo tiempo, por lo que tras 5 minutos transcurridos desde la llamada de hello demasiado**get_messages**, los mensajes que no se eliminaron estará visibles de nuevo.</span><span class="sxs-lookup"><span data-stu-id="4adc7-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="4adc7-169">Cómo: obtener la longitud de cola de Hola</span><span class="sxs-lookup"><span data-stu-id="4adc7-169">How to: Get hello queue length</span></span>
<span data-ttu-id="4adc7-170">Puede obtener una estimación del número de Hola de mensajes en una cola.</span><span class="sxs-lookup"><span data-stu-id="4adc7-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="4adc7-171">Hola **download_attributes** método pide tooretrieve de servicio de cola de hello atributos de la cola de hello, incluido el número de mensajes de Hola.</span><span class="sxs-lookup"><span data-stu-id="4adc7-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="4adc7-172">Hola **approximate_message_count** método obtiene el número aproximado de Hola de mensajes en cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="4adc7-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

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

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="4adc7-173">Cómo eliminar una cola</span><span class="sxs-lookup"><span data-stu-id="4adc7-173">How to: Delete a queue</span></span>
<span data-ttu-id="4adc7-174">toodelete una cola y todos los mensajes de Hola contenidos en él, llamada hello **delete_queue_if_exists** método hello en objetos de cola.</span><span class="sxs-lookup"><span data-stu-id="4adc7-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4adc7-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4adc7-175">Next steps</span></span>
<span data-ttu-id="4adc7-176">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn de vínculos más sobre el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4adc7-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="4adc7-177">¿Cómo toouse almacenamiento de blobs de C++</span><span class="sxs-lookup"><span data-stu-id="4adc7-177">How toouse Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="4adc7-178">¿Cómo toouse almacenamiento de tablas de C++</span><span class="sxs-lookup"><span data-stu-id="4adc7-178">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="4adc7-179">Enumeración de los recursos de almacenamiento de Azure en C++</span><span class="sxs-lookup"><span data-stu-id="4adc7-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="4adc7-180">Referencia de la biblioteca de clientes de almacenamiento para C++</span><span class="sxs-lookup"><span data-stu-id="4adc7-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="4adc7-181">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="4adc7-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)