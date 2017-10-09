---
title: aaaService Bus con .NET y AMQP 1.0 | Documentos de Microsoft
description: Uso de Azure Service Bus desde .NET con AMQP
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>Uso de Service Bus desde .NET con AMQP 1.0

## <a name="downloading-hello-service-bus-sdk"></a>Descargar Hola SDK del Bus de servicio

Compatibilidad con AMQP 1.0 está disponible en hello versión 2.1 o posterior del SDK de Bus de servicio. Puede asegurarse de que tiene versión más reciente de hello mediante la descarga de bits de Bus de servicio de Hola de [NuGet][NuGet].

## <a name="configuring-net-applications-toouse-amqp-10"></a>Configurar aplicaciones de .NET toouse AMQP 1.0

De forma predeterminada, biblioteca de cliente de .NET de Bus de servicio de Hola se comunica con hello servicio de Bus de servicio mediante un protocolo dedicado basado en SOAP. toouse AMQP 1.0 en lugar de protocolo predeterminado de hello requiere una configuración explícita en la cadena de conexión de Bus de servicio de hello, como se describe en la sección siguiente Hola. Aparte de este cambio, el código de la aplicación permanece invariable al utilizar AMQP 1.0.

En la versión actual de hello, hay algunas características de la API que no son compatibles cuando se usa AMQP. Estas características no compatibles se enumeran más adelante en la sección de hello [no admite características, restricciones y diferencias de comportamiento](#unsupported-features-restrictions-and-behavioral-differences). Algunos de los ajustes de configuración avanzada de hello también tienen un significado diferente al usar AMQP.

### <a name="configuration-using-appconfig"></a>Configuración mediante App.config

Es recomendable para los valores de toostore del archivo de configuración de aplicaciones toouse Hola App.config. Para las aplicaciones de Bus de servicio, puede usar la cadena de conexión de Bus de servicio de App.config toostore Hola. A continuación se muestra un archivo App.config de ejemplo:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

Hola valo hello `Microsoft.ServiceBus.ConnectionString` configuración es la cadena de conexión de Bus de servicio de Hola que es usado tooconfigure Hola conexión tooService Bus. formato de Hello es el siguiente:

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

Donde `[namespace]` y `SharedAccessKey` se obtienen de hello [portal de Azure] [ Azure portal] cuando se crea un espacio de nombres de Bus de servicio. Para obtener más información, consulte [crear un espacio de nombres de Bus de servicio mediante el portal de Azure de hello][Create a Service Bus namespace using hello Azure portal].

Al usar AMQP, anexe la cadena de conexión de hello con `;TransportType=Amqp`. Esta notación indica toomake de biblioteca de cliente de hello su tooService conexión Bus mediante AMQP 1.0.

## <a name="message-serialization"></a>Serialización de mensajes

Cuando se usa el protocolo predeterminado de hello, comportamiento de serialización predeterminado de Hola de biblioteca de cliente de .NET de hello es hello de toouse [DataContractSerializer] [ DataContractSerializer] escriba tooserialize una [BrokeredMessage ] [ BrokeredMessage] instancia para el transporte entre la biblioteca de cliente de Hola y Hola servicio service Bus. Al utilizar el modo de transporte AMQP de hello, biblioteca de cliente de hello usa el sistema de tipos AMQP de hello para la serialización de hello [mensaje negociado] [ BrokeredMessage] en un mensaje AMQP. Esta serialización permite toobe de mensaje de Hola reciba e interprete por una aplicación receptora que potencialmente se ejecuta en una plataforma diferente, por ejemplo, una aplicación de Java que use Hola API de JMS tooaccess Bus de servicio.

Al construir un [BrokeredMessage] [ BrokeredMessage] instancia, puede proporcionar un objeto .NET como un tooserve de constructor de parámetro toohello como cuerpo del mensaje Hola de mensaje de bienvenida. Para los objetos que pueden ser tipos primitivos tooAMQP asignada, cuerpo de Hola se serializa en tipos de datos AMQP. Si el objeto de hello no se puede asignar directamente a un tipo primitivo de AMQP; es decir, se serializa un tipo personalizado definido por la aplicación hello y, a continuación, el objeto de hello mediante hello [DataContractSerializer][DataContractSerializer], y se envían los bytes de hello serializado en un mensaje de datos AMQP.

toofacilitate interoperabilidad con clientes que no sean. NET, use solo los tipos de .NET que se pueden serializar directamente en tipos AMQP para el cuerpo de Hola de mensaje de bienvenida. Hello en la tabla siguiente detalla esos tipos y el sistema de hello correspondiente asignación toohello AMQP tipo.

| Tipo de objeto de cuerpo de .NET | Tipo de AMQP asignado | Tipo de sección de cuerpo de AMQP |
| --- | --- | --- |
| booleano |boolean |Valor de AMQP |
| byte |ubyte |Valor de AMQP |
| ushort |ushort |Valor de AMQP |
| uint |uint |Valor de AMQP |
| ulong |ulong |Valor de AMQP |
| sbyte |byte |Valor de AMQP |
| short |short |Valor de AMQP |
| int |int |Valor de AMQP |
| long |long |Valor de AMQP |
| float |float |Valor de AMQP |
| double |double |Valor de AMQP |
| decimal |decimal128 |Valor de AMQP |
| char |char |Valor de AMQP |
| DateTime |timestamp |Valor de AMQP |
| Guid |uuid |Valor de AMQP |
| byte[] |binary |Valor de AMQP |
| string |string |Valor de AMQP |
| System.Collections.IList |list |Valor AMQP: elementos contenidos en la colección de hello solo pueden ser los que se definen en esta tabla. |
| System.Array |array |Valor AMQP: elementos contenidos en la colección de hello solo pueden ser los que se definen en esta tabla. |
| System.Collections.IDictionary |map |Valor AMQP: elementos contenidos en la colección de hello solo pueden ser los que se definen en esta tabla. Nota: se admiten sólo las claves de cadena. |
| Identificador URI |Se describe la cadena (vea hello en la tabla siguiente) |Valor de AMQP |
| Datetimeoffset |Longitud descrita (vea hello en la tabla siguiente) |Valor de AMQP |
| TimeSpan |Longitud descrita (vea la siguiente hello) |Valor de AMQP |
| Stream |binary |Datos de AMQP (pueden ser varios) secciones de datos de Hello contienen bytes sin formato Hola leídos del objeto de secuencia de Hola. |
| Otro objeto |binary |Datos de AMQP (pueden ser varios) Contiene binarios Hola serializado del objeto de Hola que usa Hola DataContractSerializer o un serializador suministrado por la aplicación hello. |

| Tipo .NET | Mapped AMQP Described Type | Notas |
| --- | --- | --- |
| Identificador URI |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |Uri.AbsoluteUri |
| Datetimeoffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| TimeSpan |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>Características no admitidas, restricciones y diferencias de comportamiento

Hola siguientes características del programa Hola a API de .NET de Bus de servicio no se admite actualmente al usar AMQP:

* Transacciones
* Envío a través de un destino de transferencia

También hay algunas pequeñas diferencias en el comportamiento de Hola de hello API de .NET de Bus de servicio al usar AMQP, protocolo de toohello comparados predeterminado:

* Hola [OperationTimeout] [ OperationTimeout] propiedad se omite.
* `MessageReceiver.Receive(TimeSpan.Zero)` se implementa como `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`.
* Finalización de mensajes mediante tokens de bloqueo solo puede realizarse mediante los receptores de mensajes de Hola que inicialmente se reciben mensajes de saludo.

## <a name="controlling-amqp-protocol-settings"></a>Control de la configuración del protocolo AMQP

Hola [API de .NET](/dotnet/api/) exponer varios valores toocontrol Hola comportamiento de hello protocolo AMQP:

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**: controles Hola crédito inicial que se aplica tooa vínculo. Hola predeterminado es 0.
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**: tamaño del marco de controles Hola máximo AMQP ofrecido durante la negociación de hello en el momento de abrir la conexión. valor predeterminado de Hello es 65.536 bytes.
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**: si las transferencias se pueden definir por lotes, este valor determina retraso máximo de hello las disposiciones de envío. Heredado por remitentes/receptores de forma predeterminada. Remitente/receptor individual puede invalidar el valor predeterminado de hello, que es de 20 milisegundos.
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)**: controla si las conexiones de AMQP se establecen a través de una conexión SSL. valor predeterminado de Hello es **true**.

## <a name="next-steps"></a>Pasos siguientes

¿Toolearn listo más? Visite Hola siguientes vínculos:

* [Información general sobre AMQP para Service Bus]
* [Compatibilidad de AMQP 1.0 con los temas y las colas con particiones de Service Bus]
* [AMQP de Service Bus para Windows Server]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[Información general sobre AMQP para Service Bus]: service-bus-amqp-overview.md
[Compatibilidad de AMQP 1.0 con los temas y las colas con particiones de Service Bus]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP de Service Bus para Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
