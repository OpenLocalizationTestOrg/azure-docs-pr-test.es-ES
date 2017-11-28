---
title: aaaHow toouse Queue storage from. Ruby | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate del servicio de cola de Azure de toouse hello y colas de delete y insert, obtener y eliminar mensajes. Los ejemplos están escritos en Ruby."
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
ms.openlocfilehash: c8eacac058442419cb9e8fe62cb69ad7ef1e2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="b3beb-104">¿Cómo toouse Queue storage from. Ruby</span><span class="sxs-lookup"><span data-stu-id="b3beb-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="b3beb-105">Información general</span><span class="sxs-lookup"><span data-stu-id="b3beb-105">Overview</span></span>
<span data-ttu-id="b3beb-106">Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio almacenamiento de cola de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b3beb-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="b3beb-107">ejemplos de Hola se escriben con hello Ruby API de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3beb-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="b3beb-108">Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear y eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="b3beb-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="b3beb-109">Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="b3beb-109">Create a Ruby Application</span></span>
<span data-ttu-id="b3beb-110">Cree una aplicación de Ruby.</span><span class="sxs-lookup"><span data-stu-id="b3beb-110">Create a Ruby application.</span></span> <span data-ttu-id="b3beb-111">Para instrucciones, consulte [Aplicación web de Ruby on Rails en una máquina virtual de Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="b3beb-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="b3beb-112">Configurar la aplicación tooAccess almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b3beb-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="b3beb-113">toouse almacenamiento de Azure, necesitará toodownload y use Hola Ruby paquete de azure, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3beb-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="b3beb-114">Use el paquete de RubyGems tooobtain Hola</span><span class="sxs-lookup"><span data-stu-id="b3beb-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="b3beb-115">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="b3beb-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="b3beb-116">Escriba "indicador instalar azure" en el indicador de hello comando ventana tooinstall hello y dependencias.</span><span class="sxs-lookup"><span data-stu-id="b3beb-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="b3beb-117">Importar paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="b3beb-117">Import hello package</span></span>
<span data-ttu-id="b3beb-118">Utilice el editor de texto, agregue Hola después de la parte superior de toohello de hello archivo Ruby donde piensa toouse almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="b3beb-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="b3beb-119">Configuración de una conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="b3beb-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="b3beb-120">módulo de Hello azure leerá las variables de entorno de hello **AZURE\_almacenamiento\_cuenta** y **AZURE\_almacenamiento\_ACCESS_KEY** para cuenta de almacenamiento de Azure de tooconnect tooyour la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="b3beb-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="b3beb-121">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello antes de usar **Azure::QueueService** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="b3beb-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="b3beb-122">tooobtain estos valores de un clásico o el Administrador de recursos de almacenamiento de la cuenta de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="b3beb-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="b3beb-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3beb-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b3beb-124">Navegar por cuenta de almacenamiento toohello que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="b3beb-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="b3beb-125">En la hoja de configuración de hello en hello derecho, haga clic en **teclas de acceso**.</span><span class="sxs-lookup"><span data-stu-id="b3beb-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="b3beb-126">En la hoja las claves de acceso Hola que aparece, podrá ver clave de acceso de hello 1 y 2 de clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="b3beb-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="b3beb-127">Puede usar cualquiera de estas.</span><span class="sxs-lookup"><span data-stu-id="b3beb-127">You can use either of these.</span></span> 
5. <span data-ttu-id="b3beb-128">Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave.</span><span class="sxs-lookup"><span data-stu-id="b3beb-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

## <a name="how-to-create-a-queue"></a><span data-ttu-id="b3beb-129">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="b3beb-129">How To: Create a Queue</span></span>
<span data-ttu-id="b3beb-130">Hello código siguiente se crea un **Azure::QueueService** objeto, lo que permite toowork con colas.</span><span class="sxs-lookup"><span data-stu-id="b3beb-130">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="b3beb-131">Hola de uso **create_queue()** método toocreate una cola con hello nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="b3beb-131">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="b3beb-132">Inserción de un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="b3beb-132">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="b3beb-133">tooinsert un mensaje en una cola, use hello **create_message()** método toocreate un mensaje nuevo y agregue toohello cola.</span><span class="sxs-lookup"><span data-stu-id="b3beb-133">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="b3beb-134">Cómo: Ver en el siguiente mensaje de Hola</span><span class="sxs-lookup"><span data-stu-id="b3beb-134">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="b3beb-135">Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **peek\_messages()** método.</span><span class="sxs-lookup"><span data-stu-id="b3beb-135">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="b3beb-136">De forma predeterminada, **peek\_messages()** inspecciona un único mensaje.</span><span class="sxs-lookup"><span data-stu-id="b3beb-136">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="b3beb-137">También puede especificar cuántos mensajes desea toopeek.</span><span class="sxs-lookup"><span data-stu-id="b3beb-137">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="b3beb-138">Cómo: Hola siguiente mensaje de eliminación de cola</span><span class="sxs-lookup"><span data-stu-id="b3beb-138">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="b3beb-139">Puede borrar un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="b3beb-139">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="b3beb-140">Cuando se llama a **lista\_messages()**, obtener el siguiente mensaje de Hola en una cola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b3beb-140">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="b3beb-141">También puede especificar cuántos mensajes desea tooget.</span><span class="sxs-lookup"><span data-stu-id="b3beb-141">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="b3beb-142">Hola mensajes procedentes de **lista\_messages()** se convierte en invisible tooany otro código que lee mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="b3beb-142">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="b3beb-143">Pasar en tiempo de espera de visibilidad de hello en segundos como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="b3beb-143">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="b3beb-144">toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="b3beb-144">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="b3beb-145">Este proceso de dos pasos de la eliminación de un mensaje garantiza cuando los tooprocess se produce un error de código puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje e inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="b3beb-145">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="b3beb-146">Las llamadas de código **eliminar\_message()** justo después de que se ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="b3beb-146">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="b3beb-147">Cómo: Cambiar el contenido de Hola de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="b3beb-147">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="b3beb-148">Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3beb-148">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="b3beb-149">código de Hello siguiente utiliza hello **update_message()** método tooupdate un mensaje.</span><span class="sxs-lookup"><span data-stu-id="b3beb-149">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="b3beb-150">método Hello devolverá una tupla que contiene la confirmación de recepción de Hola Hola del mensaje de cola y un valor de hora de fecha UTC que representa al mensaje de saludo será visible en la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3beb-150">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="b3beb-151">Opciones adicionales para extraer mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="b3beb-151">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="b3beb-152">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="b3beb-152">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="b3beb-153">En primer lugar, puede obtener un lote de mensajes.</span><span class="sxs-lookup"><span data-stu-id="b3beb-153">You can get a batch of message.</span></span>
2. <span data-ttu-id="b3beb-154">Puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="b3beb-154">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="b3beb-155">ejemplo de código siguiente Hello usa Hola **lista\_messages()** tooget 15 mensajes de método en una llamada.</span><span class="sxs-lookup"><span data-stu-id="b3beb-155">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="b3beb-156">A continuación, imprime y elimina cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="b3beb-156">Then it prints and deletes each message.</span></span> <span data-ttu-id="b3beb-157">También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="b3beb-157">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="b3beb-158">Cómo: Obtener la longitud de la cola de Hola</span><span class="sxs-lookup"><span data-stu-id="b3beb-158">How To: Get hello Queue Length</span></span>
<span data-ttu-id="b3beb-159">Puede obtener una estimación del número de Hola de mensajes en cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3beb-159">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="b3beb-160">Hola **obtener\_cola\_metadata()** método pide número aproximado de mensajes de Hola de tooreturn de servicio de hello cola y los metadatos acerca de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3beb-160">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="b3beb-161">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="b3beb-161">How To: Delete a Queue</span></span>
<span data-ttu-id="b3beb-162">toodelete una cola y todos los mensajes de Hola contenidas en ella, llamada hello **eliminar\_queue()** método hello en objetos de cola.</span><span class="sxs-lookup"><span data-stu-id="b3beb-162">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="b3beb-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3beb-163">Next Steps</span></span>
<span data-ttu-id="b3beb-164">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b3beb-164">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="b3beb-165">Visite hello [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="b3beb-165">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="b3beb-166">Visite hello [Azure SDK para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repositorio en GitHub</span><span class="sxs-lookup"><span data-stu-id="b3beb-166">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="b3beb-167">Para obtener una comparación entre Hola el servicio de cola de Azure se describe en este artículo y colas de Bus de servicio de Azure descrito en hello [cómo toouse colas de Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) artículo, consulte [colas de Azure y colas de Bus de servicio: comparación y Contrastar](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="b3beb-167">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
