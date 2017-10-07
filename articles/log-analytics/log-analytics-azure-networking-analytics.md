---
title: "solución de análisis de red en el análisis de registros aaaAzure | Documentos de Microsoft"
description: "Puede usar Hola soluciones de análisis de redes de Azure en registros de puerta de enlace de aplicaciones de Azure y análisis de registros tooreview registros de grupo de seguridad de red de Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="bde4b-103">Soluciones de supervisión de redes de Azure en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="bde4b-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="bde4b-104">Análisis de registros ofrecen Hola siguientes soluciones para supervisar las redes:</span><span class="sxs-lookup"><span data-stu-id="bde4b-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="bde4b-105">Monitor de rendimiento de red (NPM)</span><span class="sxs-lookup"><span data-stu-id="bde4b-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="bde4b-106">Supervisar el estado de saludo de la red</span><span class="sxs-lookup"><span data-stu-id="bde4b-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="bde4b-107">Azure tooreview de análisis de puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="bde4b-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="bde4b-108">Registros de Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="bde4b-109">Métricas de Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="bde4b-110">Tooreview de análisis del grupo de seguridad de red de Azure</span><span class="sxs-lookup"><span data-stu-id="bde4b-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="bde4b-111">Registros de Azure Network Security Group</span><span class="sxs-lookup"><span data-stu-id="bde4b-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="bde4b-112">Network Performance Monitor (NPM) (monitor de rendimiento de red)</span><span class="sxs-lookup"><span data-stu-id="bde4b-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="bde4b-113">Hola [Monitor de rendimiento de red](log-analytics-network-performance-monitor.md) solución de administración es una solución, que supervisa la disponibilidad de redes, la disponibilidad y el estado de Hola de supervisión de red.</span><span class="sxs-lookup"><span data-stu-id="bde4b-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="bde4b-114">Es utilizado toomonitor conectividad entre:</span><span class="sxs-lookup"><span data-stu-id="bde4b-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="bde4b-115">Nube pública y entorno local</span><span class="sxs-lookup"><span data-stu-id="bde4b-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="bde4b-116">Centros de datos y ubicaciones de usuario (sucursales)</span><span class="sxs-lookup"><span data-stu-id="bde4b-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="bde4b-117">Subredes que hospedan distintos niveles de una aplicación de varios niveles.</span><span class="sxs-lookup"><span data-stu-id="bde4b-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="bde4b-118">Para más información consulte [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="bde4b-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="bde4b-119">Azure Application Gateway y Network Security Group Analytics</span><span class="sxs-lookup"><span data-stu-id="bde4b-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="bde4b-120">soluciones de Hola toouse:</span><span class="sxs-lookup"><span data-stu-id="bde4b-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="bde4b-121">Agregar tooLog de solución de administración de hello análisis, y</span><span class="sxs-lookup"><span data-stu-id="bde4b-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="bde4b-122">Habilitar el área de trabajo de diagnóstico toodirect Hola diagnósticos tooa análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="bde4b-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="bde4b-123">No es necesario toowrite Hola registros tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="bde4b-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="bde4b-124">Puede habilitar el diagnóstico y solución de hello correspondientes para uno o ambos de los grupos de seguridad de red y puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bde4b-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="bde4b-125">Si no habilita el registro de diagnóstico para un tipo de recurso determinado, pero instalar soluciones de hello, hojas de panel de Hola para ese recurso están en blanco y mostrar un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="bde4b-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="bde4b-126">En enero de 2017 Hola admite manera de enviar registros de puertas de enlace de aplicaciones y grupos de seguridad de red tooLog cambiado de análisis.</span><span class="sxs-lookup"><span data-stu-id="bde4b-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="bde4b-127">Si ve hello **el análisis de redes de Azure (en desuso)** solución, consulte demasiado[migrar desde soluciones de análisis de red antiguo hello](#migrating-from-the-old-networking-analytics-solution) para conocer los pasos necesita toofollow.</span><span class="sxs-lookup"><span data-stu-id="bde4b-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="bde4b-128">Revisión de los detalles de recopilación de datos de redes de Azure</span><span class="sxs-lookup"><span data-stu-id="bde4b-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="bde4b-129">análisis de la puerta de enlace de aplicaciones de Azure de Hola y soluciones de administración de análisis de grupo de seguridad de red de hello recopilan registros de diagnósticos directamente desde las puertas de enlace de aplicaciones de Azure y los grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="bde4b-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="bde4b-130">No es necesario toowrite Hola registros tooAzure almacenamiento de blobs y no hay ningún agente es necesario para la recopilación de datos.</span><span class="sxs-lookup"><span data-stu-id="bde4b-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="bde4b-131">Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos para el análisis de la puerta de enlace de aplicaciones de Azure y análisis del grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="bde4b-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="bde4b-132">Plataforma</span><span class="sxs-lookup"><span data-stu-id="bde4b-132">Platform</span></span> | <span data-ttu-id="bde4b-133">Agente directo</span><span class="sxs-lookup"><span data-stu-id="bde4b-133">Direct agent</span></span> | <span data-ttu-id="bde4b-134">Agente System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="bde4b-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="bde4b-135">Azure</span><span class="sxs-lookup"><span data-stu-id="bde4b-135">Azure</span></span> | <span data-ttu-id="bde4b-136">¿Se requiere Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="bde4b-136">Operations Manager required?</span></span> | <span data-ttu-id="bde4b-137">Se envían los datos del agente de Operations Manager a través del grupo de administración</span><span class="sxs-lookup"><span data-stu-id="bde4b-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="bde4b-138">Frecuencia de recopilación</span><span class="sxs-lookup"><span data-stu-id="bde4b-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="bde4b-139">Azure</span><span class="sxs-lookup"><span data-stu-id="bde4b-139">Azure</span></span> |  |  |<span data-ttu-id="bde4b-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="bde4b-140">&#8226;</span></span> |  |  |<span data-ttu-id="bde4b-141">Cuando se inicia sesión</span><span class="sxs-lookup"><span data-stu-id="bde4b-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="bde4b-142">Solución Azure Application Gateway Analytics de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="bde4b-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Símbolo de Azure Application Gateway Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="bde4b-144">Hola siguiendo los registros es compatibles con las puertas de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="bde4b-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="bde4b-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="bde4b-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="bde4b-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="bde4b-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="bde4b-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="bde4b-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="bde4b-148">Hola siguiendo las métricas se admite para las puertas de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="bde4b-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="bde4b-149">Rendimiento de 5 minutos</span><span class="sxs-lookup"><span data-stu-id="bde4b-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="bde4b-150">Instalar y configurar soluciones de Hola</span><span class="sxs-lookup"><span data-stu-id="bde4b-150">Install and configure hello solution</span></span>
<span data-ttu-id="bde4b-151">Usar hello siguiendo las instrucciones tooinstall y configurar soluciones de análisis de hello puerta de enlace de aplicaciones de Azure:</span><span class="sxs-lookup"><span data-stu-id="bde4b-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="bde4b-152">Habilitar la solución de análisis de puerta de enlace de aplicaciones de Azure Hola de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="bde4b-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="bde4b-153">Habilitar el registro de diagnóstico para hello [las puertas de enlace de la aplicación](../application-gateway/application-gateway-diagnostics.md) desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="bde4b-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="bde4b-154">Habilitar los diagnósticos de puerta de enlace de aplicaciones de Azure en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="bde4b-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="bde4b-155">Hola portal de Azure, navegue toohello Application Gateway recursos toomonitor</span><span class="sxs-lookup"><span data-stu-id="bde4b-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="bde4b-156">Seleccione *registros de diagnóstico* hello tooopen después de la página</span><span class="sxs-lookup"><span data-stu-id="bde4b-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![imagen del recurso de Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="bde4b-158">Haga clic en *Activar diagnósticos* hello tooopen después de la página</span><span class="sxs-lookup"><span data-stu-id="bde4b-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![imagen del recurso de Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="bde4b-160">tooturn en diagnóstico, haga clic en *en* en *estado*</span><span class="sxs-lookup"><span data-stu-id="bde4b-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="bde4b-161">Haga clic en la casilla de verificación de Hola para *enviar tooLog análisis*</span><span class="sxs-lookup"><span data-stu-id="bde4b-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="bde4b-162">Seleccione un área de trabajo de Log Analytics existente o cree un área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bde4b-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="bde4b-163">Haga clic en la casilla de hello en **registro** para cada uno de toocollect de tipos de registro de hello</span><span class="sxs-lookup"><span data-stu-id="bde4b-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="bde4b-164">Haga clic en *guardar* registro de hello tooenable de diagnóstico tooLog análisis</span><span class="sxs-lookup"><span data-stu-id="bde4b-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="bde4b-165">Habilitación de los diagnósticos de red de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bde4b-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="bde4b-166">Hola siguiente script de PowerShell ofrece un ejemplo de cómo tooenable registro de diagnóstico para las puertas de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bde4b-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="bde4b-167">Uso de análisis de Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-167">Use Azure Application Gateway analytics</span></span>
![imagen del icono de análisis de Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="bde4b-169">Tras hacer clic en hello **análisis de puerta de enlace de aplicaciones de Azure** icono en hello información general, puede ver resúmenes de los registros y, a continuación, profundizar en toodetails para hello siguientes categorías:</span><span class="sxs-lookup"><span data-stu-id="bde4b-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="bde4b-170">Registros de acceso de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="bde4b-171">Errores de cliente y servidor de los registros de acceso de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="bde4b-172">Solicitudes por hora para cada Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="bde4b-173">Solicitudes fallidas por hora para cada Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="bde4b-174">Errores por agente de usuario de las puertas de enlace de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="bde4b-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="bde4b-175">Rendimiento de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-175">Application Gateway performance</span></span>
  * <span data-ttu-id="bde4b-176">Estado de host de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="bde4b-177">Percentil 95 y máximo para las solicitudes fallidas de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="bde4b-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![imagen del panel de análisis de Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![imagen del panel de análisis de Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="bde4b-180">En hello **análisis de puerta de enlace de aplicaciones de Azure** panel, revise la información de resumen de Hola de uno de los módulos de hello y, a continuación, haga clic en uno tooview para obtener información acerca de la página de búsqueda de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="bde4b-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="bde4b-181">En cualquiera de las páginas de búsqueda de registro de hello, puede ver los resultados por tiempo, resultados detallados y el historial de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="bde4b-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="bde4b-182">También puede filtrar por resultados de facetas toonarrow Hola.</span><span class="sxs-lookup"><span data-stu-id="bde4b-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="bde4b-183">Solución Azure Network Security Group Analytics de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="bde4b-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Símbolo de Azure Network Security Group Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="bde4b-185">Hola siguiendo los registros es compatibles con grupos de seguridad de red:</span><span class="sxs-lookup"><span data-stu-id="bde4b-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="bde4b-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="bde4b-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="bde4b-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="bde4b-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="bde4b-188">Instalar y configurar soluciones de Hola</span><span class="sxs-lookup"><span data-stu-id="bde4b-188">Install and configure hello solution</span></span>
<span data-ttu-id="bde4b-189">Usar hello siguiendo las instrucciones tooinstall y configurar soluciones de análisis de redes de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="bde4b-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="bde4b-190">Habilitar la solución de análisis de grupo de seguridad de red de Azure Hola de [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="bde4b-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="bde4b-191">Habilitar el registro de diagnóstico para hello [grupo de seguridad de red](../virtual-network/virtual-network-nsg-manage-log.md) recursos que desee toomonitor.</span><span class="sxs-lookup"><span data-stu-id="bde4b-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="bde4b-192">Habilitar los diagnósticos de grupo de seguridad de red de Azure en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="bde4b-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="bde4b-193">Hola portal de Azure, navegue toomonitor de recurso de grupo de seguridad de red toohello</span><span class="sxs-lookup"><span data-stu-id="bde4b-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="bde4b-194">Seleccione *registros de diagnóstico* hello tooopen después de la página</span><span class="sxs-lookup"><span data-stu-id="bde4b-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![imagen del recurso Grupo de seguridad de red de Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="bde4b-196">Haga clic en *Activar diagnósticos* hello tooopen después de la página</span><span class="sxs-lookup"><span data-stu-id="bde4b-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![imagen del recurso Grupo de seguridad de red de Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="bde4b-198">tooturn en diagnóstico, haga clic en *en* en *estado*</span><span class="sxs-lookup"><span data-stu-id="bde4b-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="bde4b-199">Haga clic en la casilla de verificación de Hola para *enviar tooLog análisis*</span><span class="sxs-lookup"><span data-stu-id="bde4b-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="bde4b-200">Seleccione un área de trabajo de Log Analytics existente o cree un área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bde4b-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="bde4b-201">Haga clic en la casilla de hello en **registro** para cada uno de toocollect de tipos de registro de hello</span><span class="sxs-lookup"><span data-stu-id="bde4b-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="bde4b-202">Haga clic en *guardar* registro de hello tooenable de diagnóstico tooLog análisis</span><span class="sxs-lookup"><span data-stu-id="bde4b-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="bde4b-203">Habilitación de los diagnósticos de red de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bde4b-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="bde4b-204">Hola siguiente script de PowerShell ofrece un ejemplo de cómo tooenable registro de diagnóstico para los grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="bde4b-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="bde4b-205">Uso de Azure Network Security Group Analytics</span><span class="sxs-lookup"><span data-stu-id="bde4b-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="bde4b-206">Tras hacer clic en hello **análisis de grupo de seguridad de red de Azure** icono en hello información general, puede ver resúmenes de los registros y, a continuación, profundizar en toodetails para hello siguientes categorías:</span><span class="sxs-lookup"><span data-stu-id="bde4b-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="bde4b-207">Flujos bloqueados de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="bde4b-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="bde4b-208">Reglas de los grupos de seguridad de red con flujos bloqueados</span><span class="sxs-lookup"><span data-stu-id="bde4b-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="bde4b-209">Direcciones MAC con flujos bloqueados</span><span class="sxs-lookup"><span data-stu-id="bde4b-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="bde4b-210">Flujos permitidos en los grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="bde4b-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="bde4b-211">Reglas de los grupos de seguridad de red con flujos permitidos</span><span class="sxs-lookup"><span data-stu-id="bde4b-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="bde4b-212">Direcciones MAC con flujos permitidos</span><span class="sxs-lookup"><span data-stu-id="bde4b-212">MAC addresses with allowed flows</span></span>

![imagen del panel Azure Network Security Group Analytics](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![imagen del panel Azure Network Security Group Analytics](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="bde4b-215">En hello **análisis de grupo de seguridad de red de Azure** panel, revise la información de resumen de Hola de uno de los módulos de hello y, a continuación, haga clic en uno tooview para obtener información acerca de la página de búsqueda de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="bde4b-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="bde4b-216">En cualquiera de las páginas de búsqueda de registro de hello, puede ver los resultados por tiempo, resultados detallados y el historial de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="bde4b-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="bde4b-217">También puede filtrar por resultados de facetas toonarrow Hola.</span><span class="sxs-lookup"><span data-stu-id="bde4b-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="bde4b-218">Migración de soluciones de análisis de red antiguo Hola</span><span class="sxs-lookup"><span data-stu-id="bde4b-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="bde4b-219">En enero de 2017 Hola admite la manera de enviar registros de puertas de enlace de aplicaciones de Azure y grupos de seguridad de red de Azure tooLog cambiado de análisis.</span><span class="sxs-lookup"><span data-stu-id="bde4b-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="bde4b-220">Estos cambios proporcionan Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bde4b-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="bde4b-221">Los registros se escriben directamente tooLog análisis sin Hola necesita toouse una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bde4b-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="bde4b-222">Menor latencia de tiempo de hello cuando los registros están genera toothem está disponible en el análisis de registros</span><span class="sxs-lookup"><span data-stu-id="bde4b-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="bde4b-223">Menos pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="bde4b-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="bde4b-224">Un formato común para todos los tipos de diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="bde4b-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="bde4b-225">Hola toouse actualiza soluciones:</span><span class="sxs-lookup"><span data-stu-id="bde4b-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="bde4b-226">Configurar toobe de diagnóstico enviado tooLog análisis directamente desde las puertas de enlace de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="bde4b-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="bde4b-227">Configurar toobe de diagnóstico que se envían directamente tooLog análisis de grupos de seguridad de red de Azure</span><span class="sxs-lookup"><span data-stu-id="bde4b-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="bde4b-228">Habilitar hello *análisis de puerta de enlace de aplicaciones de Azure* hello y *análisis de grupo de seguridad de red de Azure* solución mediante Hola proceso se describe en [soluciones de análisis de registros agregar desde Hola Galería de soluciones](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="bde4b-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="bde4b-229">Actualizar cualquier consulta guardada, paneles o alertas toouse Hola nuevo tipo de datos</span><span class="sxs-lookup"><span data-stu-id="bde4b-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="bde4b-230">El tipo es tooAzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="bde4b-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="bde4b-231">Puede usar registros de red de hello ResourceType toofilter tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bde4b-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="bde4b-232">En lugar de:</span><span class="sxs-lookup"><span data-stu-id="bde4b-232">Instead of:</span></span> | <span data-ttu-id="bde4b-233">Uso:</span><span class="sxs-lookup"><span data-stu-id="bde4b-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="bde4b-234">Para cualquier campo que tenga un sufijo de \_s, \_d., o \_g en nombre de hello, cambiar Hola primer carácter toolower mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="bde4b-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="bde4b-235">Para cualquier campo que tenga un sufijo de \_o en nombre, datos de Hola se divide en campos individuales en función de los nombres de campo de hello anidado.</span><span class="sxs-lookup"><span data-stu-id="bde4b-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="bde4b-236">Quitar hello *análisis de redes de Azure (en desuso)* solución.</span><span class="sxs-lookup"><span data-stu-id="bde4b-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="bde4b-237">Si usa PowerShell, utilice `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`.</span><span class="sxs-lookup"><span data-stu-id="bde4b-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="bde4b-238">Datos recopilan antes de cambiar de hello no está visible en la nueva solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="bde4b-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="bde4b-239">Puede seguir tooquery para este uso de datos Hola tipo anterior y nombres de campo.</span><span class="sxs-lookup"><span data-stu-id="bde4b-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bde4b-240">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="bde4b-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="bde4b-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bde4b-241">Next steps</span></span>
* <span data-ttu-id="bde4b-242">Use [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de diagnóstico de Azure.</span><span class="sxs-lookup"><span data-stu-id="bde4b-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
