---
title: "aaaOverview del modelo de programación de servicio confiable del tejido de hello | Documentos de Microsoft"
description: "Obtenga información sobre el modelo de programación de un servicio fiable de Service Fabric y comience a escribir sus propios servicios."
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>Información general sobre Reliable Services
Azure Service Fabric simplifica la escritura y administración de los servicios de Reliable Services con y sin estado. En este tema se explica:

* modelo de programación de servicios de confianza de Hola para servicios sin estado y con estado.
* Opciones de Hello tiene toomake al escribir un servicio confiable.
* Algunos escenarios y ejemplos de cuándo toouse Reliable Services y cómo se escriben.

Servicios de confianza es uno de hello modelos disponibles en el tejido de servicio de programación. Hola otro es el modelo de programación de Actor confiable de hello, que proporciona un modelo de programación de Actor virtual sobre el modelo de servicios de confianza Hola. Para obtener más información sobre el modelo de programación de Reliable Actors hello, consulte [tooService Introducción tejido Reliable Actors](service-fabric-reliable-actors-introduction.md).

Service Fabric administra la duración de hello de servicios, desde el aprovisionamiento y la implementación a través de la actualización y eliminación, tanto a través de [administración de aplicaciones de Service Fabric](service-fabric-deploy-remove-applications.md).

## <a name="what-are-reliable-services"></a>¿Qué son los servicios de Reliable Services?
Servicios de confianza le ofrece una sencilla y eficaz, nivel superior toohelp modelo express ¿qué es importante tooyour aplicación de programación. Con los servicios de confianza Hola modelo de programación, obtendrá:

* Resto de toohello de acceso de hello las API de programación de Service Fabric. A diferencia de los servicios de Fabric de servicio modelada como [invitado ejecutables](service-fabric-deploy-existing-app.md), servicios de confianza obtener rest de hello toouse de hello las API de tejido de servicio directamente. Esto permite a los servicios:
  * Consultar el sistema Hola
  * informe de mantenimiento sobre entidades de clúster de Hola
  * recibir notificaciones sobre los cambios de configuración y de código,
  * buscar otros servicios y comunicarse con ellos,
  * (opcionalmente) utilice hello [colecciones confiable](service-fabric-reliable-services-reliable-collections.md)
  * .. .y concederles acceso toomany otras funciones, todo ello desde un modelo de programación de primera clase en varios lenguajes de programación.
* Un modelo sencillo para ejecutar su propio código parecido a los modelos de programación que está acostumbrado a utilizar. El código tiene un punto de entrada bien definido y un ciclo de vida de fácil administración.
* Un modelo de comunicación acoplable. Utilizar transporte Hola de su elección, como HTTP con [API Web](service-fabric-reliable-services-communication-webapi.md), WebSockets, protocolos TCP personalizados o cualquier otra cosa. Reliable Services proporciona excelentes opciones ya integradas, o puede proporcionar las suyas propias.
* Para los servicios con estado, modelo de programación de servicios confiables Hola permite tooconsistently y almacenar el estado justo dentro de su servicio de forma confiable mediante el uso de [colecciones confiable](service-fabric-reliable-services-reliable-collections.md). Colecciones de confianza son un sencillo conjunto de clases de colección altamente disponible y confiable que estará familiarizado tooanyone que ha utilizado las colecciones de C#. Tradicionalmente, los servicios necesitaban sistemas externos para efectuar la administración de estados de confianza. Con las colecciones de confianza, puede almacenar el equipo de estado siguiente tooyour con hello mismo alta disponibilidad y confiabilidad se haya llegado tooexpect de alta disponibilidad almacenes externos. Este modelo también mejora la latencia porque se están colocar compute de Hola y el estado que necesita toofunction.

Vea este vídeo de Microsoft Virtual Academy para obtener información general de Reliable Services: <center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>¿Qué hace que Reliable Services sea diferente?
Los servicios fiables de Service Fabric son diferentes de los servicios que haya podido escribir previamente. Service Fabric proporciona confiabilidad, disponibilidad, coherencia y escalabilidad.

* **Confiabilidad** : el servicio permanece seguridad incluso en entornos poco confiables donde las máquinas se producirá un error o haga clic en problemas de red, o en casos donde hello servicios por sí mismos encontrar errores y bloqueos o producirá un error. Para los servicios con estado, su estado se conserva incluso en presencia de Hola de red u otros errores.
* **Disponibilidad**: su servicio es accesible y responde. Service Fabric mantiene el número de copias en ejecución deseado.
* **Escalabilidad** : servicios se desacoplan de hardware específico, y puede aumentar o reducir según sea necesario a través de hello adición o eliminación de hardware u otros recursos. Servicios son tooensure fácilmente con particiones (especialmente en el caso de hello con estado) que se puede escalar el servicio de Hola y controlar errores parciales. Servicios se pueden crear y eliminar dinámicamente a través de código, lo cual más toobe instancias Active según sea necesario, diga en las solicitudes de toocustomer de respuesta. Por último, Service Fabric anima a ligero de toobe de servicios. Service Fabric permite miles de servicios toobe aprovisionado dentro de un proceso único, en lugar de requerir o dedicar instancias completas de sistema operativo o de instancia única de tooa de procesos de un servicio.
* **Coherencia** -toda la información almacenada en este servicio puede garantizarse toobe coherente. Esto se cumple incluso con varias colecciones de confianza dentro de un servicio. Pueden realizarse cambios en varias colecciones dentro de un servicio de un modo transaccional pormenorizado.

## <a name="service-lifecycle"></a>Ciclo de vida del servicio
Tanto si el servicio está con estado como sin estado, Reliable Services proporciona un ciclo de vida simple que permite conectar rápidamente el código y empezar a trabajar.  Hay sólo una o dos métodos que necesita tooimplement tooget su servicio activos y en funcionamiento.

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** -este método es donde el servicio Hola define la pila (s) de comunicación de Hola que desea toouse. Hola pila de comunicación, como [API Web](service-fabric-reliable-services-communication-webapi.md), es lo que define Hola extremo de escucha o puntos de conexión para Hola service (cómo los clientes tener acceso servicio hello). También define cómo interactúan los mensajes de Hola que aparecen con el resto de Hola Hola de código de servicio.
* **Coredispatcher** : este método es que el servicio ejecuta su lógica de negocios, y donde debería iniciar las tareas en segundo plano que se deben ejecutar para vida Hola Hola. token de cancelación de Hello proporcionada es una señal para cuándo debe detenerse ese trabajo. Por ejemplo, si servicio Hola necesita toopull mensajes fuera de una cola confiable y procesarlos, esto es donde se produce ese trabajo.

Si está aprendiendo servicios confiables para hello primera vez, siga leyendo. Si desea obtener un tutorial detallado sobre el ciclo de vida de hello de servicios de confianza, puede diríjase demasiado[este artículo](service-fabric-reliable-services-lifecycle.md).

## <a name="example-services"></a>Servicios de ejemplo
Conocer este modelo de programación, echemos un vistazo a cómo encajan estas piezas dos toosee de distintos servicios.

### <a name="stateless-reliable-services"></a>Servicios fiables sin estado
Un servicio sin estado es aquélla en la que no hay ningún estado mantenido dentro de servicio de Hola a través de llamadas. Cualquier estado que esté presente es completamente descartable y no requiere sincronización, replicación, persistencia o alta disponibilidad.

Por ejemplo, considere la posibilidad de una calculadora que no tiene memoria y recibe todos los tooperform de términos y las operaciones a la vez.

En este caso, Hola `RunAsync()` (C#) o `runAsync()` (Java) de hello servicio puede estar vacío, porque no hay ninguna experiencia ese servicio Hola de procesamiento de tareas debe toodo. Cuando se crea el servicio de calculadora de hello, devuelve un `ICommunicationListener` (C#) o `CommunicationListener` (Java) (por ejemplo [API Web](service-fabric-reliable-services-communication-webapi.md)) que se abre un extremo en algún puerto de escucha. Este extremo de escucha se enlaza los métodos de cálculo diferentes toohello (ejemplo: "Add (n1, n2)") que definen la API pública de la calculadora Hola.

Cuando se realiza una llamada desde un cliente, se invoca el método adecuado de hello, y servicio de calculadora de hello realiza operaciones de hello en hello datos proporcionan y devuelve el resultado de hello. No almacena ningún estado.

El hecho de no almacenar ningún estado interno hace que esta calculadora de ejemplo sea sencilla. Pero la mayoría de los servicios no son realmente sin estado. En su lugar, externalizar su toosome estado otro almacén. (Por ejemplo, cualquier aplicación web que se base en mantener el estado de sesión en un almacén de respaldo o una memoria caché no es sin estado).

Un ejemplo común de servicios sin estado cómo se utilizan en Service Fabric es como un front-end que expone Hola API de acceso público para una aplicación web. servicio de front-end de Hello, a continuación, comunica toostateful services toocomplete una solicitud de usuario. En este caso, las llamadas de los clientes son tooa dirigido conocido puerto, como 80, donde está escuchando el servicio sin estado Hola. Este servicio sin estado recibe la llamada de Hola y determina si llamada Hola procede de un usuario de confianza y qué servicio se está destinado.  A continuación, servicio sin estado Hola reenvía toohello de partición correcta del servicio con estado de hello para la llamada hello y espera una respuesta. Cuando el servicio sin estado Hola recibe una respuesta, responde toohello de cliente original. Hay un ejemplo de un servicio como este en nuestras muestras de [C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService). Esto es sólo un ejemplo de este patrón en los ejemplos de hello, hay otras personas en otros ejemplos también.

### <a name="stateful-reliable-services"></a>Servicios fiables con estado
Un servicio con estado es aquel que debe tener alguna parte del estado mantienen coherentes y presente para hello toofunction de servicio. Considere un servicio que calcula constantemente una media acumulada de algún valor basándose en las actualizaciones que recibe. toodo esto, debe tener el conjunto actual de Hola de solicitudes entrantes que necesita tooprocess y Hola promedio actual. Cualquier servicio que recupera, procesa y almacena la información en un almacén externo (por ejemplo, en la actualidad un almacén de tablas o blobs de Azure) es con estado. Solo se mantiene su estado en el almacén de estado externo de Hola.

La mayoría de servicios hoy almacena su estado externamente, ya que el almacén externo de hello es lo que proporciona confiabilidad, disponibilidad, escalabilidad y coherencia de ese estado. En Service Fabric, servicio no es necesario toostore su estado externamente. Tejido de servicio se encarga de estos requisitos para el código del servicio de Hola y el estado del servicio de Hola.

> [!NOTE]
> Linux todavía no es compatible con Reliable Services con estado (para C# o Java).
>

Supongamos que queremos toowrite un servicio que procesa las imágenes. toodo esto, Hola servicio toma una serie de hello y la imagen de conversiones tooperform en esa imagen. Luego devuelve un agente de escucha de comunicación (por ejemplo, una WebAPI) que expone una API como `ConvertImage(Image i, IList<Conversion> conversions)`. Cuando recibe una solicitud, el servicio de hello almacena en un `IReliableQueue`y devuelve algún cliente toohello de Id., por lo que puede realizar el seguimiento de solicitud de Hola.

En este servicio, `RunAsync()` podría ser más complejo. servicio de Hello tiene un bucle dentro de su `RunAsync()` que extrae las solicitudes fuera de `IReliableQueue` y realiza las conversiones de hello solicitadas. resultados de Hello también se almacenan en un `IReliableDictionary` por lo que cuando vuelve a estar cliente hello pueden recibir sus imágenes convertidos. tooensure que incluso si algo va mal imagen hello no se pierde, este servicio confiable podría extraer de la cola de hello, realizar conversiones de Hola y almacenar el resultado de hello todo en una sola transacción. En este caso, mensaje de bienvenida se quita de la cola de Hola y resultados de Hola se almacenan en diccionario de resultado de hello solo cuando las conversiones de hello están completos. Como alternativa, servicio Hola podría extraer imágenes hello de la cola de Hola e inmediatamente se almacenan en un almacén remoto. Esto reduce Hola cantidad de servicio de estado de hello tiene toomanage, pero aumenta la complejidad debido a que el servicio de hello tiene tookeep Hola metadatos necesarios toomanage Hola el almacén remoto de. Con estos dos métodos, si se produce un error en solicitud de Hola Hola intermedio permanece en Hola cola espera toobe procesado.

Una toonote algo acerca de este servicio es que parece un servicio de .NET normal. Hello única diferencia es que hello las estructuras de datos que se va a usar (`IReliableQueue` y `IReliableDictionary`) se proporcionan con Service Fabric y son altamente disponibles, confiables y coherentes.

## <a name="when-toouse-reliable-services-apis"></a>Cuando toouse confiable de las API de servicios
Si cualquiera de los siguientes Hola caracterizan a sus necesidades de servicio de aplicación, debe considerar las API de servicios de confianza:

* Desea que el código de su servicio (y, opcionalmente, estado) toobe altamente disponible y confiable
* Necesita garantías transaccionales en varias unidades de estado (por ejemplo, pedidos y artículos de línea de estos).
* El estado de la aplicación puede modelarse naturalmente como Reliable Dictionaries y Queues.
* El código de aplicaciones o estado debe toobe alta disponibilidad con una latencia baja lecturas y escrituras.
* La aplicación necesita la granularidad de las operaciones de transacción o simultaneidad de hello toocontrol a través de una o varias recopilaciones confiable.
* Desea que las comunicaciones de hello toomanage u Hola control esquema para el servicio de creación de particiones.
* El código necesita un entorno de tiempo de ejecución de subproceso libre.
* La aplicación necesita toodynamically crear o destruir diccionarios confiable o las colas o todo servicios en tiempo de ejecución.
* Debe tooprogrammatically proporcionado por el tejido de servicio de copia de seguridad y restauración características de control de estado de su servicio.
* La aplicación necesita toomaintain el historial de cambios de estado de sus unidades.
* Desea toodevelop o utilizar los proveedores de estado personalizado, desarrollado para otros fabricantes.

## <a name="next-steps"></a>Pasos siguientes
* [Introducción a Reliable Services de Service Fabric de Microsoft Azure](service-fabric-reliable-services-quick-start.md)
* [Uso avanzado de Reliable Services](service-fabric-reliable-services-advanced-usage.md)
* [modelo de programación de Hello Reliable Actors](service-fabric-reliable-actors-introduction.md)
