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
# <a name="actor-events"></a>Eventos de actor
Eventos de actor proporcionan un notificaciones de mejor esfuerzo de toosend de forma de los clientes de hello actor toohello. Los eventos de actor están diseñados para la comunicación entre actor y cliente, y no deben usarse para una comunicación entre actores.

Mostrar fragmentos de código siguiente Hola cómo toouse eventos de actor en la aplicación.

Defina una interfaz que describe eventos de hello publicados por actor Hola. Esta interfaz se debe derivar de hello `IActorEvents` interfaz. Hola argumentos de métodos de hello deben ser [serializable de contrato de datos](service-fabric-reliable-actors-notes-on-actor-type-serialization.md). Hola métodos deben devolver void, como evento de las notificaciones son una forma y esfuerzo.

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
Declare los eventos de hello publicados por actor de hello en la interfaz de actor Hola.

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
En el lado del cliente hello, implemente el controlador de eventos de Hola.

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

En el cliente de hello, cree un actor de toohello de proxy que publica los eventos de Hola y suscribirán eventos tooits.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

En caso de hello de conmutaciones por error, actor Hola puede conmutar por error tooa otro proceso o nodo. proxy de actor Hola administra suscripciones activas de Hola y automáticamente volver a suscribe ellos. Puede controlar el intervalo de saludo nueva suscripción a través de Hola `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API. toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.

En actor hello, simplemente tiene que publicar eventos de hello cuando se producen. Si hay eventos de toohello de los suscriptores, en tiempo de ejecución de hello actores les enviará Hola notificación.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>Pasos siguientes
* [Reentrada de actor](service-fabric-reliable-actors-reentrancy.md)
* [Supervisión del rendimiento y diagnósticos de los actores](service-fabric-reliable-actors-diagnostics.md)
* [Documentación de referencia de la API de actor](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Código de ejemplo de C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Código de ejemplo de .NET Core de C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Código de ejemplo de Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)
