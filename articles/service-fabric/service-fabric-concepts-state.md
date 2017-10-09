---
title: aaaDefinine y administrar el estado en Azure microservicios | Documentos de Microsoft
description: "¿Cómo toodefine y administrar el estado del servicio de Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a>Estado de servicio
**Estado del servicio** hace referencia toohello en memoria o en los datos de disco que un servicio requiere toofunction. Incluye, por ejemplo, las estructuras de datos de Hola y variables de miembro que el servicio de hello lee y escribe toodo trabajo. Dependiendo de cómo se ha diseñado el servicio de hello, también puede incluir archivos u otros recursos que se almacenan en el disco. Por ejemplo, hello archivos de una base de datos utilizaría toostore registros de transacciones y de datos.

Como servicio de ejemplo, consideremos una calculadora. Un servicio de calculadora básica toma dos números y devuelve la suma. Realizar este cálculo no implica ninguna variable de miembro ni otros datos.

Ahora considere la posibilidad de Hola calculadora mismo, pero con un método adicional para almacenar y devolver la suma último Hola se ha calculado. Este servicio ahora tiene estado. Con estado significa que contiene un estado que escribe toowhen calcula una suma nuevo y se lee de cuando se le solicite suma calculada última tooreturn de Hola.

En Azure Service Fabric, el primer servicio de Hola se denomina un servicio sin estado. servicio de segundo de Hola se denomina un servicio con estado.

## <a name="storing-service-state"></a>Almacenamiento del estado de servicio
Estado puede ser externalizado o comparte ubicación con el código de hello es la manipulación de estado de Hola. Externalización de estado normalmente se realiza mediante una base de datos externo o almacenan de otros datos que se ejecuta en distintos equipos a través de red de Hola o fuera de proceso en Hola el mismo equipo. En nuestro ejemplo de la Calculadora, almacén de datos de hello podría ser una base de datos SQL o una instancia de almacén de la tabla de Azure. Cada suma de hello toocompute solicitud realiza una actualización en estos datos y solicita toohello servicio tooreturn Hola valor resultados en el valor actual de Hola que se capturan desde el almacén de Hola. 

Estado también puede coexistir con el código de hello que manipula el estado de saludo. Los servicios con estado de Service Fabric se suelen crear mediante este modelo. Service Fabric proporciona Hola infraestructura tooensure que este estado es altamente disponible, coherente y duradero y que los servicios de hello creados de esta forma pueden escalar fácilmente.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre conceptos de Service Fabric, vea Hola siguientes artículos:

* [Disponibilidad de los servicios de Service Fabric](service-fabric-availability-services.md)
* [Escalabilidad de servicios de Service Fabric](service-fabric-concepts-scalability.md)
* [Creación de particiones de los servicios de Service Fabric](service-fabric-concepts-partitioning.md)
* [Service Fabric Reliable Services](service-fabric-reliable-services-introduction.md)
