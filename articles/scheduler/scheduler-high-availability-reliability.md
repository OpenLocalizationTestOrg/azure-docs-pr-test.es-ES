---
title: aaaScheduler alta disponibilidad y confiabilidad
description: Alta disponibilidad y confiabilidad de Programador
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a>Alta disponibilidad y confiabilidad de Programador
## <a name="azure-scheduler-high-availability"></a>Alta disponibilidad de Programador de Azure
Como servicio principal de la plataforma Azure, Programador de Azure tiene una alta disponibilidad y presenta implementación de servicio con redundancia geográfica y replicación geográfica regional de trabajos.

### <a name="geo-redundant-service-deployment"></a>Implementación de servicio con redundancia geográfica
El programador de Azure está disponible a través de la interfaz de usuario en casi cada región geográfica que está actualmente en Azure Hola. lista de Hola de regiones que está disponible en el programador de Azure es [enumerados aquí](https://azure.microsoft.com/regions/#services). Si un centro de datos en una región hospedada deja de estar disponible, las capacidades de conmutación por error de hello del programador de Azure son tales que Hola servicio está disponible desde otro centro de datos.

### <a name="geo-regional-job-replication"></a>Replicación geográfica regional de trabajos
No solo se hello Azure Scheduler front-end disponible para las solicitudes de administración, pero su propio trabajo es también una replicación geográfica. Cuando hay una interrupción en una región, el programador de Azure conmuta por error y se asegura de que el trabajo de Hola se ejecuta desde otro centro de datos en la región geográfica emparejada de Hola.

Por ejemplo, si creó un trabajo en la zona Centro-Sur de EE. UU., Programador de Azure replica automáticamente ese trabajo en la zona Centro-Norte de EE. UU. Cuando hay un error en Ee.uu. Central sur, programador de Azure garantiza que el trabajo de Hola se ejecuta desde Ee.uu. Central Norte. 

![][1]

Como resultado, el programador de Azure garantiza que los datos permanecen en Hola misma región geográfica más amplia en caso de un error de Azure. Como resultado, no debe duplicar el trabajo solo tooadd alta disponibilidad: el programador de Azure proporciona automáticamente capacidades de alta disponibilidad para los trabajos.

## <a name="azure-scheduler-reliability"></a>Confiabilidad de Programador de Azure
El programador de Azure garantiza su propia alta disponibilidad y adopta un enfoque diferente trabajos toouser creados. Por ejemplo, puede que su trabajo invoque un extremo HTTP que no está disponible. El programador de Azure, no obstante, intenta tooexecute su trabajo correctamente, por lo que le ofrece opciones alternativas toodeal con error. Programador de Azure hace esto de dos maneras:

### <a name="configurable-retry-policy-via-retrypolicy"></a>Directiva de reintentos configurable a través de "retryPolicy"
El programador de Azure permite tooconfigure una directiva de reintentos. De forma predeterminada, si se produce un error en un trabajo, el programador intenta trabajo Hola cuatro veces más, a intervalos de 30 segundos. Puede volver a configurar esta directiva de reintento toobe una (por ejemplo, diez veces, en intervalos de 30 segundos) más agresiva o más flexible (por ejemplo, dos veces, en intervalos diarios).

Como ejemplo de cuándo esto puede resultar de ayuda, puede crear un trabajo que se ejecute una vez por semana e invoca un extremo HTTP. Si el punto de conexión de hello HTTP está inactivo durante unas horas cuando se ejecuta el trabajo, no puede toowait una semana para hello trabajo toorun nuevo puesto que incluso directiva de reintentos de hello predeterminada se producirá un error. En tales casos, se puede reconfigurar tooretry de directiva de reintentos estándar Hola cada tres horas (por ejemplo) en lugar de cada 30 segundos.

toolearn cómo tooconfigure una directiva de reintentos, consulte demasiado[retryPolicy](scheduler-concepts-terms.md#retrypolicy).

### <a name="alternate-endpoint-configurability-via-erroraction"></a>Capacidad de configuración alternativa de extremos a través de "errorAction"
Si el extremo de destino de hello para el trabajo del programador de Azure sigue inaccesible, el programador de Azure vuelve toohello extremo de control de errores alternativo después de seguir la directiva de reintentos. Si se configura un extremo de control de errores alternativo, Programador de Azure lo invoca. Con un extremo alternativo, sus propios trabajos tendrán alta disponibilidad en la cara de Hola de error.

Por ejemplo, en el diagrama de hello siguiente, el programador de Azure sigue su toohit de directiva de reintento de un servicio web de Nueva York. Después de hello reintentos por error, comprueba si hay una alternativa. Después continúa y comienza a realizar solicitudes toohello alternativas con hello misma directiva de reintentos.

![][2]

Tenga en cuenta que Hola la misma directiva de reintentos aplica la acción original de tooboth Hola y Hola error alternativa. Es también posible toohave Hola error alternativa tipo de acción de ser diferente de hello principal tipo de acción. Por ejemplo, puede invocar un extremo HTTP acción principal de hello, acción de error de hello en su lugar pueden una cola de almacenamiento, la cola de bus de servicio o la acción de tema de bus de servicio que realiza el registro de errores.

toolearn cómo tooconfigure un extremo alternativo, consulte demasiado[errorAction](scheduler-concepts-terms.md#action-and-erroraction).

## <a name="see-also"></a>Otras referencias
 [¿Qué es Programador?](scheduler-intro.md)

 [Conceptos, terminología y jerarquía de entidades de Programador de Azure](scheduler-concepts-terms.md)

 [Empezar a usar a Scheduler en hello portal de Azure](scheduler-get-started-portal.md)

 [Planes y facturación en Programador de Azure](scheduler-plans-billing.md)

 [¿Cómo se programa toobuild complejo y periodicidad avanzada con el programador de Azure](scheduler-advanced-complexity.md)

 [Referencia de API de REST de Programador de Azure](https://msdn.microsoft.com/library/mt629143)

 [Referencia de cmdlets de PowerShell de Programador de Azure](scheduler-powershell-reference.md)

 [Límites, valores predeterminados y códigos de error de Programador de Azure](scheduler-limits-defaults-errors.md)

 [Autenticación de salida de Programador de Azure](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
