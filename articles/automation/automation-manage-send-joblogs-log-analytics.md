---
title: "aaaForward tooOMS de datos de trabajo de automatización de Azure Log Analytics | Documentos de Microsoft"
description: "En este artículo se muestra cómo transmite toosend estado y el runbook de trabajo administración y la visión adicional de tooMicrosoft análisis de registros de Operations Management Suite toodeliver."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>Reenviar el estado del trabajo y flujos de trabajo de automatización tooLog Analytics (OMS)
Automatización puede enviar runbook trabajo estado y el trabajo secuencias tooyour análisis de registros de Microsoft Operations Management Suite (OMS) área de trabajo.  Registros de trabajo y flujos de trabajo están visibles en el portal de Azure de Hola o con PowerShell, para los trabajos individuales y esto le permiten tooperform simple investigaciones. Ahora con Log Analytics puede:

* Obtener información sobre los trabajos de Automatización
* Desencadenador de un correo electrónico o una alerta en función del estado de trabajo del runbook (por ejemplo, error o en suspensión)
* Escribir consultas avanzadas en las transmisiones de trabajos
* Correlacionar trabajos en cuentas de Automatización
* Visualizar el historial de trabajos a lo largo del tiempo     

## <a name="prerequisites-and-deployment-considerations"></a>Requisitos previos y consideraciones de implementación
tooLog análisis de registros de toostart enviar la automatización, necesita:

1. Hola noviembre de 2016 o posterior de la versión de [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Un área de trabajo de Log Analytics. Para más información, consulte [Introducción a Log Analytics](../log-analytics/log-analytics-get-started.md). 
3. Hola ResourceId para su cuenta de automatización de Azure

toofind Hola ResourceId para la cuenta de automatización de Azure y el área de trabajo de análisis de registros, ejecute hello después de PowerShell:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Si tiene varias cuentas de automatización o áreas de trabajo, en la salida de hello de hello anterior comandos, encontrar Hola *nombre* necesita tooconfigure y copie el valor de Hola para *ResourceId*.

Si necesita hello toofind *nombre* de la cuenta de automatización en hello portal de Azure seleccione su cuenta de automatización de hello **cuenta de automatización** hoja y seleccione **todas las configuraciones**.  De hello **toda la configuración de** hoja, en **configuración de la cuenta** seleccione **propiedades**.  Hola **propiedades** hoja, se pueden tener en cuenta estos valores.<br> ![Propiedades de una cuenta de Automatización](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png)(Introducción a Log Analytics).

## <a name="set-up-integration-with-log-analytics"></a>Configuración de la integración con Log Analytics
1. En el equipo, inicie **Windows PowerShell** de hello **iniciar** pantalla.  
2. Copie y pegue Hola después de PowerShell y Editar valor Hola Hola `$workspaceId` y `$automationAccountId`.  Para hello `-Environment` parámetro, los valores válidos son *nube de Azure* o *AzureUSGovernment* según el entorno de nube de hello si está trabajando en.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

Después de ejecutar este script, verá los registros de Log Analytics a los 10 minutos de escribir los nuevos JobLogs o JobStreams.

registros de hello toosee, ejecute hello después de la consulta de búsqueda de registros de análisis de registros:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>Comprobación de la configuración
área de trabajo de análisis de registros de tooyour los registros de tooconfirm que está enviando la cuenta de automatización, compruebe que diagnósticos están establecidos correctamente en la cuenta de automatización de hello mediante Hola después de PowerShell:

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

En la salida de hello Asegúrese de que:
+ En *registros*, Hola valor para *habilitado* es *True*
+ Hola valo *WorkspaceId* se establece toohello ResourceId de su área de trabajo de análisis de registros


## <a name="log-analytics-records"></a>Registros de Log Analytics
Diagnósticos de Azure Automation crea dos tipos de registros en Log Analytics y se etiquetan como **Type=AzureDiagnostics**.

### <a name="job-logs"></a>Registros de trabajo
| Propiedad | Descripción |
| --- | --- |
| TimeGenerated |Fecha y hora cuando se ejecuta el trabajo del runbook de Hola. |
| RunbookName_s |nombre de Hola de runbook de Hola. |
| Caller_s |Quién inició la operación de Hola.  Los valores posibles son una dirección de correo electrónico o el sistema para los trabajos programados. |
| Tenant_g | GUID que identifica el inquilino de Hola para hello llamador. |
| JobId_g |GUID que es el Id. de trabajo de runbook de Hola Hola. |
| ResultType |estado de Hola de trabajo de runbook de Hola.  Los valores posibles son:<br>Started<br>Stopped<br>Suspended<br>Con error<br>Completado |
| Categoría | Clasificación de tipo hello de datos.  Para la automatización, el valor de hello es JobLogs. |
| nombreOperación | Especifica el tipo de saludo de operación realizada en Azure.  Para la automatización, el valor de hello es trabajo. |
| Recurso | Nombre de cuenta de automatización de hello |
| SourceSystem | Cómo análisis de registros recopilan los datos de Hola. Siempre *Azure* para Diagnósticos de Azure. |
| ResultDescription |Describe el estado de resultado del trabajo de runbook de Hola.  Los valores posibles son:<br>- Se inicia el trabajo<br>- Error del trabajo<br>- Trabajo completado |
| CorrelationId |GUID que es el Id. de correlación de trabajo de runbook de Hola Hola. |
| ResourceId |Especifica el identificador de recurso de cuenta de automatización de Azure de Hola de runbook de Hola. |
| SubscriptionId | Hola suscripción de Azure identificador (GUID) para la cuenta de automatización de Hola. |
| ResourceGroup | Nombre del grupo de recursos de Hola de hello cuenta de automatización. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>Flujos de trabajo
| Propiedad | Descripción |
| --- | --- |
| TimeGenerated |Fecha y hora cuando se ejecuta el trabajo del runbook de Hola. |
| RunbookName_s |nombre de Hola de runbook de Hola. |
| Caller_s |Quién inició la operación de Hola.  Los valores posibles son una dirección de correo electrónico o el sistema para los trabajos programados. |
| StreamType_s |tipo de Hola de flujo de trabajo. Los valores posibles son:<br>progreso<br>- Salida<br>Warning (Advertencia)<br>Error<br>DEBUG<br>- Detallado |
| Tenant_g | GUID que identifica el inquilino de Hola para hello llamador. |
| JobId_g |GUID que es el Id. de trabajo de runbook de Hola Hola. |
| ResultType |estado de Hola de trabajo de runbook de Hola.  Los valores posibles son:<br>- In Progress |
| Categoría | Clasificación de tipo hello de datos.  Para la automatización, el valor de hello es JobStreams. |
| nombreOperación | Especifica el tipo de saludo de operación realizada en Azure.  Para la automatización, el valor de hello es trabajo. |
| Recurso | Nombre de cuenta de automatización de hello |
| SourceSystem | Cómo análisis de registros recopilan los datos de Hola. Siempre *Azure* para Diagnósticos de Azure. |
| ResultDescription |Incluye el flujo de salida de hello de runbook de Hola. |
| CorrelationId |GUID que es el Id. de correlación de trabajo de runbook de Hola Hola. |
| ResourceId |Especifica el identificador de recurso de cuenta de automatización de Azure de Hola de runbook de Hola. |
| SubscriptionId | Hola suscripción de Azure identificador (GUID) para la cuenta de automatización de Hola. |
| ResourceGroup | Nombre del grupo de recursos de Hola de hello cuenta de automatización. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Visualización de registros de Automatización en Log Analytics
Ahora que ha iniciado la enviar los registros de trabajo automatización tooLog análisis, veamos lo que puede hacer con estos registros de análisis de registros.

registros de hello toosee, ejecute hello después de consulta:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Envío de un correo electrónico cuando se produce un error en un trabajo del runbook o se suspende
Uno de nuestros clientes superior pide es para hello capacidad toosend un texto o un correo electrónico cuando algo va mal con un trabajo de runbook.   

la regla toocreate una alerta, primero debe crear una búsqueda de registros de runbook de hello registros de trabajos que se deben invocar alerta Hola.  Haga clic en hello **alerta** botón toocreate y configurar la regla de alerta de Hola.

1. En la página de información general de análisis de registro de hello, haga clic en **búsqueda de registros**.
2. Crear una consulta de búsqueda de registro para la alerta escribiendo Hola después de búsqueda en el campo de consulta de hello: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` también puede agrupar por hello RunbookName mediante el uso de:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   Si ha configurado los registros de más de una automatización de la cuenta o suscripción tooyour área de trabajo, puede agrupar las alertas por suscripción y cuenta de automatización.  Nombre de la cuenta de automatización se puede derivar de campo de recursos de hello en búsqueda de Hola de JobLogs.  
3. Hola tooopen **Agregar regla de alerta** pantalla, haga clic en **alerta** al principio de Hola de página de Hola. Para obtener más información sobre la alerta de hello opciones tooconfigure hello, consulte [alertas en los análisis de registros](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Búsqueda de todos los trabajos que se han completado con errores
Además tooalerting cuando se produzcan errores, puede encontrar cuando un trabajo de runbook tiene un error de no terminación. En estos casos PowerShell genera una secuencia de error, pero errores de no terminación de Hola no hacer su trabajo toosuspend o se producirá un error.    

1. En el área de trabajo de Log Analytics, haga clic en **Búsqueda de registros**.
2. En el campo de consulta de hello, escriba `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` y, a continuación, haga clic en **búsqueda**.

### <a name="view-job-streams-for-a-job"></a>Visualización de las transmisiones de un trabajo
Cuando se depura un trabajo, también puede toolook en flujos de trabajo de Hola.  Hello consulta siguiente muestra todos los flujos de Hola de un único trabajo con GUID de 2ebd22ea-e05e-4eb9 - 9D 76 d73cbd4356e0:   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>Visualización del estado del historial de trabajos
Por último, puede que desee toovisualize el historial de trabajos con el tiempo.  Puede usar este toosearch de consulta para el estado de saludo de los trabajos con el tiempo.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![Gráfico del historial de trabajos de OMS](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Resumen
Mediante el envío de la automatización trabajo estado y flujo de datos tooLog análisis, puede obtener una mejor visión estado Hola de los trabajos de automatización de la forma:
+ Configurar toonotify de alertas para cuando se produce un problema
+ Mediante vistas personalizadas y toovisualize de las consultas de búsqueda los resultados de runbook, el estado del trabajo de runbook y otros relacionados con indicadores clave o las métricas.  

Análisis de registros proporciona mayor visibilidad operativa trabajos de automatización de tooyour y pueden ayudar a incidentes de dirección más rápidas.  

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de cómo las consultas de búsqueda diferente de tooconstruct y revisión Hola automatización trabajo registros con análisis de registros, vea [búsquedas de registro de análisis de registros](../log-analytics/log-analytics-log-searches.md)
* toounderstand toocreate y recuperar mensajes de error y de salida de runbooks, vea [Runbook de salida y mensajes](automation-runbook-output-and-messages.md)
* más información acerca de la ejecución de un runbook, cómo toomonitor runbook trabajos y otros detalles técnicos, consulte toolearn [realizar un seguimiento de un trabajo de runbook](automation-runbook-execution.md)
* toolearn más información sobre análisis de registros de OMS y orígenes de la colección de datos, vea [datos de almacenamiento de Azure recopilar en información general de análisis de registros](../log-analytics/log-analytics-azure-storage.md)
