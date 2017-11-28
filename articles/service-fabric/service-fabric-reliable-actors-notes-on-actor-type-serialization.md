---
title: "Notas de Reliable Actors sobre la serialización del tipo de actor | Microsoft Docs"
description: "Examina los requisitos básicos para la definición de clases serializables que se pueden usar para definir interfaces y estados de Reliable Actors de Service Fabric"
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
ms.openlocfilehash: 4b48b893e5a3bf5620f00a336576efe1ad63def8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="72e4a-103">Notas sobre la serialización del tipo de Reliable Actors de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="72e4a-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="72e4a-104">Los argumentos de todos los métodos, los tipos de resultados de las tareas que devuelve cada método de una interfaz de actor y los objetos almacenados en el administrador de estados de un actor deben ser [serializables de contratos de datos](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="72e4a-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="72e4a-105">Esto también se aplica a los argumentos de los métodos definidos en [interfaces de eventos de actor](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="72e4a-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="72e4a-106">(Los métodos de interfaz de eventos de actor siempre devuelven void).</span><span class="sxs-lookup"><span data-stu-id="72e4a-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="72e4a-107">Tipos de datos personalizados</span><span class="sxs-lookup"><span data-stu-id="72e4a-107">Custom data types</span></span>
<span data-ttu-id="72e4a-108">En este ejemplo, la siguiente interfaz de actor define un método que devuelve un tipo de datos personalizado denominado `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="72e4a-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="72e4a-109">La interfaz se implementa mediante un actor que utiliza el administrador de estado para almacenar un objeto `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="72e4a-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="72e4a-110">En este ejemplo, el objeto `VoicemailBox` se serializa en los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="72e4a-110">In this example, the `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="72e4a-111">El objeto se transmite entre una instancia de actor y un llamador.</span><span class="sxs-lookup"><span data-stu-id="72e4a-111">The object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="72e4a-112">El objeto se guarda en el administrador de estados, donde se almacena en un disco y se replica en otros nodos.</span><span class="sxs-lookup"><span data-stu-id="72e4a-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span></span>

<span data-ttu-id="72e4a-113">El marco de Reliable Actors usa la serialización DataContract.</span><span class="sxs-lookup"><span data-stu-id="72e4a-113">The Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="72e4a-114">Por lo tanto, los objetos de datos personalizados y sus miembros se deben anotar con los atributos **DataContract** y **DataMember**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="72e4a-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="72e4a-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72e4a-115">Next steps</span></span>
* [<span data-ttu-id="72e4a-116">Ciclo de vida de un actor y recolección de elementos no utilizados</span><span class="sxs-lookup"><span data-stu-id="72e4a-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="72e4a-117">Recordatorios y temporizadores de los actores</span><span class="sxs-lookup"><span data-stu-id="72e4a-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="72e4a-118">Eventos de actor</span><span class="sxs-lookup"><span data-stu-id="72e4a-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="72e4a-119">Reentrada de actor</span><span class="sxs-lookup"><span data-stu-id="72e4a-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="72e4a-120">Polimorfismo de actores y patrones de diseño orientado a objetos</span><span class="sxs-lookup"><span data-stu-id="72e4a-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="72e4a-121">Supervisión del rendimiento y diagnósticos de los actores</span><span class="sxs-lookup"><span data-stu-id="72e4a-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
