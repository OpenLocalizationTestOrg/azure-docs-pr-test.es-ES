---
title: "Preguntas más frecuentes (P+F) de Service Bus aaaAzure | Documentos de Microsoft"
description: Respuestas a algunas preguntas frecuentes acerca de Azure Service Bus.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>Preguntas más frecuentes sobre Service Bus
En este artículo se responden algunas preguntas frecuentes sobre Microsoft Azure Service Bus. También puede visitar hello [preguntas frecuentes de Azure admite](http://go.microsoft.com/fwlink/?LinkID=185083) para información general de precios y soporte técnico de Azure.

## <a name="general-questions-about-azure-service-bus"></a>Preguntas generales sobre Azure Service Bus
### <a name="what-is-azure-service-bus"></a>Qué es Azure Service Bus
[Service Bus de Azure](service-bus-messaging-overview.md) es una plataforma de nube de mensajería asincrónica que le permite toosend los datos entre sistemas desacoplados. Microsoft ofrece esta característica como un servicio, lo que significa que no es necesario toohost cualquiera de su propio hardware en orden toouse se.

### <a name="what-is-a-service-bus-namespace"></a>¿Qué es un espacio de nombres de Service Bus?
Un [espacio de nombres](service-bus-create-namespace-portal.md) proporciona un contenedor con un ámbito para el desvío de recursos de Service Bus en la aplicación. Crear uno es necesario toouse Bus de servicio y puede ser uno de hello primeros pasos en la introducción.

### <a name="what-is-an-azure-service-bus-queue"></a>¿Qué es una cola de Azure Service Bus?
Una [cola de Service Bus](service-bus-queues-topics-subscriptions.md) es una entidad en la que se almacenan los mensajes. Las colas son especialmente útiles cuando tenga varias aplicaciones o varias partes de una aplicación distribuida que necesitan toocommunicate entre sí. cola de Hello es Centro de distribución de tooa similar que varios productos (mensajes) se reciben y, a continuación, se envían desde esa ubicación.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>¿Qué son los temas y las suscripciones de Azure Service Bus?
Un tema se puede visualizar como una cola y cuando utiliza varias suscripciones, se convierte en un modelo de mensajería más enriquecido; básicamente en una herramienta de comunicación de uno a varios. Este modelo de publicación/suscripción (o *pub/sub*) permite a una aplicación que envía ese mensaje recibido por varias aplicaciones de un tema de tooa de mensaje con varios toohave de suscripciones.

### <a name="what-is-a-partitioned-entity"></a>¿Qué es una entidad con particiones?
Un único agente de mensajes controla una cola o tema convencional, que se almacena en un almacén de mensajería. Las [colas o temas con particiones](service-bus-partitioning.md) las administran varios agentes de mensajes y se almacenan en varios almacenes de mensajería. Esto significa que el rendimiento global de una cola o tema particionado de Hola ya no está limitado por el rendimiento de Hola de un solo agente de mensajes o almacén de mensajería. Además, una interrupción temporal de un almacén de mensajería no hace que una cola o tema con particiones deje de estar disponible.

Tenga en cuenta que la ordenación no está garantizada al utilizar particiones de entidades. En el caso de hello que una partición no está disponible, todavía puede enviar y recibir mensajes de Hola otras particiones.

## <a name="best-practices"></a>Prácticas recomendadas
### <a name="what-are-some-azure-service-bus-best-practices"></a>¿Cuáles son algunos de los procedimientos recomendados para Azure Service Bus?
* [Las prácticas recomendadas para mejorar el rendimiento mediante Service Bus] [ Best practices for performance improvements using Service Bus] : este artículo describe cómo toooptimize rendimiento al intercambiar mensajes.

### <a name="what-should-i-know-before-creating-entities"></a>¿Qué debo saber antes de crear entidades?
Hola propiedades de una cola y tema siguientes es inmutable. Tenga esto en cuenta al aprovisionar las entidades ya que esto no se puede modificar, sin crear una nueva entidad de reemplazo.

* Tamaño
* Creación de particiones
* Sesiones
* Detección de duplicados
* Entidad exprés

## <a name="pricing"></a>Precios
En esta sección responde a algunas preguntas frecuentes acerca de la estructura de precios de Bus de servicio de Hola.

Hola [Service Bus precios y facturación](service-bus-pricing-billing.md) artículo explica metros de facturación de hello en el Bus de servicio y para obtener información sobre opciones de precios de Bus de servicio, consulte [detalles de precios de Bus de servicio](https://azure.microsoft.com/pricing/details/service-bus/).

También puede visitar hello [preguntas más frecuentes de soporte técnico de Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para obtener información sobre precios de Azure general. 

### <a name="how-do-you-charge-for-service-bus"></a>¿Cómo se cobra Service Bus?
Para más información sobre los precios de Service Bus, consulte los [detalles de precios de Service Bus][Pricing overview]. Además se indicó toohello precios, se le cobra por las transferencias de datos asociadas por salidas Hola centro de datos en el que se aprovisiona la aplicación.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>¿Qué uso del Bus de servicio es transferencia toodata de asunto? ¿Cuál no lo está?
Cualquier transferencia de datos dentro de una determinada región de Azure se proporciona sin cargo alguno, así como las transferencias de datos entrantes. Transferencia de datos fuera de una región es cargos de tooegress de asunto que se pueden encontrar [aquí](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>¿Service Bus cobra por almacenamiento?
No, Service Bus no cobra por almacenamiento. Sin embargo, hay una cuota limitación Hola cantidad máxima de datos que pueden permanecer por cola/tema. Consulte la siguiente pregunta Frecuente de Hola.

## <a name="quotas"></a>Cuotas

Para obtener una lista de cuotas y límites de Bus de servicio, vea hello [información general de las cuotas de Bus de servicio][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>¿Service Bus tiene alguna cuota de uso?
De forma predeterminada, para cualquier servicio en la nube, Microsoft establece una cuota de uso mensual agregada que se calcula en todas las suscripciones del cliente. Dado que entendemos que puede necesitar más de estos límites, póngase en contacto con el servicio de atención al cliente en cualquier momento para que podamos conocer sus necesidades y ajustar estos límites adecuadamente. Bus de servicio, cuota de uso agregadas hello es 5 millones de mensajes al mes.

Aunque nos reservamos Hola derecho toodisable una cuenta de cliente que ha superado sus cuotas de uso de un mes determinado, se proporcionará la notificación por correo electrónico y hacer que un cliente toocontact de varios intentos antes de realizar cualquier acción. Los clientes que superen estas cuotas seguirán responsables de cargos que superen las cuotas de Hola.

Al igual que con otros servicios en Azure, Bus de servicio aplica un conjunto de tooensure de cuotas específicas que hay hace un uso de recursos. Puede encontrar más detalles acerca de estas cuotas en hello [información general de las cuotas de Bus de servicio][Quotas overview].

## <a name="troubleshooting"></a>Solución de problemas
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>¿Cuáles son algunas de las excepciones de hello generadas por las API de Bus de servicio de Azure y sus acciones sugeridas?
Para obtener una lista de posibles excepciones de Service Bus, consulte [Información general sobre excepciones][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>¿Qué es una firma de acceso compartido y qué lenguajes admiten la generación de una firma?
Las firmas de acceso compartido son un mecanismo de autenticación basado en URI y valores hash seguros SHA-256. Para obtener información acerca de cómo toogenerate sus propias firmas en el nodo, PHP, Java y C\#, vea hello [firmas de acceso compartido] [ Shared Access Signatures] artículo.

## <a name="subscription-and-namespace-management"></a>Administración de suscripción y espacio de nombres
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>¿Cómo se puede migrar una suscripción de Azure de espacio de nombres tooanother?

Puede mover un espacio de nombres de tooanother de una suscripción de Azure, mediante cualquier hello [portal de Azure](https://portal.azure.com) o comandos de PowerShell. En una operación de orden tooexecute hello, espacio de nombres de hello ya debe estar activo. debe ser un administrador en ambos origen Hola usuario Hola ejecutar comandos de Hola y de destino las suscripciones.

#### <a name="portal"></a>Portal

Hola toouse suscripción de tooanother de espacios de nombres de Service Bus toomigrate de portal de Azure, siga instrucciones de hello [aquí](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

Hello secuencia de comandos de PowerShell siguiente mueve un espacio de nombres de tooanother de una suscripción de Azure. tooexecute esta operación, el espacio de nombres de hello ya debe estar activo y usuario Hola ejecutar comandos de PowerShell de hello debe ser un administrador en ambas suscripciones de origen y de destino de Hola.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de Bus de servicio, vea Hola temas siguientes.

* [Introducción a Azure Service Bus Premium (entrada de blog)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introducción a Azure Service Bus Premium (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Información general de Service Bus](service-bus-messaging-overview.md)
* [Información general sobre la arquitectura de Azure Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Introducción a las colas de Service Bus](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
