---
title: "aaaAzure Premium de Bus de servicio de mensajería estándar precios niveles introducción y | Documentos de Microsoft"
description: "Niveles de mensajería Premium y Estándar de Service Bus"
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a>Niveles de mensajería Premium y Estándar del Bus de servicio

La mensajería de Service Bus, que incluye entidades como colas y temas, combina las funcionalidades de la mensajería empresarial con una completa semántica de publicación-suscripción en la escala de nube. Mensajería de Bus de servicio se utiliza como red troncal de comunicación de Hola para muchas soluciones de nube sofisticadas.

Hola *Premium* capa de mensajería de Bus de servicio trata las solicitudes de cliente comunes alrededor de escala, rendimiento y disponibilidad para aplicaciones de misión crítica. Aunque los conjuntos de características de hello son casi idénticos, estas dos capas de mensajería de Bus de servicio son tooserve diseñada distintos casos de uso.

Algunas diferencias de alto nivel se resaltan en hello en la tabla siguiente.

| Premium | Estándar |
| --- | --- |
| Capacidad de proceso elevada |Capacidad de proceso variable |
| Rendimiento predecible |Latencia variable |
| Precio fijo |Precios según la variante de pago por uso |
| Carga de trabajo de capacidad tooscale arriba y abajo |N/D |
| Tamaño del mensaje too1 MB |Tamaño de mensaje too256 KB |

**Mensajería de Service Bus Premium** proporciona aislamiento de recursos en el nivel de CPU y memoria de Hola para que cada carga de trabajo de cliente se ejecuta de forma aislada. Este contenedor de recursos se llama *unidad de mensajería*. A cada espacio de nombres premium se le asigna al menos una unidad de mensajería. Puede comprar 1, 2 o 4 unidades de mensajería para cada espacio de nombres Premium del Bus de servicio. Una carga de trabajo único o una entidad puede abarcar varias unidades de mensajes y se puede cambiar el número de Hola de unidades de mensajería como desee, aunque es facturación en unas tasas de 24 horas o diaria. resultado de Hello es rendimiento predecible y repetible para su solución basada en el Bus de servicio.

Este rendimiento no es solo más predecible y presenta mayor disponibilidad, sino que también es más rápido. Mensajería Premium de Bus de servicio se basa en el motor de almacenamiento de hello introducida en [centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/). Con la mensajería Premium, es mucho más rápido que con el nivel estándar Hola un buen rendimiento.

## <a name="premium-messaging-technical-differences"></a>Diferencias técnicas de la mensajería Premium

Hello las secciones siguientes describen algunas diferencias entre los niveles de mensajes estándares y Premium.

### <a name="partitioned-queues-and-topics"></a>Temas y colas con particiones

Los temas y colas con particiones se admiten en la mensajería Premium; de hecho, estas entidades siempre tienen particiones (y no se pueden deshabilitar). Sin embargo, Premium particiones colas y temas no funcionan Hola Hola a igual que en los niveles estándar y Basic de Bus de servicio de mensajería. No mensajería Premium usa SQL como almacén de datos y ya no tiene Hola competencia de recursos asociado con una plataforma compartida. Como resultado, no es necesario tooimprove rendimiento particiones. Además, recuento de particiones de hello cambió de 16 particiones en mensajes estándar too2 particiones en Premium. Tener dos particiones garantiza la disponibilidad y es un número más adecuado para el entorno en tiempo de ejecución de hello Premium. 

Con la mensajería Premium, cuando se especifica el tamaño de Hola de una entidad con [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), que tamaño se divide por igual entre las particiones de hello 2, a diferencia de [estándar particiones entidades](service-bus-partitioning.md#standard) en qué Hola tamaño total es 16 veces Hola tamaño especificado. 

Para más información sobre las particiones, consulte [Temas y colas con particiones](service-bus-partitioning.md).

### <a name="express-entities"></a>Entidades exprés

Dado que la mensajería premium se ejecuta en un entorno de tiempo de ejecución completamente aislado, no se admiten entidades rápidas en los espacios de nombres Premium. Para obtener más información acerca de la característica express hello, vea hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) propiedad.

Si tiene código que se ejecuta bajo tooport estándar de mensajería y desea toohello nivel de Premium, que seguro Hola [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) propiedad se establece demasiado**false** (Hola el valor predeterminado).

## <a name="get-started-with-premium-messaging"></a>Introducción a la Mensajería premium

Introducción a mensajería Premium es sencillo y proceso de hello toothat similar de mensajería estándar. Comience con la [creación de un espacio de nombres](service-bus-create-namespace-portal.md). Asegúrese de que selecciona **Premium** en **Plan de tarifa**.

![create-premium-namespace][create-premium-namespace]

También puede crear un [espacios de nombres premium con plantillas de Azure Resource Manager](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).


## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de la mensajería de Bus de servicio, vea Hola temas siguientes.

* [Introducción a la mensajería Premium de Azure Service Bus (entrada de blog)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introducción a la mensajería Premium de Azure Service Bus (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Introducción a la mensajería de Service Bus](service-bus-messaging-overview.md)
* [¿Cómo toouse colas de Service Bus](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
