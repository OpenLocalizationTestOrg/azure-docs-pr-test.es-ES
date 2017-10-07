---
title: "aaaCollect Azure del servicio registros y métricas de análisis de registros | Documentos de Microsoft"
description: "Configurar los diagnósticos en Azure recursos toowrite registros y métricas de tooLog análisis."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Recopilación de registros y métricas de Azure para servicios de Log Analytics

Hay cuatro maneras diferentes de recopilar registros y métricas para servicios de Azure:

1. Diagnósticos de Azure dirigir tooLog Analytics (*diagnósticos* en hello en la tabla siguiente)
2. Diagnósticos de Azure tooAzure almacenamiento tooLog Analytics (*almacenamiento* en hello en la tabla siguiente)
3. Conectores para los servicios de Azure (*conectores* en hello en la tabla siguiente)
4. Las secuencias de comandos toocollect y, a continuación, los datos de entrada en el análisis de registros (espacios en blanco en hello en la tabla siguiente y servicios que no aparecen)


| Servicio                 | Tipo de recurso                           | Registros        | Métricas     | Solución |
| --- | --- | --- | --- | --- |
| Puertas de enlace de aplicaciones    | Microsoft.Network/applicationGateways   | Diagnóstico | Diagnóstico | [Azure Application Gateway Analytics](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Application Insights    |                                         | Conector   | Conector   | [Application Insights Connector](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (versión preliminar) |
| Cuentas de automatización     | Microsoft.Automation/AutomationAccounts | Diagnóstico |             | [Más información](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Cuentas de Batch          | Microsoft.Batch/batchAccounts           | Diagnóstico | Diagnóstico | |
| Servicios en la nube clásica  |                                         | Almacenamiento     |             | [Más información](log-analytics-azure-storage-iis-table.md) |
| Cognitive Services      | Microsoft.CognitiveServices/accounts    |             | Diagnóstico | |
| Data Lake Analytics     | Microsoft.DataLakeAnalytics/accounts    | Diagnóstico |             | |
| Data Lake Store         | Microsoft.DataLakeStore/accounts        | Diagnóstico |             | |
| Espacio de nombres del Centro de eventos     | Microsoft.EventHub/namespaces           | Diagnóstico | Diagnóstico | |
| IoT Hubs                | Microsoft.Devices/IotHubs               |             | Diagnóstico | |
| Key Vault               | Microsoft.KeyVault/vaults               | Diagnóstico |             | [KeyVault Analytics](log-analytics-azure-key-vault.md) |
| Equilibradores de carga          | Microsoft.Network/loadBalancers         | Diagnóstico |             |  |
| Logic Apps              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | Diagnóstico | Diagnóstico | |
| Grupos de seguridad de red | Microsoft.Network/networksecuritygroups | Diagnóstico |             | [Azure Network Security Group Analytics](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| Almacenes de recuperación         | Microsoft.RecoveryServices/vaults       |             |             | [Azure Recovery Services Analytics (versión preliminar)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Servicios de búsqueda         | Microsoft.Search/searchServices         | Diagnóstico | Diagnóstico | |
| Espacio de nombres de Bus de servicio   | Microsoft.ServiceBus/namespaces         | Diagnóstico | Diagnóstico | [Service Bus Analytics (versión preliminar)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | Almacenamiento     |             | [Service Fabric Analytics (versión preliminar)](log-analytics-service-fabric.md) |
| SQL (v12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | Diagnóstico | [Azure SQL Analytics (versión preliminar)](log-analytics-azure-sql.md) |
| Almacenamiento                 |                                         |             | Script      | [Azure Storage Analytics (versión preliminar)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| Virtual Machines        | Microsoft.Compute/virtualMachines       | Extensión   | Extensión <br> Diagnóstico  | |
| Conjuntos de escalado de máquinas virtuales | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | Diagnóstico | |
| Granjas de servidores web        | Microsoft.Web/serverfarms               |             | Diagnóstico | |
| Sitios web               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | Diagnóstico | [Azure Web Apps Analytics (versión preliminar)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Para la supervisión de máquinas virtuales Azure (Linux y Windows), se recomienda instalar hello [extensión de máquina virtual de análisis de registro](log-analytics-azure-vm-extension.md). agente de Hello proporciona información recopilada desde dentro de las máquinas virtuales. También puede utilizar la extensión de Hola para conjuntos de escalas de máquina Virtual.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Diagnósticos de Azure directa tooLog análisis
Muchos recursos de Azure son métricas y registros de diagnóstico pueda toowrite directamente tooLog análisis y esto forma Hola preferido para recopilar datos de hello para el análisis. Al utilizar Diagnósticos de Azure, se escriben inmediatamente datos tooLog análisis y no hay ningún toostorage necesidad toofirst escritura Hola datos.

Recursos de Azure que admiten [monitor Azure](../monitoring-and-diagnostics/monitoring-overview.md) puede enviar sus registros y métricas directamente tooLog análisis.

* Para obtener detalles de Hola de métricas disponibles hello, consulte demasiado[métricas con el Monitor de Azure admitidas](../monitoring-and-diagnostics/monitoring-supported-metrics.md).
* Para obtener detalles de Hola de registros disponibles de hello, consulte demasiado[admite servicios y el esquema para los registros de diagnóstico](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

### <a name="enable-diagnostics-with-powershell"></a>Habilitación de diagnósticos con PowerShell
Necesita Hola noviembre de 2016 (v2.3.0) o posterior de la versión de [Azure PowerShell](/powershell/azure/overview).

Hola después PowerShell de ejemplo muestra cómo toouse [AzureRmDiagnosticSetting conjunto](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable diagnósticos en un grupo de seguridad de red. Hello mismo enfoque funciona para todos los recursos admitidos: establecer `$resourceId` toohello Id. de recurso del recurso de Hola que desea tooenable los diagnósticos para.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Habilitación de diagnósticos con plantillas de Resource Manager

tooenable diagnósticos en un recurso cuando se crea y le han enviado diagnósticos hello tooyour área de trabajo de análisis de registros que puede usar un toohello similar de plantilla uno a continuación. Este ejemplo es para una cuenta de automatización, pero funciona con todos los tipos de recursos admitidos.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Toostorage de diagnósticos de Azure, a continuación, tooLog análisis

Para recopilar registros desde dentro de algunos recursos, es posible toosend Hola registros tooAzure almacenamiento y, a continuación, configurar registros de hello tooread de análisis de registros de almacenamiento.

Análisis de registros pueden usar este diagnóstico toocollect de enfoque del almacenamiento de Azure para hello después de recursos y los registros:

| Recurso | Registros |
| --- | --- |
| Service Fabric |ETWEvent <br> Evento operativo <br> Eventos de Reliable Actors <br> Evento de Reliable Services |
| Virtual Machines |Syslog de Linux <br> Evento de Windows <br> Registro de IIS <br> Windows ETWEvent |
| Roles web <br> Roles de trabajo |Syslog de Linux <br> Evento de Windows <br> Registro de IIS <br> Windows ETWEvent |

> [!NOTE]
> Se le cobra Azure tarifas normales para almacenamiento y las transacciones cuando envíe diagnósticos tooa cuenta de almacenamiento y al análisis de registros lee datos de Hola desde su cuenta de almacenamiento.
>
>

Vea [Use el almacenamiento de blobs para almacenamiento IIS y la tabla de eventos](log-analytics-azure-storage-iis-table.md) toolearn más información acerca de cómo análisis de registros puede recopilar estos registros.

## <a name="connectors-for-azure-services"></a>Conectores para servicios de Azure

Hay un conector para Application Insights, que permite que los datos recopilados por toobe Application Insights enviado tooLog análisis.

Obtener más información sobre hello [conector de Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>Las secuencias de comandos toocollect y post datos tooLog análisis

Para los servicios de Azure que no proporcionan un tooLog de registros y las métricas de toosend de forma directa análisis puede usar un toocollect de script de automatización de Azure Hola métricas y registro. Hola Hola script a continuación, envío Hola datos tooLog análisis mediante [API del recopilador de datos](log-analytics-data-collector-api.md)

Galería de plantillas de Azure de Hello tiene [ejemplos del uso de automatización de Azure](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect datos de servicios y enviarlo tooLog análisis.

## <a name="next-steps"></a>Pasos siguientes

* [Usar almacenamiento de blobs para almacenamiento IIS y la tabla de eventos](log-analytics-azure-storage-iis-table.md) tooread registros de Hola para servicios de Azure que escriben diagnósticos tootable tooblob escrito almacenamiento de registros de almacenamiento o IIS.
* [Habilitar soluciones](log-analytics-add-solutions.md) visión tooprovide datos Hola.
* [Usar consultas de búsqueda](log-analytics-log-searches.md) tooanalyze datos de saludo.
