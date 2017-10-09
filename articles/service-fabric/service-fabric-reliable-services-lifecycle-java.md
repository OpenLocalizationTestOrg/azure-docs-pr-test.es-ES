---
title: aaaOverview del ciclo de vida de hello Service Fabric confiable de servicios de Azure | Documentos de Microsoft
description: "Obtenga información acerca de los eventos de ciclo de vida distinto de hello en servicios de Service Fabric confiables"
services: Service-Fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: pakunapa;
ms.openlocfilehash: 6d48c217d12bc5248c2da57b544aac747cecd872
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

* Durante el inicio:
  * se construyen los servicios,
  * Tienen un tooconstruct oportunidad y devolver cero o más agentes de escucha
  * Se abre cualquier agente de escucha devuelta, que permita la comunicación con el servicio de Hola
  * se denomina método de Coredispatcher del servicio de Hello, permitiendo Hola toodo de servicio de larga ejecución o trabajo en segundo plano
* Durante el cierre:
  * toorunAsync pasado token Hola de cancelación se cancela y se cierran los agentes de escucha de Hola
  * Una vez completado, se destruye propio objeto de servicio Hola

No hay información alrededor de hello exacto de orden de estos eventos. En concreto, orden de Hola de eventos puede cambiar ligeramente dependiendo de si Hola servicio confiable es Stateless o con estado. Además, los servicios con estado, tenemos toodeal con el escenario de intercambio principal Hola. Durante esta secuencia, rol de Hola de principal es tooanother transfieren réplica (o vuelve a estar) sin el servicio de Hola que se va a cerrar. Por último, tenemos toothink acerca de las condiciones de error o un error.

## <a name="stateless-service-startup"></a>Inicio de un servicio sin estado
ciclo de vida de Hola de un servicio sin estado es bastante sencilla. Este es el orden Hola de eventos:

1. Hola se construye servicio
2. A continuación, suceden dos cosas simultáneamente:
    - Se invoca `StatelessService.createServiceInstanceListeners()` y se abren los agentes de escucha devueltos (se llama a `CommunicationListener.openAsync()` en cada agente de escucha).
    - Hola Coredispatcher método servicio (`StatelessService.runAsync()`) se llama
3. Si está presente, se llama el método onOpenAsync de hello del servicio (en concreto, `StatelessService.onOpenAsync()` se llama. Se trata de una invalidación poco habitual, pero está disponible).

Es importante toonote que no hay ningún orden entre Hola llamadas toocreate y agentes de escucha de hello abierto y Coredispatcher. pueden abrir los agentes de escucha de Hola antes de inicia la Coredispatcher. De forma similar, Coredispatcher terminen invoca antes de que los agentes de escucha de comunicación de hello están abiertos o incluso construidos. Si no se necesita ninguna sincronización, se deja como ejercicio toohello implementador. Soluciones comunes:

* En ocasiones, los agentes de escucha no pueden funcionar hasta que se crea otra información o se realiza un trabajo. Para los servicios sin estado que trabajo normalmente se puede realizar en el constructor del servicio de hello, durante hello `createServiceInstanceListeners()` llamar a, o como parte de la construcción de Hola de hello propio agente de escucha.
* A veces hello código en Coredispatcher no quiere toostart hasta que los agentes de escucha de hello están abiertos. En este caso, hace falta coordinación adicional. Una solución habitual es algunos marca dentro de los agentes de escucha hello, que indica cuándo ha completado, que se comprueba en Coredispatcher antes de continuar el trabajo de tooactual.

## <a name="stateless-service-shutdown"></a>Cierre de un servicio sin estado
Cuando se va a cerrar un servicio sin estado, Hola se sigue el mismo patrón, solo en orden inverso:

1. En paralelo
    - Se cierran todos los agentes de escucha abiertos (se llama a `CommunicationListener.closeAsync()` en cada agente de escucha)
    - token de cancelación de Hello pasa demasiado`runAsync()` se cancela (comprobación del token de cancelación de hello `isCancelled` propiedad devuelve true y si se llama del token de hello `throwIfCancellationRequested` método inicie una excepción un `CancellationException`)
2. Una vez `closeAsync()` completa en cada agente de escucha y `runAsync()` también completa, del servicio de hello `StatelessService.onCloseAsync()` se llama el método, si está presente (nuevo es una invalidación raro).
3. Después de `StatelessService.onCloseAsync()` completa, se destruye el objeto de servicio de Hola

## <a name="notes-on-service-lifecycle"></a>Notas sobre el ciclo de vida del servicio
* Ambos hello `runAsync()` hello y método `createServiceInstanceListeners` llamadas son opcionales. Un servicio puede tener uno, ambos o ninguno. Por ejemplo, si servicio Hola hace todo el trabajo en las llamadas de toouser de respuesta, no es necesario para el mismo tooimplement `runAsync()`. Es necesario solo escuchas de comunicación de Hola y su código asociado. Del mismo modo, crear y devolver los agentes de escucha de comunicación es opcional, como servicio de hello puede tener solo fondo toodo de trabajo y por lo que solo necesita tooimplement`runAsync()`
* Es válido para un servicio toocomplete `runAsync()` correctamente y vuelva a partir de él. Esto no se considera una condición de error y representaría el trabajo en segundo plano de la realización de servicio de Hola Hola. Para los servicios de confianza con estado `runAsync()` se denominaría nuevo si servicio de Hola se degrada de principal y, a continuación, promocionar tooprimary atrás.
* Si sale de un servicio de `runAsync()` iniciando una excepción inesperada, se trata de un error y se cierra el objeto de servicio de Hola y notifica un error de estado.
* Aunque no hay ningún límite de tiempo en la devolución de estos métodos, se pierde inmediatamente toowrite de capacidad de hello y, por tanto, no se puede completar cualquier trabajo real. Se recomienda que vuelva tan pronto como sea posible tras la recepción de solicitud de cancelación de Hola. Si el servicio no responde toothese API llamadas en un período razonable de tiempo que Service Fabric forzosamente puede finalizar su servicio. Esto solo suele pasar durante las actualizaciones de aplicación o cuando se elimina un servicio. Este tiempo de espera es de 15 minutos de manera predeterminada.
* Errores en hello `onCloseAsync()` resultado de la ruta de acceso en `onAbort()` que se la llame que es una oportunidad de mejor esfuerzo de última oportunidad para hello servicio tooclean seguridad y liberar cualquier recurso que ha solicitado.

> [!NOTE]
> Las instancias con estado de Reliable Services aún no se admiten en Java.
>
>

## <a name="next-steps"></a>Pasos siguientes
* [Servicios de tooReliable de introducción](service-fabric-reliable-services-introduction.md)
* [Introducción a Reliable Services de Service Fabric de Microsoft Azure](service-fabric-reliable-services-quick-start.md)
* [Uso avanzado de Reliable Services](service-fabric-reliable-services-advanced-usage.md)
