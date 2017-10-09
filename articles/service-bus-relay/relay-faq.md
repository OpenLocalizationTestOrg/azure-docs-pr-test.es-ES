---
title: "Preguntas más frecuentes de retransmisión aaaAzure | Documentos de Microsoft"
description: "Obtener toosome respuestas preguntas más frecuentes acerca de la retransmisión de Azure."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 886d2c7f-838f-4938-bd23-466662fb1c8e
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: ab14431e27df43287940e7d12ea37e4093638d21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-faqs"></a>Preguntas frecuentes sobre Azure Relay

En este artículo se responden algunas preguntas frecuentes sobre [Azure Relay](https://azure.microsoft.com/services/service-bus/). Consulte [Preguntas más frecuentes de soporte técnico de Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para información general sobre los precios y el soporte técnico de Azure.

## <a name="general-questions"></a>Preguntas generales
### <a name="what-is-azure-relay"></a>¿Qué es Relay de Azure?
Hola [servicio de retransmisión de Azure](relay-what-is-it.md) facilita sus aplicaciones híbridas ayudando a más seguros exponer servicios que residen dentro de una nube pública de empresas corporativas red toohello. Puede exponer servicios Hola sin tener que abrir una conexión de firewall y sin necesidad de la infraestructura de red corporativa de tooa cambios intrusivo.

### <a name="what-is-a-relay-namespace"></a>¿Qué es el espacio de nombres de Relay?
A [espacio de nombres](relay-create-namespace-portal.md) es un contenedor de ámbito que puede usar recursos de retransmisión tooaddress dentro de la aplicación. Debe crear una retransmisión de toouse de espacio de nombres. Esto es uno de los primeros pasos de hello en la introducción.

### <a name="what-happened-tooservice-bus-relay-service"></a>¿Qué problema tooService servicio de retransmisión de Bus?
Hola anteriormente denominado servicio de retransmisión de Bus de servicio ahora se denomina retransmisión de WCF. Puede seguir toouse este servicio como de costumbre. característica de las conexiones híbridas de Hello es una versión actualizada de un servicio que se ha trasplantados de los servicios de BizTalk de Azure. Retransmisión de WCF y las conexiones híbridas continúan toobe compatible.

## <a name="pricing"></a>Precios
Permite determinar sección algunas preguntas más frecuentes sobre Hola retransmisión estructura de precios. También puede consultar [Preguntas más frecuentes de soporte técnico de Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para información general sobre los precios de Azure. Para más información sobre los precios de Relay, consulte [Precios de Service Bus][Pricing overview].

### <a name="how-do-you-charge-for-hybrid-connections-and-wcf-relay"></a>¿Cómo se cobra por Conexiones híbridas y WCF Relay?
Para obtener información completa sobre los precios de retransmisión, consulte hello [conexiones híbridas y retransmisiones de WCF] [ Pricing overview] tabla en la página de detalles de precios de hello Bus de servicio. Además los precios toohello indican en la página, se le cobra por las transferencias de datos asociadas por salidas Hola centro de datos en el que se aprovisiona la aplicación.

### <a name="how-am-i-billed-for-hybrid-connections"></a>¿Cómo se factura Conexiones híbridas?
Presentamos tres escenarios de facturación de ejemplo para Conexiones híbridas:

*   Escenario 1:
    *   Tiene un agente de escucha único, como una instancia del Administrador de conexiones híbridas instalado y en ejecución continuamente para mes completo Hola Hola.
    *   Enviar/3 GB de datos a través de conexiones de Hola durante el mes de Hola. 
    *   El cargo total es de 5 dólares.
*   Escenario 2:
    *   Tiene un agente de escucha único, como una instancia del Administrador de conexiones híbridas instalado y en ejecución continuamente para mes completo Hola Hola.
    *   Enviar 10 GB de datos a través de conexiones de Hola durante el mes de Hola.
    *   El cargo total es de 7,50 dólares. Es 5 $ para conexión de Hola y primeras 5 GB + $2,50 para Hola adicional 5 GB de datos.
*   Escenario 3:
    *   Tiene dos instancias, A y B, del Administrador de conexiones híbridas instalado y en ejecución continuamente para mes completo Hola Hola.
    *   Enviar/3 GB de datos a través de la conexión A durante los meses de Hola.
    *   Enviar 6 GB de datos a través de la conexión B durante los meses de Hola.
    *   El cargo total es de 10,50 dólares. Es $5 para la conexión A + 5 $ para la conexión B + 0,50 $ (por gigabyte sexto de hello en conexión B).

Tenga en cuenta que los precios de hello usados en ejemplos de hello aplicable solo durante el período de vista previa de las conexiones híbridas de Hola. Los precios son toochange asunto en disponibilidad general de las conexiones híbridas.

### <a name="how-are-hours-calculated-for-relay"></a>¿Cómo se calculan las horas de retransmisión?

WCF Relay solo está disponibles en los espacios de nombres de nivel Estándar. En cualquier otro caso, el precio y las [cuotas de conexión](../service-bus-messaging/service-bus-quotas.md) de las retransmisiones permanecen igual. Esto significa que retransmisiones continuar toobe cobra según el número de Hola de mensajes (no de operaciones) y horas de retransmisión. Para obtener más información, vea hello ["Retransmisiones de WCF y las conexiones híbridas"](https://azure.microsoft.com/pricing/details/service-bus/) tabla en la página de detalles de precios de Hola.

### <a name="what-if-i-have-more-than-one-listener-connected-tooa-specific-relay"></a>¿Qué ocurre si tengo más de una retransmisión específico de agente de escucha tooa conectado?
En algunos casos, una sola retransmisión puede tener varios agentes de escucha conectados. Una retransmisión se considera abierta el agente de escucha de retransmisión al menos una vez tooit conectado. Agregar resultados de los agentes de escucha tooan retransmisión abierta en horas de retransmisión adicionales. Hola número de retransmisión remitentes (clientes que invocan o enviar mensajes de toorelays) que están conectados tooa retransmisión no afecta al cálculo de Hola de horas de retransmisión.

### <a name="how-is-hello-messages-meter-calculated-for-wcf-relays"></a>¿Cómo se calcula el contador de mensajes de Hola para retransmisiones de WCF?
(**Esto aplica solo tooWCF retransmisiones. Los mensajes no son un costo en Conexiones híbridas.** )

En general, mensajes facturables para retransmisiones se calculan mediante el uso de Hola mismo método que se usa para asíncrona entidades (colas, temas y suscripciones), se ha descrito anteriormente. Sin embargo, hay algunas diferencias importantes.

Enviar una retransmisión de Bus de servicio de tooa de mensaje se trata como un "completo a través de" envío toohello escucha de retransmisión que recibe el mensaje de bienvenida. No se trata como una retransmisión de Bus de servicio de envío operación toohello, seguida por un agente de escucha de retransmisión de toohello de entrega. Una invocación de servicio de estilo de solicitud y respuesta (de una copia de seguridad too64 KB) en un resultados de agente de escucha de retransmisión en dos mensajes facturables: un mensaje facturable por solicitud de Hola y un mensaje facturable por respuesta hello (suponiendo que la respuesta de hello también es 64 KB o menor). Esto es diferente a usar un toomediate cola entre un cliente y un servicio. Si utiliza un toomediate de cola entre un cliente y un servicio, hello mismo patrón de solicitud y respuesta requiere una cola de toohello de envío de solicitudes, seguida de una eliminación de cola/entrega del servicio de toohello de cola de Hola. Esto es seguido de una cola de tooanother de envío de respuesta y una eliminación de cola/entrega de ese cliente toohello en cola. Con hello mismo tamaño suposiciones a lo largo de (arriba too64 KB), realizan Hola cola modelo da como resultado 4 mensajes facturables. Se le facturará para dos veces el número de hello del programa Hola a tooimplement mensajes que mismo patrón que se consigue mediante retransmisión. Por supuesto, hay ventajas toousing colas tooachieve este patrón, como la durabilidad y equilibrio de carga. Estas ventajas pueden justificar gastos adicionales de Hola.

Retransmisiones que se abren mediante el uso de hello **netTCPRelay** enlace WCF tratan los mensajes como mensajes individuales, sino como un flujo de datos que pasan por el sistema de Hola. Cuando se usa este enlace, solo hello remitente y el agente de escucha tienen visibilidad en tramas de hello individuales de mensajes de saludo enviados y recibidos. Para las retransmisiones que utilizan hello **netTCPRelay** enlace, todos los datos se trata como una secuencia para calcular los mensajes facturables. En este caso, Service Bus calcula la cantidad total de Hola de datos enviados o recibidos a través de cada retransmisión individual en forma de 5 minutos. A continuación, divide esa cantidad total de datos por número de hello toodetermine de 64 KB de mensajes facturables para dicha retransmisión durante ese período de tiempo.

## <a name="quotas"></a>Cuotas
| Nombre de cuota | Scope | Tipo | Comportamiento cuando se supera | Valor |
| --- | --- | --- | --- | --- |
| Agentes de escucha simultáneos en una retransmisión |Entidad |estática |Se rechazan las solicitudes posteriores de conexiones adicionales y se recibe una excepción al llamar a código de hello. |25 |
| Agentes de escucha simultáneos |Todo el sistema |estática |Se rechazan las solicitudes posteriores de conexiones adicionales y se recibe una excepción al llamar a código de hello. |2.000 |
| Conexiones de retransmisión simultáneas por todos los puntos de conexión de retransmisión en un espacio de nombres de servicio |Todo el sistema |estático |- |5.000 |
| Puntos de conexión de retransmisión por espacio de nombres de servicio |Todo el sistema |estático |- |10.000 |
| Tamaño de mensaje de las retransmisiones [NetOnewayRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.netonewayrelaybinding.aspx) y [NetEventRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.neteventrelaybinding.aspx) |Todo el sistema |estática |Se rechazan los mensajes entrantes que superen estas cuotas y llamar a código de hello recibe una excepción. |64 KB |
| Tamaño de mensaje de las retransmisiones [HttpRelayTransportBindingElement](https://msdn.microsoft.com/library/microsoft.servicebus.httprelaytransportbindingelement.aspx) y [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) |Todo el sistema |estático |- |Ilimitado |

### <a name="does-relay-have-any-usage-quotas"></a>¿Tiene Relay cuotas de uso?
De forma predeterminada, para cualquier servicio en la nube, Microsoft establece una cuota de uso mensual agregada que se calcula en todas las suscripciones del cliente. Somos conscientes de que en ocasiones sus necesidades pueden superar estos límites. Puede ponerse en contacto con el servicio de atención al cliente en cualquier momento para que podamos conocer sus necesidades y ajustar estos límites según corresponda. Bus de servicio, cuotas de uso agregadas Hola son los siguientes:

* 5 millardos de mensajes
* 2 millones de horas de retransmisión

Aunque nos reservamos Hola derecho toodisable una cuenta que supera sus cuotas de uso mensual, proporcionamos notificación por correo electrónico y hacemos del cliente Hola de toocontact de varios intentos antes de realizar cualquier acción. Los clientes que superen estas cuotas siguen siendo responsables de cargos por exceso de las mismas.

### <a name="naming-restrictions"></a>Restricciones de nomenclatura
El nombre de un espacio de nombres de Relay debe tener entre 6 y 50 caracteres de longitud.

## <a name="subscription-and-namespace-management"></a>Administración de suscripción y espacio de nombres
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>¿Cómo se puede migrar una suscripción de Azure de espacio de nombres tooanother?

toomove un espacio de nombres de una suscripción de tooanother de suscripción de Azure, puede que cualquier uso Hola [portal de Azure](https://portal.azure.com) o utilizar los comandos de PowerShell. toomove una suscripción de tooanother de espacio de nombres, el espacio de nombres de hello ya debe estar activo. usuario de Hola ejecutando comandos de Hola debe ser un usuario de administrador en ambas suscripciones Hola de origen y de destino.

#### <a name="azure-portal"></a>Azure Portal

Hola toouse espacios de nombres de Azure toomigrate portal Azure retransmisión de suscripción de tooanother de una suscripción, vea [mover tooa de recursos nuevo grupo de recursos o suscripción](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

toouse PowerShell toomove un espacio de nombres de la suscripción de tooanother de una suscripción de Azure, Hola de uso después de la secuencia de comandos. tooexecute esta operación, el espacio de nombres de hello ya debe estar activo y usuario Hola ejecutar comandos de PowerShell de hello debe ser un usuario de administrador en ambas suscripciones de origen y de destino de Hola.

```powershell
# Create a new resource group in hello target subscription.
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move hello namespace from hello source subscription toohello target subscription.
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="troubleshooting"></a>Solución de problemas
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-relay-apis-and-suggested-actions-you-can-take"></a>¿Cuáles son algunas de las excepciones de hello generados por las API de retransmisión de Azure y sugiere acciones que puede realizar?
Para obtener una descripción de excepciones comunes y las acciones sugeridas que puede realizar, consulte [Excepciones de Azure Relay][Relay exceptions].

### <a name="what-is-a-shared-access-signature-and-which-languages-can-i-use-toogenerate-a-signature"></a>¿Qué es una firma de acceso compartido y qué idiomas puedo usar toogenerate una firma?
Las firmas de acceso compartido (SAS) son un mecanismo de autenticación basado en valores hash seguros SHA-256 o en URI. Para obtener información sobre cómo toogenerate sus propias firmas en el nodo, PHP, Java, C y C#, ven [autenticación de Service Bus con firmas de acceso compartido][Shared Access Signatures].

### <a name="is-it-possible-toowhitelist-relay-endpoints"></a>¿Es posible toowhitelist extremos de retransmisión?
Sí. cliente de retransmisión de Hello realiza conexiones toohello servicio de retransmisión de Azure mediante el uso de nombres de dominio completo. Los clientes pueden agregar una entrada para `*.servicebus.windows.net` en los firewalls compatibles con la creación de listas de autorizados de DNS.

## <a name="next-steps"></a>Pasos siguientes
* [Creación de un espacio de nombres](relay-create-namespace-portal.md)
* [Introducción a .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introducción a Node](relay-hybrid-connections-node-get-started.md)

[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Relay exceptions]: relay-exceptions.md
[Shared access signatures]: ../service-bus-messaging/service-bus-sas.md