---
title: aaaIntroduction tooAzure Advisor | Documentos de Microsoft
description: Utilice Azure Advisor toooptimize las implementaciones de Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 5d796fc06366221efdb6f1bda39ab3fb676abfd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-advisor"></a>Introducción tooAzure Advisor

Obtenga información sobre el Asistente de Azure y sus capacidades claves así como toofrequently respuestas preguntas más frecuentes.

## <a name="what-is-advisor"></a>¿Qué es Advisor?
Advisor es un consultor personalizado en la nube que le ayudará a seguir toooptimize de prácticas recomendada las implementaciones de Azure. Analiza la telemetría de uso y la configuración de recursos y, a continuación, recomienda soluciones que pueden ayudar a mejoran la rentabilidad hello, rendimiento, alta disponibilidad y seguridad de los recursos de Azure.

Con Advisor, puede:
* Obtener sugerencias de procedimientos recomendados proactivas, prácticas y personalizadas, 
* Mejorar el rendimiento de hello, seguridad y alta disponibilidad de los recursos a medida que identifique tooreduce oportunidades gasto general Azure.
* Obtener recomendaciones con acciones propuestas en línea.

Puede tener acceso a asesor a través de hello [portal de Azure](https://aka.ms/azureadvisordashboard). Inicie sesión en toohello [portal](https://portal.azure.com), seleccione **examinar**y, a continuación, desplácese demasiado**Asistente de Azure**. panel de Asistente de Hello muestra recomendaciones personalizadas para una suscripción seleccionada. 

recomendaciones de Hola se dividen en cuatro categorías: 

* **Alta disponibilidad**: tooensure y mejorar la continuidad de Hola de las aplicaciones empresariales críticas. Para obtener más información, consulte las [recomendaciones sobre alta disponibilidad de Advisor](advisor-high-availability-recommendations.md).

* **Seguridad**: toodetect amenazas y vulnerabilidades que podrían dar lugar a infracciones de toosecurity. Para obtener más información, consulte las [recomendaciones sobre seguridad de Advisor](advisor-security-recommendations.md).

* **Rendimiento**: velocidad de hello tooimprove de las aplicaciones. Para obtener más información, consulte las [recomendaciones sobre rendimiento de Advisor](advisor-performance-recommendations.md).

* **Costo**: toooptimize y reducir la Azure general dedican. Para obtener más información, consulte las [recomendaciones sobre el costo de Advisor](advisor-cost-recommendations.md).

  ![Tipos de recomendaciones de Advisor](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> tooaccess las recomendaciones del asistente, primero debe *registrar su suscripción* con el asistente. Una suscripción se registra cuando un *suscripción propietario* inicia Hola Hola de panel y hace clic en el asistente **obtener recomendaciones** botón. Esta operación *solo se realiza una vez*. Después de registra la suscripción de hello, puede tener acceso a las recomendaciones del asistente como *propietario*, *colaborador*, o *lector* para una suscripción de un grupo de recursos, o recurso específico.

Puede hacer clic en un toolearn de recomendación más sobre él. También puede obtener información sobre las acciones que puede realizar tootake ventaja de una oportunidad o resolver un problema. 

Advisor ofrece recomendaciones con acciones insertadas o vínculos de documentación. Al hacer clic en una acción en línea le guiará por una tooimplement "viaje de usuario interactiva" se. Al hacer clic en un vínculo de documentación señala toodocumentation que describe cómo implementar la acción de hello toomanually. 

Advisor actualiza las recomendaciones cada hora. Si no tiene la intención de una acción inmediata tootake en una recomendación, puede posponer durante un período de tiempo especificado o descartarla. 

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="how-do-i-access-advisor"></a>¿Cómo se accede a Advisor?
Puede tener acceso a asesor a través de hello [portal de Azure](https://aka.ms/azureadvisordashboard). Inicie sesión en toohello [portal](https://portal.azure.com), seleccione **examinar**y, a continuación, desplácese demasiado**Asistente de Azure**. panel de Asistente de Hello muestra recomendaciones personalizadas para una suscripción seleccionada. 

También puede ver las recomendaciones del asistente a través de la hoja de recursos de máquina virtual de Hola. Elige una máquina virtual y, a continuación, desplácese tooAdvisor recomendaciones en el menú de Hola. 

### <a name="what-permissions-do-i-need-tooaccess-advisor"></a>¿Qué permisos necesito tooaccess Advisor?

tooaccess las recomendaciones del asistente, primero debe *registrar su suscripción* con el asistente. Una suscripción se registra cuando un *suscripción propietario* inicia Hola Hola de panel y hace clic en el asistente **obtener recomendaciones** botón. Esta operación *solo se realiza una vez*. Después de registra la suscripción de hello, puede tener acceso a las recomendaciones del asistente como *propietario*, *colaborador*, o *lector* para una suscripción de un grupo de recursos, o recurso específico.

### <a name="how-often-are-advisor-recommendations-updated"></a>¿Con qué frecuencia se actualizan las recomendaciones de Advisor?

Las recomendaciones de Advisor se actualizan cada hora.

### <a name="what-resources-does-advisor-provide-recommendations-for"></a>¿Para qué recursos Advisor ofrece recomendaciones?

Advisor proporciona recomendaciones para máquinas virtuales, conjuntos de disponibilidad, puertas de enlace de aplicaciones, App Services, servidores SQL Server, bases de datos SQL y Redis Cache.

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a>¿Se puede posponer o descartar una recomendación?

toosnooze o descartar una recomendación, haga clic en hello **posponer** botón o vínculo. Puede especificar un tiempo de posposición período o seleccione **nunca** toodismiss Hola recomendación.

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de las recomendaciones del asistente, vea:

* [Introducción a Advisor](advisor-get-started.md)
* [Recomendaciones sobre alta disponibilidad de Advisor](advisor-high-availability-recommendations.md)
* [Recomendaciones sobre seguridad de Advisor](advisor-security-recommendations.md)
* [Recomendaciones sobre rendimiento de Advisor](advisor-performance-recommendations.md)
* [Recomendaciones sobre el costo de Advisor](advisor-cost-recommendations.md)
