---
title: aaaOverview del ciclo de vida de hello Service Fabric confiable de servicios de Azure | Documentos de Microsoft
description: "Obtenga información acerca de los eventos de ciclo de vida distinto de hello en servicios de Service Fabric confiables"
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Información general del ciclo de vida de Reliable Services
> [!div class="op_single_selector"]
> * [C# en Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java en Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Al pensar en los ciclos de vida de hello de servicios de confianza, conceptos básicos de hello del ciclo de vida de hello son hello más importante. En general:

- Durante el inicio:
  - se construyen los servicios,
  - Tienen un tooconstruct oportunidad y devolver cero o más agentes de escucha
  - Se abre cualquier agente de escucha devuelta, que permita la comunicación con el servicio de Hola
  - Coredispatcher del servicio de Hello método se llama, permitiendo hello toodo larga ejecución del servicio o trabajo en segundo plano
- Durante el cierre:
  - tooRunAsync pasado token Hola de cancelación se cancela y se cierran los agentes de escucha de Hola
  - Una vez completado, se destruye propio objeto de servicio Hola

No hay información alrededor de hello exacto de orden de estos eventos. En concreto, orden de Hola de eventos puede cambiar ligeramente dependiendo de si Hola servicio confiable es Stateless o con estado. Además, los servicios con estado, tenemos toodeal con el escenario de intercambio principal Hola. Durante esta secuencia, rol de Hola de principal es tooanother transfieren réplica (o vuelve a estar) sin el servicio de Hola que se va a cerrar. Por último, tenemos toothink acerca de las condiciones de error o un error.

## <a name="stateless-service-startup"></a>Inicio de un servicio sin estado
ciclo de vida de Hola de un servicio sin estado es bastante sencilla. Este es el orden Hola de eventos:

1. Hola se construye servicio
2. A continuación, suceden dos cosas simultáneamente:
    - Se invoca `StatelessService.CreateServiceInstanceListeners()` y se abren los agentes de escucha devueltos. Se llama a `ICommunicationListener.OpenAsync()` en cada uno de los agentes de escucha.
    - Hola del servicio `StatelessService.RunAsync()` se llama al método
3. Si está presente, Hola del servicio `StatelessService.OnOpenAsync()` se llama al método. Esta invalidación es poco habitual, pero está disponible.

Es importante toonote que no hay ningún orden entre Hola llamadas toocreate y agentes de escucha de hello abierto y Coredispatcher. pueden abrir los agentes de escucha de Hola antes de inicia la Coredispatcher. De forma similar, Coredispatcher terminen invoca antes de que los agentes de escucha de comunicación de hello están abiertos o incluso construidos. Si no se necesita ninguna sincronización, se deja como ejercicio toohello implementador. Soluciones comunes:

  - En ocasiones, los agentes de escucha no pueden funcionar hasta que se crea otra información o se realiza un trabajo. En el caso de los servicios sin estado, normalmente, esto puede hacerse en otras ubicaciones, como: 
    - en el constructor del servicio de Hola
    - durante el saludo `CreateServiceInstanceListeners()` llamar a
    - como parte de la construcción de Hola de hello propio agente de escucha
  - A veces hello código en Coredispatcher no quiere toostart hasta que los agentes de escucha de hello están abiertos. En este caso, hace falta coordinación adicional. Una solución habitual es algún indicador dentro de los agentes de escucha hello, que indica cuándo ha completado. Esta marca, a continuación, se comprueba en Coredispatcher antes de continuar el trabajo de tooactual.

## <a name="stateless-service-shutdown"></a>Cierre de un servicio sin estado
Cuando se va a cerrar un servicio sin estado, Hola se sigue el mismo patrón, solo en orden inverso:

1. En paralelo
    - Todos los agentes de escucha abiertos se cierran. Se llama a `ICommunicationListener.CloseAsync()` en cada uno de los agentes de escucha.
    - token de cancelación de Hello pasa demasiado`RunAsync()` se cancela. Comprobando token de cancelación de hello `IsCancellationRequested` propiedad devuelve true y si se llama del token de hello `ThrowIfCancellationRequested` método inicie una excepción un `OperationCanceledException`.
2. Una vez `CloseAsync()` completa en cada agente de escucha y `RunAsync()` también completa, del servicio de hello `StatelessService.OnCloseAsync()` se llama el método, si está presente. Es raro que toooverride `StatelessService.OnCloseAsync()`.
3. Después de `StatelessService.OnCloseAsync()` completa, se destruye el objeto de servicio de Hola

## <a name="stateful-service-startup"></a>Inicio de un servicio con estado
Servicios con estado tienen un servicios de toostateless de patrón similar, con unos pocos cambios. Al iniciarse un servicio con estado, orden de Hola de eventos es el siguiente:

1. Hola se construye servicio
2. Se llama a `StatefulServiceBase.OnOpenAsync()`. Esto se reemplaza uncommonly en servicio Hola.
3. Hello ocurrirá lo siguiente en paralelo
    - Se invoca a `StatefulServiceBase.CreateServiceReplicaListeners()`. 
      - Si el servicio de hello es un elemento principal se abren todos los agentes de escucha devueltas. Se llama a `ICommunicationListener.OpenAsync()` en cada uno de los agentes de escucha.
      - Si el servicio de hello es un elemento secundario, sólo los agentes de escucha marcan como `ListenOnSecondary = true` están abiertos. No es muy frecuente tener agentes de escucha abiertos en servicios secundarios.
    - Hola si Hola servicio actualmente es un servicio de hello principal, `StatefulServiceBase.RunAsync()` se llama al método
4. Una vez que todos Hola del agente de escucha de réplica `OpenAsync()` una llamada de finalización y `RunAsync()` se llama, `StatefulServiceBase.OnChangeRoleAsync()` se llama. Esto se reemplaza uncommonly en servicio Hola.

Servicios de toostateless del mismo modo, no hay ningún coordinación entre el orden de hello en qué Hola agentes de escucha se crea y se abre y cuando se llama a Coredispatcher. Si necesita coordinación, soluciones de hello son mucho Hola mismo. Hay un caso adicional: decir que las llamadas de Hola que llegan a los agentes de escucha de comunicación de hello requieren información que se mantiene dentro de algunas [colecciones confiable](service-fabric-reliable-services-reliable-collections.md). Dado escuchas de comunicación de hello podrían abrir antes de colecciones confiable de hello son legibles o de escritura, y antes de que se puede iniciar Coredispatcher, algunos coordinación adicional es necesario. solución más sencilla y más común de Hello es para tooreturn de agentes de escucha de comunicación de hello algún código de error que Hola Hola solicitud de cliente utiliza tooknow tooretry.

## <a name="stateful-service-shutdown"></a>Cierre de un servicio con estado
De igual forma tooStateless services, eventos de ciclo de vida de Hola durante el cierre son Hola igual durante el inicio, pero invierten. Cuando un servicio con estado se está cerrando, hello ocurrirá lo siguiente:

1. En paralelo
    - Todos los agentes de escucha abiertos se cierran. Se llama a `ICommunicationListener.CloseAsync()` en cada uno de los agentes de escucha.
    - token de cancelación de Hello pasa demasiado`RunAsync()` se cancela. Comprobando token de cancelación de hello `IsCancellationRequested` propiedad devuelve true y si se llama del token de hello `ThrowIfCancellationRequested` método inicie una excepción un `OperationCanceledException`.
2. Una vez `CloseAsync()` completa en cada agente de escucha y `RunAsync()` también completa, del servicio de hello `StatefulServiceBase.OnChangeRoleAsync()` se llama. (Esto uncommonly se reemplaza en el servicio de hello).
    - Esperando Coredispatcher toocomplete solo es necesario si esta réplica de servicio es un elemento principal.
3. Una vez Hola `StatefulServiceBase.OnChangeRoleAsync()` método finaliza, hello `StatefulServiceBase.OnCloseAsync()` se llama al método. Esta invalidación es poco habitual, pero está disponible.
3. Después de `StatefulServiceBase.OnCloseAsync()` completa, se destruye el objeto de servicio de Hola.

## <a name="stateful-service-primary-swaps"></a>Intercambios de servicios con estado principales
Mientras se ejecuta un servicio con estado, sólo hello las réplicas principales de que los servicios con estado tienen sus agentes de escucha de comunicación abiertos y su método Coredispatcher llamado. Los secundarios se construyen, pero no reciben más llamadas. Mientras un servicio con estado se ejecuta sin embargo, pueden cambiar qué réplica actualmente es hello principal. ¿Qué significa esto en términos de los eventos de ciclo de vida de Hola que puede ver una réplica? Hola comportamiento Hola réplica con estado ve depende de si es réplica Hola se degradan o promueve durante el intercambio de Hola.

### <a name="for-hello-primary-being-demoted"></a>Que se degradan para hello principal
Tejido de servicio necesita esta toostop réplica procesar mensajes y salga de cualquier trabajo en segundo plano que esté realizando. Como resultado, este servicio paso parece similar toowhen Hola se está cerrando. Una diferencia es que hello servicio no destruye o se cierra puesto que permanece como un elemento secundario. se llama después de las API de Hola:

1. En paralelo
    - Todos los agentes de escucha abiertos se cierran. Se llama a `ICommunicationListener.CloseAsync()` en cada uno de los agentes de escucha.
    - token de cancelación de Hello pasa demasiado`RunAsync()` se cancela. Comprobando token de cancelación de hello `IsCancellationRequested` propiedad devuelve true y si se llama del token de hello `ThrowIfCancellationRequested` método inicie una excepción un `OperationCanceledException`.
2. Una vez `CloseAsync()` completa en cada agente de escucha y `RunAsync()` también completa, del servicio de hello `StatefulServiceBase.OnChangeRoleAsync()` se llama. Esto se reemplaza uncommonly en servicio Hola.

### <a name="for-hello-secondary-being-promoted"></a>Promocionado para hello secundaria
De forma similar, Service Fabric necesita este toostart réplica realiza escuchas de mensajes en el cable de Hola e iniciar las tareas en segundo plano se ocupa de sobre. Como resultado, este aspecto del proceso se crea el servicio de hello toowhen similar, salvo que la réplica Hola propio ya existe. se llama después de las API de Hola:

1. En paralelo
    - Se invoca `StatefulServiceBase.CreateServiceReplicaListeners()` y se abren los agentes de escucha devueltos. Se llama a `ICommunicationListener.OpenAsync()` en cada uno de los agentes de escucha.
    - Hola del servicio `StatefulServiceBase.RunAsync()` se llama al método
2. Una vez que todos Hola del agente de escucha de réplica `OpenAsync()` una llamada de finalización y `RunAsync()` se ha llamado `StatefulServiceBase.OnChangeRoleAsync()` se llama. Esto se reemplaza uncommonly en servicio Hola.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>Problemas habituales durante la degradación de la categoría principal y el cierre de un servicio con estado
Cambios de Service Fabric Hola principal de un servicio con estado para una variedad de motivos. Hello más comunes son [clúster reequilibrio](service-fabric-cluster-resource-manager-balancing.md) y [actualización de la aplicación](service-fabric-application-upgrade.md). Durante estas operaciones (así como durante el cierre del servicio normal, como vería si se eliminó el servicio de hello), es importante que Hola Hola de respeto de servicio `CancellationToken`. Los servicios que no administren correctamente la cancelación experimentarán errores. En concreto, estas operaciones será lentas desde Service Fabric espera Hola servicios toostop correctamente. En última instancia, esto puede provocar actualizaciones toofailed ese tiempo de espera y revertir. Token de cancelación de error toohonor Hola también puede producir desequilibrados clústeres porque nodos obtener acceso rápidos pero no se volverán a equilibrar servicios Hola puesto que tarda demasiado toomove ellos en otro lugar. 

Puesto que Servicios de hello están activo, también es probable que estén usando hello [colecciones confiable](service-fabric-reliable-services-reliable-collections.md). En Service Fabric, cuando se degrada principal, uno de hello lo que ocurre es que el estado de acceso de escritura toohello subyacente se ha revocado. Esto conduce tooa segundo conjunto de problemas que pueden afectar el ciclo de vida de servicio de Hola. colecciones de Hello devueltos excepciones basadas en tiempo de Hola y si se ha movido réplica Hola o apagado. Estas excepciones deberían administrarse correctamente. Las excepciones iniciadas por Service Fabric pueden corresponder a dos categorías: permanentes [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) y transitorias [(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet). Excepciones permanentes deben registrarse y produzca, mientras que las excepciones transitorias de Hola se pueden reintentar basado en alguna lógica de reintento.

Control de excepciones de Hola que proceden de uso de hello `ReliableCollections` junto con eventos de ciclo de vida de servicio es una parte importante de prueba y validación de un servicio confiable. Hola recomendación es el servicio bajo una carga de siempre toorun al realizar actualizaciones y [chaos pruebas](service-fabric-controlled-chaos.md) antes de implementar alguna vez tooproduction. Estos pasos básicos ayudan a garantizar que el servicio está implementado correctamente y puede administrar los eventos del ciclo de vida correctamente.


## <a name="notes-on-service-lifecycle"></a>Notas sobre el ciclo de vida del servicio
  - Ambos hello `RunAsync()` hello y método `CreateServiceReplicaListeners/CreateServiceInstanceListeners` llamadas son opcionales. Un servicio puede tener uno, ambos o ninguno. Por ejemplo, si servicio Hola hace todo el trabajo en las llamadas de toouser de respuesta, no es necesario para el mismo tooimplement `RunAsync()`. Es necesario solo escuchas de comunicación de Hola y su código asociado. Del mismo modo, crear y devolver los agentes de escucha de comunicación es opcional, como servicio de hello puede tener solo fondo toodo de trabajo y por lo que solo necesita tooimplement`RunAsync()`
  - Es válido para un servicio toocomplete `RunAsync()` correctamente y vuelva a partir de él. La finalización no es una condición de error. Completar `RunAsync()` indica que ha finalizado el trabajo en segundo plano del servicio de Hola Hola. Para los servicios de confianza con estado, `RunAsync()` se llama de nuevo si la réplica de Hola se degrada de tooSecondary principal y, a continuación, promocionar tooPrimary atrás.
  - Si un servicio sale de `RunAsync()` iniciando una excepción inesperada, se considera un error. se cierra el objeto de servicio de Hola y notifica un error de estado.
  - Aunque no hay ningún límite de tiempo en la devolución de estos métodos, que inmediatamente pierda Hola capacidad toowrite tooReliable colecciones y, por tanto, no puede completar cualquier trabajo real. Se recomienda que vuelva tan pronto como sea posible tras la recepción de solicitud de cancelación de Hola. Si el servicio no responde toothese API llamadas en un período razonable de tiempo que Service Fabric forzosamente puede finalizar su servicio. Esto solo suele pasar durante las actualizaciones de aplicación o cuando se elimina un servicio. Este tiempo de espera es de 15 minutos de manera predeterminada.
  - Errores en hello `OnCloseAsync()` resultado de la ruta de acceso en `OnAbort()` que se la llame que es una oportunidad de mejor esfuerzo de última oportunidad para hello servicio tooclean seguridad y liberar cualquier recurso que ha solicitado.

## <a name="next-steps"></a>Pasos siguientes
- [Servicios de tooReliable de introducción](service-fabric-reliable-services-introduction.md)
- [Introducción a Reliable Services de Service Fabric de Microsoft Azure](service-fabric-reliable-services-quick-start.md)
- [Uso avanzado de Reliable Services](service-fabric-reliable-services-advanced-usage.md)
