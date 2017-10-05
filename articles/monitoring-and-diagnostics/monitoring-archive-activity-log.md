---
title: Archivo del registro de actividades de Azure | Microsoft Docs
description: "Aprenda a archivar el registro de actividades de Azure para su retención a largo plazo en una cuenta de almacenamiento."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 0e3a5b84f57eac96249430fa1c2c4cc076c2926a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="archive-the-azure-activity-log"></a><span data-ttu-id="d627b-103">Archivo del registro de actividades de Azure</span><span class="sxs-lookup"><span data-stu-id="d627b-103">Archive the Azure Activity Log</span></span>
<span data-ttu-id="d627b-104">En este artículo, le mostraremos cómo puede usar Azure Portal, los cmdlets de PowerShell o la CLI multiplataforma para archivar el [**registro de actividades de Azure**](monitoring-overview-activity-logs.md) en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d627b-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, or Cross-Platform CLI to archive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="d627b-105">Esta opción es útil si desea conservar el registro de actividades más de 90 días (con control total sobre la directiva de retención) para auditorías, análisis estáticos o copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d627b-105">This option is useful if you would like to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="d627b-106">Si solo necesita conservar los eventos durante 90 días o menos, no es necesario configurar el archivado en una cuenta de almacenamiento, ya que los eventos del registro de actividades se conservan en la plataforma de Azure durante 90 días sin necesidad de habilitar el archivado.</span><span class="sxs-lookup"><span data-stu-id="d627b-106">If you only need to retain your events for 90 days or less you do not need to set up archival to a storage account, since Activity Log events are retained in the Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d627b-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d627b-107">Prerequisites</span></span>
<span data-ttu-id="d627b-108">Antes de comenzar, necesita [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) en la que poder archivar el registro de actividades.</span><span class="sxs-lookup"><span data-stu-id="d627b-108">Before you begin, you need to [create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Activity Log.</span></span> <span data-ttu-id="d627b-109">Le recomendamos encarecidamente que no utilice una cuenta de almacenamiento existente que tenga otros datos sin supervisión almacenados en ella, para que pueda controlar mejor el acceso a los datos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="d627b-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="d627b-110">Sin embargo, si también va a archivar los registros y las métricas de Diagnóstico en una cuenta de almacenamiento, puede que tenga sentido utilizar esa cuenta de almacenamiento para el registro de actividades para mantener todos los datos de supervisión en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="d627b-110">However, if you are also archiving Diagnostic Logs and metrics to a storage account, it may make sense to use that storage account for your Activity Log as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="d627b-111">La cuenta de almacenamiento que use debe ser una cuenta de almacenamiento de propósito general no una cuenta de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="d627b-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="d627b-112">La cuenta de almacenamiento no tiene que estar en la misma suscripción que la que emite los registros, siempre que el usuario que configura la configuración tenga acceso RBAC adecuado a ambas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="d627b-112">The storage account does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="d627b-113">Perfil de registro</span><span class="sxs-lookup"><span data-stu-id="d627b-113">Log Profile</span></span>
<span data-ttu-id="d627b-114">Para archivar el registro de actividades mediante cualquiera de los métodos siguientes, debe establecer el **perfil de registro** para una suscripción.</span><span class="sxs-lookup"><span data-stu-id="d627b-114">To archive the Activity Log using any of the methods below, you set the **Log Profile** for a subscription.</span></span> <span data-ttu-id="d627b-115">El perfil de registro define el tipo de eventos que se almacenan o transmiten y las salidas: cuenta de almacenamiento y/o centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="d627b-115">The Log Profile defines the type of events that are stored or streamed and the outputs—storage account and/or event hub.</span></span> <span data-ttu-id="d627b-116">También define la directiva de retención (el número de días que deben conservarse) para los eventos almacenados en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d627b-116">It also defines the retention policy (number of days to retain) for events stored in a storage account.</span></span> <span data-ttu-id="d627b-117">Si la directiva de retención se establece en cero los eventos se almacenan indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="d627b-117">If the retention policy is set to zero, events are stored indefinitely.</span></span> <span data-ttu-id="d627b-118">De lo contrario, se puede establecer en cualquier valor entre 1 y 2147483647.</span><span class="sxs-lookup"><span data-stu-id="d627b-118">Otherwise, this can be set to any value between 1 and 2147483647.</span></span> <span data-ttu-id="d627b-119">Las directivas de retención se aplican a diario, por lo que al final de un día (UTC) se eliminan los registros del día que quede fuera de la directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="d627b-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="d627b-120">Por ejemplo, si tuviera una directiva de retención de un día, se eliminarían los registros de anteayer al principio del día de hoy.</span><span class="sxs-lookup"><span data-stu-id="d627b-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span> <span data-ttu-id="d627b-121">[Puede leer más acerca de los perfiles de registro aquí](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="d627b-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-the-activity-log-using-the-portal"></a><span data-ttu-id="d627b-122">Archivo del registro de actividades mediante el portal</span><span class="sxs-lookup"><span data-stu-id="d627b-122">Archive the Activity Log using the portal</span></span>
1. <span data-ttu-id="d627b-123">En el portal, haga clic en el vínculo **Registro de actividades** situado en el lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="d627b-123">In the portal, click the **Activity Log** link on the left-side navigation.</span></span> <span data-ttu-id="d627b-124">Si no ve un vínculo para el registro de actividades, haga clic primero en el vínculo **Más servicios** .</span><span class="sxs-lookup"><span data-stu-id="d627b-124">If you don’t see a link for the Activity Log, click the **More Services** link first.</span></span>
   
    ![Ir a la hoja del registro de actividades](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="d627b-126">En la parte superior de la hoja, haga clic en **Exportar**.</span><span class="sxs-lookup"><span data-stu-id="d627b-126">At the top of the blade, click **Export**.</span></span>
   
    ![Hacer clic en el botón Exportar](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="d627b-128">En la hoja que aparece, seleccione la casilla para **exportar a una cuenta de almacenamiento** y seleccione una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d627b-128">In the blade that appears, check the box for **Export to a storage account** and select a storage account.</span></span>
   
    ![Establecer una cuenta de almacenamiento](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="d627b-130">Con el control deslizante o el cuadro de texto, defina el número de días que deben conservarse los eventos del registro de actividades en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d627b-130">Using the slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="d627b-131">Si prefiere que los datos se conserven en la cuenta de almacenamiento indefinidamente establezca este número en cero.</span><span class="sxs-lookup"><span data-stu-id="d627b-131">If you prefer to have your data persisted in the storage account indefinitely, set this number to zero.</span></span>
5. <span data-ttu-id="d627b-132">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="d627b-132">Click **Save**.</span></span>

## <a name="archive-the-activity-log-via-powershell"></a><span data-ttu-id="d627b-133">Archivo del registro de actividades a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d627b-133">Archive the Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="d627b-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d627b-134">Property</span></span> | <span data-ttu-id="d627b-135">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d627b-135">Required</span></span> | <span data-ttu-id="d627b-136">Description</span><span class="sxs-lookup"><span data-stu-id="d627b-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d627b-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="d627b-137">StorageAccountId</span></span> |<span data-ttu-id="d627b-138">No</span><span class="sxs-lookup"><span data-stu-id="d627b-138">No</span></span> |<span data-ttu-id="d627b-139">Identificador de recurso de la cuenta de almacenamiento donde se deben guardar los registros de actividades.</span><span class="sxs-lookup"><span data-stu-id="d627b-139">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="d627b-140">Ubicaciones</span><span class="sxs-lookup"><span data-stu-id="d627b-140">Locations</span></span> |<span data-ttu-id="d627b-141">Sí</span><span class="sxs-lookup"><span data-stu-id="d627b-141">Yes</span></span> |<span data-ttu-id="d627b-142">Lista separada por comas de las regiones para las que desea recopilar eventos del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="d627b-142">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="d627b-143">Puede ver una lista de todas las regiones [si visita esta página](https://azure.microsoft.com/en-us/regions) o mediante [la API de REST de administración de Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="d627b-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="d627b-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="d627b-144">RetentionInDays</span></span> |<span data-ttu-id="d627b-145">Sí</span><span class="sxs-lookup"><span data-stu-id="d627b-145">Yes</span></span> |<span data-ttu-id="d627b-146">Número de días que deben retenerse los eventos, entre 1 y 2147483647.</span><span class="sxs-lookup"><span data-stu-id="d627b-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="d627b-147">Con el valor cero, se almacenan los registros indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="d627b-147">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="d627b-148">Categorías</span><span class="sxs-lookup"><span data-stu-id="d627b-148">Categories</span></span> |<span data-ttu-id="d627b-149">Sí</span><span class="sxs-lookup"><span data-stu-id="d627b-149">Yes</span></span> |<span data-ttu-id="d627b-150">Lista separada por comas de las categorías de eventos que deben recopilarse.</span><span class="sxs-lookup"><span data-stu-id="d627b-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="d627b-151">Los valores posibles son Write, Delete y Action.</span><span class="sxs-lookup"><span data-stu-id="d627b-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-the-activity-log-via-cli"></a><span data-ttu-id="d627b-152">Archivo del registro de actividades a través de CLI</span><span class="sxs-lookup"><span data-stu-id="d627b-152">Archive the Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="d627b-153">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d627b-153">Property</span></span> | <span data-ttu-id="d627b-154">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d627b-154">Required</span></span> | <span data-ttu-id="d627b-155">Description</span><span class="sxs-lookup"><span data-stu-id="d627b-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d627b-156">name</span><span class="sxs-lookup"><span data-stu-id="d627b-156">name</span></span> |<span data-ttu-id="d627b-157">Sí</span><span class="sxs-lookup"><span data-stu-id="d627b-157">Yes</span></span> |<span data-ttu-id="d627b-158">Nombre de su perfil de registro.</span><span class="sxs-lookup"><span data-stu-id="d627b-158">Name of your log profile.</span></span> |
| <span data-ttu-id="d627b-159">storageId</span><span class="sxs-lookup"><span data-stu-id="d627b-159">storageId</span></span> |<span data-ttu-id="d627b-160">No</span><span class="sxs-lookup"><span data-stu-id="d627b-160">No</span></span> |<span data-ttu-id="d627b-161">Identificador de recurso de la cuenta de almacenamiento donde se deben guardar los registros de actividades.</span><span class="sxs-lookup"><span data-stu-id="d627b-161">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="d627b-162">Ubicaciones</span><span class="sxs-lookup"><span data-stu-id="d627b-162">locations</span></span> |<span data-ttu-id="d627b-163">Sí</span><span class="sxs-lookup"><span data-stu-id="d627b-163">Yes</span></span> |<span data-ttu-id="d627b-164">Lista separada por comas de las regiones para las que desea recopilar eventos del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="d627b-164">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="d627b-165">Puede ver una lista de todas las regiones [si visita esta página](https://azure.microsoft.com/en-us/regions) o mediante [la API de REST de administración de Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="d627b-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="d627b-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="d627b-166">retentionInDays</span></span> |<span data-ttu-id="d627b-167">Sí</span><span class="sxs-lookup"><span data-stu-id="d627b-167">Yes</span></span> |<span data-ttu-id="d627b-168">Número de días que deben retenerse los eventos, entre 1 y 2147483647.</span><span class="sxs-lookup"><span data-stu-id="d627b-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="d627b-169">Con el valor cero, se almacenarán los registros indefinidamente (de manera indefinida).</span><span class="sxs-lookup"><span data-stu-id="d627b-169">A value of zero will store the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="d627b-170">Categorías</span><span class="sxs-lookup"><span data-stu-id="d627b-170">categories</span></span> |<span data-ttu-id="d627b-171">Sí</span><span class="sxs-lookup"><span data-stu-id="d627b-171">Yes</span></span> |<span data-ttu-id="d627b-172">Lista separada por comas de las categorías de eventos que deben recopilarse.</span><span class="sxs-lookup"><span data-stu-id="d627b-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="d627b-173">Los valores posibles son Write, Delete y Action.</span><span class="sxs-lookup"><span data-stu-id="d627b-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-the-activity-log"></a><span data-ttu-id="d627b-174">Esquema de almacenamiento del registro de actividades</span><span class="sxs-lookup"><span data-stu-id="d627b-174">Storage schema of the Activity Log</span></span>
<span data-ttu-id="d627b-175">Una vez que haya configurado el archivado, se creará un contenedor de almacenamiento en la cuenta de almacenamiento en cuanto se produzca un evento del registro de actividades.</span><span class="sxs-lookup"><span data-stu-id="d627b-175">Once you have set up archival, a storage container will be created in the storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="d627b-176">Los blobs dentro del contenedor siguen el mismo formato en el registro de actividades y en los registros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="d627b-176">The blobs within the container follow the same format across the Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="d627b-177">La estructura de estos blobs es:</span><span class="sxs-lookup"><span data-stu-id="d627b-177">The structure of these blobs is:</span></span>

> <span data-ttu-id="d627b-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={año con cuatro dígitos}/m={mes con dos dígitos}/d={día con dos dígitos}/h={hora en formato de 24 horas con dos dígitos}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="d627b-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="d627b-179">Por ejemplo, un nombre de blob podría ser:</span><span class="sxs-lookup"><span data-stu-id="d627b-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="d627b-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="d627b-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="d627b-181">Cada blob PT1H.json contiene un blob JSON de eventos que se produjeron en la hora especificada en la dirección URL del blob (por ejemplo h = 12).</span><span class="sxs-lookup"><span data-stu-id="d627b-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (e.g. h=12).</span></span> <span data-ttu-id="d627b-182">Durante la hora en cuestión, los eventos se anexan al archivo PT1H.json a medida que se producen.</span><span class="sxs-lookup"><span data-stu-id="d627b-182">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="d627b-183">El valor de los minutos (m = 00) siempre es 00, ya que los eventos del registro de actividades se dividen en blobs individuales por hora.</span><span class="sxs-lookup"><span data-stu-id="d627b-183">The minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="d627b-184">En el archivo PT1H.json, cada evento se almacena en la matriz de "registros" con este formato:</span><span class="sxs-lookup"><span data-stu-id="d627b-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="d627b-185">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="d627b-185">Element name</span></span> | <span data-ttu-id="d627b-186">Description</span><span class="sxs-lookup"><span data-stu-id="d627b-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d627b-187">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="d627b-187">time</span></span> |<span data-ttu-id="d627b-188">Marca de tiempo de cuándo el servicio de Azure generó el evento que procesó la solicitud correspondiente al evento.</span><span class="sxs-lookup"><span data-stu-id="d627b-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="d627b-189">ResourceId</span><span class="sxs-lookup"><span data-stu-id="d627b-189">resourceId</span></span> |<span data-ttu-id="d627b-190">Identificador de recurso del recurso afectado.</span><span class="sxs-lookup"><span data-stu-id="d627b-190">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="d627b-191">operationName</span><span class="sxs-lookup"><span data-stu-id="d627b-191">operationName</span></span> |<span data-ttu-id="d627b-192">Nombre de la operación.</span><span class="sxs-lookup"><span data-stu-id="d627b-192">Name of the operation.</span></span> |
| <span data-ttu-id="d627b-193">categoría</span><span class="sxs-lookup"><span data-stu-id="d627b-193">category</span></span> |<span data-ttu-id="d627b-194">Categoría de la acción, p. ej.</span><span class="sxs-lookup"><span data-stu-id="d627b-194">Category of the action, eg.</span></span> <span data-ttu-id="d627b-195">Write, Read, Action.</span><span class="sxs-lookup"><span data-stu-id="d627b-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="d627b-196">resultType</span><span class="sxs-lookup"><span data-stu-id="d627b-196">resultType</span></span> |<span data-ttu-id="d627b-197">Tipo del resultado, p. ej.</span><span class="sxs-lookup"><span data-stu-id="d627b-197">The type of the result, eg.</span></span> <span data-ttu-id="d627b-198">Success, Failure, Start</span><span class="sxs-lookup"><span data-stu-id="d627b-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="d627b-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="d627b-199">resultSignature</span></span> |<span data-ttu-id="d627b-200">Depende del tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="d627b-200">Depends on the resource type.</span></span> |
| <span data-ttu-id="d627b-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="d627b-201">durationMs</span></span> |<span data-ttu-id="d627b-202">Duración de la operación en milisegundos</span><span class="sxs-lookup"><span data-stu-id="d627b-202">Duration of the operation in milliseconds</span></span> |
| <span data-ttu-id="d627b-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="d627b-203">callerIpAddress</span></span> |<span data-ttu-id="d627b-204">La dirección IP del usuario que ha realizado la operación, la notificación de UPN o la notificación de SPN basada en la disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="d627b-204">IP address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="d627b-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="d627b-205">correlationId</span></span> |<span data-ttu-id="d627b-206">Normalmente, un GUID en formato de cadena.</span><span class="sxs-lookup"><span data-stu-id="d627b-206">Usually a GUID in the string format.</span></span> <span data-ttu-id="d627b-207">Los eventos que comparten correlationId pertenecen a la misma acción general.</span><span class="sxs-lookup"><span data-stu-id="d627b-207">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="d627b-208">identidad</span><span class="sxs-lookup"><span data-stu-id="d627b-208">identity</span></span> |<span data-ttu-id="d627b-209">Blob JSON que describe la autorización y las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d627b-209">JSON blob describing the authorization and claims.</span></span> |
| <span data-ttu-id="d627b-210">authorization</span><span class="sxs-lookup"><span data-stu-id="d627b-210">authorization</span></span> |<span data-ttu-id="d627b-211">Blob de propiedades RBAC del evento.</span><span class="sxs-lookup"><span data-stu-id="d627b-211">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="d627b-212">Normalmente incluye las propiedades "action", "role" y "scope".</span><span class="sxs-lookup"><span data-stu-id="d627b-212">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="d627b-213">level</span><span class="sxs-lookup"><span data-stu-id="d627b-213">level</span></span> |<span data-ttu-id="d627b-214">Nivel del evento.</span><span class="sxs-lookup"><span data-stu-id="d627b-214">Level of the event.</span></span> <span data-ttu-id="d627b-215">Uno de los siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose"</span><span class="sxs-lookup"><span data-stu-id="d627b-215">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="d627b-216">location</span><span class="sxs-lookup"><span data-stu-id="d627b-216">location</span></span> |<span data-ttu-id="d627b-217">Región en la que se ha producido la ubicación (o global).</span><span class="sxs-lookup"><span data-stu-id="d627b-217">Region in which the location occurred (or global).</span></span> |
| <span data-ttu-id="d627b-218">propiedades</span><span class="sxs-lookup"><span data-stu-id="d627b-218">properties</span></span> |<span data-ttu-id="d627b-219">Conjunto de pares `<Key, Value>` (es decir, diccionario) que describe los detalles del evento.</span><span class="sxs-lookup"><span data-stu-id="d627b-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="d627b-220">Las propiedades y el uso de estas propiedades pueden variar según el recurso.</span><span class="sxs-lookup"><span data-stu-id="d627b-220">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d627b-221">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d627b-221">Next steps</span></span>
* [<span data-ttu-id="d627b-222">Descargar blobs para el análisis</span><span class="sxs-lookup"><span data-stu-id="d627b-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="d627b-223">Transmitir el registro de actividades a Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="d627b-223">Stream the Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="d627b-224">Obtener más información acerca del registro de actividades</span><span class="sxs-lookup"><span data-stu-id="d627b-224">Read more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)

