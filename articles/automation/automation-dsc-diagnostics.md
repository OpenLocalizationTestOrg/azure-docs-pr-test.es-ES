---
title: "aaaForward informes datos tooOMS análisis de registros de DSC de automatización de Azure | Documentos de Microsoft"
description: "Este artículo se demuestra cómo deseado toosend Configuration (DSC) de reporting datos tooMicrosoft análisis de registros de Operations Management Suite toodeliver obtener información adicional y la administración de estado."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Reenviar reporting datos tooOMS análisis de registros de DSC de automatización de Azure

Automatización puede enviar el área de trabajo de DSC nodo estado datos tooyour análisis de registros de Microsoft Operations Management Suite (OMS).  
Estado de cumplimiento es visible en el portal de Azure de Hola o con PowerShell, para los nodos y para los recursos de DSC individuales en configuraciones de nodo. Con Log Analytics puede:

* Obtener información de cumplimiento de nodos administrados y recursos individuales
* Desencadenar un correo electrónico o una alerta basados en el estado de cumplimiento
* Escribir consultas avanzadas en los nodos administrados
* Correlacionar el estado de cumplimiento en las cuentas de Automation
* Visualizar el historial de cumplimiento de los nodo con el paso del tiempo

## <a name="prerequisites"></a>Requisitos previos

toostart enviar el DSC de automatización de informes tooLog análisis, es necesario:

* Hola noviembre de 2016 o posterior de la versión de [Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Una cuenta de Automatización de Azure Para más información, consulte [Introducción a Azure Automation](automation-offering-get-started.md)
* Un área de trabajo de Log Analytics con una oferta de servicio de **Automation & Control**. Para más información, consulte [Introducción a Log Analytics](../log-analytics/log-analytics-get-started.md).
* Al menos un nodo de DSC de Azure Automation. Para más información, consulte [Incorporación de máquinas para administrarlas con DSC de Azure Automation](automation-dsc-onboarding.md) 

## <a name="set-up-integration-with-log-analytics"></a>Configuración de la integración con Log Analytics

toobegin importar datos de DSC de automatización de Azure a análisis de registros, Hola completa pasos:

1. Inicie sesión en tooyour cuenta de Azure en PowerShell. Consulte [Inicio de sesión con Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)
1. Obtener hello _ResourceId_ de su cuenta de automatización ejecutando el siguiente comando de PowerShell de hello: (si tiene más de una cuenta de automatización, elija hello _ResourceID_ de cuenta de hello desea tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Obtener hello _ResourceId_ de su área de trabajo de análisis de registros ejecutando el siguiente comando de PowerShell de hello: (si tiene más de un área de trabajo, elija hello _ResourceID_ para el área de trabajo de hello desee tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. Hola ejecución siguiente comando de PowerShell, reemplazar `<AutomationResourceId>` y `<WorkspaceResourceId>` con hello _ResourceId_ valores de cada uno de los pasos anteriores de hello:

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Si desea toostop importar datos de DSC de automatización de Azure a análisis de registros, ejecute hello siguiente comando de PowerShell.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Ver registros de hello DSC

Después de configurar la integración con análisis de registros para los datos de DSC de automatización, un **búsqueda de registros** botón aparecerá en hello **nodos** hoja de la cuenta de automatización. Haga clic en hello **Log Search** botón tooview registros de Hola para datos del nodo DSC.

![Botón Búsqueda de registros](media/automation-dsc-diagnostics/log-search-button.png)

Hola **Log Search** hoja se abre y ve un **DscNodeStatusData** operación para cada nodo de DSC y un **DscResourceStatusData** operación para cada [DSC recursos](https://msdn.microsoft.com/powershell/dsc/resources) llama en hello configuración aplicada toothat nodo.

Hola **DscResourceStatusData** operación contiene información de error para los recursos de DSC que dieron error.

Haga clic en cada operación de datos de saludo de hello lista toosee para esa operación.

También puede ver registros de hello mediante la [búsqueda de análisis de registros. Consulte [Búsqueda de datos mediante búsquedas de registros](../log-analytics/log-analytics-log-searches.md).
Consulta de tipo hello siguiente toofind su DSC registros:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

También puede restringir la consulta Hola por nombre de la operación de Hola. Por ejemplo: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>Envío de un correo electrónico cuando se produce un error en cualquier comprobación de cumplimiento de DSC

Uno de nuestras principales solicitudes de cliente es para Hola capacidad toosend un texto o un correo electrónico cuando algo va mal con una configuración de DSC.   

la regla toocreate una alerta, primero debe crear una búsqueda de registros de registros de informes de DSC Hola que se debe invocar la alerta de Hola.  Haga clic en hello **alerta** botón toocreate y configurar la regla de alerta de Hola.

1. En la página de información general de análisis de registro de hello, haga clic en **búsqueda de registros**.
1. Crear una consulta de búsqueda de registro para la alerta, escriba Hola después de búsqueda en el campo de consulta de hello:`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  Si ha configurado los registros de más de una automatización de la cuenta o suscripción tooyour área de trabajo, puede agrupar las alertas por suscripción y cuenta de automatización.  
  Nombre de la cuenta de automatización se puede derivar de campo de recursos de hello en búsqueda de Hola de DscNodeStatusData.  
1. Hola tooopen **Agregar regla de alerta** pantalla, haga clic en **alerta** al principio de Hola de página de Hola. Para obtener más información sobre la alerta de hello opciones tooconfigure hello, consulte [alertas en los análisis de registros](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-failed-dsc-resources-across-all-nodes"></a>Búsqueda de recursos de DSC con errores en todos los nodos

Una ventaja de usar Log Analytics es que es posible buscar comprobaciones con errores en todos los nodos.
toofind todas las instancias de recursos de DSC con errores.

1. En la página de información general de análisis de registro de hello, haga clic en **búsqueda de registros**.
1. Crear una consulta de búsqueda de registro para la alerta, escriba Hola después de búsqueda en el campo de consulta de hello:`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>Visualización del historial de estado del nodo de DSC

Por último, puede que desee toovisualize el historial de estado del nodo de DSC con el tiempo.  
Puede usar este toosearch de consulta de estado de Hola de su estado de nodo de DSC con el tiempo.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

Se mostrará un gráfico de estado del nodo Hola con el tiempo.

## <a name="log-analytics-records"></a>Registros de Log Analytics

Diagnostics, de Azure Automation, crea dos categorías de registros en Log Analytics.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| Propiedad | Descripción |
| --- | --- |
| TimeGenerated |Fecha y hora cuando se ejecutó la comprobación del cumplimiento Hola. |
| nombreOperación |DscNodeStatusData |
| ResultType |Si el nodo de hello es compatible. |
| NodeName_s |nombre de Hello del nodo administrado Hola. |
| NodeComplianceStatus_s |Si el nodo de hello es compatible. |
| DscReportStatus |Si la comprobación del cumplimiento Hola ejecutó correctamente. |
| ConfigurationMode | Cómo la configuración de hello es nodo toohello aplicada. Los valores posibles son __"ApplyOnly"__, __"ApplyandMonitior"__ y __"ApplyandAutoCorrect"__. <ul><li>__ApplyOnly__: DSC aplica la configuración de hello y no hace nada más, a menos que se inserte una nueva configuración de nodo de destino toohello o desde un servidor cuando se extrae una nueva configuración. Después de la aplicación inicial de una nueva configuración, DSC no comprueba si se ha producido una desviación desde un estado configurado previamente. DSC intentos de configuración de hello tooapply hasta que se complete antes de __ApplyOnly__ surte efecto. </li><li> __ApplyAndMonitor__: se trata de valor predeterminado de Hola. Hola LCM aplica las nuevas configuraciones. Después de la aplicación inicial de una nueva configuración, si el nodo de destino de Hola se desplaza del estado de hello deseado, DSC notifica la discrepancia de hello en los registros. DSC intentos de configuración de hello tooapply hasta que se complete antes de __ApplyAndMonitor__ surte efecto.</li><li>__ApplyAndAutoCorrect__: DSC aplica las configuraciones nuevas. Después de la aplicación inicial de una nueva configuración, si el nodo de destino de Hola se desplaza del estado de hello deseado, DSC notifica la discrepancia de hello en los registros y, a continuación, vuelve a aplicar la configuración actual de Hola.</li></ul> |
| HostName_s | nombre de Hello del nodo administrado Hola. |
| IPAddress | dirección IPv4 de Hola de hello administra el nodo. |
| Categoría | DscNodeStatus |
| Recurso | nombre de Hola de hello cuenta de automatización de Azure. |
| Tenant_g | GUID que identifica el inquilino de Hola para hello llamador. |
| NodeId_g |GUID que identifica el nodo administrado Hola. |
| DscReportId_g |GUID que identifica el informe de Hola. |
| LastSeenTime_t |Fecha y hora cuando el informe de hello fue la última vez. |
| ReportStartTime_t |Fecha y hora de inicio de informe de Hola. |
| ReportEndTime_t |Fecha y hora de finalización informe Hola. |
| NumberOfResources_d |número de Hola de recursos de DSC se denomina hello configuración aplicada toohello nodo. |
| SourceSystem | Cómo análisis de registros recopilan los datos de Hola. Siempre *Azure* para Diagnósticos de Azure. |
| ResourceId |Especifica la cuenta de automatización de Azure Hola. |
| ResultDescription | Descripción de Hola para esta operación. |
| SubscriptionId | Hola suscripción de Azure identificador (GUID) para la cuenta de automatización de Hola. |
| ResourceGroup | Nombre del grupo de recursos de Hola de hello cuenta de automatización. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID que es el Id. de correlación del informe de cumplimiento de normas de Hola Hola. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| Propiedad | Descripción |
| --- | --- |
| TimeGenerated |Fecha y hora cuando se ejecutó la comprobación del cumplimiento Hola. |
| nombreOperación |DscResourceStatusData|
| ResultType |Si el recurso de hello es compatible. |
| NodeName_s |nombre de Hello del nodo administrado Hola. |
| Categoría | DscNodeStatus |
| Recurso | nombre de Hola de hello cuenta de automatización de Azure. |
| Tenant_g | GUID que identifica el inquilino de Hola para hello llamador. |
| NodeId_g |GUID que identifica el nodo administrado Hola. |
| DscReportId_g |GUID que identifica el informe de Hola. |
| DscResourceId_s |nombre de Hola de instancia del recurso Hola DSC. |
| DscResourceName_s |nombre de Hello del recurso de hello DSC. |
| DscResourceStatus_s |Si Hola recurso de DSC es compatible. |
| DscModuleName_s |nombre de Hola Hola del módulo de PowerShell que contiene el recurso de DSC de Hola. |
| DscModuleVersion_s |versión de Hola Hola del módulo de PowerShell que contiene el recurso de DSC de Hola. |
| DscConfigurationName_s |nombre de Hola de configuración de hello aplica toohello nodo. |
| ErrorCode_s | código de error de Hello, si el error del recurso de Hola. |
| ErrorMessage_s |mensaje de error de Hello si produce un error de recurso de Hola. |
| DscResourceDuration_d |tiempo de Hello, en segundos, que se ejecutó el recurso de DSC Hola. |
| SourceSystem | Cómo análisis de registros recopilan los datos de Hola. Siempre *Azure* para Diagnósticos de Azure. |
| ResourceId |Especifica la cuenta de automatización de Azure Hola. |
| ResultDescription | Descripción de Hola para esta operación. |
| SubscriptionId | Hola suscripción de Azure identificador (GUID) para la cuenta de automatización de Hola. |
| ResourceGroup | Nombre del grupo de recursos de Hola de hello cuenta de automatización. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID que es el Id. de correlación del informe de cumplimiento de normas de Hola Hola. |

## <a name="summary"></a>Resumen

Mediante el envío de su tooLog de datos análisis de DSC de automatización, puede obtener una mejor visión estado Hola de los nodos de DSC de automatización mediante:

* Configurar toonotify de alertas para cuando se produce un problema
* Mediante vistas personalizadas y toovisualize de las consultas de búsqueda los resultados de runbook, el estado del trabajo de runbook y otros relacionados con indicadores clave o las métricas.  

Análisis de registros proporciona mayor visibilidad operativa tooyour DSC de automatización datos y pueden ayudar a incidentes de dirección más rápidamente.  

## <a name="next-steps"></a>Pasos siguientes

* toolearn más información acerca de cómo las consultas de búsqueda diferente de tooconstruct y revisión Hola DSC de automatización se registra con el análisis de registros, vea [búsquedas de registro de análisis de registros](../log-analytics/log-analytics-log-searches.md)
* toolearn más sobre el uso de DSC de automatización de Azure, consulte [Introducción a DSC de automatización de Azure](automation-dsc-getting-started.md)
* toolearn más información sobre análisis de registros de OMS y orígenes de la colección de datos, vea [datos de almacenamiento de Azure recopilar en información general de análisis de registros](../log-analytics/log-analytics-azure-storage.md)

