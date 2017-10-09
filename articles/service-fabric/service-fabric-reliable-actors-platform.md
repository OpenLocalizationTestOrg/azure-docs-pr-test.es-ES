---
title: aaaReliable actores en Service Fabric | Documentos de Microsoft
description: "Describe cómo Reliable Actors están organizadas por niveles en los servicios de confianza y usar las características de Hola de plataforma de Service Fabric Hola."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a>Uso de Reliable Actors plataforma Service Fabric de Hola
Este artículo explica cómo funcionan los actores confiable en plataforma de Azure Service Fabric Hola. Actores confiables que se ejecutan en un marco de trabajo que se hospeda en una implementación de un servicio confiable con estado llamado hello *servicio de actor*. servicio de actor Hello contiene todos los ciclo de vida de hello componentes necesarios toomanage hello y un mensaje que envía para los actores:

* Hola en tiempo de ejecución de Actor administra el ciclo de vida, recolección de elementos y aplica el acceso de un único subproceso.
* Un agente de escucha de comunicación remota de servicio de actor acepta tooactors de llamadas de acceso remoto y los envía instancia de tooa distribuidor tooroute toohello actor adecuado.
* Hola proveedor de estado de Actor ajusta los proveedores de estado (por ejemplo, el proveedor de estado de hello colecciones confiable) y proporciona un adaptador para la administración de estado de actor.

Estos componentes forman juntos Hola Actor confiable marco de trabajo.

## <a name="service-layering"></a>Servicio en capas
Porque el propio servicio de actor hello es un servicio confiable, todos Hola [modelo de aplicación](service-fabric-application-model.md), ciclo de vida, [empaquetado](service-fabric-package-apps.md), [implementación](service-fabric-deploy-remove-applications.md), actualizar y ajuste de escala en conceptos de Servicios de confianza aplican Hola mismo tooactor manera en los servicios. 

![Servicio de actor en capas][1]

Hello diagrama anterior muestra hello relación entre marcos de aplicaciones de Service Fabric de Hola y el código de usuario. Elementos azul representan el marco de aplicación de servicios de confianza de hello, naranja representa el marco de trabajo de hello Actor confiable y verde representa código de usuario.

En servicios de confianza, el servicio hereda hello `StatefulService` clase. Esta clase deriva de `StatefulServiceBase`, o bien de `StatelessService` en el caso de los servicios sin estado. Servicio de actor Hola se utiliza en Reliable Actors. servicio de actor Hello es una implementación diferente de hello `StatefulServiceBase` clase ese patrón de actor implementa Hola donde ejecutan los actores. Porque el propio servicio de actor hello es simplemente una implementación de `StatefulServiceBase`, puede escribir su propio servicio que deriva de `ActorService` y características de nivel de servicio implemente Hola mismo tal como lo haría al heredar `StatefulService`, como:

* Copia de seguridad y restauración del servicio.
* Funcionalidad compartida para todos los actores, por ejemplo, un interruptor.
* Llamadas a procedimiento remoto en el propio servicio de actor hello y en cada actor individual.

> [!NOTE]
> Los servicios sin estado no son compatibles actualmente en Java/Linux.

### <a name="using-hello-actor-service"></a>Usar servicio de actor Hola
Instancias de actor tengan en el que se ejecuta el servicio de actor de toohello de acceso. A través del servicio de actor hello, instancias de actor mediante programación pueden obtener el contexto de servicio de Hola. contexto de servicio de Hello tiene Id. de partición de Hola, nombre del servicio, nombre de la aplicación y otra información específica de la plataforma de Service Fabric:

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


Al igual que todos los servicios de confianza, el servicio de actor de hello debe estar registrado con un tipo de servicio en tiempo de ejecución de hello Service Fabric. Para servicio de actor de hello toorun las instancias del actor, el tipo de actor también debe registrarse con el servicio de actor Hola. Hola `ActorRuntime` método de registro realizará esta tarea para actores. En el caso más simple de hello, simplemente puede registrar el tipo de actor e implícitamente se usará el servicio de actor Hola con la configuración predeterminada:

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

Como alternativa, puede usar una expresión lambda que se proporciona mediante servicio de actor de hello registro método tooconstruct Hola. Puede, a continuación, configurar el servicio de actor de Hola y crear de forma explícita las instancias de actor, donde puede insertar actor de tooyour dependencias a través de su constructor:

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a>Métodos de servicio de actor
Hola implementa de servicio de Actor `IActorService` (C#) o `ActorService` (Java), que implementa a su vez `IService` (C#) o `Service` (Java). Se trata de una interfaz de hello utilizada por la comunicación remota de servicios de confianza, lo que permite llamadas a procedimiento remoto en los métodos de servicio. Contiene métodos de nivel de servicio a los que se puede llamar de manera remota a través del servicio remoto.

#### <a name="enumerating-actors"></a>Enumeración de los actores
servicio de actor Hola permite que un cliente tooenumerate metadatos sobre los actores de Hola que hospeda el servicio de Hola. Dado que Hola actor es un servicio con estado con particiones, enumeration se realiza por partición. Ya que cada partición puede contener varios actores, enumeración de Hola se devuelve como un conjunto de resultados paginados. páginas de Hola se entró en bucle en hasta que se lean todas las páginas. Hola siguiente ejemplo se muestra cómo obtener una lista de todos los actores activas de una partición de un servicio de actor toocreate:

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a>Eliminación de actores
servicio de actor Hello también proporciona una función para eliminar actores:

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

Para obtener más información acerca de cómo eliminar actores y su estado, vea hello [documentación de ciclo de vida de actor](service-fabric-reliable-actors-lifecycle.md).

### <a name="custom-actor-service"></a>Servicio de actor personalizado
Mediante el uso de lambda de registro de hello actor, puede registrar su propio servicio de actor personalizada que deriva de `ActorService` (C#) y `FabricActorService` (Java). En este servicio de actor personalizado, puede implementar su propia funcionalidad de nivel de servicio mediante la escritura de una clase de servicio que hereda `ActorService` (C#) o `FabricActorService` (Java). Un servicio de actor personalizada hereda todas las funciones en tiempo de ejecución de actor Hola de `ActorService` (C#) o `FabricActorService` (Java) y puede ser usado tooimplement sus propios métodos de servicio.

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
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
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a>Implementación de la copia de seguridad y restauración de los actores
 En el siguiente ejemplo de Hola, servicio de actor personalizada hello expone un tooback método los datos de actor aprovechando las ventajas de agente de escucha de comunicación remota de hello ya está presente en `ActorService`:

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


En este ejemplo, `IMyActorService` es un contrato remoto que implementa `IService` (C#) y `Service` (Java) y, luego, lo implementa `MyActorService`. Si se agrega este contrato de comunicación remota, métodos en `IMyActorService` ahora también están disponibles tooa cliente mediante la creación de un proxy de acceso remoto a través de `ActorServiceProxy`:

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a>Modelo de aplicación
Servicios de actor son servicios de confianza, por lo que el modelo de aplicación hello es Hola igual. Sin embargo, herramientas de generación de hello actor framework generan algunos de los archivos de modelo de aplicación Hola para usted.

### <a name="service-manifest"></a>Manifiesto de servicio
herramientas de generación de Hello actor framework generan automáticamente contenido Hola su actor del ServiceManifest.xml del archivo de servicio. Este archivo incluye:

* El tipo de servicio de actor. nombre del tipo Hello se genera basándose en el nombre del proyecto de su actor. En función de atributos de persistencia de hello en su actor, hello HasPersistedState marca también se establece en consecuencia.
* Paquete de código.
* Paquete de configuración.
* Recursos y puntos de conexión.

### <a name="application-manifest"></a>Manifiesto de aplicación
herramientas de generación de Hello actor framework crean automáticamente una definición de servicio predeterminado para el servicio de actor. herramientas de generación de Hello rellenan propiedades de servicio de hello predeterminadas:

* Número de conjunto de réplicas está determinado por el atributo de persistencia de hello en su actor. Cada atributo de persistencia de Hola de tiempo en su actor se cambia, número de conjunto de réplicas de hello en definición de servicio de hello predeterminado se restablece en consecuencia.
* Intervalo y el esquema de partición se establecen tooUniform Int64 con hello completa Int64 rango con clave.

## <a name="service-fabric-partition-concepts-for-actors"></a>Conceptos de partición de Service Fabric para los actores
Los servicios de actor son servicios con estado particionados. Cada partición de un servicio de actor contiene un conjunto de actores. Las particiones de servicio se distribuyen automáticamente sobre varios nodos en Service Fabric. Como resultado, se distribuyen las instancias de actor.

![Partición y distribución de actores][5]

Es posible crear Reliable Services con distintos intervalos de claves de partición y esquemas de partición. servicio de actor Hello usa esquema de partición Int64 Hola con hello completa Int64 rangos con clave toomap actores toopartitions.

### <a name="actor-id"></a>Id. de actor
Cada actor que se crea en el servicio de hello tiene un identificador único asociado con él, representado por hello `ActorId` clase. `ActorId`es un valor de identificador opaco que puede utilizarse para la distribución uniforme de los actores incluidos en particiones de servicio de hello mediante la generación de identificadores aleatorios:

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


Cada `ActorId` es tooan con hash Int64. Se trata de por qué servicio de actor Hola debe utilizar un esquema de partición Int64 con hello completa Int64 rango con clave. Sin embargo, los valores de identificadores personalizados se pueden usar para un valor `ActorID`, incluidos GUID/UUID, cadenas y valores Int64.

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

Cuando se usa GUID/UUID y cadenas, los valores de hello son hash tooan Int64. Sin embargo, cuando está explícitamente proporcionando un tooan Int64 `ActorId`, Hola Int64 asignará directamente tooa partición sin más algoritmos hash. Puede usar este toocontrol técnica que actores de Hola de partición se colocan en.

## <a name="next-steps"></a>Pasos siguientes
* [Administración de estados de los actores](service-fabric-reliable-actors-state-management.md)
* [Ciclo de vida de un actor y recolección de elementos no utilizados](service-fabric-reliable-actors-lifecycle.md)
* [Documentación de referencia de la API de actores](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Código de ejemplo de .NET](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Código de ejemplo de Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
