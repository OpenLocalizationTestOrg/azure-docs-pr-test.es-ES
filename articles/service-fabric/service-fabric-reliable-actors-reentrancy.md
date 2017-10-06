---
title: aaaReentrancy en microservicios Azure basado en actores | Documentos de Microsoft
description: "Introducción tooreentrancy de servicio de Fabric Reliable Actors"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a>Reentrada de Reliable Actors
tiempo de ejecución de Reliable Actors Hello, de forma predeterminada, permite reentrada basado en contexto de llamada lógico. Esto permite reentrante de actores toobe si están en hello misma cadena de contexto de llamada. Por ejemplo, un Actor envía un tooActor mensaje B, que envía un tooActor mensaje C. Como parte del procesamiento de mensajes de Hola, si llama a C Actor Actor A, mensajes de bienvenida es reentrante, por lo que se le permitirá. Los demás mensajes que formen parte de un contexto de llamada distinto se bloquearán en el actor A hasta que complete el procesamiento.

Hay dos opciones disponibles para la reentrada actor definida en hello `ActorReentrancyMode` enum:

* `LogicalCallContext` (comportamiento predeterminado)
* `Disallowed` : deshabilita la reentrada.

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
Se puede establecer la reentrada en la configuración de una clase `ActorService`durante el registro. saludo aplica a instancias de actor tooall creadas en el servicio de actor Hola.

Hello en el ejemplo siguiente se muestra un servicio de actor que establece el modo de reentrada Hola demasiado`ActorReentrancyMode.Disallowed`. En este caso, si un actor envía un actor de tooanother mensaje reentrante, una excepción de tipo `FabricException` se iniciará.

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a>Pasos siguientes
* Obtener más información acerca de reentrada en hello [documentación de referencia de API de Actor](https://msdn.microsoft.com/library/azure/dn971626.aspx)
