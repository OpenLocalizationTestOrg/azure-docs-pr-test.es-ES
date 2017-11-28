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
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="a8f9d-103">Reentrada de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="a8f9d-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="a8f9d-104">tiempo de ejecución de Reliable Actors Hello, de forma predeterminada, permite reentrada basado en contexto de llamada lógico.</span><span class="sxs-lookup"><span data-stu-id="a8f9d-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="a8f9d-105">Esto permite reentrante de actores toobe si están en hello misma cadena de contexto de llamada.</span><span class="sxs-lookup"><span data-stu-id="a8f9d-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="a8f9d-106">Por ejemplo, un Actor envía un tooActor mensaje B, que envía un tooActor mensaje C. Como parte del procesamiento de mensajes de Hola, si llama a C Actor Actor A, mensajes de bienvenida es reentrante, por lo que se le permitirá.</span><span class="sxs-lookup"><span data-stu-id="a8f9d-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="a8f9d-107">Los demás mensajes que formen parte de un contexto de llamada distinto se bloquearán en el actor A hasta que complete el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="a8f9d-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="a8f9d-108">Hay dos opciones disponibles para la reentrada actor definida en hello `ActorReentrancyMode` enum:</span><span class="sxs-lookup"><span data-stu-id="a8f9d-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="a8f9d-109">`LogicalCallContext` (comportamiento predeterminado)</span><span class="sxs-lookup"><span data-stu-id="a8f9d-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="a8f9d-110">`Disallowed` : deshabilita la reentrada.</span><span class="sxs-lookup"><span data-stu-id="a8f9d-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="a8f9d-111">Se puede establecer la reentrada en la configuración de una clase `ActorService`durante el registro.</span><span class="sxs-lookup"><span data-stu-id="a8f9d-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="a8f9d-112">saludo aplica a instancias de actor tooall creadas en el servicio de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="a8f9d-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="a8f9d-113">Hello en el ejemplo siguiente se muestra un servicio de actor que establece el modo de reentrada Hola demasiado`ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="a8f9d-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="a8f9d-114">En este caso, si un actor envía un actor de tooanother mensaje reentrante, una excepción de tipo `FabricException` se iniciará.</span><span class="sxs-lookup"><span data-stu-id="a8f9d-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="a8f9d-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8f9d-115">Next steps</span></span>
* <span data-ttu-id="a8f9d-116">Obtener más información acerca de reentrada en hello [documentación de referencia de API de Actor](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8f9d-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
