---
title: "Información general sobre API de Azure Relay | Microsoft Docs"
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
ms.openlocfilehash: 8d93a0344adc3b0b7617f3a7d85124142d7a7555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="d6221-103">API de Relay disponibles</span><span class="sxs-lookup"><span data-stu-id="d6221-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="d6221-104">API de tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="d6221-104">Runtime APIs</span></span>

<span data-ttu-id="d6221-105">La siguiente table enumera todos los clientes del runtime de Relay disponibles.</span><span class="sxs-lookup"><span data-stu-id="d6221-105">The following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="d6221-106">La sección de [información adicional](#additional-information) contiene más información sobre el estado de cada biblioteca de runtime.</span><span class="sxs-lookup"><span data-stu-id="d6221-106">The [additional information](#additional-information) section contains more information about the status of each runtime library.</span></span>

| <span data-ttu-id="d6221-107">Lenguaje/plataforma</span><span class="sxs-lookup"><span data-stu-id="d6221-107">Language/Platform</span></span> | <span data-ttu-id="d6221-108">Característica disponible</span><span class="sxs-lookup"><span data-stu-id="d6221-108">Available feature</span></span> | <span data-ttu-id="d6221-109">Paquete del cliente</span><span class="sxs-lookup"><span data-stu-id="d6221-109">Client package</span></span> | <span data-ttu-id="d6221-110">Repositorio</span><span class="sxs-lookup"><span data-stu-id="d6221-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6221-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="d6221-111">.NET Standard</span></span> | <span data-ttu-id="d6221-112">conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="d6221-112">Hybrid Connections</span></span> | [<span data-ttu-id="d6221-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="d6221-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="d6221-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="d6221-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="d6221-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d6221-115">.NET Framework</span></span> | <span data-ttu-id="d6221-116">Retransmisión de WCF</span><span class="sxs-lookup"><span data-stu-id="d6221-116">WCF Relay</span></span> | [<span data-ttu-id="d6221-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="d6221-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="d6221-118">N/D</span><span class="sxs-lookup"><span data-stu-id="d6221-118">N/A</span></span> |
| <span data-ttu-id="d6221-119">Nodo</span><span class="sxs-lookup"><span data-stu-id="d6221-119">Node</span></span> | <span data-ttu-id="d6221-120">conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="d6221-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="d6221-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="d6221-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="d6221-122">Información adicional</span><span class="sxs-lookup"><span data-stu-id="d6221-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="d6221-123">.NET</span><span class="sxs-lookup"><span data-stu-id="d6221-123">.NET</span></span>
<span data-ttu-id="d6221-124">El ecosistema de .NET tiene varios entornos de ejecución y, por tanto, hay varias bibliotecas de .NET para Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d6221-124">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="d6221-125">La biblioteca de .NET Standard se puede ejecutar mediante .NET Core o .NET Framework, mientras que la biblioteca de .NET Framework solo puede ejecutarse en un entorno de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d6221-125">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="d6221-126">Para ampliar la información sobre las versiones de .NET Framework, consulte [Versiones de marcos de trabajo](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="d6221-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6221-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6221-127">Next steps</span></span>
<span data-ttu-id="d6221-128">Para obtener más información sobre Azure Relay, visite estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="d6221-128">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="d6221-129">¿Qué es Relay de Azure?</span><span class="sxs-lookup"><span data-stu-id="d6221-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="d6221-130">Preguntas más frecuentes acerca de Relay</span><span class="sxs-lookup"><span data-stu-id="d6221-130">Relay FAQ</span></span>](relay-faq.md)