---
title: "Preguntas más frecuentes de los centros de eventos aaaAzure | Documentos de Microsoft"
description: Preguntas frecuentes sobre Azure Event Hubs (P+F)
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: bfa10984-eb22-4671-861a-f377a90d9372
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm;shvija
ms.openlocfilehash: cc0844edcc38ad167cde9497d58d44155fc90b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-frequently-asked-questions"></a>Preguntas frecuentes sobre Event Hubs

## <a name="general"></a>General

### <a name="what-is-hello-difference-between-event-hubs-basic-and-standard-tiers"></a>¿Cuál es la diferencia de hello entre niveles estándares y básico de centros de eventos?

nivel estándar de Hola de centros de eventos de Azure proporciona características más allá de lo que está disponible en el nivel básico de Hola. Hola siguientes características se incluyen con estándar:
* Retención de eventos más prolongada
* Conexiones asíncronas adicionales, con un cargo por encima del límite durante más de número de hello incluido
* Más de un único grupo de consumidores
* [Capture](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)

Para obtener más información sobre los precios de niveles, incluidos dedicado de concentradores de eventos, vea hello [detalles de precios de centros de eventos](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="what-are-event-hubs-throughput-units"></a>¿Qué son las unidades de procesamiento de los Centros de eventos?

Seleccionar explícitamente las unidades de rendimiento de los centros de eventos, ya sea a través del portal de Azure de Hola o plantillas de administrador de recursos de centros de eventos. Unidades de rendimiento aplican tooall centros de eventos en un espacio de nombres de los centros de eventos, y cada unidad de rendimiento da derecho hello toohello de espacio de nombres siguientes capacidades:

* Too1 MB por segundo de eventos de entrada (eventos enviados a un concentrador de eventos), pero no más de 1000 eventos de entrada, las operaciones de administración o un control llamadas de API por segundo.
* Too2 MB por segundo de eventos de salida (eventos consumidos de un concentrador de eventos).
* Backup too84 GB de almacenamiento de eventos (suficiente para el período de retención de 24 horas de hello predeterminado).

Unidades de rendimiento de los centros de eventos se facturan por horas, según Hola número máximo de unidades seleccionadas durante hello tiene hora.

### <a name="how-are-event-hubs-throughput-unit-limits-enforced"></a>¿Cómo se aplican los límites de unidades de rendimiento de los Centros de eventos?
Si el rendimiento de entrada totales de Hola o frecuencia de eventos de entrada totales de hello en todos los concentradores de eventos en un espacio de nombres supera acumuladas de unidad de rendimiento agregado hello, remitentes están limitados y recibirán errores para indicarles que se ha superado esa cuota de entrada de Hola.

Si el rendimiento de salida total de Hola o tasa de salida de hello total de eventos en todos los concentradores de eventos en un espacio de nombres supera acumuladas de unidad de rendimiento agregado hello, receptores están limitados y recibirán errores para indicarles que se ha superado esa cuota de salida de hello. Las cuotas de entrada y salida se aplican por separado, por lo que ningún remitente pueda provocar eventos consumo tooslow hacia abajo, así como tampoco puede un receptor de impedir que los eventos se envíen a un concentrador de eventos.

### <a name="is-there-a-limit-on-hello-number-of-throughput-units-that-can-be-selected"></a>¿Hay un límite del número de Hola de unidades de rendimiento que se pueden seleccionar?
Hay una cuota predeterminada de 20 unidades de procesamiento por espacio de nombres. Puede solicitar una cuota de unidades de procesamiento mayor, si rellena una incidencia de soporte técnico. Más allá del límite de unidad de rendimiento 20 hello, los paquetes están disponibles en 20 y 100 unidades de rendimiento. Tenga en cuenta que el uso de más de 20 unidades de rendimiento quita el número de Hola de toochange de hello capacidad de unidades de rendimiento sin presentar una incidencia de soporte técnico.

### <a name="can-i-use-a-single-amqp-connection-toosend-and-receive-from-multiple-event-hubs"></a>¿Puedo usar un único toosend de conexión de AMQP y recibir de varios centros de eventos?
Sí, siempre y cuando todos los concentradores de eventos de Hola Hola mismo espacio de nombres.

### <a name="what-is-hello-maximum-retention-period-for-events"></a>¿Cuál es el período de retención máximo de Hola de eventos?
El nivel Standard de los Centros de eventos admite actualmente un período de retención máximo de 7 días. Tenga en cuenta que los centros de eventos no están concebidos como almacén de datos permanente. Períodos de retención mayores que 24 horas están pensadas para escenarios en los que es conveniente tooreplay un evento transmitir a Hola mismos sistemas; Por ejemplo, tootrain o comprobar un nuevo modelo de aprendizaje automático en los datos existentes. Si necesita un mensaje retención más allá de 7 días, lo que permite [captura de los centros de eventos](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview) en tu evento concentrador extrae datos de Hola de su cuenta de almacenamiento de toohello de concentrador de eventos o la cuenta de servicio de lago de datos de Azure de su elección. Si habilita Capture, se le cobrará un cargo en función de la unidad de procesamiento comprada.

### <a name="where-is-azure-event-hubs-available"></a>¿Dónde está disponible Azure Event Hubs?
Azure Event Hubs está disponible en todas las regiones de Azure admitidas. Para obtener una lista, visite hello [regiones de Azure](https://azure.microsoft.com/regions/) página.  

## <a name="best-practices"></a>Prácticas recomendadas

### <a name="how-many-partitions-do-i-need"></a>¿Cuántas particiones necesito?
Por favor, tenga en cuenta que Hola recuento de particiones en un centro de eventos no se puede modificar después de la instalación. Con esto en mente, es importante toothink sobre cuántas particiones necesita antes de comenzar. 

Los concentradores de eventos es tooallow diseñado un lector de una sola partición por grupo de consumidores. En la mayoría de los casos de uso, la configuración predeterminada de Hola de cuatro particiones es suficiente. Si desea tooscale el procesamiento de eventos, puede que desee tooconsider agregar particiones adicionales. No hay ningún límite de rendimiento específico en una partición, sin embargo, el rendimiento agregado hello en el espacio de nombres está limitado por número de Hola de unidades de rendimiento. Medida que aumenta el número de Hola de unidades de rendimiento en el espacio de nombres, puede que desee particiones adicionales tooallow lectores simultáneos tooachieve su propio rendimiento máximo.

Sin embargo, si tiene un modelo en el que la aplicación tiene una partición determinada de tooa de afinidad, aumentar Hola número de particiones puede no ser de cualquier tooyou beneficio. Para más información al respecto, vea [Disponibilidad y coherencia](event-hubs-availability-and-consistency.md).

## <a name="pricing"></a>Precios

### <a name="where-can-i-find-more-pricing-information"></a>¿Dónde puedo encontrar más información sobre precios?
Para obtener información completa sobre los precios de centros de eventos, vea hello [detalles de precios de centros de eventos](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="is-there-a-charge-for-retaining-event-hubs-events-for-more-than-24-hours"></a>¿Hay un cargo por retener eventos de los Centros de eventos durante más de 24 horas?
nivel de concentradores de eventos estándar de Hello permiten retención de mensajes períodos más de 24 horas, durante un máximo de 7 días. Si el tamaño de Hola de número total de Hola de eventos almacenados supera la asignación de almacenamiento de hello para el número de Hola de unidades de rendimiento seleccionadas (84 GB por unidad de rendimiento), tamaño de Hola que supera la asignación de Hola se aplican cargos en hello publicado tarifa de almacenamiento de blobs de Azure. asignación de almacenamiento de Hello en cada unidad de rendimiento cubre todos los costos de almacenamiento de información durante períodos de retención de 24 horas (valor predeterminado de hello) incluso si la unidad de rendimiento de Hola se usa una asignación de entrada máxima de toohello.

### <a name="how-is-hello-event-hubs-storage-size-calculated-and-charged"></a>¿Cómo se calcula y se cobra de hello tamaño de almacenamiento de los centros de eventos?
Hola el tamaño total de todos los eventos almacenados, incluida la sobrecarga interna de encabezados del evento o en las estructuras de almacenamiento de disco en todos los concentradores de eventos, se mide a lo largo del día de Hola. Al final de Hola de hello día, se calcula el tamaño de almacenamiento máximo de Hola. asignación de almacenamiento diaria Hola se calcula basándose en un mínimo de unidades de rendimiento seleccionadas durante el día de hello (cada unidad de rendimiento proporciona una asignación de 84 GB) Hola. Si se supera el tamaño total de Hola Hola calcula diariamente de asignación de almacenamiento, almacenamiento de exceso de Hola se factura con las tarifas de almacenamiento de blobs de Azure (en hello **almacenamiento localmente redundante** velocidad).

### <a name="how-are-event-hubs-ingress-events-calculated"></a>¿Cómo se calculan los eventos de entrada de los Centros de eventos?
Cada evento enviar tooan concentrador de eventos cuenta como un mensaje facturable. Un *eventos de entrada* se define como una unidad de datos que es menor o igual too64 KB. Cualquier evento que sea menor o igual too64 KB de tamaño se considera toobe un evento facturable. Si el evento de hello es mayor que 64 KB, número de Hola de eventos facturables se calcula según el tamaño del evento toohello, en múltiplos de 64 KB. Por ejemplo, un evento de 8 KB enviado toohello concentrador de eventos se factura como un evento, pero un mensaje de 96 KB enviado toohello concentrador de eventos se factura dos eventos.

Eventos consumidos de un concentrador de eventos, así como las operaciones de administración y llamadas de control como puntos de control, no se cuentan como eventos de entrada facturable, pero incrementan la asignación de unidad de rendimiento toohello.

### <a name="do-brokered-connection-charges-apply-tooevent-hubs"></a>¿Pueden aplicar cargos por conexión asíncrona concentradores tooEvent?
Se aplican cargos de conexión solo cuando se usa el protocolo AMQP Hola. No hay ningún cargo de conexión para el envío de eventos mediante HTTP, independientemente del número de Hola de envío de sistemas o dispositivos. Si tiene previsto toouse AMQP (por ejemplo, tooachieve más eventos de transmisión por secuencias o tooenable bidireccional una comunicación eficaz en escenarios de comando y control de IoT), vea hello [información sobre los precios de centros de eventos](https://azure.microsoft.com/pricing/details/event-hubs/) página para obtener más información acerca de cómo número de conexiones se incluye en cada nivel de servicio.

### <a name="how-is-event-hubs-capture-billed"></a>¿Cómo se factura Event Hubs Capture?
Está habilitada la captura cuando cualquier centro de eventos en el espacio de nombres de hello tiene habilitada la opción de captura de Hola. Event Hubs Capture se factura por horas y por unidad de procesamiento comprada. Tal como Hola recuento de unidad de rendimiento aumenta o disminuye, captura de los centros de eventos facturación refleja estos cambios en incrementos de una hora completa. Para más información sobre Event Hubs Capture, vea los [detalles de los precios de Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="will-i-be-billed-for-hello-storage-account-i-select-for-event-hubs-capture"></a>¿Cobrarán Hola cuenta de almacenamiento que se selecciona para la captura de los centros de eventos?
Capture usa la cuenta de almacenamiento que se especifique al habilitarlo en un servicio centro de eventos. Como se trata de la cuenta de almacenamiento, los cambios de esta configuración son tooyour facturación de suscripción de Azure.

## <a name="quotas"></a>Cuotas

### <a name="are-there-any-quotas-associated-with-event-hubs"></a>¿Hay alguna cuota asociada a los centros Event Hubs?
Para obtener una lista de todas las cuotas de los centros Event Hubs, consulte [Cuotas](event-hubs-quotas.md).

## <a name="troubleshooting"></a>Solución de problemas

### <a name="what-are-some-of-hello-exceptions-generated-by-event-hubs-and-their-suggested-actions"></a>¿Cuáles son algunas de las excepciones de hello generadas por sus acciones sugeridas y centros de eventos?
Para obtener una lista de posibles excepciones de Event Hubs, consulte [Información general sobre excepciones](event-hubs-messaging-exceptions.md).

### <a name="diagnostic-logs"></a>Registros de diagnóstico
Los concentradores de eventos admite dos tipos de [registros de diagnóstico](event-hubs-diagnostic-logs.md) -registros de errores de captura y registros operativos - de los cuales se representan en json y se pueden activar a través de Hola portal de Azure.

### <a name="support-and-sla"></a>SLA y soporte técnico
El soporte técnico de los centros de eventos está disponible a través de hello [foros de la Comunidad](https://social.msdn.microsoft.com/forums/azure/home). Se ofrece de forma gratuita soporte técnico para la administración de suscripciones y la facturación.

toolearn más información sobre nuestro SLA, consulte hello [contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/) página.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](event-hubs-create.md)
