---
title: aaaPolymorphism en el marco de trabajo de hello Reliable Actors | Documentos de Microsoft
description: "Crear jerarquías de interfaces de .NET y tipos de funcionalidad de Reliable Actors framework tooreuse hello y definiciones de API."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>Polimorfismo en el marco de trabajo de hello Reliable Actors
Hola Reliable Actors marco de trabajo permite actores toobuild utilizando numerosos Hola mismas técnicas que le gustaría usar en diseño orientado a objetos. Una de estas técnicas es polimorfismo, que permite que los tipos e interfaces tooinherit de más generalizada elementos primarios. Herencia en el marco de trabajo de hello Reliable Actors generalmente sigue el modelo de .NET de hello con algunas restricciones adicionales. En el caso de Java/Linux, sigue modelo de Java de Hola.

## <a name="interfaces"></a>Interfaces
el marco de trabajo de Hello Reliable Actors requiere toodefine toobe al menos una interfaz implementada por el tipo de actor. Esta interfaz es toogenerate usa una clase de proxy que puede usarse en los clientes toocommunicate con los actores. Las interfaces pueden heredar elementos de otras interfaces, siempre y cuando todas las implementadas por un tipo de actor y todos sus elementos principales deriven de IActor(C#) o Actor(Java) en última instancia. IActor(C#) y Actor(Java) son interfaces base definido por la plataforma de Hola para actores en marcos de hello .NET y Java respectivamente. Por lo tanto, ejemplo de Hola polimorfismo clásico utilizando formas sería algo parecido a esto:

![Jerarquía de la interfaz de los actores de forma][shapes-interface-hierarchy]

## <a name="types"></a>Tipos
También puede crear una jerarquía de tipos de actor, que se derivan de la clase base de hello Actor que proporciona la plataforma de Hola. En caso de hello de formas, es posible que tenga una base de `Shape`(C#) o `ShapeImpl`tipo (Java):

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

Subtipos de `Shape`(C#) o `ShapeImpl`(Java) puede invalidar los métodos de hello base.

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

Hola Nota `ActorService` atributo en el tipo de actor Hola. Este atributo indica el marco de trabajo de hello Actor confiable que debe crear automáticamente un servicio de hospedaje actores de este tipo. En algunos casos, puede que quieran toocreate un tipo base que está pensado únicamente para la funcionalidad de uso compartido con subtipos y nunca será tooinstantiate usado actores concretas. En esos casos, debe usar hello `abstract` tooindicate de palabra clave que no se va a crear nunca un actor basado en ese tipo.

## <a name="next-steps"></a>Pasos siguientes
* Vea [cómo el marco de trabajo de hello Reliable Actors aprovecha la plataforma Service Fabric de hello](service-fabric-reliable-actors-platform.md) tooprovide confiabilidad, escalabilidad y el estado coherente.
* Obtenga información acerca de hello [ciclo de vida de actor](service-fabric-reliable-actors-lifecycle.md).

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
