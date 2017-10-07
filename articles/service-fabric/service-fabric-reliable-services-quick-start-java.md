---
title: aaaCreate su primera microservicio confiable de Azure en Java | Documentos de Microsoft
description: "Introducción toocreating una aplicación de Microsoft Azure Service Fabric con servicios y sin estado."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
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

En este artículo se explica conceptos básicos de hello de servicios de Azure Service Fabric confiable y le guía a través de la creación e implementación de una aplicación de servicio confiable simple escrita en Java. Este vídeo de Microsoft Virtual Academy también muestra cómo toocreate un servicio confiable sin estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Instalación y configuración
Antes de empezar, asegúrese de que tiene el entorno de desarrollo de Service Fabric Hola configurado en su equipo.
Si necesita tooset, configúrelo, vaya demasiado[introducción en Mac](service-fabric-get-started-mac.md) o [introducción en Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Conceptos básicos
tooget a trabajar con servicios de confianza, solo se necesita toounderstand algunos conceptos básicos:

* **Tipo de servicio**: se trata de la implementación del servicio. Se define mediante la clase hello escribir que extiende `StatelessService` y cualquier otro código o a las dependencias que se usan en él, junto con un nombre y un número de versión.
* **Con el nombre de instancia de servicio**: toorun su servicio, crear instancias con nombre de su tipo de servicio, mucho como crear instancias de objeto de un tipo de clase. Las instancias de servicio son, en realidad, creaciones de instancias de objetos de la clase de servicio que escribe.
* **Host de servicio**: Hola instancias de servicio crear necesidad toorun dentro de un host con nombre. host de servicio de Hello es simplemente un proceso donde se pueden ejecutar instancias de su servicio.
* **Registro de servicio**: el registro incluye todos los elementos. Hello service type debe estar registrado con hello Service Fabric en tiempo de ejecución en un servicio de instancias de host tooallow Service Fabric toocreate del mismo toorun.  

## <a name="create-a-stateless-service"></a>Creación de un servicio sin estado
Comience por crear una aplicación de Service Fabric. Hola servicio SDK de tejido para Linux incluye un Yeoman scaffolding de hello tooprovide de generador para una aplicación de Service Fabric con un servicio sin estado. Comience ejecutando Hola siguientes Yeoman de comandos:

```bash
$ yo azuresfjava
```

Siga Hola instrucciones toocreate una **confiable servicio sin estado**. Para este tutorial, hello y aplicación de hello de nombre "HelloWorldApplication" servicio "HelloWorld". resultado de Hello incluye directorios para hello `HelloWorldApplication` y `HelloWorld`.

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>Implementar el servicio de Hola
Abra **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Esta clase define el tipo de servicio de Hola y puede ejecutar cualquier código. API de servicio de Hello proporciona dos puntos de entrada para el código:

* Un método de punto de entrada de extremo abierto, llamado `runAsync()`, donde puede comenzar a ejecutar cualquier carga de trabajo, incluidas cargas de trabajo de proceso de larga duración.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* Un punto de entrada de comunicación en el que puede conectar su pila de comunicación preferida. Aquí es donde puede empezar a recibir las solicitudes de usuarios y otros servicios.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

En este tutorial, nos centramos en hello `runAsync()` método de punto de entrada. Aquí es donde puede comenzar a ejecutar el código de inmediato.

### <a name="runasync"></a>RunAsync
plataforma de Hello llama a este método cuando una instancia de un servicio es tooexecute colocado y listo. Para un servicio sin estado, que simplemente significa que cuando se abre la instancia de servicio de Hola. Un token de cancelación se proporciona toocoordinate cuando la instancia de servicio necesita toobe cerrado. En Service Fabric, este ciclo de apertura y cierre de una instancia de servicio puede producir varias veces más vida Hola Hola como un todo. Esto puede ocurrir por diversos motivos, incluidos los siguientes:

* sistema de Hello mueve las instancias de servicio para equilibrar los recursos.
* Se producen errores en el código.
* se actualiza la aplicación Hello o sistema.
* hardware subyacente Hola experimenta una interrupción inesperada.

Esta orquestación está administrada por Service Fabric tookeep el servicio de alta disponibilidad y equilibrado correctamente.

`runAsync()` no debe bloquearse de forma sincrónica. La implementación de Coredispatcher debe devolver un toocontinue de CompletableFuture tooallow hello en tiempo de ejecución. Si la carga de trabajo necesita tooimplement una tarea de ejecución prolongada que debe realizarse dentro de Hola CompletableFuture.

#### <a name="cancellation"></a>Cancelación
Cancelación de la carga de trabajo es un esfuerzo cooperativo organizado Hola proporcionada el token de cancelación. Hola sistema espera que la tarea tooend (de realización correcta, cancelación o error) antes de que pase. Es importante toohonor Hola cancelación token, finalizar cualquier trabajo y salir `runAsync()` lo más rápido posible al sistema de hello solicita la cancelación. Hello ejemplo siguiente se muestra cómo toohandle un evento de cancelación:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>Registro de servicios
Tipos de servicio deben registrarse con el tiempo de ejecución de hello Service Fabric. tipo de servicio de Hola se define en hello `ServiceManifest.xml` y la clase de servicio que implementa `StatelessService`. Registro del servicio se realiza en el punto de entrada principal del proceso de Hola. En este ejemplo, Hola proceso en el punto de entrada principal sea `HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>Ejecutar la aplicación hello

Hola Yeoman scaffolding incluye un gradle script toobuild Hola aplicación y bash scripts toodeploy y quitar la aplicación. aplicación de hello toorun, primera aplicación Hola de compilación con gradle:

```bash
$ gradle
```

Esto crea un paquete de aplicación de Service Fabric que puede implementarse mediante la CLI de Service Fabric.

### <a name="deploy-with-service-fabric-cli"></a>Implementación con la CLI de Service Fabric

script de "Install.sh" Hello contiene Hola necesarios Service Fabric CLI comandos toodeploy Hola paquete de la aplicación. Ejecute la aplicación de "Install.sh" script toodeploy Hola.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Pasos siguientes

* [Introducción a la CLI de Service Fabric](service-fabric-cli.md)
