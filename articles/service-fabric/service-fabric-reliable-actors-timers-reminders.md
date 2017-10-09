---
title: aaaReliable actores temporizadores y recordatorios | Documentos de Microsoft
description: "Introducción tootimers y avisos de Reliable Actors de tejido de servicio."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="0836c-103">Recordatorios y temporizadores de los actores</span><span class="sxs-lookup"><span data-stu-id="0836c-103">Actor timers and reminders</span></span>
<span data-ttu-id="0836c-104">Los actores pueden programar el trabajo periódico mediante el registro de temporizadores o recordatorios.</span><span class="sxs-lookup"><span data-stu-id="0836c-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="0836c-105">Este artículo se muestra cómo toouse temporizadores y recordatorios y explica las diferencias de hello entre ellos.</span><span class="sxs-lookup"><span data-stu-id="0836c-105">This article shows how toouse timers and reminders and explains hello differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="0836c-106">Temporizadores de actor</span><span class="sxs-lookup"><span data-stu-id="0836c-106">Actor timers</span></span>
<span data-ttu-id="0836c-107">Temporizadores de actor proporcionan un contenedor simple en una tooensure de temporizador de .NET o Java que los métodos de devolución de llamada de hello respetan garantías de simultaneidad basada en Active Hola Hola actores proporciona en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0836c-107">Actor timers provide a simple wrapper around a .NET or Java timer tooensure that hello callback methods respect hello turn-based concurrency guarantees that hello Actors runtime provides.</span></span>

<span data-ttu-id="0836c-108">Actores pueden utilizar hello `RegisterTimer`(C#) o `registerTimer`(Java) y `UnregisterTimer`(C#) o `unregisterTimer`métodos (Java) en su base de clase tooregister y anular el registro de los temporizadores.</span><span class="sxs-lookup"><span data-stu-id="0836c-108">Actors can use hello `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class tooregister and unregister their timers.</span></span> <span data-ttu-id="0836c-109">ejemplo de Hola siguiente muestra uso de Hola de temporizador API.</span><span class="sxs-lookup"><span data-stu-id="0836c-109">hello example below shows hello use of timer APIs.</span></span> <span data-ttu-id="0836c-110">Hola API son muy similar timer de .NET toohello o temporizador de Java.</span><span class="sxs-lookup"><span data-stu-id="0836c-110">hello APIs are very similar toohello .NET timer or Java timer.</span></span> <span data-ttu-id="0836c-111">En este ejemplo, cuando el temporizador de hello vence, en tiempo de ejecución de hello actores llamará hello `MoveObject`(C#) o `moveObject`método (Java).</span><span class="sxs-lookup"><span data-stu-id="0836c-111">In this example, when hello timer is due, hello Actors runtime will call hello `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="0836c-112">método Hello se garantiza la simultaneidad basada en el turno de toorespect Hola.</span><span class="sxs-lookup"><span data-stu-id="0836c-112">hello method is guaranteed toorespect hello turn-based concurrency.</span></span> <span data-ttu-id="0836c-113">Esto significa que no habrá otros métodos de actor o devoluciones de llamada de temporizador o recordatorio en curso hasta que esta devolución de llamada complete la ejecución.</span><span class="sxs-lookup"><span data-stu-id="0836c-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="0836c-114">Hola siguiente período de temporizador de hello comenzará al finalizar la devolución de llamada de hello ejecución.</span><span class="sxs-lookup"><span data-stu-id="0836c-114">hello next period of hello timer starts after hello callback completes execution.</span></span> <span data-ttu-id="0836c-115">Esto implica que temporizador Hola se detuvo durante la devolución de llamada de saludo se está ejecutando y se inicia cuando finaliza la devolución de llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="0836c-115">This implies that hello timer is stopped while hello callback is executing and is started when hello callback finishes.</span></span>

<span data-ttu-id="0836c-116">en tiempo de ejecución de Hello actores guarda los cambios realizados el Administrador de estado del actor toohello cuando finaliza la devolución de llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="0836c-116">hello Actors runtime saves changes made toohello actor's State Manager when hello callback finishes.</span></span> <span data-ttu-id="0836c-117">Si se produce un error en Guardar el estado de hello, ese objeto actor se desactivará y se activará una nueva instancia.</span><span class="sxs-lookup"><span data-stu-id="0836c-117">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="0836c-118">Todos los temporizadores se detienen cuando actor Hola está desactivado como parte de la colección de elementos no utilizados.</span><span class="sxs-lookup"><span data-stu-id="0836c-118">All timers are stopped when hello actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="0836c-119">Después de eso, no se invoca ninguna devolución de llamada de temporizador.</span><span class="sxs-lookup"><span data-stu-id="0836c-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="0836c-120">Además, el tiempo de ejecución de hello actores no conserva toda la información sobre los temporizadores de Hola que se estaban ejecutando antes de la desactivación.</span><span class="sxs-lookup"><span data-stu-id="0836c-120">Also, hello Actors runtime does not retain any information about hello timers that were running before deactivation.</span></span> <span data-ttu-id="0836c-121">Es una toohello actor tooregister los temporizadores que necesita cuando se reactiva Hola futuras.</span><span class="sxs-lookup"><span data-stu-id="0836c-121">It is up toohello actor tooregister any timers that it needs when it is reactivated in hello future.</span></span> <span data-ttu-id="0836c-122">Para obtener más información, vea la sección de hello en [recolección actor](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="0836c-122">For more information, see hello section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="0836c-123">Recordatorios de actor</span><span class="sxs-lookup"><span data-stu-id="0836c-123">Actor reminders</span></span>
<span data-ttu-id="0836c-124">Los avisos son un mecanismo tootrigger persistentes devoluciones de llamada en un actor en horas especificadas.</span><span class="sxs-lookup"><span data-stu-id="0836c-124">Reminders are a mechanism tootrigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="0836c-125">Su funcionalidad es tootimers similar.</span><span class="sxs-lookup"><span data-stu-id="0836c-125">Their functionality is similar tootimers.</span></span> <span data-ttu-id="0836c-126">Pero a diferencia de los temporizadores, los avisos se activan en todas las circunstancias hasta que actor Hola explícitamente anula el registro de ellas o actor Hola explícitamente se elimina.</span><span class="sxs-lookup"><span data-stu-id="0836c-126">But unlike timers, reminders are triggered under all circumstances until hello actor explicitly unregisters them or hello actor is explicitly deleted.</span></span> <span data-ttu-id="0836c-127">En concreto, recordatorios se activan a través de las conmutaciones por error y desactivaciones actor porque el tiempo de ejecución de hello actores conserva la información sobre los avisos de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="0836c-127">Specifically, reminders are triggered across actor deactivations and failovers because hello Actors runtime persists information about hello actor's reminders.</span></span>

<span data-ttu-id="0836c-128">tooregister un aviso, llama a un actor hello `RegisterReminderAsync` método proporcionado en la clase base hello, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="0836c-128">tooregister a reminder, an actor calls hello `RegisterReminderAsync` method provided on hello base class, as shown in hello following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

<span data-ttu-id="0836c-129">En este ejemplo, `"Pay cell phone bill"` es el nombre de aviso de Hola.</span><span class="sxs-lookup"><span data-stu-id="0836c-129">In this example, `"Pay cell phone bill"` is hello reminder name.</span></span> <span data-ttu-id="0836c-130">Esto es una cadena que Hola actor utiliza toouniquely identificar un aviso.</span><span class="sxs-lookup"><span data-stu-id="0836c-130">This is a string that hello actor uses toouniquely identify a reminder.</span></span> <span data-ttu-id="0836c-131">`BitConverter.GetBytes(amountInDollars)`(C#) es el contexto de Hola que está asociado con el aviso de Hola.</span><span class="sxs-lookup"><span data-stu-id="0836c-131">`BitConverter.GetBytes(amountInDollars)`(C#) is hello context that is associated with hello reminder.</span></span> <span data-ttu-id="0836c-132">Se pasará toohello atrás actor es decir, como una devolución de llamada de argumento toohello recordatorio, `IRemindable.ReceiveReminderAsync`(C#) o `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="0836c-132">It will be passed back toohello actor as an argument toohello reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="0836c-133">Actores que use recordatorios deben implementar hello `IRemindable` interfaz, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0836c-133">Actors that use reminders must implement hello `IRemindable` interface, as shown in hello example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="0836c-134">Cuando se desencadena un aviso, en tiempo de ejecución de hello Reliable Actors invocarán hello `ReceiveReminderAsync`(C#) o `receiveReminderAsync`método (Java) en hello Actor.</span><span class="sxs-lookup"><span data-stu-id="0836c-134">When a reminder is triggered, hello Reliable Actors runtime will invoke hello  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on hello Actor.</span></span> <span data-ttu-id="0836c-135">Un actor puede registrar varios avisos y Hola `ReceiveReminderAsync`(C#) o `receiveReminderAsync`(Java) método se invoca cuando se desencadena cualquiera de estos avisos.</span><span class="sxs-lookup"><span data-stu-id="0836c-135">An actor can register multiple reminders, and hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="0836c-136">actor Hola puede utilizar el nombre de aviso de Hola que se pasa en toohello `ReceiveReminderAsync`(C#) o `receiveReminderAsync`(Java) método toofigure qué se desencadenó el aviso.</span><span class="sxs-lookup"><span data-stu-id="0836c-136">hello actor can use hello reminder name that is passed in toohello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method toofigure out which reminder was triggered.</span></span>

<span data-ttu-id="0836c-137">en tiempo de ejecución de actores Hello guarda estado del actor Hola cuando se hello `ReceiveReminderAsync`(C#) o `receiveReminderAsync`finaliza la llamada a (Java).</span><span class="sxs-lookup"><span data-stu-id="0836c-137">hello Actors runtime saves hello actor's state when hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="0836c-138">Si se produce un error en Guardar el estado de hello, ese objeto actor se desactivará y se activará una nueva instancia.</span><span class="sxs-lookup"><span data-stu-id="0836c-138">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="0836c-139">toounregister un aviso, llama a un actor hello `UnregisterReminderAsync`(C#) o `unregisterReminderAsync`método (Java), como se muestra en los ejemplos de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="0836c-139">toounregister a reminder, an actor calls hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in hello examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="0836c-140">Como se indicó anteriormente, Hola `UnregisterReminderAsync`(C#) o `unregisterReminderAsync`(Java) método acepta un `IActorReminder`(C#) o `ActorReminder`(interfaz) (Java).</span><span class="sxs-lookup"><span data-stu-id="0836c-140">As shown above, hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="0836c-141">Hola actor clase base admite un `GetReminder`(C#) o `getReminder`método (Java) que puede ser utilizados tooretrieve hello `IActorReminder`(C#) o `ActorReminder`(interfaz) (Java) pasando en nombre de aviso de Hola.</span><span class="sxs-lookup"><span data-stu-id="0836c-141">hello actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used tooretrieve hello `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in hello reminder name.</span></span> <span data-ttu-id="0836c-142">Esto resulta útil porque actor hello no necesita hello toopersist `IActorReminder`(C#) o `ActorReminder`interfaz (Java) que se devolvió desde hello `RegisterReminder`(C#) o `registerReminder`llamada a un método (Java).</span><span class="sxs-lookup"><span data-stu-id="0836c-142">This is convenient because hello actor does not need toopersist hello `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from hello `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0836c-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0836c-143">Next Steps</span></span>
<span data-ttu-id="0836c-144">Obtenga información sobre los eventos y la reentrada de Reliable Actor:</span><span class="sxs-lookup"><span data-stu-id="0836c-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="0836c-145">Eventos de actor</span><span class="sxs-lookup"><span data-stu-id="0836c-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="0836c-146">Reentrada de actor</span><span class="sxs-lookup"><span data-stu-id="0836c-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
