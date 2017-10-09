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
# <a name="available-event-hubs-apis"></a>API disponibles de Event Hubs

## <a name="runtime-apis"></a>API de tiempo de ejecución

Hola aquí te mostramos una descripción de todos los clientes en tiempo de ejecución de los centros de eventos de Azure está disponibles. Aunque algunas de estas bibliotecas también incluyen la funcionalidad de administración limitada, también hay [determinadas bibliotecas](#management-apis) dedicado toomanagement operaciones. enfoque de núcleo de Hola de estas bibliotecas es toosend y recibir mensajes desde un centro de eventos.

Vea [información adicional](#additional-information) para obtener más detalles sobre el estado actual de cada biblioteca en tiempo de ejecución Hola.

| Lenguaje/plataforma | Paquete del cliente | Paquete EventProcessorHost | Repositorio |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET Framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | N/D |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| Nodo | [NPM](https://www.npmjs.com/package/azure-event-hubs) | N/D | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | N/D | N/D | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>Información adicional

#### <a name="net"></a>.NET
ecosistema de .NET de Hello tiene varios tiempos de ejecución, por lo tanto, hay varias bibliotecas de .NET para los concentradores de eventos. biblioteca estándar de .NET de Hello puede ejecutarse mediante .NET Core u Hola .NET Framework, mientras la biblioteca de .NET Framework de hello solo puede ejecutarse en un entorno de .NET Framework. Para ampliar la información sobre las versiones de .NET Framework, consulte [Versiones de marcos de trabajo](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).

#### <a name="node"></a>Nodo

biblioteca de Node.js Hola está actualmente en versión preliminar y se mantiene como un proyecto secundario por los empleados de Microsoft y colaboradores externos. Todas las contribuciones, incluido código fuente, son bienvenidas y se revisarán.

## <a name="management-apis"></a>API de administración

Hola aquí te mostramos una lista de todas las bibliotecas específicas de administración está disponible. Ninguna de estas bibliotecas contienen operaciones de tiempo de ejecución y son para propósitos de Hola de administración de entidades de los centros de eventos.

| Lenguaje/plataforma | Paquete de administración | Repositorio |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](event-hubs-create.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)