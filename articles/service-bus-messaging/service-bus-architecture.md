---
title: "Introducción a la arquitectura de procesamiento de mensajes de Bus de servicio de aaaAzure | Documentos de Microsoft"
description: Describe la arquitectura de procesamiento de mensajes de Hola de Bus de servicio de Azure.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: f7606e40cdf6db3797a0db2de9365453ff2a158e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-architecture"></a>Arquitectura del Bus de servicio
Este artículo describe la arquitectura de procesamiento de mensajes de Hola de Bus de servicio de Azure.

## <a name="service-bus-scale-units"></a>Unidades de escala del Bus de servicio
El Bus de servicio se organizada por *unidades de escala*. Una unidad de escala es una unidad de implementación y contiene todos los componentes necesarios Hola ejecución servicio. Cada región implementa una o más unidades de escala del Bus de servicio.

Un espacio de nombres de Bus de servicio es la unidad de escala tooa asignada. unidad de escala de Hello controla todos los tipos de entidades de Service Bus (colas, temas, suscripciones). Una unidad de escalado del Bus de servicio consta de Hola de los componentes siguientes:

* **Un conjunto de nodos de puerta de enlace.** Los nodos de puerta de enlace autentican las solicitudes entrantes. Cada nodo de puerta de enlace tiene una dirección IP pública.
* **Un conjunto de nodos de agente de mensajería.** Los nodos de agente de mensajería procesan solicitudes relacionadas con entidades de mensajería.
* **Un almacén de puerta de enlace.** almacén de puerta de enlace de Hello contiene los datos de Hola para todas las entidades que se definen en esta unidad de escala. almacén de puerta de enlace de Hola se implementa en una base de datos de SQL Azure.
* **Varios almacenes de mensajería.** Almacenes de mensajería contienen mensajes de saludo de todas las colas, temas y suscripciones que se definen en esta unidad de escala. También contiene todos los datos de suscripción. A menos que [particiones entidades de mensajería](service-bus-partitioning.md) está habilitado, una cola o tema es almacén de mensajería tooone asignada. Las suscripciones se almacenan en hello mismo almacén de mensajería como su tema primario. Excepto para Service Bus [mensajería Premium](service-bus-premium-messaging.md), almacenes de mensajería de Hola se implementan en las bases de datos de SQL Azure.

## <a name="containers"></a>Contenedores
A cada entidad de mensajería se le asigna a un contenedor específico. Un contenedor es una construcción lógica que utiliza exactamente un toostore de almacén de mensajería todos los datos para este contenedor. Cada contenedor se asigna tooa nodo de broker de mensajería. Normalmente, hay más contenedores que nodos de agente de mensajería. Por tanto, cada nodo de agente de mensajería carga varios contenedores. distribución de Hola de nodo de agente de mensajería de contenedores tooa está organizada de manera que igualmente se cargan todos los nodos de agente de mensajería. Si los cambios de modelo de carga de hello (por ejemplo, uno de hello contenedores obtiene muy ocupado) o si un nodo de broker mensajería deja de estar disponible temporalmente, Hola contenedores se redistribuyen entre nodos de agente de mensajería de Hola.

## <a name="processing-of-incoming-messaging-requests"></a>Procesamiento de solicitudes entrantes de mensajería
Cuando un cliente envía una tooService solicitud Bus, equilibrador de carga de Azure Hola lo enruta tooany de nodos de la puerta de enlace de Hola. nodo de puerta de enlace de Hello autoriza la solicitud de saludo. Si la solicitud de saludo se refiere a una entidad de mensajería (cola, tema, suscripción), nodo de puerta de enlace de hello busca entidad hello en el almacén de puerta de enlace de Hola y determina qué Hola de almacén de mensajería se encuentra la entidad. A continuación, busca qué nodo de broker de mensajería está dando servicio a este contenedor y envía Hola solicitud toothat de nodo de agente de mensajería. Hola de nodo de agente de mensajería procesa la solicitud de Hola y actualiza el estado de la entidad de hello en el almacén de contenedor de Hola. Hola de nodo de agente de mensajería, a continuación, envía Hola respuesta toohello atrás puerta de enlace nodo, que envía a un cliente de toohello espera respuesta adecuada esa solicitud original Hola emitido.

![Procesamiento de solicitudes entrantes de mensajería](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha leído una información general de arquitectura de Bus de servicio, visite Hola siguientes vínculos para obtener más información:

* [Introducción a la mensajería del Bus de servicio](service-bus-messaging-overview.md)
* [Elementos fundamentales del Bus de servicio](service-bus-fundamentals-hybrid-solutions.md)
* Una [solución de mensajería en cola mediante las colas de Service Bus](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


