---
title: "administración de Estados de los actores aaaReliable | Documentos de Microsoft"
description: "Describe cómo se administra, se conserva y se replica el estado de Reliable Actors para alta disponibilidad."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="f3c53-103">Administración de estado de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="f3c53-103">Reliable Actors state management</span></span>
<span data-ttu-id="f3c53-104">Reliable Actors son objetos uniproceso que encapsulan la lógica y el estado.</span><span class="sxs-lookup"><span data-stu-id="f3c53-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="f3c53-105">Como actores se ejecutan en servicios de confianza, mantener el estado de forma confiable mediante el uso de Hola los mismos mecanismos de persistencia y la replicación que usa servicios de confianza.</span><span class="sxs-lookup"><span data-stu-id="f3c53-105">Because actors run on Reliable Services, they can maintain state reliably by using hello same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="f3c53-106">De esta manera, actores no pierdan su estado después de los errores al realizar la reactivación después de la recolección de elementos, o cuando se mueven entre los nodos de un clúster de vencimiento tooresource equilibrio o las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="f3c53-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due tooresource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="f3c53-107">Persistencia y replicación del estado</span><span class="sxs-lookup"><span data-stu-id="f3c53-107">State persistence and replication</span></span>
<span data-ttu-id="f3c53-108">Todos los actores confiable se consideran *stateful* dado que cada instancia de actor asigna tooa Id. único.</span><span class="sxs-lookup"><span data-stu-id="f3c53-108">All Reliable Actors are considered *stateful* because each actor instance maps tooa unique ID.</span></span> <span data-ttu-id="f3c53-109">Esto significa que toohello llamadas repetidas son el mismo Id. de actor enruta toohello misma instancia de actor.</span><span class="sxs-lookup"><span data-stu-id="f3c53-109">This means that repeated calls toohello same actor ID are routed toohello same actor instance.</span></span> <span data-ttu-id="f3c53-110">En un sistema sin estado, por el contrario, el cliente llama no se garantiza que toobe enrutado toohello mismo servidor cada vez.</span><span class="sxs-lookup"><span data-stu-id="f3c53-110">In a stateless system, by contrast, client calls are not guaranteed toobe routed toohello same server every time.</span></span> <span data-ttu-id="f3c53-111">Por este motivo, los servicios de actor siempre son servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="f3c53-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="f3c53-112">Aunque los actores se consideran con estado, no significa que deben almacenar el estado de manera confiable.</span><span class="sxs-lookup"><span data-stu-id="f3c53-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="f3c53-113">Actores pueden elegir el nivel de Hola de persistencia de estado y la replicación basada en sus datos requisitos de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="f3c53-113">Actors can choose hello level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="f3c53-114">**Un estado persistente**: estado persistente toodisk y es too3 replicada o varias réplicas.</span><span class="sxs-lookup"><span data-stu-id="f3c53-114">**Persisted state**: State is persisted toodisk and is replicated too3 or more replicas.</span></span> <span data-ttu-id="f3c53-115">Esto es opción de almacenamiento de estado más duradero hello, donde puede conservar el estado a través de la interrupción de todo el clúster.</span><span class="sxs-lookup"><span data-stu-id="f3c53-115">This is hello most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="f3c53-116">**Estado volátil**: el estado es too3 replicada o varias réplicas y solo se mantiene en la memoria.</span><span class="sxs-lookup"><span data-stu-id="f3c53-116">**Volatile state**: State is replicated too3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="f3c53-117">Esto proporciona resistencia frente a errores de nodo, errores de actores y durante las actualizaciones y el equilibrio de recursos.</span><span class="sxs-lookup"><span data-stu-id="f3c53-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="f3c53-118">Sin embargo, el estado no es persistente toodisk.</span><span class="sxs-lookup"><span data-stu-id="f3c53-118">However, state is not persisted toodisk.</span></span> <span data-ttu-id="f3c53-119">Por lo que si todas las réplicas se pierden al mismo tiempo, estado de hello también se pierde.</span><span class="sxs-lookup"><span data-stu-id="f3c53-119">So if all replicas are lost at once, hello state is lost as well.</span></span>
* <span data-ttu-id="f3c53-120">**Ningún estado persistente**: estado no se replican o se escribe toodisk.</span><span class="sxs-lookup"><span data-stu-id="f3c53-120">**No persisted state**: State is not replicated or written toodisk.</span></span> <span data-ttu-id="f3c53-121">Este nivel es de actores que simplemente no tienen estado toomaintain forma confiable.</span><span class="sxs-lookup"><span data-stu-id="f3c53-121">This level is for actors that simply don't need toomaintain state reliably.</span></span>

<span data-ttu-id="f3c53-122">Cada nivel de persistencia es simplemente otra configuración del *proveedor de estado* y de la *replicación* del servicio.</span><span class="sxs-lookup"><span data-stu-id="f3c53-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="f3c53-123">Si no se escribe el estado toodisk depende de proveedor de estado de hello--componente hello en un servicio confiable que almacena el estado.</span><span class="sxs-lookup"><span data-stu-id="f3c53-123">Whether or not state is written toodisk depends on hello state provider--hello component in a reliable service that stores state.</span></span> <span data-ttu-id="f3c53-124">La replicación depende de con cuántas réplicas se ha implementado un servicio.</span><span class="sxs-lookup"><span data-stu-id="f3c53-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="f3c53-125">Al igual que con los servicios de confianza, ambos Hola proveedor de estado y número de réplicas puede ajustar fácilmente manualmente.</span><span class="sxs-lookup"><span data-stu-id="f3c53-125">As with Reliable Services, both hello state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="f3c53-126">el marco de trabajo de Hello actor proporciona un atributo que, cuando se utiliza en un actor, automáticamente se selecciona un proveedor de estado de forma predeterminada y se genera automáticamente la configuración de réplica recuento tooachieve uno de estos tres valores de persistencia.</span><span class="sxs-lookup"><span data-stu-id="f3c53-126">hello actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count tooachieve one of these three persistence settings.</span></span> <span data-ttu-id="f3c53-127">atributo de StatePersistence de Hello no es heredado por una clase derivada, cada tipo de Actor debe proporcionar su nivel de StatePersistence.</span><span class="sxs-lookup"><span data-stu-id="f3c53-127">hello StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="f3c53-128">Estado persistente</span><span class="sxs-lookup"><span data-stu-id="f3c53-128">Persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
<span data-ttu-id="f3c53-129">Esta configuración usa un proveedor de estado que almacena los datos en disco y establece automáticamente Hola servicio réplica recuento too3.</span><span class="sxs-lookup"><span data-stu-id="f3c53-129">This setting uses a state provider that stores data on disk and automatically sets hello service replica count too3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="f3c53-130">Estado volátil</span><span class="sxs-lookup"><span data-stu-id="f3c53-130">Volatile state</span></span>
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="f3c53-131">Esta configuración usa un proveedor de estado de solo en memoria y conjuntos de Hola too3 de recuento de réplica.</span><span class="sxs-lookup"><span data-stu-id="f3c53-131">This setting uses an in-memory-only state provider and sets hello replica count too3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="f3c53-132">Sin estado persistente</span><span class="sxs-lookup"><span data-stu-id="f3c53-132">No persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="f3c53-133">Esta configuración usa un proveedor de estado de solo en memoria y conjuntos de Hola too1 de recuento de réplica.</span><span class="sxs-lookup"><span data-stu-id="f3c53-133">This setting uses an in-memory-only state provider and sets hello replica count too1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="f3c53-134">Valores predeterminados y configuración generada</span><span class="sxs-lookup"><span data-stu-id="f3c53-134">Defaults and generated settings</span></span>
<span data-ttu-id="f3c53-135">Cuando usas hello `StatePersistence` atributo, un proveedor de estado se selecciona automáticamente en tiempo de ejecución cuando se inicia el servicio de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="f3c53-135">When you're using hello `StatePersistence` attribute, a state provider is automatically selected for you at runtime when hello actor service starts.</span></span> <span data-ttu-id="f3c53-136">número de réplicas de Hello, sin embargo, se establece en tiempo de compilación por hello actor de Visual Studio herramientas de compilación.</span><span class="sxs-lookup"><span data-stu-id="f3c53-136">hello replica count, however, is set at compile time by hello Visual Studio actor build tools.</span></span> <span data-ttu-id="f3c53-137">Hello herramientas de compilación generan automáticamente un *servicio predeterminado* para servicio de actor hello en ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="f3c53-137">hello build tools automatically generate a *default service* for hello actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="f3c53-138">Los parámetros se crean para **min replica set size** y **target replica set size**.</span><span class="sxs-lookup"><span data-stu-id="f3c53-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="f3c53-139">Puede cambiar estos parámetros manualmente.</span><span class="sxs-lookup"><span data-stu-id="f3c53-139">You can change these parameters manually.</span></span> <span data-ttu-id="f3c53-140">Pero cada Hola tiempo `StatePersistence` se cambia el atributo, parámetros de Hola se establecen los valores de tamaño de conjunto de réplica de toohello predeterminados para hello seleccionado `StatePersistence` atributos, reemplazar los valores anteriores.</span><span class="sxs-lookup"><span data-stu-id="f3c53-140">But each time hello `StatePersistence` attribute is changed, hello parameters are set toohello default replica set size values for hello selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="f3c53-141">En otras palabras, son valores de hello que establezca en ServiceManifest.xml *sólo* se reemplaza en tiempo de compilación cuando cambia hello `StatePersistence` valor de atributo.</span><span class="sxs-lookup"><span data-stu-id="f3c53-141">In other words, hello values that you set in ServiceManifest.xml are *only* overridden at build time when you change hello `StatePersistence` attribute value.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a><span data-ttu-id="f3c53-142">Administrador de estado</span><span class="sxs-lookup"><span data-stu-id="f3c53-142">State manager</span></span>
<span data-ttu-id="f3c53-143">Cada instancia de actor tiene su propio administrador de estado: una estructura de datos similar a un diccionario que almacena de manera confiable los pares clave-valor.</span><span class="sxs-lookup"><span data-stu-id="f3c53-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="f3c53-144">Administrador de Estados de Hello es un contenedor alrededor de un proveedor de estado.</span><span class="sxs-lookup"><span data-stu-id="f3c53-144">hello state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="f3c53-145">Puede usar lo toostore datos sin tener en cuenta qué configuración de persistencia se utiliza.</span><span class="sxs-lookup"><span data-stu-id="f3c53-145">You can use it toostore data regardless of which persistence setting is used.</span></span> <span data-ttu-id="f3c53-146">No se proporciona ninguna garantía de que un servicio en ejecución actor puede cambiarse desde un tooa de configuración de estado volátil (en memoria-solo) conserva la configuración de estado a través de una actualización gradual y conservan los datos.</span><span class="sxs-lookup"><span data-stu-id="f3c53-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting tooa persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="f3c53-147">Sin embargo, es posible toochange recuento de réplica para un servicio en ejecución.</span><span class="sxs-lookup"><span data-stu-id="f3c53-147">However, it is possible toochange replica count for a running service.</span></span>

<span data-ttu-id="f3c53-148">Las claves del administrador de estado deben ser cadenas.</span><span class="sxs-lookup"><span data-stu-id="f3c53-148">State manager keys must be strings.</span></span> <span data-ttu-id="f3c53-149">Los valores son genéricos y pueden ser de cualquier tipo, incluidos los tipos personalizados.</span><span class="sxs-lookup"><span data-stu-id="f3c53-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="f3c53-150">Valores almacenados en el Administrador de estado de hello deben ser serializable de contrato de datos porque se puede transmitir a través de nodos de la red tooother Hola durante la replicación y puede escribirse toodisk, dependiendo de la configuración de persistencia de estado de un actor.</span><span class="sxs-lookup"><span data-stu-id="f3c53-150">Values stored in hello state manager must be data contract serializable because they might be transmitted over hello network tooother nodes during replication and might be written toodisk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="f3c53-151">Administrador de Estados de Hello expone los métodos de diccionario comunes para administrar el estado, similar toothose que se encuentra en el diccionario de confianza.</span><span class="sxs-lookup"><span data-stu-id="f3c53-151">hello state manager exposes common dictionary methods for managing state, similar toothose found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="f3c53-152">Acceso al estado</span><span class="sxs-lookup"><span data-stu-id="f3c53-152">Accessing state</span></span>
<span data-ttu-id="f3c53-153">Estado puede tener acceso a través del Administrador de estado de Hola por clave.</span><span class="sxs-lookup"><span data-stu-id="f3c53-153">State can be accessed through hello state manager by key.</span></span> <span data-ttu-id="f3c53-154">Los métodos del administrador de estado son completamente asincrónicos, ya que pueden requerir una E/S de disco cuando los actores tienen un estado persistente.</span><span class="sxs-lookup"><span data-stu-id="f3c53-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="f3c53-155">Después del primer acceso, los objetos de estado se almacenan en caché en la memoria.</span><span class="sxs-lookup"><span data-stu-id="f3c53-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="f3c53-156">Las operaciones de acceso repetidas acceden a los objetos directamente desde la memoria y devuelven sincrónicamente sin incurrir en la sobrecarga de intercambio de contexto asincrónico o de E/S de disco.</span><span class="sxs-lookup"><span data-stu-id="f3c53-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="f3c53-157">Se quita un objeto de estado de caché de Hola Hola casos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f3c53-157">A state object is removed from hello cache in hello following cases:</span></span>

* <span data-ttu-id="f3c53-158">Un método de actor inicia una excepción no controlada después de que recupera un objeto de administrador de Estados de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3c53-158">An actor method throws an unhandled exception after it retrieves an object from hello state manager.</span></span>
* <span data-ttu-id="f3c53-159">Un actor se vuelve a activar después de haberse desactivado o después de un error.</span><span class="sxs-lookup"><span data-stu-id="f3c53-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="f3c53-160">páginas de proveedor de estado de Hello estado toodisk.</span><span class="sxs-lookup"><span data-stu-id="f3c53-160">hello state provider pages state toodisk.</span></span> <span data-ttu-id="f3c53-161">Este comportamiento depende de la implementación del proveedor de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3c53-161">This behavior depends on hello state provider implementation.</span></span> <span data-ttu-id="f3c53-162">proveedor de estado predeterminado de Hola para hello `Persisted` tiene este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="f3c53-162">hello default state provider for hello `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="f3c53-163">Puede recuperar el estado mediante el uso de un estándar *obtener* operación que produce `KeyNotFoundException`(C#) o `NoSuchElementException`(Java) si no existe una entrada para la clave de hello:</span><span class="sxs-lookup"><span data-stu-id="f3c53-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for hello key:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

<span data-ttu-id="f3c53-164">El estado también se puede recuperar mediante un método *TryGet* que no se inicia si no existe ninguna entrada para una clave:</span><span class="sxs-lookup"><span data-stu-id="f3c53-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a><span data-ttu-id="f3c53-165">Almacenamiento del estado</span><span class="sxs-lookup"><span data-stu-id="f3c53-165">Saving state</span></span>
<span data-ttu-id="f3c53-166">métodos de recuperación de administrador de estado de Hello devuelven un objeto de tooan de referencia en la memoria local.</span><span class="sxs-lookup"><span data-stu-id="f3c53-166">hello state manager retrieval methods return a reference tooan object in local memory.</span></span> <span data-ttu-id="f3c53-167">Modificar este objeto en la memoria local por sí sola no hace que éste toobe guarda de manera duradera.</span><span class="sxs-lookup"><span data-stu-id="f3c53-167">Modifying this object in local memory alone does not cause it toobe saved durably.</span></span> <span data-ttu-id="f3c53-168">Cuando un objeto se recupera del Administrador de Estados de Hola y modificado, se debe volver a en hello estado manager toobe guarda de manera duradera.</span><span class="sxs-lookup"><span data-stu-id="f3c53-168">When an object is retrieved from hello state manager and modified, it must be reinserted into hello state manager toobe saved durably.</span></span>

<span data-ttu-id="f3c53-169">Puede insertar el estado mediante el uso de un incondicional *establecer*, que es Hola equivalente de hello `dictionary["key"] = value` sintaxis:</span><span class="sxs-lookup"><span data-stu-id="f3c53-169">You can insert state by using an unconditional *Set*, which is hello equivalent of hello `dictionary["key"] = value` syntax:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

<span data-ttu-id="f3c53-170">Puede agregar el estado mediante un método *Add*.</span><span class="sxs-lookup"><span data-stu-id="f3c53-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="f3c53-171">Este método produce `InvalidOperationException`(C#) o `IllegalStateException`(Java) cuando intente tooadd una clave que ya existe.</span><span class="sxs-lookup"><span data-stu-id="f3c53-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries tooadd a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

<span data-ttu-id="f3c53-172">También puede agregar el estado mediante un método *TryAdd*.</span><span class="sxs-lookup"><span data-stu-id="f3c53-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="f3c53-173">Este método no se produce al intentar tooadd una clave que ya existe.</span><span class="sxs-lookup"><span data-stu-id="f3c53-173">This method does not throw when it tries tooadd a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

<span data-ttu-id="f3c53-174">Al final de Hola de un método de actor, Administrador de Estados de hello guarda automáticamente los valores que se han agregado o modificado por una operación insert o update.</span><span class="sxs-lookup"><span data-stu-id="f3c53-174">At hello end of an actor method, hello state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="f3c53-175">Un proceso de "Guardar" puede incluir toodisk conservar y replicación, según los valores de hello utilizados.</span><span class="sxs-lookup"><span data-stu-id="f3c53-175">A "save" can include persisting toodisk and replication, depending on hello settings used.</span></span> <span data-ttu-id="f3c53-176">Los valores que no se han modificado no se conservan ni se replican.</span><span class="sxs-lookup"><span data-stu-id="f3c53-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="f3c53-177">Si no se ha modificado ningún valor, Hola operación de guardar no hace nada.</span><span class="sxs-lookup"><span data-stu-id="f3c53-177">If no values have been modified, hello save operation does nothing.</span></span> <span data-ttu-id="f3c53-178">Si se produce un error en Guardar, hello estado modificado se descarta y se vuelve a cargar el estado original de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3c53-178">If saving fails, hello modified state is discarded and hello original state is reloaded.</span></span>

<span data-ttu-id="f3c53-179">También puede guardar estado por llamada hello `SaveStateAsync` método en actor Hola base:</span><span class="sxs-lookup"><span data-stu-id="f3c53-179">You can also save state manually by calling hello `SaveStateAsync` method on hello actor base:</span></span>

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a><span data-ttu-id="f3c53-180">Eliminación del estado</span><span class="sxs-lookup"><span data-stu-id="f3c53-180">Removing state</span></span>
<span data-ttu-id="f3c53-181">Puede quitar permanentemente estado desde el Administrador de estado de un actor por llamada hello *quitar* método.</span><span class="sxs-lookup"><span data-stu-id="f3c53-181">You can remove state permanently from an actor's state manager by calling hello *Remove* method.</span></span> <span data-ttu-id="f3c53-182">Este método produce `KeyNotFoundException`(C#) o `NoSuchElementException`(Java) cuando intente tooremove una clave que no existe.</span><span class="sxs-lookup"><span data-stu-id="f3c53-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries tooremove a key that doesn't exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

<span data-ttu-id="f3c53-183">También puede quitar estado permanentemente mediante hello *TryRemove* método.</span><span class="sxs-lookup"><span data-stu-id="f3c53-183">You can also remove state permanently by using hello *TryRemove* method.</span></span> <span data-ttu-id="f3c53-184">Este método no se produce al intentar tooremove una clave que no existe.</span><span class="sxs-lookup"><span data-stu-id="f3c53-184">This method does not throw when it tries tooremove a key that does not exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="f3c53-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3c53-185">Next steps</span></span>

<span data-ttu-id="f3c53-186">Estado que se almacena en Reliable Actors debe ser serializado antes de su toodisk escrito y replican para lograr alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f3c53-186">State that's stored in Reliable Actors must be serialized before its written toodisk and replicated for high availability.</span></span> <span data-ttu-id="f3c53-187">Aprenda más sobre la [serialización del tipo de actor](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="f3c53-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="f3c53-188">A continuación, aprenda más en [Supervisión del rendimiento y diagnósticos de los actores](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="f3c53-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
