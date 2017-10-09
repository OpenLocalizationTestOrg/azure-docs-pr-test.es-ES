---
title: "Hola aaaIntroducing Administrador de recursos de clúster de tejido de servicio | Documentos de Microsoft"
description: "Un administrador de recursos de clúster de tejido de servicio de introducción toohello."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: cfab735b-923d-4246-a2a8-220d4f4e0c64
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e815925880e2f3a755294de1dcfb9b88fbdde08a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-hello-service-fabric-cluster-resource-manager"></a>Introducción a Administrador de recursos de clúster de Service Fabric Hola
Tradicionalmente administrar servicios en línea o sistemas de TI había diseñado dedicar específico máquinas físicas o virtuales toothose servicios concretos o sistemas. Los servicios se diseñaban como capas. Podía haber una capa "web" y una capa "datos" o "almacenamiento". Las aplicaciones tengan un nivel de mensajería donde las solicitudes fluidas de entrada y salida, así como un conjunto de máquinas dedicado toocaching. Cada tipo de carga de trabajo o nivel tenía máquinas específicas dedicado tooit: base de datos de hello tiene dos máquinas tooit dedicado, servidores web de hello algunos. Si un tipo determinado de carga de trabajo debe máquinas Hola que se encontraba en toorun demasiado activo, agregar más máquinas con ese mismo nivel toothat de configuración. Sin embargo, no todas las cargas de trabajo se pueden escalar horizontalmente tan fácilmente, especialmente con capa de datos de hello normalmente reemplazaría máquinas con máquinas más grandes. Así de sencillo. Si se produce un error en una máquina, esa parte de hello aplicación global se ejecutaba en capacidad inferior hasta que se puede restaurar el equipo de Hola. Esto sigue siendo sencillo (aunque no necesariamente divertido).

Ahora, sin embargo Hola mundo de servicio y arquitectura de software ha cambiado. Es más habitual que las aplicaciones hayan adoptado un diseño de escalado horizontal. Es habitual la compilación de aplicaciones con contenedores o microservicios (o ambos). Ahora, aunque todavía puede tener solo unas pocas máquinas, no se ejecutan como una única instancia de una carga de trabajo. Pueden incluso ejecutarse varias cargas de trabajo diferentes en hello mismo tiempo. Ahora tiene docenas de tipos de servicios distintos (ninguno de los cuales consume los recursos de toda una máquina), quizás cientos de instancias distintas de esos servicios. Cada instancia con nombre tendría una o más instancias o réplicas para alta disponibilidad (HA). Dependiendo de los tamaños de Hola de las cargas de trabajo y el grado de ocupación son, probable que se encuentre con cientos o miles de equipos. 

De repente administrando el entorno no es tan sencillo como administrar unos máquinas toosingle dedicado tipos de cargas de trabajo. Los servidores son virtuales y ya no tienen nombres (han conmutado actitudes de [toocattle mascotas](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20) después de que todos). La configuración es menor sobre máquinas de Hola y más información acerca de los propios servicios Hola. Hardware que está dedicado tooa única instancia de una carga de trabajo es en gran medida algo Hola anterior. Los propios servicios se han convertido en pequeños sistemas distribuidos que abarcan múltiples piezas pequeñas de hardware estándar.

Dado que la aplicación ya no es una serie de monolitos repartidos en varios niveles, ahora dispone de muchos más toodeal de combinaciones con. ¿Quién decide qué tipos de cargas de trabajo pueden ejecutarse en cada hardware o cuántas? ¿Las cargas de trabajo funcionan bien en hello mismo hardware y que están en conflicto? Cuando una máquina deja de funcionar, ¿cómo sabe lo que se estaba ejecutando en esa máquina? ¿Quién es el responsable de asegurarse de que esa carga de trabajo empiece a ejecutarse de nuevo? Espera para la copia de toocome de hello máquina (virtual)? o ¿las cargas de trabajo conmutan por error automáticamente tooother máquinas y seguir en ejecución? ¿Se requiere la intervención humana? ¿Qué pasa con las actualizaciones en este entorno?

Como los desarrolladores y operadores que trabaja en este entorno, vamos ayuda toowant administrar esta complejidad. ¿Una contratación por comilona y complejidad de hello toohide con personas probablemente no son respuesta correcta de hello, por lo que lo que hacemos?

## <a name="introducing-orchestrators"></a>Presentación de los organizadores
"Organizador" es Hola término general que un elemento de software que ayuda a los administradores a administrar estos tipos de entornos. Orchestrators son componentes de Hola que llevar a cabo en las solicitudes como "Me gustaría cinco copias de este servicio se ejecuta en mi entorno". Intentan toomake Hola coincidencia Hola deseado estado del entorno, con independencia de lo que ocurre.

Los orquestadores (y no el personal humano) son los que entran en acción cuando una máquina falla o cuando una carga de trabajo finaliza por algún motivo inesperado. La mayoría de los orquestadores no solo administran los errores. Otras características que tienen es administrar implementaciones nuevas, controlar las actualizaciones y administrar el consumo de recursos y gobierno. Todos los orchestrators son fundamentalmente acerca del mantenimiento de algún estado deseado de configuración en el entorno de Hola. Desea toobe pueda tootell organizador la esperada y que Hola trabajo pesado. Aurora de Mesos, Docker Datacenter/Docker Swarm, Kubernetes y Service Fabric son ejemplos de orquestadores. Estas orchestrators se están toomeet activamente desarrollado Hola necesidades de cargas de trabajo reales en entornos de producción. 

## <a name="orchestration-as-a-service"></a>La organización como servicio
Hola, Administrador de recursos del clúster es el componente del sistema de Hola que controla la orquestación de Service Fabric. trabajo del Administrador de recursos de clúster Hola se divide en tres partes:

1. Aplicar reglas
2. Optimizar el entorno
3. Ayudar con otros procesos

toosee cómo funciona Hola, Administrador de recursos del clúster, vea Hola después de vídeo Microsoft Virtual Academy:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>Qué no es
En las aplicaciones tradicionales de nivel N siempre hubo un [equilibrador de carga](https://en.wikipedia.org/wiki/Load_balancing_(computing)). Normalmente esto era un equilibrador de carga de red (NLB) o un equilibrador de carga de aplicación (ALB) dependiendo de dónde SAT. en la pila de red de Hola. Algunos equilibradores de carga se basan en componentes de hardware, como la oferta de BigIP de F5, y otros en componentes de software, como NLB de Microsoft. En otros entornos podría ver algo parecido a HAProxy, nginx, Istio o Envoy en este rol. En estas arquitecturas, trabajo Hola de equilibrio de carga es tooensure cargas de trabajo sin estado (aproximadamente) recepción Hola misma cantidad de trabajo. Las estrategias de equilibro de carga variaban. Algunos equilibradores enviaría cada llamada diferente tooa otro servidor. Otros proporcionaban asignación o afinidad de la sesión. Equilibradores más avanzados usar estimación de la carga real o informes tooroute una llamada en función de sus costos previstos y la carga de la máquina actual.

Equilibradores de red o mensaje enrutadores intentó tooensure que Hola a nivel de web/trabajo permanecido como aproximadamente equilibrado. Estrategias para el equilibrio de capa de datos de hello eran dependiente en el mecanismo de almacenamiento de datos de Hola y diferente. Equilibrio de la capa de datos de hello dependiera de particionamiento de datos, almacenamiento en caché, administradas vistas, procedimientos almacenados y otros mecanismos de específicas del almacén.

Aunque algunas de estas estrategias son interesantes, Hola, Administrador de recursos de clúster de tejido de servicio no es nada como un equilibrador de carga de red o una memoria caché. Un equilibrador de carga de red equilibra front-ends mediante la distribución del tráfico a través de front-ends. Hola, Administrador de recursos de clúster de tejido de servicio tiene una estrategia diferente. Básicamente, Service Fabric mueve *servicios* toowhere hacen Hola más conveniente, se espera un tráfico o cargar toofollow. Por ejemplo, se podría mover toonodes de servicios que están actualmente inactivos porque servicios de Hola que existen no hacen mucho trabajo. nodos de Hello pueden ser frío porque servicios de Hola que estaban presentes eliminados o movidos en otro lugar. Otro ejemplo: Hola, Administrador de recursos del clúster también podría mover un servicio fuera de una máquina. Quizás máquina hello es sobre toobe actualizado o está sobrecargado debido tooa un incremento en el consumo de servicios de hello en ejecución. Alernatively, requisitos de recursos del servicio de hello podrán haya aumentado. Como resultado no hay suficientes recursos en este toocontinue máquina ejecutarlo. 

Dado que es responsable de transferir servicios alrededor de Hola, Administrador de recursos del clúster, contiene un toowhat de espacio en comparación con distintas características que se encuentra en un equilibrador de carga de red. Esto es porque los equilibradores de carga de red entregar toowhere de tráfico de red ya son servicios, incluso si no es lo ideal para ejecutar el propio servicio Hola esa ubicación. Hola, Administrador de recursos de clúster de Service Fabric emplea fundamentalmente distintas estrategias para garantizar el uso eficaz de los recursos de hello en clúster de Hola.

## <a name="next-steps"></a>Pasos siguientes
- Para obtener información sobre el flujo de información y arquitectura de hello en hello Administrador de recursos del clúster, visite [este artículo](service-fabric-cluster-resource-manager-architecture.md)
- Hola, Administrador de recursos del clúster tiene muchas opciones para describir el clúster de Hola. toofind más información acerca de las métricas, vea este artículo en [que describe un clúster de Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
- Para más información acerca de cómo configurar servicios, [lea sobre la configuración de servicios](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Las métricas son cómo Hola, Administrador de recursos de clúster de tejido de servicio administra capacidad en clúster de Hola y consumo. más información acerca de las métricas y cómo tooconfigure ellos desproteger toolearn [este artículo](service-fabric-cluster-resource-manager-metrics.md)
- Hola, Administrador de recursos del clúster funciona con capacidades de administración de Service Fabric. toofind más información acerca de que la integración, leer [este artículo](service-fabric-cluster-resource-manager-management-integration.md)
- toofind out acerca de cómo Hola, Administrador de recursos del clúster administra y equilibra la carga en el clúster de hello, desproteger artículo hello en [equilibrio de carga](service-fabric-cluster-resource-manager-balancing.md)
