---
title: aaaCreate su primera microservicio Azure basado en actores en C# | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de crear, depurar e implementar un servicio simple basado en actores mediante servicio de Fabric Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
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

En este artículo se explica conceptos básicos de Hola de Azure Service Fabric Reliable Actors y le guía a través de crear, depurar e implementar una aplicación sencilla de Actor confiable en Visual Studio.

## <a name="installation-and-setup"></a>Instalación y configuración
Antes de empezar, asegúrese de que tiene el entorno de desarrollo de Service Fabric Hola configurado en su equipo.
Si necesita tooset, configúrelo, vea instrucciones detalladas en [cómo tooset el entorno de desarrollo de hello](service-fabric-get-started.md).

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

## <a name="create-a-new-project-in-visual-studio"></a>Creación de un proyecto en Visual Studio
Inicie Visual Studio 2015 o Visual Studio 2017 como administrador y cree un nuevo proyecto de aplicación de Service Fabric:

![Herramientas de Service Fabric para Visual Studio: nuevo proyecto][1]

En el siguiente cuadro de diálogo hello, puede elegir a tipo hello de proyecto que desea toocreate.

![Plantillas de proyecto de Service Fabric][5]

Proyecto HelloWorld de hello, vamos a usar servicio de Service Fabric Reliable Actors Hola.

Después de haber creado la solución de hello, debería ver Hola siguiente estructura:

![Estructura de proyecto de Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a>Bloques de creación básicos de Reliable Actors
Una solución típica de Reliable Actors se compone de tres proyectos:

* **proyecto de aplicación Hola (MyActorApplication)**. Se trata de un proyecto de Hola que todos los servicios de hello juntos para la implementación de los paquetes. Contiene hello *ApplicationManifest.xml* y scripts de PowerShell para administrar la aplicación hello.
* **proyecto de interfaz de Hello (MyActor.Interfaces)**. Este es el proyecto de Hola que contiene la definición de interfaz Hola actor Hola. En el proyecto de MyActor.Interfaces hello, se pueden definir las interfaces de Hola que se usará en actores de hello en soluciones de Hola. Las interfaces de actor pueden definirse en cualquier proyecto con cualquier nombre, pero la interfaz de hello define el contrato de actor de hello compartida por la implementación de actor de Hola y clientes de Hola que llaman actor hello, por lo que normalmente tiene sentido toodefine en un ensamblado separar de la implementación de actor hello y puede compartirse entre varios otros proyectos.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **proyecto de servicio de actor Hello (MyActor)**. Esto es Hola proyecto utilizado toodefine Hola Service Fabric servicio que es continuo toohost Hola actor. Contiene implementación Hola de actor Hola. Una implementación de actor es una clase que deriva de un tipo base hello `Actor` e implementa Hola interfaces que se definen en hello MyActor.Interfaces proyecto. Una clase de actor también debe implementar un constructor que acepta un `ActorService` instancia y un `ActorId` y los pasa toohello base `Actor` clase. Esto permite la inyección de dependencia de constructor de dependencias de plataforma.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

servicio de actor Hola debe estar registrado con un tipo de servicio en tiempo de ejecución de hello Service Fabric. En orden para hello toorun de servicio de Actor las instancias del actor, el tipo de actor también deben registrarse con el servicio de Actor hello. Hola `ActorRuntime` método de registro realizará esta tarea para actores.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Si se inicia desde un proyecto nuevo en Visual Studio y tiene una sola definición de actor, registro de hello se incluye de forma predeterminada en el código de hello que genera Visual Studio. Si define otros actores en servicio de hello, necesita registro de actor hello tooadd mediante:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> Hello en tiempo de ejecución de servicio Fabric actores emite algunos [eventos y contadores de rendimiento relacionados con los métodos de tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). Son útiles para la supervisión del rendimiento y los diagnósticos.
> 
> 

## <a name="debugging"></a>Depuración
herramientas de Service Fabric Hola para Visual Studio admiten la depuración en el equipo local. Puede iniciar una sesión de depuración mediante la tecla F5 de posicionamiento Hola. Visual Studio compila (si es necesario) paquetes. También implementa la aplicación hello en clúster de Service Fabric local hello y asocia el depurador de Hola.

Durante el proceso de implementación de hello, puede ver el progreso de Hola Hola **salida** ventana.

![Ventana de resultados de depuración de Service Fabric][3]

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre [cómo Reliable Actors usar plataforma Service Fabric de hello](service-fabric-reliable-actors-platform.md).

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
