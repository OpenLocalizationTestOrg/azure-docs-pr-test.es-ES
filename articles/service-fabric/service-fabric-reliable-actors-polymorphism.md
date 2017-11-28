---
title: Polimorfismo en el marco de Reliable Actors | Microsoft Docs
description: "Cree jerarquías de tipos e interfaces de .NET en el marco de trabajo de Reliable Actors para volver a usar la funcionalidad y las definiciones de la API."
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
ms.openlocfilehash: 36a59a41b2261369a2062c76ef90aebf7e24a221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="polymorphism-in-the-reliable-actors-framework"></a><span data-ttu-id="fbf80-103">Polimorfismo en el marco de trabajo de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="fbf80-103">Polymorphism in the Reliable Actors framework</span></span>
<span data-ttu-id="fbf80-104">El marco de Reliable Actors permite compilar actores empleando muchas de las mismas técnicas que usaría en el diseño orientado a objetos.</span><span class="sxs-lookup"><span data-stu-id="fbf80-104">The Reliable Actors framework allows you to build actors using many of the same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="fbf80-105">Una de esas técnicas es el polimorfismo, que los tipos y las interfaces hereden de elementos primarios más generalizados.</span><span class="sxs-lookup"><span data-stu-id="fbf80-105">One of those techniques is polymorphism, which allows types and interfaces to inherit from more generalized parents.</span></span> <span data-ttu-id="fbf80-106">La herencia en el marco de Reliable Actors suele seguir el modelo de .NET con algunas restricciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="fbf80-106">Inheritance in the Reliable Actors framework generally follows the .NET model with a few additional constraints.</span></span> <span data-ttu-id="fbf80-107">En el caso de Java/Linux, sigue el modelo de Java.</span><span class="sxs-lookup"><span data-stu-id="fbf80-107">In case of Java/Linux, it follows the Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="fbf80-108">Interfaces</span><span class="sxs-lookup"><span data-stu-id="fbf80-108">Interfaces</span></span>
<span data-ttu-id="fbf80-109">El marco Reliable Actors requiere la definición de al menos una interfaz que se implementará por el tipo de actor.</span><span class="sxs-lookup"><span data-stu-id="fbf80-109">The Reliable Actors framework requires you to define at least one interface to be implemented by your actor type.</span></span> <span data-ttu-id="fbf80-110">Esta interfaz se usa para generar una clase de proxy que se puede usar por los clientes para comunicarse con los actores.</span><span class="sxs-lookup"><span data-stu-id="fbf80-110">This interface is used to generate a proxy class that can be used by clients to communicate with your actors.</span></span> <span data-ttu-id="fbf80-111">Las interfaces pueden heredar elementos de otras interfaces, siempre y cuando todas las implementadas por un tipo de actor y todos sus elementos principales deriven de IActor(C#) o Actor(Java) en última instancia.</span><span class="sxs-lookup"><span data-stu-id="fbf80-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="fbf80-112">IActor(C#) y Actor(Java) son las interfaces base definidas por plataforma destinadas a actores en .NET Framework y en la plataforma Java, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="fbf80-112">IActor(C#) and Actor(Java) are the platform-defined base interfaces for actors in the frameworks .NET and Java respectively.</span></span> <span data-ttu-id="fbf80-113">Así, el ejemplo clásico de polimorfismo en el que se usan formas sería algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbf80-113">Thus, the classic polymorphism example using shapes might look something like this:</span></span>

![Jerarquía de la interfaz de los actores de forma][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="fbf80-115">Tipos</span><span class="sxs-lookup"><span data-stu-id="fbf80-115">Types</span></span>
<span data-ttu-id="fbf80-116">También puede crear una jerarquía de tipos de actores, que se derivan de la clase Actor base proporcionada por la plataforma.</span><span class="sxs-lookup"><span data-stu-id="fbf80-116">You can also create a hierarchy of actor types, which are derived from the base Actor class that is provided by the platform.</span></span> <span data-ttu-id="fbf80-117">En el caso de las formas, es posible tener un tipo base `Shape`(C#) o `ShapeImpl`(Java):</span><span class="sxs-lookup"><span data-stu-id="fbf80-117">In the case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="fbf80-118">Los subtipos de `Shape`(C#) o `ShapeImpl`(Java) pueden invalidar métodos del tipo base.</span><span class="sxs-lookup"><span data-stu-id="fbf80-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from the base.</span></span>

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

<span data-ttu-id="fbf80-119">Observe el atributo `ActorService` en el tipo de actor.</span><span class="sxs-lookup"><span data-stu-id="fbf80-119">Note the `ActorService` attribute on the actor type.</span></span> <span data-ttu-id="fbf80-120">Este atributo indica al marco de Reliable Actors que debe crear automáticamente un servicio para hospedar actores de este tipo.</span><span class="sxs-lookup"><span data-stu-id="fbf80-120">This attribute tells the Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="fbf80-121">En algunos casos, quizás quiera crear un tipo base que esté pensado únicamente para compartir la funcionalidad con subtipos y que nunca se usará para crear instancias de actores concretos.</span><span class="sxs-lookup"><span data-stu-id="fbf80-121">In some cases, you may wish to create a base type that is solely intended for sharing functionality with subtypes and will never be used to instantiate concrete actors.</span></span> <span data-ttu-id="fbf80-122">En esos casos, debe usar la palabra clave `abstract` para indicar que nunca va a crear un actor basado en ese tipo.</span><span class="sxs-lookup"><span data-stu-id="fbf80-122">In those cases, you should use the `abstract` keyword to indicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbf80-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fbf80-123">Next steps</span></span>
* <span data-ttu-id="fbf80-124">Consulte [cómo el marco de trabajo de Reliable Actors aprovecha la plataforma de Service Fabric](service-fabric-reliable-actors-platform.md) para ofrecer confiabilidad, escalabilidad y un estado coherente.</span><span class="sxs-lookup"><span data-stu-id="fbf80-124">See [how the Reliable Actors framework leverages the Service Fabric platform](service-fabric-reliable-actors-platform.md) to provide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="fbf80-125">Obtenga información sobre el [ciclo de vida de los actores](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="fbf80-125">Learn about the [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
