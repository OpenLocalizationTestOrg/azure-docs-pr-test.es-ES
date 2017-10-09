---
title: "Introducción a la API de concentradores de eventos aaaAzure | Documentos de Microsoft"
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
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="3f722-103">API disponibles de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3f722-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="3f722-104">API de tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="3f722-104">Runtime APIs</span></span>

<span data-ttu-id="3f722-105">Hola aquí te mostramos una descripción de todos los clientes en tiempo de ejecución de los centros de eventos de Azure está disponibles.</span><span class="sxs-lookup"><span data-stu-id="3f722-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="3f722-106">Aunque algunas de estas bibliotecas también incluyen la funcionalidad de administración limitada, también hay [determinadas bibliotecas](#management-apis) dedicado toomanagement operaciones.</span><span class="sxs-lookup"><span data-stu-id="3f722-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="3f722-107">enfoque de núcleo de Hola de estas bibliotecas es toosend y recibir mensajes desde un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="3f722-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="3f722-108">Vea [información adicional](#additional-information) para obtener más detalles sobre el estado actual de cada biblioteca en tiempo de ejecución Hola.</span><span class="sxs-lookup"><span data-stu-id="3f722-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="3f722-109">Lenguaje/plataforma</span><span class="sxs-lookup"><span data-stu-id="3f722-109">Language/Platform</span></span> | <span data-ttu-id="3f722-110">Paquete del cliente</span><span class="sxs-lookup"><span data-stu-id="3f722-110">Client package</span></span> | <span data-ttu-id="3f722-111">Paquete EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="3f722-111">EventProcessorHost package</span></span> | <span data-ttu-id="3f722-112">Repositorio</span><span class="sxs-lookup"><span data-stu-id="3f722-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3f722-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="3f722-113">.NET Standard</span></span> | [<span data-ttu-id="3f722-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="3f722-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="3f722-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="3f722-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="3f722-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="3f722-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="3f722-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3f722-117">.NET Framework</span></span> | [<span data-ttu-id="3f722-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="3f722-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="3f722-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="3f722-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="3f722-120">N/D</span><span class="sxs-lookup"><span data-stu-id="3f722-120">N/A</span></span> |
| <span data-ttu-id="3f722-121">Java</span><span class="sxs-lookup"><span data-stu-id="3f722-121">Java</span></span> | [<span data-ttu-id="3f722-122">Maven</span><span class="sxs-lookup"><span data-stu-id="3f722-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="3f722-123">Maven</span><span class="sxs-lookup"><span data-stu-id="3f722-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="3f722-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="3f722-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="3f722-125">Nodo</span><span class="sxs-lookup"><span data-stu-id="3f722-125">Node</span></span> | [<span data-ttu-id="3f722-126">NPM</span><span class="sxs-lookup"><span data-stu-id="3f722-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="3f722-127">N/D</span><span class="sxs-lookup"><span data-stu-id="3f722-127">N/A</span></span> | [<span data-ttu-id="3f722-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="3f722-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="3f722-129">C</span><span class="sxs-lookup"><span data-stu-id="3f722-129">C</span></span> | <span data-ttu-id="3f722-130">N/D</span><span class="sxs-lookup"><span data-stu-id="3f722-130">N/A</span></span> | <span data-ttu-id="3f722-131">N/D</span><span class="sxs-lookup"><span data-stu-id="3f722-131">N/A</span></span> | [<span data-ttu-id="3f722-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="3f722-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="3f722-133">Información adicional</span><span class="sxs-lookup"><span data-stu-id="3f722-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="3f722-134">.NET</span><span class="sxs-lookup"><span data-stu-id="3f722-134">.NET</span></span>
<span data-ttu-id="3f722-135">ecosistema de .NET de Hello tiene varios tiempos de ejecución, por lo tanto, hay varias bibliotecas de .NET para los concentradores de eventos.</span><span class="sxs-lookup"><span data-stu-id="3f722-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="3f722-136">biblioteca estándar de .NET de Hello puede ejecutarse mediante .NET Core u Hola .NET Framework, mientras la biblioteca de .NET Framework de hello solo puede ejecutarse en un entorno de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3f722-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="3f722-137">Para ampliar la información sobre las versiones de .NET Framework, consulte [Versiones de marcos de trabajo](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="3f722-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="3f722-138">Nodo</span><span class="sxs-lookup"><span data-stu-id="3f722-138">Node</span></span>

<span data-ttu-id="3f722-139">biblioteca de Node.js Hola está actualmente en versión preliminar y se mantiene como un proyecto secundario por los empleados de Microsoft y colaboradores externos.</span><span class="sxs-lookup"><span data-stu-id="3f722-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="3f722-140">Todas las contribuciones, incluido código fuente, son bienvenidas y se revisarán.</span><span class="sxs-lookup"><span data-stu-id="3f722-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="3f722-141">API de administración</span><span class="sxs-lookup"><span data-stu-id="3f722-141">Management APIs</span></span>

<span data-ttu-id="3f722-142">Hola aquí te mostramos una lista de todas las bibliotecas específicas de administración está disponible.</span><span class="sxs-lookup"><span data-stu-id="3f722-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="3f722-143">Ninguna de estas bibliotecas contienen operaciones de tiempo de ejecución y son para propósitos de Hola de administración de entidades de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="3f722-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="3f722-144">Lenguaje/plataforma</span><span class="sxs-lookup"><span data-stu-id="3f722-144">Language/Platform</span></span> | <span data-ttu-id="3f722-145">Paquete de administración</span><span class="sxs-lookup"><span data-stu-id="3f722-145">Management package</span></span> | <span data-ttu-id="3f722-146">Repositorio</span><span class="sxs-lookup"><span data-stu-id="3f722-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3f722-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="3f722-147">.NET Standard</span></span> | [<span data-ttu-id="3f722-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="3f722-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="3f722-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="3f722-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="3f722-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f722-150">Next steps</span></span>
<span data-ttu-id="3f722-151">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="3f722-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="3f722-152">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3f722-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="3f722-153">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="3f722-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="3f722-154">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3f722-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)