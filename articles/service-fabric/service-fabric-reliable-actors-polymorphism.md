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
# <a name="polymorphism-in-hello-reliable-actors-framework"></a><span data-ttu-id="195e8-103">Polimorfismo en el marco de trabajo de hello Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="195e8-103">Polymorphism in hello Reliable Actors framework</span></span>
<span data-ttu-id="195e8-104">Hola Reliable Actors marco de trabajo permite actores toobuild utilizando numerosos Hola mismas técnicas que le gustaría usar en diseño orientado a objetos.</span><span class="sxs-lookup"><span data-stu-id="195e8-104">hello Reliable Actors framework allows you toobuild actors using many of hello same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="195e8-105">Una de estas técnicas es polimorfismo, que permite que los tipos e interfaces tooinherit de más generalizada elementos primarios.</span><span class="sxs-lookup"><span data-stu-id="195e8-105">One of those techniques is polymorphism, which allows types and interfaces tooinherit from more generalized parents.</span></span> <span data-ttu-id="195e8-106">Herencia en el marco de trabajo de hello Reliable Actors generalmente sigue el modelo de .NET de hello con algunas restricciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="195e8-106">Inheritance in hello Reliable Actors framework generally follows hello .NET model with a few additional constraints.</span></span> <span data-ttu-id="195e8-107">En el caso de Java/Linux, sigue modelo de Java de Hola.</span><span class="sxs-lookup"><span data-stu-id="195e8-107">In case of Java/Linux, it follows hello Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="195e8-108">Interfaces</span><span class="sxs-lookup"><span data-stu-id="195e8-108">Interfaces</span></span>
<span data-ttu-id="195e8-109">el marco de trabajo de Hello Reliable Actors requiere toodefine toobe al menos una interfaz implementada por el tipo de actor.</span><span class="sxs-lookup"><span data-stu-id="195e8-109">hello Reliable Actors framework requires you toodefine at least one interface toobe implemented by your actor type.</span></span> <span data-ttu-id="195e8-110">Esta interfaz es toogenerate usa una clase de proxy que puede usarse en los clientes toocommunicate con los actores.</span><span class="sxs-lookup"><span data-stu-id="195e8-110">This interface is used toogenerate a proxy class that can be used by clients toocommunicate with your actors.</span></span> <span data-ttu-id="195e8-111">Las interfaces pueden heredar elementos de otras interfaces, siempre y cuando todas las implementadas por un tipo de actor y todos sus elementos principales deriven de IActor(C#) o Actor(Java) en última instancia.</span><span class="sxs-lookup"><span data-stu-id="195e8-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="195e8-112">IActor(C#) y Actor(Java) son interfaces base definido por la plataforma de Hola para actores en marcos de hello .NET y Java respectivamente.</span><span class="sxs-lookup"><span data-stu-id="195e8-112">IActor(C#) and Actor(Java) are hello platform-defined base interfaces for actors in hello frameworks .NET and Java respectively.</span></span> <span data-ttu-id="195e8-113">Por lo tanto, ejemplo de Hola polimorfismo clásico utilizando formas sería algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="195e8-113">Thus, hello classic polymorphism example using shapes might look something like this:</span></span>

![Jerarquía de la interfaz de los actores de forma][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="195e8-115">Tipos</span><span class="sxs-lookup"><span data-stu-id="195e8-115">Types</span></span>
<span data-ttu-id="195e8-116">También puede crear una jerarquía de tipos de actor, que se derivan de la clase base de hello Actor que proporciona la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="195e8-116">You can also create a hierarchy of actor types, which are derived from hello base Actor class that is provided by hello platform.</span></span> <span data-ttu-id="195e8-117">En caso de hello de formas, es posible que tenga una base de `Shape`(C#) o `ShapeImpl`tipo (Java):</span><span class="sxs-lookup"><span data-stu-id="195e8-117">In hello case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="195e8-118">Subtipos de `Shape`(C#) o `ShapeImpl`(Java) puede invalidar los métodos de hello base.</span><span class="sxs-lookup"><span data-stu-id="195e8-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from hello base.</span></span>

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

<span data-ttu-id="195e8-119">Hola Nota `ActorService` atributo en el tipo de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="195e8-119">Note hello `ActorService` attribute on hello actor type.</span></span> <span data-ttu-id="195e8-120">Este atributo indica el marco de trabajo de hello Actor confiable que debe crear automáticamente un servicio de hospedaje actores de este tipo.</span><span class="sxs-lookup"><span data-stu-id="195e8-120">This attribute tells hello Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="195e8-121">En algunos casos, puede que quieran toocreate un tipo base que está pensado únicamente para la funcionalidad de uso compartido con subtipos y nunca será tooinstantiate usado actores concretas.</span><span class="sxs-lookup"><span data-stu-id="195e8-121">In some cases, you may wish toocreate a base type that is solely intended for sharing functionality with subtypes and will never be used tooinstantiate concrete actors.</span></span> <span data-ttu-id="195e8-122">En esos casos, debe usar hello `abstract` tooindicate de palabra clave que no se va a crear nunca un actor basado en ese tipo.</span><span class="sxs-lookup"><span data-stu-id="195e8-122">In those cases, you should use hello `abstract` keyword tooindicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="195e8-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="195e8-123">Next steps</span></span>
* <span data-ttu-id="195e8-124">Vea [cómo el marco de trabajo de hello Reliable Actors aprovecha la plataforma Service Fabric de hello](service-fabric-reliable-actors-platform.md) tooprovide confiabilidad, escalabilidad y el estado coherente.</span><span class="sxs-lookup"><span data-stu-id="195e8-124">See [how hello Reliable Actors framework leverages hello Service Fabric platform](service-fabric-reliable-actors-platform.md) tooprovide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="195e8-125">Obtenga información acerca de hello [ciclo de vida de actor](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="195e8-125">Learn about hello [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
