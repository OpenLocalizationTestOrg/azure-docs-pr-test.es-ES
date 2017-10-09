---
title: "aaaOverview de métricas en Microsoft Azure | Documentos de Microsoft"
description: "Información general sobre las métricas y su uso en Microsoft Azure"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Información general sobre las métricas en Microsoft Azure
Este artículo describe qué son las métricas en Microsoft Azure, sus ventajas y cómo toostart con ellos.  

## <a name="what-are-metrics"></a>¿Qué son las métricas?
Monitor de Azure permite la visibilidad de toogain de telemetría de tooconsume en el rendimiento de Hola y el estado de las cargas de trabajo en Azure. Hola el tipo más importante de los datos de telemetría de Azure es métricas hello (también denominadas contadores de rendimiento) emitidas por Azure más recursos. Monitor de Azure proporciona tooconfigure de varias maneras y consumir estas métricas para la supervisión y solución de problemas.

## <a name="what-can-you-do-with-metrics"></a>¿Para qué sirven las métricas?
Las métricas son una valiosa fuente de telemetría y habilitar hello toodo siguientes tareas:

* **Un seguimiento del rendimiento de hello** del recurso (por ejemplo, una aplicación de la máquina virtual, sitio Web o lógica) al trazar sus métricas en un gráfico de portal y fijar ese tooa gráfico del panel.
* **Recibir notificaciones de un problema** que impactos Hola rendimiento de su recurso cuando una métrica supera un umbral determinado.
* **Configurar acciones automatizadas**, como escalar automáticamente un recurso o activar un runbook cuando una métrica cruza un umbral determinado.
* **Realizar análisis avanzados** o elaborar informes de tendencias de rendimiento o de uso de los recursos.
* **Archivo** Hola historial de rendimiento o mantenimiento de su recurso **de cumplimiento o auditoría** fines.

## <a name="what-are-hello-characteristics-of-metrics"></a>¿Cuáles son las características de Hola de métricas?
Las métricas tienen Hola siguientes características:

* Todas las métricas tienen una **frecuencia de 1 minuto**. Recibirá un valor métrico de cada minuto desde el recurso, lo que le ofrece visibilidad en tiempo real en estado de Hola y el estado de su recurso casi.
* Las métricas están **disponibles de forma inmediata**. No necesita tooopt en o configurar diagnósticos adicionales.
* Puede acceder a **30 días del historial** de cada métrica. Puede buscar rápidamente las tendencias de mensual y recientes de hello en el rendimiento de Hola o estado del recurso.

También puede:

* Configurar una métrica **alerta regla que envía una notificación o toma la acción automatizada** cuando métrica Hola cruza el umbral de Hola que ha configurado. Escalado automático es una acción automatizada especial que permite tooscale espera las solicitudes entrantes de recursos toomeet o carga en su sitio Web o los recursos informáticos. Puede configurar una configuración de regla tooscale o alejar en función de una métrica de traspasar un umbral de escalado automático.

* **Ruta** todas las métricas Application Insights o análisis de registros (OMS) tooenable instantánea analytics, búsqueda y alertas personalizadas a datos de métricas de sus recursos. También puede transmitir métricas tooan concentrador de eventos, lo que le toothen enrutarlas tooAzure análisis de transmisiones o toocustom aplicaciones para el análisis casi en tiempo real. Puede configurar la transmisión del centro de eventos con la configuración de diagnóstico.

* **Archivar métricas toostorage** de retención más largo o usarlos para informes fuera de línea. Es posible distribuir el almacenamiento de blobs de métricas tooAzure al configurar opciones de diagnóstico para el recurso.

* Detectar fácilmente, tener acceso a, y **ver todas las métricas** a través del portal de Azure cuando seleccione un recurso y trazar métricas de hello en un gráfico de Hola.

* **Consumir** a través de las métricas de Hola Hola nuevas API de REST de Monitor de Azure.

* **Consulta** métricas mediante el uso de cmdlets de PowerShell de Hola u Hola API de REST de multiplataforma.

  ![Enrutamiento de métricas en Azure Monitor](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a>Métricas de acceso a través del portal de Hola
Aquí te mostramos una visita guiada rápida de cómo toocreate un gráfico de métrica mediante el uso de Hola portal de Azure.

### <a name="tooview-metrics-after-creating-a-resource"></a>métricas de tooview después de crear un recurso
1. Hola abrir portal de Azure.
2. Cree un sitio web de Azure App Service.
3. Después de crear un sitio Web, vaya a toohello **Introducción** hoja del sitio Web de Hola.
4. Puede ver las nuevas métricas como un icono de **Supervisión**. A continuación, puede editar mosaico hello y seleccionar métricas más.

   ![Métricas de un recurso en Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a>tooaccess todas las métricas en un solo lugar
1. Hola abrir portal de Azure.
2. Navegue toohello nueva **Monitor** pestaña y seleccione y, a continuación, Hola **métricas** opción aparecen debajo de él.
3. Seleccione la suscripción, el grupo de recursos y el nombre de hello del recurso de Hola de lista desplegable de Hola.
4. Ver la lista de métricas disponibles de Hola. A continuación, seleccione la métrica de hello interesa y trazar.
5. Puede anclar lo toohello panel haciendo clic en el pin de hello en la esquina superior derecha de Hola.

   ![Acceso a todas las métricas en un solo lugar en Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> Puede acceder a las métricas en el nivel de host de máquinas virtuales (basadas en Azure Resource Manager) y conjuntos de escalas de máquina virtual sin ninguna configuración adicional de diagnóstico. Estas nuevas métricas a nivel de host están disponibles para las instancias de Windows y Linux. Estas métricas no son toobe confundirse con hello las métricas de nivel de sistema operativo invitado que tienen toowhen acceso que activar diagnósticos de Azure en sus máquinas virtuales o conjuntos de escalas de máquina virtual. toolearn más información acerca de la configuración de diagnósticos, vea [¿qué es Microsoft Azure Diagnostics](../azure-diagnostics.md).
>
>

## <a name="access-metrics-via-hello-rest-api"></a>Métricas de acceso a través de la API de REST de Hola
Las métricas de Azure son accesibles a través de hello las API de supervisión de Azure. Hay dos API que facilitan la detección de métricas y el acceso a ellas:

* Hola de uso [API de REST de definiciones de métrica de supervisión de Azure](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess Hola lista de métricas que están disponibles para un servicio.
* Hola de uso [API de REST de métricas de supervisión de Azure](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess Hola datos de métricas real.

> [!NOTE]
> Este artículo tratan las métricas de Hola a través de hello [nueva API para las métricas de](https://msdn.microsoft.com/library/dn931930.aspx) para recursos de Azure. versión de API de Hola para definiciones de métrica nueva API de hello es 2016-03-01 y versión de Hola para las métricas de API es 2016-09-01. las métricas y las definiciones de métrica heredado de Hola pueden obtenerse con hello API versión 2014-04-01.
>
>

Para ver un tutorial más detallado usando hello las API de REST de Monitor de Azure, consulte [tutorial de API de REST de Azure Monitor](monitoring-rest-api-walkthrough.md).

## <a name="export-metrics"></a>Exportación de métricas
Puede ir toohello **configuración de diagnóstico** hoja en hello **Monitor** ficha y ver opciones de exportación de Hola para las métricas. Puede seleccionar las métricas (y registros de diagnóstico) toobe enrutan tooBlob almacenamiento, los concentradores de eventos de tooAzure o tooOMS para casos de uso que se mencionaron anteriormente en este artículo.

 ![Opciones de exportación de métricas en Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview3.png)

Puede configurar esto a través de plantillas de Resource Manager, [PowerShell](insights-powershell-samples.md), la [CLI de Azure](insights-cli-samples.md) o las [API de REST](https://msdn.microsoft.com/library/dn931943.aspx).

## <a name="take-action-on-metrics"></a>Realización de acciones en las métricas
notificaciones de tooreceive o automatizada de realizar acciones en datos de métrica, puede configurar reglas de alerta o configuración de escalado automático.

### <a name="configure-alert-rules"></a>Configuración de reglas de alerta
Puede configurar reglas de alerta basadas en las métricas. Estas reglas de alerta pueden comprobar si una métrica ha superado un umbral determinado. A continuación, pueden notificar por correo electrónico o activan un webhook que puede ser utilizado toorun cualquier secuencia de comandos personalizada. También puede utilizar las integraciones de hello webhook tooconfigure producto de otro fabricante.

 ![Métricas y reglas de alerta en Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Escalado automático de recursos de Azure
Algunos recursos de Azure admiten Hola escalado o de varios toohandle instancias las cargas de trabajo. Escalado automático aplica tooApp servicio (aplicaciones Web), conjuntos de escalas de máquina virtual y los servicios de nube de Azure clásico. Puede configurar tooscale de reglas de escalado automático o cuando una determinada métrica que afecta a la carga de trabajo supera un umbral que especifique. Para obtener más información, vea la [información general sobre la funcionalidad de escalado automático](monitoring-overview-autoscale.md).

 ![Métricas y escalado automático en Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>Más información sobre los servicios y las métricas compatibles
Azure Monitor es una nueva infraestructura de métricas. Admite Hola después de los servicios de Azure en hello Azure hello y portal de nueva versión de hello API de Monitor de Azure:

* Máquinas virtuales (basadas en Azure Resource Manager)
* Conjuntos de escalado de máquinas virtuales
* Batch
* Espacio de nombres de Event Hubs
* Espacio de nombres de Service Bus (solo SKU premium)
* SQL Database (versión 12)
* Elastic SQL Pool
* Sitios web
* Granjas de servidores web
* Aplicaciones lógicas
* IoT Hub
* Redis Cache
* Redes: puertas de enlace de aplicaciones
* Search

Puede ver una lista detallada de todos los servicios de hello compatibles y sus métricas en [métricas de supervisión de Azure--métricas admitidas por el tipo de recurso](monitoring-supported-metrics.md).

## <a name="next-steps"></a>Pasos siguientes
Consulte los vínculos de toohello a lo largo de este artículo. Además, puede obtener información sobre los siguientes temas:  

* [Métricas comunes de escalado automático](insights-autoscale-common-metrics.md)
* [¿Cómo toocreate las reglas de alerta](insights-alerts-portal.md)
* [Análisis de registros desde Azure Storage con Log Analytics](../log-analytics/log-analytics-azure-storage.md)
