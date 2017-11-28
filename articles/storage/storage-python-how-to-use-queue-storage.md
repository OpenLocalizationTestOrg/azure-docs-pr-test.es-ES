---
title: Uso de Queue Storage en Python | Microsoft Docs
description: Aprenda a usar el servicio de colas de Azure de Python para crear y eliminar colas e insertar, obtener y eliminar mensajes.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 1ad3ba6853edda93034b84996823262cb017c71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="f8ef1-103">Uso del almacenamiento de colas de Python</span><span class="sxs-lookup"><span data-stu-id="f8ef1-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="f8ef1-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f8ef1-104">Overview</span></span>
<span data-ttu-id="f8ef1-105">Esta guía muestra cómo realizar algunas tareas comunes a través del servicio de almacenamiento en cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="f8ef1-106">Los ejemplos están escritos en Python y usan el [SDK de Almacenamiento de Microsoft Azure para Python].</span><span class="sxs-lookup"><span data-stu-id="f8ef1-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="f8ef1-107">Entre los escenarios descritos se incluyen **insertar**, **ojear**, **obtener** y **eliminar** mensajes de la cola, así como **crear y eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="f8ef1-108">Para obtener más información acerca de las colas, consulte la sección [Pasos siguientes].</span><span class="sxs-lookup"><span data-stu-id="f8ef1-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="f8ef1-109">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="f8ef1-109">How To: Create a Queue</span></span>
<span data-ttu-id="f8ef1-110">El objeto **QueueService** permite trabajar con colas.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="f8ef1-111">El siguiente código crea un objeto **QueueService** .</span><span class="sxs-lookup"><span data-stu-id="f8ef1-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="f8ef1-112">Agregue lo siguiente cerca de la parte superior de todo archivo Python en el que desee obtener acceso al almacenamiento de Azure mediante programación:</span><span class="sxs-lookup"><span data-stu-id="f8ef1-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="f8ef1-113">El código siguiente crea un objeto **QueueService** utilizando el nombre de la cuenta de almacenamiento y la clave de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="f8ef1-114">Reemplace 'myaccount' y 'mykey' por la clave y el nombre de cuenta.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="f8ef1-115">Inserción de un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="f8ef1-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="f8ef1-116">Para insertar un mensaje en una cola, use el método **put\_message** para crear un nuevo mensaje y agregarlo a la cola.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="f8ef1-117">Inspección del siguiente mensaje</span><span class="sxs-lookup"><span data-stu-id="f8ef1-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="f8ef1-118">Puede inspeccionar el mensaje situado en la parte delantera de una cola, sin quitarlo de la cola, mediante una llamada al método **peek\_messages**.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="f8ef1-119">De forma predeterminada, **peek\_messages** inspecciona un único mensaje.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="f8ef1-120">Cómo quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="f8ef1-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="f8ef1-121">El código borra un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="f8ef1-122">Si llama a **get\_messages**, obtiene, de forma predeterminada, el siguiente mensaje en una cola.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="f8ef1-123">Un mensaje devuelto por **get\_messages** se hace invisible a cualquier otro código de lectura de mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="f8ef1-124">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="f8ef1-125">Para terminar de quitar el mensaje de la cola, también debe llamar a **delete\_message**.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="f8ef1-126">Este proceso de extracción de un mensaje que consta de dos pasos garantiza que si su código no puede procesar un mensaje a causa de un error de hardware o software, otra instancia de su código puede obtener el mismo mensaje e intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="f8ef1-127">Su código llama a **delete\_message** justo después de que se haya procesado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="f8ef1-128">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="f8ef1-129">En primer lugar, puede obtener un lote de mensajes (hasta 32).</span><span class="sxs-lookup"><span data-stu-id="f8ef1-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="f8ef1-130">En segundo lugar, puede establecer un tiempo de espera de la invisibilidad más largo o más corto para que el código disponga de más o menos tiempo para procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="f8ef1-131">El siguiente ejemplo de código utiliza el método **get\_messages** para obtener 16 mensajes en una llamada.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="f8ef1-132">A continuación, procesa cada mensaje con un bucle for.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="f8ef1-133">También establece el tiempo de espera de la invisibilidad en cinco minutos para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="f8ef1-134">Cambio del contenido de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="f8ef1-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="f8ef1-135">Puede cambiar el contenido de un mensaje local en la cola.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="f8ef1-136">Si el mensaje representa una tarea de trabajo, puede usar esta característica para actualizar el estado de la tarea de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="f8ef1-137">El código siguiente utiliza el método **update\_message** para actualizar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="f8ef1-138">El tiempo de espera de visibilidad se establece en 0, lo que significa que el mensaje aparece inmediatamente y se actualiza el contenido.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="f8ef1-139">Obtención de la longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="f8ef1-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="f8ef1-140">Puede obtener una estimación del número de mensajes existentes en una cola.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="f8ef1-141">El método **get\_queue\_metadata** solicita a Queue service que devuelva los metadatos sobre la cola y **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="f8ef1-142">El resultado solo es aproximado, ya que se pueden agregar o borrar mensajes después de que el servicio de cola haya respondido su solicitud.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="f8ef1-143">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="f8ef1-143">How To: Delete a Queue</span></span>
<span data-ttu-id="f8ef1-144">Para eliminar una cola y todos los mensajes contenidos en ella, llame al método **delete\_queue**.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="f8ef1-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8ef1-145">Next Steps</span></span>
<span data-ttu-id="f8ef1-146">Ahora que está familiarizado con los aspectos básicos del Almacenamiento en cola, siga estos vínculos para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f8ef1-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="f8ef1-147">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="f8ef1-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="f8ef1-148">API de REST de servicios de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="f8ef1-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="f8ef1-149">[Blog del equipo de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="f8ef1-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="f8ef1-150">[SDK de Almacenamiento de Microsoft Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="f8ef1-150">[Microsoft Azure Storage SDK for Python]</span></span>

<span data-ttu-id="f8ef1-151">[Blog del equipo de almacenamiento de Azure]: http://blogs.msdn.com/b/windowsazurestorage/</span><span class="sxs-lookup"><span data-stu-id="f8ef1-151">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/</span></span>
<span data-ttu-id="f8ef1-152">[SDK de Almacenamiento de Microsoft Azure para Python]: https://github.com/Azure/azure-storage-python</span><span class="sxs-lookup"><span data-stu-id="f8ef1-152">[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python</span></span>