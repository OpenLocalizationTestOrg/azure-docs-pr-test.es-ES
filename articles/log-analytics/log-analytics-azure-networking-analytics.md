---
title: "Solución Azure Networking Analytics de Log Analytics | Microsoft Docs"
description: "Puede usar la solución Azure Networking Analytics en Log Analytics para revisar los registros de los grupos de seguridad de red de Azure y los registros de Azure Application Gateway."
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
ms.openlocfilehash: 06b67322b3812a668a515ecc357171ede1d85441
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="3caa9-103">Soluciones de supervisión de redes de Azure en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3caa9-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="3caa9-104">Log Analytics ofrece las siguientes soluciones para supervisar las redes:</span><span class="sxs-lookup"><span data-stu-id="3caa9-104">Log Analytics offers the following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="3caa9-105">Monitor de rendimiento de red (NPM)</span><span class="sxs-lookup"><span data-stu-id="3caa9-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="3caa9-106">Supervisión del mantenimiento de la red</span><span class="sxs-lookup"><span data-stu-id="3caa9-106">Monitor the health of your network</span></span>
* <span data-ttu-id="3caa9-107">Azure Application Gateway Analytics para revisar</span><span class="sxs-lookup"><span data-stu-id="3caa9-107">Azure Application Gateway analytics to review</span></span>
 * <span data-ttu-id="3caa9-108">Registros de Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="3caa9-109">Métricas de Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="3caa9-110">Azure Network Security Group Analytics para revisar</span><span class="sxs-lookup"><span data-stu-id="3caa9-110">Azure Network Security Group analytics to review</span></span>
 * <span data-ttu-id="3caa9-111">Registros de Azure Network Security Group</span><span class="sxs-lookup"><span data-stu-id="3caa9-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="3caa9-112">Network Performance Monitor (NPM) (monitor de rendimiento de red)</span><span class="sxs-lookup"><span data-stu-id="3caa9-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="3caa9-113">La Solución de administración [Network Performance Monitor](log-analytics-network-performance-monitor.md) supervisa el mantenimiento, la disponibilidad y accesibilidad de las redes.</span><span class="sxs-lookup"><span data-stu-id="3caa9-113">The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.</span></span>  <span data-ttu-id="3caa9-114">Se utiliza para supervisar la conectividad entre:</span><span class="sxs-lookup"><span data-stu-id="3caa9-114">It is used to monitor connectivity between:</span></span>

* <span data-ttu-id="3caa9-115">Nube pública y entorno local</span><span class="sxs-lookup"><span data-stu-id="3caa9-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="3caa9-116">Centros de datos y ubicaciones de usuario (sucursales)</span><span class="sxs-lookup"><span data-stu-id="3caa9-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="3caa9-117">Subredes que hospedan distintos niveles de una aplicación de varios niveles.</span><span class="sxs-lookup"><span data-stu-id="3caa9-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="3caa9-118">Para más información consulte [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="3caa9-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="3caa9-119">Azure Application Gateway y Network Security Group Analytics</span><span class="sxs-lookup"><span data-stu-id="3caa9-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="3caa9-120">Para usar las soluciones:</span><span class="sxs-lookup"><span data-stu-id="3caa9-120">To use the solutions:</span></span>
1. <span data-ttu-id="3caa9-121">Agregue la Solución de administración a Log Analytics y</span><span class="sxs-lookup"><span data-stu-id="3caa9-121">Add the management solution to Log Analytics, and</span></span>
2. <span data-ttu-id="3caa9-122">Habilite los diagnósticos para que se dirijan a un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3caa9-122">Enable diagnostics to direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="3caa9-123">No se requiere escribir los registros en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3caa9-123">It is not necessary to write the logs to Azure Blob storage.</span></span>

<span data-ttu-id="3caa9-124">Puede habilitar los diagnósticos y la solución correspondiente solo para Application Gateway, solo para Networking Security Groups o para ambas.</span><span class="sxs-lookup"><span data-stu-id="3caa9-124">You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="3caa9-125">Si no habilita el registro de diagnósticos para un tipo de recurso en particular, pero instala la solución, las hojas de panel para ese recurso estarán en blanco y mostrarán un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="3caa9-125">If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="3caa9-126">En enero de 2017, cambia la forma de enviar registros de Application Gateway y Network Security Group a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3caa9-126">In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="3caa9-127">Si consulta la solución **Azure Networking Analytics (en desuso)**, remítase a la sección [Migración desde la solución Networking Analytics antigua ](#migrating-from-the-old-networking-analytics-solution) para conocer los pasos que debe seguir.</span><span class="sxs-lookup"><span data-stu-id="3caa9-127">If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="3caa9-128">Revisión de los detalles de recopilación de datos de redes de Azure</span><span class="sxs-lookup"><span data-stu-id="3caa9-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="3caa9-129">Las soluciones de administración Azure Application Gateway Analytics y Network Security Group Analytics recopilan registros de diagnósticos directamente de Azure Application Gateways y Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="3caa9-129">The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="3caa9-130">No es necesario escribir los registros en Azure Blob Storage y no se requiere ningún agente para la recopilación de datos.</span><span class="sxs-lookup"><span data-stu-id="3caa9-130">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="3caa9-131">En la siguiente tabla se muestran los métodos de recopilación de datos y otros detalles sobre cómo se reúnen los datos análisis de Azure Application Gateway y Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="3caa9-131">The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.</span></span>

| <span data-ttu-id="3caa9-132">Plataforma</span><span class="sxs-lookup"><span data-stu-id="3caa9-132">Platform</span></span> | <span data-ttu-id="3caa9-133">Agente directo</span><span class="sxs-lookup"><span data-stu-id="3caa9-133">Direct agent</span></span> | <span data-ttu-id="3caa9-134">Agente System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3caa9-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="3caa9-135">Azure</span><span class="sxs-lookup"><span data-stu-id="3caa9-135">Azure</span></span> | <span data-ttu-id="3caa9-136">¿Se requiere Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="3caa9-136">Operations Manager required?</span></span> | <span data-ttu-id="3caa9-137">Se envían los datos del agente de Operations Manager a través del grupo de administración</span><span class="sxs-lookup"><span data-stu-id="3caa9-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="3caa9-138">Frecuencia de recopilación</span><span class="sxs-lookup"><span data-stu-id="3caa9-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3caa9-139">Azure</span><span class="sxs-lookup"><span data-stu-id="3caa9-139">Azure</span></span> |  |  |<span data-ttu-id="3caa9-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="3caa9-140">&#8226;</span></span> |  |  |<span data-ttu-id="3caa9-141">Cuando se inicia sesión</span><span class="sxs-lookup"><span data-stu-id="3caa9-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="3caa9-142">Solución Azure Application Gateway Analytics de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3caa9-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Símbolo de Azure Application Gateway Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="3caa9-144">Para Application Gateway se admiten los siguientes registros:</span><span class="sxs-lookup"><span data-stu-id="3caa9-144">The following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="3caa9-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="3caa9-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="3caa9-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="3caa9-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="3caa9-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="3caa9-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="3caa9-148">Las métricas siguientes son compatibles con Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="3caa9-148">The following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="3caa9-149">Rendimiento de 5 minutos</span><span class="sxs-lookup"><span data-stu-id="3caa9-149">5 minute throughput</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="3caa9-150">Instalación y configuración de la solución</span><span class="sxs-lookup"><span data-stu-id="3caa9-150">Install and configure the solution</span></span>
<span data-ttu-id="3caa9-151">Para instalar y configurar la solución Azure Application Gateway, siga estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="3caa9-151">Use the following instructions to install and configure the Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="3caa9-152">Habilite la solución Azure Application Gateway Analytics desde [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) o mediante el proceso descrito en el artículo sobre[ incorporación de soluciones de Log Analytics desde la Galería de soluciones](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3caa9-152">Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="3caa9-153">Habilite el registro de diagnósticos para las [Application Gateway](../application-gateway/application-gateway-diagnostics.md) que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="3caa9-153">Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-the-portal"></a><span data-ttu-id="3caa9-154">Habilitación de los diagnósticos de Azure Application Gateway en el portal</span><span class="sxs-lookup"><span data-stu-id="3caa9-154">Enable Azure Application Gateway diagnostics in the portal</span></span>

1. <span data-ttu-id="3caa9-155">En Azure Portal, navegue hasta el recurso de Application Gateway que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="3caa9-155">In the Azure portal, navigate to the Application Gateway resource to monitor</span></span>
2. <span data-ttu-id="3caa9-156">Seleccione *Registros de diagnósticos* para abrir la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="3caa9-156">Select *Diagnostics logs* to open the following page</span></span>

   ![imagen del recurso de Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="3caa9-158">Haga clic en *Activar diagnósticos* para abrir la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="3caa9-158">Click *Turn on diagnostics* to open the following page</span></span>

   ![imagen del recurso de Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="3caa9-160">Para activar los diagnósticos, haga clic en *Activar* en *Estado*.</span><span class="sxs-lookup"><span data-stu-id="3caa9-160">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="3caa9-161">Haga clic en la casilla *Send to Log Analytics* (Enviar a Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="3caa9-161">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="3caa9-162">Seleccione un área de trabajo de Log Analytics existente o cree un área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3caa9-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="3caa9-163">En **Registro**, haga clic en la casilla correspondiente a cada uno de los tipos de registro para recopilar.</span><span class="sxs-lookup"><span data-stu-id="3caa9-163">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="3caa9-164">Haga clic en *Guardar* para habilitar el registro de diagnósticos en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3caa9-164">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="3caa9-165">Habilitación de los diagnósticos de red de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3caa9-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="3caa9-166">El siguiente script de PowerShell proporciona un ejemplo de cómo habilitar el registro de diagnósticos puertas de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3caa9-166">The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="3caa9-167">Uso de análisis de Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-167">Use Azure Application Gateway analytics</span></span>
![imagen del icono de análisis de Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="3caa9-169">Tras hacer clic en el icono **Azure Application Gateway analytics** (Análisis de Azure Application Gateway) en Overview (Información general), puede ver resúmenes de los registros y desplazarse hasta los detalles de las categorías siguientes:</span><span class="sxs-lookup"><span data-stu-id="3caa9-169">After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="3caa9-170">Registros de acceso de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="3caa9-171">Errores de cliente y servidor de los registros de acceso de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="3caa9-172">Solicitudes por hora para cada Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="3caa9-173">Solicitudes fallidas por hora para cada Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="3caa9-174">Errores por agente de usuario de las puertas de enlace de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3caa9-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="3caa9-175">Rendimiento de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-175">Application Gateway performance</span></span>
  * <span data-ttu-id="3caa9-176">Estado de host de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="3caa9-177">Percentil 95 y máximo para las solicitudes fallidas de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3caa9-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![imagen del panel de análisis de Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![imagen del panel de análisis de Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="3caa9-180">En el panel **Azure Application Gateway analytics** (Análisis de Azure Application Gateway), revise la información de resumen en una de las hojas y haga clic en una para obtener información detallada sobre la página de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="3caa9-180">On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="3caa9-181">En cualquiera de las páginas de búsqueda de registros, puede ver los resultados por tiempo, resultados detallados y el historial de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="3caa9-181">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="3caa9-182">También puede filtrar por las facetas para restringir los resultados.</span><span class="sxs-lookup"><span data-stu-id="3caa9-182">You can also filter by facets to narrow the results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="3caa9-183">Solución Azure Network Security Group Analytics de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3caa9-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Símbolo de Azure Network Security Group Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="3caa9-185">Para los grupos de seguridad de red se admiten los siguientes registros:</span><span class="sxs-lookup"><span data-stu-id="3caa9-185">The following logs are supported for network security groups:</span></span>

* <span data-ttu-id="3caa9-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="3caa9-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="3caa9-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="3caa9-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="3caa9-188">Instalación y configuración de la solución</span><span class="sxs-lookup"><span data-stu-id="3caa9-188">Install and configure the solution</span></span>
<span data-ttu-id="3caa9-189">Para instalar y configurar la solución Azure Networking Analytics, siga estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="3caa9-189">Use the following instructions to install and configure the Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="3caa9-190">Habilite la solución Azure Network Security Group Analytics desde [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) o mediante el proceso descrito en el artículo sobre[ incorporación de soluciones de Log Analytics desde la Galería de soluciones](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3caa9-190">Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="3caa9-191">Habilite el registro de diagnósticos para los recursos de [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="3caa9-191">Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-the-portal"></a><span data-ttu-id="3caa9-192">Habilitación de los diagnósticos de Azure Network Security Group en el portal</span><span class="sxs-lookup"><span data-stu-id="3caa9-192">Enable Azure network security group diagnostics in the portal</span></span>

1. <span data-ttu-id="3caa9-193">En Azure Portal, navegue hasta el recurso Grupo de seguridad de red que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="3caa9-193">In the Azure portal, navigate to the Network Security Group resource to monitor</span></span>
2. <span data-ttu-id="3caa9-194">Seleccione *Registros de diagnósticos* para abrir la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="3caa9-194">Select *Diagnostics logs* to open the following page</span></span>

   ![imagen del recurso Grupo de seguridad de red de Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="3caa9-196">Haga clic en *Activar diagnósticos* para abrir la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="3caa9-196">Click *Turn on diagnostics* to open the following page</span></span>

   ![imagen del recurso Grupo de seguridad de red de Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="3caa9-198">Para activar los diagnósticos, haga clic en *Activar* en *Estado*.</span><span class="sxs-lookup"><span data-stu-id="3caa9-198">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="3caa9-199">Haga clic en la casilla *Send to Log Analytics* (Enviar a Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="3caa9-199">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="3caa9-200">Seleccione un área de trabajo de Log Analytics existente o cree un área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3caa9-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="3caa9-201">En **Registro**, haga clic en la casilla correspondiente a cada uno de los tipos de registro para recopilar.</span><span class="sxs-lookup"><span data-stu-id="3caa9-201">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="3caa9-202">Haga clic en *Guardar* para habilitar el registro de diagnósticos en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3caa9-202">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="3caa9-203">Habilitación de los diagnósticos de red de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3caa9-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="3caa9-204">El siguiente script de PowerShell proporciona un ejemplo de cómo habilitar el registro de diagnósticos para grupos de seguridad de red:</span><span class="sxs-lookup"><span data-stu-id="3caa9-204">The following PowerShell script provides an example of how to enable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="3caa9-205">Uso de Azure Network Security Group Analytics</span><span class="sxs-lookup"><span data-stu-id="3caa9-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="3caa9-206">Tras hacer clic en el icono **Azure Network Security Group Analytics** en Overview (Información general), puede ver resúmenes de los registros y desplazarse hasta los detalles de las categorías siguientes:</span><span class="sxs-lookup"><span data-stu-id="3caa9-206">After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="3caa9-207">Flujos bloqueados de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="3caa9-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="3caa9-208">Reglas de los grupos de seguridad de red con flujos bloqueados</span><span class="sxs-lookup"><span data-stu-id="3caa9-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="3caa9-209">Direcciones MAC con flujos bloqueados</span><span class="sxs-lookup"><span data-stu-id="3caa9-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="3caa9-210">Flujos permitidos en los grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="3caa9-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="3caa9-211">Reglas de los grupos de seguridad de red con flujos permitidos</span><span class="sxs-lookup"><span data-stu-id="3caa9-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="3caa9-212">Direcciones MAC con flujos permitidos</span><span class="sxs-lookup"><span data-stu-id="3caa9-212">MAC addresses with allowed flows</span></span>

![imagen del panel Azure Network Security Group Analytics](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![imagen del panel Azure Network Security Group Analytics](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="3caa9-215">En el panel **Azure Network Security Group Analytics**, revise la información de resumen en una de las hojas y haga clic en una para obtener información detallada sobre la página de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="3caa9-215">On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="3caa9-216">En cualquiera de las páginas de búsqueda de registros, puede ver los resultados por tiempo, resultados detallados y el historial de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="3caa9-216">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="3caa9-217">También puede filtrar por las facetas para restringir los resultados.</span><span class="sxs-lookup"><span data-stu-id="3caa9-217">You can also filter by facets to narrow the results.</span></span>

## <a name="migrating-from-the-old-networking-analytics-solution"></a><span data-ttu-id="3caa9-218">Migración desde la solución Networking Analytics antigua</span><span class="sxs-lookup"><span data-stu-id="3caa9-218">Migrating from the old Networking Analytics solution</span></span>
<span data-ttu-id="3caa9-219">En enero de 2017, cambia la forma de enviar registros de Azure Application Gateway y Azure Network Security Group a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3caa9-219">In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="3caa9-220">Estos cambios proporcionan las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3caa9-220">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="3caa9-221">Los registros se escriben directamente en Log Analytics sin necesidad de usar una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3caa9-221">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="3caa9-222">Menor latencia desde el momento en el que los registros se generan hasta que están disponibles en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3caa9-222">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="3caa9-223">Menos pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="3caa9-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="3caa9-224">Un formato común para todos los tipos de diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="3caa9-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="3caa9-225">Para usar las soluciones actualizadas:</span><span class="sxs-lookup"><span data-stu-id="3caa9-225">To use the updated solutions:</span></span>

1. <span data-ttu-id="3caa9-226">[Configure los diagnósticos que se van a enviar directamente a Log Analytics desde Azure Application Gateway](#enable-azure-application-gateway-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="3caa9-226">[Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways](#enable-azure-application-gateway-diagnostics-in-the-portal)</span></span>
2. <span data-ttu-id="3caa9-227">[Configure los diagnósticos que se van a enviar directamente a Log Analytics desde Azure Network Security Group](#enable-azure-network-security-group-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="3caa9-227">[Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups](#enable-azure-network-security-group-diagnostics-in-the-portal)</span></span>
2. <span data-ttu-id="3caa9-228">Habilite la solución *Azure Application Gateway Analytics* y *Azure Network Security Group Analytics* mediante el proceso que se describe en [Incorporación de soluciones de administración de Log Analytics](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3caa9-228">Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="3caa9-229">Actualice cualquier consulta guardada, panel o alerta para usar el nuevo tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="3caa9-229">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="3caa9-230">El tipo es AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="3caa9-230">Type is to AzureDiagnostics.</span></span> <span data-ttu-id="3caa9-231">Puede usar ResourceType para filtrar registros de redes de Azure.</span><span class="sxs-lookup"><span data-stu-id="3caa9-231">You can use the ResourceType to filter to Azure networking logs.</span></span>

    | <span data-ttu-id="3caa9-232">En lugar de:</span><span class="sxs-lookup"><span data-stu-id="3caa9-232">Instead of:</span></span> | <span data-ttu-id="3caa9-233">Uso:</span><span class="sxs-lookup"><span data-stu-id="3caa9-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="3caa9-234">Para todos los campos que tengan un sufijo \_s, \_d o \_g en el nombre, cambie el primer carácter a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3caa9-234">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
   + <span data-ttu-id="3caa9-235">Para todos los campos que tengan un sufijo \_o en el nombre, los datos se dividen en campos individuales según los nombres de campo anidados.</span><span class="sxs-lookup"><span data-stu-id="3caa9-235">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span>
4. <span data-ttu-id="3caa9-236">Quite la solución *Azure Networking Analytics (en desuso)*.</span><span class="sxs-lookup"><span data-stu-id="3caa9-236">Remove the *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="3caa9-237">Si usa PowerShell, utilice `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`.</span><span class="sxs-lookup"><span data-stu-id="3caa9-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="3caa9-238">Los datos recopilados antes del cambio no aparecen en la nueva solución.</span><span class="sxs-lookup"><span data-stu-id="3caa9-238">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="3caa9-239">Puede seguir consultando estos datos con el tipo y los nombres de campo anteriores.</span><span class="sxs-lookup"><span data-stu-id="3caa9-239">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3caa9-240">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="3caa9-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="3caa9-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3caa9-241">Next steps</span></span>
* <span data-ttu-id="3caa9-242">Use [Búsquedas de registros en Log Analytics](log-analytics-log-searches.md) para ver datos detallados sobre los diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3caa9-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.</span></span>
