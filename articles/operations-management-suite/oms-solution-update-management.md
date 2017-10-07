---
title: "solución de administración de OMS aaaUpdate | Documentos de Microsoft"
description: "Este artículo está previsto toohelp comprender cómo toouse esta toomanage solución actualizaciones para los equipos de Windows y Linux."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>Solución Administración de actualizaciones de OMS

![Símbolo de Administración de actualizaciones](./media/oms-solution-update-management/update-management-symbol.png)

Hola solución de administración de actualizaciones en OMS permite toomanage actualizaciones de seguridad del sistema operativo para los equipos de Windows y Linux implementados en Azure, local entornos u otros proveedores de nube.  Puede evaluar el estado de Hola de actualizaciones disponibles en todos los equipos de agente y administrar el proceso de instalar las actualizaciones necesarias para los servidores de hello rápidamente.


## <a name="solution-overview"></a>Información general de la solución
Equipos administrados por OMS utilizan siguiente de Hola para llevar a cabo las implementaciones de evaluación y actualización:

* Agente de OMS para Windows o Linux
* Extensión DSC (configuración de estado deseado) de PowerShell para Linux
* Hybrid Runbook Worker de Automation
* Microsoft Update o Windows Server Update Services para equipos Windows

Hola después de diagramas muestra una vista conceptual del flujo de datos y comportamiento de hello con la solución de hello evalúa y aplica tooall de actualizaciones de seguridad conectado Windows Server y los equipos Linux en un área de trabajo.    

#### <a name="windows-server"></a>Windows Server
![Flujo del proceso de administración de actualizaciones en Windows Server](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Flujo del proceso de administración de actualizaciones en Linux](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

Después de que el equipo de hello realiza un examen de cumplimiento de las actualizaciones, agente de OMS Hola envía información de hello en tooOMS de forma masiva. En un equipo de la ventana, examen de cumplimiento de Hola se realiza cada 12 horas de forma predeterminada.  Además se inicia la programación de exámenes toohello, examen de hello para el cumplimiento de las actualizaciones dentro de 15 minutos si Hola Microsoft Monitoring Agent (MMA) es instalación tooupdate reiniciado, antes y después de la instalación de actualización.  Con un equipo Linux, examen de cumplimiento de Hola se realiza cada tres horas de forma predeterminada y se inicia un examen de cumplimiento en 15 minutos si se reinicia el agente MMA Hola.  

Hello información de compatibilidad, a continuación, procesa y resumen en paneles de hello incluidos en soluciones de Hola o usar búsqueda definida por el usuario o pre-definida consultas.  Hello solución informa de cómo actualizada Hola equipo se basa en el origen está configurado toosynchronize con.  Si el equipo de Windows hello es tooWSUS tooreport configurado, dependiendo de cuándo WSUS sincronizó por última vez con Microsoft Update, los resultados de hello pueden diferir de lo que se muestra en Microsoft Updates.  Hello mismo para equipos Linux que están configurados tooreport tooa local repositorio frente a un repositorio público.   

Puede implementar e instalar las actualizaciones de software en equipos que requieren actualizaciones de hello mediante la creación de una implementación programada.  Las actualizaciones se clasifican como *opcional* no se incluyen en el ámbito de la implementación de Hola para equipos Windows, solo las actualizaciones necesarias.  Hello implementación programada define qué equipos de destino recibirá actualizaciones aplicables hello, ya sea explícitamente especificando equipos o seleccionar una [grupo de equipos](../log-analytics/log-analytics-computer-groups.md) que se basa en las búsquedas de registros de un conjunto determinado de equipos.  También especifica un tooapprove de programación y designar un período de tiempo cuando se permiten las actualizaciones toobe instalado en.  Los Runbooks instalan las actualizaciones en Azure Automation.  No puede ver estos runbooks, que no requieren ninguna configuración.  Cuando se crea una implementación de actualización, crea una programación que inicia un runbook de actualización maestro en hello especificado hora de los equipos de hello incluido.  Este runbook maestro inicia un runbook secundario en cada agente que realiza la instalación de las actualizaciones necesarias.       

En la fecha de Hola y la hora especificadas en la implementación de actualizaciones de hello, equipos de destino de hello ejecuta la implementación de hello en paralelo.  Un examen es primera tooverify realizada Hola actualizaciones siguen siendo necesarias y los instala.  Es importante toonote para equipos cliente WSUS, si no se aprueban las actualizaciones de hello en WSUS, parche Hola se producirá un error.  resultados de Hola de actualizaciones de hello aplicado se reenvían tooOMS toobe procesados y resumidos en paneles de Hola u Hola buscar eventos de Hola.     

## <a name="prerequisites"></a>Requisitos previos
* solución de Hello admite realizar evaluaciones de actualización en Windows Server 2008 y versiones posteriores y actualice las implementaciones en Windows Server 2008 R2 SP1 y versiones posteriores.  No se admiten las opciones de instalación de Server Core y Nano Server.

    > [!NOTE]
    > Compatibilidad para la implementación de actualizaciones tooWindows Server 2008 R2 SP1 requiere que .NET Framework 4.5 y WMF 5.0 o posterior.
    >  
* No se admiten los sistemas operativos cliente Windows.  
* Agentes de Windows deben ser toocommunicate configurado con un servidor de Windows Server Update Services (WSUS) o tener acceso tooMicrosoft Update.  

    > [!NOTE]
    > el agente de Windows Hello no puede administrar simultáneamente mediante System Center Configuration Manager.  
    >
* CentOS 6 (x86/x64) y 7 (x64)  
* Red Hat Enterprise (x86/x64) 6 y 7 (x64)  
* SUSE Linux Enterprise Server 11 (x86/x64) y 12 (x64)  
* Ubuntu 12.04 LTS y versiones más recientes (x86/x64)   
    > [!NOTE]  
    > las actualizaciones de tooavoid se aplica fuera de una ventana de mantenimiento en Ubuntu, vuelva a configurar actualizaciones automáticas de toodisable de paquete de actualización desatendida. Para obtener información acerca de cómo tooconfigure, vea [tema de las actualizaciones automáticas en hello Ubuntu Server guía](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).

* Agentes de Linux deben tener el repositorio de actualización de tooan de acceso.  

    > [!NOTE]
    > Un agente de OMS para Linux están configuradas áreas de trabajo OMS tooreport toomultiple no es compatible con esta solución.  
    >

Para obtener información adicional acerca de cómo tooinstall Hola agente de OMS para Linux y descargar la versión más reciente de hello, consulte demasiado[agente de Operations Management Suite para Linux](https://github.com/microsoft/oms-agent-for-linux).  Para obtener información sobre cómo tooinstall Hola agente de OMS para Windows, revise [Operations Management Suite agente para Windows](../log-analytics/log-analytics-windows-agents.md).  

### <a name="permissions"></a>Permisos
En orden toocreate implementaciones de actualizaciones, deberá toobe concede el rol de colaborador de hello en su cuenta de automatización y el área de trabajo de análisis de registros.  

## <a name="solution-components"></a>Componentes de soluciones
Esta solución consta de hello después de recursos que se agregan tooyour cuenta de automatización y agentes directamente conectados o el grupo de administración conectados de Operations Manager.

### <a name="management-packs"></a>Módulos de administración
Si el grupo de administración de System Center Operations Manager está conectado tooan área de trabajo OMS, Hola después de módulos de administración se instala en Operations Manager.  Estos módulos de administración también se instalan en equipos Windows directamente conectados después de agregar esta solución. No hay nada tooconfigure o administrará con estos módulos de administración.

* Intelligence Pack Update Assessment de Microsoft System Center Advisor (Microsoft.IntelligencePacks.UpdateAssessment)
* Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)
* Módulo de administración de Update Deployment

Para obtener más información sobre cómo se actualizan los módulos de administración de soluciones, consulte [tooLog de conexión de Operations Manager análisis](../log-analytics/log-analytics-om-agents.md).

### <a name="hybrid-worker-groups"></a>Grupos de Hybrid Worker
Después de habilitar esta solución, cualquier equipo con Windows conectadas directamente tooyour área de trabajo OMS se configura automáticamente como un runbooks de hello Hybrid Runbook Worker toosupport incluido en esta solución.  Para cada equipo con Windows administrado por solución hello, se enumerará en la hoja de grupos de trabajo de Runbook híbrido Hola de cuenta de automatización de hello sigue la convención de nomenclatura de hello *Hostname FQDN_GUID*.  Estos grupos no pueden ser grupos de destino de runbooks de su cuenta, porque se producirá un error. Estos grupos son solo previsto toosupport solución de administración de Hola.   

Obstante, puede agregar el grupo Hybrid Runbook Worker tooa equipos de Windows hello en su toosupport de cuenta de automatización los runbooks de automatización mientras está utilizando la misma cuenta para la solución de Hola y pertenencia al grupo de Hybrid Runbook Worker de Hola.  Esta funcionalidad se ha agregado tooversion 7.2.12024.0 de hello Hybrid Runbook Worker.  

## <a name="configuration"></a>Configuración
Realizar Hola siguiendo los pasos tooadd Hola administración de actualizaciones solución tooyour área de trabajo OMS y confirme están informando de agentes. El área de trabajo de Windows agentes tooyour ya estaba conectado se agregan automáticamente sin ninguna configuración adicional.

Puede implementar solución de hello mediante Hola siguientes métodos:

* De Azure Marketplace en hello portal de Azure mediante la selección de la oferta de automatización y Control de Hola o solución de administración de actualizaciones
* Desde la Galería de soluciones de OMS en el área de trabajo OMS Hola

Si ya tiene una cuenta de automatización y el área de trabajo OMS vinculado en hello mismo grupo de recursos y la región, seleccionar el Control y la automatización se comprobar la configuración y solo instalar soluciones de Hola y configúrelo en ambos servicios.  Selección de solución de administración de actualizaciones de Hola de Azure Marketplace ofrece Hola mismo comportamiento.  Si no tiene ambos servicios implementados en su suscripción, siga los pasos de Hola Hola **crear nueva solución** hoja y confirme que desea tooinstall Hola otros seleccionado previamente soluciones recomendadas.  Si lo desea, puede agregar tooyour de solución de administración de actualizaciones de hello siguiendo los pasos de Hola de área de trabajo OMS se describe en [soluciones de OMS agregar](../log-analytics/log-analytics-add-solutions.md) de hello Galería de soluciones.  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>Confirme que los agentes OMS y tooOMS de conectados del grupo de administración de Operations Manager

tooconfirm conectados directamente el agente de OMS para Linux y Windows se comuniquen con OMS, después de unos minutos, puede ejecutar Hola después de la búsqueda de registros:

* Linux: `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Windows: `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`

En un equipo Windows, puede revisar Hola después tooverify conectividad del agente con OMS:

1.  Abra Microsoft Monitoring Agent en el Panel de Control y, en hello **Azure Log Analytics (OMS)** ficha, hello agente muestra un mensaje que indica: **Hola Microsoft Monitoring Agent se ha conectado correctamente toohello Microsoft Servicio de Operations Management Suite**.   
2.  Abrir el registro de eventos de Windows hello, navegue demasiado**aplicación y el Administrador de servicios Logs\Operations** y busque 3000 de Id. de evento y 5002 de conector de servicio de origen.  Estos eventos indican equipo Hola se ha registrado con el área de trabajo OMS de Hola y está recibiendo la configuración.  

Si agente hello no es capaz de toocommunicate con hello servicio de OMS y toocommunicate configurado con hello internet a través de un servidor proxy o firewall, confirme Hola firewall o servidor proxy está configurado correctamente revisando [red configuración para el agente de Windows](../log-analytics/log-analytics-windows-agents.md#network) o [configuración de red para el agente Linux](../log-analytics/log-analytics-agent-linux.md#network).

> [!NOTE]
> Si los sistemas Linux toocommunicate configurado con un servidor proxy o puerta de enlace de OMS e incorporación esta solución, actualice hello *proxy.conf* grupo de permisos toogrant hello omiuser permiso de lectura en archivo Hola realizar Hola siguientes comandos:  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


Los agentes de Linux recién agregados mostrarán el estado **Actualizado** después de haber realizado una evaluación.  Este proceso puede tardar horas too6.

grupo de administración se comunica con OMS, consulte Operations Manager tooconfirm [validar la integración de Operations Manager con OMS](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms).

## <a name="data-collection"></a>Colección de datos
### <a name="supported-agents"></a>Agentes admitidos
Hello en la tabla siguiente describe los orígenes de hello conectado que son compatibles con esta solución.

| Origen conectado | Compatible | Description |
| --- | --- | --- |
| Agentes de Windows |Sí |solución de Hello recopila información acerca de las actualizaciones del sistema de Windows para agentes e inicia la instalación de las actualizaciones necesarias. |
| Agentes de Linux |Sí |solución de Hello recopila información acerca de las actualizaciones del sistema de agentes de Linux e inicia la instalación de las actualizaciones necesarias en distribuciones admitidas. |
| Grupo de administración de Operations Manager |Sí |solución de Hola recopila información acerca de las actualizaciones del sistema de agentes en un grupo de administración conectados.<br>Una conexión directa de tooLog de agente de Operations Manager Hola análisis no es necesario. Datos se reenvían desde el repositorio de OMS de toohello del grupo de administración de Hola. |
| Cuenta de almacenamiento de Azure |No |Azure Storage no incluye información acerca de las actualizaciones del sistema. |

### <a name="collection-frequency"></a>Frecuencia de recopilación
Para cada equipo Windows administrado, se realiza un examen dos veces al día. Hola de cada 15 minutos API de Windows se llama tooquery para hello última actualización tiempo toodetermine si estado ha cambiado y, caso en ese se inicia un examen de cumplimiento de normas.  Para cada equipo Linux administrado, se realiza un examen cada tres horas.

Puede tardar entre 30 minutos horas too6 para toodisplay actualizar datos del panel de Hola de equipos administrados.   

## <a name="using-hello-solution"></a>Uso de solución de Hola
Cuando se agrega el área de trabajo OMS de tooyour de solución de hello administración de actualizaciones, Hola **administración de actualizaciones** mosaico se agregarán tooyour panel de OMS. Este icono muestra un recuento y una representación gráfica del número de Hola de equipos en su entorno y su cumplimiento de las actualizaciones.<br><br>
![Icono Update Management Summary](media/oms-solution-update-management/update-management-summary-tile.png) (Resumen de administración de actualizaciones)  


## <a name="viewing-update-assessments"></a>Visualización de evaluaciones de la actualización
Haga clic en hello **administración de actualizaciones** icono tooopen hello **administración de actualizaciones** panel.<br><br> ![Panel Update Management Summary](./media/oms-solution-update-management/update-management-dashboard.png) (Resumen de administración de actualizaciones)<br>

Este panel proporciona un análisis detallado del estado de las actualizaciones clasificadas por tipo de sistema operativo y clasificación de la actualización: crítica, seguridad u otros (por ejemplo, una actualización de definiciones). resultados de Hello en cada icono en este panel reflejan sólo las actualizaciones aprobadas para implementación, que se basa en función de origen de sincronización de equipos de Hola.   Hola **las implementaciones de actualizaciones** icono cuando se selecciona, redirige la página de las implementaciones de actualizaciones de toohello donde puede ver las programaciones, las implementaciones que se está ejecutando actualmente, las implementaciones de completado, o programar una nueva implementación.  

Puede ejecutar una búsqueda de registros que devuelve todos los registros haciendo clic en icono concreto de Hola o toorun una consulta de una categoría determinada y criterios predefinidos, seleccione uno de hello lista disponible en hello **consultas comunes de actualización** columna.    

## <a name="installing-updates"></a>Instalación de actualizaciones
Una vez que las actualizaciones se han evaluado para todos Hola Linux y equipos de Windows en el área de trabajo, puede haber requiere actualizaciones instaladas mediante la creación de un *parche*.  Una implementación de actualizaciones es una instalación programada de las actualizaciones necesarias en uno o más equipos.  Que especifica la fecha de Hola y la hora para la implementación de hello además tooa equipo o un grupo de equipos que deben incluirse en el ámbito de Hola de una implementación.  toolearn más información acerca de los grupos de equipos, consulte [grupos de equipos de análisis de registros](../log-analytics/log-analytics-computer-groups.md).  Al incluir grupos de equipos en su implementación de actualización, memnbership de grupo se evalúa solo una vez en tiempo de Hola de programar la creación.  No se reflejarán los cambios subsiguientes tooa grupo.  toowork evitar este problema, eliminar la implementación de actualización de hello programado y vuelva a crearlo.

> [!NOTE]
> Máquinas virtuales de Windows que se implementan a partir de hello Azure Marketplace de forma predeterminada se establecen las actualizaciones automáticas de tooreceive de servicio de actualización de Windows.  Este comportamiento no cambia después de agregar esta solución o el área de trabajo de máquinas virtuales de Windows tooyour.  Si lo hace, las actualizaciones no activamente administradas con esta solución, Hola comportamiento predeterminado (aplicar automáticamente las actualizaciones) se aplicará.  

Para las máquinas virtuales creadas desde Hola petición Red Hat Enterprise Linux (RHEL) imágenes disponibles en Azure Marketplace, están registrados tooaccess hello [infraestructura de actualización de Red Hat (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) implementado en Azure.  Cualquier otra distribución de Linux debe actualizarse del repositorio de archivos en línea de distribuciones de hello siguiendo sus métodos admitidos.  

### <a name="viewing-update-deployments"></a>Visualización de implementaciones de actualizaciones
Haga clic en hello **parche** icono tooview Hola lista de implementaciones de actualizaciones existentes.  Se agrupan por estado: **Programado**, **En ejecución** y **Completado**.<br><br> ![Página de programación de las implementaciones de actualizaciones](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

propiedades de Hello mostradas para cada implementación de actualización se describen en hello en la tabla siguiente.

| Propiedad | Descripción |
| --- | --- |
| Nombre |Nombre del programa Hola parche. |
| Schedule |Tipo de programación.  Las opciones disponibles son *Una vez*, *Periodicidad semanal* o *Periodicidad mensual*. |
| Hora de inicio |Fecha y hora en que Hola parche es toostart programada. |
| Duration |Número de minutos Hola parche se permite toorun.  Si no están instaladas todas las actualizaciones dentro de esta duración, a continuación, Hola actualizaciones restantes debe esperar hasta que Hola parche siguiente. |
| Servidores |Número de equipos afectados por hello parche.  |
| Estado |Estado actual de hello parche.<br><br>Los valores posibles son:<br>- No iniciado<br>- En ejecución<br>- Finalizado |

Seleccione completado parche tooview Hola pantalla de detalles que incluye columnas de hello en hello en la tabla siguiente.  Estas columnas se todavía no se rellena si Hola parche no se han iniciado.<br><br> ![Información general de los resultados de la implementación de actualizaciones](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| Columna | Descripción |
| --- | --- |
| **Vista de equipos** | |
| Equipos Windows |Muestra el número de Hola de equipos de Windows en hello parche por estado.  Haga clic en un estado toorun una búsqueda de registros devuelve que todos los registros de actualizaciones con ese estado de implementación de actualización de Hola. |
| Equipos Linux |Muestra el número de Hola de equipos Linux en hello parche por estado.  Haga clic en un estado toorun una búsqueda de registros devuelve que todos los registros de actualizaciones con ese estado de implementación de actualización de Hola. |
| Estado de la instalación del equipo |Indica equipos Hola implicados en hello parche y el porcentaje de Hola de actualizaciones que han instalado correctamente. Haga clic en uno de hello entradas toorun una búsqueda de registros devuelve todas las actualizaciones que faltan y críticas. |
| **Vista de actualizaciones** | |
| Actualizaciones de Windows |Enumera las actualizaciones de Windows incluidas en hello implementación de actualización y su estado de instalación por cada actualización.  Seleccione un toorun de actualización de una búsqueda de registros devolver todas actualizan registros para la actualización específica o haga clic en hello estado toorun una búsqueda de registros devuelve que todos los registros para la implementación de Hola de actualizaciones. |
| Actualizaciones de Linux |Enumera las actualizaciones de Linux incluidas en la implementación de actualización de Hola y de su estado de instalación por cada actualización.  Seleccione un toorun de actualización de una búsqueda de registros devolver todas actualizan registros para la actualización específica o haga clic en hello estado toorun una búsqueda de registros devuelve que todos los registros para la implementación de Hola de actualizaciones. |

### <a name="creating-an-update-deployment"></a>Creación de una implementación de actualizaciones
Cree una nueva implementación de actualización, haga clic en hello **agregar** situado en la parte superior de Hola de Hola Hola de tooopen de pantalla **nueva implementación de actualización** página.  Debe proporcionar valores para las propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
| --- | --- |
| Nombre |Implementación de actualización de nombre único tooidentify Hola. |
| Zona horaria |Toouse de zona horaria para la hora de inicio de Hola. |
| Tipo de programación | Tipo de programación.  Las opciones disponibles son *Una vez*, *Periodicidad semanal* o *Periodicidad mensual*.  
| Hora de inicio |Fecha y hora toostart Hola parche. **Nota:** hello en primer lugar se puede ejecutar una implementación es de 30 minutos de la hora actual si necesita toodeploy inmediatamente. |
| Duration |Número de minutos Hola parche se permite toorun.  Si no están instaladas todas las actualizaciones dentro de esta duración, a continuación, Hola actualizaciones restantes debe esperar hasta que Hola parche siguiente. |
| Equipos |Nombres de equipos o tooinclude de grupos de equipo y de destino en hello parche.  Seleccione una o más entradas de lista desplegable Hola. |

<br><br> ![Página New Update Deployment (Nueva implementación de actualizaciones)](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>Intervalo de tiempo
De forma predeterminada, ámbito de Hola de datos de hello analizados en hello solución de administración de actualizaciones es de todos los grupos de administración conectados generados dentro de hello último día.

Seleccione el intervalo de tiempo de hello toochange de datos de hello, **datos en función de** en parte superior de hello del panel de Hola. Puede seleccionar registros de creado o actualizado en hello últimos 7 días, 1 día o 6 horas. O puede seleccionar **Personalizado** y especificar un intervalo de fechas personalizado.

## <a name="log-analytics-records"></a>Registros de Log Analytics
Hola solución de administración de actualizaciones crea dos tipos de registros en el repositorio OMS Hola.

### <a name="update-records"></a>Registros de actualización
Se crea un registro con el tipo **Actualizar** para cada actualización que está instalada o es necesaria en cada equipo. Actualizar los registros tienen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
| --- | --- |
| Tipo |*Actualizar* |
| SourceSystem |origen de Hola que aprobar la instalación de actualización de Hola.<br>Los valores posibles son:<br>- Microsoft Update<br>- Windows Update<br>- SCCM<br>- Servidores Linux (recuperado de los administradores de paquetes) |
| Aprobado |Especifica si se ha aprobado la actualización de hello para la instalación.<br> Para los servidores Linux, actualmente es opcional, ya que la aplicación de revisiones no está administrada por OMS. |
| Clasificación para Windows |Clasificación de actualización de Hola.<br>Los valores posibles son:<br>- Aplicaciones<br>- Actualizaciones críticas<br>- Actualizaciones de definiciones<br>- Feature Packs<br>- Actualizaciones de seguridad<br>- Service Packs<br>- Paquetes acumulativos de actualizaciones<br>- Actualizaciones |
| Clasificación para Linux |Cassification de actualización de Hola.<br>Los valores posibles son:<br>- Actualizaciones críticas<br>- Actualizaciones de seguridad<br>- Otras actualizaciones |
| Equipo |Nombre del equipo de Hola. |
| InstallTimeAvailable |Especifica si está disponible desde otra hora de instalación de hello agentes instalados Hola mismo actualizar. |
| InstallTimePredictionSeconds |Calcula el tiempo de instalación en segundos en función de otros agentes que instalaron Hola misma actualización. |
| KBID |Id. de artículo Hola KB que describe la actualización de Hola. |
| ManagementGroupName |Nombre del grupo de administración de Hola para agentes de SCOM.  En el caso de los otros agentes, es AOI-<workspace ID>. |
| MSRCBulletinID |Id. de boletín de seguridad de Microsoft de Hola que describe la actualización de Hola. |
| MSRCSeverity |Gravedad del boletín de seguridad de Microsoft de Hola.<br>Los valores posibles son:<br>- Crítico<br>- Importante<br>- Moderado |
| Opcional |Especifica si la actualización de hello es opcional. |
| Producto |Nombre de la actualización de Hola de producto de hello es.  Haga clic en **vista** tooopen artículo de hello en un explorador. |
| PackageSeverity |gravedad de Hola de vulnerabilidades de hello corregidos en esta actualización, notificado por los proveedores de distribución de Linux Hola. |
| PublishDate |Fecha y hora en que Hola actualización se instaló. |
| RebootBehavior |Especifica si la actualización de hello fuerza un reinicio.<br>Los valores posibles son:<br>- canrequestreboot<br>- neverreboots |
| RevisionNumber |Número de revisión de actualización de Hola. |
| SourceComputerId |GUID toouniquely identificar equipo Hola. |
| TimeGenerated |Fecha y hora en que Hola registro se actualizó por última vez. |
| Título |Título de actualización de Hola. |
| UpdateID |GUID toouniquely identificar actualización Hola. |
| UpdateState |Especifica si la actualización de hello está instalada en este equipo.<br>Los valores posibles son:<br>-Instalado - actualización de hello está instalada en este equipo.<br>-Necesita - actualización de hello no está instalado y es necesario en este equipo. |

Cuando se realiza cualquier búsqueda de registros que devuelve los registros con un tipo de **actualización** puede seleccionar hello **actualizaciones** vista que muestra un conjunto de iconos resumir las actualizaciones de hello devueltas por la búsqueda de Hola. Puede hacer clic en las entradas de Hola Hola **ausente y aplica las actualizaciones** y **actualizaciones obligatorias y opcionales** iconos de conjunto de toothat tooscope Hola vista de actualizaciones. Seleccione hello **lista** o **tabla** ver registros individuales de tooreturn Hola.<br>

![Vista de actualización de búsqueda de registros con actualización de tipo de registro](./media/oms-solution-update-management/update-la-view-updates.png)  

Hola **tabla** vista, puede hacer clic en hello **KBID** para cualquier registro tooopen un explorador con el artículo KB Hola. Esto permite tooquickly que conozca detalles de Hola de actualización concreto de Hola.<br>

![Vista de tabla de búsqueda de registros con iconos de actualizaciones de tipo de registro](./media/oms-solution-update-management/update-la-view-table.png)

Hola **lista** vista, haga clic en hello **vista** artículo de vínculo siguiente toohello KBID tooopen Hola KB.<br>

![Vista de lista de búsqueda de registros con iconos de actualizaciones de tipo de registro](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>Registros de UpdateSummary
Se crea un registro con un tipo de **UpdateSummary** para cada equipo del agente de Windows. Este registro se actualiza cada vez que se examina el equipo de Hola para las actualizaciones. **UpdateSummary** registros tienen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
| --- | --- |
| Tipo |UpdateSummary |
| SourceSystem |OpsManager |
| Equipo |Nombre del equipo de Hola. |
| CriticalUpdatesMissing |Número de actualizaciones críticas que faltan en el equipo de Hola. |
| ManagementGroupName |Nombre del grupo de administración de Hola para agentes de SCOM. En el caso de los otros agentes, es AOI-<workspace ID>. |
| NETRuntimeVersion |Versión de runtime de .NET de hello instalado en el equipo de Hola. |
| OldestMissingSecurityUpdateBucket |Depósito toocategorize la hora de Hola desde que se publicó más antigua actualización de seguridad Hola que faltan en este equipo.<br>Los valores posibles son:<br>- Anterior<br>- Hace 180 días<br>- Hace 150 días<br>- Hace 120 días<br>- Hace 90 días<br>- Hace 60 días<br>- Hace 30 días<br>- Reciente |
| OldestMissingSecurityUpdateInDays |Número de días desde que se publicó más antigua actualización de seguridad Hola que faltan en este equipo. |
| OsVersion |Versión del sistema operativo de hello instalado en el equipo de Hola. |
| OtherUpdatesMissing |Número de otras actualizaciones que faltan en el equipo de Hola. |
| SecurityUpdatesMissing |Número de actualizaciones de seguridad que faltan en el equipo de Hola. |
| SourceComputerId |GUID toouniquely identificar equipo Hola. |
| TimeGenerated |Fecha y hora en que Hola registro se actualizó por última vez. |
| TotalUpdatesMissing |Número total de actualizaciones que faltan en el equipo de Hola. |
| WindowsUpdateAgentVersion |Número de versión del agente de Windows Update de hello en el equipo de Hola. |
| WindowsUpdateSetting |Configuración para el equipo de hello instalará las actualizaciones importantes.<br>Los valores posibles son:<br>- Deshabilitado<br>- Notificar antes de la instalación<br>- Instalación programada |
| WSUSServer |Servidor de dirección URL de WSUS si Hola equipo está configurado toouse uno. |

## <a name="sample-log-searches"></a>Búsquedas de registros de ejemplo
Hello en la tabla siguiente proporciona búsquedas de registros de ejemplo para actualizar los registros recopilados por esta solución.

| Consultar | Descripción |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |Servidores basados en Windows que necesitan actualizaciones |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |Servidores Linux que necesitan actualizaciones | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Todos los equipos con actualizaciones pendientes |
| Type=Update UpdateState=Needed Optional=false Computer="COMPUTER01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |Actualizaciones pendientes para un equipo específico (reemplace el valor por el nombre del equipo)|
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") |Todos los equipos con actualizaciones de seguridad o críticas pendientes | 
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |Actualizaciones críticas o de seguridad necesarias para las máquinas a las que se aplican manualmente las actualizaciones |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Security Updates" OR Classification="Critical Updates") UpdateState=Needed Optional=false &#124; Distinct Computer} |Eventos de error para las máquinas que tienen pendientes actualizaciones de seguridad o críticas necesarias |
| Type=Update Optional=false Classification="Update Rollups" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Todos los equipos con paquetes acumulativos de actualizaciones pendientes | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |Actualizaciones distintivas pendientes en todos los equipos | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |Servidores basados en Windows con actualizaciones con error en la ejecución de la actualización | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |Servidores Linux con actualizaciones con error en la ejecución de la actualización | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |Pertenencia a un equipo WSUS | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |Configuración de actualizaciones automáticas | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |Equipos con la actualización automática deshabilitada | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" &#124; measure count() by Computer |Lista de todas las máquinas de Linux de Hola que hay un paquete de actualización disponible | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") &#124; measure count() by Computer |Lista de todas las máquinas de Linux de Hola que hay un paquete de actualización disponible que corrige una vulnerabilidad de seguridad o crítico | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" |Lista de todos los paquetes que tienen una actualización disponible | 
| Type=Update  and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") |Lista de todos los paquetes que tienen una actualización disponible que soluciona una vulnerabilidad de seguridad o crítica | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |Lista de las implementaciones de actualizaciones que han modificado equipos | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |Equipos que se actualizaron en esta ejecución de la actualización (reemplace el valor por el nombre de la implementación de actualizaciones) | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |Lista de todas las máquinas de "Ubuntu" hello con cualquier actualización disponible | 

## <a name="troubleshooting"></a>Solución de problemas

Esta sección proporciona información toohelp solucionar problemas con hello solución de administración de actualizaciones.  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>¿Cómo se pueden solucionar los problemas de incorporación?
Si se producen problemas al intentar tooonboard solución de Hola o una máquina virtual, compruebe hello **aplicación y el Administrador de servicios Logs\Operations** registro de eventos para eventos con el mensaje de Id. de 4502 y evento de eventos que contiene **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.  Hello en la tabla siguiente destaca los mensajes de error específicos y una posible solución para cada uno.  

| Message | Motivo | Solución |   
|----------|----------|----------|  
| No se puede tooRegister máquina para la administración de revisiones,<br>error en el registro con la excepción<br>System.InvalidOperationException: {"Message":"La máquina ya<br>registrar tooa otra cuenta. "} | Máquina ya está incorporado tooanother área de trabajo de administración de actualizaciones | Realizar una limpieza de artefactos antiguos por [Eliminando grupo de hello hybrid runbook](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| No se puede registrar demasiado máquina para la administración de revisiones,<br>error en el registro con la excepción<br>System.Net.Http.HttpRequestException: Se produjo un error al enviar la solicitud de saludo. ---><br>System.Net.WebException: conexión subyacente hello<br>se cerró: error inesperado<br>en una operación de recepción. ---> System.ComponentModel.Win32Exception:<br>no se pueden comunicar Hola cliente y servidor,<br>dado que no poseen un algoritmo común | El proxy, la puerta de enlace o el firewall están bloqueando la comunicación | [Revise los requisitos de red](../automation/automation-offering-get-started.md#network-planning)|  
| No se puede tooRegister máquina para la administración de revisiones,<br>error en el registro con la excepción<br>Newtonsoft.Json.JsonReaderException: error al analizar el valor de infinito positivo. | El proxy, la puerta de enlace o el firewall están bloqueando la comunicación | [Revise los requisitos de red](../automation/automation-offering-get-started.md#network-planning)| 
| certificado de Hello presentado por el servicio de hello <wsid>. ODS.opinsights.Azure.com<br>no fue emitido por una entidad de certificación<br>utilizada para los servicios de Microsoft. Póngase en contacto con<br>su toosee de administrador de red si se está ejecutando a un proxy que intercepta<br>la comunicación TLS/SSL. |El proxy, la puerta de enlace o el firewall están bloqueando la comunicación | [Revise los requisitos de red](../automation/automation-offering-get-started.md#network-planning)|  
| No se puede tooRegister máquina para la administración de revisiones,<br>error en el registro con la excepción<br>AgentService.HybridRegistration.<br>PowerShell.Certificates.CertificateCreationException:<br>No se pudo toocreate un certificado autofirmado. ---><br>System.UnauthorizedAccessException: se denegó el acceso. | Error al generar un certificado autofirmado | Compruebe que la cuenta del sistema tiene<br>toofolder de acceso de lectura:<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>¿Cómo puedo solucionar problemas con las implementaciones de actualizaciones?
Puede ver los resultados de Hola de hello runbook responsable de implementar actualizaciones de hello incluidas en el parche de hello programada de hoja de trabajos de Hola de su cuenta de automatización que se vincula con el área de trabajo OMS de hello admiten esta solución.  Hola runbook **MicrosoftOMSComputer revisión** es un runbook secundario que tiene como destino un equipo administrado específico y revisar el flujo detallado de hello presentará información detallada para que la implementación.  salida de Hello van a mostrar que requiere que las actualizaciones son aplicables, descargar estado, estado de la instalación y detalles adicionales.<br><br> ![Estado del trabajo de implementación de actualizaciones](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

Para más información, consulte [Mensajes y salidas del runbook de Automation](../automation/automation-runbook-output-and-messages.md).   

## <a name="next-steps"></a>Pasos siguientes
* Usar búsquedas de registros en [análisis de registros](../log-analytics/log-analytics-log-searches.md) tooview obtener datos actualizados.
* [Crear sus propios paneles](../log-analytics/log-analytics-dashboards.md) que muestren el cumplimiento de las actualizaciones de los equipos administrados.
* [Crear alertas](../log-analytics/log-analytics-alerts.md) cuando se detectan actualizaciones críticas pendientes en equipos, o bien cuando un equipo tiene las actualizaciones automáticas deshabilitadas.  
