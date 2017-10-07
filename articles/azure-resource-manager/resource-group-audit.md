---
title: aaaView actividad de Azure registra recursos toomonitor | Documentos de Microsoft
description: Actividad de uso hello registra errores y las acciones del usuario tooreview. Muestra PowerShell del Portal de Azure, CLI de Azure CLI y REST.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="76405-104">Ver la actividad registra acciones de tooaudit en recursos</span><span class="sxs-lookup"><span data-stu-id="76405-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="76405-105">Mediante los registros de actividad, puede determinar:</span><span class="sxs-lookup"><span data-stu-id="76405-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="76405-106">las operaciones que se realizaron en los recursos de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="76405-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="76405-107">quién inició la operación de hello (aunque las operaciones iniciadas por un servicio back-end no devuelven un usuario como autor de llamada de hello)</span><span class="sxs-lookup"><span data-stu-id="76405-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="76405-108">Cuando se ha producido la operación de Hola</span><span class="sxs-lookup"><span data-stu-id="76405-108">when hello operation occurred</span></span>
* <span data-ttu-id="76405-109">estado de Hola de operación de Hola</span><span class="sxs-lookup"><span data-stu-id="76405-109">hello status of hello operation</span></span>
* <span data-ttu-id="76405-110">valores de Hello de otras propiedades que pueden ayudarle a investigación operación Hola</span><span class="sxs-lookup"><span data-stu-id="76405-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="76405-111">Puede recuperar información de los registros de actividad de Hola a través del portal de hello, PowerShell, CLI de Azure, API de REST de visión, o [biblioteca .NET de visión](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="76405-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="76405-112">Portal</span><span class="sxs-lookup"><span data-stu-id="76405-112">Portal</span></span>
1. <span data-ttu-id="76405-113">registros de actividad de hello tooview a través del portal de hello, seleccione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="76405-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![seleccionar registro de actividad](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="76405-115">O bien, tooautomatically filtrar el registro de actividad de Hola para un determinado recurso o grupo de recursos, seleccione **registro de actividad** de esa hoja de recursos.</span><span class="sxs-lookup"><span data-stu-id="76405-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="76405-116">Tenga en cuenta que este registro de actividad de Hola se filtra automáticamente por recurso Hola seleccionado.</span><span class="sxs-lookup"><span data-stu-id="76405-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![filtrar por recurso](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="76405-118">Hola **registro de actividad** hoja, verá un resumen de las operaciones recientes.</span><span class="sxs-lookup"><span data-stu-id="76405-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![mostrar acciones](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="76405-120">número de hello toorestrict de operaciones que se muestra, seleccione las distintas condiciones.</span><span class="sxs-lookup"><span data-stu-id="76405-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="76405-121">Por ejemplo, hello siguiente imagen muestra hello **Timespan** y **evento iniciado por** campos cambiaron las acciones de hello tooview realizadas por un usuario determinado o una aplicación para hello mes pasado.</span><span class="sxs-lookup"><span data-stu-id="76405-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="76405-122">Seleccione **aplicar** tooview resultados de saludo de la consulta.</span><span class="sxs-lookup"><span data-stu-id="76405-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![establecer opciones de filtro](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="76405-124">Si necesita toorun consulta de Hola de nuevo más tarde, seleccione **guardar** y asigne un nombre de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="76405-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![guardar consulta](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="76405-126">tooquickly al ejecutar una consulta, puede seleccionar uno de consultas integradas de hello, como implementaciones con error.</span><span class="sxs-lookup"><span data-stu-id="76405-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![seleccionar consulta](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="76405-128">consulta seleccionada Hola establece automáticamente los valores de filtro de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="76405-128">hello selected query automatically sets hello required filter values.</span></span>

    ![ver errores de implementación](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="76405-130">Seleccione uno de hello operaciones toosee un resumen del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="76405-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![ver operación](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="76405-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="76405-132">PowerShell</span></span>
1. <span data-ttu-id="76405-133">entradas del registro tooretrieve, ejecute hello **Get AzureRmLog** comando.</span><span class="sxs-lookup"><span data-stu-id="76405-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="76405-134">Proporcionar la lista de parámetros adicionales toofilter Hola de entradas.</span><span class="sxs-lookup"><span data-stu-id="76405-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="76405-135">Si no especifica una hora inicial y final, se devuelven las entradas de hello última hora.</span><span class="sxs-lookup"><span data-stu-id="76405-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="76405-136">Por ejemplo, las operaciones de Hola de tooretrieve de un grupo de recursos durante la última hora de hello ejecutan:</span><span class="sxs-lookup"><span data-stu-id="76405-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="76405-137">Hola de ejemplo siguiente muestra cómo actividad de hello toouse registro operaciones tooresearch realizadas durante un tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="76405-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="76405-138">Hola se especifican las fechas de inicio y finalización en un formato de fecha.</span><span class="sxs-lookup"><span data-stu-id="76405-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="76405-139">O bien, puede usar funciones toospecify Hola fecha intervalo de fechas, como Hola últimos 14 días.</span><span class="sxs-lookup"><span data-stu-id="76405-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="76405-140">Según la hora de inicio de Hola que especifique, comandos anteriores Hola pueden devolver una lista larga de operaciones para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="76405-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="76405-141">Puede filtrar los resultados de Hola para lo está buscando al proporcionar criterios de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="76405-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="76405-142">Por ejemplo, si está tratando de tooresearch cómo una aplicación web se detiene, podría ejecutar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76405-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="76405-143">En este ejemplo se muestra que someone@contoso.com ha realizado una acción de detención.</span><span class="sxs-lookup"><span data-stu-id="76405-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="76405-144">Puede buscar las acciones de hello realizadas por un usuario determinado, incluso para un grupo de recursos que ya no existe.</span><span class="sxs-lookup"><span data-stu-id="76405-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="76405-145">Puede filtrar por las operaciones con errores.</span><span class="sxs-lookup"><span data-stu-id="76405-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="76405-146">Se puede concentrar en un error examinando el mensaje de estado de Hola para esa entrada.</span><span class="sxs-lookup"><span data-stu-id="76405-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="76405-147">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="76405-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="76405-148">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="76405-148">Azure CLI</span></span>
* <span data-ttu-id="76405-149">las entradas del registro tooretrieve ejecutar hello **mostrar de registro del grupo de azure** comando.</span><span class="sxs-lookup"><span data-stu-id="76405-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="76405-150">API de REST</span><span class="sxs-lookup"><span data-stu-id="76405-150">REST API</span></span>
<span data-ttu-id="76405-151">operaciones de REST de Hola para trabajar con el registro de actividad de hello forman parte del programa Hola a [API de REST de visión](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="76405-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="76405-152">eventos de registro de actividad de tooretrieve, consulte [lista de los eventos de administración de hello en una suscripción](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="76405-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="76405-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76405-153">Next steps</span></span>
* <span data-ttu-id="76405-154">Registros de actividad de Azure pueden utilizarse con Power BI toogain mayor información útil sobre las acciones de hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="76405-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="76405-155">Consulte [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)(Consulta y análisis de registros de auditoría de Azure en Power BI y más).</span><span class="sxs-lookup"><span data-stu-id="76405-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="76405-156">toolearn acerca de cómo establecer directivas de seguridad, consulte [el Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="76405-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="76405-157">toolearn acerca de los comandos de Hola para ver las operaciones de implementación, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="76405-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="76405-158">toolearn tooprevent eliminaciones en un recurso para todos los usuarios, vea [bloquear los recursos con el Administrador de recursos de Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="76405-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

