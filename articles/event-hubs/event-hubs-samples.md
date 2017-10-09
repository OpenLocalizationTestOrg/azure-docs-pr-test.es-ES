---
title: ejemplos de los centros de eventos aaaAzure | Documentos de Microsoft
description: Ejemplos de Azure Event Hubs
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a>Ejemplos de Event Hubs 

conjunto de ejemplos de los centros de eventos de Azure Hello muestra las características claves de [centros de eventos de Azure](/azure/event-hubs/). En este artículo se clasifica y describe los ejemplos de hello disponibles, con vínculos tooeach.

En tiempo de Hola de redactar este artículo, los ejemplos de los centros de eventos se encuentran en distintos lugares:

- [Ejemplos de código para desarrolladores de MSDN](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Para obtener más información sobre las diferentes versiones de .NET Framework de hello, consulte [marcos de trabajo y los destinos](/dotnet/articles/standard/frameworks).

Se agregarán más ejemplos con el tiempo, así que revise este sitio con frecuencia para comprobar las actualizaciones.

## <a name="net-standard"></a>.NET Standard

Hello en los ejemplos siguientes se muestran cómo toosend y recibir eventos mediante hello [cliente de los centros de eventos](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) para hello [biblioteca estándar de .NET](/dotnet/articles/standard/library).

### <a name="send-events"></a>Envío de eventos 

Hola [empezar a enviar](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) muestra cómo toowrite un núcleo de .NET consola aplicación que envía el concentrador de eventos de tooan de eventos.

### <a name="receive-events"></a>Recepción de eventos 

Hola [empezar a recibir con hello Host procesador de eventos](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) ejemplo es una aplicación de consola .NET Core que recibe los mensajes de un concentrador de eventos mediante Hola Host procesador de eventos.

## <a name="net-framework"></a>.NET Framework   

Estos ejemplos muestran varias otras características de los centros de eventos de Azure, como destino Hola [biblioteca de .NET Framework](/dotnet/framework/index).
 
### <a name="notify-users-of-events-received"></a>Notificación a los usuarios sobre los eventos recibidos

Hola [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) ejemplo notifica a los usuarios de los datos recibidos de sensores u otros sistemas.

### <a name="get-started-with-event-hubs"></a>Introducción a los Centros de eventos 

Hola [evento Introducción a concentradores](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) muestra capacidades básicas de Hola de centros de eventos, como cómo enviar concentrador de eventos de eventos tooan toocreate un centro de eventos y consumir eventos mediante hello [Host de procesador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>Escalado horizontal del procesamiento de eventos 

Hola [escalar horizontalmente el procesamiento de eventos](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) ejemplo muestra cómo hello toouse [Host procesador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) carga de trabajo de toodistribute Hola de consumo de la secuencia de los centros de eventos. Muestra cómo hello tooimplement **EventProcessor** y **EventProcessorFactory** flujo de eventos de objetos toomanage Hola. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>Extracción de datos de SQL a un centro de eventos

Hola [de datos de SQL de extracción](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) ejemplo muestra cómo toopull datos desde una instancia de SQL de la tabla y empújelo concentrador de eventos tooan, toouse como una entrada en aplicaciones analíticas siguen en la cadena.

### <a name="pull-web-data-into-an-event-hub"></a>Extracción de datos web a un centro de eventos 

Hola [importar datos desde web hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) ejemplo muestra cómo toopull datos desde public fuentes (por ejemplo Hola información del departamento de transporte tráfico de fuentes de distribución) y empújelo tooan concentrador de eventos.

## <a name="next-steps"></a>Pasos siguientes

Más información acerca de las versiones de .NET Framework visitando Hola siguientes vínculos:

- [Marcos y destinos](/dotnet/articles/standard/frameworks)
- [.NET Framework 4.6 y 4.5](/dotnet/framework/index)

Puede obtener más información acerca de los centros de eventos en hello siguientes artículos:

- [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
- [Creación de un centro de eventos](event-hubs-create.md)
- [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)