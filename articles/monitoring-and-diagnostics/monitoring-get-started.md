---
title: aaaGet trabajar con el Monitor de Azure | Documentos de Microsoft
description: "Introducción al uso de una visión general de Azure Monitor toogain en operación de Hola de los recursos y realizar acciones en función de los datos."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a>Introducción a Azure Monitor
Monitor de Azure es servicio de plataforma de Hola que proporciona un único origen para la supervisión de recursos de Azure. Con el Monitor de Azure, puede visualizar, consultar, enrutar, archivar y tomar medidas sobre las métricas de Hola y registros procedentes de recursos de Azure. Puede trabajar con estos datos con la hoja de portal de Monitor de hello, [Cmdlets de PowerShell de Monitor](insights-powershell-samples.md), [multiplataforma CLI](insights-cli-samples.md), o [API de REST de Azure Monitor](https://msdn.microsoft.com/library/dn931943.aspx). En este artículo se abordan algunos de los componentes clave de Hola de Monitor de Azure, mediante el portal de Hola de demostración.

1. En el portal de hello, navegue demasiado**más servicios** y buscar hello **Monitor** opción. Haga clic en tooadd de icono de estrella de hello esta lista de favoritos de opción tooyour para que siempre sea fácilmente accesible desde la barra de navegación del lado izquierdo de Hola.
   
    ![Supervisar en la lista de servicios de Hola](./media/monitoring-get-started/monitor-more-services.png)
2. Haga clic en hello **Monitor** tooopen opción seguridad hello **Monitor** hoja. En esta hoja se encuentran toda la configuración de supervisión y los datos en una sola vista consolidada. Abre por primera vez toohello **registro de actividad** sección.
   
    ![Navegación en la hoja Monitor](./media/monitoring-get-started/monitor-blade-nav.png)
   
    Monitor de Azure tiene tres categorías básicas de los datos de supervisión: Hola **registro de actividad**, **métricas**, y **registros de diagnóstico**.
3. Haga clic en **registro de actividad** tooensure que Hola sección del registro de actividad se muestra.
   
    ![Hoja Registro de actividades](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    Hola [ **registro de actividad** ](monitoring-overview-activity-logs.md) describe todas las operaciones realizadas en recursos de la suscripción. Gracias a Hola registro de actividad, puede determinar hello ' qué, quién y cuándo ' para cualquier crear, actualizar o eliminar las operaciones en recursos de la suscripción. Por ejemplo, hello registro de actividad indica cuando una aplicación web se ha detenido y que detuvo. Eventos de registro de actividad se almacenan en la plataforma de Hola y tooquery disponible durante 90 días.
   
    Puede crear y guardar consultas para filtros comunes y, a continuación, pin hello más importantes consultas tooa panel del portal, por lo que siempre sabrá si se han producido eventos que cumplen los criterios.
4. Filtrar Hola vista tooa determinado grupo de recursos a través de hello última semana, haga clic en hello **guardar** botón.
   
    ![Guardar consulta de registro de actividad](./media/monitoring-get-started/monitor-act-log-save.png)
5. Ahora, haga clic en hello **Pin** botón.
   
    ![Haga clic en Anclar para anclar el registro de actividades](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    La mayoría de las vistas de hello en este tutorial puede ser anclados tooa panel. Esto ayuda a crear un único origen de información de datos operativos de los servicios. 
6. Panel de tooyour devuelto. Ahora puede ver que consulta Hola (y el número de resultados) se muestran en el panel. Esto es útil si desea que consulte tooquickly las acciones de alto perfil que se han producido recientemente en su suscripción, p. ej. se ha asignado un nuevo rol o se ha eliminado una máquina virtual.
   
    ![Actividad registro anclado toodashboard](./media/monitoring-get-started/monitor-act-log-db.png)
7. Devolver toohello **Monitor** icono y haga clic en hello **métricas** sección. Primero debe tooselect un recurso de filtrado y seleccionando using Hola desplegable Opciones principio de Hola de hoja de Hola.
   
    ![Recursos de filtro para las métricas](./media/monitoring-get-started/monitor-met-filter.png)
   
    Todos los recursos de Azure emiten [**métricas**](monitoring-overview-metrics.md). Esta vista reúne todas las métricas en un solo panel de vidrio para que pueda comprender fácilmente el rendimiento de los recursos.
8. Una vez haya seleccionado un recurso, todas las métricas disponibles aparecen en la parte izquierda de la hoja de Hola de Hola. Puede varias métricas del gráfico a la vez seleccionando las métricas y modificar el intervalo de tipo y la hora del gráfico de Hola. También puede ver todas las alertas de métricas establecidas en este recurso.
   
    ![Cuadro de métricas](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > Algunas métricas solo están disponibles si se habilita [Application Insights](../application-insights/app-insights-overview.md) o Windows, o Linux Azure Diagnostics en el recurso.
   > 
   > 
9. Cuando esté satisfecho con el gráfico, puede usar hello **Pin** toopin de botón tooyour panel.
10. Devolver toohello **Monitor** hoja y haga clic en **registros de diagnóstico**.
    
    ![Hoja Registros de diagnóstico](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    [**Registros de diagnóstico** ](monitoring-overview-of-diagnostic-logs.md) son registros genera *por* un recurso que proporcionan datos sobre el funcionamiento de Hola de ese recurso. Por ejemplo, los contadores de reglas de grupo de seguridad de red y los registros de flujo de trabajo de aplicación lógica son tipos de registros de diagnóstico. Estos registros se pueden almacenados en una cuenta de almacenamiento, transmitido tooan concentrador de eventos, o enviar demasiado[análisis de registros](../log-analytics/log-analytics-overview.md). Log Analytics es el producto de inteligencia operativa de Microsoft para búsqueda avanzada y alertas.
    
    En el portal de hello puede ver y filtrar una lista de todos los recursos en su suscripción tooidentify si tienen registros de diagnóstico habilitados.
11. Haga clic en un recurso en la hoja de registros de diagnóstico de Hola. Si los registros de diagnóstico se almacenan en una cuenta de almacenamiento, verá una lista de registros por hora que se pueden descargar directamente.
    
    ![Registros de diagnóstico para un recurso](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    También puede hacer clic en **configuración de diagnóstico**, que permite tooset seguridad o modificar la configuración de cuenta de almacenamiento de archivo tooa, tooEvent centros de transmisión por secuencias, o enviar el área de trabajo de análisis de registros tooa.
    
    ![Habilitar registros de diagnóstico](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    Si ha configurado tooLog análisis de registros de diagnóstico, puede buscar ellos, a continuación, en hello **búsqueda de registros** sección del portal de Hola de.
12. Navegue toohello **alertas** sección de hoja de Monitor de Hola.
    
    ![hoja de alertas para el público](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    Aquí puede administrar todas las [**alertas**](monitoring-overview-alerts.md) de los recursos de Azure. Esto incluye alertas en métricas, eventos de registro de actividad, pruebas web de Application Insights (ubicaciones) y diagnósticos proactivos de Application Insights. Las alertas pueden activar un toobe de correo electrónico enviado o una dirección URL de HTTP POST tooa webhook.
13. Haga clic en **Agregar alerta métrica** toocreate una alerta.
    
    ![Add metric alert](./media/monitoring-get-started/monitor-alerts-add.png)
    
    También puede anclar un tooeasily del panel de alerta tooyour ver su estado en cualquier momento.
14. Hola sección Monitor también incluye vínculos demasiado[Application Insights](../application-insights/app-insights-overview.md) aplicaciones y [análisis de registros](../log-analytics/log-analytics-overview.md) soluciones de administración. Estos otros productos de Microsoft están perfectamente integrados en Azure Monitor.
15. Si no usa Application Insights o Log Analytics, lo más probable es que Azure Monitor tenga una asociación con los productos actuales de supervisión, registro y alertas. Consulte nuestro [página de socios](monitoring-partners.md) para obtener una lista completa e instrucciones sobre cómo toointegrate.

Siguiendo estos pasos y anclar el panel de tooa de todos los iconos pertinentes, puede crear vistas completa de la aplicación y la infraestructura como este:

![Panel de Azure Monitor](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>Pasos siguientes
* Hola de lectura [Monitor de información general de Azure](monitoring-overview.md)

