---
title: "aaaCollecting datos de análisis de registros con un runbook en automatización de Azure | Documentos de Microsoft"
description: "Tutorial paso a paso le guía por la creación de un runbook en datos de toocollect de automatización de Azure en el repositorio de OMS de hello para el análisis por análisis de registros."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>Recopilación de datos de Log Analytics con un runbook de Azure Automation
Puede recopilar una cantidad significativa de datos en Log Analytics desde diversos orígenes como son los [orígenes de datos](../log-analytics/log-analytics-data-sources.md) de agentes y también los [datos recopilados de Azure](../log-analytics/log-analytics-azure-storage.md).  Hay un escenarios aunque donde debe toocollect datos que no es accesible a través de estos orígenes estándares.  En estos casos, puede usar hello [API de recopilador de datos HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite datos tooLog análisis desde cualquier cliente de la API de REST.  Un tooperform método común esta recopilación de datos está usando un runbook en automatización de Azure.   

Este tutorial le guía a través del proceso de Hola para crear y programar un runbook en automatización de Azure toowrite datos tooLog análisis.


## <a name="prerequisites"></a>Requisitos previos
Este escenario requiere Hola siguiendo los recursos configurados en su suscripción de Azure.  Ambos pueden ser una cuenta gratuita.

- [Área de trabajo de Log Analytics](../log-analytics/log-analytics-get-started.md).
- [Cuenta de Azure Automation](../automation/automation-offering-get-started.md).

## <a name="overview-of-scenario"></a>Información general del escenario
En este tutorial, escribirá un runbook que recopila información acerca de los trabajos de Automation.  Runbooks de automatización de Azure se implementan con PowerShell, por lo que podrá empezar por escribir y probar una secuencia de comandos en el editor de automatización de Azure Hola.  Cuando haya comprobado que está recopilando información de hello necesario, podrá escribir ese tooLog análisis de datos y comprobar el tipo de datos personalizados de Hola.  Por último, creará un runbook de programación toostart Hola a intervalos regulares.

> [!NOTE]
> Puede configurar la automatización de Azure toosend trabajo información tooLog análisis sin este runbook.  Este escenario es principalmente el tutorial de hello toosupport usado y se recomienda que enviar el área de trabajo de hello datos tooa prueba.  


## <a name="1-install-data-collector-api-module"></a>1. Instalación del módulo Data Collector API
Cada [solicitud de API de recopilador de datos HTTP hello](../log-analytics/log-analytics-data-collector-api.md#create-a-request) debe tener el formato adecuado e incluir un encabezado de autorización.  Para hacer esto en su runbook, pero se puede reducir la cantidad de Hola de código necesario, con un módulo que simplifica este proceso.  Es un módulo que puede usar [OMSIngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI) Hola Galería de PowerShell.

toouse una [módulo](../automation/automation-integration-modules.md) en un runbook, debe instalarse en su cuenta de automatización.  Funciones de módulo de Hola Hola a cualquier runbook Hola, a continuación, puede usar la misma cuenta.  Puede instalar un nuevo módulo seleccionando **Activos** > **Módulos** > **Agregar un módulo** en su cuenta de Automation.  

Hola Galería de PowerShell aunque le ofrece una toodeploy opciones rápidas un módulo directamente tooyour automatización de la cuenta para poder utilizar esta opción para este tutorial.  

![Módulo OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. Vaya demasiado[Galería de PowerShell](https://www.powershellgallery.com/).
2. Busque **OMSIngestionAPI**.
3. Haga clic en hello **implementar tooAzure automatización** botón.
4. Seleccione su cuenta de automatización y haga clic en **Aceptar** módulo de hello tooinstall.


## <a name="2-create-automation-variables"></a>2. Creación de las variables de Automation
[Las variables de Automation](..\automation\automation-variables.md) contienen valores que pueden usarse en todos los runbooks en su cuenta de Automation.  Realizan runbooks más flexible, ya que permite toochange estos valores sin necesidad de editar Hola runbook real. Requiere que todas las solicitudes de API de recopilador de datos HTTP Hola Hola identificador y la clave de área de trabajo OMS de Hola y activos de variable hay toostore ideal esta información.  

![variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. Hola portal de Azure, navegue tooyour cuenta de automatización.
2. Seleccione **Variables** en **Recursos compartidos**.
2. Haga clic en **agregar una variable** y cree dos variables de hello en hello en la tabla siguiente.

| Propiedad | Valor de identificador de área de trabajo | Valor de clave de área de trabajo |
|:--|:--|:--|
| Nombre | WorkspaceId | WorkspaceKey |
| Tipo | String | String |
| Valor | Pegue en hello Id. de área de trabajo del área de trabajo de análisis de registros. | Pegue con hello principal o secundaria de su área de trabajo de análisis de registros. |
| Cifrados | No | Sí |



## <a name="3-create-runbook"></a>3. Creación de runbook

Automatización de Azure tiene un editor en el portal de Hola donde puede editar y probar su runbook.  Tiene toowork del editor de script de Hola opción toouse Hola con [PowerShell directamente](../automation/automation-edit-textual-runbook.md) o [crear un runbook gráfico](../automation/automation-graphical-authoring-intro.md).  En este tutorial, trabajará con un script de PowerShell. 

![Edición de un runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. Navegue tooyour cuenta de automatización.  
2. Haga clic en **Runbooks** > **Agregar un runbook** > **Crear un nuevo runbook**.
3. Nombre de runbook de hello, escriba **trabajos de automatización de recopilar**.  Para tipo de runbook de hello, seleccione **PowerShell**.
4. Haga clic en **crear** toocreate Hola runbook e inicio Hola del editor.
5. Copie y pegue Hola siguiente código en hello runbook.  Consulte toohello comentarios en el script de Hola para ver una explicación del código de hello.
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4. Prueba del runbook
Automatización de Azure incluye un entorno demasiado[probar su runbook](../automation/automation-testing-runbook.md) antes de publicarla.  Puede inspeccionar los datos de Hola Hola runbook recogidos y compruebe que escribe tooLog análisis según lo esperado antes de publicarlo tooproduction. 
 
![Prueba del runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. Haga clic en **guardar** toosave Hola runbook.
1. Haga clic en **panel prueba** tooopen Hola runbook en el entorno de prueba de Hola.
3. Puesto que el runbook tiene parámetros, le tooenter solicitadas valores para ellos.  Escriba Hola nombre del grupo de recursos de Hola y automatización de hello información de la cuenta que su curso toocollect trabajo de.
4. Haga clic en **iniciar** toohello iniciar runbook Hola.
3. Hola runbook se iniciará con un estado de **en cola** antes de que entre demasiado**ejecutando**.  
3. Hola runbook debe mostrar un resultado detallado con trabajos de hello recopilados en formato json.  Si no aparece ningún trabajo, a continuación, no se haya ningún trabajo creado en la cuenta de automatización de Hola Hola última hora.  Pruebe a iniciar cualquier runbook en la cuenta de automatización de hello y, a continuación, realice pruebas de Hola de nuevo.
4. Asegúrese de que la salida de hello no muestra que los errores en hello exponer comandos tooLog análisis.  Debe tener una continuación toohello similar de mensaje.

    ![Registro de salida](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5. Comprobación de los registros de Log Analytics
Una vez que se ha completado Hola runbook de prueba y haya comprobado que la salida de hello ha sido recibida correctamente, puede comprobar que los registros de Hola se crearon con una [búsqueda de registros de análisis de registros](../log-analytics/log-analytics-log-searches.md).

![Resultados del registro](media/operations-management-suite-runbook-datacollect/log-output.png)

1. Hola portal de Azure, seleccione el área de trabajo de análisis de registros.
2. Haga clic en **Búsqueda de registros**.
3. Hola de tipo siguiente comando `Type=AutomationJob_CL` y haga clic en el botón de búsqueda de Hola. Tenga en cuenta que el tipo de registro de hello incluye _CL que no se especifica en el script de Hola.  Ese sufijo es tooindicate de tipo de registro automáticamente anexados toohello que es un tipo de registro personalizado.
4. Debería ver uno o varios de los registros devueltos que indica que runbook Hola funciona según lo previsto.


## <a name="6-publish-hello-runbook"></a>6. Publicar Hola runbook
Una vez que haya comprobado que runbook Hola funciona correctamente, necesita toopublish, por lo que puede ejecutar en producción.  Puede continuar tooedit y probar Hola runbook sin modificar la versión publicada de Hola.  

![Publicación del runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. Devolver tooyour cuenta de automatización.
2. Haga clic en **Runbooks** y seleccione **Collect-Automation-jobs**.
3. Haga clic en **Editar** y, a continuación, en **Publicar**.
4. Haga clic en **Sí** cuando tooverify frecuentes que desea toooverwrite Hola previamente versión publicada.

## <a name="7-set-logging-options"></a>7. Establecimiento de las opciones de registro 
De prueba, era capaz de tooview [resultados detallados](../automation/automation-runbook-output-and-messages.md#message-streams) porque se establece Hola $VerbosePreference variable en el script de Hola.  Para entornos de producción, debe propiedades de registro de hello tooset de runbook de hello si desea que los resultados detallados de tooview.  Hola runbook usado en este tutorial, se mostrará datos de json de Hola que se envían tooLog análisis.

![Registro y seguimiento](media/operations-management-suite-runbook-datacollect/logging.png)

1. En Propiedades de hello para el runbook seleccione **registro y seguimiento** en **configuración del Runbook**.
2. Cambiar configuración de Hola para **registros detallados** demasiado**en**.
3. Haga clic en **Guardar**.

## <a name="8-schedule-runbook"></a>8. Programación de un runbook
Hola toostart de manera más común un runbook que recopila datos de supervisión es tooschedule se toorun automáticamente.  Para ello, crear un [programación en automatización de Azure](../automation/automation-schedules.md) y adjuntar tooyour runbook.

![Programación de un runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. En Propiedades de hello para el runbook, seleccione **programaciones** en **recursos**.
2. Haga clic en **agregar una programación** > **vincular un runbook de programación tooyour** > **crear una nueva programación**.
5. Tipo de hello siguientes valores para la programación de Hola y haga clic en **crear**.

| Propiedad | Valor |
|:--|:--|
| Nombre | AutomationJobs-Hourly |
| Se inicia | Seleccione cualquier momento al menos 5 minutos anterior Hola hora actual. |
| Periodicidad | Periódica |
| Repetir cada | 1 hora |
| Configurar expiración | No |

Una vez que se creó la programación de hello, necesita valores de parámetro de hello tooset que se usará cada vez que esta programación inicia runbook Hola.

6. Haga clic en **Configurar parámetros y ejecutar configuraciones**.
7. Rellene los valores de **ResourceGroupName** y **AutomationAccountName**.
8. Haga clic en **Aceptar**. 

## <a name="9-verify-runbook-starts-on-schedule"></a>9. Comprobación de que el runbook se inicia según la programación
Siempre que se inicia un runbook, [se crea un trabajo](../automation/automation-runbook-execution.md) y se registran sus resultados.  De hecho, se trata de hello está recopilando los mismos trabajos que Hola runbook.  Puede comprobar que dicho runbook Hola se inicia como se esperaba mediante la comprobación de trabajos de Hola Hola runbook después de que transcurra el tiempo de inicio de Hola para programación Hola.

![Trabajos](media/operations-management-suite-runbook-datacollect/jobs.png)

1. En Propiedades de hello para el runbook, seleccione **trabajos** en **recursos**.
2. Debería ver que una lista de trabajos para cada runbook de Hola de tiempo se inició.
3. Haga clic en uno de hello trabajos tooview sus detalles.
4. Haga clic en **todos los registros de** tooview Hola registros y resultados de runbook de Hola.
5. Desplácese toohello inferior toofind una imagen de toohello similar de entrada siguiente.<br>![Detallado](media/operations-management-suite-runbook-datacollect/verbose.png)
6. Haga clic en esta entrada de datos json que envían tooLog análisis detallados que tooview Hola.



## <a name="next-steps"></a>Pasos siguientes
- Use [Diseñador de vistas](../log-analytics/log-analytics-view-designer.md) Hola de toocreate una vista muestra los datos que ha recopilado toohello repositorio de análisis de registros.
- Empaquetar su runbook en un [solución de administración de](operations-management-suite-solutions-creating.md) toodistribute toocustomers.
- Más información sobre [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).
- Más información sobre [Azure Automation](https://docs.microsoft.com/azure/automation/).
- Obtener más información sobre hello [API de recopilador de datos HTTP](../log-analytics/log-analytics-data-collector-api.md).
