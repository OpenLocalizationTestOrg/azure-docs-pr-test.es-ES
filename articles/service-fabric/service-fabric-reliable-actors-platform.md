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
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="b97f6-103">Uso de Reliable Actors plataforma Service Fabric de Hola</span><span class="sxs-lookup"><span data-stu-id="b97f6-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="b97f6-104">Este artículo explica cómo funcionan los actores confiable en plataforma de Azure Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="b97f6-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="b97f6-105">Actores confiables que se ejecutan en un marco de trabajo que se hospeda en una implementación de un servicio confiable con estado llamado hello *servicio de actor*.</span><span class="sxs-lookup"><span data-stu-id="b97f6-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="b97f6-106">servicio de actor Hello contiene todos los ciclo de vida de hello componentes necesarios toomanage hello y un mensaje que envía para los actores:</span><span class="sxs-lookup"><span data-stu-id="b97f6-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="b97f6-107">Hola en tiempo de ejecución de Actor administra el ciclo de vida, recolección de elementos y aplica el acceso de un único subproceso.</span><span class="sxs-lookup"><span data-stu-id="b97f6-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="b97f6-108">Un agente de escucha de comunicación remota de servicio de actor acepta tooactors de llamadas de acceso remoto y los envía instancia de tooa distribuidor tooroute toohello actor adecuado.</span><span class="sxs-lookup"><span data-stu-id="b97f6-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="b97f6-109">Hola proveedor de estado de Actor ajusta los proveedores de estado (por ejemplo, el proveedor de estado de hello colecciones confiable) y proporciona un adaptador para la administración de estado de actor.</span><span class="sxs-lookup"><span data-stu-id="b97f6-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="b97f6-110">Estos componentes forman juntos Hola Actor confiable marco de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b97f6-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="b97f6-111">Servicio en capas</span><span class="sxs-lookup"><span data-stu-id="b97f6-111">Service layering</span></span>
<span data-ttu-id="b97f6-112">Porque el propio servicio de actor hello es un servicio confiable, todos Hola [modelo de aplicación](service-fabric-application-model.md), ciclo de vida, [empaquetado](service-fabric-package-apps.md), [implementación](service-fabric-deploy-remove-applications.md), actualizar y ajuste de escala en conceptos de Servicios de confianza aplican Hola mismo tooactor manera en los servicios.</span><span class="sxs-lookup"><span data-stu-id="b97f6-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![Servicio de actor en capas][1]

<span data-ttu-id="b97f6-114">Hello diagrama anterior muestra hello relación entre marcos de aplicaciones de Service Fabric de Hola y el código de usuario.</span><span class="sxs-lookup"><span data-stu-id="b97f6-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="b97f6-115">Elementos azul representan el marco de aplicación de servicios de confianza de hello, naranja representa el marco de trabajo de hello Actor confiable y verde representa código de usuario.</span><span class="sxs-lookup"><span data-stu-id="b97f6-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="b97f6-116">En servicios de confianza, el servicio hereda hello `StatefulService` clase.</span><span class="sxs-lookup"><span data-stu-id="b97f6-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="b97f6-117">Esta clase deriva de `StatefulServiceBase`, o bien de `StatelessService` en el caso de los servicios sin estado.</span><span class="sxs-lookup"><span data-stu-id="b97f6-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="b97f6-118">Servicio de actor Hola se utiliza en Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="b97f6-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="b97f6-119">servicio de actor Hello es una implementación diferente de hello `StatefulServiceBase` clase ese patrón de actor implementa Hola donde ejecutan los actores.</span><span class="sxs-lookup"><span data-stu-id="b97f6-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="b97f6-120">Porque el propio servicio de actor hello es simplemente una implementación de `StatefulServiceBase`, puede escribir su propio servicio que deriva de `ActorService` y características de nivel de servicio implemente Hola mismo tal como lo haría al heredar `StatefulService`, como:</span><span class="sxs-lookup"><span data-stu-id="b97f6-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="b97f6-121">Copia de seguridad y restauración del servicio.</span><span class="sxs-lookup"><span data-stu-id="b97f6-121">Service backup and restore.</span></span>
* <span data-ttu-id="b97f6-122">Funcionalidad compartida para todos los actores, por ejemplo, un interruptor.</span><span class="sxs-lookup"><span data-stu-id="b97f6-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="b97f6-123">Llamadas a procedimiento remoto en el propio servicio de actor hello y en cada actor individual.</span><span class="sxs-lookup"><span data-stu-id="b97f6-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="b97f6-124">Los servicios sin estado no son compatibles actualmente en Java/Linux.</span><span class="sxs-lookup"><span data-stu-id="b97f6-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="b97f6-125">Usar servicio de actor Hola</span><span class="sxs-lookup"><span data-stu-id="b97f6-125">Using hello actor service</span></span>
<span data-ttu-id="b97f6-126">Instancias de actor tengan en el que se ejecuta el servicio de actor de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="b97f6-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="b97f6-127">A través del servicio de actor hello, instancias de actor mediante programación pueden obtener el contexto de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b97f6-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="b97f6-128">contexto de servicio de Hello tiene Id. de partición de Hola, nombre del servicio, nombre de la aplicación y otra información específica de la plataforma de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="b97f6-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="b97f6-129">Al igual que todos los servicios de confianza, el servicio de actor de hello debe estar registrado con un tipo de servicio en tiempo de ejecución de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b97f6-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="b97f6-130">Para servicio de actor de hello toorun las instancias del actor, el tipo de actor también debe registrarse con el servicio de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="b97f6-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="b97f6-131">Hola `ActorRuntime` método de registro realizará esta tarea para actores.</span><span class="sxs-lookup"><span data-stu-id="b97f6-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="b97f6-132">En el caso más simple de hello, simplemente puede registrar el tipo de actor e implícitamente se usará el servicio de actor Hola con la configuración predeterminada:</span><span class="sxs-lookup"><span data-stu-id="b97f6-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="b97f6-133">Como alternativa, puede usar una expresión lambda que se proporciona mediante servicio de actor de hello registro método tooconstruct Hola.</span><span class="sxs-lookup"><span data-stu-id="b97f6-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="b97f6-134">Puede, a continuación, configurar el servicio de actor de Hola y crear de forma explícita las instancias de actor, donde puede insertar actor de tooyour dependencias a través de su constructor:</span><span class="sxs-lookup"><span data-stu-id="b97f6-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="b97f6-135">Métodos de servicio de actor</span><span class="sxs-lookup"><span data-stu-id="b97f6-135">Actor service methods</span></span>
<span data-ttu-id="b97f6-136">Hola implementa de servicio de Actor `IActorService` (C#) o `ActorService` (Java), que implementa a su vez `IService` (C#) o `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="b97f6-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="b97f6-137">Se trata de una interfaz de hello utilizada por la comunicación remota de servicios de confianza, lo que permite llamadas a procedimiento remoto en los métodos de servicio.</span><span class="sxs-lookup"><span data-stu-id="b97f6-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="b97f6-138">Contiene métodos de nivel de servicio a los que se puede llamar de manera remota a través del servicio remoto.</span><span class="sxs-lookup"><span data-stu-id="b97f6-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="b97f6-139">Enumeración de los actores</span><span class="sxs-lookup"><span data-stu-id="b97f6-139">Enumerating actors</span></span>
<span data-ttu-id="b97f6-140">servicio de actor Hola permite que un cliente tooenumerate metadatos sobre los actores de Hola que hospeda el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b97f6-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="b97f6-141">Dado que Hola actor es un servicio con estado con particiones, enumeration se realiza por partición.</span><span class="sxs-lookup"><span data-stu-id="b97f6-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="b97f6-142">Ya que cada partición puede contener varios actores, enumeración de Hola se devuelve como un conjunto de resultados paginados.</span><span class="sxs-lookup"><span data-stu-id="b97f6-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="b97f6-143">páginas de Hola se entró en bucle en hasta que se lean todas las páginas.</span><span class="sxs-lookup"><span data-stu-id="b97f6-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="b97f6-144">Hola siguiente ejemplo se muestra cómo obtener una lista de todos los actores activas de una partición de un servicio de actor toocreate:</span><span class="sxs-lookup"><span data-stu-id="b97f6-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="b97f6-145">Eliminación de actores</span><span class="sxs-lookup"><span data-stu-id="b97f6-145">Deleting actors</span></span>
<span data-ttu-id="b97f6-146">servicio de actor Hello también proporciona una función para eliminar actores:</span><span class="sxs-lookup"><span data-stu-id="b97f6-146">hello actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="b97f6-147">Para obtener más información acerca de cómo eliminar actores y su estado, vea hello [documentación de ciclo de vida de actor](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="b97f6-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="b97f6-148">Servicio de actor personalizado</span><span class="sxs-lookup"><span data-stu-id="b97f6-148">Custom actor service</span></span>
<span data-ttu-id="b97f6-149">Mediante el uso de lambda de registro de hello actor, puede registrar su propio servicio de actor personalizada que deriva de `ActorService` (C#) y `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="b97f6-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="b97f6-150">En este servicio de actor personalizado, puede implementar su propia funcionalidad de nivel de servicio mediante la escritura de una clase de servicio que hereda `ActorService` (C#) o `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="b97f6-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="b97f6-151">Un servicio de actor personalizada hereda todas las funciones en tiempo de ejecución de actor Hola de `ActorService` (C#) o `FabricActorService` (Java) y puede ser usado tooimplement sus propios métodos de servicio.</span><span class="sxs-lookup"><span data-stu-id="b97f6-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="b97f6-152">Implementación de la copia de seguridad y restauración de los actores</span><span class="sxs-lookup"><span data-stu-id="b97f6-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="b97f6-153">En el siguiente ejemplo de Hola, servicio de actor personalizada hello expone un tooback método los datos de actor aprovechando las ventajas de agente de escucha de comunicación remota de hello ya está presente en `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="b97f6-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

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


<span data-ttu-id="b97f6-154">En este ejemplo, `IMyActorService` es un contrato remoto que implementa `IService` (C#) y `Service` (Java) y, luego, lo implementa `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="b97f6-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="b97f6-155">Si se agrega este contrato de comunicación remota, métodos en `IMyActorService` ahora también están disponibles tooa cliente mediante la creación de un proxy de acceso remoto a través de `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="b97f6-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="b97f6-156">Modelo de aplicación</span><span class="sxs-lookup"><span data-stu-id="b97f6-156">Application model</span></span>
<span data-ttu-id="b97f6-157">Servicios de actor son servicios de confianza, por lo que el modelo de aplicación hello es Hola igual.</span><span class="sxs-lookup"><span data-stu-id="b97f6-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="b97f6-158">Sin embargo, herramientas de generación de hello actor framework generan algunos de los archivos de modelo de aplicación Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="b97f6-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="b97f6-159">Manifiesto de servicio</span><span class="sxs-lookup"><span data-stu-id="b97f6-159">Service manifest</span></span>
<span data-ttu-id="b97f6-160">herramientas de generación de Hello actor framework generan automáticamente contenido Hola su actor del ServiceManifest.xml del archivo de servicio.</span><span class="sxs-lookup"><span data-stu-id="b97f6-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="b97f6-161">Este archivo incluye:</span><span class="sxs-lookup"><span data-stu-id="b97f6-161">This file includes:</span></span>

* <span data-ttu-id="b97f6-162">El tipo de servicio de actor.</span><span class="sxs-lookup"><span data-stu-id="b97f6-162">Actor service type.</span></span> <span data-ttu-id="b97f6-163">nombre del tipo Hello se genera basándose en el nombre del proyecto de su actor.</span><span class="sxs-lookup"><span data-stu-id="b97f6-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="b97f6-164">En función de atributos de persistencia de hello en su actor, hello HasPersistedState marca también se establece en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="b97f6-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="b97f6-165">Paquete de código.</span><span class="sxs-lookup"><span data-stu-id="b97f6-165">Code package.</span></span>
* <span data-ttu-id="b97f6-166">Paquete de configuración.</span><span class="sxs-lookup"><span data-stu-id="b97f6-166">Config package.</span></span>
* <span data-ttu-id="b97f6-167">Recursos y puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="b97f6-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="b97f6-168">Manifiesto de aplicación</span><span class="sxs-lookup"><span data-stu-id="b97f6-168">Application manifest</span></span>
<span data-ttu-id="b97f6-169">herramientas de generación de Hello actor framework crean automáticamente una definición de servicio predeterminado para el servicio de actor.</span><span class="sxs-lookup"><span data-stu-id="b97f6-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="b97f6-170">herramientas de generación de Hello rellenan propiedades de servicio de hello predeterminadas:</span><span class="sxs-lookup"><span data-stu-id="b97f6-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="b97f6-171">Número de conjunto de réplicas está determinado por el atributo de persistencia de hello en su actor.</span><span class="sxs-lookup"><span data-stu-id="b97f6-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="b97f6-172">Cada atributo de persistencia de Hola de tiempo en su actor se cambia, número de conjunto de réplicas de hello en definición de servicio de hello predeterminado se restablece en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="b97f6-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="b97f6-173">Intervalo y el esquema de partición se establecen tooUniform Int64 con hello completa Int64 rango con clave.</span><span class="sxs-lookup"><span data-stu-id="b97f6-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="b97f6-174">Conceptos de partición de Service Fabric para los actores</span><span class="sxs-lookup"><span data-stu-id="b97f6-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="b97f6-175">Los servicios de actor son servicios con estado particionados.</span><span class="sxs-lookup"><span data-stu-id="b97f6-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="b97f6-176">Cada partición de un servicio de actor contiene un conjunto de actores.</span><span class="sxs-lookup"><span data-stu-id="b97f6-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="b97f6-177">Las particiones de servicio se distribuyen automáticamente sobre varios nodos en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b97f6-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="b97f6-178">Como resultado, se distribuyen las instancias de actor.</span><span class="sxs-lookup"><span data-stu-id="b97f6-178">Actor instances are distributed as a result.</span></span>

![Partición y distribución de actores][5]

<span data-ttu-id="b97f6-180">Es posible crear Reliable Services con distintos intervalos de claves de partición y esquemas de partición.</span><span class="sxs-lookup"><span data-stu-id="b97f6-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="b97f6-181">servicio de actor Hello usa esquema de partición Int64 Hola con hello completa Int64 rangos con clave toomap actores toopartitions.</span><span class="sxs-lookup"><span data-stu-id="b97f6-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="b97f6-182">Id. de actor</span><span class="sxs-lookup"><span data-stu-id="b97f6-182">Actor ID</span></span>
<span data-ttu-id="b97f6-183">Cada actor que se crea en el servicio de hello tiene un identificador único asociado con él, representado por hello `ActorId` clase.</span><span class="sxs-lookup"><span data-stu-id="b97f6-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="b97f6-184">`ActorId`es un valor de identificador opaco que puede utilizarse para la distribución uniforme de los actores incluidos en particiones de servicio de hello mediante la generación de identificadores aleatorios:</span><span class="sxs-lookup"><span data-stu-id="b97f6-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="b97f6-185">Cada `ActorId` es tooan con hash Int64.</span><span class="sxs-lookup"><span data-stu-id="b97f6-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="b97f6-186">Se trata de por qué servicio de actor Hola debe utilizar un esquema de partición Int64 con hello completa Int64 rango con clave.</span><span class="sxs-lookup"><span data-stu-id="b97f6-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="b97f6-187">Sin embargo, los valores de identificadores personalizados se pueden usar para un valor `ActorID`, incluidos GUID/UUID, cadenas y valores Int64.</span><span class="sxs-lookup"><span data-stu-id="b97f6-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="b97f6-188">Cuando se usa GUID/UUID y cadenas, los valores de hello son hash tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="b97f6-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="b97f6-189">Sin embargo, cuando está explícitamente proporcionando un tooan Int64 `ActorId`, Hola Int64 asignará directamente tooa partición sin más algoritmos hash.</span><span class="sxs-lookup"><span data-stu-id="b97f6-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="b97f6-190">Puede usar este toocontrol técnica que actores de Hola de partición se colocan en.</span><span class="sxs-lookup"><span data-stu-id="b97f6-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b97f6-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b97f6-191">Next steps</span></span>
* [<span data-ttu-id="b97f6-192">Administración de estados de los actores</span><span class="sxs-lookup"><span data-stu-id="b97f6-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="b97f6-193">Ciclo de vida de un actor y recolección de elementos no utilizados</span><span class="sxs-lookup"><span data-stu-id="b97f6-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="b97f6-194">Documentación de referencia de la API de actores</span><span class="sxs-lookup"><span data-stu-id="b97f6-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="b97f6-195">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="b97f6-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="b97f6-196">Código de ejemplo de Java</span><span class="sxs-lookup"><span data-stu-id="b97f6-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
