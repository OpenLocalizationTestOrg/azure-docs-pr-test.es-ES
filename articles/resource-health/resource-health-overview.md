---
title: "información general sobre el mantenimiento de recursos aaaAzure | Documentos de Microsoft"
description: "Estado de los recursos de Azure. Información general"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: b920241b2f64a0695ba2c32e9ccb0c2c3739986d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Información general sobre Azure Resource Health
 
Resource Health le ayuda a diagnosticar y obtener soporte técnico cuando un problema de Azure afecta a sus recursos. Le informa sobre el estado de hello actuales y pasadas de los recursos y le ayuda a mitigar los problemas. Resource Health le proporciona soporte técnico si necesita ayuda con los problemas de los servicios de Azure.

Mientras que [estado de Azure](https://status.azure.com) le informa sobre los problemas de servicio que afectan a un amplio conjunto de los clientes de Azure, el estado de los recursos, obtendrá un panel personalizado de mantenimiento de Hola de los recursos. Estado de los recursos muestra todos los tiempos de hello los recursos no estaban disponibles en hello vencido tooAzure problemas del servicio. Esto facilita para toounderstand si se infringe un SLA. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>¿Qué se considera que es un recurso y cómo Resource Health decide si el estado de un recurso es correcto?
Un recurso es una instancia de un tipo de recurso que un servicio de Azure ofrece a través de Azure Resource Manager, por ejemplo: una máquina virtual, una aplicación web o una base de datos de SQL Database.

Estado de los recursos se basa en señales emitidas por hello distintos servicios de Azure tooassess si un recurso es correcto o no. Si un recurso está en mal estado, estado de los recursos analiza información adicional toodetermine Hola origen Hola problema. También se identifican las acciones que Microsoft está llevando a cabo toofix problema de Hola o qué acciones puede llevar a cabo tooaddress Hola causa de problema de Hola. 

Comprueba la lista completa de Hola de revisión de los tipos de recursos y el estado de [estado de los recursos de Azure](resource-health-checks-resource-types.md) para obtener más detalles sobre cómo se evalúa el estado.

## <a name="health-status-provided-by-resource-health"></a>Estado de mantenimiento proporcionado por Resource Health
estado de Hola de un recurso es uno de hello siguientes estados:

### <a name="available"></a>Disponible
servicio de Hello no ha detectado los eventos que tienen efecto sobre el estado de Hola de recurso de Hola. En casos donde los recursos de Hola se ha recuperado de tiempo de inactividad imprevisto durante Hola última Hola 24 horas aparecerá **se recuperó recientemente** notificación.

![Máquina virtual disponible en Resource Health](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>No disponible
Hola servicio ha detectado un evento de plataforma no afectar el estado de Hola de recurso de Hola o de plataforma en curso.

#### <a name="platform-events"></a>Eventos de plataforma
Estos eventos se desencadenan en varios componentes de infraestructura de Azure hello e incluyen tanto acciones programadas como mantenimiento planeado e incidentes inesperados como un reinicio del host no planeada.

Mantenimiento de recursos proporciona detalles adicionales sobre el evento de hello, proceso de recuperación de Hola y habilita la compatibilidad con de toocontact incluso si no tienes un Microsoft active contrato de soporte técnico.

![Máquina virtual recursos mantenimiento no está disponible debido a eventos tooplatform](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>Eventos no de plataforma
Estos eventos se activan mediante acciones realizadas por los usuarios, por ejemplo, detener una máquina virtual o alcance Hola número máximo de conexiones tooa caché en Redis.

![Máquina virtual recursos mantenimiento no está disponible debido a eventos de plataforma toonon](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>Desconocido
Este estado de mantenimiento indica que Resource Health no ha recibido información sobre este recurso durante más de 10 minutos. Aunque este estado no es una indicación definitiva del estado de Hola de recursos de hello, es un punto de datos importantes en el proceso de solución de problemas de hello:
* Si está ejecutando recursos hello como estado de hello esperado del recurso de hello actualizará tooAvailable después de unos minutos.
* Si experimenta problemas con el recurso de hello, hello estado desconocido puede sugerir recursos Hola se ve afectado por un evento de plataforma de Hola.

![Máquina virtual Desconocida de Resource Health](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>Informe de un estado incorrecto
Si en cualquier momento considera estado actual de hello es incorrecta, puede hacernos saber haciendo clic en **informan del estado de mantenimiento incorrecto**. En casos donde se ven afectados por un problema de Azure, le recomendamos que toocontact de soporte técnico de hoja de mantenimiento de recursos de Hola. 

![Informe de estado incorrecto en Resource Health](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>Información histórica
Puede tener acceso a los días de too14 de datos de historial de mantenimiento, haga clic en **ver el historial de** en la hoja de estado de recursos de Hola. 

![Historial de informes en Resource Health](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>Introducción
tooopen estado de recursos para un recurso
1.  Inicie sesión en hello portal de Azure.
2.  Navegar tooyour recurso.
3.  En el menú de recursos de hello ubicado en el lado izquierdo de hello, haga clic en **estado de los recursos**.

![Apertura de Resource Health desde la hoja Recurso](./media/resource-health-overview/from-resource-blade.png)

También puede tener acceso a mantenimiento de recursos, haga clic en **más servicios**y escribiendo **estado de los recursos** Hola de tooopen de cuadro de texto de filtro **ayuda y soporte técnico** hoja. Por último, haga clic en [**Resource Health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).

![Apertura de Resource Health desde Más servicios](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>Pasos siguientes

Consulte estos toolearn recursos más información acerca del estado de los recursos:
-  [Tipos de recurso y comprobaciones de estado en Azure Resource Health](resource-health-checks-resource-types.md)
-  [Preguntas más frecuentes de Azure Resource Health](resource-health-faq.md)




