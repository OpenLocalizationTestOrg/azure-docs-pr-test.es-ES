---
title: "Capacidad de prueba: comunicación del servicio | Microsoft Docs"
description: "La comunicación entre servicios es un punto crítico de integración de una aplicación de Service Fabric. En este artículo se describen las consideraciones de diseño y las técnicas de prueba."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a>Escenarios de capacidad de prueba de Service Fabric: comunicación del servicio
Los microservicios y los estilos de arquitectura orientados a servicios emergen naturalmente en Service Fabric de Azure. En estos tipos de arquitecturas distribuidas, dividida en componentes microservicio aplicaciones suelen constar de varios servicios que necesitan tootalk tooeach otros. En los casos de hello incluso más sencillos, generalmente tiene al menos un servicio web sin estado y un servicio de almacenamiento de datos con estado que necesita toocommunicate.

Comunicación del servicio a servicio es un punto de integración críticos de una aplicación, porque cada servicio expone un servicios tooother de API remoto. El trabajo con un conjunto de límites de API que implican E/S requiere generalmente tomar algunas precauciones y realizar una buena cantidad de pruebas y validaciones.

Hay numerosas toomake consideraciones cuando estos límites de servicio se conectan entre sí en un sistema distribuido:

* *Protocolo de transporte*. ¿Se utilizará HTTP para una mayor interoperabilidad, o bien un protocolo binario personalizado para el máximo rendimiento?
* *Control de errores*. ¿Cómo se controlarán los errores transitorios y permanentes? ¿Qué ocurrirá cuando mueve de un servicio tooa otro nodo?
* *Tiempos de espera y latencia*. ¿En las aplicaciones de varios niveles, cómo cada nivel de servicio controlará latencia a través de usuario de pila y toohello Hola?

Si usa uno de los componentes de comunicación del servicio integrado Hola proporcionados por Service Fabric o crear la suya propia, probar las interacciones de hello entre los servicios es la resistencia de tooensuring crítico en la aplicación.

## <a name="prepare-for-services-toomove"></a>Preparar para toomove de servicios
Las instancias de los servicios pueden desplazarse con el tiempo. Esto ocurre especialmente cuando se configuran con métricas de carga para el equilibrio óptimo personalizado de los recursos. Service Fabric se mueve el toomaximize de instancias de servicio su disponibilidad incluso durante las actualizaciones, las conmutaciones por error, escalado horizontal y otras situaciones que ocurren durante la duración de Hola de un sistema distribuido.

Como servicios moverse en clúster de hello, los clientes y otros servicios deben ser toohandle preparada dos escenarios cuando hablan tooa servicio:

* réplica de partición o instancia de servicio de Hola se ha movido desde Hola había hablado tooit de última hora. Se trata de una parte normal de un ciclo de vida de servicio y debe ser toohappen esperado durante la vigencia de saludo de la aplicación.
* réplica de partición o instancia de servicio de Hello está en proceso de Hola de mover. Aunque conmutación por error de un servicio desde una tooanother de nodo se produce muy rápidamente en el tejido de servicio, puede haber un retraso en la disponibilidad si Hola comunicación del componente del servicio es toostart lenta.

El control correcto de estas situaciones es importante para lograr que un sistema funcione sin problemas. toodo por lo tanto, tenga en cuenta que:

* Todos los servicios que pueden estar conectados toohas una *dirección* que realiza escuchas en (por ejemplo, HTTP o WebSockets). Cuando una instancia del servicio o una partición se desplaza, cambia el punto de conexión de su dirección. (Mueve tooa otro nodo con una dirección IP diferente). Si usa componentes de comunicación integradas de hello, controlará volver a resolver direcciones de servicio para usted.
* Puede haber un aumento de latencia de servicio como Hola servicio instancia comienza su agente de escucha temporal nuevo. Esto depende en rapidez servicio Hola abre el agente de escucha de hello después de mover la instancia de servicio de Hola.
* Las conexiones existentes necesitan toobe cierra y vuelve a abrir después de abre el servicio de hello en un nuevo nodo. Reinicio o apagado de nodo estable da tiempo para toobe de las conexiones existentes cerrar correctamente.

### <a name="test-it-move-service-instances"></a>Pruébelo: mover instancias de servicio
Mediante el uso de herramientas de capacidad de prueba del tejido de servicio, puede crear un tootest del escenario de prueba estas situaciones de maneras diferentes:

1. Mover la réplica principal de un servicio con estado.
   
    Hello réplica principal de una partición de servicio con estado puede aplicarse para una serie de motivos. Use este tootarget Hola una réplica principal de un toosee de partición específica cómo mover la toohello de reaccionar de servicios de una manera muy controlada.
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. Detener un nodo.
   
    Cuando se detiene un nodo, se desplaza de Service Fabric todas las de hello service instancias o particiones que había en ese tooone de nodo de Hola otros nodos disponibles en el clúster de Hola. Utilice este tootest una situación donde un nodo se pierde desde el clúster y todas las instancias de servicio hello y réplicas en ese nodo tienen toomove.
   
    Puede detener un nodo mediante Hola PowerShell **ServiceFabricNode Stop** cmdlet:
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a>Mantener la disponibilidad del servicio
Como una plataforma Service Fabric es tooprovide diseñada alta disponibilidad de los servicios. Sin embargo, los problemas de infraestructura subyacentes pueden provocar que no exista disponibilidad en casos extremos. Es importante tootest para estos escenarios, demasiado.

Los servicios con estado utilizan un estado de tooreplicate sistema basado en quórum para lograr alta disponibilidad. Esto significa que un quórum de réplicas debe toobe tooperform disponibles las operaciones de escritura. En casos excepcionales, como en un error generalizado de hardware, puede que no esté disponible el cuórum de réplicas. En estos casos, no será capaz de tooperform las operaciones de escritura, pero se seguirá tooperform capaz de las operaciones de lectura.

### <a name="test-it-write-operation-unavailability"></a>Pruébelo: falta de disponibilidad de la operación de escritura
Mediante herramientas de la capacidad de prueba de hello en Service Fabric, también puede insertar un error que provoca la pérdida del quórum como una prueba. Aunque este escenario es poco frecuente, es importante que los clientes y servicios que dependen de un servicio con estado están preparados situaciones toohandle donde no pueden tomar tooit las solicitudes de escritura. También es importante que el propio servicio con estado de hello es consciente de esta posibilidad y correctamente puede comunicarla toocallers.

Puede inducir la pérdida del quórum Hola PowerShell **ServiceFabricPartitionQuorumLoss Invoke** cmdlet:

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

En este ejemplo, establecemos `QuorumLossMode` demasiado`QuorumReplicas` tooindicate que queremos pérdida del quórum tooinduce sin apagar todas las réplicas. De este modo, las operaciones de lectura sigan siendo posibles. tootest un escenario donde una partición completa no está disponible, puede establecer este modificador demasiado`AllReplicas`.

## <a name="next-steps"></a>Pasos siguientes
[Más información sobre las acciones de capacidad de prueba](service-fabric-testability-actions.md)

[Más información sobre los escenarios de capacidad de prueba](service-fabric-testability-scenarios.md)

