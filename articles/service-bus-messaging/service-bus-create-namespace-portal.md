---
title: aaaHow toocreate un espacio de nombres de Bus de servicio en hello portal de Azure | Documentos de Microsoft
description: Crear un espacio de nombres de Bus de servicio mediante Hola portal de Azure.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a><span data-ttu-id="6d2b2-103">Crear un espacio de nombres de Bus de servicio mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6d2b2-103">Create a Service Bus namespace using hello Azure portal</span></span>

<span data-ttu-id="6d2b2-104">Un espacio de nombres es un contenedor con un ámbito para todos los componentes de la mensajería.</span><span class="sxs-lookup"><span data-stu-id="6d2b2-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="6d2b2-105">Varias colas y temas pueden residir en un único espacio de nombres, y los espacios de nombres suelen servir de contenedores de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d2b2-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="6d2b2-106">Hay dos maneras diferentes toocreate un espacio de nombres de Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="6d2b2-106">There are two different ways toocreate a Service Bus namespace:</span></span>

1. <span data-ttu-id="6d2b2-107">Azure Portal (este artículo)</span><span class="sxs-lookup"><span data-stu-id="6d2b2-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="6d2b2-108">[Plantillas de Resource Manager][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="6d2b2-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-hello-azure-portal"></a><span data-ttu-id="6d2b2-109">Crear un espacio de nombres en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6d2b2-109">Create a namespace in hello Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="6d2b2-110">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="6d2b2-110">Congratulations!</span></span> <span data-ttu-id="6d2b2-111">Ha creado un espacio de nombres de mensajería de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6d2b2-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d2b2-112">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d2b2-112">Next steps</span></span>

<span data-ttu-id="6d2b2-113">Visite nuestro [ejemplos de GitHub][github-samples], que muestran algunos de hello características de mensajería de Bus de servicio de Azure más avanzadas.</span><span class="sxs-lookup"><span data-stu-id="6d2b2-113">Check out our [GitHub samples][github-samples], which show some of hello more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
