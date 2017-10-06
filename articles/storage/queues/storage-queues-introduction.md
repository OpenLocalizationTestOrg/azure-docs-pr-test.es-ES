---
title: aaaIntroduction tooAzure almacenamiento de cola | Documentos de Microsoft
description: "Introducción tooAzure almacenamiento de cola"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a>Introducción tooQueues

Almacenamiento de la cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS. Un mensaje de la cola solo puede estar too64 KB de tamaño y una cola puede contener millones de mensajes, seguridad toohello límite de capacidad total de una cuenta de almacenamiento.

## <a name="common-uses"></a>Usos habituales

El almacenamiento en cola suele usarse para realizar las siguientes tareas:

* Crear un trabajo pendiente de tooprocess de trabajo de forma asincrónica
* Pasar mensajes de un rol de trabajador de Azure de tooan de rol web de Azure

## <a name="queue-service-concepts"></a>Conceptos del servicio Queue

Hola servicio cola contiene Hola de los componentes siguientes:

![Conceptos de cola](./media/storage-queues-introduction/queue1.png)

* **Formato de dirección URL:** las colas son direccionables mediante Hola siguiendo el formato de dirección URL:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Hola después de la dirección URL de direcciones una cola en el diagrama de hello:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Cuenta de almacenamiento:** todos los accesos tooAzure almacenamiento se realiza a través de una cuenta de almacenamiento. Consulte [Objetivos de escalabilidad y rendimiento del almacenamiento de Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) para obtener información sobre la capacidad de la cuenta de almacenamiento.

* **Cola:** una cola contiene un conjunto de mensajes. Todos los mensajes deben encontrarse en una cola. Tenga en cuenta que ese nombre de cola de hello debe estar en minúsculas. Para más información, consulte [Asignar nombres a colas y metadatos](https://msdn.microsoft.com/library/azure/dd179349.aspx).

* **Mensaje:** un mensaje, en cualquier formato, de seguridad too64 KB. tiempo máximo de Hola que un mensaje puede permanecer en la cola de hello es siete días.

## <a name="next-steps"></a>Pasos siguientes

* [crear una cuenta de almacenamiento](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Introducción a las colas con .NET](storage-dotnet-how-to-use-queues.md)
