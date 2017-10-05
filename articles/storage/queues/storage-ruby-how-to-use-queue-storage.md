---
title: Uso de Queue Storage en Ruby | Microsoft Docs
description: "Aprenda a utilizar el servicio Cola de Azure para crear y eliminar colas e insertar, obtener y eliminar mensajes. Los ejemplos están escritos en Ruby."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: b1a7dd36af6c45bf085342cdf9c1c926a5040792
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-ruby"></a><span data-ttu-id="c3229-104">Uso del almacenamiento de colas de Ruby</span><span class="sxs-lookup"><span data-stu-id="c3229-104">How to use Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="c3229-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c3229-105">Overview</span></span>
<span data-ttu-id="c3229-106">Esta guía muestra cómo realizar algunas tareas comunes a través del servicio de almacenamiento en cola de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c3229-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="c3229-107">Los ejemplos están escritos usando la API Ruby de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3229-107">The samples are written using the Ruby Azure API.</span></span>
<span data-ttu-id="c3229-108">Entre los escenarios descritos se incluyen **insertar**, **ojear**, **obtener** y **eliminar** mensajes de la cola, así como **crear y eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="c3229-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="c3229-109">Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="c3229-109">Create a Ruby Application</span></span>
<span data-ttu-id="c3229-110">Cree una aplicación de Ruby.</span><span class="sxs-lookup"><span data-stu-id="c3229-110">Create a Ruby application.</span></span> <span data-ttu-id="c3229-111">Para instrucciones, consulte [Aplicación web de Ruby on Rails en una máquina virtual de Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="c3229-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="c3229-112">Configuración de la aplicación para obtener acceso al almacenamiento</span><span class="sxs-lookup"><span data-stu-id="c3229-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="c3229-113">Para usar el almacenamiento de Azure tendrá que descargar y usar el paquete Ruby azure, que incluye un conjunto de útiles bibliotecas que se comunican con los servicios REST de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c3229-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="c3229-114">Uso de RubyGems para obtener el paquete</span><span class="sxs-lookup"><span data-stu-id="c3229-114">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="c3229-115">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="c3229-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="c3229-116">Escriba "gem install azure" en la ventana de comandos para instalar la gema y las dependencias.</span><span class="sxs-lookup"><span data-stu-id="c3229-116">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="c3229-117">Importación del paquete</span><span class="sxs-lookup"><span data-stu-id="c3229-117">Import the package</span></span>
<span data-ttu-id="c3229-118">Con el editor de texto que prefiera, agregue lo siguiente al principio del archivo de Ruby en el que pretenda utilizar el almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="c3229-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="c3229-119">Configuración de una conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c3229-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="c3229-120">El módulo azure leerá las variables de entorno **AZURE\_STORAGE\_ACCOUNT** y **AZURE\_STORAGE\_ACCESS_KEY** para obtener información necesaria para conectarse a su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c3229-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="c3229-121">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta antes de usar **Azure::QueueService** con el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="c3229-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="c3229-122">Para obtener estos valores desde una cuenta de almacenamiento de Azure Resource Manager o clásica en el Portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="c3229-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="c3229-123">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c3229-123">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c3229-124">Vaya a la cuenta de almacenamiento que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="c3229-124">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="c3229-125">En la hoja Configuración que se encuentra a la derecha, haga clic en **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="c3229-125">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="c3229-126">En la hoja Claves de acceso que aparece, verá la clave de acceso 1 y 2.</span><span class="sxs-lookup"><span data-stu-id="c3229-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="c3229-127">Puede usar cualquiera de estas.</span><span class="sxs-lookup"><span data-stu-id="c3229-127">You can use either of these.</span></span> 
5. <span data-ttu-id="c3229-128">Haga clic en el icono de copia para copiar la clave en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="c3229-128">Click the copy icon to copy the key to the clipboard.</span></span> 

## <a name="how-to-create-a-queue"></a><span data-ttu-id="c3229-129">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="c3229-129">How To: Create a Queue</span></span>
<span data-ttu-id="c3229-130">El siguiente código crea un objeto **Azure::QueueService** , que permite trabajar con colas.</span><span class="sxs-lookup"><span data-stu-id="c3229-130">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="c3229-131">Utilice el método **create_queue()** para crear una cola con el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="c3229-131">Use the **create_queue()** method to create a queue with the specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="c3229-132">Inserción de un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="c3229-132">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="c3229-133">Para insertar un mensaje en una cola, utilice el método **create_message()** para crear un nuevo mensaje y agregarlo a la cola.</span><span class="sxs-lookup"><span data-stu-id="c3229-133">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="c3229-134">Inspección del siguiente mensaje</span><span class="sxs-lookup"><span data-stu-id="c3229-134">How To: Peek at the Next Message</span></span>
<span data-ttu-id="c3229-135">Puede inspeccionar el mensaje situado en la parte delantera de una cola, sin quitarlo de la cola, mediante una llamada al método **peek\_messages()**.</span><span class="sxs-lookup"><span data-stu-id="c3229-135">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span></span> <span data-ttu-id="c3229-136">De forma predeterminada, **peek\_messages()** inspecciona un único mensaje.</span><span class="sxs-lookup"><span data-stu-id="c3229-136">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="c3229-137">También puede indicar cuántos mensajes desea inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="c3229-137">You can also specify how many messages you want to peek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="c3229-138">Extracción del siguiente mensaje de la cola</span><span class="sxs-lookup"><span data-stu-id="c3229-138">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="c3229-139">Puede borrar un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="c3229-139">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="c3229-140">Al llamar a **list\_messages()**, obtiene, de forma predeterminada, el siguiente mensaje en una cola.</span><span class="sxs-lookup"><span data-stu-id="c3229-140">When you call **list\_messages()**, you get the next message in a queue by default.</span></span> <span data-ttu-id="c3229-141">También puede indicar cuántos mensajes desea obtener.</span><span class="sxs-lookup"><span data-stu-id="c3229-141">You can also specify how many messages you want to get.</span></span> <span data-ttu-id="c3229-142">Los mensajes devueltos por **list\_messages()** se hacen invisibles para cualquier otro código que lea mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="c3229-142">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="c3229-143">Usted proporciona el tiempo de espera de la visibilidad en segundos a modo de parámetro.</span><span class="sxs-lookup"><span data-stu-id="c3229-143">You pass in the visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="c3229-144">Para terminar quitando el mensaje de la cola, también debe llamar a **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="c3229-144">To finish removing the message from the queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="c3229-145">Este proceso de extracción de un mensaje que consta de dos pasos garantiza que si su código no puede procesar un mensaje a causa de un error de hardware o software, otra instancia de su código puede obtener el mismo mensaje e intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c3229-145">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="c3229-146">El código llama a **delete\_message()** justo después de que se haya procesado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="c3229-146">Your code calls **delete\_message()** right after the message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="c3229-147">Cambio del contenido de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="c3229-147">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="c3229-148">Puede cambiar el contenido de un mensaje local en la cola.</span><span class="sxs-lookup"><span data-stu-id="c3229-148">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="c3229-149">El código siguiente usa el método **update_message()** para actualizar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="c3229-149">The code below uses the **update_message()** method to update a message.</span></span> <span data-ttu-id="c3229-150">Este método devolverá una tupla que contiene la recepción de confirmación del mensaje en cola y un valor de fecha y hora UTC que representa el momento en que el mensaje estará visible en la cola.</span><span class="sxs-lookup"><span data-stu-id="c3229-150">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="c3229-151">Opciones adicionales para extraer mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="c3229-151">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="c3229-152">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="c3229-152">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="c3229-153">En primer lugar, puede obtener un lote de mensajes.</span><span class="sxs-lookup"><span data-stu-id="c3229-153">You can get a batch of message.</span></span>
2. <span data-ttu-id="c3229-154">En segundo lugar, puede establecer un tiempo de espera de la invisibilidad más largo o más corto para que el código disponga de más o menos tiempo para procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="c3229-154">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="c3229-155">El siguiente ejemplo de código utiliza el método **list\_messages()** para obtener 15 mensajes en una llamada.</span><span class="sxs-lookup"><span data-stu-id="c3229-155">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span></span> <span data-ttu-id="c3229-156">A continuación, imprime y elimina cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="c3229-156">Then it prints and deletes each message.</span></span> <span data-ttu-id="c3229-157">También establece el tiempo de espera de la invisibilidad en cinco minutos para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="c3229-157">It also sets the invisibility timeout to five minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="c3229-158">Obtención de la longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="c3229-158">How To: Get the Queue Length</span></span>
<span data-ttu-id="c3229-159">Puede obtener una estimación del número de mensajes existentes en la cola.</span><span class="sxs-lookup"><span data-stu-id="c3229-159">You can get an estimation of the number of messages in the queue.</span></span> <span data-ttu-id="c3229-160">El método **get\_queue\_metadata()** solicita a Queue service que devuelva el recuento aproximado de mensajes y metadatos sobre la cola.</span><span class="sxs-lookup"><span data-stu-id="c3229-160">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="c3229-161">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="c3229-161">How To: Delete a Queue</span></span>
<span data-ttu-id="c3229-162">Para eliminar una cola y todos los mensajes contenidos en ella, llame al método **delete\_queue()** en el objeto de cola.</span><span class="sxs-lookup"><span data-stu-id="c3229-162">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="c3229-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3229-163">Next Steps</span></span>
<span data-ttu-id="c3229-164">Ahora que está familiarizado con los aspectos básicos del almacenamiento de colas, utilice estos vínculos para obtener más información acerca de tareas de almacenamiento más complejas.</span><span class="sxs-lookup"><span data-stu-id="c3229-164">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="c3229-165">Visite el [blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="c3229-165">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="c3229-166">Visite el repositorio de [SDK de Azure para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) en GitHub</span><span class="sxs-lookup"><span data-stu-id="c3229-166">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="c3229-167">Podrá encontrar una comparación entre Azure Queue Service, que se explica en este artículo, y Azure Service Bus Queues, que se explican en el artículo [Utilización de las colas de Service Bus](/develop/ruby/how-to-guides/service-bus-queues/), en el documento [Colas de Azure y Colas de Service Bus: comparación y diferencias](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md).</span><span class="sxs-lookup"><span data-stu-id="c3229-167">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>