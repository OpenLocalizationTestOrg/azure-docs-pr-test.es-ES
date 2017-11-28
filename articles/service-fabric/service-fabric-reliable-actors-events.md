---
title: Eventos en microservicios de Azure basados en actores | Microsoft Docs
description: "Introducción a los eventos de Reliable Actors de Service Fabric."
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
ms.openlocfilehash: d936670c548ff709fc2e935d3f28d94e4bde8a04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="actor-events"></a><span data-ttu-id="74d41-103">Eventos de actor</span><span class="sxs-lookup"><span data-stu-id="74d41-103">Actor events</span></span>
<span data-ttu-id="74d41-104">Los eventos de actor ofrecen una manera de enviar notificaciones de mejor esfuerzo del actor a los clientes.</span><span class="sxs-lookup"><span data-stu-id="74d41-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span></span> <span data-ttu-id="74d41-105">Los eventos de actor están diseñados para la comunicación entre actor y cliente, y no deben usarse para una comunicación entre actores.</span><span class="sxs-lookup"><span data-stu-id="74d41-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="74d41-106">Los fragmentos de código siguientes muestran cómo usar los eventos de actor en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="74d41-106">The following code snippets show how to use actor events in your application.</span></span>

<span data-ttu-id="74d41-107">Defina una interfaz que describa los eventos publicados por el actor.</span><span class="sxs-lookup"><span data-stu-id="74d41-107">Define an interface that describes the events published by the actor.</span></span> <span data-ttu-id="74d41-108">Esta interfaz debe derivarse de la interfaz `IActorEvents` .</span><span class="sxs-lookup"><span data-stu-id="74d41-108">This interface must be derived from the `IActorEvents` interface.</span></span> <span data-ttu-id="74d41-109">Los argumentos de los métodos deben ser [serializable de contratos de datos](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="74d41-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="74d41-110">Los métodos deben devolver void, ya que las notificaciones de eventos son unidireccionales y de mejor esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="74d41-110">The methods must return void, as event notifications are one way and best effort.</span></span>

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
<span data-ttu-id="74d41-111">Declare los eventos publicados por el actor en la interfaz del actor.</span><span class="sxs-lookup"><span data-stu-id="74d41-111">Declare the events published by the actor in the actor interface.</span></span>

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
<span data-ttu-id="74d41-112">En el lado cliente, implemente el controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="74d41-112">On the client side, implement the event handler.</span></span>

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

<span data-ttu-id="74d41-113">En el cliente, cree un proxy para el actor que publica el evento y suscríbase a sus eventos.</span><span class="sxs-lookup"><span data-stu-id="74d41-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="74d41-114">Si se producen conmutaciones por error, el actor puede realizar una conmutación por error a un nodo o proceso diferentes.</span><span class="sxs-lookup"><span data-stu-id="74d41-114">In the event of failovers, the actor may fail over to a different process or node.</span></span> <span data-ttu-id="74d41-115">El proxy del actor administra las suscripciones activas y las vuelve a suscribir automáticamente.</span><span class="sxs-lookup"><span data-stu-id="74d41-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="74d41-116">Puede controlar el intervalo de suscribir nuevamente mediante la API `ActorProxyEventExtensions.SubscribeAsync<TEvent>` .</span><span class="sxs-lookup"><span data-stu-id="74d41-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="74d41-117">Para cancelar la suscripción, use la API `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` .</span><span class="sxs-lookup"><span data-stu-id="74d41-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="74d41-118">En el actor, simplemente publique los eventos cuando se produzcan.</span><span class="sxs-lookup"><span data-stu-id="74d41-118">On the actor, simply publish the events as they happen.</span></span> <span data-ttu-id="74d41-119">Si hay suscriptores del evento, el tiempo de ejecución de los actores les enviará la notificación.</span><span class="sxs-lookup"><span data-stu-id="74d41-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="74d41-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="74d41-120">Next steps</span></span>
* [<span data-ttu-id="74d41-121">Reentrada de actor</span><span class="sxs-lookup"><span data-stu-id="74d41-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="74d41-122">Supervisión del rendimiento y diagnósticos de los actores</span><span class="sxs-lookup"><span data-stu-id="74d41-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="74d41-123">Documentación de referencia de la API de actor</span><span class="sxs-lookup"><span data-stu-id="74d41-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="74d41-124">Código de ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="74d41-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="74d41-125">Código de ejemplo de .NET Core de C#</span><span class="sxs-lookup"><span data-stu-id="74d41-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="74d41-126">Código de ejemplo de Java</span><span class="sxs-lookup"><span data-stu-id="74d41-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
