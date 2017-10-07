---
title: las aplicaciones de Azure Service Bus de aaaInsulating frente a desastres e interrupciones | Documentos de Microsoft
description: "Describe técnicas que puede usar las aplicaciones de tooprotect frente a una posible interrupción de Bus de servicio."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 349b4968456c9f15375753d83495246f5a3ddfdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>Procedimientos recomendados para aislar aplicaciones ante desastres e interrupciones de Bus de servicio
Las aplicaciones críticas deben funcionar de manera continua, incluso en presencia de Hola de interrupciones o desastres imprevistos. En este tema se describe técnicas que puede usar las aplicaciones de Bus de servicio de tooprotect frente a un desastre o una interrupción del servicio posibles.

Una interrupción del servicio se define como indisponibilidad temporal de Hola de Bus de servicio de Azure. interrupción de Hello puede afectar a algunos componentes de Bus de servicio, como el almacén de mensajería o incluso Hola todo el centro de datos. Una vez resuelto el problema de hello, Bus de servicio vuelve a estar disponible. Normalmente, una interrupción no provoca la pérdida de mensajes ni otros datos. Un ejemplo de un error de componente es indisponibilidad de Hola de un almacén de mensajería determinado. Un ejemplo de una interrupción de todo el centro de datos es un error de alimentación del centro de datos de Hola o un conmutador de red defectuoso del centro de datos. Una interrupción puede durar desde unos tooa minutos pocos días.

Un desastre se define como la pérdida permanente de Hola de una unidad de escala de Bus de servicio o el centro de datos. Centro de datos de Hello puede o puede no estar disponible de nuevo. Normalmente, un desastre provoca la pérdida de algunos o todos los mensajes u otros datos. Algunos ejemplos de desastres son los incendios, las inundaciones o los terremotos.

## <a name="current-architecture"></a>Arquitectura actual
Bus de servicio usa varios almacenes toostore mensajes de mensajería se envían tooqueues o temas. Una cola sin particiones o tema se asigna tooone almacén de mensajes. Si este almacén de mensajería no está disponible, se producirá un error en todas las operaciones de esa cola o tema.

Todas las entidades de mensajería de Service Bus (colas, temas, retransmisiones) residen en un espacio de nombres de servicio, asociado con un centro de datos. Bus de servicio no habilita la replicación geográfica automática de datos, ni tampoco permite un espacio de nombres toospan varios centros de datos.

## <a name="protecting-against-acs-outages"></a>Protección contra interrupciones de ACS
Si está usando credenciales de ACS y este deja de estar disponible, los clientes ya no pueden obtener tokens. Los clientes que tienen un token en tiempo de hello que ACS deja de funcionar pueden continuar toouse Bus de servicio hasta que expiran los tokens de Hola. duración del token Hola predeterminado es de 3 horas.

tooprotect contra los cortes de ACS, use tokens de firma de acceso compartido (SAS). En este caso, cliente hello autentica directamente con el Bus de servicio mediante la firma de un token autogenerado con una clave secreta. Llamadas tooACS ya no son necesarias. Para obtener más información sobre los tokens SAS, consulte [Autenticación y autorización de Service Bus][Service Bus authentication].

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>Protección de colas y temas contra errores en el almacén de mensajería
Una cola sin particiones o tema se asigna tooone almacén de mensajes. Si este almacén de mensajería no está disponible, se producirá un error en todas las operaciones de esa cola o tema. A particiones cola en hello en otra parte, consta de varios fragmentos. Cada fragmento se guarda en un almacén de mensajería diferente. Cuando se envía un mensaje tooa cola o tema particionado, Service Bus asigna tooone de mensaje Hola de fragmentos de Hola. Si no está disponible el almacén de mensajería correspondiente hello, Bus de servicio escribe otro fragmento de hello mensaje tooa, si es posible. Para obtener más información sobre las entidades con particiones, consulte [Entidades de mensajería con particiones][Partitioned messaging entities].

## <a name="protecting-against-datacenter-outages-or-disasters"></a>Protección contra desastres o interrupciones del centro de datos
tooallow para una conmutación por error entre dos centros de datos, puede crear un espacio de nombres del servicio de Bus de servicio en cada centro de datos. Hola, por ejemplo, el espacio de nombres de servicio de Bus de servicio **contosoPrimary.servicebus.windows.net** es posible que encuentre en la región Norte/Central de Estados Unidos de hello, y **contosoSecondary.servicebus.windows.net**podría encontrarse en la región sur/Central nos de Hola. Si una entidad de mensajería de Service Bus debe permanecer accesible en presencia de Hola de una interrupción del centro de datos, puede crear esa entidad en ambos espacios de nombres.

Para obtener más información, vea Hola sección "Error de Bus de servicio dentro de un centro de datos de Azure" [asincrónica de alta disponibilidad y patrones de mensajería][Asynchronous messaging patterns and high availability].

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>Protección de los extremos de retransmisión contra desastres o interrupciones del centro de datos
Replicación geográfica de extremos de retransmisión permite que un servicio que expone un toobe de extremo de retransmisión accesible en presencia de Hola de interrupciones del Bus de servicio. servicio de Hola tooachieve replicación geográfica, debe crear dos extremos de retransmisión en diferentes espacios de nombres. espacios de nombres de Hello deben residir en distintos centros de datos y Hola dos extremos deben tener nombres diferentes. Por ejemplo, se puede acceder a un punto de conexión principal en **contosoPrimary.servicebus.windows.net/myPrimaryService**, mientras que su equivalente secundario resulta accesible en **contosoSecondary.servicebus.windows.net/mySecondaryService**.

el servicio de Hello, a continuación, escucha en ambos extremos y un cliente puede invocar el servicio de Hola a través de cualquier punto de conexión. Una aplicación cliente aleatoriamente elige uno de hello retransmisiones como extremo principal de Hola y envía su extremo activo toohello de solicitud. Si se produce un error en la operación de hello con un código de error, este error indica que ese extremo de retransmisión hello no está disponible. aplicación Hello abre un extremo de copia de seguridad de canal toohello y vuelve a solicitud de saludo. En ese momento Hola active y extremos de reserva de hello intercambian sus roles: aplicación de cliente de hello considera Hola antiguo extremo activo toobe Hola nuevo extremo de copia de seguridad y toobe de extremo de reserva anterior de Hola Hola nuevo extremo activo. Si ambas operaciones producen un error, roles de Hola de dos entidades de hello permanecen sin cambios y se devuelve un error.

Hola [replicación geográfica con Bus de servicio retransmite mensajes] [ Geo-replication with Service Bus relayed Messages] ejemplo muestra cómo se retransmite tooreplicate.

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>Protección de colas y temas contra desastres o interrupciones del centro de datos
tooachieve resistencia frente a interrupciones del centro de datos cuando se usa mensajería asíncrona, Bus de servicio admite dos métodos: *active* y *pasivo* replicación. Para cada enfoque, si una determinada cola o tema debe permanecer accesible en presencia de Hola de una interrupción del centro de datos, puede crearlo en ambos espacios de nombres. Ambas entidades pueden tener Hola mismo nombre. Por ejemplo, se puede acceder a una cola principal en **contosoPrimary.servicebus.windows.net/myQueue**, mientras que su equivalente secundaria resulta accesible en **contosoSecondary.servicebus.windows.net/myQueue**.

Si la aplicación hello no requiere comunicación permanente de remitente al receptor, aplicación hello puede implementar una cola del lado cliente duradera tooprevent pérdida y tooshield Hola remitente del mensaje de los errores transitorios de Bus de servicio.

## <a name="active-replication"></a>Replicación activa
La replicación activa usa entidades en ambos espacios de nombres para cada operación. Cualquier cliente que envía un mensaje envía dos copias de hello mismo mensaje. Hola primera copia se envía la entidad primaria toohello (por ejemplo, **contosoPrimary.servicebus.windows.net/sales**), y la segunda copia del mensaje de bienvenida de Hola se envía la entidad secundaria toohello (por ejemplo,  **contosoSecondary.servicebus.windows.net/sales**).

Un cliente recibe mensajes de ambas colas. procesos de receptor de Hola Hola primera copia de un mensaje, y se suprime la segunda copia de Hola. toosuppress mensajes duplicados, el remitente de hello debe etiquetar cada mensaje con un identificador único. Ambas copias del mensaje de saludo deben estar etiquetados con hello mismo identificador. Puede usar hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] o [BrokeredMessage.Label] [ BrokeredMessage.Label] propiedades, o un hello de tootag de propiedad personalizada Mensaje. receptor de Hello debe mantener una lista de mensajes que ya ha recibido.

Hola [replicación geográfica con mensajes asíncronos del Bus de servicio] [ Geo-replication with Service Bus Brokered Messages] muestra la replicación activa de entidades de mensajería.

> [!NOTE]
> enfoque de Hello replicación activa dobla el número de Hola de operaciones, por lo tanto, este enfoque puede suponer toohigher costo.
> 
> 

## <a name="passive-replication"></a>Replicación pasiva
En caso de hello sin errores, replicación pasiva solo usa una de dos entidades de mensajería Hola. Un cliente envía la entidad activa de hello mensaje toohello. Si se produce un error en la operación de hello en entidad activa Hola con un código de error que indica el centro de datos de Hola que entidad activa de hosts Hola podría no estar disponible, el cliente de hello envía una copia de la entidad de seguridad de toohello de mensaje de Hola. En ese momento Hola activa y las entidades de copia de seguridad de hello intercambian sus roles: Hola antigua entidad activa toobe Hola nueva entidad de seguridad considera que el cliente remitente hello y entidad de seguridad anterior de hello es la nueva entidad activa de Hola. Si ambas operaciones producen un error, roles de Hola de dos entidades de hello permanecen sin cambios y se devuelve un error.

Un cliente recibe mensajes de ambas colas. Porque no hay posibilidad de dicho receptor Hola recibe dos copias del mismo mensaje, hello de hello receptor debe suprimir los mensajes duplicados. Puede suprimir duplicados en hello misma forma en que se ha descrito para la replicación activa.

En general, la replicación pasiva es más económica que la activa porque en la mayoría de los casos se realiza una única operación. Latencia, el rendimiento y coste económico son idénticos toohello no replicada escenario.

Cuando se utiliza la replicación pasiva, Hola mensajes de los escenarios siguientes se pueden perder o recibirse dos veces:

* **Pérdida o retraso de mensaje**: suponga que remitente Hola enviado correctamente una cola de mensajes m1 toohello principal, y, a continuación, cola de hello deja de estar disponible antes de que el receptor de hello reciba m1. remitente de Hello envía una cola de mensajes posteriores m2 toohello secundaria. Si la cola principal hello no está disponible temporalmente, receptor Hola recibe m1 después de cola de hello vuelva a estar disponible. En el caso de un desastre, es no posible que receptor Hola nunca reciba m1.
* **Recepción duplicada**: suponga ese remitente Hola envía una cola principal de mensaje m toohello. Bus de servicio correctamente procesa m, pero se produce un error toosend una respuesta. Una vez Hola enviar agota el tiempo de operación, remitente Hola envía una copia idéntica de la cola de m toohello secundaria. Si receptor Hola primera copia de Hola de tooreceive capaz de m antes de cola de hello principal deja de estar disponible, receptor Hola recibe ambas copias de m en aproximadamente Hola mismo tiempo. Si receptor hello no es primera copia de Hola de tooreceive capaz de m antes de cola de hello principal deja de estar disponible, receptor Hola recibe inicialmente solo Hola segunda copia de m, pero, a continuación, recibe una segunda copia de m cuando la cola principal Hola deja de estar disponible.

Hola [replicación geográfica con Bus de servicio asíncrona mensajes] [ Geo-replication with Service Bus Brokered Messages] ejemplo muestra la replicación pasiva de entidades de mensajería.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la recuperación ante desastres, vea estos artículos:

* [Continuidad de negocio de SQL Database de Azure][Azure SQL Database Business Continuity]
* [Diseño de aplicaciones resistentes de Azure][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[Geo-replication with Service Bus Relayed Messages]: http://code.msdn.microsoft.com/Geo-replication-with-16dbfecd
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: http://code.msdn.microsoft.com/Geo-replication-with-f5688664
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
