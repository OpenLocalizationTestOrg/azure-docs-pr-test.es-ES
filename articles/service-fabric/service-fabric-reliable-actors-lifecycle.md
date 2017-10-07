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
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>Ciclo de vida, recolección automática de elementos no utilizados y eliminación manual de actores
Se activa un actor Hola la primera vez que se realiza una llamada tooany de sus métodos. Un actor está desactivado (recolectan en tiempo de ejecución de hello actores) si no se utiliza para un período de tiempo configurable. Un actor y su estado también se pueden eliminar manualmente en cualquier momento.

## <a name="actor-activation"></a>Activación de actores
Cuando se activa un actor, se produce el siguiente hello:

* Cuando se recibe una llamada para un actor y no hay ninguno activo, se crea uno nuevo.
* estado del actor Hola se carga si mantiene el estado.
* Hola `OnActivateAsync` (C#) o `onActivateAsync` se llama al método (Java) (que se puede invalidar en la implementación de actor hello).
* actor Hola ahora se considera activo.

## <a name="actor-deactivation"></a>Desactivación de actores
Cuando un actor está desactivado, se produce el siguiente hello:

* Cuando no se utiliza un actor durante un período de tiempo, se quita de tabla de actores Active Hola.
* Hola `OnDeactivateAsync` (C#) o `onDeactivateAsync` se llama al método (Java) (que se puede invalidar en la implementación de actor hello). Esto borra todos los temporizadores de hello para el actor Hola. Las operaciones de actor como los cambios de estado no deben llamarse desde este método.

> [!TIP]
> Hello en tiempo de ejecución de tejido actores emite algunos [eventos relacionados con tooactor activación y desactivación](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters). Son útiles para la supervisión del rendimiento y los diagnósticos.
>
>

### <a name="actor-garbage-collection"></a>Recolección de actores no utilizados
Cuando un actor está desactivado, se libera el objeto de actor de toohello de referencias y puede ser recolectado normalmente por el recolector de elementos no utilizados de java virtual machine (JVM) u Hola common language runtime (CLR). Recolección de elementos solo limpia los objetos de actor Hola; lo hace **no** quitar estado almacenado en el Administrador de estado del actor Hola. actor de Hello siguiente tiempo Hola se activa, se crea un nuevo objeto de actor y se restaura su estado.

¿Qué se considera "se usa?" a fin de Hola de desactivación y recolección de elementos?

* Se recibe una llamada.
* `IRemindable.ReceiveReminderAsync`método que se invoca (se aplica solo si actor hello usa recordatorios)

> [!NOTE]
> Si actor Hola utiliza temporizadores y se invoca la devolución de llamada de temporizador, lo hace **no** recuento como "se usa?".
>
>

Antes de entrar en detalles de Hola de desactivación, es hello toodefine importante términos siguientes:

* *Intervalo de detección*. Esto es en qué Hola actores en tiempo de ejecución examina su tabla actores Active actores que pueden desactivar el intervalo de saludo y el recolector. Hola valor predeterminado es 1 minuto.
* *Tiempo de espera de inactividad*. Es Hola cantidad de tiempo que un actor requiere tooremain sin usar (inactivo) antes de que se puede desactivar y el recolector. Hola valor predeterminado es 60 minutos.

Por lo general, no es necesario toochange estos valores predeterminados. Sin embargo, si es necesario, estos intervalos pueden cambiarse mediante `ActorServiceSettings` al registrar el [servicio de actor](service-fabric-reliable-actors-platform.md):

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
Para cada actor activa, en tiempo de ejecución de hello actor realiza un seguimiento de hello cantidad de tiempo que ha estado inactivo (es decir, no se utiliza). tiempo de ejecución de Hello actor comprueba cada uno de los actores de hello cada `ScanIntervalInSeconds` toosee si es posible de elementos no utilizados se recopilan y se recopila, si ha estado inactiva durante `IdleTimeoutInSeconds`.

Cada vez que se usa un actor, su tiempo de inactividad es too0 de restablecimiento. Después de esto, actor Hola puede recopilarán sólo si nuevo permanece inactiva durante `IdleTimeoutInSeconds`. Recuerde que un actor se considera toohave sido usa si se ejecuta un método de interfaz de actor o una devolución de llamada de aviso de actor. Un actor está **no** considera toohave sido usa si se ejecuta su devolución de llamada de temporizador.

Hello siguiente diagrama muestra hello ciclo de vida de un actor único tooillustrate estos conceptos.

![Ejemplo de tiempo de inactividad][1]

ejemplo de Hola muestra impacto Hola de llamadas al método actor, avisos y temporizadores en duración de Hola de este actor. Hola siguientes puntos acerca de ejemplo de Hola merece la pena comentar:

* ScanInterval IdleTimeout se establecen y too5 y 10 respectivamente. (Unidades no importa en este caso, puesto que nuestro objetivo es solo el concepto de hello tooillustrate.)
* examen de Hola para actores toobe recolección se produce en T = 0, 5, 10, 15, 20, 25, tal como se define por intervalo de recorrido de saludo de 5.
* Un temporizador periódico se activa en T=4,8,12,16,20,24 y se ejecuta su devolución de llamada. No afecta a tiempo de inactividad de Hola de actor Hola.
* Una llamada al método de actor en T = 7 restablece too0 de tiempo de inactividad de Hola y retrasa la recolección de elementos Hola de actor Hola.
* Ejecuta una devolución de llamada de aviso de actor en T = 14 y más retrasos Hola recolección de actor Hola.
* Durante el análisis de recopilación de elementos no utilizados de hello en T = 25, tiempo de inactividad del actor Hola finalmente supera el tiempo de inactividad de Hola de 10 y actor hello es recolectado.

Un actor nunca se recolectará como elemento no utilizado mientras se ejecuta uno de sus métodos, independientemente del tiempo que se dedique a la ejecución de ese método. Tal y como se mencionó anteriormente, ejecución de Hola de métodos de interfaz de actor y las devoluciones de llamada de recordatorio impide la recolección mediante el restablecimiento too0 de tiempo de inactividad del actor hello. ejecución de Hola de devoluciones de llamada de temporizador no restablece hello too0 de tiempo de inactividad. Sin embargo, recolección de elementos Hola de actor Hola se aplaza hasta que devolución de llamada de temporizador de hello ha completado su ejecución.

## <a name="deleting-actors-and-their-state"></a>Eliminación de actores y su estado
Recolección de elementos de actores desactivados solo limpia los objetos de actor hello, pero no elimina los datos que se almacenan en el Administrador de estado de un actor. Cuando se vuelva a activar un actor, sus datos se efectúa tooit disponible a través de hello Administrador de Estados. En casos donde actores almacenar datos en el Administrador de estado y se desactiva pero nunca se vuelve a activar, puede ser necesario tooclean sus datos.

Hola [servicio de Actor](service-fabric-reliable-actors-platform.md) proporciona una función para eliminar los actores de un llamador remoto:

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

La eliminación de un actor tendrá Hola después efectos dependiendo de si o no está activo actualmente actor hello:

* **Actor activo**
  * El actor se quita de la lista de actores activos y se desactiva.
  * Su estado se elimina permanentemente.
* **Actor inactivo**
  * Su estado se elimina permanentemente.

Tenga en cuenta que no puede llamar un actor eliminar por sí sola desde uno de sus métodos de actor porque actor hello no se puede eliminar mientras se ejecuta dentro de un contexto de llamada de actor en qué hello en tiempo de ejecución ha obtenido un bloqueo alrededor de un único subproceso acceso de la llamada a tooenforce Hola actor.

## <a name="next-steps"></a>Pasos siguientes
* [Recordatorios y temporizadores de los actores](service-fabric-reliable-actors-timers-reminders.md)
* [Eventos de actor](service-fabric-reliable-actors-events.md)
* [Reentrada de actor](service-fabric-reliable-actors-reentrancy.md)
* [Supervisión del rendimiento y diagnósticos de los actores](service-fabric-reliable-actors-diagnostics.md)
* [Documentación de referencia de la API de actor](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Código de ejemplo de C#](https://github.com/Azure/servicefabric-samples)
* [Código de ejemplo de Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
