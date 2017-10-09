---
title: "Conector de administración de servicio de OMS aaaIT | Documentos de Microsoft"
description: "Use Hola conector de administración de servicios de TI toocentrally supervisión y administrar elementos de trabajo ITSM hello en OMS, y solucione los problemas rápidamente."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>Administración centralizada de los elementos de trabajo ITSM con IT Service Management Connector (versión preliminar)

![Símbolo de IT Service Management Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

Puede usar hello conector de administración de servicio de TI (ITSMC) en el monitor de toocentrally de análisis de registros de OMS y administrar elementos de trabajo entre sus productos y servicios ITSM.

Hola conector de administración de servicios de TI integra los servicios y productos de administración de servicio de TI (ITSM) existente con análisis de registros de OMS.  solución de Hello tiene integración bidireccional con productos o servicios a ITSM, donde proporciona Hola incidentes toocreate opción de los usuarios de OMS, alertas o eventos de solución ITSM. Conector de Hello también importa datos tales como incidentes y solicitudes de cambio de solución ITSM en análisis de registros de OMS.

Con IT Service Management Connector, puede:

  - Supervisar y administrar de manera centralizada elementos de trabajo para productos y servicios de ITSM que se usan en toda la organización.
  - Crear elementos de trabajo de ITSM (como alertas, eventos, incidentes) en ITSM desde alertas de OMS y a través de la búsqueda de registros.
  - Leer incidentes y solicitudes de cambio en la solución ITSM y correlacionarlos con los datos de registro correspondientes en el área de trabajo de Log Analytics.
  - Buscar cualquier evento inesperado e inusual y resolverlos, incluso antes de que los usuarios finales de hello llamar y registrarlos toohello departamento de soporte técnico.
  - Importar datos de elementos de trabajo a Log Analytics y crear informes de indicador de rendimiento clave (KPI).  Con estos informes, puede identificar y evaluar varios elementos importantes, como la evaluación de malware, y actuar en consecuencia.
  - Ver paneles protegidos para obtener información más detallada sobre incidentes, solicitudes de cambio y sistemas afectados.
  - Solucionar problemas con mayor rapidez al correlacionar con otras soluciones de administración en el área de trabajo de análisis de registros de Hola.


## <a name="prerequisites"></a>Requisitos previos

elementos de trabajo de tooimport Hola ITSM en análisis de registros de OMS, solución de hello requiere una conexión entre Hola conector de administración de servicios de TI en OMS de Hola y Hola TI SM productos o servicios desde la que importar elementos de trabajo de Hola.


## <a name="configuration"></a>Configuración

Hola de agregar espacio de trabajo OMS de tooyour de la solución de conector de administración de servicios de TI, mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).

Conector de administración de servicios de TI icono como se ve en la Galería de soluciones de hello:

![icono de conector](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Tras la adición de correcta, verá Hola conector de administración de servicios de TI en **OMS** > **configuración** > **orígenes conectados.**

![ITSMC conectado](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> De forma predeterminada, Hola conector de administración de servicios de TI actualiza los datos de la conexión de hello una vez en cada 24 horas. toorefresh datos de la conexión al instante para cualquier plantilla o modificaciones actualizan realizados, haga clic en conexión siguiente tooyour de hello actualización botón que se muestra.

 ![Actualización de ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Módulos de administración
Esta solución no necesita ningún módulo de administración.

## <a name="connected-sources"></a>Orígenes conectados

Hello siguientes ITSM productos/servicios admite Hola conector de administración de servicios de TI:

- [System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>Uso de solución de Hola

Una vez Hola conector de administración de servicios de TI de OMS se conecta con el servicio ITSM, servicios de análisis de registros de hello inicia la recopilación de datos de Hola Hola conectado ITSM productos/service.

> [!NOTE]
> - Los datos que importa la solución IT Service Management Connector aparecen en Log Analytics como eventos denominados **ServiceDesk_CL**.
- Los eventos contienen un campo llamado **ServiceDeskWorkItemType_s**. que puede tomar su valor como incidentes, o solicitud de cambio, función hello de elemento de trabajo datos contenidos en hello **ServiceDesk_CL** eventos.

## <a name="input-data"></a>Datos de entrada
Los elementos de trabajo importan de hello ITSM productos y servicios.

Hello información siguiente muestra ejemplos de datos recopilados por el conector de administración de servicios de TI de hello:

> [!NOTE]
> Función hello de elemento de trabajo importado en el análisis de registros de tipo **ServiceDesk_CL** contiene Hola siguientes campos:

**Elemento de trabajo:****incidentes**  
ServiceDeskWorkItemType_s="Incidente"

**Fields**

- ServiceDeskConnectionName
- Service Desk ID
- Estado
- Urgencia
- Impacto
- Prioridad
- Escalado
- Creado por
- Resuelto por
- Cerrado por
- Origen
- Asignado a
- Categoría
- Título
- Descripción
- Fecha de creación
- Fecha de cierre
- Fecha de resolución
- Fecha de última modificación
- Equipo


**Elemento de trabajo:****solicitudes de cambio**

ServiceDeskWorkItemType_s="ChangeRequest"

**Fields**
- ServiceDeskConnectionName
- Service Desk ID
- Creado por
- Cerrado por
- Origen
- Asignado a
- Título
- Tipo
- Categoría
- Estado
- Escalado
- Estado del conflicto
- Urgencia
- Prioridad
- Riesgo
- Impacto
- Asignado a
- Fecha de creación
- Fecha de cierre
- Fecha de última modificación
- Fecha de solicitud
- Fecha de inicio planeada
- Fecha de finalización planeada
- Fecha de inicio del trabajo
- Fecha de finalización del trabajo
- Descripción
- Equipo

## <a name="output-data-for-a-servicenow-incident"></a>Datos de salida para un incidente de ServiceNow

| Campo OMS | Campo ITSM |
|:--- |:--- |
| ServiceDeskId_s| Number |
| IncidentState_s | Estado |
| Urgency_s |Urgencia |
| Impact_s |Impacto|
| Priority_s | Prioridad |
| CreatedBy_s | Abierto por |
| ResolvedBy_s | Resuelto por|
| ClosedBy_s  | Cerrado por |
| Source_s| Tipo de contacto |
| AssignedTo_s | Asignado demasiado |
| Category_s | Categoría |
| Title_s|  Descripción breve |
| Description_s|  Notas |
| CreatedDate_t|  Abierto |
| ClosedDate_t| closed|
| ResolvedDate_t|Resuelto|
| Equipo  | Elemento de configuración |

## <a name="output-data-for-a-servicenow-change-request"></a>Datos de salida para una solicitud de cambio de ServiceNow

| Campo OMS | Campo ITSM |
|:--- |:--- |
| ServiceDeskId_s| Number |
| CreatedBy_s | Solicitado por |
| ClosedBy_s | Cerrado por |
| AssignedTo_s | Asignado demasiado |
| Title_s|  Descripción breve |
| Type_s|  Tipo |
| Category_s|  Categoría |
| CRState_s|  Estado|
| Urgency_s|  Urgencia |
| Priority_s| Prioridad|
| Risk_s| Riesgo|
| Impact_s| Impacto|
| RequestedDate_t  | Solicitado por fecha |
| ClosedDate_t | Fecha de cierre |
| PlannedStartDate_t  |     Fecha de inicio planeada |
| PlannedEndDate_t  |   Fecha de finalización planeada |
| WorkStartDate_t  | Fecha de inicio real |
| WorkEndDate_t | Fecha de finalización real|
| Description_s | Descripción |
| Equipo  | Elemento de configuración |

**Pantalla de Log Analytics de ejemplo para datos de ITSM:**

![Pantalla de Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>IT Service Management Connector: integración con otras soluciones de OMS

Conector de administración de servicio de TI, actualmente admite la integración con hello mapa de servicio de la solución.

Mapa de servicio detecta automáticamente Hola componentes de la aplicación en Windows y los mapas y sistemas Linux Hola comunicación entre los servicios. Permite tooview los servidores que pensar en ellos, como sistemas interconectados que ofrecen servicios críticos. Mapa de servicio muestra las conexiones entre servidores, procesos y puertos en cualquier arquitectura conectada TCP sin una configuración necesaria que sea distinta a la instalación de un agente. Más información: [Mapa de servicio](../operations-management-suite/operations-management-suite-service-map.md).

Con esta integración, puede ver los elementos de departamento de soporte de servicio Hola creados en soluciones ITSM de hello tal y como se muestra en el siguiente ejemplo de Hola:

![Solución integrada ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>Creación de elementos de trabajo de ITSM para alertas de OMS

Para las alertas OMS de hello, puede crear elementos de trabajo asociados en los orígenes de ITSM Hola conectado.  toodo, Hola de uso siguiente procedimiento:

1. De **Log Search** ventana, ejecute un datos tooview de consulta de búsqueda de registro. Resultados de la consulta son origen de Hola de elementos de trabajo.
2. En **Log Search**, haga clic en **alerta** tooopen hello **Agregar regla de alerta** página.

    ![Pantalla de Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. En hello **Agregar regla de alerta** ventana, proporcione los detalles de hello necesario de **nombre**, **gravedad**, **consulta de búsqueda**, y  **Criterios de alerta** (medida de ventana/métrica de tiempo).
4. Seleccione **Sí** en **Acciones de ITSM**.
5. Seleccione la conexión de ITSM de hello **Seleccionar conexión** lista.
6. Proporcione detalles de hello según sea necesario.
7. un elemento de trabajo independiente para cada entrada de registro de esta alerta, seleccione hello toocreate **crear elementos de trabajo individuales para cada entrada de registro** casilla de verificación.

    O

    Deje esta casilla de verificación toocreate no seleccionados solo un elemento de trabajo para cualquier número de entradas del registro en esta alerta.

7. Haga clic en **Guardar**.

alerta de OMS Hola se creará bajo **alertas**. Hola elementos se crean cuando se cumpla la condición de alerta especificado Hola de trabajo de la conexión ITSM correspondiente.

## <a name="create-itsm-work-items-from-oms-logs"></a>Creación de elementos de trabajo de ITSM desde registros de OMS

Puede crear elementos de trabajo en los orígenes de ITSM Hola conectado mediante búsqueda de registros de OMS. toodo, Hola de uso siguiente procedimiento:

1. De **Log Search**, buscar Hola requerido datos, seleccione detalles de Hola y haga clic en **crear elemento de trabajo**.

    Hola **elemento de trabajo de ITSM crear** aparecerá la ventana:

    ![Pantalla de Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Agregue Hola detalles siguientes:

  - **Título de elemento de trabajo**: título de elemento de trabajo de Hola.
  - **Descripción de elemento de trabajo**: descripción de elemento de trabajo nuevo Hola.
  - **Afectado equipo**: nombre del equipo de Hola donde se encontraron estos datos de registro.
  - **Seleccionar conexión**: conexión ITSM del que desee toocreate este elemento de trabajo.
  - **Elemento de trabajo**: tipo de elemento de trabajo.

3. toouse una plantilla de elemento de trabajo existente de un incidente, haga clic en **Sí** en **generar elemento de trabajo basado en la plantilla de hello** opción y, a continuación, haga clic en **crear**.

    O bien,

    Haga clic en **n** si desea tooprovide los valores personalizados.

4. Proporcione los valores adecuados de Hola Hola **tipo de contacto**, **impacto**, **urgencia**, **categoría**, y **subcategoría**  cuadros de texto y, a continuación, haga clic en **crear**.

se creará el elemento de trabajo de Hola Hola ITSM, que también se puede ver en OMS.

## <a name="troubleshoot-itsm-connections-in-oms"></a>Solución de problemas de conexión de ITSM en OMS
1.  Si se produce un error en la conexión de la interfaz de usuario del origen conectado y obtener hello **Error al guardar la conexión** de mensajes, Hola después de:
 - En el caso de las conexiones de ServiceNow, Cherwell y Provance, asegúrese de secreto de cliente y el Id. de nombre de usuario/contraseña y el cliente hello correctamente especificado para cada una de las conexiones de Hola. Si Hola error persiste, compruebe si dispone de suficientes privilegios en conexión de hello correspondiente ITSM producto toomake Hola.
 - En el caso de Service Manager, asegúrese de que se implementa correctamente hello Web app y conexión híbrida se crea. conexión de hello tooverify correctamente se establece con equipo de Service Manager local hello, visite URL de la aplicación hello Web tal como se detalla en la documentación de Hola para realizar hello [conexión híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  Si no obtener se sincronizan datos de ServiceNow en OMS, asegurarse de que esa instancia de ServiceNow hello no está en espera. En algún momento posible en hello ServiceNow Dev instancias, cuando esté inactivo. Else, problema de Hola de informe.
3.  Si obtener se activan alertas de OMS, pero no obtener se crean elementos de trabajo en el producto ITSM o elementos de configuración no están recibiendo elementos toowork creado/vinculada o para toda la información genérica, Hola siguientes:
 -  Solución de conector de administración de servicios de TI en el portal de OMS puede ser usado tooget un resumen de elementos de trabajo/conexiones/equipos etcetera. Haga clic en el mensaje de error de hello en la hoja de estado de hello, navegue demasiado**búsqueda de registros** y ver Hola conexión que tiene el error de hello mediante detalles de hello en el mensaje de error de saludo.
 - directamente puede ver información de errores/relacionado de Hola Hola **Log Search** página con *tipo = ServiceDeskLog_CL*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Solucionar problemas de implementación de aplicaciones web de Service Manager
1.  En el caso de los problemas con la implementación de aplicación web, asegúrese de que dispone de suficientes permisos de suscripción de hello mencionado toocreate/implementar recursos.
2.  Si **no establece la referencia de objeto tooinstance de un objeto** aparece el mensaje de error durante la ejecución hello [script](log-analytics-itsmc-service-manager-script.md) Asegúrese de que ha especificado valores válidos en **configuración de usuario**sección.
3.  Si se produce un error de espacio de nombres de retransmisión de bus de servicio de toocreate, asegúrese de que hello necesarios de proveedor de recursos está registrado en la suscripción de Hola. Si no está registrado, crear manualmente de hello portal de Azure. También puede crear mientras [crear conexión híbrida de hello](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) de hello portal de Azure.


## <a name="contact-us"></a>Ponerse en contacto con nosotros

Para cualquier consulta o comentarios en hello conector de administración de servicios de TI, póngase en contacto con nosotros en [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Pasos siguientes
[Agregar tooIT de productos y servicios ITSM Service Management Connector](log-analytics-itsmc-connections.md).
