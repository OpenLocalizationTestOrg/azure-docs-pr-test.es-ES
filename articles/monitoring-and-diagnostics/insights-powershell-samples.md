---
title: "ejemplos de inicio rápido de PowerShell de Monitor de aaaAzure. | Microsoft Docs"
description: "Usar PowerShell tooaccess características del Monitor de Azure, como el escalado automático, alertas, webhooks y buscar registros de actividad."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Ejemplos de inicio rápido de PowerShell de Azure Monitor
Este artículo se demuestra que tome las muestras toohelp de comandos de PowerShell obtener acceso a características del Monitor de Azure. Monitor de Azure le permite tooAutoScale servicios en la nube, máquinas virtuales y las aplicaciones Web y toosend notificaciones de alerta o direcciones URL de web de llamada basadas en valores de datos de telemetría configurado.

> [!NOTE]
> Monitor de Azure es Hola nuevo nombre lo que se conoce como "Azure Insights" hasta 25 de septiembre de 2016. Sin embargo, hello sigue siendo comandos espacios de nombres de hello y, por tanto, contienen información"Hola".
> 
> 

## <a name="set-up-powershell"></a>Configurar PowerShell
Si no lo ha hecho ya, configure toorun de PowerShell en el equipo. Para obtener más información, consulte [cómo tooInstall y configurar PowerShell](/powershell/azure/overview).

## <a name="examples-in-this-article"></a>Ejemplos de este artículo
ejemplos de Hello en el artículo Hola muestra cómo puede usar cmdlets de Monitor de Azure. También puede revisar la lista completa de Hola de cmdlets de PowerShell de Monitor de Azure en [Cmdlets de Azure Monitor (visión)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).

## <a name="sign-in-and-use-subscriptions"></a>Inicio de sesión y uso de suscripciones
En primer lugar, inicie sesión en tooyour suscripción de Azure.

```PowerShell
Login-AzureRmAccount
```

Para ello, toosign en. Una vez hecho, se muestran el id. predeterminado de la suscripción, el id. de inquilino y la cuenta. Todos los Hola cmdlets de Azure, trabajar en el contexto de Hola de su suscripción de manera predeterminada. lista de hello tooview de suscripciones que tiene acceso, use Hola siguiente comando.

```PowerShell
Get-AzureRmSubscription
```

toochange su trabajo contexto tooa otra suscripción, Hola de uso siguiente comando.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>Recuperación del registro de actividades para una suscripción
Hola de uso `Get-AzureRmLog` cmdlet.  siguiente Hola es algunos ejemplos comunes.

Obtener las entradas del registro de este toopresent de fecha y hora:

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

Obtención de entradas de registro entre un intervalo de fecha y hora:

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Obtención de entradas de registro de un grupo de recursos específico:

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

Obtención de entradas de registro de un proveedor de recursos específico entre un intervalo de fecha y hora:

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Obtener todas las entradas de registro con un llamador concreto:

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

Hola siguiente comando recupera Hola últimos 1000 eventos del registro de actividad de hello:

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog` es compatible con muchos otros parámetros. Vea hello `Get-AzureRmLog` referencia para obtener más información.

> [!NOTE]
> `Get-AzureRmLog` solo proporciona 15 días de historial. Con hello **MaxEvents -** parámetro permite tooquery Hola últimos N eventos, más allá de 15 días. tooaccess eventos anteriores a 15 días, utilice Hola API de REST o SDK (ejemplo de C# con hello SDK). Si no incluye **StartTime**, es el valor predeterminado de hello **EndTime** menos una hora. Si no incluye **EndTime**, valor predeterminado de hello es la hora actual. Todas las horas se muestran en UTC.
> 
> 

## <a name="retrieve-alerts-history"></a>Recuperación del historial de alertas
Hola a tooview todos los eventos de alerta, puede consultar los registros de Azure Resource Manager usando hello en los ejemplos siguientes.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

regla de historial de hello tooview de una alerta específica, puede usar hello `Get-AzureRmAlertHistory` cmdlet, pasando el Id. de recurso de Hola de regla de alerta de Hola.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

Hola `Get-AzureRmAlertHistory` cmdlet admite varios parámetros. Puede obtener más información en [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).

## <a name="retrieve-information-on-alert-rules"></a>Recuperación de información sobre reglas de alerta
Todos Hola siga los comandos actúan en un grupo de recursos denominado "montest".

Ver todas las propiedades de Hola de regla de alerta de hello:

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

Recuperación de todas las alertas de un grupo de recursos:

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

Recuperación de todas las reglas de alerta de un recurso de destino. Por ejemplo, todas las reglas de alerta se establecen en una máquina virtual.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule` es compatible con otros parámetros. Consulte [Get AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) para obtener más información.

## <a name="create-metric-alerts"></a>Creación de alertas de métrica
Puede usar hello `Add-AlertRule` toocreate de cmdlet, actualizar o deshabilitar una regla de alerta.

Puede crear propiedades de correo electrónico y webhook mediante `New-AzureRmAlertRuleEmail` y `New-AzureRmAlertRuleWebhook` respectivamente. En el cmdlet de la regla de alerta de hello, asignar estos como acciones toohello **acciones** propiedad de hello regla de alerta.

Hello en la tabla siguiente describe los parámetros de Hola y valores usado toocreate una alerta con una métrica.

| Parámetro | value |
| --- | --- |
| Nombre |simpletestdiskwrite |
| Ubicación (Location) de esta regla de alerta |Este de EE. UU. |
| ResourceGroup |montest |
| TargetResourceId |/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig |
| MetricName de alerta de Hola que se crea |\PhysicalDisk (_Total) \Disk escrituras por segundo. Vea hello `Get-MetricDefinitions` acerca de cómo tooretrieve Hola nombres de métrica exactos del cmdlet |
| operator |GreaterThan |
| Valor de umbral (número por segundo para esta métrica) |1 |
| WindowSize (formato hh:mm:ss) |00:05:00 |
| agregador (estadística de métrica de hello, que utiliza el recuento de promedio, en este caso) |Media |
| mensajes de correo electrónico personalizados (matriz de cadenas) |"foo@example.com","bar@example.com" |
| enviar correo electrónico tooowners, colaboradores y los lectores |-SendToServiceOwners |

Creación de una acción de correo electrónico

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

Crear una acción de Webhook

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

Crear regla de alerta de hello en la métrica de % de CPU de hello en una máquina virtual clásica

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

Recuperar la regla de alerta de Hola

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

Hola Agregar alerta cmdlet también actualiza la regla de Hola si ya existe una regla de alerta para hello tiene propiedades. toodisable una regla de alerta, incluya el parámetro hello **- DisableRule**.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>Obtención de una lista de métricas disponibles para las alertas
Puede usar hello `Get-AzureRmMetricDefinition` lista de cmdlets tooview Hola de todas las métricas para un recurso concreto.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

Hello en el ejemplo siguiente se genera una tabla con nombre de métrica de Hola y Hola unidad para él.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Hay disponible una lista completa de opciones para `Get-AzureRmMetricDefinition` en [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).

## <a name="create-and-manage-autoscale-settings"></a>Creación y administración de la configuración de escalado automático
Los recursos, como las aplicaciones web, las máquinas virtuales, los servicios en la nube o los conjuntos de escalado de máquinas virtuales, solo pueden tener una configuración de escalado automático.
Sin embargo, cada configuración de escalado automático puede tener varios perfiles. Por ejemplo, uno para un perfil de escalado basado en el rendimiento y otro para uno basado en la programación. Cada perfil puede tener varias reglas configuradas. Para obtener más información acerca de escalado automático, consulte [cómo tooAutoscale una aplicación](../cloud-services/cloud-services-how-to-scale.md).

Estos son los pasos de Hola que se usará:

1. Cree reglas.
2. Crear perfiles de Hola de asignación de reglas que creó previamente toohello perfiles.
3. Opcional: cree notificaciones de escalado automático configurando las propiedades de Webhook y correo electrónico.
4. Crear una configuración de escalado automático con un nombre de recurso de destino de hello mediante la asignación de perfiles de Hola y notificaciones que creó en los pasos anteriores de Hola.

Hello en los ejemplos siguientes muestran cómo se puede crear una configuración de escalado automático para un conjunto de escala de máquinas virtuales para un sistema operativo de Windows usando la métrica de uso de CPU de Hola.

En primer lugar, cree una regla tooscale y de salida, con un aumento del número de instancia.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

A continuación, cree una regla tooscale de, con una disminución del recuento de instancia.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

A continuación, cree un perfil para las reglas de Hola.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

Cree una propiedad de Webhook.

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

Crear ninguna propiedad de notificación de hello para la configuración de escalado automático de hello, incluido el correo electrónico y Hola webhook que creó anteriormente.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

Finalmente, cree Hola configuración tooadd Hola perfil de escalado automático que haya creado anteriormente.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

Para obtener más información sobre cómo administrar la configuración de escalado automático, consulte [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).

## <a name="autoscale-history"></a>Historial de escalado automático
Hello en el ejemplo siguiente se muestra cómo puede ver eventos recientes de escalado automático y esta alerta. Usar historial de hello actividad registro búsqueda tooview Hola escalado automático.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

Puede usar hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve historial de Autoescala.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

Para obtener más información, consulte [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).

### <a name="view-details-for-an-autoscale-setting"></a>Consulta de los detalles de una configuración de escalado automático
Puede usar hello `Get-Autoscalesetting` tooretrieve de cmdlet para obtener más información acerca de la configuración de escalado automático de Hola.

Hello en el ejemplo siguiente se muestra información detallada sobre todas las opciones de escalado automático en el grupo de recursos de hello 'myrg1'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

Hello en el ejemplo siguiente se muestra información detallada sobre todas las opciones de escalado automático en el grupo de recursos de hello 'myrg1' y Hola específicamente la configuración de escalado automático con el nombre 'MyScaleVMSSSetting'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>Eliminación de una configuración de escalado automático
Puede usar hello `Remove-Autoscalesetting` cmdlet toodelete una configuración de escalado automático.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>Administración de perfiles de registro para el registro de actividades
Puede crear un *registro perfil* y exportar los datos de la cuenta de almacenamiento de tooa de registro de actividad y pueden configurar la retención de datos para él. Si lo desea, también puede transmitir datos de hello tooyour concentrador de eventos. Tenga en cuenta que esta característica se encuentra actualmente en la fase de vista previa y solo puede crear un perfil de registro por suscripción. Puede usar hello después cmdlets con los toocreate de suscripción actual y administrar perfiles de registro. También puede elegir una suscripción específica. Aunque PowerShell tiene como valor predeterminado toohello de suscripción actual, puede cambiar siempre que el uso de `Set-AzureRmContext`. Puede configurar la cuenta de almacenamiento de tooany de datos tooroute de registro de actividad o un concentrador de eventos dentro de esa suscripción. Los datos se escriben como archivos blob en formato JSON.

### <a name="get-a-log-profile"></a>Obtención de un perfil de registro
toofetch los perfiles de registro existente, use hello `Get-AzureRmLogProfile` cmdlet.

### <a name="add-a-log-profile-without-data-retention"></a>Adición de un perfil de registro sin retención de datos
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Eliminación de perfil de registro
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>Adición de un perfil de registro con retención de datos
Puede especificar hello **- RetentionInDays** propiedad con hello número de días, como un entero positivo, donde se conservan los datos de Hola.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>Adición de un perfil de registro retención y EventHub
En suma toorouting su cuenta de toostorage de datos, también puede transmitirlo tooan concentrador de eventos. Tenga en cuenta que en esta versión preliminar hello y versión de configuración de la cuenta de almacenamiento es obligatorio pero configuración del centro de eventos es opcional.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>Configuración de registros de diagnóstico
Muchos servicios de Azure proporcionan tooEvent centros de envío de registros adicionales y telemetría que puede ser datos toosave configurado en la cuenta de almacenamiento de Azure, o envían el área de trabajo de análisis de registros de OMS tooan. Esta operación solo puede realizarse en un nivel de recursos y concentrador de evento o la cuenta de almacenamiento Hola debe estar presente en hello misma región como recurso de destino de Hola donde se configura la configuración de diagnósticos de Hola.

### <a name="get-diagnostic-setting"></a>Obtención de la configuración de diagnóstico
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

Deshabilitación de la configuración de diagnóstico

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

Habilitación de la configuración de diagnóstico sin retención

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

Habilitación la configuración de diagnóstico con retención

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Habilitación de la configuración de diagnóstico con retención para una categoría de registro específica

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Habilitación de la configuración de diagnóstico para Event Hubs

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

Habilitación de la configuración de diagnóstico para OMS

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
