---
title: aaaEvents en microservicios Azure basado en actores | Documentos de Microsoft
description: "Introducción tooevents de Reliable Actors de tejido de servicio."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a><span data-ttu-id="310f3-103">Eventos de actor</span><span class="sxs-lookup"><span data-stu-id="310f3-103">Actor events</span></span>
<span data-ttu-id="310f3-104">Eventos de actor proporcionan un notificaciones de mejor esfuerzo de toosend de forma de los clientes de hello actor toohello.</span><span class="sxs-lookup"><span data-stu-id="310f3-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="310f3-105">Los eventos de actor están diseñados para la comunicación entre actor y cliente, y no deben usarse para una comunicación entre actores.</span><span class="sxs-lookup"><span data-stu-id="310f3-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="310f3-106">Mostrar fragmentos de código siguiente Hola cómo toouse eventos de actor en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="310f3-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="310f3-107">Defina una interfaz que describe eventos de hello publicados por actor Hola.</span><span class="sxs-lookup"><span data-stu-id="310f3-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="310f3-108">Esta interfaz se debe derivar de hello `IActorEvents` interfaz.</span><span class="sxs-lookup"><span data-stu-id="310f3-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="310f3-109">Hola argumentos de métodos de hello deben ser [serializable de contrato de datos](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="310f3-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="310f3-110">Hola métodos deben devolver void, como evento de las notificaciones son una forma y esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="310f3-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="310f3-111">Declare los eventos de hello publicados por actor de hello en la interfaz de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="310f3-111">Declare hello events published by hello actor in hello actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="310f3-112">En el lado del cliente hello, implemente el controlador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="310f3-112">On hello client side, implement hello event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="310f3-113">En el cliente de hello, cree un actor de toohello de proxy que publica los eventos de Hola y suscribirán eventos tooits.</span><span class="sxs-lookup"><span data-stu-id="310f3-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="310f3-114">En caso de hello de conmutaciones por error, actor Hola puede conmutar por error tooa otro proceso o nodo.</span><span class="sxs-lookup"><span data-stu-id="310f3-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="310f3-115">proxy de actor Hola administra suscripciones activas de Hola y automáticamente volver a suscribe ellos.</span><span class="sxs-lookup"><span data-stu-id="310f3-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="310f3-116">Puede controlar el intervalo de saludo nueva suscripción a través de Hola `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="310f3-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="310f3-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="310f3-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="310f3-118">En actor hello, simplemente tiene que publicar eventos de hello cuando se producen.</span><span class="sxs-lookup"><span data-stu-id="310f3-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="310f3-119">Si hay eventos de toohello de los suscriptores, en tiempo de ejecución de hello actores les enviará Hola notificación.</span><span class="sxs-lookup"><span data-stu-id="310f3-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="310f3-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="310f3-120">Next steps</span></span>
* [<span data-ttu-id="310f3-121">Reentrada de actor</span><span class="sxs-lookup"><span data-stu-id="310f3-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="310f3-122">Supervisión del rendimiento y diagnósticos de los actores</span><span class="sxs-lookup"><span data-stu-id="310f3-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="310f3-123">Documentación de referencia de la API de actor</span><span class="sxs-lookup"><span data-stu-id="310f3-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="310f3-124">Código de ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="310f3-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="310f3-125">Código de ejemplo de .NET Core de C#</span><span class="sxs-lookup"><span data-stu-id="310f3-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="310f3-126">Código de ejemplo de Java</span><span class="sxs-lookup"><span data-stu-id="310f3-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
