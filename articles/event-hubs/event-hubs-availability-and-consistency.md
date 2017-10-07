---
title: aaaAvailability y la coherencia en los centros de eventos de Azure | Documentos de Microsoft
description: "Cómo crea particiones de cantidad máxima de hello tooprovide de disponibilidad y la coherencia con el uso de los centros de eventos de Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a>Disponibilidad y coherencia en Event Hubs

## <a name="overview"></a>Información general
Centros de eventos de Azure usan un [particiones modelo](event-hubs-features.md#partitions) tooimprove disponibilidad y la ejecución en paralelo en un centro de eventos único. Por ejemplo, si un centro de eventos tiene cuatro particiones y una de estas particiones se mueve desde un servidor tooanother en una operación de equilibrio de carga, puede enviar y recibir de tres otras particiones. Además, tener varias particiones permite toohave lectores simultáneos más procesamiento de los datos, mejorar el rendimiento global. Entender las implicaciones de Hola de particiones y el orden en un sistema distribuido es un aspecto crucial de diseño de la solución.

toohelp explican equilibrio de hello entre la ordenación y la disponibilidad, vea hello [teorema CAP](https://en.wikipedia.org/wiki/CAP_theorem), también conocido como teorema de Brewer. Este teorema describe elección Hola entre coherencia, la disponibilidad y tolerancia a la partición.

El teorema de Brewer define la coherencia y la disponibilidad de la forma siguiente:
* Tolerancia de partición: Hola capacidad de un toocontinue de sistema de procesamiento de datos de procesamiento de datos incluso si se produce un error de la partición.
* Disponibilidad: un nodo sin error devuelve una respuesta razonable en un plazo prudente (sin errores ni tiempos de espera).
* : Una lectura se garantiza la coherencia tooreturn hello más reciente de escritura para un cliente determinado.

## <a name="partition-tolerance"></a>Tolerancia a la partición
Event Hubs se basa en un modelo de datos con particiones. Puede configurar Hola número de particiones en el centro de eventos durante la instalación, pero no se puede cambiar este valor más adelante. Puesto que se deben utilizar particiones con concentradores de eventos, tiene una toomake una decisión sobre la disponibilidad y coherencia para la aplicación.

## <a name="availability"></a>Disponibilidad
Hello tooget de manera más sencilla a trabajar con concentradores de eventos es el comportamiento predeterminado de toouse Hola. Si crea un nuevo `EventHubClient` de objetos y usar hello `Send` método, los eventos se distribuyen automáticamente entre las particiones en el centro de eventos. Este comportamiento permite Hola mayor cantidad de tiempo de actividad.

Para los casos de uso que requieren el máximo de hello tiempo, este modelo es preferido.

## <a name="consistency"></a>Coherencia
En algunos casos, puede ser importante Hola clasificación de eventos. Por ejemplo, puede que desee su tooprocess sistema back-end un comando de actualización antes de un comando de eliminación. En este caso, puede establecer la clave de partición de hello en un evento, o usar un `PartitionSender` tooonly objeto enviar eventos tooa determinada partición. Este modo se asegura que si estos eventos se leen desde la partición de hello, se leen en orden.

Con esta configuración, tenga en cuenta que si hello toowhich de partición determinada que está enviando no está disponible, recibirá una respuesta de error. Como punto de comparación, si no tiene una partición única tooa de afinidad, Hola servicio de centros de eventos envía el evento toohello siguiente partición disponible.

Tooensure de solución posible una ordenación, a la vez que también se minimiza el tiempo, sería tooaggregate eventos como parte de la aplicación de procesamiento de eventos. Hola tooaccomplish de manera más fácil esto es toostamp el evento con una propiedad de número de secuencia personalizada. Hola siguiente código muestra un ejemplo:

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

Este ejemplo envía su tooone de eventos de particiones disponibles hello en el centro de eventos y establece el número de secuencia correspondiente de Hola desde su aplicación. Esta solución requiere toobe estado mantenido por la aplicación de procesamiento, pero proporciona a las remitentes de un punto de conexión que es más probable que toobe disponible.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general sobre el servicio Event Hubs](event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](event-hubs-create.md)
