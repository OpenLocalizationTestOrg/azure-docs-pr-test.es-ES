---
title: aaaHow toouse almacenamiento de cola de Python | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola servicio de cola de Azure de Python toocreate y eliminar colas, insertar, obtener y eliminar mensajes."
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
ms.openlocfilehash: f4f902a2c314401e5c1768fbc80566c8ba25c058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="0e181-103">¿Cómo toouse almacenamiento de cola de Python</span><span class="sxs-lookup"><span data-stu-id="0e181-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="0e181-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0e181-104">Overview</span></span>
<span data-ttu-id="0e181-105">Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio de almacenamiento de cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e181-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="0e181-106">ejemplos de Hello están escritos en Python y usar hello [SDK de almacenamiento de Microsoft Azure para Python].</span><span class="sxs-lookup"><span data-stu-id="0e181-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="0e181-107">Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear y eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="0e181-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="0e181-108">Para obtener más información sobre las colas, consulte la sección toohello [pasos].</span><span class="sxs-lookup"><span data-stu-id="0e181-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="0e181-109">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="0e181-109">How To: Create a Queue</span></span>
<span data-ttu-id="0e181-110">Hola **QueueService** objeto le permite trabajar con colas.</span><span class="sxs-lookup"><span data-stu-id="0e181-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="0e181-111">Hello código siguiente se crea un **QueueService** objeto.</span><span class="sxs-lookup"><span data-stu-id="0e181-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="0e181-112">Agregue los siguiente Hola cerca de la parte superior de Hola de cualquier archivo de Python en el que desea acceso tooprogrammatically almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="0e181-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="0e181-113">Hello código siguiente se crea un **QueueService** objeto mediante la clave de cuenta y el nombre de la cuenta del almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="0e181-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="0e181-114">Reemplace 'myaccount' y 'mykey' por la clave y el nombre de cuenta.</span><span class="sxs-lookup"><span data-stu-id="0e181-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="0e181-115">Inserción de un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="0e181-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="0e181-116">tooinsert un mensaje en una cola, use hello **colocar\_mensaje** método para crear un nuevo mensaje y agregar toohello cola.</span><span class="sxs-lookup"><span data-stu-id="0e181-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="0e181-117">Cómo: Ver en el siguiente mensaje de Hola</span><span class="sxs-lookup"><span data-stu-id="0e181-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="0e181-118">Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **peek\_mensajes** método.</span><span class="sxs-lookup"><span data-stu-id="0e181-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="0e181-119">De forma predeterminada, **peek\_messages** inspecciona un único mensaje.</span><span class="sxs-lookup"><span data-stu-id="0e181-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="0e181-120">Cómo quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="0e181-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="0e181-121">El código borra un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="0e181-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="0e181-122">Cuando se llama a **obtener\_mensajes**, obtener el siguiente mensaje de Hola en una cola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0e181-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="0e181-123">Un mensaje devuelto de **obtener\_mensajes** se convierte en invisible tooany otro código que lee mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="0e181-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="0e181-124">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="0e181-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="0e181-125">toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **eliminar\_mensaje**.</span><span class="sxs-lookup"><span data-stu-id="0e181-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="0e181-126">Este proceso de dos pasos de la eliminación de un mensaje garantiza que cuando el código produce un error tooprocess un mensaje debido a un error de hardware o software, otra instancia del código puede obtener el mismo mensaje y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="0e181-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="0e181-127">Las llamadas de código **eliminar\_mensaje** justo después de que se ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="0e181-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="0e181-128">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="0e181-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="0e181-129">En primer lugar, puede obtener un lote de mensajes (arriba too32).</span><span class="sxs-lookup"><span data-stu-id="0e181-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="0e181-130">En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="0e181-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="0e181-131">siguiente Hola código de ejemplo utiliza la **obtener\_mensajes** mensajes tooget 16 de método en una llamada.</span><span class="sxs-lookup"><span data-stu-id="0e181-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="0e181-132">A continuación, procesa cada mensaje con un bucle for.</span><span class="sxs-lookup"><span data-stu-id="0e181-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="0e181-133">También establece tiempo de espera de invisibilidad de hello en cinco minutos para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="0e181-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="0e181-134">Cómo: Cambiar el contenido de Hola de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="0e181-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="0e181-135">Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e181-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="0e181-136">Si el mensaje representa una tarea de trabajo, puede usar este tooupdate característica el estado de la tarea de trabajo de hello.</span><span class="sxs-lookup"><span data-stu-id="0e181-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="0e181-137">código de Hello siguiente utiliza hello **actualizar\_mensaje** método tooupdate un mensaje.</span><span class="sxs-lookup"><span data-stu-id="0e181-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="0e181-138">tiempo de espera de visibilidad de Hola se establece too0, lo que significa que el mensaje aparece inmediatamente y se actualizó el contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e181-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="0e181-139">Cómo: Obtener la longitud de la cola de Hola</span><span class="sxs-lookup"><span data-stu-id="0e181-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="0e181-140">Puede obtener una estimación del número de Hola de mensajes en una cola.</span><span class="sxs-lookup"><span data-stu-id="0e181-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="0e181-141">El **obtener\_cola\_metadatos** método pide Hola cola servicio tooreturn metadatos acerca de la cola de Hola y Hola **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="0e181-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="0e181-142">resultado de Hello solo es aproximado porque los mensajes se pueden agregar o quitar después de que el servicio cola responde tooyour solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e181-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="0e181-143">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="0e181-143">How To: Delete a Queue</span></span>
<span data-ttu-id="0e181-144">toodelete una cola y todos los mensajes de Hola contenidas en ella, llame a la **eliminar\_cola** método.</span><span class="sxs-lookup"><span data-stu-id="0e181-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="0e181-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e181-145">Next Steps</span></span>
<span data-ttu-id="0e181-146">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="0e181-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="0e181-147">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="0e181-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="0e181-148">API de REST de servicios de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="0e181-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="0e181-149">[Blog del equipo de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="0e181-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="0e181-150">[SDK de almacenamiento de Microsoft Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="0e181-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog del equipo de almacenamiento de Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[SDK de almacenamiento de Microsoft Azure para Python]: https://github.com/Azure/azure-storage-python