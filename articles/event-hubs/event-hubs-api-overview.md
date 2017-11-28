---
title: "Introducción a la API de Azure Event Hubs | Microsoft Docs"
description: "Información general sobre las API de Azure Event Hubs disponibles"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 40cd76e1aacb68d6051cae4a3c90a8970f5449f0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="026bc-103">API disponibles de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="026bc-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="026bc-104">API de tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="026bc-104">Runtime APIs</span></span>

<span data-ttu-id="026bc-105">A continuación, se muestra una descripción de todos los clientes del tiempo de ejecución de Azure Event Hubs disponibles.</span><span class="sxs-lookup"><span data-stu-id="026bc-105">The following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="026bc-106">Aunque algunas de estas bibliotecas también incluyen la funcionalidad de administración limitada, también hay [determinadas bibliotecas](#management-apis) dedicadas a las operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="026bc-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="026bc-107">El enfoque central de estas bibliotecas es enviar y recibir mensajes de un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="026bc-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="026bc-108">Consulte la [información adicional](#additional-information) para más detalles sobre el estado actual de cada biblioteca del entorno de ejecución.</span><span class="sxs-lookup"><span data-stu-id="026bc-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="026bc-109">Lenguaje/plataforma</span><span class="sxs-lookup"><span data-stu-id="026bc-109">Language/Platform</span></span> | <span data-ttu-id="026bc-110">Paquete del cliente</span><span class="sxs-lookup"><span data-stu-id="026bc-110">Client package</span></span> | <span data-ttu-id="026bc-111">Paquete EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="026bc-111">EventProcessorHost package</span></span> | <span data-ttu-id="026bc-112">Repositorio</span><span class="sxs-lookup"><span data-stu-id="026bc-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="026bc-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="026bc-113">.NET Standard</span></span> | [<span data-ttu-id="026bc-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="026bc-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="026bc-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="026bc-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="026bc-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="026bc-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="026bc-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="026bc-117">.NET Framework</span></span> | [<span data-ttu-id="026bc-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="026bc-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="026bc-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="026bc-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="026bc-120">N/D</span><span class="sxs-lookup"><span data-stu-id="026bc-120">N/A</span></span> |
| <span data-ttu-id="026bc-121">Java</span><span class="sxs-lookup"><span data-stu-id="026bc-121">Java</span></span> | [<span data-ttu-id="026bc-122">Maven</span><span class="sxs-lookup"><span data-stu-id="026bc-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="026bc-123">Maven</span><span class="sxs-lookup"><span data-stu-id="026bc-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="026bc-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="026bc-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="026bc-125">Nodo</span><span class="sxs-lookup"><span data-stu-id="026bc-125">Node</span></span> | [<span data-ttu-id="026bc-126">NPM</span><span class="sxs-lookup"><span data-stu-id="026bc-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="026bc-127">N/D</span><span class="sxs-lookup"><span data-stu-id="026bc-127">N/A</span></span> | [<span data-ttu-id="026bc-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="026bc-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="026bc-129">C</span><span class="sxs-lookup"><span data-stu-id="026bc-129">C</span></span> | <span data-ttu-id="026bc-130">N/D</span><span class="sxs-lookup"><span data-stu-id="026bc-130">N/A</span></span> | <span data-ttu-id="026bc-131">N/D</span><span class="sxs-lookup"><span data-stu-id="026bc-131">N/A</span></span> | [<span data-ttu-id="026bc-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="026bc-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="026bc-133">Información adicional</span><span class="sxs-lookup"><span data-stu-id="026bc-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="026bc-134">.NET</span><span class="sxs-lookup"><span data-stu-id="026bc-134">.NET</span></span>
<span data-ttu-id="026bc-135">El ecosistema de .NET tiene varios entornos de ejecución y, por tanto, hay varias bibliotecas de .NET para Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="026bc-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="026bc-136">La biblioteca de .NET Standard se puede ejecutar mediante .NET Core o .NET Framework, mientras que la biblioteca de .NET Framework solo puede ejecutarse en un entorno de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="026bc-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="026bc-137">Para ampliar la información sobre las versiones de .NET Framework, consulte [Versiones de marcos de trabajo](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="026bc-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="026bc-138">Nodo</span><span class="sxs-lookup"><span data-stu-id="026bc-138">Node</span></span>

<span data-ttu-id="026bc-139">La biblioteca de Node.js está en versión preliminar y los empleados de Microsoft y colaboradores externos la mantienen como un proyecto secundario.</span><span class="sxs-lookup"><span data-stu-id="026bc-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="026bc-140">Todas las contribuciones, incluido código fuente, son bienvenidas y se revisarán.</span><span class="sxs-lookup"><span data-stu-id="026bc-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="026bc-141">API de administración</span><span class="sxs-lookup"><span data-stu-id="026bc-141">Management APIs</span></span>

<span data-ttu-id="026bc-142">A continuación se proporciona una lista de todas las bibliotecas específicas de administración disponibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="026bc-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="026bc-143">Ninguna de estas bibliotecas contiene operaciones de entornos de ejecución y son exclusivamente para administrar las entidades de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="026bc-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="026bc-144">Lenguaje/plataforma</span><span class="sxs-lookup"><span data-stu-id="026bc-144">Language/Platform</span></span> | <span data-ttu-id="026bc-145">Paquete de administración</span><span class="sxs-lookup"><span data-stu-id="026bc-145">Management package</span></span> | <span data-ttu-id="026bc-146">Repositorio</span><span class="sxs-lookup"><span data-stu-id="026bc-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="026bc-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="026bc-147">.NET Standard</span></span> | [<span data-ttu-id="026bc-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="026bc-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="026bc-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="026bc-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="026bc-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="026bc-150">Next steps</span></span>
<span data-ttu-id="026bc-151">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="026bc-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="026bc-152">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="026bc-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="026bc-153">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="026bc-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="026bc-154">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="026bc-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)