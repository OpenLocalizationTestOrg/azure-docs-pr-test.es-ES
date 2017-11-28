---
title: "Introducción a la API de retransmisión aaaAzure | Documentos de Microsoft"
description: "Información general sobre las API de Azure Relay disponibles"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="31e68-103">API de Relay disponibles</span><span class="sxs-lookup"><span data-stu-id="31e68-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="31e68-104">API de tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="31e68-104">Runtime APIs</span></span>

<span data-ttu-id="31e68-105">Hello tabla siguiente enumeran a todos los clientes en tiempo de ejecución de retransmisión disponibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="31e68-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="31e68-106">Hola [información adicional](#additional-information) sección contiene más información sobre el estado de Hola de cada biblioteca en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="31e68-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="31e68-107">Lenguaje/plataforma</span><span class="sxs-lookup"><span data-stu-id="31e68-107">Language/Platform</span></span> | <span data-ttu-id="31e68-108">Característica disponible</span><span class="sxs-lookup"><span data-stu-id="31e68-108">Available feature</span></span> | <span data-ttu-id="31e68-109">Paquete del cliente</span><span class="sxs-lookup"><span data-stu-id="31e68-109">Client package</span></span> | <span data-ttu-id="31e68-110">Repositorio</span><span class="sxs-lookup"><span data-stu-id="31e68-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="31e68-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="31e68-111">.NET Standard</span></span> | <span data-ttu-id="31e68-112">conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="31e68-112">Hybrid Connections</span></span> | [<span data-ttu-id="31e68-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="31e68-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="31e68-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="31e68-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="31e68-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="31e68-115">.NET Framework</span></span> | <span data-ttu-id="31e68-116">Retransmisión de WCF</span><span class="sxs-lookup"><span data-stu-id="31e68-116">WCF Relay</span></span> | [<span data-ttu-id="31e68-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="31e68-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="31e68-118">N/D</span><span class="sxs-lookup"><span data-stu-id="31e68-118">N/A</span></span> |
| <span data-ttu-id="31e68-119">Nodo</span><span class="sxs-lookup"><span data-stu-id="31e68-119">Node</span></span> | <span data-ttu-id="31e68-120">conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="31e68-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="31e68-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="31e68-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="31e68-122">Información adicional</span><span class="sxs-lookup"><span data-stu-id="31e68-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="31e68-123">.NET</span><span class="sxs-lookup"><span data-stu-id="31e68-123">.NET</span></span>
<span data-ttu-id="31e68-124">ecosistema de .NET de Hello tiene varios tiempos de ejecución, por lo tanto, hay varias bibliotecas de .NET para los concentradores de eventos.</span><span class="sxs-lookup"><span data-stu-id="31e68-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="31e68-125">biblioteca estándar de .NET de Hello puede ejecutarse mediante .NET Core u Hola .NET Framework, mientras la biblioteca de .NET Framework de hello solo puede ejecutarse en un entorno de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="31e68-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="31e68-126">Para ampliar la información sobre las versiones de .NET Framework, consulte [Versiones de marcos de trabajo](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="31e68-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31e68-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="31e68-127">Next steps</span></span>
<span data-ttu-id="31e68-128">toolearn más información acerca de la retransmisión de Azure, visite estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="31e68-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="31e68-129">¿Qué es Relay de Azure?</span><span class="sxs-lookup"><span data-stu-id="31e68-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="31e68-130">Preguntas más frecuentes acerca de Relay</span><span class="sxs-lookup"><span data-stu-id="31e68-130">Relay FAQ</span></span>](relay-faq.md)