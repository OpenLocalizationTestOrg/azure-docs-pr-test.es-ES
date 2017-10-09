---
title: "aaaCreate su primera aplicación de Service Fabric en C# | Documentos de Microsoft"
description: "Introducción toocreating una aplicación de Microsoft Azure Service Fabric con servicios y sin estado."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Introducción a los servicios de confianza
> [!div class="op_single_selector"]
> * [C# en Windows](service-fabric-reliable-services-quick-start.md)
> * [Java en Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Una aplicación de Service Fabric de Azure contiene uno o varios servicios que ejecutan su código. Esta guía le mostrará cómo toocreate sin estado y con estado las aplicaciones de Service Fabric con [servicios confiables](service-fabric-reliable-services-introduction.md).  Este vídeo de Microsoft Virtual Academy también muestra cómo toocreate un servicio confiable sin estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Conceptos básicos
tooget a trabajar con servicios de confianza, solo se necesita toounderstand algunos conceptos básicos:

* **Tipo de servicio**: se trata de la implementación del servicio. Se define mediante la clase hello escribir que extiende `StatelessService` y cualquier otro código o a las dependencias que se usan en él, junto con un nombre y un número de versión.
* **Con el nombre de instancia de servicio**: toorun su servicio, crear instancias con nombre de su tipo de servicio, mucho como crear instancias de objeto de un tipo de clase. Una instancia de servicio tiene un nombre en forma de Hola de identificadores URI utilizando Hola "fabric: /" esquema, como "fabric: / MyApp/MyService".
* **Host de servicio**: Hola instancias de servicio crear necesidad toorun dentro de un proceso de host con nombre. host de servicio de Hello es simplemente un proceso donde se pueden ejecutar instancias de su servicio.
* **Registro de servicio**: el registro incluye todos los elementos. Hello service type debe estar registrado con hello Service Fabric en tiempo de ejecución en un servicio de instancias de host tooallow Service Fabric toocreate del mismo toorun.  

## <a name="create-a-stateless-service"></a>Creación de un servicio sin estado
Un servicio sin estado es un tipo de servicio que se encuentra actualmente norm hello en aplicaciones de nube. Se considera sin estado porque el propio servicio hello no contiene datos que es necesario toobe almacenada de forma confiable u ofrezca alta disponibilidad. Si se cierra una instancia de un servicio sin estado, todo su estado interno se pierde. En este tipo de servicio, el estado debe ser almacén externo de tooan persistente, como tablas de Azure o una base de datos SQL, para él toobe realizados altamente disponible y confiable.

Inicie Visual Studio 2015 o Visual Studio 2017 como administrador y cree un nuevo proyecto de aplicación de Service Fabric denominado *HelloWorld*:

![Usar toocreate de cuadro de diálogo de hello nuevo proyecto una nueva aplicación de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Después, cree un proyecto de servicio sin estado denominado *HelloWorldStateless*:

![En el segundo cuadro de diálogo hello, cree un proyecto de servicio sin estado](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

La solución contiene ahora dos proyectos:

* *HelloWorld*. Se trata de hello *aplicación* proyecto que contiene su *services*. También contiene el manifiesto de aplicación Hola que describe la aplicación hello, así como un número de secuencias de comandos de PowerShell que le ayudarán a toodeploy la aplicación.
* *HelloWorldStateless*. Se trata de un proyecto de servicio de Hola. Que contiene la implementación de servicio sin estado Hola.

## <a name="implement-hello-service"></a>Implementar el servicio de Hola
Abra hello **HelloWorldStateless.cs** archivo de proyecto de servicio de Hola. En Service Fabric, un servicio puede ejecutar cualquier lógica de negocios. API de servicio de Hello proporciona dos puntos de entrada para el código:

* Llama a un método de punto de entrada abierto denominado " *RunAsync*" donde puede comenzar la ejecución de cualquier carga de trabajo que desee, como cargas de trabajo de proceso de larga duración.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* Un punto de entrada de comunicación en el que puede conectar su pila de comunicación preferida, como ASP.NET Core. Aquí es donde puede empezar a recibir las solicitudes de usuarios y otros servicios.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

En este tutorial, nos centraremos en hello `RunAsync()` método de punto de entrada. Aquí es donde puede comenzar a ejecutar el código de inmediato.
plantilla de proyecto de Hello incluye una implementación de ejemplo `RunAsync()` que incrementa un recuento gradual.

> [!NOTE]
> Para obtener más información acerca de cómo la pila toowork con una comunicación, vea [servicios de API Web del servicio tejido con OWIN hospeda a sí mismo](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

plataforma de Hello llama a este método cuando una instancia de un servicio es tooexecute colocado y listo. Para un servicio sin estado, que simplemente significa que cuando se abre la instancia de servicio de Hola. Un token de cancelación se proporciona toocoordinate cuando la instancia de servicio necesita toobe cerrado. En Service Fabric, este ciclo de apertura y cierre de una instancia de servicio puede producir varias veces más vida Hola Hola como un todo. Esto puede ocurrir por diversos motivos, incluidos los siguientes:

* sistema de Hello mueve las instancias de servicio para equilibrar los recursos.
* Se producen errores en el código.
* se actualiza la aplicación Hello o sistema.
* hardware subyacente Hola experimenta una interrupción inesperada.

Esta orquestación está administrada por hello sistema tookeep el servicio de alta disponibilidad y equilibrado correctamente.

`RunAsync()` no debe bloquearse de forma sincrónica. La implementación de Coredispatcher debe devolver una tarea o await en cualquier toocontinue de tiempo de ejecución de las operaciones de ejecución prolongada o de bloqueo tooallow Hola. Tenga en cuenta en hello `while(true)` bucle en el ejemplo anterior de hello, una devolución de tarea `await Task.Delay()` se utiliza. Si la carga de trabajo debe bloquearse de forma sincrónica, debería programar una nueva tarea con `Task.Run()` en la implementación de `RunAsync`.

Cancelación de la carga de trabajo es un esfuerzo cooperativo organizado Hola proporcionada el token de cancelación. Hola sistema esperará la tarea tooend (de realización correcta, cancelación o error) antes de que pase. Es importante toohonor Hola cancelación token, finalizar cualquier trabajo y salir `RunAsync()` lo más rápido posible al sistema de hello solicita la cancelación.

En este ejemplo de servicio sin estado, el recuento de Hola se almacena en una variable local. Pero porque se trata de un servicio sin estado, valor de Hola que se almacena solamente existe por hello ciclo de vida actual de su instancia de servicio. Cuando el servicio de Hola se mueve o se reinicia, el valor de Hola se pierde.

## <a name="create-a-stateful-service"></a>Creación de un servicio con estado
Service Fabric presenta un nuevo tipo de servicio que es con estado. Un servicio con estado puede mantener el estado confiable dentro Hola propio servicio, colocado con código de hello que lo está usando. Estado ofrezca alta disponibilidad por Service Fabric sin almacén externo de hello necesidad toopersist estado tooan.

tooconvert un valor de contador de toohighly sin estado disponible y persistente, incluso cuando el servicio de Hola se mueve o se reinicia, se necesita un servicio con estado.

En Hola mismo *HelloWorld* aplicación, puede agregar un nuevo servicio con el botón secundario en referencias de servicios de hello en el proyecto de aplicación de Hola y seleccionando **Agregar -> nuevo servicio de Fabric**.

![Agregar una aplicación de Service Fabric tooyour de servicio](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Seleccione **Servicio con estado** y asígnele el nombre *HelloWorldStateful*. Haga clic en **Aceptar**.

![Usar toocreate de cuadro de diálogo de hello nuevo proyecto un nuevo servicio con estado de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

La aplicación ahora debería tener dos servicios: Hola servicio sin estado *HelloWorldStateless* y el servicio con estado hello *HelloWorldStateful*.

Un servicio con estado tiene Hola mismos puntos de entrada como un servicio sin estado. Hola principal diferencia es disponibilidad Hola de un *proveedor de estado* estado que puede almacenar de forma confiable. Tejido de servicio incluye una implementación de proveedor de estado llama [colecciones confiable](service-fabric-reliable-services-reliable-collections.md), que le permite crear estructuras de datos replicados mediante Hola confiable Administrador de estado. Un servicio de confianza con estado usa este proveedor de estado de forma predeterminada.

Abra **HelloWorldStateful.cs** en *HelloWorldStateful*, que contiene Hola sigue Coredispatcher método:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()` funciona de forma similar en los servicios con y sin estado. Sin embargo, en un servicio con estado, plataforma Hola realiza un trabajo adicional en su nombre antes de ejecutar `RunAsync()`. Este trabajo puede incluir asegurarse de que el Administrador de estado confiable de Hola y confiable de colecciones son toouse listo.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>Confiable hello el Administrador de estado confiable y colecciones
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) es una implementación de diccionario que puede usar tooreliably almacenar el estado de servicio de Hola. Con Service Fabric y confiable de las colecciones, puede almacenar los datos directamente en el servicio sin necesidad de Hola de un almacén persistente externo. Gracias a Reliable Collections, los datos tendrán una alta disponibilidad. Service Fabric realiza esta tarea creando y administrando automáticamente varias *réplicas* de su servicio. También proporciona una API que abstrae las complejidades de hello alejada de la administración de las réplicas y sus transiciones de estado.

Reliable Collections puede almacenar cualquier tipo de .NET, incluidos los tipos personalizados, con un par de advertencias:

* Tejido de servicio hace que el estado de la alta disponibilidad *replicar* estado entre nodos y colecciones confiable almacenar el disco de toolocal de datos en cada réplica. Es decir, todo lo que se almacena en Reliable Collections debe ser *serializable*. De forma predeterminada, se usan colecciones confiable [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) para la serialización, por lo que es importante toomake seguro de que los tipos son [admite Hola serializador de contratos de datos](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) cuando se usa de forma predeterminada Hola serializador.
* Los objetos se replican para obtener una alta disponibilidad cuando se confirman transacciones en Reliable Collections. Los objetos almacenados en Reliable Collections se mantienen en la memoria local en el servicio. Esto significa que tiene un objeto de toohello de referencia local.
  
   Es importante que no modifica las instancias locales de esos objetos sin realizar una operación de actualización en la colección confiable de hello en una transacción. Esto es porque cambios toolocal instancias de objetos no se replicarán automáticamente. Debe volver a insertar el objeto de hello en el diccionario de Hola o utilizar uno de hello *actualizar* métodos en el diccionario de Hola.

Hola, Administrador de estado confiable administra colecciones confiable en su nombre. Puede simplemente pedir Hola confiable Administrador de Estados para una colección de confianza por su nombre en cualquier momento y en cualquier lugar en el servicio. Hola, Administrador de estado confiable garantiza que se recibe una referencia. No recomendamos guardar referencias de instancias de la colección de tooreliable en variables de miembro de clase o propiedades. Debe tener especial cuidado tooensure que se establece la referencia de hello instancia tooan en todo momento en el ciclo de vida de servicio de Hola. Hola el Administrador de estado confiable administra este trabajo automáticamente, y está optimizado para la repetición de visitas.

### <a name="transactional-and-asynchronous-operations"></a>Operaciones transaccionales y asincrónicas
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Colecciones confiables tienen muchas Hola mismas operaciones que sus `System.Collections.Generic` y `System.Collections.Concurrent` homólogos, excepto LINQ. Sin embargo, las operaciones relacionadas con Reliable Collections son asincrónicas. Esto es porque las operaciones de escritura con colecciones de confianza realizan tooreplicate de las operaciones de E/S y conservan datos toodisk.

Las operaciones de Reliable Collections son *transaccionales*, de modo que el estado puede mantenerse de forma coherente entre varias operaciones y colecciones Reliable Collections. Por ejemplo, puede quitar de la cola un elemento de trabajo de una cola confiable, realizar una operación en él y guardar el resultado de hello en un diccionario confiable, todo dentro de una sola transacción. Se trata como una operación atómica, y garantiza que se realizará correctamente la operación completa de Hola o se revertirá la operación completa de Hola. Si se produce un error después de dequeue elemento Hola pero antes de guardar el resultado de hello, se revierte la transacción entera de Hola y elemento de hello permanece en la cola de Hola para su procesamiento.

## <a name="run-hello-application"></a>Ejecutar la aplicación hello
Devolvemos ahora toohello *HelloWorld* aplicación. Ahora puede compilar e implementar sus servicios. Cuando se presiona **F5**, la aplicación será el clúster local tooyour compilado e implementado.

Después de hello de servicios de inicio que se ejecuta, puede ver Hola genera eventos de seguimiento de eventos para Windows (ETW) en un **eventos de diagnóstico** ventana. Tenga en cuenta que los eventos de hello muestra del servicio sin estado de Hola y Hola servicio con estado en la aplicación hello. Puede pausar flujo Hola haciendo clic en hello **pausar** botón. A continuación, puede examinar detalles Hola de un mensaje al expandir ese mensaje.

> [!NOTE]
> Antes de ejecutar la aplicación hello, asegúrese de que tiene un clúster de desarrollo local que se ejecuta. Extraer del repositorio hello [Guía de introducción](service-fabric-get-started.md) para obtener información sobre cómo configurar su entorno local.
> 
> 

![Ver eventos de diagnóstico en Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>Pasos siguientes
[Depuración de la aplicación del Service Fabric en Visual Studio](service-fabric-debugging-your-application.md)

[Introducción a los servicios de la API web de Microsoft Azure Service Fabric con autohospedaje OWIN](service-fabric-reliable-services-communication-webapi.md)

[Obtenga más información acerca de las colecciones fiables](service-fabric-reliable-services-reliable-collections.md)

[Implementar una aplicación](service-fabric-deploy-remove-applications.md)

[Actualización de aplicaciones](service-fabric-application-upgrade.md)

[Referencia para desarrolladores de servicios confiables](https://msdn.microsoft.com/library/azure/dn706529.aspx)

