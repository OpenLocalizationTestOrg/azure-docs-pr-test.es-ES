---
title: "aaaAzure tutorial de API de REST de supervisión | Documentos de Microsoft"
description: "¿Cómo tooauthenticate solicita tooand uso Hola API de REST de supervisión de Azure."
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a>Tutorial sobre la API de REST de supervisión de Azure
Este artículo muestra cómo tooperform autenticación por lo que el código pueda utilizar hello [referencia de la API de REST de Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Hola API de Monitor de Azure facilita tooprogrammatically posible recuperar Hola predeterminadas disponibles las definiciones métricas (tipo de Hola de métrica como el tiempo de CPU, las solicitudes, etc.), granularidad y valores de métrica. Una vez recuperado, datos de hello pueden guardarse en un almacén de datos independiente como base de datos de SQL Azure, base de datos de Azure Cosmos o Azure Data Lake. Desde allí se pueden realizar análisis adicionales según sea necesario.

Además de trabajar con varios puntos de datos de métrica, como se muestra en este artículo, Hola Monitor API facilita las reglas de alerta de posibles toolist, ver registros de actividad y mucho más. Para obtener una lista completa de las operaciones disponibles, vea hello [referencia de la API de REST de Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Autenticación de solicitudes de Azure Monitor
Hola primer paso es tooauthenticate solicitud de saludo.

Todas las tareas de hello ejecutadas en modelo de autenticación de hello Azure Monitor API uso hello Azure Resource Manager. Por lo tanto, todas las solicitudes deben autenticarse con Azure Active Directory (Azure AD). Una aplicación de cliente hello de enfoque tooauthenticate es toocreate una entidad de seguridad de servicio de Azure AD y recuperar el token de autenticación (JWT) de Hola. Hello secuencia de comandos de ejemplo siguiente muestra cómo crear un anuncio de Azure entidad de servicio a través de PowerShell. Para ver un tutorial más detallado, consulte la documentación del toohello en [con Azure PowerShell toocreate una entidad de seguridad tooaccess los recursos del servicio](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). También es posible demasiado[crear una entidad de servicio a través del portal de Azure hello](../azure-resource-manager/resource-group-create-service-principal-portal.md).

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

Hola tooquery API de Monitor de Azure, aplicación de cliente de hello debe usar Hola creado anteriormente tooauthenticate principal de servicio. Hola siguiente script de PowerShell de ejemplo muestra un enfoque, con hello [biblioteca de autenticación de Active Directory](../active-directory/active-directory-authentication-libraries.md) toohelp (AAL) obtener el token de autenticación de JWT de Hola. token de JWT de Hola se pasa como parte de un parámetro de autorización HTTP en solicitudes toohello API de REST de Monitor de Azure.

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

Una vez completado el paso de configuración de autenticación de hello, a continuación, se pueden ejecutar consultas en hello API de REST de Monitor de Azure. Hay dos consultas útiles:

1. Hola definiciones métricas para un recurso de la lista
2. Recuperar valores de métrica de Hola

## <a name="retrieve-metric-definitions"></a>Recuperación de las definiciones de métricas
> [!NOTE]
> definiciones de métrica de tooretrieve con hello API de REST de Monitor de Azure, use "2016-03-01" como Hola versión de API.
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
Para una aplicación de lógica de Azure, las definiciones de métrica de hello tendría un aspecto similar toohello siguiente captura de pantalla:

![Alt "Vista JSON de la respuesta de la definición de la métrica"](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Para obtener más información, vea hello [lista definiciones de métrica de Hola para un recurso en la API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentación.

## <a name="retrieve-metric-values"></a>Recuperación de los valores de métrica
Una vez que se conocen las definiciones de métricas disponibles hello, que no esté tooretrieve posibles Hola valores de métrica relacionados. Use nombre 'value' de métrica de hello (no Hola 'localizedValue') para cualquier solicitud de filtrado (por ejemplo, recuperar hello 'CpuTime' y 'Solicita' métrica puntos de datos). Si no se especifica ningún filtro, se devuelve la métrica de hello predeterminada.

> [!NOTE]
> los valores de métrica tooretrieve con hello API de REST de Monitor de Azure, use "2016-06-01" como Hola versión de API.
>
>

**Método**: GET

**URI de solicitud**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&amp;api-version=*{apiVersion}*

Por ejemplo, puntos de datos de métricas de RunsSucceeded de tooretrieve Hola para hello dado el intervalo de tiempo y un detalle de tiempo de 1 hora, solicitud de hello sería como sigue:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

resultado de Hello tendría un aspecto similar ejemplo toohello siguiente captura de pantalla:

![Alt "Respuesta JSON que muestra el valor de métrica del tiempo medio de respuesta"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

tooretrieve varios datos o agregación de puntos, agregue los nombres de definición de métricas de Hola y filtro de toohello de tipos de agregación, tal como se muestra en el siguiente ejemplo de Hola:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>Uso de ARMClient
Una alternativa toousing PowerShell (como se muestra arriba), es toouse [ARMClient](https://github.com/projectkudu/ARMClient) en su equipo de Windows. ARMClient administra la autenticación de hello Azure AD (y token JWT resultante) automáticamente. Hello pasos siguientes describen el uso de ARMClient para recuperar datos de métrica:

1. Instale [Chocolatey](https://chocolatey.org/) y [ARMClient](https://github.com/projectkudu/ARMClient).
2. En una ventana de terminal, escriba *inicio de sesión de armclient.exe*. Esto le toolog en tooAzure.
3. Escriba *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Escriba *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![ALT "Using ARMClient toowork con hello Azure API de REST de supervisión"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Recuperar Hola Id. de recurso
Utilizando la API de REST de hello realmente puede ayudar a definiciones de métricas disponibles toounderstand hello, granularidad y valores relacionados. Dicha información es útil cuando se usa hello [biblioteca de administración de Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Hola anterior código toouse de Id. de recurso de hello es toohello de ruta de acceso completa de hello deseado recursos de Azure. Por ejemplo, tooquery en una aplicación Web de Azure, Id. de recurso de hello sería:

*/subscriptions/{identificador-suscripción}/resourceGroups/{nombre-grupo-recursos}/providers/Microsoft.Web/sites/{nombre-sitio}/*

Hello lista siguiente contiene algunos ejemplos de formatos de Id. de recurso de distintos recursos de Azure:

* **IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*
* **Grupo elástico SQL** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*
* **SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*
* **Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*
* **Conjuntos de escala de VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*
* **VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*
* **Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*

Hay alternativas tooretrieving Hola Id. de recurso, incluido el uso de explorador de recursos de Azure, ver recursos de hello deseado en hello portal de Azure y, a través de PowerShell u Hola CLI de Azure.

### <a name="azure-resource-explorer"></a>Explorador de recursos de Azure
Id. de recurso de hello toofind para un recurso deseado, un enfoque útil es toouse hello [Explorador de recursos de Azure](https://resources.azure.com) herramienta. Navegar por los recursos toohello deseado y, a continuación, busque en el Id. de Hola se muestra, como en la siguiente captura de pantalla de hello:

![Alt "Explorador de recursos de Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Azure Portal
Id. de recurso de Hello también puede obtenerse de hello portal de Azure. por lo tanto, toodo navegue recursos toohello deseado y, a continuación, seleccione Propiedades. Hola Id. de recurso se muestra en la hoja de propiedades de hello, tal como se muestra en la siguiente captura de pantalla de hello:

![ALT "Id. de recurso aparece en la hoja de propiedades de Hola Hola portal de Azure"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
Id. de recurso de Hola se puede recuperar mediante cmdlets de PowerShell de Azure también. Por ejemplo, Id. de recurso de hello tooobtain para una aplicación Web de Azure, ejecute cmdlet Hola Get-AzureRmWebApp, como en la siguiente captura de pantalla de Hola:

![Alt "Identificador de recurso obtenido a través de PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>CLI de Azure
tooretrieve Hola Id. de recurso con hello CLI de Azure, ejecutar el comando "Mostrar webapp de azure" Hola, especificar hello '--json' opción, como se muestra en la siguiente captura de pantalla de hello:

![Alt "Identificador de recurso obtenido a través de PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Recuperación de datos del registro de actividades
En suma tooworking con definiciones de métrica y valores relacionados, también es posible tooretrieve adicionales recursos interesantes visión tooAzure relacionados. Por ejemplo, es posible tooquery [registro de actividad](https://msdn.microsoft.com/library/azure/dn931934.aspx) datos. Hello en el ejemplo siguiente muestra cómo utilizar datos de registro de hello API de REST de Azure Monitor tooquery actividad dentro de un intervalo de fechas específico para una suscripción de Azure:

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>Pasos siguientes
* Hola de revisión [información general de supervisión](monitoring-overview.md).
* Hola de vista [métricas con el Monitor de Azure admitidas](monitoring-supported-metrics.md).
* Hola de revisión [referencia de la API de REST de Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Hola de revisión [biblioteca de administración de Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
