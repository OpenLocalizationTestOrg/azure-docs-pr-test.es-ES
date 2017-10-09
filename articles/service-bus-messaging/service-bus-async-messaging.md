---
title: "mensajería asíncrona del Bus aaaService | Documentos de Microsoft"
description: "Descripción de la mensajería asincrónica de Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>Patrones de mensajería asincrónica y alta disponibilidad

La mensajería asincrónica se puede implementar de varias maneras. Con colas, temas y suscripciones, Azure Service Bus admite la asincronía a través de un mecanismo de almacenamiento y reenvío. Durante el funcionamiento normal (sincrónico), enviar temas y tooqueues de mensajes y recibir mensajes de colas y suscripciones. Las aplicaciones que escriba dependen de que estas entidades estén siempre disponibles. Cuando cambia el estado de la entidad de hello, debido tooa variedad de circunstancias, es necesario un tooprovide forma una entidad de capacidad reducida que pueda satisfacer la mayoría de las necesidades.

Las aplicaciones normalmente utilizan tooenable de patrones de mensajería asincrónica un número de escenarios de comunicación. Puede crear aplicaciones en el que los clientes pueden enviar mensajes tooservices, incluso cuando no se está ejecutando el servicio de Hola. Las aplicaciones que presentan ráfagas de comunicaciones, una cola puede ayudar a nivel Hola carga proporcionando una lugar las comunicaciones toobuffer. Por último, puede obtener una carga simple pero eficaz mensajes de toodistribute equilibrador entre varias máquinas.

En orden toomaintain la disponibilidad de cualquiera de estas entidades, considere la posibilidad de varias maneras diferentes en que estas entidades pueden aparecer no disponibles para un sistema de mensajería duradero. Por lo general, vemos entidad Hola se convierten en tooapplications disponible que escribimos de hello después de maneras diferentes:

* No se puede toosend mensajes.
* No se puede tooreceive mensajes.
* No se puede toomanage entidades (crear, recuperar, actualizar o eliminar entidades).
* Servicio de hello toocontact no se puede.

Para cada uno de estos errores, distintos modos de error hay que habilitar un trabajo de aplicación toocontinue tooperform en algún nivel de capacidad reducida. Por ejemplo, un sistema que puede enviar mensajes, pero no recibirlos, puede recibir pedidos de clientes pero no procesarlos. En este tema se tratan los posibles problemas que se pueden producir y cómo se mitigan. Bus de servicio ha presentado a una serie de procedimientos para mitigar problemas que deben participar en y, en este tema también explica hello las reglas que rigen Hola usan de esas mitigaciones participar en.

## <a name="reliability-in-service-bus"></a>Confiabilidad en Service Bus
Hay varias maneras de problemas de mensajes y entidad toohandle y hay directrices que rigen el uso adecuado de Hola de esas mitigaciones. directrices de hello toounderstand, primero debe entender lo que puede producir un error en el Bus de servicio. Pagar toohello diseño de los sistemas de Azure, todos estos problemas suelen toobe corta duración. En un nivel alto, distintas causas de falta de disponibilidad de hello aparecerán como sigue:

* Limitación desde un sistema externo del que depende Service Bus. Se produce una limitación de las interacciones con los recursos de proceso y almacenamiento.
* Problema en un sistema del que depende Service Bus. Por ejemplo, pueden aparecer problemas en una parte determinada del almacenamiento.
* Error de Service Bus en un subsistema individual. En esta situación, un nodo de proceso puede entrar en un estado incoherente y debe reiniciarse, haciendo que todas las entidades usa equilibrio tooload tooother nodos. A su vez, esto puede provocar que los mensajes se procesen más lentamente durante un breve periodo.
* Error de Service Bus en un centro de datos de Azure. Se trata de un "error catastrófico" durante el cual, sistema de hello es inalcanzable durante muchos minutos o unas pocas horas.

> [!NOTE]
> término de Hello **almacenamiento** puede significar almacenamiento de Azure y SQL Azure.
> 
> 

Service Bus contiene varios procedimientos para mitigar estos problemas. Hola las secciones siguientes tratan cada problema y sus respectivos procedimientos para solucionarlos.

### <a name="throttling"></a>Limitaciones
Con Service Bus, la limitación permite la administración cooperativa de la velocidad de los mensajes. Cada nodo individual de Service Bus alberga muchas entidades. Cada una de esas entidades realiza demandas en sistema de hello en cuanto a CPU, memoria, almacenamiento y otras facetas. Si cualquiera de estas facetas detecta un uso que supera los umbrales definidos, Service Bus puede denegar una solicitud determinada. Hola llamador recibe una [ServerBusyException] [ ServerBusyException] y reintentos después de 10 segundos.

Como una mitigación, código de hello debe leer error hello y detener los reintentos del mensaje de bienvenida de al menos 10 segundos. Puesto que el error de hello puede ocurrir en fragmentos de aplicación de cliente de hello, se espera que cada pieza de forma independiente ejecuta lógica de reintento de Hola. código de Hello puede reducir la probabilidad de Hola de limitarse al habilitar la creación de particiones en una cola o tema.

### <a name="issue-for-an-azure-dependency"></a>Problema en una dependencia de Azure
Otros componentes de Azure en ocasiones pueden tener problemas de servicio ocasionalmente. Por ejemplo, cuando se actualiza un sistema que usa Service Bus, dicho sistema puede experimentar temporalmente la reducción de sus funcionalidades. toowork alrededor de estos tipos de problemas, Service Bus con regularidad investiga e implementa las mitigaciones. Aparecen los efectos secundarios de estas mitigaciones. Por ejemplo, toohandle transitorio problemas con el almacenamiento, Bus de servicio implementa un sistema que permite toowork de operaciones de envío de mensaje de forma coherente. Debido a la naturaleza toohello de mitigación de hello, un mensaje enviado puede tardar hasta too15 minutos tooappear en hello afectado cola o suscripción y está listo para una operación de recepción. Por lo general, la mayoría de las entidades no sufrirán este problema. Sin embargo, dado el número de Hola de entidades de Bus de servicio dentro de Azure, esta solución provisional a veces es necesario para un pequeño subconjunto de clientes de Bus de servicio.

### <a name="service-bus-failure-on-a-single-subsystem"></a>Error de Service Bus en un subsistema individual
Con cualquier aplicación, circunstancias pueden hacer que un componente interno de Service Bus toobecome incoherente. Al Bus de servicio detecta esto, recopila datos de tooaid de aplicación Hola diagnosticar qué ocurrió. Una vez que se recopilan los datos de hello, aplicación hello es reinicia en un intento tooreturn se tooa de estado coherente. Este proceso tiene lugar con bastante rapidez y resultados en una entidad parezca toobe no está disponible para la tooa varios minutos, aunque típico tiempos de inactividad son mucho más cortas.

En estos casos, se genera la aplicación de cliente de hello un [System.TimeoutException] [ System.TimeoutException] o [MessagingException] [ MessagingException] excepción. Bus de servicio contiene una solución para este problema en forma de Hola de lógica de reintento de cliente automatizada. Una vez que se agota el período de reintento de hello y no se entrega el mensaje de bienvenida, puede explorar con otras características como [emparejar los espacios de nombres][paired namespaces]. Estos espacios de nombres tienen otros riesgos que se describen en este artículo.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Error de Service Bus en un centro de datos de Azure
motivo más probable de Hola de un error en un centro de datos de Azure es una implementación de actualización incorrecta del Bus de servicio o un sistema dependiente. Como Hola plataforma ha madurado, ha disminuido probabilidad Hola de este tipo de error. También puede producir un error en el centro por motivos como Hola siguientes:

* Interrupción del suministro eléctrico (desaparecen la fuente de alimentación y la generación de energía).
* Conectividad (interrupción de Internet entre los clientes y Azure).

En ambos casos, un desastre natural o provocado por el hombre causó el problema de Hola. toowork resolver este problema y asegurarse de que todavía puede enviar mensajes, puede usar [emparejar los espacios de nombres] [ paired namespaces] tooenable mensajes toobe enviado tooa segunda ubicación mientras Hola ubicación principal vuelve a correcto nuevo. Para más información, consulte [Procedimientos recomendados para aislar aplicaciones ante desastres e interrupciones de Service Bus][Best practices for insulating applications against Service Bus outages and disasters].

## <a name="paired-namespaces"></a>Espacios de nombres emparejados
Hola [emparejar los espacios de nombres] [ paired namespaces] característica admite escenarios en los que una entidad de Bus de servicio o implementación en un centro de datos deja de estar disponible. Este evento se produce con poca frecuencia, los sistemas distribuidos todavía deben estar preparados toohandle peores casos posibles. Normalmente, este evento se produce porque algún elemento del que depende Service Bus sufre un problema temporal. disponibilidad de las aplicaciones toomaintain durante una interrupción, los usuarios de Bus de servicio pueden utilizar dos espacios de nombres independientes, preferiblemente en centros de datos independientes, toohost sus entidades de mensajería. resto de Hola de esta sección utiliza Hola siguiente terminología:

* Espacio de nombres principal: Hola espacio de nombres con el que interactúa la aplicación de envío y las operaciones de recepción.
* Espacio de nombres secundario: Hola espacio de nombres que actúa como un espacio de nombres principal toohello copia de seguridad. La lógica de la aplicación no interactúa con este espacio de nombres.
* Intervalo de conmutación por error: cantidad de Hola de errores normales de tooaccept de tiempo antes de la aplicación hello cambia del espacio de nombres secundario de hello espacio de nombres principal toohello.

Los espacios de nombres emparejados admiten la *disponibilidad de envío*. Enviar mensajes de Hola capacidad toosend conserva la disponibilidad. disponibilidad de envío toouse, la aplicación debe cumplir Hola según los requisitos:

1. Solo se reciben mensajes de Hola espacio de nombres principal.
2. Dada la cola o tema de tooa de mensajes enviados puede llegar desordenados.
3. Los mensajes de una sesión pueden llegar desordenados. Esto no es algo habitual en el funcionamiento normal de las sesiones, Esto significa que la aplicación usa toologically agrupar mensajes de las sesiones.
4. Solo se mantiene el estado de sesión en el espacio de nombres principal Hola.
5. cola principal Hola puede ponerse en línea y empezar a Aceptar mensajes antes de que la cola secundaria Hola ofrece todos los mensajes en cola principal Hola.

Hola las secciones siguientes tratan Hola API, cómo se implementan las API de Hola y muestra código de ejemplo que usa la característica de Hola. Tenga en cuenta que esta característica tiene asociadas unos costos.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>Hola API de MessagingFactory.PairNamespaceAsync
característica de espacios de nombres emparejados Hola incluye hello [PairNamespaceAsync] [ PairNamespaceAsync] método en hello [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] clase:

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Cuando se completa la tarea hello, Hola emparejamiento del espacio de nombres también es tooact al completo y listo para cualquier [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], o [TopicClient] [ TopicClient] creado con hello [MessagingFactory] [ MessagingFactory] instancia. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] es la clase de base de Hola para hello diferentes tipos de emparejamiento disponibles con un [MessagingFactory] [ MessagingFactory] objeto. Actualmente, Hola solo clase derivada es una denominada [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], que implementa los requisitos de disponibilidad de envío de Hola. [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions] tiene un conjunto de constructores que se compilan entre sí. Examinando el constructor de hello con hello mayoría de los parámetros, puede conocer Hola comportamiento del programa Hola a otros constructores.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

Estos parámetros tienen Hola siguientes significados:

* *secondaryNamespaceManager*: un inicializado [NamespaceManager] [ NamespaceManager] instancia para el espacio de nombres secundario Hola ese hello [PairNamespaceAsync] [ PairNamespaceAsync] pueden utilizar el método tooset Hola espacio de nombres secundario. Administrador de espacio de nombres de Hello es la lista de Hola de tooobtain usado de colas de espacio de nombres de Hola y toomake seguro de que existen las colas de trabajo pendiente de hello necesario. Si no existen, se crearán. [NamespaceManager] [ NamespaceManager] requiere Hola capacidad toocreate un token con hello **administrar** de notificación.
* *messagingFactory*: Hola [MessagingFactory] [ MessagingFactory] instancia para el espacio de nombres secundario Hola. Hola [MessagingFactory] [ MessagingFactory] objeto es toosend utilizado y, si hello [EnableSyphon] [ EnableSyphon] propiedad se establece demasiado**true** , recibir mensajes desde las colas de trabajo pendiente de Hola.
* *backlogQueueCount*: número de Hola de trabajo pendiente pone en cola toocreate. Este valor debe ser al menos 1. Al enviar el trabajo pendiente de toohello de mensajes, se elige aleatoriamente una de estas colas. Si establece Hola valor too1, sólo una cola nunca puede utilizarse. Cuando esto sucede y cola de hello un pedido pendiente genera errores, el cliente de hello no es capaz de tootry una cola de pedidos pendientes diferente y puede producir un error toosend el mensaje. Se recomienda establecer este valor toosome mayor valor y predeterminado Hola valor too10. Puede cambiar este tooa superior o la aplicación envía a un valor inferior según la cantidad de datos por día. Cada cola de trabajos pendientes puede contener una too5 GB de mensajes.
* *failoverInterval*: Hola cantidad de tiempo durante los cuales aceptará errores en el espacio de nombres principal Hola antes de cambiar cualquier entidad única a través del espacio de nombres secundario toohello. Las conmutaciones por error se producen entidad por entidad. Con frecuencia,  las entidades de un espacio de nombres individual residen en nodos diferentes de Service Bus. Un error en una de las entidades no implica un error en otra. Puede establecer este valor demasiado[System.TimeSpan.Zero] [ System.TimeSpan.Zero] toofailover toohello secundaria inmediatamente después de su primer error no transitorio. Los errores que desencadenan el temporizador de conmutación por error de hello son cualquiera [MessagingException] [ MessagingException] en qué hello [IsTransient] [ IsTransient] propiedad es false, o un [System.TimeoutException][System.TimeoutException]. Otras excepciones como [UnauthorizedAccessException] [ UnauthorizedAccessException] hacen que la conmutación por error, porque indican que el cliente hello está configurado incorrectamente. A [ServerBusyException] [ ServerBusyException] no causa conmutación por error porque es de procedimiento correcto de hello toowait 10 segundos, a continuación, enviar mensaje de bienvenida de nuevo.
* *enableSyphon*: indica que este emparejamiento concreto también debe desviar mensajes del espacio de nombres principal de hello espacio de nombres secundario toohello atrás. En general, las aplicaciones que envían mensajes deben establecer este valor demasiado**false**; las aplicaciones que reciben mensajes deben establecer este valor demasiado**true**. motivo Hello es que con frecuencia, hay menos receptores de mensajes que remitentes. Según el número de Hola de destinatarios, puede elegir toohave un deberes de sifón única aplicación Hola de identificador de instancia. El uso de muchos destinatarios conlleva costos por cada cola de trabajos pendientes.

toouse Hola código, cree un elemento principal [MessagingFactory] [ MessagingFactory] instancia, una base de datos secundaria [MessagingFactory] [ MessagingFactory] instancia, una base de datos secundaria [NamespaceManager] [ NamespaceManager] instancia y un [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] instancia. llamada de Hello puede ser tan simple como siguiente hello:

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Hola cuando la tarea devuelta por hello [PairNamespaceAsync] [ PairNamespaceAsync] método finaliza, todo está configurado y listo toouse. Antes de que se devuelva la tarea hello, que no ha completado todos de trabajo en segundo plano Hola necesario para hello emparejamiento toowork derecha. Como resultado, no debería empezar a enviar mensajes hasta que devuelva la tarea hello. Si se produjeron errores, por ejemplo, credenciales no válidas o colas de trabajo pendiente de error toocreate hello, esas excepciones se producirá una vez finalizada la tarea hello. Una vez que se devuelve la tarea hello, compruebe que las colas de Hola se encuentra o se crearon mediante el examen de hello [BacklogQueueCount] [ BacklogQueueCount] propiedad en su [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] instancia. Para el anterior código de hello, esa operación aparece como sigue:

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de mensajería asíncrona de Bus de servicio, conozca más detalles [emparejar los espacios de nombres][paired namespaces].

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
