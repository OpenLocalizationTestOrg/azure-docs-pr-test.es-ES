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
# <a name="available-relay-apis"></a>API de Relay disponibles

## <a name="runtime-apis"></a>API de tiempo de ejecución

Hello tabla siguiente enumeran a todos los clientes en tiempo de ejecución de retransmisión disponibles actualmente.

Hola [información adicional](#additional-information) sección contiene más información sobre el estado de Hola de cada biblioteca en tiempo de ejecución.

| Lenguaje/plataforma | Característica disponible | Paquete del cliente | Repositorio |
| --- | --- | --- | --- |
| .NET Standard | conexiones híbridas | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET Framework | Retransmisión de WCF | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | N/D |
| Nodo | conexiones híbridas | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>Información adicional

#### <a name="net"></a>.NET
ecosistema de .NET de Hello tiene varios tiempos de ejecución, por lo tanto, hay varias bibliotecas de .NET para los concentradores de eventos. biblioteca estándar de .NET de Hello puede ejecutarse mediante .NET Core u Hola .NET Framework, mientras la biblioteca de .NET Framework de hello solo puede ejecutarse en un entorno de .NET Framework. Para ampliar la información sobre las versiones de .NET Framework, consulte [Versiones de marcos de trabajo](/dotnet/articles/standard/frameworks#framework-versions).

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la retransmisión de Azure, visite estos vínculos:
* [¿Qué es Relay de Azure?](relay-what-is-it.md)
* [Preguntas más frecuentes acerca de Relay](relay-faq.md)