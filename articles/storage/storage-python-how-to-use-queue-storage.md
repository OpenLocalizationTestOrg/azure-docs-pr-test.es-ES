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
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a>¿Cómo toouse almacenamiento de cola de Python
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio de almacenamiento de cola de Azure. ejemplos de Hello están escritos en Python y usar hello [SDK de almacenamiento de Microsoft Azure para Python]. Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear y eliminar colas**. Para obtener más información sobre las colas, consulte la sección toohello [pasos].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>Creación de una cola
Hola **QueueService** objeto le permite trabajar con colas. Hello código siguiente se crea un **QueueService** objeto. Agregue los siguiente Hola cerca de la parte superior de Hola de cualquier archivo de Python en el que desea acceso tooprogrammatically almacenamiento de Azure:

```python
from azure.storage.queue import QueueService
```

Hello código siguiente se crea un **QueueService** objeto mediante la clave de cuenta y el nombre de la cuenta del almacenamiento Hola. Reemplace 'myaccount' y 'mykey' por la clave y el nombre de cuenta.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Inserción de un mensaje en una cola
tooinsert un mensaje en una cola, use hello **colocar\_mensaje** método para crear un nuevo mensaje y agregar toohello cola.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>Cómo: Ver en el siguiente mensaje de Hola
Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **peek\_mensajes** método. De forma predeterminada, **peek\_messages** inspecciona un único mensaje.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>Cómo quitar mensajes de la cola
El código borra un mensaje de una cola en dos pasos. Cuando se llama a **obtener\_mensajes**, obtener el siguiente mensaje de Hola en una cola de forma predeterminada. Un mensaje devuelto de **obtener\_mensajes** se convierte en invisible tooany otro código que lee mensajes de esta cola. De forma predeterminada, este mensaje permanece invisible durante 30 segundos. toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **eliminar\_mensaje**. Este proceso de dos pasos de la eliminación de un mensaje garantiza que cuando el código produce un error tooprocess un mensaje debido a un error de hardware o software, otra instancia del código puede obtener el mismo mensaje y vuelva a intentarlo. Las llamadas de código **eliminar\_mensaje** justo después de que se ha procesado el mensaje de bienvenida.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

Hay dos formas de personalizar la recuperación de mensajes de una cola.
En primer lugar, puede obtener un lote de mensajes (arriba too32). En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje. siguiente Hola código de ejemplo utiliza la **obtener\_mensajes** mensajes tooget 16 de método en una llamada. A continuación, procesa cada mensaje con un bucle for. También establece tiempo de espera de invisibilidad de hello en cinco minutos para cada mensaje.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Cómo: Cambiar el contenido de Hola de un mensaje en cola
Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola. Si el mensaje representa una tarea de trabajo, puede usar este tooupdate característica el estado de la tarea de trabajo de hello. código de Hello siguiente utiliza hello **actualizar\_mensaje** método tooupdate un mensaje. tiempo de espera de visibilidad de Hola se establece too0, lo que significa que el mensaje aparece inmediatamente y se actualizó el contenido de Hola.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>Cómo: Obtener la longitud de la cola de Hola
Puede obtener una estimación del número de Hola de mensajes en una cola. El **obtener\_cola\_metadatos** método pide Hola cola servicio tooreturn metadatos acerca de la cola de Hola y Hola **approximate_message_count**. resultado de Hello solo es aproximado porque los mensajes se pueden agregar o quitar después de que el servicio cola responde tooyour solicitud.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>Eliminación de una cola
toodelete una cola y todos los mensajes de Hola contenidas en ella, llame a la **eliminar\_cola** método.

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn de vínculos más.

* [Centro para desarrolladores de Python](/develop/python/)
* [API de REST de servicios de almacenamiento de Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog del equipo de almacenamiento de Azure]
* [SDK de almacenamiento de Microsoft Azure para Python]

[Blog del equipo de almacenamiento de Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[SDK de almacenamiento de Microsoft Azure para Python]: https://github.com/Azure/azure-storage-python