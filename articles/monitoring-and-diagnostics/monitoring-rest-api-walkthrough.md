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
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="90892-103">Tutorial sobre la API de REST de supervisión de Azure</span><span class="sxs-lookup"><span data-stu-id="90892-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="90892-104">Este artículo muestra cómo tooperform autenticación por lo que el código pueda utilizar hello [referencia de la API de REST de Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="90892-104">This article shows you how tooperform authentication so your code can use hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="90892-105">Hola API de Monitor de Azure facilita tooprogrammatically posible recuperar Hola predeterminadas disponibles las definiciones métricas (tipo de Hola de métrica como el tiempo de CPU, las solicitudes, etc.), granularidad y valores de métrica.</span><span class="sxs-lookup"><span data-stu-id="90892-105">hello Azure Monitor API makes it possible tooprogrammatically retrieve hello available default metric definitions (hello type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="90892-106">Una vez recuperado, datos de hello pueden guardarse en un almacén de datos independiente como base de datos de SQL Azure, base de datos de Azure Cosmos o Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="90892-106">Once retrieved, hello data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="90892-107">Desde allí se pueden realizar análisis adicionales según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="90892-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="90892-108">Además de trabajar con varios puntos de datos de métrica, como se muestra en este artículo, Hola Monitor API facilita las reglas de alerta de posibles toolist, ver registros de actividad y mucho más.</span><span class="sxs-lookup"><span data-stu-id="90892-108">Besides working with various metric data points, as this article demonstrates, hello Monitor API makes it possible toolist alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="90892-109">Para obtener una lista completa de las operaciones disponibles, vea hello [referencia de la API de REST de Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="90892-109">For a full list of available operations, see hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="90892-110">Autenticación de solicitudes de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="90892-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="90892-111">Hola primer paso es tooauthenticate solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="90892-111">hello first step is tooauthenticate hello request.</span></span>

<span data-ttu-id="90892-112">Todas las tareas de hello ejecutadas en modelo de autenticación de hello Azure Monitor API uso hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="90892-112">All hello tasks executed against hello Azure Monitor API use hello Azure Resource Manager authentication model.</span></span> <span data-ttu-id="90892-113">Por lo tanto, todas las solicitudes deben autenticarse con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90892-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="90892-114">Una aplicación de cliente hello de enfoque tooauthenticate es toocreate una entidad de seguridad de servicio de Azure AD y recuperar el token de autenticación (JWT) de Hola.</span><span class="sxs-lookup"><span data-stu-id="90892-114">One approach tooauthenticate hello client application is toocreate an Azure AD service principal and retrieve hello authentication (JWT) token.</span></span> <span data-ttu-id="90892-115">Hello secuencia de comandos de ejemplo siguiente muestra cómo crear un anuncio de Azure entidad de servicio a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90892-115">hello following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="90892-116">Para ver un tutorial más detallado, consulte la documentación del toohello en [con Azure PowerShell toocreate una entidad de seguridad tooaccess los recursos del servicio](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="90892-116">For a more detailed walk-through, refer toohello documentation on [using Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="90892-117">También es posible demasiado[crear una entidad de servicio a través del portal de Azure hello](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="90892-117">It is also possible too[create a service principal via hello Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

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

<span data-ttu-id="90892-118">Hola tooquery API de Monitor de Azure, aplicación de cliente de hello debe usar Hola creado anteriormente tooauthenticate principal de servicio.</span><span class="sxs-lookup"><span data-stu-id="90892-118">tooquery hello Azure Monitor API, hello client application should use hello previously created service principal tooauthenticate.</span></span> <span data-ttu-id="90892-119">Hola siguiente script de PowerShell de ejemplo muestra un enfoque, con hello [biblioteca de autenticación de Active Directory](../active-directory/active-directory-authentication-libraries.md) toohelp (AAL) obtener el token de autenticación de JWT de Hola.</span><span class="sxs-lookup"><span data-stu-id="90892-119">hello following example PowerShell script shows one approach, using hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp get hello JWT authentication token.</span></span> <span data-ttu-id="90892-120">token de JWT de Hola se pasa como parte de un parámetro de autorización HTTP en solicitudes toohello API de REST de Monitor de Azure.</span><span class="sxs-lookup"><span data-stu-id="90892-120">hello JWT token is passed as part of an HTTP Authorization parameter in requests toohello Azure Monitor REST API.</span></span>

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

<span data-ttu-id="90892-121">Una vez completado el paso de configuración de autenticación de hello, a continuación, se pueden ejecutar consultas en hello API de REST de Monitor de Azure.</span><span class="sxs-lookup"><span data-stu-id="90892-121">Once hello authentication setup step is complete, queries can then be executed against hello Azure Monitor REST API.</span></span> <span data-ttu-id="90892-122">Hay dos consultas útiles:</span><span class="sxs-lookup"><span data-stu-id="90892-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="90892-123">Hola definiciones métricas para un recurso de la lista</span><span class="sxs-lookup"><span data-stu-id="90892-123">List hello metric definitions for a resource</span></span>
2. <span data-ttu-id="90892-124">Recuperar valores de métrica de Hola</span><span class="sxs-lookup"><span data-stu-id="90892-124">Retrieve hello metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="90892-125">Recuperación de las definiciones de métricas</span><span class="sxs-lookup"><span data-stu-id="90892-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="90892-126">definiciones de métrica de tooretrieve con hello API de REST de Monitor de Azure, use "2016-03-01" como Hola versión de API.</span><span class="sxs-lookup"><span data-stu-id="90892-126">tooretrieve metric definitions using hello Azure Monitor REST API, use "2016-03-01" as hello API version.</span></span>
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
<span data-ttu-id="90892-127">Para una aplicación de lógica de Azure, las definiciones de métrica de hello tendría un aspecto similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="90892-127">For an Azure Logic App, hello metric definitions would appear similar toohello following screenshot:</span></span>

![Alt "Vista JSON de la respuesta de la definición de la métrica"](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="90892-129">Para obtener más información, vea hello [lista definiciones de métrica de Hola para un recurso en la API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentación.</span><span class="sxs-lookup"><span data-stu-id="90892-129">For more information, see hello [List hello metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="90892-130">Recuperación de los valores de métrica</span><span class="sxs-lookup"><span data-stu-id="90892-130">Retrieve Metric Values</span></span>
<span data-ttu-id="90892-131">Una vez que se conocen las definiciones de métricas disponibles hello, que no esté tooretrieve posibles Hola valores de métrica relacionados.</span><span class="sxs-lookup"><span data-stu-id="90892-131">Once hello available metric definitions are known, it is then possible tooretrieve hello related metric values.</span></span> <span data-ttu-id="90892-132">Use nombre 'value' de métrica de hello (no Hola 'localizedValue') para cualquier solicitud de filtrado (por ejemplo, recuperar hello 'CpuTime' y 'Solicita' métrica puntos de datos).</span><span class="sxs-lookup"><span data-stu-id="90892-132">Use hello metric’s name ‘value’ (not hello ‘localizedValue’) for any filtering requests (for example, retrieve hello ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="90892-133">Si no se especifica ningún filtro, se devuelve la métrica de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="90892-133">If no filters are specified, hello default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="90892-134">los valores de métrica tooretrieve con hello API de REST de Monitor de Azure, use "2016-06-01" como Hola versión de API.</span><span class="sxs-lookup"><span data-stu-id="90892-134">tooretrieve metric values using hello Azure Monitor REST API, use "2016-06-01" as hello API version.</span></span>
>
>

<span data-ttu-id="90892-135">**Método**: GET</span><span class="sxs-lookup"><span data-stu-id="90892-135">**Method**: GET</span></span>

<span data-ttu-id="90892-136">**URI de solicitud**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&amp;api-version=*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="90892-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="90892-137">Por ejemplo, puntos de datos de métricas de RunsSucceeded de tooretrieve Hola para hello dado el intervalo de tiempo y un detalle de tiempo de 1 hora, solicitud de hello sería como sigue:</span><span class="sxs-lookup"><span data-stu-id="90892-137">For example, tooretrieve hello RunsSucceeded metric data points for hello given time range and for a time grain of 1 hour, hello request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="90892-138">resultado de Hello tendría un aspecto similar ejemplo toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="90892-138">hello result would appear similar toohello example following screenshot:</span></span>

![Alt "Respuesta JSON que muestra el valor de métrica del tiempo medio de respuesta"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="90892-140">tooretrieve varios datos o agregación de puntos, agregue los nombres de definición de métricas de Hola y filtro de toohello de tipos de agregación, tal como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="90892-140">tooretrieve multiple data or aggregation points, add hello metric definition names and aggregation types toohello filter, as seen in hello following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="90892-141">Uso de ARMClient</span><span class="sxs-lookup"><span data-stu-id="90892-141">Use ARMClient</span></span>
<span data-ttu-id="90892-142">Una alternativa toousing PowerShell (como se muestra arriba), es toouse [ARMClient](https://github.com/projectkudu/ARMClient) en su equipo de Windows.</span><span class="sxs-lookup"><span data-stu-id="90892-142">An alternative toousing PowerShell (as shown above), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="90892-143">ARMClient administra la autenticación de hello Azure AD (y token JWT resultante) automáticamente.</span><span class="sxs-lookup"><span data-stu-id="90892-143">ARMClient handles hello Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="90892-144">Hello pasos siguientes describen el uso de ARMClient para recuperar datos de métrica:</span><span class="sxs-lookup"><span data-stu-id="90892-144">hello following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="90892-145">Instale [Chocolatey](https://chocolatey.org/) y [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="90892-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="90892-146">En una ventana de terminal, escriba *inicio de sesión de armclient.exe*.</span><span class="sxs-lookup"><span data-stu-id="90892-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="90892-147">Esto le toolog en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="90892-147">This prompts you toolog in tooAzure.</span></span>
3. <span data-ttu-id="90892-148">Escriba *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="90892-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="90892-149">Escriba *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="90892-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![ALT "Using ARMClient toowork con hello Azure API de REST de supervisión"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a><span data-ttu-id="90892-151">Recuperar Hola Id. de recurso</span><span class="sxs-lookup"><span data-stu-id="90892-151">Retrieve hello Resource ID</span></span>
<span data-ttu-id="90892-152">Utilizando la API de REST de hello realmente puede ayudar a definiciones de métricas disponibles toounderstand hello, granularidad y valores relacionados.</span><span class="sxs-lookup"><span data-stu-id="90892-152">Using hello REST API can really help toounderstand hello available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="90892-153">Dicha información es útil cuando se usa hello [biblioteca de administración de Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="90892-153">That information is helpful when using hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="90892-154">Hola anterior código toouse de Id. de recurso de hello es toohello de ruta de acceso completa de hello deseado recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="90892-154">For hello preceding code, hello resource ID toouse is hello full path toohello desired Azure resource.</span></span> <span data-ttu-id="90892-155">Por ejemplo, tooquery en una aplicación Web de Azure, Id. de recurso de hello sería:</span><span class="sxs-lookup"><span data-stu-id="90892-155">For example, tooquery against an Azure Web App, hello resource ID would be:</span></span>

<span data-ttu-id="90892-156">*/subscriptions/{identificador-suscripción}/resourceGroups/{nombre-grupo-recursos}/providers/Microsoft.Web/sites/{nombre-sitio}/*</span><span class="sxs-lookup"><span data-stu-id="90892-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="90892-157">Hello lista siguiente contiene algunos ejemplos de formatos de Id. de recurso de distintos recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="90892-157">hello following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="90892-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span><span class="sxs-lookup"><span data-stu-id="90892-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="90892-159">**Grupo elástico SQL** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span><span class="sxs-lookup"><span data-stu-id="90892-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="90892-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span><span class="sxs-lookup"><span data-stu-id="90892-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="90892-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span><span class="sxs-lookup"><span data-stu-id="90892-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="90892-162">**Conjuntos de escala de VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="90892-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="90892-163">**VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="90892-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="90892-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span><span class="sxs-lookup"><span data-stu-id="90892-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="90892-165">Hay alternativas tooretrieving Hola Id. de recurso, incluido el uso de explorador de recursos de Azure, ver recursos de hello deseado en hello portal de Azure y, a través de PowerShell u Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="90892-165">There are alternative approaches tooretrieving hello resource ID, including using Azure Resource Explorer, viewing hello desired resource in hello Azure portal, and via PowerShell or hello Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="90892-166">Explorador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="90892-166">Azure Resource Explorer</span></span>
<span data-ttu-id="90892-167">Id. de recurso de hello toofind para un recurso deseado, un enfoque útil es toouse hello [Explorador de recursos de Azure](https://resources.azure.com) herramienta.</span><span class="sxs-lookup"><span data-stu-id="90892-167">toofind hello resource ID for a desired resource, one helpful approach is toouse hello [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="90892-168">Navegar por los recursos toohello deseado y, a continuación, busque en el Id. de Hola se muestra, como en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="90892-168">Navigate toohello desired resource and then look at hello ID shown, as in hello following screenshot:</span></span>

![Alt "Explorador de recursos de Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="90892-170">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="90892-170">Azure portal</span></span>
<span data-ttu-id="90892-171">Id. de recurso de Hello también puede obtenerse de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="90892-171">hello resource ID can also be obtained from hello Azure portal.</span></span> <span data-ttu-id="90892-172">por lo tanto, toodo navegue recursos toohello deseado y, a continuación, seleccione Propiedades.</span><span class="sxs-lookup"><span data-stu-id="90892-172">toodo so, navigate toohello desired resource and then select Properties.</span></span> <span data-ttu-id="90892-173">Hola Id. de recurso se muestra en la hoja de propiedades de hello, tal como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="90892-173">hello Resource ID is displayed in hello Properties blade, as seen in hello following screenshot:</span></span>

![ALT "Id. de recurso aparece en la hoja de propiedades de Hola Hola portal de Azure"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="90892-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="90892-175">Azure PowerShell</span></span>
<span data-ttu-id="90892-176">Id. de recurso de Hola se puede recuperar mediante cmdlets de PowerShell de Azure también.</span><span class="sxs-lookup"><span data-stu-id="90892-176">hello resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="90892-177">Por ejemplo, Id. de recurso de hello tooobtain para una aplicación Web de Azure, ejecute cmdlet Hola Get-AzureRmWebApp, como en la siguiente captura de pantalla de Hola:</span><span class="sxs-lookup"><span data-stu-id="90892-177">For example, tooobtain hello resource ID for an Azure Web App, execute hello Get-AzureRmWebApp cmdlet, as in hello following screenshot:</span></span>

![Alt "Identificador de recurso obtenido a través de PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="90892-179">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="90892-179">Azure CLI</span></span>
<span data-ttu-id="90892-180">tooretrieve Hola Id. de recurso con hello CLI de Azure, ejecutar el comando "Mostrar webapp de azure" Hola, especificar hello '--json' opción, como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="90892-180">tooretrieve hello resource ID using hello Azure CLI, execute hello 'azure webapp show' command, specifying hello '--json' option, as shown in hello following screenshot:</span></span>

![Alt "Identificador de recurso obtenido a través de PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="90892-182">Recuperación de datos del registro de actividades</span><span class="sxs-lookup"><span data-stu-id="90892-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="90892-183">En suma tooworking con definiciones de métrica y valores relacionados, también es posible tooretrieve adicionales recursos interesantes visión tooAzure relacionados.</span><span class="sxs-lookup"><span data-stu-id="90892-183">In addition tooworking with metric definitions and related values, it is also possible tooretrieve additional interesting insights related tooAzure resources.</span></span> <span data-ttu-id="90892-184">Por ejemplo, es posible tooquery [registro de actividad](https://msdn.microsoft.com/library/azure/dn931934.aspx) datos.</span><span class="sxs-lookup"><span data-stu-id="90892-184">As an example, it is possible tooquery [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="90892-185">Hello en el ejemplo siguiente muestra cómo utilizar datos de registro de hello API de REST de Azure Monitor tooquery actividad dentro de un intervalo de fechas específico para una suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="90892-185">hello following sample demonstrates using hello Azure Monitor REST API tooquery activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="90892-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90892-186">Next steps</span></span>
* <span data-ttu-id="90892-187">Hola de revisión [información general de supervisión](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90892-187">Review hello [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="90892-188">Hola de vista [métricas con el Monitor de Azure admitidas](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="90892-188">View hello [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="90892-189">Hola de revisión [referencia de la API de REST de Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="90892-189">Review hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="90892-190">Hola de revisión [biblioteca de administración de Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="90892-190">Review hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
