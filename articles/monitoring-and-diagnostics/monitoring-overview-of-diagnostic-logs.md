---
title: "aaaOverview de registros de diagnóstico de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué son los registros de diagnóstico de Azure y cómo puede usarlos toounderstand los eventos que se producen en un recurso de Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="6a938-103">Recopile y use los datos de registro provenientes de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="6a938-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="6a938-104">Qué son los registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="6a938-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="6a938-105">**Registros de diagnóstico de nivel de recurso de Azure** son registros emitidos por un recurso que proporcionan datos enriquecidos y frecuentes acerca de la operación de Hola de ese recurso.</span><span class="sxs-lookup"><span data-stu-id="6a938-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="6a938-106">contenido de Hola de estos registros varía según el tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="6a938-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="6a938-107">Por ejemplo, los contadores de regla de grupo de seguridad de red y las auditorías de Key Vault son dos categorías de registros de recursos.</span><span class="sxs-lookup"><span data-stu-id="6a938-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="6a938-108">Registros de diagnóstico de nivel de recursos se diferencian hello [registro de actividad](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="6a938-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="6a938-109">Hola registro de actividad proporciona una visión general de las operaciones de Hola que se realizaron en los recursos de la suscripción con el Administrador de recursos, por ejemplo, crear una máquina virtual o eliminar una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="6a938-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="6a938-110">Hola registro de actividad es un registro de nivel de suscripción.</span><span class="sxs-lookup"><span data-stu-id="6a938-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="6a938-111">Los registros de diagnóstico de nivel de recursos proporcionan una visión general de las operaciones realizadas dentro del mismo recurso, por ejemplo, obtener un secreto de un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a938-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="6a938-112">Los registros de diagnóstico de nivel de recursos también difieren de los registros de diagnóstico de nivel de sistema operativo invitado.</span><span class="sxs-lookup"><span data-stu-id="6a938-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="6a938-113">Estos son los recopilados por un agente que se ejecuta dentro de una máquina virtual u otro tipo de recurso admitido.</span><span class="sxs-lookup"><span data-stu-id="6a938-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="6a938-114">Registros de diagnóstico de nivel de recursos no requieren ningún dato específico del recurso de agente y capturar de hello plataforma Windows Azure, mientras que los registros de diagnóstico de nivel de sistema operativo invitado capturan datos de sistema operativo de Hola y aplicaciones que se ejecutan en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6a938-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="6a938-115">No todos los recursos admiten Hola nuevo tipo de registros de diagnóstico de recursos que se describen aquí.</span><span class="sxs-lookup"><span data-stu-id="6a938-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="6a938-116">Este artículo contiene una lista de la sección Qué tipos de recursos admiten registros de diagnóstico de nivel de recurso nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="6a938-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="6a938-117">Comparación de los registros de diagnóstico de recursos y otros tipos de registros</span><span class="sxs-lookup"><span data-stu-id="6a938-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="6a938-118">Qué se puede hacer con los registros de diagnóstico de nivel de recursos</span><span class="sxs-lookup"><span data-stu-id="6a938-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="6a938-119">Estas son algunas cosas de Hola que puede hacer con los registros de diagnóstico de recursos:</span><span class="sxs-lookup"><span data-stu-id="6a938-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![Ubicación lógica de los registros de diagnóstico de recursos](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="6a938-121">Guardarlos tooa [ **cuenta de almacenamiento** ](monitoring-archive-diagnostic-logs.md) para la inspección de auditoría o manual.</span><span class="sxs-lookup"><span data-stu-id="6a938-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="6a938-122">Puede especificar el tiempo (en días) de retención de hello mediante **configuración de diagnóstico de recurso**.</span><span class="sxs-lookup"><span data-stu-id="6a938-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="6a938-123">[Transmitirlos demasiado**centros de eventos** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) para ingesta por un servicio de otro fabricante o una solución de análisis personalizada como Power BI.</span><span class="sxs-lookup"><span data-stu-id="6a938-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="6a938-124">Analizarlos con [Log Analytics de OMS](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="6a938-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="6a938-125">Puede usar una cuenta de almacenamiento o espacio de nombres de los centros de eventos que no esté en Hola misma suscripción como Hola una emisión de registros.</span><span class="sxs-lookup"><span data-stu-id="6a938-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="6a938-126">usuario de Hola que configura los valores de hello debe tener las suscripciones tooboth de acceso correspondientes RBAC Hola.</span><span class="sxs-lookup"><span data-stu-id="6a938-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="6a938-127">Configuración de diagnóstico de recursos</span><span class="sxs-lookup"><span data-stu-id="6a938-127">Resource diagnostic settings</span></span>
<span data-ttu-id="6a938-128">Los registros de diagnóstico de recursos para recursos que no son de proceso se configuran mediante la configuración de diagnóstico de recursos.</span><span class="sxs-lookup"><span data-stu-id="6a938-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="6a938-129">**Configuración de diagnóstico de recursos** para un control de recursos:</span><span class="sxs-lookup"><span data-stu-id="6a938-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="6a938-130">Dónde se envían los registros de diagnóstico y las métricas (cuenta de almacenamiento, Event Hubs o Log Analytics de OMS).</span><span class="sxs-lookup"><span data-stu-id="6a938-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="6a938-131">Qué categorías de registro se envían y si se envían también datos de métrica.</span><span class="sxs-lookup"><span data-stu-id="6a938-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="6a938-132">Cuánto tiempo se debe conservar cada categoría de registro en una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6a938-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="6a938-133">Una retención de cero días significa que los registros se conservan de forma indefinida.</span><span class="sxs-lookup"><span data-stu-id="6a938-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="6a938-134">En caso contrario, valor de hello puede ser cualquier número de días comprendido entre 1 y 2147483647.</span><span class="sxs-lookup"><span data-stu-id="6a938-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="6a938-135">Si se han establecido directivas de retención pero almacenar los registros en una cuenta de almacenamiento está deshabilitada (por ejemplo, si solo se seleccionan las opciones de los centros de eventos o OMS), las directivas de retención de hello no tienen ningún efecto.</span><span class="sxs-lookup"><span data-stu-id="6a938-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="6a938-136">Las directivas de retención aplicada por día, por lo que en hello final de un día (UTC), los registros de día de Hola que es ahora más allá de la directiva de retención de Hola se eliminan.</span><span class="sxs-lookup"><span data-stu-id="6a938-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="6a938-137">Por ejemplo, si tuviera una directiva de retención de un día, en principio de Hola de hoy día de Hola Hola registros de hello anteayer se eliminarán.</span><span class="sxs-lookup"><span data-stu-id="6a938-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="6a938-138">Estas opciones se configuran fácilmente a través de la configuración de diagnóstico de Hola para un recurso en hello portal de Azure, a través de los comandos de PowerShell de Azure y la CLI o hello [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a938-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="6a938-139">Registros de diagnóstico y las métricas para de capa de SO invitado de Hola de uso de recursos (por ejemplo, las máquinas virtuales o Service Fabric) de proceso [un mecanismo independiente para la configuración y selección de salidas](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6a938-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="6a938-140">¿Cómo tooenable colección de registros de diagnóstico de recursos</span><span class="sxs-lookup"><span data-stu-id="6a938-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="6a938-141">Recopilación de registros de diagnóstico de recursos se puede habilitar [como parte de la creación de un recurso en una plantilla de administrador de recursos](./monitoring-enable-diagnostic-logs-using-template.md) o después de que se crea un recurso de página de ese recurso en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a938-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="6a938-142">También puede habilitar la recopilación en cualquier momento mediante comandos de Azure PowerShell o CLI o con hello API de REST de Monitor de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a938-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="6a938-143">Estas instrucciones no pueden aplicar directamente tooevery recurso.</span><span class="sxs-lookup"><span data-stu-id="6a938-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="6a938-144">Vea los vínculos de esquema de hello en parte inferior de Hola de este paso especial de toounderstand de página que se pueden aplicar a tipos de recursos de toocertain.</span><span class="sxs-lookup"><span data-stu-id="6a938-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="6a938-145">Habilitar la recopilación de registros de diagnóstico de recursos en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="6a938-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="6a938-146">Puede habilitar la recopilación de registros de diagnóstico de recursos de hello Azure portal después de que se ha creado un recurso por recurso específico tooa va o navegando tooAzure Monitor.</span><span class="sxs-lookup"><span data-stu-id="6a938-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="6a938-147">tooenable esto a través del Monitor de Azure:</span><span class="sxs-lookup"><span data-stu-id="6a938-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="6a938-148">Hola [portal de Azure](http://portal.azure.com), desplácese tooAzure Monitor y haga clic en **configuración de diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="6a938-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sección de supervisión de Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="6a938-150">Si lo desea Hola lista Filtrar por tipo de recurso o grupo de recursos, a continuación, haga clic en el recurso de hello para el que le gustaría tooset una configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="6a938-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="6a938-151">Si ninguna configuración existe en el recurso de Hola que ha seleccionado, son toocreate solicitada una configuración.</span><span class="sxs-lookup"><span data-stu-id="6a938-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="6a938-152">Haga clic en "Activar diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="6a938-152">Click "Turn on diagnostics."</span></span>

   ![Agregar configuración de diagnóstico: sin configuración actual](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="6a938-154">Si hay una configuración existente en el recurso de hello, verá una lista de configuraciones ya configurado en este recurso.</span><span class="sxs-lookup"><span data-stu-id="6a938-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="6a938-155">Haga clic en "Agregar configuración de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="6a938-155">Click "Add diagnostic setting."</span></span>

   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="6a938-157">Asigne un nombre de su configuración, Hola casillas para cada toowhich de destino que desee toosend datos y configurar el recurso que se utiliza para cada destino.</span><span class="sxs-lookup"><span data-stu-id="6a938-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="6a938-158">También puede establecer un número de días tooretain estos registros mediante el uso de hello **retención (días)** controles deslizantes (sólo aplicable toohello almacenamiento cuenta de destino).</span><span class="sxs-lookup"><span data-stu-id="6a938-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="6a938-159">Una retención de cero días almacena los registros de hello indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="6a938-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="6a938-161">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6a938-161">Click **Save**.</span></span>

<span data-ttu-id="6a938-162">Transcurridos unos instantes, Hola nueva opción aparece en la lista de valores para este recurso, y registros de diagnóstico se envían toohello especifica destinos tan pronto como los nuevos datos de evento se generan.</span><span class="sxs-lookup"><span data-stu-id="6a938-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="6a938-163">Habilitación de la recopilación de registros de diagnóstico de recursos mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a938-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="6a938-164">colección de tooenable de registros de diagnóstico de recursos a través de PowerShell de Azure, Hola de uso siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="6a938-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="6a938-165">tooenable almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="6a938-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="6a938-166">identificador de cuenta de almacenamiento de Hola Hola Id. de recurso para los registros de hello almacenamiento cuenta toowhich desea toosend Hola de.</span><span class="sxs-lookup"><span data-stu-id="6a938-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="6a938-167">tooenable transmisión por secuencias de concentrador de eventos de registros de diagnóstico tooan, use este comando:</span><span class="sxs-lookup"><span data-stu-id="6a938-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="6a938-168">Identificador de regla de bus de servicio de Hello es una cadena con este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="6a938-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="6a938-169">enviar tooenable del área de trabajo de análisis de registros de tooa registros de diagnóstico, use este comando:</span><span class="sxs-lookup"><span data-stu-id="6a938-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="6a938-170">Puede obtener Id. de recurso de Hola de su área de trabajo de análisis de registros mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6a938-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="6a938-171">Puede combinar estos parámetros tooenable varias opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="6a938-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="6a938-172">Habilitación de la recopilación de registros de diagnóstico de recursos mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="6a938-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="6a938-173">tooenable colección de registros de diagnóstico de recursos a través de hello CLI de Azure, use Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="6a938-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="6a938-174">tooenable almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="6a938-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="6a938-175">identificador de cuenta de almacenamiento de Hola Hola Id. de recurso para los registros de hello almacenamiento cuenta toowhich desea toosend Hola de.</span><span class="sxs-lookup"><span data-stu-id="6a938-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="6a938-176">tooenable transmisión por secuencias de concentrador de eventos de registros de diagnóstico tooan, use este comando:</span><span class="sxs-lookup"><span data-stu-id="6a938-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="6a938-177">Identificador de regla de bus de servicio de Hello es una cadena con este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="6a938-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="6a938-178">enviar tooenable del área de trabajo de análisis de registros de tooa registros de diagnóstico, use este comando:</span><span class="sxs-lookup"><span data-stu-id="6a938-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="6a938-179">Puede combinar estos parámetros tooenable varias opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="6a938-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="6a938-180">Habilitación de la recopilación de registros de diagnóstico de recursos mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="6a938-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="6a938-181">configuración de diagnóstico de toochange con hello API de REST de Monitor de Azure, consulte [este documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a938-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="6a938-182">Administrar la configuración de diagnóstico de recursos en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="6a938-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="6a938-183">Asegúrese de que todos los recursos estén instalados con la configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="6a938-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="6a938-184">Navegue demasiado**Monitor** Hola portal y abra **configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="6a938-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Hoja de registros de diagnóstico en el portal de Hola](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="6a938-186">Puede que tenga tooclick "más sección"servicios de toofind Hola Monitor.</span><span class="sxs-lookup"><span data-stu-id="6a938-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="6a938-187">Aquí puede ver y filtrar todos los recursos que admiten la configuración de diagnóstico toosee si tienen los diagnósticos están habilitados.</span><span class="sxs-lookup"><span data-stu-id="6a938-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="6a938-188">También puede explorar en profundidad toosee si se establecen varias opciones de configuración en un recurso y compruebe qué cuenta de almacenamiento, el espacio de nombres de los centros de eventos o el área de trabajo de análisis de registros que se transmiten datos a.</span><span class="sxs-lookup"><span data-stu-id="6a938-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Resultados de los registros de diagnóstico en el portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="6a938-190">Agregar que una configuración de diagnóstico, se abrirá Hola vista de configuración de diagnóstico, donde puede habilitar, deshabilitar o modificar la configuración de diagnóstico para hello recurso seleccionado.</span><span class="sxs-lookup"><span data-stu-id="6a938-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="6a938-191">Servicios admitidos, categorías y esquemas para los registros de diagnóstico de recursos</span><span class="sxs-lookup"><span data-stu-id="6a938-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="6a938-192">[Consulte este artículo](monitoring-diagnostic-logs-schema.md) para obtener una lista completa de los esquemas utilizados por los servicios y las categorías de registro de hello y servicios compatibles.</span><span class="sxs-lookup"><span data-stu-id="6a938-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a938-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6a938-193">Next steps</span></span>

* [<span data-ttu-id="6a938-194">Registros de diagnóstico de recursos de secuencia demasiado**centros de eventos**</span><span class="sxs-lookup"><span data-stu-id="6a938-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="6a938-195">Cambiar la configuración de diagnóstico de recursos mediante Hola API de REST de Monitor de Azure</span><span class="sxs-lookup"><span data-stu-id="6a938-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="6a938-196">Análisis de registros desde Azure Storage con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6a938-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
