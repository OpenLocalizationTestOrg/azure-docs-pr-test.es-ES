---
title: "aaaAzure Hybrid Runbook Worker de automatización | Documentos de Microsoft"
description: "Este artículo proporciona información sobre cómo instalar y usar Hybrid Runbook Worker que es una característica de automatización de Azure que permite toorun runbooks en máquinas en el centro de datos local o el proveedor de nube."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>Automatización de recursos en los centros de datos o nube con Hybrid Runbook Worker
Runbooks de automatización de Azure no puede tener acceso a recursos de otras nubes o en su entorno local puesto que ejecutan en hello nube de Azure.  característica de Hello Hybrid Runbook Worker de automatización de Azure permite toorun runbooks directamente en los equipos de Hola que alojan funciones de Hola y con los recursos en hello entorno toomanage esos recursos locales. Runbooks se almacenan y administran en automatización de Azure y, a continuación, entregarse tooone o más equipos designados.  

Esta funcionalidad se muestra en hello después de imagen:<br>  

![Información general de Trabajo híbrido de runbook](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Para una descripción general técnica de consideraciones de implementación y el rol de Hybrid Runbook Worker hello, consulte [información general sobre la arquitectura de automatización](automation-offering-get-started.md#automation-architecture-overview).    

## <a name="hybrid-runbook-worker-groups"></a>Grupos de Trabajos híbridos de runbook
Cada Hybrid Runbook Worker es miembro de un grupo de Hybrid Runbook Worker que especifique cuando se instala el agente de Hola.  Un grupo puede incluir solo un agente, pero puede instalar varios agentes en un grupo para contar con alta disponibilidad.

Cuando se inicia un runbook en un Runbook Worker híbrido, especificar grupo Hola donde se ejecuta.  los miembros de Hello del grupo de hello determinan qué trabajador atienda la solicitud de saludo.  No es posible especificar un trabajo determinado.

## <a name="relationship-tooservice-management-automation"></a>Relación tooService Management Automation
[Service Management Automation (SMA)](https://technet.microsoft.com/library/dn469260.aspx) permite toorun Hola mismo runbooks que son compatibles con automatización de Azure en su centro de datos local. SMA normalmente se implementa junto con Windows Azure Pack, dado que Windows Azure Pack contiene una interfaz gráfica para la administración de SMA. A diferencia de la automatización de Azure, SMA requiere una instalación local que incluye hello toohost de servidores web API, los runbooks de toocontain de base de datos y configuración de SMA y trabajos de Runbook Workers tooexecute runbook. Automatización de Azure proporciona estos servicios en la nube de Hola y solo requiere toomaintain Hola Hybrid Runbook Workers en su entorno local.

Si es un usuario existente de SMA, puede mover el toobe de automatización de runbooks tooAzure utilizado con Hybrid Runbook Worker sin realizar ningún cambio, suponiendo que se comporten de sus propios tooresources de autenticación, como se describe en [ejecutar runbooks en un Runbook híbrido Trabajo](automation-hrw-run-runbooks.md).  Runbooks de SMA ejecutar en el contexto de Hola de cuenta de servicio de hello en el servidor de trabajador de hello logrando que la autenticación de hello runbooks.

Puede usar Hola siguiendo criterios toodetermine si es más adecuada para sus requerimientos de automatización de Azure con Hybrid Runbook Worker o Service Management Automation.

* SMA requiere una instalación local de sus componentes subyacentes que están conectados tooWindows Azure Pack, si se requiere una interfaz gráfica de administración. Se requieren más recursos locales con costos de mantenimiento más elevados que Azure Automation, que solo necesita un agente instalado en Runbook Workers locales. agentes de Hello administrados por Operations Management Suite, reduce aún más los costes de mantenimiento.
* Automatización de Azure almacena sus runbooks en la nube de Hola y los entrega a local tooon Hybrid Runbook Workers. Si su directiva de seguridad no permite este comportamiento, deberá usar SMA.
* SMA se incluye con System Center; y por tanto, requiere una licencia de System Center 2012 R2. Azure Automation se basa en un modelo de suscripción en niveles.
* Presenta características avanzadas, como Runbooks gráficos que no están disponibles en SMA.

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>Instalar Hola Windows Hybrid Runbook Worker 

tooinstall y configurar un Hybrid Runbook Worker de Windows, hay dos métodos disponibles.  Hola recomienda método consiste en utilizar una automatización de runbook toocompletely automatizar el proceso Hola necesario tooconfigure un equipo de Windows.  segundo método de Hello es posterior a una instalación de toomanually procedimiento paso a paso y configurar el rol de Hola.  

> [!NOTE]
> configuración de hello toomanage de los servidores que admiten roles Hybrid Runbook Worker de Hola a la configuración de estado deseado (DSC), necesita tooadd usarlas como nodos de DSC.  Para obtener más información sobre su incorporación para la administración con DSC, consulte [Incorporación de máquinas para administrarlas con DSC de Azure Automation](automation-dsc-onboarding.md).           
><br>
>Si habilita hello [solución de administración de actualizaciones](../operations-management-suite/oms-solution-update-management.md), cualquier equipo con Windows conectado tooyour área de trabajo OMS se configura automáticamente como un Hybrid Runbook Worker los runbooks toosupport incluido en esta solución.  Sin embargo, no está registrado en ningún grupo de Hybrid Worker ya definido en la cuenta de Automation.  Hola equipo puede agregarse tooa grupo de Hybrid Runbook Worker en su toosupport de cuenta de automatización los runbooks de automatización mientras está utilizando la misma cuenta para la solución de Hola y pertenencia al grupo de Hybrid Runbook Worker de Hola.  Esta funcionalidad se ha agregado tooversion 7.2.12024.0 de hello Hybrid Runbook Worker.  

Hola de revisión después de obtener información sobre hello [requisitos de hardware y software](automation-offering-get-started.md#hybrid-runbook-worker) y [información para preparar su red](automation-offering-get-started.md#network-planning) antes de empezar a implementar un Runbook Worker híbrido.  Después de haber implementado correctamente un runbook worker, revise [ejecutar runbooks en un Runbook Worker híbrido](automation-hrw-run-runbooks.md) toolearn cómo tooconfigure su tooautomate runbooks procesa en su centro de datos local o en otro entorno de nube.  
 
### <a name="automated-deployment"></a>Implementación automatizada

Realizar Hola siguientes pasos de instalación de hello tooautomate y la configuración del rol de Windows Hybrid Worker Hola.  

1. Descargar hello *New-OnPremiseHybridWorker.ps1* script de Hola [Galería de PowerShell](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript) directamente desde el equipo Hola ejecuta Hola Hybrid Runbook Worker rol o desde otro equipo en el entorno y cópielo toohello trabajo.  

    Hola *OnPremiseHybridWorker.ps1 New* script requiere Hola parámetros siguientes durante la ejecución:

  * *AutomationAccountName* (obligatorio): nombre de hello de la cuenta de automatización.  
  * *ResourceGroupName* (obligatorio): nombre de Hola Hola del grupo de recursos asociado a su cuenta de automatización.  
  * *HybridGroupName* (obligatorio): nombre de Hola de un grupo de Hybrid Runbook Worker que especifique como destino para admitir este escenario de runbooks de Hola. 
  *  *Id. de suscripción* (obligatorio): Hola Id. de suscripción de Azure que su cuenta de automatización es miembro.
  *  *WorkspaceName* (opcional): Hola OMS nombre de área de trabajo.  Si no tiene un área de trabajo OMS, el script de Hola crea y configura uno.  

     > [!NOTE]
     > Actualmente están regiones Hola de automatización sola admitidas para la integración con OMS - **sudeste de Australia**, **UU 2**, **sudeste de Asia**, y **oeste Europa**.  Si su cuenta de automatización no está en una de esas regiones, script de Hola crea un área de trabajo OMS, pero le advierte que no se pueden vincular todos estos elementos.
     > 
2. En el equipo, inicie **Windows PowerShell** de hello **iniciar** pantalla en modo de administrador.  
3. Desde el shell de línea de comandos de PowerShell de hello, desplazarse por las carpetas de toohello, que contiene el script de Hola descargó y ejecutarla cambiar valores de hello para parámetros *- AutomationAccountName*, *- ResourceGroupName* , *- HybridGroupName*, *- SubscriptionId*, y *- WorkspaceName*.

     > [!NOTE] 
     > Son tooauthenticate solicitada con Azure después de ejecutar script de Hola.  Se **debe** iniciar sesión con una cuenta que sea miembro del rol de los administradores de suscripciones de Hola y Coadministrador de suscripción de Hola.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. Son solicitadas tooagree tooinstall **NuGet** y son tooauthenticate solicitada con sus credenciales de Azure.<br><br> ![Ejecución del script New-OnPremiseHybridWorker](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. Una vez completada la secuencia de comandos de hello, hoja de grupos de trabajo híbrido de hello mostrará nuevo grupo de Hola y el número de miembros o si un grupo existente, se incrementa el número de Hola de miembros.  Puede seleccionar grupo de hello en lista de Hola Hola **grupos de trabajo híbrido** hoja y seleccione hello **Hybrid Workers** icono.  En hello **Hybrid Workers** hoja, verá que cada miembro del grupo de hello mencionados.  

### <a name="manual-deployment"></a>Implementación manual 
Realizar los dos primeros pasos de hello una vez para su entorno de automatización y, a continuación, repita Hola restantes pasos para cada equipo de trabajo.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Creación del área de trabajo de Operations Management Suite
Si todavía no tiene un área de trabajo de Operations Management Suite, puede crear uno siguiendo las instrucciones que aparecen en [Administración del área de trabajo](../log-analytics/log-analytics-manage-access.md). Si cuenta con un área de trabajo existente, puede usarla.

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2. Agregar automatización de la solución tooOperations área de trabajo de Management Suite
Las soluciones agregan funcionalidad tooOperations Management Suite.  solución de automatización de Hello agrega funcionalidad para automatización de Azure, incluida la compatibilidad con Hybrid Runbook Worker.  Cuando se agrega el área de trabajo de hello solución tooyour, empuja automáticamente equipo de agente de toohello de componentes de trabajo que va a instalar en el paso siguiente de saludo.

Siga las instrucciones de hello en [tooadd una solución mediante la Galería de soluciones de hello](../log-analytics/log-analytics-add-solutions.md) tooadd hello **automatización** área de trabajo de solución tooyour Operations Management Suite.

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3. Instalar Microsoft Monitoring Agent Hola
Hola Microsoft Monitoring Agent conecta equipos tooOperations Management Suite.  Al instalar el agente de hello en el equipo local y conectarse tooyour área de trabajo, descargará automáticamente los componentes de hello necesarios para Hybrid Runbook Worker.

Siga las instrucciones de hello en [tooLog de equipos de Windows conectarse análisis](../log-analytics/log-analytics-windows-agents.md) tooinstall agente de hello en el equipo local de Hola.  Puede repetir este proceso para varios tooadd de equipos de entornos de varios trabajadores tooyour.

Cuando el agente de Hola se ha conectado correctamente tooOperations Management Suite, se enumerarán en hello **orígenes conectados** ficha de hello Operations Management Suite **configuración** panel.  Puede comprobar que el agente Hola ha descargado correctamente solución de automatización de hello cuando tiene una carpeta denominada **AzureAutomationFiles** en Files\Microsoft Agent\Agent supervisión de C:\Program Files\Microsoft.  versión de hello tooconfirm de hello Hybrid Runbook Worker, puede navegar tooC:\Program Files\Microsoft Agent\Agent\AzureAutomation\ supervisión y observe hello \\ *versión* subcarpeta.   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4. Instalar el entorno de runbook de Hola y conectar tooAzure automatización
Cuando se agrega un tooOperations agente Management Suite, solución de automatización de hello empuja hello **HybridRegistration** módulo de PowerShell, que contiene Hola **Add-HybridRunbookWorker** cmdlet.  Usar este entorno de runbook de cmdlet tooinstall hello en el equipo de Hola y registrarlo con automatización de Azure.

Abra una sesión de PowerShell en modo de administrador y ejecute hello después de módulo de hello tooimport de comandos.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

A continuación, ejecute hello **Add-HybridRunbookWorker** cmdlet con hello según la sintaxis:

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

Para obtener información de hello necesaria para este cmdlet impide hello **administrar claves** hoja Hola portal de Azure.  Para abrir esta hoja, seleccione hello **claves** opción de hello **configuración** hoja en su cuenta de automatización.

![Información general de Trabajo híbrido de runbook](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** es nombre Hola de hello grupo Hybrid Runbook Worker. Si este grupo ya existe en la cuenta de automatización de Hola, equipo de hello actual se agrega tooit.  Si todavía no existe, se agregará.
* **Punto de conexión** es hello **URL** campo hello **administrar claves** hoja.
* **Símbolo (token)** es hello **clave de acceso principal** en hello **administrar claves** hoja.  

Hola de uso **-Verbose** cambiar con **Add-HybridRunbookWorker** tooreceive obtener información acerca de la instalación de Hola.

#### <a name="5-install-powershell-modules"></a>5. Instalación de módulos PowerShell
Runbooks puede usar cualquiera de las actividades de Hola y cmdlets definidos en módulos de hello instalados en su entorno de automatización de Azure.  Estos módulos no son equipos locales tooon implementadas automáticamente, por lo que debe instalar manualmente.  excepción de Hello es hello módulo de Azure, que se instala de forma predeterminada, proporciona acceso toocmdlets para todas las actividades y los servicios de Azure para la automatización de Azure.

Puesto que el objetivo principal de Hola de característica de Hybrid Runbook Worker de hello es toomanage los recursos locales, lo más probable es que necesario módulos de hello tooinstall que estos recursos de soporte técnico.  Puede hacer referencia demasiado[instalar módulos](http://msdn.microsoft.com/library/dd878350.aspx) para obtener información acerca de cómo instalar los módulos de Windows PowerShell.  Módulos que están instalados deben estar en una ubicación de referencia variable de entorno PSModulePath para que se importan automáticamente por Hybrid worker de Hola.  Para obtener más información, consulte [modificar Hola ruta de instalación de PSModulePath](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx). 

## <a name="removing-hybrid-runbook-worker"></a>Eliminación de Hybrid Runbook Worker 
Puede quitar uno o más Hybrid Runbook Workers de un grupo o puede quitar el grupo de hello, dependiendo de los requisitos.  tooremove un Hybrid Runbook Worker desde un equipo local, realice Hola pasos.

1. Hola portal de Azure, navegue tooyour cuenta de automatización.  
2. De hello **configuración** hoja, seleccione **claves** y tenga en cuenta los valores de hello para el campo **URL** y **clave de acceso principal**.  Necesitará esta información para el paso siguiente de saludo.
3. Abra una sesión de PowerShell en modo de administrador y ejecute hello siguiente command - `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`.  Hola de uso **-Verbose** cambie para un registro detallado del proceso de eliminación de Hola.

> [!NOTE]
> No se quitará Hola Microsoft Monitoring Agent desde equipo hello, solo la funcionalidad de Hola y la configuración del rol de hello Hybrid Runbook Worker.  

## <a name="remove-hybrid-worker-groups"></a>Eliminación de grupos de Hybrid Worker
tooremove un grupo, primero debe tooremove Hola Hybrid Runbook Worker de cada equipo que sea miembro del grupo de hello mediante el procedimiento de hello mostrado anteriormente y, a continuación, realizar Hola siguiente grupo de pasos tooremove Hola.  

1. Abrir cuenta de automatización de Hola Hola portal de Azure.
2. Seleccione hello **grupos de trabajo híbrido** icono y Hola **grupos de trabajo híbrido** hoja, grupo de hello seleccione desea toodelete.  Después de seleccionar el grupo específico de hello, Hola **grupo Hybrid worker** se muestra la hoja de propiedades.<br> ![Hoja Grupo de Hybrid Runbook Worker](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. En la hoja de propiedades de hello para el grupo seleccionado de hello, haga clic en **eliminar**.  Aparece un mensaje preguntándole tooconfirm esta acción, seleccione **Sí** si está seguro de que desea tooproceed.<br> ![Cuadro de diálogo de confirmación de eliminación de grupo](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> Este proceso puede tardar unos segundos toocomplete y se puede realizar un seguimiento de su progreso en **notificaciones** en el menú de Hola.  

## <a name="troubleshooting"></a>Solución de problemas 
Hola Hybrid Runbook Worker depende hello toocommunicate Microsoft Monitoring Agent con su trabajo de automatización de la cuenta tooregister hello, trabajos de runbook e informar del estado de recepción. Si se produce un error en el registro de trabajo de hello, aquí tiene algunas posibles causas de error de hello:  

1. hybrid worker de Hello está detrás de un servidor proxy o firewall.  
    Compruebe el equipo de hello tiene acceso de salida too*.azure-automation.net en el puerto 443.  

2. Hello hybrid worker de Hola de equipo se está quedando tiene menos de hardware mínima Hola [requisitos](automation-offering-get-started.md#hybrid-runbook-worker).  
    Hola a equipos que ejecutan Hola Hybrid Runbook Worker deben cumplir los requisitos mínimos de hardware antes de designar toohost esta característica. En caso contrario, según la utilización de recursos de Hola de otros procesos en segundo plano y la contención porque runbooks durante la ejecución, equipo de Hola se convierten en utilizarán más y provocar retrasos de trabajo de runbook o tiempos de espera.
   Confirme equipo Hola designado de la característica de Hybrid Runbook Worker de hello toorun cumple los requisitos mínimos de hardware de Hola.  Si es así, supervisar toodetermine de uso de CPU y memoria de las posibles correlaciones entre el rendimiento de Hola de procesos de Hybrid Runbook Worker y Windows.  Si no hay presión de CPU o memoria, esto puede indicar Hola necesidad tooupgrade o agregue procesadores adicionales, o aumento de memoria tooaddress Hola cuello de botella de recursos y resolver errores de Hola. Como alternativa, seleccione un recurso de proceso diferente que puede admitir los requisitos mínimos de Hola y escalar cuando las demandas de carga de trabajo indican que un aumento es necesario.
    
3. Hola servicio del agente de supervisión de Microsoft no se está ejecutando.  
    Si no se está ejecutando Hola servicio de Windows del agente de supervisión de Microsoft, esto evita que Hola Hybrid Runbook Worker se comuniquen con automatización de Azure.  Compruebe está ejecutando el agente de hello escribiendo el siguiente comando de PowerShell de hello: `get-service healthservice`.  Si se detiene el servicio de hello, escriba Hola siguiente comando en el servicio de PowerShell toostart Hola: `start-service healthservice`.  

4. Hola **aplicación y el Administrador de servicios Logs\Operations** registro de eventos, vea evento 4502 y que contiene EventMessage **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**con hello después Descripción: *certificado Hola presentado por el servicio de hello <wsid>. ODS.opinsights.Azure.com no fue emitido por una entidad de certificación utilizada para los servicios de Microsoft. Póngase en contacto con su toosee de administrador de red si se está ejecutando a un proxy que intercepta la comunicación TLS/SSL. artículo de Hello kb3126513 incluye tiene información adicional para solucionar problemas de conectividad.*
    Esto puede deberse a la red o proxy firewall blockking comunicación tooMicrosoft Azure.  Compruebe el equipo de hello tiene acceso de salida too*.azure-automation.net en los puertos 443.

Los registros se almacenan localmente en cada Hybrid Worker en C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Puede comprobar si hay cualquier advertencia o error se escriban toohello **aplicaciones y servicios Logs\Microsoft-SMA\Operations** y **aplicación y el Administrador de servicios Logs\Operations** que el registro de eventos indica una conectividad u otro problema que afecte a la incorporación de hello rol tooAzure automatización o un problema al realizar las operaciones normales.  

## <a name="next-steps"></a>Pasos siguientes
Revisión [ejecutar runbooks en un Runbook Worker híbrido](automation-hrw-run-runbooks.md) toolearn cómo tooconfigure su tooautomate runbooks procesa en su centro de datos local o en otro entorno de nube.
