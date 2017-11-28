---
title: aaaOverview del ciclo de vida de microservicios de Azure basado en actores | Documentos de Microsoft
description: "Explica el ciclo de vida de Reliable Actors de Service Fabric, la recolección de elementos no utilizados y la eliminación manual de actores y su estado"
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="63979-103">Ciclo de vida, recolección automática de elementos no utilizados y eliminación manual de actores</span><span class="sxs-lookup"><span data-stu-id="63979-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="63979-104">Se activa un actor Hola la primera vez que se realiza una llamada tooany de sus métodos.</span><span class="sxs-lookup"><span data-stu-id="63979-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="63979-105">Un actor está desactivado (recolectan en tiempo de ejecución de hello actores) si no se utiliza para un período de tiempo configurable.</span><span class="sxs-lookup"><span data-stu-id="63979-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="63979-106">Un actor y su estado también se pueden eliminar manualmente en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="63979-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="63979-107">Activación de actores</span><span class="sxs-lookup"><span data-stu-id="63979-107">Actor activation</span></span>
<span data-ttu-id="63979-108">Cuando se activa un actor, se produce el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="63979-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="63979-109">Cuando se recibe una llamada para un actor y no hay ninguno activo, se crea uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="63979-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="63979-110">estado del actor Hola se carga si mantiene el estado.</span><span class="sxs-lookup"><span data-stu-id="63979-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="63979-111">Hola `OnActivateAsync` (C#) o `onActivateAsync` se llama al método (Java) (que se puede invalidar en la implementación de actor hello).</span><span class="sxs-lookup"><span data-stu-id="63979-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="63979-112">actor Hola ahora se considera activo.</span><span class="sxs-lookup"><span data-stu-id="63979-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="63979-113">Desactivación de actores</span><span class="sxs-lookup"><span data-stu-id="63979-113">Actor deactivation</span></span>
<span data-ttu-id="63979-114">Cuando un actor está desactivado, se produce el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="63979-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="63979-115">Cuando no se utiliza un actor durante un período de tiempo, se quita de tabla de actores Active Hola.</span><span class="sxs-lookup"><span data-stu-id="63979-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="63979-116">Hola `OnDeactivateAsync` (C#) o `onDeactivateAsync` se llama al método (Java) (que se puede invalidar en la implementación de actor hello).</span><span class="sxs-lookup"><span data-stu-id="63979-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="63979-117">Esto borra todos los temporizadores de hello para el actor Hola.</span><span class="sxs-lookup"><span data-stu-id="63979-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="63979-118">Las operaciones de actor como los cambios de estado no deben llamarse desde este método.</span><span class="sxs-lookup"><span data-stu-id="63979-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="63979-119">Hello en tiempo de ejecución de tejido actores emite algunos [eventos relacionados con tooactor activación y desactivación](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="63979-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="63979-120">Son útiles para la supervisión del rendimiento y los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="63979-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="63979-121">Recolección de actores no utilizados</span><span class="sxs-lookup"><span data-stu-id="63979-121">Actor garbage collection</span></span>
<span data-ttu-id="63979-122">Cuando un actor está desactivado, se libera el objeto de actor de toohello de referencias y puede ser recolectado normalmente por el recolector de elementos no utilizados de java virtual machine (JVM) u Hola common language runtime (CLR).</span><span class="sxs-lookup"><span data-stu-id="63979-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="63979-123">Recolección de elementos solo limpia los objetos de actor Hola; lo hace **no** quitar estado almacenado en el Administrador de estado del actor Hola.</span><span class="sxs-lookup"><span data-stu-id="63979-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="63979-124">actor de Hello siguiente tiempo Hola se activa, se crea un nuevo objeto de actor y se restaura su estado.</span><span class="sxs-lookup"><span data-stu-id="63979-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="63979-125">¿Qué se considera "se usa?" a fin de Hola de desactivación y recolección de elementos?</span><span class="sxs-lookup"><span data-stu-id="63979-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="63979-126">Se recibe una llamada.</span><span class="sxs-lookup"><span data-stu-id="63979-126">Receiving a call</span></span>
* <span data-ttu-id="63979-127">`IRemindable.ReceiveReminderAsync`método que se invoca (se aplica solo si actor hello usa recordatorios)</span><span class="sxs-lookup"><span data-stu-id="63979-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="63979-128">Si actor Hola utiliza temporizadores y se invoca la devolución de llamada de temporizador, lo hace **no** recuento como "se usa?".</span><span class="sxs-lookup"><span data-stu-id="63979-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="63979-129">Antes de entrar en detalles de Hola de desactivación, es hello toodefine importante términos siguientes:</span><span class="sxs-lookup"><span data-stu-id="63979-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="63979-130">*Intervalo de detección*.</span><span class="sxs-lookup"><span data-stu-id="63979-130">*Scan interval*.</span></span> <span data-ttu-id="63979-131">Esto es en qué Hola actores en tiempo de ejecución examina su tabla actores Active actores que pueden desactivar el intervalo de saludo y el recolector.</span><span class="sxs-lookup"><span data-stu-id="63979-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="63979-132">Hola valor predeterminado es 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="63979-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="63979-133">*Tiempo de espera de inactividad*.</span><span class="sxs-lookup"><span data-stu-id="63979-133">*Idle timeout*.</span></span> <span data-ttu-id="63979-134">Es Hola cantidad de tiempo que un actor requiere tooremain sin usar (inactivo) antes de que se puede desactivar y el recolector.</span><span class="sxs-lookup"><span data-stu-id="63979-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="63979-135">Hola valor predeterminado es 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="63979-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="63979-136">Por lo general, no es necesario toochange estos valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="63979-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="63979-137">Sin embargo, si es necesario, estos intervalos pueden cambiarse mediante `ActorServiceSettings` al registrar el [servicio de actor](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="63979-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
<span data-ttu-id="63979-138">Para cada actor activa, en tiempo de ejecución de hello actor realiza un seguimiento de hello cantidad de tiempo que ha estado inactivo (es decir, no se utiliza).</span><span class="sxs-lookup"><span data-stu-id="63979-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="63979-139">tiempo de ejecución de Hello actor comprueba cada uno de los actores de hello cada `ScanIntervalInSeconds` toosee si es posible de elementos no utilizados se recopilan y se recopila, si ha estado inactiva durante `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="63979-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="63979-140">Cada vez que se usa un actor, su tiempo de inactividad es too0 de restablecimiento.</span><span class="sxs-lookup"><span data-stu-id="63979-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="63979-141">Después de esto, actor Hola puede recopilarán sólo si nuevo permanece inactiva durante `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="63979-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="63979-142">Recuerde que un actor se considera toohave sido usa si se ejecuta un método de interfaz de actor o una devolución de llamada de aviso de actor.</span><span class="sxs-lookup"><span data-stu-id="63979-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="63979-143">Un actor está **no** considera toohave sido usa si se ejecuta su devolución de llamada de temporizador.</span><span class="sxs-lookup"><span data-stu-id="63979-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="63979-144">Hello siguiente diagrama muestra hello ciclo de vida de un actor único tooillustrate estos conceptos.</span><span class="sxs-lookup"><span data-stu-id="63979-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![Ejemplo de tiempo de inactividad][1]

<span data-ttu-id="63979-146">ejemplo de Hola muestra impacto Hola de llamadas al método actor, avisos y temporizadores en duración de Hola de este actor.</span><span class="sxs-lookup"><span data-stu-id="63979-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="63979-147">Hola siguientes puntos acerca de ejemplo de Hola merece la pena comentar:</span><span class="sxs-lookup"><span data-stu-id="63979-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="63979-148">ScanInterval IdleTimeout se establecen y too5 y 10 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="63979-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="63979-149">(Unidades no importa en este caso, puesto que nuestro objetivo es solo el concepto de hello tooillustrate.)</span><span class="sxs-lookup"><span data-stu-id="63979-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="63979-150">examen de Hola para actores toobe recolección se produce en T = 0, 5, 10, 15, 20, 25, tal como se define por intervalo de recorrido de saludo de 5.</span><span class="sxs-lookup"><span data-stu-id="63979-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="63979-151">Un temporizador periódico se activa en T=4,8,12,16,20,24 y se ejecuta su devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="63979-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="63979-152">No afecta a tiempo de inactividad de Hola de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="63979-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="63979-153">Una llamada al método de actor en T = 7 restablece too0 de tiempo de inactividad de Hola y retrasa la recolección de elementos Hola de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="63979-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="63979-154">Ejecuta una devolución de llamada de aviso de actor en T = 14 y más retrasos Hola recolección de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="63979-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="63979-155">Durante el análisis de recopilación de elementos no utilizados de hello en T = 25, tiempo de inactividad del actor Hola finalmente supera el tiempo de inactividad de Hola de 10 y actor hello es recolectado.</span><span class="sxs-lookup"><span data-stu-id="63979-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="63979-156">Un actor nunca se recolectará como elemento no utilizado mientras se ejecuta uno de sus métodos, independientemente del tiempo que se dedique a la ejecución de ese método.</span><span class="sxs-lookup"><span data-stu-id="63979-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="63979-157">Tal y como se mencionó anteriormente, ejecución de Hola de métodos de interfaz de actor y las devoluciones de llamada de recordatorio impide la recolección mediante el restablecimiento too0 de tiempo de inactividad del actor hello.</span><span class="sxs-lookup"><span data-stu-id="63979-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="63979-158">ejecución de Hola de devoluciones de llamada de temporizador no restablece hello too0 de tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="63979-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="63979-159">Sin embargo, recolección de elementos Hola de actor Hola se aplaza hasta que devolución de llamada de temporizador de hello ha completado su ejecución.</span><span class="sxs-lookup"><span data-stu-id="63979-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="63979-160">Eliminación de actores y su estado</span><span class="sxs-lookup"><span data-stu-id="63979-160">Deleting actors and their state</span></span>
<span data-ttu-id="63979-161">Recolección de elementos de actores desactivados solo limpia los objetos de actor hello, pero no elimina los datos que se almacenan en el Administrador de estado de un actor.</span><span class="sxs-lookup"><span data-stu-id="63979-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="63979-162">Cuando se vuelva a activar un actor, sus datos se efectúa tooit disponible a través de hello Administrador de Estados.</span><span class="sxs-lookup"><span data-stu-id="63979-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="63979-163">En casos donde actores almacenar datos en el Administrador de estado y se desactiva pero nunca se vuelve a activar, puede ser necesario tooclean sus datos.</span><span class="sxs-lookup"><span data-stu-id="63979-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="63979-164">Hola [servicio de Actor](service-fabric-reliable-actors-platform.md) proporciona una función para eliminar los actores de un llamador remoto:</span><span class="sxs-lookup"><span data-stu-id="63979-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="63979-165">La eliminación de un actor tendrá Hola después efectos dependiendo de si o no está activo actualmente actor hello:</span><span class="sxs-lookup"><span data-stu-id="63979-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="63979-166">**Actor activo**</span><span class="sxs-lookup"><span data-stu-id="63979-166">**Active Actor**</span></span>
  * <span data-ttu-id="63979-167">El actor se quita de la lista de actores activos y se desactiva.</span><span class="sxs-lookup"><span data-stu-id="63979-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="63979-168">Su estado se elimina permanentemente.</span><span class="sxs-lookup"><span data-stu-id="63979-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="63979-169">**Actor inactivo**</span><span class="sxs-lookup"><span data-stu-id="63979-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="63979-170">Su estado se elimina permanentemente.</span><span class="sxs-lookup"><span data-stu-id="63979-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="63979-171">Tenga en cuenta que no puede llamar un actor eliminar por sí sola desde uno de sus métodos de actor porque actor hello no se puede eliminar mientras se ejecuta dentro de un contexto de llamada de actor en qué hello en tiempo de ejecución ha obtenido un bloqueo alrededor de un único subproceso acceso de la llamada a tooenforce Hola actor.</span><span class="sxs-lookup"><span data-stu-id="63979-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63979-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="63979-172">Next steps</span></span>
* [<span data-ttu-id="63979-173">Recordatorios y temporizadores de los actores</span><span class="sxs-lookup"><span data-stu-id="63979-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="63979-174">Eventos de actor</span><span class="sxs-lookup"><span data-stu-id="63979-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="63979-175">Reentrada de actor</span><span class="sxs-lookup"><span data-stu-id="63979-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="63979-176">Supervisión del rendimiento y diagnósticos de los actores</span><span class="sxs-lookup"><span data-stu-id="63979-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="63979-177">Documentación de referencia de la API de actor</span><span class="sxs-lookup"><span data-stu-id="63979-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="63979-178">Código de ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="63979-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="63979-179">Código de ejemplo de Java</span><span class="sxs-lookup"><span data-stu-id="63979-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
