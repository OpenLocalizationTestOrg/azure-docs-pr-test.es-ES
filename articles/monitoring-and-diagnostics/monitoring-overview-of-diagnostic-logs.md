---
title: "Información general sobre los registros de diagnóstico de Azure | Microsoft Docs"
description: "Aprenda qué son los registros de diagnóstico de Azure y cómo puede usarlos para entender los eventos que se producen en un recurso de Azure."
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
ms.openlocfilehash: d59abde29fc7b73a799e5bf3659b02f824b693de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="a3edd-103">Recopile y use los datos de registro provenientes de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="a3edd-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="a3edd-104">Qué son los registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="a3edd-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="a3edd-105">Los **registros de diagnóstico de nivel de recursos de Azure** son registros emitidos por un recurso que proporcionan datos exhaustivos y frecuentes acerca del funcionamiento de ese recurso.</span><span class="sxs-lookup"><span data-stu-id="a3edd-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="a3edd-106">El contenido de estos registros varía según el tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a3edd-106">The content of these logs varies by resource type.</span></span> <span data-ttu-id="a3edd-107">Por ejemplo, los contadores de regla de grupo de seguridad de red y las auditorías de Key Vault son dos categorías de registros de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3edd-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="a3edd-108">Lo registros de diagnóstico de nivel de recursos son distintos del [registro de actividad](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a3edd-108">Resource-level diagnostic logs differ from the [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="a3edd-109">El registro de actividad proporciona una visión general de las operaciones que se realizaron en los recursos de la suscripción con Resource Manager, por ejemplo, crear una máquina virtual o eliminar una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="a3edd-109">The Activity Log provides insight into the operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="a3edd-110">El registro de actividad es un registro de nivel de suscripción.</span><span class="sxs-lookup"><span data-stu-id="a3edd-110">The Activity Log is a subscription-level log.</span></span> <span data-ttu-id="a3edd-111">Los registros de diagnóstico de nivel de recursos proporcionan una visión general de las operaciones realizadas dentro del mismo recurso, por ejemplo, obtener un secreto de un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="a3edd-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="a3edd-112">Los registros de diagnóstico de nivel de recursos también difieren de los registros de diagnóstico de nivel de sistema operativo invitado.</span><span class="sxs-lookup"><span data-stu-id="a3edd-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="a3edd-113">Estos son los recopilados por un agente que se ejecuta dentro de una máquina virtual u otro tipo de recurso admitido.</span><span class="sxs-lookup"><span data-stu-id="a3edd-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="a3edd-114">Los registros de diagnóstico de nivel de recursos no requieren ningún agente y capturan datos específicos de recurso de la plataforma Azure, mientras que los registros de diagnóstico de nivel de sistema operativo invitado capturan los datos desde el sistema operativo y las aplicaciones que se ejecutan en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3edd-114">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself, while guest OS-level diagnostic logs capture data from the operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="a3edd-115">No todos los recursos admiten el nuevo tipo de registros de diagnóstico de recursos que se describe aquí.</span><span class="sxs-lookup"><span data-stu-id="a3edd-115">Not all resources support the new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="a3edd-116">En este artículo se incluye una sección en la que se muestran los tipos de recurso que admiten los nuevos registros de diagnóstico de nivel de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3edd-116">This article contains a section listing which resource types support the new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="a3edd-117">Comparación de los registros de diagnóstico de recursos y otros tipos de registros</span><span class="sxs-lookup"><span data-stu-id="a3edd-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="a3edd-118">Qué se puede hacer con los registros de diagnóstico de nivel de recursos</span><span class="sxs-lookup"><span data-stu-id="a3edd-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="a3edd-119">Estas son algunas de las cosas que puede hacer con los registros de diagnóstico de recursos:</span><span class="sxs-lookup"><span data-stu-id="a3edd-119">Here are some of the things you can do with resource diagnostic logs:</span></span>

![Ubicación lógica de los registros de diagnóstico de recursos](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="a3edd-121">Guardarlos en una [**cuenta de almacenamiento**](monitoring-archive-diagnostic-logs.md) para archivarlos o inspeccionarlos manualmente.</span><span class="sxs-lookup"><span data-stu-id="a3edd-121">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="a3edd-122">Puede especificar el tiempo de retención (en días) usando la **configuración de diagnóstico de recursos**.</span><span class="sxs-lookup"><span data-stu-id="a3edd-122">You can specify the retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="a3edd-123">[Transmitirlos a **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) para la ingestión en un servicio de terceros o una solución de análisis personalizado como PowerBI.</span><span class="sxs-lookup"><span data-stu-id="a3edd-123">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="a3edd-124">Analizarlos con [Log Analytics de OMS](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="a3edd-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="a3edd-125">Puede usar una cuenta de almacenamiento o un espacio de nombres de Event Hubs que no esté en la misma suscripción que el que emite los registros.</span><span class="sxs-lookup"><span data-stu-id="a3edd-125">You can use a storage account or Event Hubs namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="a3edd-126">El usuario que configura los ajustes debe tener el acceso de RBAC adecuado a ambas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="a3edd-126">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="a3edd-127">Configuración de diagnóstico de recursos</span><span class="sxs-lookup"><span data-stu-id="a3edd-127">Resource diagnostic settings</span></span>
<span data-ttu-id="a3edd-128">Los registros de diagnóstico de recursos para recursos que no son de proceso se configuran mediante la configuración de diagnóstico de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3edd-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="a3edd-129">**Configuración de diagnóstico de recursos** para un control de recursos:</span><span class="sxs-lookup"><span data-stu-id="a3edd-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="a3edd-130">Dónde se envían los registros de diagnóstico y las métricas (cuenta de almacenamiento, Event Hubs o Log Analytics de OMS).</span><span class="sxs-lookup"><span data-stu-id="a3edd-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="a3edd-131">Qué categorías de registro se envían y si se envían también datos de métrica.</span><span class="sxs-lookup"><span data-stu-id="a3edd-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="a3edd-132">Cuánto tiempo se debe conservar cada categoría de registro en una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a3edd-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="a3edd-133">Una retención de cero días significa que los registros se conservan de forma indefinida.</span><span class="sxs-lookup"><span data-stu-id="a3edd-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="a3edd-134">De lo contrario, el valor puede ser cualquier número de días comprendido entre 1 y 2147483647.</span><span class="sxs-lookup"><span data-stu-id="a3edd-134">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="a3edd-135">Si se establecen directivas de retención, pero el almacenamiento de registros en una cuenta de almacenamiento está deshabilitado (por ejemplo, si solo se han seleccionado las opciones de Event Hubs u OMS), las directivas de retención no surten ningún efecto.</span><span class="sxs-lookup"><span data-stu-id="a3edd-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="a3edd-136">Las directivas de retención se aplican a diario, por lo que al final de un día (UTC) se eliminan los registros del día que quede fuera de la directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="a3edd-136">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="a3edd-137">Por ejemplo, si tuviera una directiva de retención de un día, se eliminarían los registros de anteayer al principio del día de hoy.</span><span class="sxs-lookup"><span data-stu-id="a3edd-137">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="a3edd-138">Estas opciones se configuran con facilidad a través de la configuración de los diagnósticos para un recurso en Azure Portal, mediante los comandos de Azure PowerShell y de la CLI, o mediante la [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3edd-138">These settings are easily configured via the diagnostic settings for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="a3edd-139">Los registros de diagnóstico y las métricas de la capa de sistema operativo invitado de los recursos de proceso (por ejemplo, máquinas virtuales o Service Fabric) usan [un mecanismo diferente para la configuración y la selección de salidas](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="a3edd-139">Diagnostic logs and metrics for from the guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-to-enable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="a3edd-140">Procedimientos para habilitar la recopilación de registros de diagnóstico de recursos</span><span class="sxs-lookup"><span data-stu-id="a3edd-140">How to enable collection of resource diagnostic logs</span></span>
<span data-ttu-id="a3edd-141">La recopilación de registros de diagnóstico de recursos se puede habilitar [como parte de la creación de un recurso en una plantilla de Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) o después de crear un recurso mediante la página del recurso en el portal.</span><span class="sxs-lookup"><span data-stu-id="a3edd-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in the portal.</span></span> <span data-ttu-id="a3edd-142">También puede habilitar la recolección en cualquier momento mediante comandos de Azure PowerShell o de la CLI, o con la API de REST de Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a3edd-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="a3edd-143">Es posible que estas instrucciones no se apliquen directamente a cada recurso.</span><span class="sxs-lookup"><span data-stu-id="a3edd-143">These instructions may not apply directly to every resource.</span></span> <span data-ttu-id="a3edd-144">Consulte los vínculos de esquema al final de esta página para ver los pasos especiales que se pueden aplicar a determinados tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3edd-144">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-the-portal"></a><span data-ttu-id="a3edd-145">Habilitación de la recopilación de registros de diagnóstico de recursos en el portal</span><span class="sxs-lookup"><span data-stu-id="a3edd-145">Enable collection of resource diagnostic logs in the portal</span></span>
<span data-ttu-id="a3edd-146">Puede habilitar la recopilación de registros de diagnóstico de recursos en Azure Portal una vez creado un recurso yendo a un recurso concreto o a Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a3edd-146">You can enable collection of resource diagnostic logs in the Azure portal after a resource has been created either by going to a specific resource or by navigating to Azure Monitor.</span></span> <span data-ttu-id="a3edd-147">Para habilitar esta opción a través de Azure Monitor:</span><span class="sxs-lookup"><span data-stu-id="a3edd-147">To enable this via Azure Monitor:</span></span>

1. <span data-ttu-id="a3edd-148">En [Azure Portal](http://portal.azure.com), desplácese a Azure Monitor y haga clic en **Configuración de diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="a3edd-148">In the [Azure portal](http://portal.azure.com), navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sección de supervisión de Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="a3edd-150">Si lo desea, filtre la lista por tipo de recurso o por grupo de recursos y, a continuación, haga clic en el recurso para el que desea establecer la configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="a3edd-150">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="a3edd-151">Si no existe ninguna configuración en el recurso que ha seleccionado, se le pide que cree una.</span><span class="sxs-lookup"><span data-stu-id="a3edd-151">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="a3edd-152">Haga clic en "Activar diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="a3edd-152">Click "Turn on diagnostics."</span></span>

   ![Agregar configuración de diagnóstico: sin configuración actual](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="a3edd-154">Si hay una configuración actual en el recurso, verá una lista de opciones ya configuradas en este recurso.</span><span class="sxs-lookup"><span data-stu-id="a3edd-154">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="a3edd-155">Haga clic en "Agregar configuración de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="a3edd-155">Click "Add diagnostic setting."</span></span>

   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="a3edd-157">Asigne un nombre a su configuración, active las casillas para cada destino al que le gustaría enviar datos y configure el recurso que se utiliza para cada uno.</span><span class="sxs-lookup"><span data-stu-id="a3edd-157">Give your setting a name, check the boxes for each destination to which you would like to send data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="a3edd-158">Además, puede establecer un número de días para conservar estos registros mediante los controles deslizantes de **Retención (días)** (solo aplicable al destino de la cuenta de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="a3edd-158">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders (only applicable to the storage account destination).</span></span> <span data-ttu-id="a3edd-159">Con una retención de cero días, los registros se almacenan indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="a3edd-159">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="a3edd-161">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a3edd-161">Click **Save**.</span></span>

<span data-ttu-id="a3edd-162">Transcurridos unos instantes, la nueva configuración aparece en la lista de opciones para este recurso y los registros de diagnóstico se envían a los destinos especificados en cuanto se generan nuevos datos de eventos.</span><span class="sxs-lookup"><span data-stu-id="a3edd-162">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are sent to the specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="a3edd-163">Habilitación de la recopilación de registros de diagnóstico de recursos mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3edd-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="a3edd-164">Para habilitar la recopilación de registros de diagnóstico de recursos con Azure PowerShell, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a3edd-164">To enable collection of resource diagnostic logs via Azure PowerShell, use the following commands:</span></span>

<span data-ttu-id="a3edd-165">Para habilitar el almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="a3edd-165">To enable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="a3edd-166">El identificador de la cuenta de almacenamiento es el identificador de recurso para la cuenta de almacenamiento a la que desea enviar los registros.</span><span class="sxs-lookup"><span data-stu-id="a3edd-166">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="a3edd-167">Para habilitar el streaming de registros de diagnóstico a un centro de eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="a3edd-167">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="a3edd-168">El identificador de regla de Service Bus es una cadena con este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="a3edd-168">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="a3edd-169">Para habilitar el envío de registros de diagnóstico a un área de trabajo de Log Analytics, use este comando:</span><span class="sxs-lookup"><span data-stu-id="a3edd-169">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

<span data-ttu-id="a3edd-170">Puede obtener el identificador de recurso de su área de trabajo de Log Analytics con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="a3edd-170">You can obtain the resource ID of your Log Analytics workspace using the following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="a3edd-171">Puede combinar estos parámetros para habilitar varias opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="a3edd-171">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="a3edd-172">Habilitación de la recopilación de registros de diagnóstico de recursos mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="a3edd-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="a3edd-173">Para habilitar la recopilación de registros de diagnóstico de recursos con la CLI de Azure, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a3edd-173">To enable collection of resource diagnostic logs via the Azure CLI, use the following commands:</span></span>

<span data-ttu-id="a3edd-174">Para habilitar el almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="a3edd-174">To enable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="a3edd-175">El identificador de la cuenta de almacenamiento es el identificador de recurso para la cuenta de almacenamiento a la que desea enviar los registros.</span><span class="sxs-lookup"><span data-stu-id="a3edd-175">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="a3edd-176">Para habilitar el streaming de registros de diagnóstico a un centro de eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="a3edd-176">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="a3edd-177">El identificador de regla de Service Bus es una cadena con este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="a3edd-177">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="a3edd-178">Para habilitar el envío de registros de diagnóstico a un área de trabajo de Log Analytics, use este comando:</span><span class="sxs-lookup"><span data-stu-id="a3edd-178">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
```

<span data-ttu-id="a3edd-179">Puede combinar estos parámetros para habilitar varias opciones de salida.</span><span class="sxs-lookup"><span data-stu-id="a3edd-179">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="a3edd-180">Habilitación de la recopilación de registros de diagnóstico de recursos mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="a3edd-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="a3edd-181">Para cambiar la configuración de diagnóstico con la API de REST de Azure Monitor, consulte [este documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3edd-181">To change diagnostic settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-the-portal"></a><span data-ttu-id="a3edd-182">Administración de la configuración de diagnóstico de recursos en el portal</span><span class="sxs-lookup"><span data-stu-id="a3edd-182">Manage resource diagnostic settings in the portal</span></span>
<span data-ttu-id="a3edd-183">Asegúrese de que todos los recursos estén instalados con la configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="a3edd-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="a3edd-184">Vaya a **Monitor** en el portal y abra **Configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="a3edd-184">Navigate to **Monitor** in the portal and open **Diagnostic settings**.</span></span>

![Hoja Registros de diagnóstico en el portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="a3edd-186">Puede que tenga que hacer clic en "More services" (Más servicios) para encontrar la sección Supervisión.</span><span class="sxs-lookup"><span data-stu-id="a3edd-186">You may have to click "More services" to find the Monitor section.</span></span>

<span data-ttu-id="a3edd-187">Aquí puede ver y filtrar todos los recursos que admiten la configuración de diagnósticos y comprobar si está habilitada para los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="a3edd-187">Here you can view and filter all resources that support diagnostic settings to see if they have diagnostics enabled.</span></span> <span data-ttu-id="a3edd-188">También puede explorar en profundidad para comprobar si hay varias opciones de configuración establecidas en un recurso y a qué cuenta de almacenamiento, espacio de nombres de Event Hubs o área de trabajo de Log Analytics se transmiten los datos.</span><span class="sxs-lookup"><span data-stu-id="a3edd-188">You can also drill down to see if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Resultados de los registros de diagnóstico en el portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="a3edd-190">Al agregar una opción de configuración de diagnóstico, se abre la vista Configuración de diagnóstico, donde puede habilitar, deshabilitar o modificar la configuración de diagnóstico para el recurso seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a3edd-190">Adding a diagnostic setting brings up the Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="a3edd-191">Servicios admitidos, categorías y esquemas para los registros de diagnóstico de recursos</span><span class="sxs-lookup"><span data-stu-id="a3edd-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="a3edd-192">[Consulte este artículo](monitoring-diagnostic-logs-schema.md) para obtener una lista completa de los servicios admitidos y las categorías de registro y los esquemas utilizados por esos servicios.</span><span class="sxs-lookup"><span data-stu-id="a3edd-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and the log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3edd-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3edd-193">Next steps</span></span>

* [<span data-ttu-id="a3edd-194">Transmisión de registros de diagnóstico a **Event Hubs**</span><span class="sxs-lookup"><span data-stu-id="a3edd-194">Stream resource diagnostic logs to **Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="a3edd-195">Cambio de la configuración de diagnóstico de recursos con la API de REST de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="a3edd-195">Change resource diagnostic settings using the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="a3edd-196">Análisis de registros desde Azure Storage con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a3edd-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
