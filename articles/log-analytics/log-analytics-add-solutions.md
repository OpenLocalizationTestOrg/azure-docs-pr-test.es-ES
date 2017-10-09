---
title: "soluciones de administración de análisis de registros de Azure aaaAdd | Documentos de Microsoft"
description: "Las soluciones de administración de Operations Management Suite (OMS)/Log Analytics son una colección de reglas de lógica, visualización y adquisición de datos que proporcionan métricas que giran en torno a una determinada área de problemas."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Agregar área de trabajo tooyour soluciones de administración de análisis de registros de Azure

Las soluciones de administración de Log Analytics son una colección de reglas de **lógica**, **visualización** y **adquisición de datos** que proporcionan métricas que giran en torno a una determinada área de problemas. Este artículo enumeran soluciones de administración compatibles con análisis de registros y muestra cómo tooadd y remove de un área de trabajo mediante el uso de Hola portal de Azure. También puede agregar soluciones en portal de OMS hello mediante Hola Galería de soluciones.

Las soluciones de administración permiten obtener información más detallada para:

* Ayudar a investigar y resolver los problemas operativos con más rapidez
* Recopilar y relacionar diversos tipos de datos de la máquina
* Ayudarle a ser proactivo con actividades que expone la solución de Hola.

> [!NOTE]
> Análisis de registros incluyen la funcionalidad de búsqueda de registros, por lo que no es necesario tooinstall una tooenable de solución de administración. Sin embargo, obtendrá visión, búsquedas sugeridas y visualizaciones de datos mediante la adición de área de trabajo de tooyour de soluciones de administración.

Mediante este artículo, agregar mediante el portal de Azure Marketplace Hola el área de trabajo de tooa a soluciones de administración. Después de agregar una solución, los datos se recopilan de los servidores de hello en su infraestructura y envía el servicio OMS toohello. Procesamiento por hello servicio OMS suele tarda horas de tooan de unos minutos. Después de servicio de hello procesa los datos de hello, podrá verlos en OMS.

Es posible quitar fácilmente una solución de administración cuando ya no se necesita. Cuando se quita una solución de administración, sus datos no se enviarán tooOMS. Si se encuentra en hello gratuita tarifa, quitar una solución puede reducir cantidad Hola de datos que se usan, ayudándole a ser debajo de la cuota diaria de datos.

## <a name="view-available-management-solutions"></a>Visualización de soluciones de administración disponibles

Hello Azure marketplace contiene lista Hola de [soluciones de administración de análisis de registros](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Puede instalar soluciones de administración de Azure marketplace, haga clic en hello **obtenerlo ahora** vínculo Hola final de cada solución.

## <a name="add-a-management-solution"></a>Incorporación de una solución de administración
1. Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com) con su suscripción de Azure.
2. Hola **New** hoja bajo **Marketplace**, seleccione **supervisión + administración**.
3. Hola **supervisión + administración** hoja, haga clic en **ver todas**.  
    ![Hoja Supervisión y administración](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. toohello derecha de **soluciones de administración de**, haga clic en **más**.
5. Hola **soluciones de administración de** hoja, seleccione una solución de administración que desea que el área de trabajo de tooadd tooa.  
    ![Hoja Supervisión y administración](./media/log-analytics-add-solutions/management-solutions.png)  
6. En la hoja de la solución de administración de hello, revise la información sobre solución de administración de hello y, a continuación, haga clic en **crear**.
7. Hola *nombre de la solución de administración* hoja, seleccione un área de trabajo que desee tooassociate con soluciones de administración de Hola.
8. Opcionalmente, cambiar la configuración de área de trabajo de hello suscripción de Azure, el grupo de recursos y la ubicación. También puede elegir **Opciones de Automation**. Haga clic en **Crear**.  
    ![área de trabajo de solución](./media/log-analytics-add-solutions/solution-workspace.png)  
9. toostart mediante la solución de administración de Hola que ha agregado el área de trabajo tooyour, navegue demasiado**análisis de registros** > **suscripciones** > ***nombre de área de trabajo ***  >  **Introducción**. Se muestra un icono nuevo para la solución de administración. Haga clic en hello mosaico tooopen se y comenzar a usar la solución de hello después de recopilaron los datos para la solución de Hola.

## <a name="remove-a-management-solution"></a>Eliminación de una solución de administración

1. Hola [portal de Azure](https://portal.azure.com), navegue demasiado**análisis de registros** > **suscripciones** > ***nombre de área de trabajo*** y, a continuación, en hello ***nombre de área de trabajo*** hoja, haga clic en **soluciones**.
2. En lista de hello soluciones de administración de, seleccione la solución de Hola que desea tooremove.
3. En la hoja de solución de hello para el área de trabajo, haga clic en **eliminar**.  
    ![eliminar solución](./media/log-analytics-add-solutions/solution-delete.png)  
4. En el cuadro de diálogo de confirmación de hello, haga clic en **Sí**.

## <a name="offers-and-pricing-tiers"></a>Ofertas y planes de tarifa

Hello en la tabla siguiente identifica qué soluciones de administración pertenecen tooeach oferta de Operations Management Suite.
tabla de Hello también identifica Hola los niveles que están disponibles para cada solución de administración de precios.
Todas las soluciones de hello en la tabla siguiente están disponibles en la Galería de soluciones hello y portal de Azure en el portal de análisis de registros de Hola Hola.

| Solución de administración                                                                       | Oferta                                                                     | Planes de tarifa<sup>1</sup>                                                 | Notas |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Análisis de registros de actividad](log-analytics-activity.md)                                                                   | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | 90 días de datos disponibles de forma gratuita<br>Datos no sometan el límite del nivel gratis toohello |
| [Evaluación de AD](log-analytics-ad-assessment.md)                                           | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Estado de replicación de AD](log-analytics-ad-replication-status.md)                           | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | Tooadd no está disponible desde el portal de Azure/marketplace. |
| [Agent Health](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | Datos no sometan el límite del nivel gratis toohello<br> Tooadd no está disponible desde el portal de Azure/marketplace. |
| [Administración de alertas](log-analytics-solution-alert-management.md)                            | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | Tooadd no está disponible desde el portal de Azure/marketplace. |
| [Application Insights Connector (versión preliminar)](log-analytics-app-insights-connector.md)                                               | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Automation Hybrid Worker](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Automation and Control</li></ul>                                  | Gratuito<br> Por&nbsp;nodo&nbsp;(OMS)                                                                         | Requiere la tooan de toobe vinculado del área de trabajo de análisis de registros cuenta de automatización |
| [Azure Application Gateway Analytics](log-analytics-azure-networking-analytics.md)    | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Azure Network Security Group Analytics](log-analytics-azure-networking-analytics.md)     | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Azure SQL Analytics (versión preliminar)](log-analytics-azure-sql.md)                                                       | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br>Por&nbsp;nodo&nbsp;(OMS)                                                                          | Requiere la tooan de toobe vinculado del área de trabajo de análisis de registros cuenta de automatización|
| [Azure Web Apps Analytics](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
|[Copia de seguridad](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Insight and Analytics</li></ul>                                   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)                                                                       | Requiere un almacén de Backup clásico.<br> Tooadd no está disponible desde el portal de Azure/marketplace. |
| [Capacity and Performance (versión preliminar)](log-analytics-capacity.md)                                                   | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Seguimiento de cambios](log-analytics-change-tracking.md)                                       | <ul><li>Automation and Control</li></ul>                                  | Gratuito<br> Por&nbsp;nodo&nbsp;(OMS)                                                                         | Requiere la tooan de toobe vinculado del área de trabajo de análisis de registros cuenta de automatización |
| [Contenedores](log-analytics-containers.md)                                                 | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [IT Service Management Connector (versión preliminar)](log-analytics-itsmc-overview.md)                                              | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Por&nbsp;nodo&nbsp;(OMS)     | |
| Supervisión de HDInsight HBase <br>(versión preliminar)                                                  | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Análisis de Key Vault](log-analytics-azure-key-vault.md)                   | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Logic Apps B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | Tooadd no está disponible desde el portal de Azure/marketplace. |
| [Evaluación de malware](log-analytics-malware.md)                                            | <ul><li>Seguridad y cumplimiento normativo</li></ul>                                 | Gratuito<br> Independiente<br>Por&nbsp;nodo&nbsp;(OMS)                                                                           | Si agrega las soluciones de seguridad y cumplimiento de normas de hello después del 19 de junio de 2017 [facturación es por nodo](https://azure.microsoft.com/pricing/details/security-compliance/), independientemente del nivel de precios de área de trabajo de Hola. Hello primeros 60 días son gratuitas.  |
| [Monitor de rendimiento de red](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Insight and Analytics</li></ul>                                   | Gratuito<br> Por&nbsp;nodo&nbsp;(OMS)                                                                         | |
| [Office 365 Analytics (versión preliminar)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Seguridad y auditoría](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Seguridad&nbsp;y&nbsp;cumplimiento</li></ul>                       | Gratuito<br> Independiente<br>Por&nbsp;nodo&nbsp;(OMS)                                                                           | Se necesita esta solución para recopilar registros de eventos de seguridad<br>Si agrega las soluciones de seguridad y cumplimiento de normas de hello después del 19 de junio de 2017 [facturación es por nodo](https://azure.microsoft.com/pricing/details/security-compliance/), independientemente del nivel de precios de área de trabajo de Hola. Hello primeros 60 días son gratuitas. |
| [Service Fabric Analytics (versión preliminar)](log-analytics-service-fabric.md)                     | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Service Map (versión preliminar)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Insight and Analytics</li></ul>                      | Gratuito<br> Por&nbsp;nodo&nbsp;(OMS)                                                                         | Disponible en Este y Centro de EE. UU. y Europa Occidental    |
| [Recuperación de sitios](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Insight and Analytics</li></ul>                                   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)                                                                       | Requiere un almacén de Site Recovery clásico.<br> Tooadd no está disponible desde el portal de Azure/marketplace. |
| [Evaluación de SQL](log-analytics-sql-assessment.md)                                         | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| Inicio y detención de máquinas virtuales durante las horas de trabajo<br>(versión preliminar)                                              | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Por&nbsp;nodo&nbsp;(OMS)                                                                         | Requiere la tooan de toobe vinculado del área de trabajo de análisis de registros cuenta de automatización |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | Tooadd no está disponible desde el portal de Azure/marketplace. |
| [System Center Operations Manager Assessment (versión preliminar)](log-analytics-scom-assessment.md)  | <ul><li>Insight and Analytics</li><li>Log Analytics</li></ul>        | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Administración de actualizaciones](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Automation and Control</li></ul>                                  | Gratuito<br> Por&nbsp;nodo&nbsp;(OMS)                                                                         | Requiere la tooan de toobe vinculado del área de trabajo de análisis de registros cuenta de automatización |
| [Update Compliance (versión preliminar)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | Sin cargos para datos ni nodos<br>Datos no sometan el límite del nivel gratis toohello.<br> Tooadd no está disponible desde el portal de Azure/marketplace. |
| [Preparación para la actualización](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | Sin cargos para datos ni nodos<br>Datos no sometan el límite del nivel gratis toohello.<br> Tooadd no está disponible desde el portal de Azure/marketplace. |
| [VMware Monitoring (versión preliminar)](log-analytics-vmware.md)                                | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Estándar<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(independiente)<br> Por&nbsp;nodo&nbsp;(OMS)   | |
| [Wire Data 2.0 (versión preliminar)](log-analytics-wire-data.md)                                                                 | <ul><li>Insight and Analytics</li></ul>                                   | Gratuito<br> Por&nbsp;nodo&nbsp;(OMS)                                                                         | Disponible en Este y Centro de EE. UU. y Europa Occidental |

<sup>1</sup> hello *estándar* y *Premium (OMS)* niveles de precios solo están disponibles para los clientes que creó su área de trabajo de análisis de registros anterior tooSeptember 21, 2016.

### <a name="community-provided-management-solutions"></a>Soluciones de administración proporcionadas por la comunidad

Comunidad proporciona soluciones están disponibles desde hello [Galería de plantillas de Azure](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) y directo de los autores de Hola.

| Solución de administración               | Oferta                                                                     | Planes de tarifa                         | Notas |
| ---                               | ---                                                                       | ---                                   | ---   |
| Todas las soluciones proporcionadas por la comunidad  | <ul><li>Insight&nbsp;and&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Por&nbsp;nodo&nbsp;(OMS)     |   Requiere la tooan de toobe vinculado del área de trabajo de análisis de registros cuenta de automatización |




## <a name="data-collection-details"></a>Detalles de la recopilación de datos
Hello en las tablas siguientes muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos de orígenes de datos y soluciones de administración de análisis de registros. Hello tablas se dividen por categorías ofertas de soluciones, que son demasiado igual[los niveles de precios de suscripción](https://go.microsoft.com/fwlink/?linkid=827926). Hola soluciones de análisis de registros de actividad es tooall disponible de forma gratuita de niveles de precios.

Hola a agente de Windows de análisis de registro y System Center Operations Manager agente son esencialmente Hola igual. el agente de Windows Hello incluye una funcionalidad adicional tooallow se tooconnect toohello OMS enrutar a través de un servidor proxy y el área de trabajo. Si utiliza a un agente de Operations Manager, se debe aplicar como un toocommunicate de agente OMS con OMS. Agentes de Operations Manager en esta tabla son agentes OMS que se encuentran conectados tooOperations Manager. Vea [tooLog de conexión de Operations Manager análisis](log-analytics-om-agents.md) para obtener información acerca de cómo conectar su tooOMS de entorno de Operations Manager existente.

> [!NOTE]
> tipo de Hola de agente que usa determina cómo se envían datos tooOMS, con hello condiciones siguientes:
> - Usa el agente de Windows hello o un agente de OMS conectados a Operations Manager.
> - Cuando se requiere Operations Manager, datos del agente de Operations Manager para la solución de hello siempre se envían tooOMS utilizar Hola grupo de administración de Operations Manager. Además, cuando se requiere Operations Manager, solución de hello utiliza solo el agente de Operations Manager Hola.
> - Cuando Operations Manager no es necesario y tabla de hello muestra que los datos del agente de Operations Manager se envían tooOMS con grupo de administración de hello y, a continuación, datos del agente de Operations Manager se envían siempre tooOMS con grupos de administración. Agentes de Windows omitir el grupo de administración de Hola y envían sus datos tooOMS directamente.
> - Si no se envían datos de agente de Operations Manager con un grupo de administración, a continuación, Hola se enviarán datos directamente tooOMS: omitiendo el grupo de administración de Hola.

### <a name="insight--analytics--log-analytics"></a>Insight and Analytics/Log Analytics

| Solución de administración | Plataforma | Microsoft Monitoring Agent | Agente de Operations Manager | Almacenamiento de Azure | ¿Se requiere Operations Manager? | Se envían los datos del agente de Operations Manager a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Análisis de registros de actividad | Azure |   |   |   |   |   | según notificación |
| Evaluación de AD |Windows |&#8226; |&#8226; |  |  |&#8226; |7 días |
| Estado de replicación de AD |Windows |&#8226; |&#8226; |  |  |&#8226; |5 días |
| Estado de mantenimiento de los agentes | Windows y Linux | &#8226; | &#8226; |   |   | &#8226; | 1 minuto |
| Administración de alertas (Nagios) |Linux |&#8226; |  |  |  |  |a la llegada |
| Administración de alertas (Zabbix) |Linux |&#8226; |  |  |  |  |1 minuto |
| Administración de alertas (Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 minutos |
| Application Insights Connector (versión preliminar) | Azure |   |   |   |   |   | según notificación |
| Azure Application Gateway Analytics | Azure |   |   |   |   |   | según notificación |
| Azure Network Security Group Analytics | Azure |   |   |   |   |   | según notificación |
| Azure SQL Analytics (versión preliminar) |Windows |  |  |  |  |  | 10 minutos |
| Administración de la capacidad |Windows |&#8226; |&#8226; |  |  |&#8226; |a la llegada |
| Contenedores | Windows y Linux | &#8226; | &#8226; |   |   |   | 3 minutos |
| Análisis de Key Vault |Windows |  |  |  |  |  |según notificación |
| Monitor de rendimiento de red | Windows | &#8226; | &#8226; |   |   |   | Protocolos de enlace TCP cada 5 segundos; se envían datos cada 3 minutos. |
| Office 365 Analytics (versión preliminar) |Windows |  |  |  |  |  |según notificación |
| Service Fabric Analytics |Windows |  |  |&#8226; |  |  |5 minutos |
| Mapa de servicio | Windows y Linux | &#8226; | &#8226; |   |   |   | 15 segundos |
| Evaluación de SQL |Windows |&#8226; |&#8226; |  |  |&#8226; |7 días |
| SurfaceHub |Windows |&#8226; |  |  |  |  |a la llegada |
| Evaluación de System Center Operations Manager (versión preliminar) | Windows | &#8226; | &#8226; |   |   | &#8226; | siete días |
| Upgrade Analytics (versión preliminar) | Windows | &#8226; |   |   |   |   | 2 días |
| Supervisión de VMware (versión preliminar) | Linux | &#8226; |   |   |   |   | 3 minutos |
| Wire Data |Windows (2012 R2 / 8.1 o posterior) |&#8226; |&#8226; |  |  |  | 1 minuto |


### <a name="automation--control"></a>Automation & Control

| Solución de administración | Plataforma | Microsoft Monitoring Agent | Agente de Operations Manager | Almacenamiento de Azure | ¿Se requiere Operations Manager? | Se envían los datos del agente de Operations Manager a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Automation Hybrid Worker | Windows | &#8226; | &#8226; |   |   |   | N/D |
| Seguimiento de cambios |Windows |&#8226; |&#8226; |  |  |&#8226; |cada hora |
| Seguimiento de cambios |Linux |&#8226; |  |  |  |  |cada hora |
| Administración de actualizaciones | Windows |&#8226; |&#8226; |  |  |&#8226; |al menos 2 veces al día y 15 minutos después de instalar una actualización |

### <a name="security--compliance"></a>Seguridad y cumplimiento

| Solución de administración | Plataforma | Microsoft Monitoring Agent | Agente de Operations Manager | Almacenamiento de Azure | ¿Se requiere Operations Manager? | Se envían los datos del agente de Operations Manager a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Evaluación antimalware |Windows |&#8226; |&#8226; |  |  |&#8226; |cada hora |
| Seguridad y auditoría<sup>1</sup> | Windows y Linux | parcial | parcial | parcial |   | parcial | varias |

<sup>1</sup> Hola seguridad y solución de auditoría puede recopilar registros de agentes de Windows, Operations Manager y Linux. Consulte [Orígenes de datos](#data-sources) para información sobre la recopilación de datos para:

- syslog
- Registros de eventos de seguridad de Windows
- Registros de Firewall de Windows
- Registros de eventos de Windows



### <a name="protection--recovery"></a>Protección y recuperación

| Solución de administración | Plataforma | Microsoft Monitoring Agent | Agente de Operations Manager | Almacenamiento de Azure | ¿Se requiere Operations Manager? | Se envían los datos del agente de Operations Manager a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Backup | Azure |   |   |   |   |   | N/D |
| Azure Site Recovery | Azure |   |   |   |   |   | N/D |


### <a name="data-sources"></a>Orígenes de datos


| Origen de datos | Plataforma | Microsoft Monitoring Agent | Agente de Operations Manager | Almacenamiento de Azure | ¿Se requiere Operations Manager? | Se envían los datos del agente de Operations Manager a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Registros de actividad de Azure |Windows |  |  |  |  |  |según notificación |
| Registros de diagnóstico de Azure |Windows |  |  |  |  |  |según notificación |
| Métricas de diagnósticos de Azure |Windows |  |  |  |  |  |según notificación |
| ETW |Windows |  |  |&#8226; |  |  |5 minutos |
| Registros IIS |Windows |&#8226; |&#8226; |&#8226; |  |  |5 minutos |
| Contadores de rendimiento |Windows |&#8226; |&#8226; |  |  |  |mínimo de 10 segundos, según lo programado |
| Contadores de rendimiento |Linux |&#8226; |  |  |  |  |mínimo de 10 segundos, según lo programado |
| syslog |Linux |&#8226; |  |  |  |  |De Almacenamiento de Azure: 10 minutos; del agente: a la llegada |
| Registros de eventos de seguridad de Windows |Windows |&#8226; |&#8226; |&#8226; |  |  |para el almacenamiento de Azure: 10 min; para el agente de hello: a la llegada |
| Registros de Firewall de Windows |Windows |&#8226; |&#8226; |  |  |  |a la llegada |
| Registros de eventos de Windows |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |para el almacenamiento de Azure: 10 min; para el agente de hello: a la llegada |



## <a name="preview-management-solutions-and-features"></a>Versión preliminar de características y soluciones de administración
Ejecutar un servicio y los siguientes procedimientos recomendados de devops, estamos capaz de toopartner con los clientes toodevelop características y soluciones.

Durante la vista previa privada, se proporcionan un grupo pequeño de los clientes acceso tooan rápida puesta en marcha de comentarios de Hola característica o solución toogain y realizar mejoras. Esta implementación temprana posee las características y funciones operativas mínimas.

Nuestro objetivo es tootry cosas rápidamente por lo que podemos encontrar lo que funciona y lo que no funciona. Se recorra en iteración este proceso hasta que los comentarios de Hola de los clientes de vista previa privada de hello nos informa de que se está listos para una versión preliminar pública.

Durante la versión preliminar pública de hello, se estén característica Hola o soluciones disponibles para tooget de todos los usuarios más comentarios y validan el ajuste de escala y la eficacia. Durante esta fase:

* Características de vista previa aparecen en la ficha de configuración de Hola y pueden habilitarse por cualquier usuario.
* Soluciones de vista previa se agregan a través de la Galería de Hola o mediante un script.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>¿Qué hay que saber sobre la versión preliminar de las características y soluciones?
Nos complace sobre las nuevas características y soluciones de administración y nos encanta trabajar con toodevelop ellos.

Las soluciones y características en versión preliminar no son adecuadas para todos los usuarios. Antes de solicitar toojoin una vista previa privada o habilitar una versión preliminar pública, asegúrese de que aceptar trabaja con algo que está en desarrollo.

Al habilitar una característica de vista previa a través del portal de hello, verá una advertencia recordándole que Hola característica está en vista previa.

#### <a name="for-both-private-and-public-preview"></a>Común a las versiones preliminares *públicas* y *privadas*
Hello siguiente información aplica vistas previas públicas y privadas de tooboth:

* Las cosas no siempre funcionan como deben.
  * Emite intervalo ante una molestia a través de toosomething no funciona en absoluto.
* Hay posibles para toohave de vista previa de hello un impacto negativo en sus sistemas / entorno.
  * Intentamos tooavoid cosas negativo ocurra toohello sistemas que está usando con OMS pero cosas inesperados a veces se producen.
* Se pueden producir pérdidas de datos y daños.
* Le pidamos que los registros de diagnóstico de toocollect u otro toohelp datos solucionar problemas.
* característica de Hola o una solución puede quitarse (de forma temporal o permanente).
  * Según lo que hemos aprendido durante la vista previa de hello podemos decidimos característica Hola de toonot versión o una solución.
* Puede que las vistas previas no funcionen o no se hayan probado con todas las configuraciones, a raíz de lo cual podremos limitar:
  * Hola sistemas operativos que se puede utilizar (por ejemplo, una característica sólo puede aplicar tooLinux en la vista previa).
  * Hola tipo de agente (MMA, Operations Manager) que se puede utilizar (por ejemplo, una característica no funcionen con Operations Manager en la vista previa).  
* Características y soluciones de vista previa no están cubiertas por hello contrato de nivel de servicio.
* El uso de las características en versión preliminar conllevará gastos.
* Las características o funcionalidades que necesita para la característica de Hola y puede ser útil de solución toobe falta o está incompleto.
* Puede que las características o soluciones no estén disponibles en todas las regiones.
* Puede que las características o soluciones no estén localizadas.
* Características / soluciones tienen un límite de número de Hola de clientes o dispositivos que pueden usar.
* Puede que necesite toouse scripts tooperform configuración y tooenable Hola/características de soluciones.
* interfaz de usuario (UI) de Hello está incompleta y se puede cambiar de día tooday.
* Puede que las versiones preliminares públicas no sean adecuadas en sistemas críticos o de producción.

#### <a name="for-private-preview"></a>Vistas previas *privadas*
En elementos de toohello de suma anteriores, Hola siguiente información es vistas previas de tooprivate específica:

* Esperamos que tooprovide nos con comentarios sobre su experiencia para que podemos hacer Hola característica o solución mejor.
* Puede que nos pongamos en contacto con usted para pedirle comentarios mediante encuestas, llamadas de teléfono o correo electrónico.
* No todo funcionará siempre como debiera.
* Puede que requiramos un acuerdo de confidencialidad para participar o que incluyamos contenido confidencial.
  * Antes de iniciar un blog, realizar TWEETS o, en caso contrario, se comunica con terceros, compruebe con el Administrador de programas que se encarga de toounderstand de vista previa de Hola Hola todas las restricciones de divulgación de información.
* No ejecute la versión preliminar en sistemas críticos o de producción.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>¿Cómo puedo obtener características de vista previa de acceso tooprivate y soluciones?
Le invitamos a las vistas previas de los clientes tooprivate a través de varias maneras diferentes dependiendo de la vista previa de Hola.

* Responder a encuestas de cliente mensual de Hola y abandonarla nos permiso toofollow contigo mejoran sus posibilidades de que se va a vista previa privada de tooa invitados.
* El equipo de cuentas de Microsoft puede elegirle.
* Puede registrarse conforme a la información publicada en [msopsmgmt](https://twitter.com/msopsmgmt).
* Puede registrarse basándose en detalles compartidos en eventos comunitarios: búsquenos en encuentros, conferencias y en comunidades en línea.

## <a name="next-steps"></a>Pasos siguientes
* [Buscar registros](log-analytics-log-searches.md) tooview detallada información recopilada por soluciones de administración.
