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
# <a name="introduction-tooqueues"></a><span data-ttu-id="e0c34-103">Introducción tooQueues</span><span class="sxs-lookup"><span data-stu-id="e0c34-103">Introduction tooQueues</span></span>

<span data-ttu-id="e0c34-104">Almacenamiento de la cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e0c34-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="e0c34-105">Un mensaje de la cola solo puede estar too64 KB de tamaño y una cola puede contener millones de mensajes, seguridad toohello límite de capacidad total de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0c34-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="e0c34-106">Usos habituales</span><span class="sxs-lookup"><span data-stu-id="e0c34-106">Common uses</span></span>

<span data-ttu-id="e0c34-107">El almacenamiento en cola suele usarse para realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e0c34-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="e0c34-108">Crear un trabajo pendiente de tooprocess de trabajo de forma asincrónica</span><span class="sxs-lookup"><span data-stu-id="e0c34-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="e0c34-109">Pasar mensajes de un rol de trabajador de Azure de tooan de rol web de Azure</span><span class="sxs-lookup"><span data-stu-id="e0c34-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="e0c34-110">Conceptos del servicio Queue</span><span class="sxs-lookup"><span data-stu-id="e0c34-110">Queue service concepts</span></span>

<span data-ttu-id="e0c34-111">Hola servicio cola contiene Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0c34-111">hello Queue service contains hello following components:</span></span>

![Conceptos de cola](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="e0c34-113">**Formato de dirección URL:** las colas son direccionables mediante Hola siguiendo el formato de dirección URL:</span><span class="sxs-lookup"><span data-stu-id="e0c34-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="e0c34-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="e0c34-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="e0c34-115">Hola después de la dirección URL de direcciones una cola en el diagrama de hello:</span><span class="sxs-lookup"><span data-stu-id="e0c34-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="e0c34-116">**Cuenta de almacenamiento:** todos los accesos tooAzure almacenamiento se realiza a través de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0c34-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="e0c34-117">Consulte [Objetivos de escalabilidad y rendimiento del almacenamiento de Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) para obtener información sobre la capacidad de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0c34-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="e0c34-118">**Cola:** una cola contiene un conjunto de mensajes.</span><span class="sxs-lookup"><span data-stu-id="e0c34-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="e0c34-119">Todos los mensajes deben encontrarse en una cola.</span><span class="sxs-lookup"><span data-stu-id="e0c34-119">All messages must be in a queue.</span></span> <span data-ttu-id="e0c34-120">Tenga en cuenta que ese nombre de cola de hello debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e0c34-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="e0c34-121">Para más información, consulte [Asignar nombres a colas y metadatos](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0c34-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="e0c34-122">**Mensaje:** un mensaje, en cualquier formato, de seguridad too64 KB.</span><span class="sxs-lookup"><span data-stu-id="e0c34-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="e0c34-123">tiempo máximo de Hola que un mensaje puede permanecer en la cola de hello es siete días.</span><span class="sxs-lookup"><span data-stu-id="e0c34-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0c34-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0c34-124">Next steps</span></span>

* [<span data-ttu-id="e0c34-125">crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e0c34-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="e0c34-126">Introducción a las colas con .NET</span><span class="sxs-lookup"><span data-stu-id="e0c34-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
