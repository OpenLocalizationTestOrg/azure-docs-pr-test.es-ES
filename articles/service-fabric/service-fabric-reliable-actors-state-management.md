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
# <a name="reliable-actors-state-management"></a>Administración de estado de Reliable Actors
Reliable Actors son objetos uniproceso que encapsulan la lógica y el estado. Como actores se ejecutan en servicios de confianza, mantener el estado de forma confiable mediante el uso de Hola los mismos mecanismos de persistencia y la replicación que usa servicios de confianza. De esta manera, actores no pierdan su estado después de los errores al realizar la reactivación después de la recolección de elementos, o cuando se mueven entre los nodos de un clúster de vencimiento tooresource equilibrio o las actualizaciones.

## <a name="state-persistence-and-replication"></a>Persistencia y replicación del estado
Todos los actores confiable se consideran *stateful* dado que cada instancia de actor asigna tooa Id. único. Esto significa que toohello llamadas repetidas son el mismo Id. de actor enruta toohello misma instancia de actor. En un sistema sin estado, por el contrario, el cliente llama no se garantiza que toobe enrutado toohello mismo servidor cada vez. Por este motivo, los servicios de actor siempre son servicios con estado.

Aunque los actores se consideran con estado, no significa que deben almacenar el estado de manera confiable. Actores pueden elegir el nivel de Hola de persistencia de estado y la replicación basada en sus datos requisitos de almacenamiento:

* **Un estado persistente**: estado persistente toodisk y es too3 replicada o varias réplicas. Esto es opción de almacenamiento de estado más duradero hello, donde puede conservar el estado a través de la interrupción de todo el clúster.
* **Estado volátil**: el estado es too3 replicada o varias réplicas y solo se mantiene en la memoria. Esto proporciona resistencia frente a errores de nodo, errores de actores y durante las actualizaciones y el equilibrio de recursos. Sin embargo, el estado no es persistente toodisk. Por lo que si todas las réplicas se pierden al mismo tiempo, estado de hello también se pierde.
* **Ningún estado persistente**: estado no se replican o se escribe toodisk. Este nivel es de actores que simplemente no tienen estado toomaintain forma confiable.

Cada nivel de persistencia es simplemente otra configuración del *proveedor de estado* y de la *replicación* del servicio. Si no se escribe el estado toodisk depende de proveedor de estado de hello--componente hello en un servicio confiable que almacena el estado. La replicación depende de con cuántas réplicas se ha implementado un servicio. Al igual que con los servicios de confianza, ambos Hola proveedor de estado y número de réplicas puede ajustar fácilmente manualmente. el marco de trabajo de Hello actor proporciona un atributo que, cuando se utiliza en un actor, automáticamente se selecciona un proveedor de estado de forma predeterminada y se genera automáticamente la configuración de réplica recuento tooachieve uno de estos tres valores de persistencia. atributo de StatePersistence de Hello no es heredado por una clase derivada, cada tipo de Actor debe proporcionar su nivel de StatePersistence.

### <a name="persisted-state"></a>Estado persistente
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
Esta configuración usa un proveedor de estado que almacena los datos en disco y establece automáticamente Hola servicio réplica recuento too3.

### <a name="volatile-state"></a>Estado volátil
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
Esta configuración usa un proveedor de estado de solo en memoria y conjuntos de Hola too3 de recuento de réplica.

### <a name="no-persisted-state"></a>Sin estado persistente
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
Esta configuración usa un proveedor de estado de solo en memoria y conjuntos de Hola too1 de recuento de réplica.

### <a name="defaults-and-generated-settings"></a>Valores predeterminados y configuración generada
Cuando usas hello `StatePersistence` atributo, un proveedor de estado se selecciona automáticamente en tiempo de ejecución cuando se inicia el servicio de actor Hola. número de réplicas de Hello, sin embargo, se establece en tiempo de compilación por hello actor de Visual Studio herramientas de compilación. Hello herramientas de compilación generan automáticamente un *servicio predeterminado* para servicio de actor hello en ApplicationManifest.xml. Los parámetros se crean para **min replica set size** y **target replica set size**.

Puede cambiar estos parámetros manualmente. Pero cada Hola tiempo `StatePersistence` se cambia el atributo, parámetros de Hola se establecen los valores de tamaño de conjunto de réplica de toohello predeterminados para hello seleccionado `StatePersistence` atributos, reemplazar los valores anteriores. En otras palabras, son valores de hello que establezca en ServiceManifest.xml *sólo* se reemplaza en tiempo de compilación cuando cambia hello `StatePersistence` valor de atributo.

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

## <a name="state-manager"></a>Administrador de estado
Cada instancia de actor tiene su propio administrador de estado: una estructura de datos similar a un diccionario que almacena de manera confiable los pares clave-valor. Administrador de Estados de Hello es un contenedor alrededor de un proveedor de estado. Puede usar lo toostore datos sin tener en cuenta qué configuración de persistencia se utiliza. No se proporciona ninguna garantía de que un servicio en ejecución actor puede cambiarse desde un tooa de configuración de estado volátil (en memoria-solo) conserva la configuración de estado a través de una actualización gradual y conservan los datos. Sin embargo, es posible toochange recuento de réplica para un servicio en ejecución.

Las claves del administrador de estado deben ser cadenas. Los valores son genéricos y pueden ser de cualquier tipo, incluidos los tipos personalizados. Valores almacenados en el Administrador de estado de hello deben ser serializable de contrato de datos porque se puede transmitir a través de nodos de la red tooother Hola durante la replicación y puede escribirse toodisk, dependiendo de la configuración de persistencia de estado de un actor.

Administrador de Estados de Hello expone los métodos de diccionario comunes para administrar el estado, similar toothose que se encuentra en el diccionario de confianza.

### <a name="accessing-state"></a>Acceso al estado
Estado puede tener acceso a través del Administrador de estado de Hola por clave. Los métodos del administrador de estado son completamente asincrónicos, ya que pueden requerir una E/S de disco cuando los actores tienen un estado persistente. Después del primer acceso, los objetos de estado se almacenan en caché en la memoria. Las operaciones de acceso repetidas acceden a los objetos directamente desde la memoria y devuelven sincrónicamente sin incurrir en la sobrecarga de intercambio de contexto asincrónico o de E/S de disco. Se quita un objeto de estado de caché de Hola Hola casos siguientes:

* Un método de actor inicia una excepción no controlada después de que recupera un objeto de administrador de Estados de Hola.
* Un actor se vuelve a activar después de haberse desactivado o después de un error.
* páginas de proveedor de estado de Hello estado toodisk. Este comportamiento depende de la implementación del proveedor de estado de Hola. proveedor de estado predeterminado de Hola para hello `Persisted` tiene este comportamiento.

Puede recuperar el estado mediante el uso de un estándar *obtener* operación que produce `KeyNotFoundException`(C#) o `NoSuchElementException`(Java) si no existe una entrada para la clave de hello:

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

El estado también se puede recuperar mediante un método *TryGet* que no se inicia si no existe ninguna entrada para una clave:

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

### <a name="saving-state"></a>Almacenamiento del estado
métodos de recuperación de administrador de estado de Hello devuelven un objeto de tooan de referencia en la memoria local. Modificar este objeto en la memoria local por sí sola no hace que éste toobe guarda de manera duradera. Cuando un objeto se recupera del Administrador de Estados de Hola y modificado, se debe volver a en hello estado manager toobe guarda de manera duradera.

Puede insertar el estado mediante el uso de un incondicional *establecer*, que es Hola equivalente de hello `dictionary["key"] = value` sintaxis:

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

Puede agregar el estado mediante un método *Add*. Este método produce `InvalidOperationException`(C#) o `IllegalStateException`(Java) cuando intente tooadd una clave que ya existe.

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

También puede agregar el estado mediante un método *TryAdd*. Este método no se produce al intentar tooadd una clave que ya existe.

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

Al final de Hola de un método de actor, Administrador de Estados de hello guarda automáticamente los valores que se han agregado o modificado por una operación insert o update. Un proceso de "Guardar" puede incluir toodisk conservar y replicación, según los valores de hello utilizados. Los valores que no se han modificado no se conservan ni se replican. Si no se ha modificado ningún valor, Hola operación de guardar no hace nada. Si se produce un error en Guardar, hello estado modificado se descarta y se vuelve a cargar el estado original de Hola.

También puede guardar estado por llamada hello `SaveStateAsync` método en actor Hola base:

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

### <a name="removing-state"></a>Eliminación del estado
Puede quitar permanentemente estado desde el Administrador de estado de un actor por llamada hello *quitar* método. Este método produce `KeyNotFoundException`(C#) o `NoSuchElementException`(Java) cuando intente tooremove una clave que no existe.

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

También puede quitar estado permanentemente mediante hello *TryRemove* método. Este método no se produce al intentar tooremove una clave que no existe.

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

## <a name="next-steps"></a>Pasos siguientes

Estado que se almacena en Reliable Actors debe ser serializado antes de su toodisk escrito y replican para lograr alta disponibilidad. Aprenda más sobre la [serialización del tipo de actor](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

A continuación, aprenda más en [Supervisión del rendimiento y diagnósticos de los actores](service-fabric-reliable-actors-diagnostics.md).
