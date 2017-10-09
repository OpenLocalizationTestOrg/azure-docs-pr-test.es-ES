---
title: "aaaApplication escenarios y diseño | Documentos de Microsoft"
description: "Información general de las categorías de las aplicaciones de nube en Service Fabric. Describe el diseño de la aplicación que usa servicios con estado y sin estado."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 7/02/2017
ms.author: mfussell
ms.openlocfilehash: e36d5b2d21a6a1e3e85c9b21190072616e4921e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-scenarios"></a>Escenarios de aplicación de Service Fabric
Azure Service Fabric ofrece una plataforma confiable y flexible que permite toowrite y ejecutar muchos tipos de servicios y aplicaciones empresariales. Estas aplicaciones y microservicios pueden encontrarse con o sin estado, y son recursos equilibrada en máquinas virtuales toomaximize eficacia. la arquitectura única Hola de Service Fabric permite tooperform cerca de análisis de datos en tiempo real, el cálculo de en memoria, transacciones paralelas y en las aplicaciones de procesamiento de eventos. Puede escalar o reducir verticalmente sus aplicaciones con facilidad (en realidad hacia dentro o hacia fuera), dependiendo de sus requisitos de recursos variables.

plataforma de Service Fabric Hello en Azure es ideal para hello siguientes categorías de aplicaciones:

* **Servicios de alta disponibilidad**: los servicios de Service Fabric proporcionan conmutación por error rápida mediante la creación de varias réplicas de servicio secundarias. Si un nodo, un proceso o servicio individuales se bloquea debido a toohardware u otro error, una de las réplicas secundarias de Hola es tooa promocionadas réplica principal con la mínima pérdida de servicio.
* **Servicios escalables**: servicios individuales se pueden crear particiones, lo que permite escalada horizontalmente en clúster de Hola de toobe de estado. Además, servicios individuales se pueden crear y quitados en marcha de Hola. Servicios rápida y fácilmente escalar horizontalmente de algunas instancias en unos toothousands de nodos de instancias en muchos nodos y escalar la en nuevo, dependiendo de sus necesidades de recursos. Puede utilizar estos servicios de Service Fabric toobuild y administrar su ciclo de vida completo.
* **Cálculo de datos no estáticos**: Service Fabric permite datos toobuild, entrada/salida y aplicaciones con estado de proceso intensivo. Service Fabric permite la colocación de Hola de procesamiento (cálculo) y los datos en las aplicaciones. Normalmente, cuando la aplicación requiere acceso toodata, hay latencia de red asociada a un nivel de caché o almacenamiento de datos externos. Con servicios Service Fabric con estado, esa latencia se elimina, lo que permite unas lecturas y escrituras de mayor rendimiento. Por ejemplo, supongamos que tiene una aplicación que realiza una selección de recomendaciones en tiempo real para los clientes con un requisito de tiempo de ida y vuelta inferior a 100 milisegundos. características de rendimiento y latencia de Hello de servicios de Service Fabric (donde cálculo Hola de selección de recomendación se coloca con datos de Hola y reglas) proporciona un usuario de toohello de experiencia con capacidad de respuesta en comparación con la implementación estándar de Hola modelo de tener toofetch Hola necesario datos del almacenamiento remoto.  
* **Aplicaciones interactivas basadas en sesión**: Service Fabric es útil si sus aplicaciones, como juegos en línea o mensajería instantánea, requieren lecturas y escrituras de baja latencia. Service Fabric permite toobuild estas aplicaciones interactivas y con estado sin necesidad de toocreate un almacén independiente o la memoria caché, según sea necesario para las aplicaciones sin estado. (Esto aumenta la latencia y es posible que presente problemas de coherencia).
* **Análisis de datos y los flujos de trabajo**: Hola rápidas lecturas y escrituras de Service Fabric permiten que las aplicaciones que se deben procesar de forma confiable eventos o flujos de datos. Service Fabric también permite que las aplicaciones que describen las canalizaciones de procesamiento, donde los resultados deben ser confiable y se haya pasado en toohello fase sin pérdida de procesamiento a continuación. Estos incluyen sistemas transaccionales y financieros, donde las garantías de procesamiento y coherencia de datos son fundamentales.
* **Recopilación de datos, procesamiento y IoT**: puesto que Service Fabric controla gran escala y tiene una latencia baja a través de sus servicios con estado, es ideal para el procesamiento de datos en millones de dispositivos que son datos hello de dispositivo de Hola y el cálculo de Hola colocados.
Hemos visto varios clientes que han desarrollado sistemas IoT con Service Fabric incluido [BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/), [Schneider Electric](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/) y [Mesh Systems](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/).

## <a name="application-design-case-studies"></a>Casos prácticos de diseño de aplicaciones
Un número de casos prácticos para ver cómo Service Fabric es toodesign usa aplicaciones se publica en hello [blog del equipo de Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/) hello y [sitio de soluciones de microservicios](https://azure.microsoft.com/solutions/microservice-applications/).

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>Diseño de aplicaciones compuestas por microservicios sin y con estado
La creación de aplicaciones con roles de trabajo del servicio en la nube de Azure es un ejemplo de servicios sin estado. En cambio, microservicios con estado mantienen su estado autorizado más allá de la solicitud de Hola y su respuesta. Esto proporciona alta disponibilidad y la coherencia del estado de Hola a través de la API simples que proporcionan garantías transaccionales respaldados por la replicación. Servicios con estado de Service Fabric democratice la alta disponibilidad, ponerlo tooall tipos de aplicaciones, no solo en las bases de datos y otros almacenes de datos. Se trata de una progresión natural. Las aplicaciones ya se han movido del uso de las bases de datos puramente relacionales para bases de datos de alta disponibilidad tooNoSQL. Ahora pueden tener las mismas aplicaciones de hello su estado "en caliente" y los datos administrados dentro de ellos para mejoras de rendimiento adicionales sin sacrificar la confiabilidad, coherencia o la disponibilidad.

Al compilar aplicaciones que se compone de microservicios, suelen tener una combinación de las aplicaciones web sin estado (ASP.NET, Node.js, etc.) realizar llamadas en servicios de nivel intermedio de negocio con y sin estado, todas implementadas en hello mismo clúster de Service Fabric mediante comandos de implementación de Service Fabric Hola. Cada uno de estos servicios es independiente con tener en cuenta tooscale, confiabilidad, uso y los recursos, lo que mejora enormemente la agilidad en desarrollo y administración del ciclo.

Con estado microservicios simplifican diseños de aplicaciones ya que eliminan la necesidad de Hola para colas adicionales de Hola y las memorias caché que han sido tradicionalmente tooaddress necesario Hola requisitos de disponibilidad y la latencia de las aplicaciones sin estado puramente. Puesto que los servicios con estado naturalmente son altamente disponible y baja latencia, esto significa que hay menos toomanage partes móvil en la aplicación como un todo. diagramas de Hello siguiente ilustran las diferencias de hello entre diseñar una aplicación que no tiene estada y otra que está activo. Aprovechando las ventajas de hello [servicios confiables](service-fabric-reliable-services-introduction.md) y [Reliable Actors](service-fabric-reliable-actors-introduction.md) modelos de programación, servicios con estado reducen la complejidad de la aplicación al conseguir un alto rendimiento y baja latencia.

## <a name="an-application-built-using-stateless-services"></a>Una aplicación compilada con servicios sin estado
![Aplicación que hace uso del servicio sin estado][Image1]

## <a name="an-application-built-using-stateful-services"></a>Una aplicación compilada con servicios con estado
![Aplicación que hace uso del servicio sin estado][Image2]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes

* Escuchar demasiado[casos prácticos de clientes](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
)
* Información sobre [casos prácticos de clientes](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)
* Más información sobre [patrones y escenarios](service-fabric-patterns-and-scenarios.md)

* Introducción a servicios de compilación y sin estado con hello Service Fabric [servicios confiables](service-fabric-reliable-services-quick-start.md) y [actores confiables](service-fabric-reliable-actors-get-started.md) modelos de programación.
* Consulte también Hola temas siguientes:
  * [Quiero información acerca de los microservicios](service-fabric-overview-microservices.md)
  * [Estado de servicio](service-fabric-concepts-state.md)
  * [Disponibilidad de los servicios de Service Fabric](service-fabric-availability-services.md)
  * [Escalación de aplicaciones de Service Fabric](service-fabric-concepts-scalability.md)
  * [Cómo crear particiones de los servicios confiables de Service Fabric](service-fabric-concepts-partitioning.md)

[Image1]: media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: media/service-fabric-application-scenarios/AppwithStatefulServices.jpg
