---
title: "información general sobre el estado del servicio de aaaAzure | Documentos de Microsoft"
description: "Información personalizada sobre cómo las aplicaciones de Azure se ven afectadas por el mantenimiento y los problemas de servicios de Azure actuales y futuros."
services: Resource health
documentationcenter: 
author: rboucher
manager: 
editor: 
ms.assetid: 
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/07/2017
ms.author: robb
ms.openlocfilehash: 2b536ee2f19757d4f2baf5529866c3d159a4670c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-health"></a>Azure Service Health
Azure Service Health proporciona información oportuna y personalizada cuando los problemas en los servicios de Azure afectan a los servicios.  También le ayuda a prepararse para el próximo mantenimiento planeado.

## <a name="service-health-events"></a>Eventos de Service Health
Service Health realiza un seguimiento de tres tipos de eventos de estado que pueden afectar a los recursos:
1. **Problemas del servicio** -Hola de problemas en los servicios de Azure que le afectan ahora mismo. 
2. **El mantenimiento planeado** -próximas acciones de mantenimiento que pueden afectar a la disponibilidad de Hola de los servicios en hello futuras.  
3. **Avisos de estado**: cambios en los servicios de Azure que requieren su atención. Por ejemplo, cuando están en desuso características de Azure o si se supera una cuota de uso.

    ![Eventos de Service Health](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a>Introducción a Service Health
el panel de estado del servicio, seleccione Hola estado del servicio toolaunch colocar en mosaico en el panel del portal. Si previamente ha quitado el icono de Hola o si está usando el panel personalizado, busque el servicio de mantenimiento de servicio de "Más servicios" (inferior izquierda del panel).
![Introducción a Service Health](./media/service-health-overview/azure-service-health-overview-1.png)

## <a name="see-current-issues-which-impact-your-services"></a>Consulta de los problemas actuales que afectan a los servicios
Hola **problemas del servicio** vista muestra los problemas en curso en servicios de Azure que afectan a los recursos. Puede saber cuándo se inició el problema de Hola y qué servicios y regiones se ven afectadas. También se puede leer toounderstand de actualización más reciente de hello lo que Azure está realizando el problema de hello tooresolve. 
![Administrar problemas de servicios](./media/service-health-overview/azure-service-health-overview-2.png)

Elija hello **impacto potencial** lista específica Hola de ficha toosee de recursos de su propiedad podría verse afectado por el problema de Hola. Puede descargar una lista CSV de estos recursos tooshare con su equipo.
![Administrar problemas de servicios - Impacto](./media/service-health-overview/azure-service-health-overview-4.png)

## <a name="get-links-and-downloadable-explanations"></a>Obtención de vínculos y explicaciones descargables 
Puede obtener un vínculo para hello problema toouse en su sistema de administración de problemas. Puede descargar PDF y, a veces, tooshare de archivos CSV con personas que no dispongan de acceso toohello portal de Azure.   
![Administrar problemas de servicios - Administración de problemas](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a>Obtención de soporte técnico de Microsoft
Si el recurso se deja en mal estado, incluso después de que se resuelve el problema de hello, póngase en contacto con soporte técnico.  Usar vínculos de soporte técnico de hello en hello derecha de la página de Hola.  

## <a name="pin-a-personalized-health-map-tooyour-dashboard"></a>Anclar un panel de estado personalizado mapa tooyour
Filtrar tooshow de estado del servicio sus suscripciones críticos para la empresa, regiones y tipos de recursos. Guardar filtro hello y anclar un panel personalizado mantenimiento world mapa tooyour portal. 
![Mapa de estado personalizado de filtro](./media/service-health-overview/azure-service-health-overview-6a.png)
![Anclar un mapa de estado personalizado](./media/service-health-overview/azure-service-health-overview-6b.png)

## <a name="configure-service-health-alerts"></a>Configuración de alertas de Service Health
Estado del servicio de Azure se integra con Azure Monitor tooalert es a través de mensajes de correo electrónico, mensajes de texto y las notificaciones de webhook cuando se ven afectados los recursos críticos para la empresa. Configurar una alerta de registro de actividad para eventos de estado del servicio de hello apropiado. Ruta toohello personas adecuadas de la organización mediante grupos de acciones de alerta. Para más información, consulte [Creación de alertas de registro de actividad en notificaciones del servicio](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).

# <a name="next-steps"></a>Pasos siguientes
Configure alertas de forma que se le notifiquen los problemas de mantenimiento. Para más información, consulte el artículo de [configuración de alertas para Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 