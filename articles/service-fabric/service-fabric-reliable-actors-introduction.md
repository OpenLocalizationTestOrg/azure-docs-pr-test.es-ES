---
title: "aaaService tejido confiable actores Introducción | Documentos de Microsoft"
description: "Modelo de programación de introducción toohello Reliable Actors de tejido de servicio."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 7fdad07f-f2d6-4c74-804d-e0d56131f060
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab010cbf936c6cf723b3d453ef95a9bf51f76c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-reliable-actors"></a>Introducción tooService tejido Reliable Actors
Actores confiables es un marco de aplicación de Service Fabric en función de hello [Actor Virtual](http://research.microsoft.com/en-us/projects/orleans/) patrón. Hola API de actores confiable proporciona un modelo de programación uniproceso basado en garantías de confiabilidad y escalabilidad de hello proporcionadas por Service Fabric.

## <a name="what-are-actors"></a>¿Qué son los actores?
Un actor es una unidad aislada e independiente de proceso y estado con ejecución uniproceso. Hola [patrón actor](https://en.wikipedia.org/wiki/Actor_model) es un modelo de cálculo para los sistemas simultáneos o distribuidos en que un gran número de estos actores puede ejecutar simultáneamente e independientemente entre sí. Los actores pueden comunicarse entre sí y pueden crear más actores.

### <a name="when-toouse-reliable-actors"></a>Cuando toouse Reliable Actors
Servicio Fabric Reliable Actors es una implementación del patrón de diseño de hello actor. Al igual que con cualquier modelo de diseño de software, decisión Hola si toouse un patrón específico estará en función de si un software diseñe problema encaja patrón Hola.

Aunque el modelo de diseño de hello actor puede ser un número de buena tooa ajuste de problemas de sistemas distribuidos y escenarios, debe valorarse cuidadosamente las restricciones de Hola de patrón de Hola y Hola framework implementar deben realizarse. Como guía general, considere la posibilidad de hello actor patrón toomodel su problema o escenario si:

* El espacio del problema implica un gran número (miles o más) de unidades pequeñas, independientes y aisladas de estado y lógica.
* Desea toowork con objetos de un único subproceso que no requieren interacción importante de los componentes externos, incluidas las consultas de estado a través de un conjunto de actores.
* Las instancias de actor no bloquearán a los autores de llamadas con retrasos imprevisibles emitiendo operaciones de E/S.

## <a name="actors-in-service-fabric"></a>Actores en Service Fabric
En Service Fabric, actores se implementan en el marco de trabajo de hello Reliable Actors: un marco de trabajo de aplicaciones basados en el patrón de actor construido sobre [servicios confiables de tejido de servicio](service-fabric-reliable-services-introduction.md). Cada servicio de Reliable Actors que escribe es en realidad un servicio de confianza con estado particionado.

Cada actor se define como una instancia de un tipo de actor, toohello idéntica forma un objeto .NET es una instancia de un tipo. NET. Por ejemplo, puede haber un tipo de actor que implementa la funcionalidad de Hola de una calculadora y podría haber muchos actores de ese tipo que se distribuyen en varios nodos en un clúster. Cada uno de esos actores se identifica de forma única mediante un identificador de actor.

### <a name="actor-lifetime"></a>Duración del actor
Actores de Service Fabric son virtuales, lo que significa que su duración no es de representación en memoria de tootheir relacionados. Como resultado, no es necesario toobe cree explícitamente o se destruya. en tiempo de ejecución de Hello Reliable Actors activa automáticamente una Hola actor primera vez que se recibe una solicitud para dicho Id. de actor Si no se usa un actor durante un período de tiempo, en tiempo de ejecución de hello Reliable Actors elementos no utilizados-recopila objeto de hello en memoria. También mantendrá conocimiento de la existencia del actor Hola necesario toobe reactivar más adelante. Para más información, consulte [Ciclo de vida de un actor y recolección de elementos no utilizados](service-fabric-reliable-actors-lifecycle.md).

Esta abstracción de duración de actor virtual lleva a cabo algunas advertencias como resultado de modelo de actor virtual Hola y de hecho la implementación Reliable Actors Hola se desvía a veces de este modelo.

* Un actor se activa automáticamente (lo que provoca un actor toobe objeto construido) Hola la primera vez que se envía un mensaje tooits Id. de actor. Después de un período de tiempo, objeto de actor hello es recolectado. Hola futuro, vuelva a usar el Id. de actor Hola hace que un actor nueva toobe objeto construido. Estado de un actor es mayor duración del objeto de hello cuando se almacenan en el Administrador de estado de Hola.
* Al llamar a cualquier método de actor para un identificador de actor se activa dicho actor. Por este motivo, los tipos de actor tienen su constructor llama implícitamente a hello en tiempo de ejecución. Por lo tanto, el código de cliente no puede pasar al constructor del tipo de parámetros toohello actor, aunque pueden pasarse a parámetros de constructor de actor toohello por el propio servicio Hola. resultado de Hello es que actores se pueden construir en un estado parcialmente inicializada por otros métodos se invocan en él, el tiempo de hello si actor Hola requiere parámetros de inicialización de cliente de Hola. No hay ningún punto de entrada único para la activación de Hola de un actor desde el cliente de Hola.
* Aunque Reliable Actors implícitamente crear objetos de actor; es necesario Hola capacidad tooexplicitly eliminar un actor y su estado.

### <a name="distribution-and-failover"></a>Distribución y conmutación por error
tooprovide escalabilidad y confiabilidad, Service Fabric distribuye actores en todo el clúster de Hola y automáticamente migra desde nodos erróneos toohealthy los según sea necesario. Se trata de una abstracción sobre un [servicio de confianza con estado particionado](service-fabric-concepts-partitioning.md). Distribución, escalabilidad, confiabilidad y conmutación automática por error se proporcionan en virtud de los hechos de Hola que actores se ejecutan dentro de un servicio confiable con estado llamado hello *servicio de Actor*.

Actores se distribuyen entre particiones de Hola de hello servicio de Actor y estas particiones se distribuyen en nodos de hello en un clúster de Service Fabric. Cada partición del servicio contiene un conjunto de actores. Service Fabric administra la distribución y la conmutación por error de las particiones del servicio Hola.

Por ejemplo, un servicio de actor con nueve particiones implementa toothree se distribuyen nodos mediante la colocación de partición de actor de hello predeterminada consiste en lo siguiente:

![Distribución de Reliable Actors][2]

Hola Actor Framework administra la configuración de los intervalos de esquema y la clave de partición para el. Esto simplifica algunas opciones, pero también implica cierta consideración:

* Servicios de confianza permite toochoose un esquema de partición, intervalo de claves (cuando se usa un intervalo de esquema de partición) y el número de partición. Actores confiables es el esquema de partición de intervalo restringido toohello (esquema de Int64 uniforme Hola) y requiere que use Hola completa Int64 rango con clave.
* De forma predeterminada, los actores se colocan aleatoriamente en particiones, dando como resultado una distribución uniforme.
* Como los actores se colocan aleatoriamente, debe esperarse que las operaciones del actor requieran siempre la comunicación de red, incluidas la serialización y deserialización de datos de la llamada al método, incurriendo en latencia y sobrecarga.
* En escenarios avanzados, es selección de ubicación de toocontrol posible actor partición mediante el uso de actor Int64 identificadores que se asignan toospecific particiones. Sin embargo, esto puede dar lugar a una distribución desequilibrada de los actores entre particiones.

Para obtener más información sobre cómo se dividen los servicios de actor, consulte demasiado[particiones conceptos para actores](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

### <a name="actor-communication"></a>Comunicación con actores
Interacciones de actor se definen en una interfaz que se comparte por actor Hola que implementa la interfaz de Hola y el cliente de Hola que obtiene un proxy actor tooan a través de hello misma interfaz. Dado que esta interfaz es tooinvoke usado actor métodos de forma asincrónica, cada método de interfaz de hello debe ser de devolución de tarea.

Las invocaciones de método y sus respuestas en última instancia como resultado las solicitudes de red en clúster de hello, por lo que argumentos de Hola y tipos de resultado de hello de tareas de Hola que deben ser serializables por plataforma de Hola. En particular, deben ser [serializables mediante contrato de datos](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

#### <a name="hello-actor-proxy"></a>proxy de actor Hola
API de cliente de Reliable Actors Hola permite la comunicación entre una instancia de actor y un cliente de actor. toocommunicate con un actor, un cliente crea un objeto de proxy de actor que implementa la interfaz de actor Hola. cliente de Hello interactúa con actor Hola invocar métodos en el objeto de proxy de Hola. proxy de actor Hola se puede utilizar para la comunicación de cliente al actor y el actor al actor.

```csharp
// Create a randomly distributed actor ID
ActorId actorId = ActorId.CreateRandom();

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
IMyActor myActor = ActorProxy.Create<IMyActor>(actorId, new Uri("fabric:/MyApp/MyActorService"));

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
await myActor.DoWorkAsync();
```

```java
// Create actor ID with some name
ActorId actorId = new ActorId("Actor1");

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
MyActor myActor = ActorProxyBase.create(actorId, new URI("fabric:/MyApp/MyActorService"), MyActor.class);

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
myActor.DoWorkAsync().get();
```


Tenga en cuenta que partes de hello dos de información usan objeto proxy de toocreate Hola actor son Id. de actor de Hola y nombre de la aplicación hello. Id. de actor Hola identifica de forma única actor hello, mientras que identifica a nombre de la aplicación Hola Hola [aplicación de Service Fabric](service-fabric-reliable-actors-platform.md#application-model) donde se implementa el actor Hola.

Hola `ActorProxy`(C#) / `ActorProxyBase`clase (Java) en el lado del cliente de hello realiza actor de hello resolución necesarios toolocate Hola por Id. y abrir un canal de comunicación con él. También realiza varios intentos toolocate actor de hello en los casos de Hola de errores de comunicación y las conmutaciones por error. Como resultado, la entrega de mensajes tiene Hola siguientes características:

* La entrega de mensajes es la mejor opción.
* Actores pueden recibir mensajes duplicados de hello mismo cliente.

### <a name="concurrency"></a>Simultaneidad
Hola Reliable Actors runtime proporciona un modelo de acceso a su vez simple para tener acceso a los métodos de actor. Esto significa que no puede haber más de un subproceso activo dentro del código del objeto de actor en ningún momento. El acceso basado en turnos simplifica considerablemente sistemas simultáneos, pues no es necesario que los mecanismos de sincronización tengan acceso a datos. También significa que los sistemas deben diseñarse con consideraciones especiales para la naturaleza de acceso de un único subproceso de Hola de cada instancia de actor.

* Una sola instancia de actor no puede procesar más de una solicitud cada vez. Una instancia de actor puede producir un cuello de botella de rendimiento si se toohandle esperado de solicitudes simultáneas.
* Actores pueden bloquearse entre sí si hay una solicitud circular entre las dos partes implicadas mientras externa se realiza una solicitud tooone de actores Hola simultáneamente. Hola actor en tiempo de ejecución tendrán automáticamente una vez en actor llama y producir un toointerrupt de autor de llamada de excepción toohello posibles situaciones de interbloqueo.

![Comunicación de Reliable Actors][3]

#### <a name="turn-based-access"></a>Acceso basada en turnos
Un turno consta de hello completar la ejecución de un método de actor en solicitud de respuesta tooa procedentes de otros clientes o actores o completar la ejecución de hello un [temporizador/aviso](service-fabric-reliable-actors-timers-reminders.md) devolución de llamada. Aunque estos métodos y las devoluciones de llamada son asincrónicas, en tiempo de ejecución de hello actores no intercalar ellos. Un turno debe completarse por completo antes de que se permita uno nuevo. En otras palabras, un actor método o un temporizador/aviso devolución de llamada que se está ejecutando actualmente debe ser totalmente finalice antes que un nuevo método tooa de llamada o devolución de llamada es permitida. Un método o una devolución de llamada se considera toohave terminado si ejecución Hola ha devuelto del método hello o tarea hello y devolución de llamada devuelta por el método hello o devolución de llamada ha terminado. Merece la pena resaltar que la simultaneidad basada en turnos se respeta incluso entre devoluciones de llamada, temporizadores y métodos diferentes.

en tiempo de ejecución de Hello actores aplica la simultaneidad basada en Active al adquirir un bloqueo por actor al principio de hello vuelta y liberación de bloqueo de hello final Hola de hello activar. Por lo tanto, la simultaneidad basada en turnos se aplica por actor y no para todos los actores. Las devoluciones de llamada de los métodos de actor, los temporizadores y los recordatorios se pueden ejecutar simultáneamente en nombre de los diferentes actores.

Hola siguiente ejemplo muestra hello por encima de los conceptos. Supongamos un tipo de actor que implementa dos métodos asincrónicos (digamos *Method1* y *Method2*), un temporizador y un recordatorio. Hola diagrama siguiente muestra un ejemplo de una escala de tiempo para la ejecución de Hola de estos métodos y las devoluciones de llamada en nombre de dos actores (*ActorId1* y *ActorId2*) que pertenecen toothis actor tipo.

![Acceso y simultaneidad basada en turnos de tiempo de ejecución de Reliable Actors][1]

Este diagrama sigue estas convenciones:

* Cada línea vertical muestra el flujo lógico de Hola de ejecución de un método o una devolución de llamada en nombre de un actor determinado.
* se producen eventos de Hello marcados en cada línea vertical en orden cronológico, con los eventos más recientes que se producen por debajo de los antiguos.
* Se usan colores diferentes para las escalas de tiempo correspondiente toodifferent actores.
* Resaltado es duración de hello tooindicate usado para qué Hola se mantiene el bloqueo por actor en nombre de un método o una devolución de llamada.

Algunos tooconsider puntos importantes:

* Mientras *Method1* se está ejecutando en nombre de *ActorId2* en la solicitud de respuesta tooclient *xyz789*, otra solicitud de cliente (*abc123*) llega que también requiere *Method1* toobe ejecutado por *ActorId2*. Sin embargo, Hola segunda ejecución de *Method1* no comienza hasta que haya finalizado la ejecución anterior de Hola. Del mismo modo, se registra un aviso por *ActorId2* se activa al *Method1* se está ejecutando en la solicitud de respuesta tooclient *xyz789*. devolución de llamada de recordatorio Hello se ejecuta una solo después de las ejecuciones de *Method1* están completos. Todo esto es debido a simultaneidad basada en tooturn que se exige para *ActorId2*.
* Del mismo modo, también se aplica la simultaneidad basada en Activar para *ActorId1*, como se muestra mediante la ejecución de Hola de *Method1*, *Method2*, y Hola de devolución de llamada de temporizador en nombre de *ActorId1* ocurre en un modo serie.
* La ejecución de *Method1* en nombre de *ActorId1* se superpone con su ejecución en nombre de *ActorId2*. Esto es así porque solo se exige la simultaneidad basada en turnos dentro de un actor y no para todos los actores.
* En algunas de las ejecuciones de devolución de llamada/método hello, Hola `Task`(C#) o `CompletableFuture`(Java) devuelto por Hola/devolución de llamada de método termina después de que vuelva el método hello. En otros, la operación asincrónica de Hola ya ha terminado por tiempo Hola Hola método/devolución de llamada devuelve. En ambos casos, se libera el bloqueo por actor Hola solo después de que devuelve ambos método/devolución de llamada de Hola y Hola de operación asincrónica finalice.

#### <a name="reentrancy"></a>Reentrada
en tiempo de ejecución de Hello actores permite reentrada de forma predeterminada. Esto significa que si un método de actor de *Actor A* llama a un método en *Actor B*, que a su vez llama a otro método en *Actor A*, que se permite método toorun. Esto es porque es parte de hello mismo contexto de cadena de llamada lógico. Todas las llamadas de temporizador y un aviso iniciar con el nuevo contexto de llamada lógico Hola. Vea hello [reentrada Reliable Actors](service-fabric-reliable-actors-reentrancy.md) para obtener más detalles.

#### <a name="scope-of-concurrency-guarantees"></a>Ámbito de garantías de simultaneidad
en tiempo de ejecución de Hello actores proporciona estas garantías de simultaneidad en situaciones donde controla la invocación de Hola de estos métodos. Por ejemplo, proporciona estas garantías para las invocaciones de método de Hola que se efectúan en la solicitud de cliente de respuesta tooa, así como para las devoluciones de llamada de temporizador y un aviso. Sin embargo, si el código de hello actor invoca directamente estos métodos fuera de los mecanismos de hello proporcionados por el tiempo de ejecución de hello actores, hello en tiempo de ejecución no puede proporcionar las garantías de simultaneidad. Por ejemplo, si se invoca el método hello en contexto de Hola de algunas tareas que no esté asociado con la tarea hello devuelto por métodos de actor hello, hello en tiempo de ejecución no proporciona garantías de simultaneidad. Si se invoca el método hello desde un subproceso actor Hola crea por sí mismo, a continuación, en tiempo de ejecución de hello también proporcionan garantías de simultaneidad. Por lo tanto, deben usar los actores de operaciones en segundo plano tooperform, [temporizadores de actor y recordatorios de actor](service-fabric-reliable-actors-timers-reminders.md) que respeta la simultaneidad basada en el turno.

## <a name="next-steps"></a>Pasos siguientes
* Para empezar, cree su primer servicio de Reliable Actors:
   * [Introducción a Reliable Actors en .NET](service-fabric-reliable-actors-get-started.md)
   * [Introducción a Reliable Actors en Java](service-fabric-reliable-actors-get-started-java.md)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-introduction/concurrency.png
[2]: ./media/service-fabric-reliable-actors-introduction/distribution.png
[3]: ./media/service-fabric-reliable-actors-introduction/actor-communication.png
