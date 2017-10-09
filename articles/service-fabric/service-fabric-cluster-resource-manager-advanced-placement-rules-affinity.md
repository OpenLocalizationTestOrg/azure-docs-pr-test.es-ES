---
title: "aaaService Administrador de recursos de clúster de tejido - afinidad | Documentos de Microsoft"
description: "Información general sobre la configuración de afinidad para servicios de Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7dc9b6d9c18d9d615d39cff7de9d7cba1c040474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>Configuración y uso de la afinidad de servicio en Service Fabric
Afinidad es un control que se proporciona principalmente toohelp facilidad Hola transición de aplicaciones monolíticas grandes en Hola a todos en la nube y microservicios. También se utiliza como una optimización para mejorar el rendimiento de hello de servicios, aunque esto puede tener efectos secundarios.

Supongamos que utiliza una aplicación de mayor tamaño, o que simplemente no se diseñó con microservicios en mente, tooService tejido (o cualquier entorno distribuido). Este tipo de transición es habitual. Empiece por elevación Hola toda aplicación en el entorno de hello, empaquetado y asegurándose de que se está ejecutando sin problemas. Iniciar, a continuación, divídala en diferentes servicios más pequeños que todos hablar tooeach otros.

Finalmente es posible que la aplicación hello tiene algunos problemas. problemas de Hello normalmente pertenecen a una de estas categorías:

1. Algún componente X en hello monolítico aplicación tenía una dependencia no documentada en el componente Y y solo se activan esos componentes en distintos servicios. Puesto que estos servicios se ejecutan ahora en diferentes nodos de clúster de hello, son rotas.
2. Estos componentes se comunican a través de (canalizaciones con nombre locales | memoria compartida | archivos en disco) y realmente necesita recursos locales de toobe toowrite pueda tooa compartido por motivos de rendimiento ahora mismo. Quizás, esa dependencia física se quite más adelante.
3. Todo es correcto, pero resulta que estos dos componentes están realmente fragmentados o son sensibles al rendimiento. Cuando se mueven a servicios independientes, el rendimiento general de la aplicación se reduce y aumenta la latencia. Como resultado, hello general de la aplicación no cumple las expectativas.

En estos casos, no desea toolose nuestro trabajo refactorización y no desea toogo toohello atrás monolito. última condición de Hello incluso puede ser deseable como un método de optimización sin formato. Sin embargo, hasta que se podemos rediseñar Hola componentes toowork de forma natural como servicios (o hasta que podemos resolver las expectativas de rendimiento de hello alguna otra manera) vamos tooneed cierto sentido de localidad.

¿Qué toodo? Podemos intentar activar la afinidad.

## <a name="how-tooconfigure-affinity"></a>La afinidad de tooconfigure
tooset la afinidad, se define una relación de afinidad entre dos servicios diferentes. Es como si hiciera que un servicio "apuntara" a otro y dijera "Este servicio solo se puede ejecutar donde se esté ejecutando ese otro". En ocasiones nos referimos tooaffinity como una relación de elementos primarios/secundarios (donde eliges secundarios hello en el elemento primario de hello). Afinidad garantiza que las réplicas de Hola o instancias de un servicio están ubicadas en hello mismo nodos como los de otro servicio.

```csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

> [!NOTE]
> Un servicio secundario solo puede participar en una relación de afinidad sencilla. Si deseara Hola secundarios toobe afinidad tootwo primario servicios al mismo tiempo tendrá un par de opciones:
> - Invertir las relaciones de hello (tiene parentService1 y parentService2 apuntar al servicio secundario actual de hello), o
> - Designar uno de los padres Hola como un concentrador, convención y tienen todos los servicios apuntan a ese servicio. 
>
> Hola resultante el comportamiento de selección de ubicación en el clúster de hello debe ser Hola mismo.
>

## <a name="different-affinity-options"></a>Diferentes opciones de afinidad
La afinidad se representa mediante uno de varios esquemas de correlación y tiene dos modos diferentes. Hola el modo más común de afinidad es lo que llamamos NonAlignedAffinity. En NonAlignedAffinity, Hola réplicas o instancias de servicios diferentes de Hola se colocan en hello mismos nodos. Hola otro modo es AlignedAffinity. AlignedAffinity resulta de utilidad con servicios con estado. Configuración con estado dos servicios toohave alineado afinidad garantiza que primarios Hola de dichos servicios están ubicados en Hola mismos nodos como unos de otros. También hace que cada par de elementos secundarios para esos servicios toobe coloca en hello mismo nodos. También es posible (aunque menos común) tooconfigure NonAlignedAffinity para los servicios con estado. Para NonAlignedAffinity, distintas réplicas de Hola de hello llevarían a cabo en dos servicios con estado Hola mismos nodos, pero sus primarios podrían acabar en nodos diferentes.

<center>
![Modos de afinidad y consecuencias][Image1]
</center>

### <a name="best-effort-desired-state"></a>Estado de mejor esfuerzo deseado
Una relación de afinidad es la mejor opción. No proporciona Hola mismas garantías de confiabilidad encargada de ejecutar Hola mismo proceso ejecutable o de la colocación. Servicios de Hello en una relación de afinidad son fundamentalmente distintas entidades que pueden producir un error y mover de forma independiente. También se puede interrumpir una relación de afinidad, aunque estas interrupciones son temporales. Por ejemplo, las limitaciones de capacidad pueden significar que sólo algunos Hola objetos de servicio en la relación de afinidad de hello caben en un nodo determinado. En estos casos, aunque hay una relación de afinidad en su lugar, no se puede aplicar a pagar toohello otras restricciones. Si es posible toodo por lo tanto, infracción de Hola se corrige automáticamente más tarde.

### <a name="chains-vs-stars"></a>Cadenas frente a estrellas
Hoy en día Hola, Administrador de recursos del clúster no es capaz de toomodel cadenas de relaciones de afinidad. Esto significa que un servicio que es un elemento secundario de una relación de afinidad no puede ser un elemento primario de otra relación de afinidad. Si desea toomodel este tipo de relación, tienen efectivamente toomodel como una estrella, en lugar de una cadena. toomove desde una estrella de tooa de cadena, secundario más bajo de hello sería toohello primario primera primario del elemento secundario en su lugar. Dependiendo de la organización de Hola de sus servicios, puede que tenga toodo varias veces. Si no hay ningún servicio de elemento primario natural, puede tener toocreate uno que actúa como un marcador de posición. Dependiendo de los requisitos, puede que también desee toolook en [grupos de aplicaciones](service-fabric-cluster-resource-manager-application-groups.md).

<center>
![Cadenas frente a Estrellas de hello contexto de las relaciones de afinidad][Image2]
</center>

Otro toonote algo acerca de las relaciones de afinidad hoy en día es que son direccionales. Esto significa que esa regla de afinidad de hello solo exige que secundarios Hola colocado con primario Hola. No garantiza que ese elemento primario Hola se encuentra con secundarios Hola. También es importante toonote que Hola relación de afinidad no se puede perfecta o al instante aplicar desde diferentes servicios tiene los ciclos de vida diferente y pueden producirá un error y mover de forma independiente. Por ejemplo, supongamos que primario Hola repentinamente conmuta por error nodo tooanother porque bloqueó. Hola, Administrador de recursos del clúster y el controlador del Administrador de conmutación por error de Hola conmutación por error en primer lugar, ya que mantener los servicios de hello, coherente y de disponibilidad es la prioridad de Hola. Una vez completada la conmutación por error de hello, se interrumpe la relación de afinidad de hello, pero no se encuentra con primario Hola Hola, Administrador de recursos del clúster se considera que todo va bien hasta que observa a que los secundarios de Hola. Estos tipos de comprobaciones se realizan periódicamente. Obtener más información sobre cómo Hola, Administrador de recursos del clúster se evalúa como restricciones está disponible en [este artículo](service-fabric-cluster-resource-manager-management-integration.md#constraint-types), y [este](service-fabric-cluster-resource-manager-balancing.md) habla más información acerca de cómo tooconfigure Hola cadencia en que estas restricciones son evalúa.   


### <a name="partitioning-support"></a>Compatibilidad con particiones
Hola final lo toonotice acerca de la afinidad es que no se admiten relaciones de afinidad donde se crean las particiones primaria de Hola. A la larga los servicios principales particionados se admitirán, pero por ahora no se permiten.

## <a name="next-steps"></a>Pasos siguientes
- Para más información sobre la configuración de servicios, vaya a [este vínculo](service-fabric-cluster-resource-manager-configure-services.md).
- los servicios de toolimit tooa pequeño conjunto de máquinas o agregar carga de hello de servicios, use [grupos de aplicaciones](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png