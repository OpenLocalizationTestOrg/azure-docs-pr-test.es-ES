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
# <a name="actor-timers-and-reminders"></a>Recordatorios y temporizadores de los actores
Los actores pueden programar el trabajo periódico mediante el registro de temporizadores o recordatorios. Este artículo se muestra cómo toouse temporizadores y recordatorios y explica las diferencias de hello entre ellos.

## <a name="actor-timers"></a>Temporizadores de actor
Temporizadores de actor proporcionan un contenedor simple en una tooensure de temporizador de .NET o Java que los métodos de devolución de llamada de hello respetan garantías de simultaneidad basada en Active Hola Hola actores proporciona en tiempo de ejecución.

Actores pueden utilizar hello `RegisterTimer`(C#) o `registerTimer`(Java) y `UnregisterTimer`(C#) o `unregisterTimer`métodos (Java) en su base de clase tooregister y anular el registro de los temporizadores. ejemplo de Hola siguiente muestra uso de Hola de temporizador API. Hola API son muy similar timer de .NET toohello o temporizador de Java. En este ejemplo, cuando el temporizador de hello vence, en tiempo de ejecución de hello actores llamará hello `MoveObject`(C#) o `moveObject`método (Java). método Hello se garantiza la simultaneidad basada en el turno de toorespect Hola. Esto significa que no habrá otros métodos de actor o devoluciones de llamada de temporizador o recordatorio en curso hasta que esta devolución de llamada complete la ejecución.

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

Hola siguiente período de temporizador de hello comenzará al finalizar la devolución de llamada de hello ejecución. Esto implica que temporizador Hola se detuvo durante la devolución de llamada de saludo se está ejecutando y se inicia cuando finaliza la devolución de llamada de Hola.

en tiempo de ejecución de Hello actores guarda los cambios realizados el Administrador de estado del actor toohello cuando finaliza la devolución de llamada de Hola. Si se produce un error en Guardar el estado de hello, ese objeto actor se desactivará y se activará una nueva instancia.

Todos los temporizadores se detienen cuando actor Hola está desactivado como parte de la colección de elementos no utilizados. Después de eso, no se invoca ninguna devolución de llamada de temporizador. Además, el tiempo de ejecución de hello actores no conserva toda la información sobre los temporizadores de Hola que se estaban ejecutando antes de la desactivación. Es una toohello actor tooregister los temporizadores que necesita cuando se reactiva Hola futuras. Para obtener más información, vea la sección de hello en [recolección actor](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Recordatorios de actor
Los avisos son un mecanismo tootrigger persistentes devoluciones de llamada en un actor en horas especificadas. Su funcionalidad es tootimers similar. Pero a diferencia de los temporizadores, los avisos se activan en todas las circunstancias hasta que actor Hola explícitamente anula el registro de ellas o actor Hola explícitamente se elimina. En concreto, recordatorios se activan a través de las conmutaciones por error y desactivaciones actor porque el tiempo de ejecución de hello actores conserva la información sobre los avisos de actor Hola.

tooregister un aviso, llama a un actor hello `RegisterReminderAsync` método proporcionado en la clase base hello, como se muestra en el siguiente ejemplo de Hola:

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

En este ejemplo, `"Pay cell phone bill"` es el nombre de aviso de Hola. Esto es una cadena que Hola actor utiliza toouniquely identificar un aviso. `BitConverter.GetBytes(amountInDollars)`(C#) es el contexto de Hola que está asociado con el aviso de Hola. Se pasará toohello atrás actor es decir, como una devolución de llamada de argumento toohello recordatorio, `IRemindable.ReceiveReminderAsync`(C#) o `Remindable.receiveReminderAsync`(Java).

Actores que use recordatorios deben implementar hello `IRemindable` interfaz, como se muestra en el siguiente ejemplo de Hola.

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

Cuando se desencadena un aviso, en tiempo de ejecución de hello Reliable Actors invocarán hello `ReceiveReminderAsync`(C#) o `receiveReminderAsync`método (Java) en hello Actor. Un actor puede registrar varios avisos y Hola `ReceiveReminderAsync`(C#) o `receiveReminderAsync`(Java) método se invoca cuando se desencadena cualquiera de estos avisos. actor Hola puede utilizar el nombre de aviso de Hola que se pasa en toohello `ReceiveReminderAsync`(C#) o `receiveReminderAsync`(Java) método toofigure qué se desencadenó el aviso.

en tiempo de ejecución de actores Hello guarda estado del actor Hola cuando se hello `ReceiveReminderAsync`(C#) o `receiveReminderAsync`finaliza la llamada a (Java). Si se produce un error en Guardar el estado de hello, ese objeto actor se desactivará y se activará una nueva instancia.

toounregister un aviso, llama a un actor hello `UnregisterReminderAsync`(C#) o `unregisterReminderAsync`método (Java), como se muestra en los ejemplos de hello siguientes.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Como se indicó anteriormente, Hola `UnregisterReminderAsync`(C#) o `unregisterReminderAsync`(Java) método acepta un `IActorReminder`(C#) o `ActorReminder`(interfaz) (Java). Hola actor clase base admite un `GetReminder`(C#) o `getReminder`método (Java) que puede ser utilizados tooretrieve hello `IActorReminder`(C#) o `ActorReminder`(interfaz) (Java) pasando en nombre de aviso de Hola. Esto resulta útil porque actor hello no necesita hello toopersist `IActorReminder`(C#) o `ActorReminder`interfaz (Java) que se devolvió desde hello `RegisterReminder`(C#) o `registerReminder`llamada a un método (Java).

## <a name="next-steps"></a>Pasos siguientes
Obtenga información sobre los eventos y la reentrada de Reliable Actor:
* [Eventos de actor](service-fabric-reliable-actors-events.md)
* [Reentrada de actor](service-fabric-reliable-actors-reentrancy.md)
