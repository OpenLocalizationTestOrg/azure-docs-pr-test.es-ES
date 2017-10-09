---
title: "notas de actores aaaReliable en actor escriba serialización | Documentos de Microsoft"
description: "Explica los requisitos básicos para definir interfaces y clases serializables que pueden ser utilizado toodefine Estados de servicio de Fabric Reliable Actors"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a>Notas sobre la serialización del tipo de Reliable Actors de Service Fabric
argumentos de Hola de todos los métodos, tipos de resultado de las tareas de hello devuelven por cada método en una interfaz de actor y deben ser objetos almacenados en el Administrador de estado de un actor [serializable de contrato de datos](https://msdn.microsoft.com/library/ms731923.aspx). Esto también aplica toohello argumentos de métodos de hello definidos en [interfaces de eventos de actor](service-fabric-reliable-actors-events.md). (Los métodos de interfaz de eventos de actor siempre devuelven void).

## <a name="custom-data-types"></a>Tipos de datos personalizados
En este ejemplo, hello siguiendo la interfaz de actor define un método que devuelve un tipo de datos personalizado denominado `VoicemailBox`:

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

Hola se implementa mediante un actor que usa Hola estado manager toostore un `VoicemailBox` objeto:

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

En este ejemplo, Hola `VoicemailBox` se serializa el objeto cuando:

* objeto de Hola se transmite entre una instancia de actor y un autor de llamada.
* objeto de Hola se guarda en el Administrador de estado de Hola donde se toodisk persistente y replican tooother nodos.

el marco de trabajo de Hello Actor confiable utiliza la serialización de DataContract. Hola por lo tanto, los objetos de datos personalizados y sus miembros se deben anotar con hello **DataContract** y **DataMember** atributos, respectivamente.

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a>Pasos siguientes
* [Ciclo de vida de un actor y recolección de elementos no utilizados](service-fabric-reliable-actors-lifecycle.md)
* [Recordatorios y temporizadores de los actores](service-fabric-reliable-actors-timers-reminders.md)
* [Eventos de actor](service-fabric-reliable-actors-events.md)
* [Reentrada de actor](service-fabric-reliable-actors-reentrancy.md)
* [Polimorfismo de actores y patrones de diseño orientado a objetos](service-fabric-reliable-actors-polymorphism.md)
* [Supervisión del rendimiento y diagnósticos de los actores](service-fabric-reliable-actors-diagnostics.md)
