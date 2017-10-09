---
title: aaaCreate su primera microservicio Azure basado en actores en Java | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de crear, depurar e implementar un servicio simple basado en actores mediante servicio de Fabric Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Introducción a Reliable Actors
> [!div class="op_single_selector"]
> * [C# en Windows](service-fabric-reliable-actors-get-started.md)
> * [Java en Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

En este artículo se explica conceptos básicos de Hola de Azure Service Fabric Reliable Actors y le guía a través de la creación e implementación de una aplicación sencilla de Actor confiable en Java.

## <a name="installation-and-setup"></a>Instalación y configuración
Antes de empezar, asegúrese de que tiene el entorno de desarrollo de Service Fabric Hola configurado en su equipo.
Si necesita tooset, configúrelo, vaya demasiado[introducción en Mac](service-fabric-get-started-mac.md) o [introducción en Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Conceptos básicos
tooget partió Reliable Actors, sólo necesita toounderstand algunos conceptos básicos:

* **Servicio de actor**. Actores confiables se empaquetan en servicios de confianza que se pueden implementar en la infraestructura de Service Fabric Hola. Las instancias de actor se activan en una instancia de servicio con nombre.
* **Registro de actor**. Como con los servicios de confianza, un servicio de Actor confiable debe toobe registrado con el tiempo de ejecución de hello Service Fabric. Además, el tipo de actor de hello necesita toobe registrado con el tiempo de ejecución de hello Actor.
* **Interfaz de actor**. interfaz de actor Hello es toodefine usa una interfaz pública fuertemente tipada de un actor. Hola terminología del modelo confiable Actor, interfaz de actor de hello define Hola pueden entender y procesar tipos de mensajes que Hola actor. Hola actor interfaz la utilizan otros actores y las aplicaciones cliente demasiado "envían" (de forma asincrónica) actor toohello de mensajes. Reliable Actors pueden implementar varias interfaces.
* **Clase ActorProxy**. tooinvoke de las aplicaciones cliente utilizan Hello ActorProxy clase Hola métodos expuestos a través de la interfaz de actor Hola. Hola ActorProxy clase proporciona dos funciones importantes:
  
  * La resolución de nombres: es capaz de toolocate actor de hello en clúster de hello (Buscar Hola nodo de clúster Hola donde estén hospedados).
  * Control de error: se puede reintentar las invocaciones de método y volver a resolver la ubicación de actor de hello después, por ejemplo, un error que requiere Hola actor toobe reubicado tooanother nodo de clúster de Hola.

Hola siguiendo las reglas que pertenecen tooactor interfaces merece la pena comentar:

* No se pueden sobrecargar los métodos de interfaz de actor.
* Los métodos de interfaz de actor no deben tener parámetros out, ref u opcionales.
* No se admiten las interfaces genéricas.

## <a name="create-an-actor-service"></a>Creación de un servicio de actor
Comience por crear una nueva aplicación de Service Fabric. Hola servicio SDK de tejido para Linux incluye un Yeoman scaffolding de hello tooprovide de generador para una aplicación de Service Fabric con un servicio sin estado. Comience ejecutando Hola siguientes Yeoman de comandos:

```bash
$ yo azuresfjava
```

Siga Hola instrucciones toocreate una **servicio de Actor confiable**. Para este tutorial, el nombre actor de hello y "HelloWorldActorApplication" a los aplicación Hola "HelloWorldActor." se crearán Hola siguiendo la técnica scaffolding:

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>Bloques de creación básicos de Reliable Actors
conceptos básicos de Hello descritos anteriormente se traducen en Hola de bloques de creación básicos de un servicio de Actor confiable.

### <a name="actor-interface"></a>Interfaz de actor
Esto contiene la definición de interfaz de Hola de actor Hola. Esta interfaz define el contrato de actor Hola compartida por la implementación de actor de Hola y clientes de Hola que llaman actor hello, por lo que normalmente tiene sentido toodefine en un lugar al que se separe de implementación de actor hello y puede compartirse por otros diversos servicios o aplicaciones de cliente.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Servicio de actor
Contiene la implementación del actor y el código de registro del actor. clase de actor Hello implementa la interfaz de actor de Hola. Aquí es donde el actor realiza su trabajo.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>Registro del actor
servicio de actor Hola debe estar registrado con un tipo de servicio en tiempo de ejecución de hello Service Fabric. En orden para hello toorun de servicio de Actor las instancias del actor, el tipo de actor también deben registrarse con el servicio de Actor hello. Hola `ActorRuntime` método de registro realizará esta tarea para actores.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>Cliente de prueba
Se trata de una aplicación de cliente de prueba simple se puede ejecutar por separado de hello Service Fabric aplicación tootest su servicio de actor. Este es un ejemplo de donde hello ActorProxy puede tooactivate usado y comunicarse con instancias de actor. No se implementa con el servicio.

### <a name="hello-application"></a>aplicación Hello
Por último, los paquetes de aplicación Hola Hola servicio de actor y cualquier otro servicio que se puede agregar en hello futura juntos para la implementación. Contiene hello *ApplicationManifest.xml* y marcadores de posición para el paquete de servicio de actor Hola.

## <a name="run-hello-application"></a>Ejecutar la aplicación hello

Hola Yeoman scaffolding incluye un gradle script toobuild Hola aplicación y bash scripts toodeploy y quitar la aplicación. aplicación de hello toodeploy, primera aplicación Hola de compilación con gradle:

```bash
$ gradle
```

Esto creará un paquete de aplicación de Service Fabric que puede implementarse mediante las herramientas de CLI de Service Fabric.

### <a name="deploy-service-fabric-cli"></a>Implementación de la CLI de Service Fabric

script de "Install.sh" Hello contiene Hola necesarios CLI de tejido de servicio (sfctl) comandos toodeploy Hola paquete de la aplicación.
Ejecute hello "Install.sh" script toodeploy Hola aplicación.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Pasos siguientes

* [Introducción a la CLI de Service Fabric](service-fabric-cli.md)
