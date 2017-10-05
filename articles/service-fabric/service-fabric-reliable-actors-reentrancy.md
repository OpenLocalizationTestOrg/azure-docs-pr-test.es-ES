---
title: Reentrada en microservicios de Azure basados en actores | Microsoft Docs
description: "Introducción a la reentrada de Service Fabric Reliable Actors"
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
ms.openlocfilehash: 00fcccb379bf1ba3875fbaba57a05b00fa228622
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="52e4c-103">Reentrada de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="52e4c-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="52e4c-104">El runtime de Reliable Actors permite, de manera predeterminada, la reentrada basada en el contexto de llamadas lógicas.</span><span class="sxs-lookup"><span data-stu-id="52e4c-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="52e4c-105">Esto permite que los actores sean reentrantes si están en la misma cadena de contexto de llamada.</span><span class="sxs-lookup"><span data-stu-id="52e4c-105">This allows for actors to be reentrant if they are in the same call context chain.</span></span> <span data-ttu-id="52e4c-106">Por ejemplo, si el actor A envía un mensaje al actor B, quien envía el mensaje al actor C; como parte del procesamiento del mensaje, si el actor C llama al actor A, el mensaje es reentrante y, por los tanto, se permitirá.</span><span class="sxs-lookup"><span data-stu-id="52e4c-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="52e4c-107">Los demás mensajes que formen parte de un contexto de llamada distinto se bloquearán en el actor A hasta que complete el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="52e4c-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="52e4c-108">Existen dos opciones disponibles para la reentrada de actores definidas en la enumeración `ActorReentrancyMode` :</span><span class="sxs-lookup"><span data-stu-id="52e4c-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="52e4c-109">`LogicalCallContext` (comportamiento predeterminado)</span><span class="sxs-lookup"><span data-stu-id="52e4c-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="52e4c-110">`Disallowed` : deshabilita la reentrada.</span><span class="sxs-lookup"><span data-stu-id="52e4c-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="52e4c-111">Se puede establecer la reentrada en la configuración de una clase `ActorService`durante el registro.</span><span class="sxs-lookup"><span data-stu-id="52e4c-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="52e4c-112">La configuración se aplica a todas las instancias de actor que creó en el servicio de actor.</span><span class="sxs-lookup"><span data-stu-id="52e4c-112">The setting applies to all actor instances created in the actor service.</span></span>

<span data-ttu-id="52e4c-113">En el ejemplo siguiente se muestra un servicio de actor que establece el modo de reentrada en `ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="52e4c-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="52e4c-114">En este caso, si un actor envía un mensaje reentrante a otro actor, se generará una excepción de tipo `FabricException` .</span><span class="sxs-lookup"><span data-stu-id="52e4c-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="52e4c-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52e4c-115">Next steps</span></span>
* <span data-ttu-id="52e4c-116">Aprenda más sobre la reentrada en la [documentación de referencia de Actor API](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="52e4c-116">Learn more about reentrancy in the [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
