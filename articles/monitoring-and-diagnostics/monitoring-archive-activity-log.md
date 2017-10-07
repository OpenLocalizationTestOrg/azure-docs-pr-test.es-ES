---
title: Hola aaaArchive registro de actividad de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooarchive registro de la actividad de Azure para la retención a largo plazo en una cuenta de almacenamiento."
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
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="e6ab3-103">Archivar hello Azure Activity Log</span><span class="sxs-lookup"><span data-stu-id="e6ab3-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="e6ab3-104">En este artículo se muestra cómo puede utilizar Hola portal de Azure, Cmdlets de PowerShell o CLI multiplataforma tooarchive su [ **Azure Activity Log** ](monitoring-overview-activity-logs.md) en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="e6ab3-105">Esta opción es útil si desea que tooretain el registro de actividad de más de 90 días (con control total sobre la directiva de retención de hello) para auditar, análisis estático, o una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="e6ab3-106">Si solo necesita tooretain sus eventos durante 90 días o menos, no es necesario tooset una cuenta de almacenamiento de archivo tooa, puesto que los eventos de registro de actividad se conservan en hello plataforma Windows Azure durante 90 días sin habilitar el archivado.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6ab3-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e6ab3-107">Prerequisites</span></span>
<span data-ttu-id="e6ab3-108">Antes de empezar, necesita demasiado[crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich puede archivar el registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="e6ab3-109">Se recomienda encarecidamente que no utilice una cuenta de almacenamiento existente que tiene otros, sin supervisión de los datos almacenados en ella para que puedan controlar mejor toomonitoring acceder a los datos.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="e6ab3-110">Sin embargo, si también va a archivar registros de diagnóstico y la cuenta de almacenamiento de tooa de métricas, puede que tenga sentido toouse esa cuenta de almacenamiento para la actividad de registro también tookeep todos los datos de supervisión en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="e6ab3-111">cuenta de almacenamiento de Hola que use debe ser una cuenta de almacenamiento de propósito general, no una cuenta de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="e6ab3-112">cuenta de almacenamiento de Hello no tiene toobe Hola misma suscripción que Hola emitir registros como usuario de Hola que configura los valores de hello tiene suscripciones de tooboth de acceso RBAC adecuadas.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="e6ab3-113">Perfil de registro</span><span class="sxs-lookup"><span data-stu-id="e6ab3-113">Log Profile</span></span>
<span data-ttu-id="e6ab3-114">Hola tooarchive registro de actividad mediante cualquiera de los siguientes métodos de hello, Establece hello **perfil del registro** para una suscripción.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="e6ab3-115">define el tipo de saludo de eventos que se almacenan o transmiten Hello perfil de registro y Hola salidas: concentrador de eventos o de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="e6ab3-116">También define la directiva de retención de hello (número de días tooretain) para los eventos almacenados en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="e6ab3-117">Si la directiva de retención de Hola se establece toozero, los eventos se almacenan indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="e6ab3-118">En caso contrario, se puede establecer tooany valor entre 1 y 2147483647.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="e6ab3-119">Las directivas de retención son aplicado por día, por lo que en hello final de un día (UTC), los registros de día de Hola que es ahora más allá de la directiva de retención de Hola se eliminarán.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="e6ab3-120">Por ejemplo, si tuviera una directiva de retención de un día, en principio de Hola de hoy día de Hola Hola registros de hello anteayer se eliminarán.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="e6ab3-121">[Puede leer más acerca de los perfiles de registro aquí](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="e6ab3-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="e6ab3-122">Archivo Hola mediante Hola portal de registro de actividad</span><span class="sxs-lookup"><span data-stu-id="e6ab3-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="e6ab3-123">En el portal de hello, haga clic en hello **registro de actividad** vínculo de navegación del lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="e6ab3-124">Si no ve un vínculo para hello registro de actividad, haga clic en hello **más servicios** vincular primero.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![Navegar por la hoja de registro tooActivity](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="e6ab3-126">En la parte superior de Hola de hoja de hello, haga clic en **exportar**.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![Haga clic en el botón Exportar de Hola](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="e6ab3-128">En la hoja de Hola que aparece, la casilla Hola para **exportar cuenta de almacenamiento de tooa** y seleccione una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![Establecer una cuenta de almacenamiento](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="e6ab3-130">Con el control deslizante de Hola o cuadro de texto, defina un número de días para el que se deben mantener eventos del registro de actividad en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="e6ab3-131">Si lo prefiere toohave los datos persisten en la cuenta de almacenamiento de hello indefinidamente, establezca este número toozero.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="e6ab3-132">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="e6ab3-133">Archivar el registro de actividad a través de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="e6ab3-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="e6ab3-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e6ab3-134">Property</span></span> | <span data-ttu-id="e6ab3-135">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e6ab3-135">Required</span></span> | <span data-ttu-id="e6ab3-136">Description</span><span class="sxs-lookup"><span data-stu-id="e6ab3-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e6ab3-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="e6ab3-137">StorageAccountId</span></span> |<span data-ttu-id="e6ab3-138">No</span><span class="sxs-lookup"><span data-stu-id="e6ab3-138">No</span></span> |<span data-ttu-id="e6ab3-139">Se debe guardar el Id. de recurso de la cuenta de almacenamiento de hello toowhich registros de actividad.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="e6ab3-140">Ubicaciones</span><span class="sxs-lookup"><span data-stu-id="e6ab3-140">Locations</span></span> |<span data-ttu-id="e6ab3-141">Sí</span><span class="sxs-lookup"><span data-stu-id="e6ab3-141">Yes</span></span> |<span data-ttu-id="e6ab3-142">Lista separada por comas de regiones que le gustaría toocollect eventos de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="e6ab3-143">Puede ver una lista de todas las regiones [visite esta página](https://azure.microsoft.com/en-us/regions) o mediante [Hola API de REST de administración de Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6ab3-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="e6ab3-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="e6ab3-144">RetentionInDays</span></span> |<span data-ttu-id="e6ab3-145">Sí</span><span class="sxs-lookup"><span data-stu-id="e6ab3-145">Yes</span></span> |<span data-ttu-id="e6ab3-146">Número de días que deben retenerse los eventos, entre 1 y 2147483647.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="e6ab3-147">Un valor de cero almacena los registros de hello indefinidamente (indefinidamente).</span><span class="sxs-lookup"><span data-stu-id="e6ab3-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="e6ab3-148">Categorías</span><span class="sxs-lookup"><span data-stu-id="e6ab3-148">Categories</span></span> |<span data-ttu-id="e6ab3-149">Sí</span><span class="sxs-lookup"><span data-stu-id="e6ab3-149">Yes</span></span> |<span data-ttu-id="e6ab3-150">Lista separada por comas de las categorías de eventos que deben recopilarse.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="e6ab3-151">Los valores posibles son Write, Delete y Action.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="e6ab3-152">Archivar el registro de actividad mediante la CLI de Hola</span><span class="sxs-lookup"><span data-stu-id="e6ab3-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="e6ab3-153">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e6ab3-153">Property</span></span> | <span data-ttu-id="e6ab3-154">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e6ab3-154">Required</span></span> | <span data-ttu-id="e6ab3-155">Description</span><span class="sxs-lookup"><span data-stu-id="e6ab3-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e6ab3-156">name</span><span class="sxs-lookup"><span data-stu-id="e6ab3-156">name</span></span> |<span data-ttu-id="e6ab3-157">Sí</span><span class="sxs-lookup"><span data-stu-id="e6ab3-157">Yes</span></span> |<span data-ttu-id="e6ab3-158">Nombre de su perfil de registro.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-158">Name of your log profile.</span></span> |
| <span data-ttu-id="e6ab3-159">storageId</span><span class="sxs-lookup"><span data-stu-id="e6ab3-159">storageId</span></span> |<span data-ttu-id="e6ab3-160">No</span><span class="sxs-lookup"><span data-stu-id="e6ab3-160">No</span></span> |<span data-ttu-id="e6ab3-161">Se debe guardar el Id. de recurso de la cuenta de almacenamiento de hello toowhich registros de actividad.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="e6ab3-162">Ubicaciones</span><span class="sxs-lookup"><span data-stu-id="e6ab3-162">locations</span></span> |<span data-ttu-id="e6ab3-163">Sí</span><span class="sxs-lookup"><span data-stu-id="e6ab3-163">Yes</span></span> |<span data-ttu-id="e6ab3-164">Lista separada por comas de regiones que le gustaría toocollect eventos de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="e6ab3-165">Puede ver una lista de todas las regiones [visite esta página](https://azure.microsoft.com/en-us/regions) o mediante [Hola API de REST de administración de Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6ab3-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="e6ab3-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="e6ab3-166">retentionInDays</span></span> |<span data-ttu-id="e6ab3-167">Sí</span><span class="sxs-lookup"><span data-stu-id="e6ab3-167">Yes</span></span> |<span data-ttu-id="e6ab3-168">Número de días que deben retenerse los eventos, entre 1 y 2147483647.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="e6ab3-169">Un valor de cero almacenará los registros de hello indefinidamente (indefinidamente).</span><span class="sxs-lookup"><span data-stu-id="e6ab3-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="e6ab3-170">Categorías</span><span class="sxs-lookup"><span data-stu-id="e6ab3-170">categories</span></span> |<span data-ttu-id="e6ab3-171">Sí</span><span class="sxs-lookup"><span data-stu-id="e6ab3-171">Yes</span></span> |<span data-ttu-id="e6ab3-172">Lista separada por comas de las categorías de eventos que deben recopilarse.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="e6ab3-173">Los valores posibles son Write, Delete y Action.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="e6ab3-174">Esquema de almacenamiento de registro de actividad de hello</span><span class="sxs-lookup"><span data-stu-id="e6ab3-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="e6ab3-175">Una vez que haya configurado archivado, se creará un contenedor de almacenamiento en la cuenta de almacenamiento de hello en cuanto se produce un evento de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="e6ab3-176">blobs de Hello en el contenedor de hello siguen Hola mismo formato en hello registro de actividad y registros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="e6ab3-177">estructura de Hola de estos blobs es:</span><span class="sxs-lookup"><span data-stu-id="e6ab3-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="e6ab3-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={año con cuatro dígitos}/m={mes con dos dígitos}/d={día con dos dígitos}/h={hora en formato de 24 horas con dos dígitos}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="e6ab3-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="e6ab3-179">Por ejemplo, un nombre de blob podría ser:</span><span class="sxs-lookup"><span data-stu-id="e6ab3-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="e6ab3-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="e6ab3-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="e6ab3-181">Cada blob PT1H.json contiene un blob JSON de eventos que se produjeron durante la hora de hello especificado en la dirección URL del blob hello (p. ej. h = 12).</span><span class="sxs-lookup"><span data-stu-id="e6ab3-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="e6ab3-182">Durante Hola hora presente, los eventos son anexados toohello PT1H.json archivo cuando se producen.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="e6ab3-183">Hola valor de minuto (m = 00) siempre es 00, puesto que los eventos de registro de actividad se dividen en los blobs individuales por hora.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="e6ab3-184">En archivo de PT1H.json hello, cada evento se almacena en la matriz de registros"hello", sigue este formato:</span><span class="sxs-lookup"><span data-stu-id="e6ab3-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

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


| <span data-ttu-id="e6ab3-185">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="e6ab3-185">Element name</span></span> | <span data-ttu-id="e6ab3-186">Description</span><span class="sxs-lookup"><span data-stu-id="e6ab3-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e6ab3-187">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="e6ab3-187">time</span></span> |<span data-ttu-id="e6ab3-188">Marca de tiempo cuando se generan eventos de Hola Hola Hola de procesamiento de servicio de Azure solicitar evento Hola correspondiente.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="e6ab3-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="e6ab3-189">resourceId</span></span> |<span data-ttu-id="e6ab3-190">Id. de recurso de hello afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="e6ab3-191">operationName</span><span class="sxs-lookup"><span data-stu-id="e6ab3-191">operationName</span></span> |<span data-ttu-id="e6ab3-192">Nombre de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-192">Name of hello operation.</span></span> |
| <span data-ttu-id="e6ab3-193">categoría</span><span class="sxs-lookup"><span data-stu-id="e6ab3-193">category</span></span> |<span data-ttu-id="e6ab3-194">Categoría de acción de hello, p. ej.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-194">Category of hello action, eg.</span></span> <span data-ttu-id="e6ab3-195">Write, Read, Action.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="e6ab3-196">resultType</span><span class="sxs-lookup"><span data-stu-id="e6ab3-196">resultType</span></span> |<span data-ttu-id="e6ab3-197">Hola tipo de resultado de hello, p. ej.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-197">hello type of hello result, eg.</span></span> <span data-ttu-id="e6ab3-198">Success, Failure, Start</span><span class="sxs-lookup"><span data-stu-id="e6ab3-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="e6ab3-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="e6ab3-199">resultSignature</span></span> |<span data-ttu-id="e6ab3-200">Depende de tipo de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="e6ab3-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="e6ab3-201">durationMs</span></span> |<span data-ttu-id="e6ab3-202">Duración de la operación de hello en milisegundos</span><span class="sxs-lookup"><span data-stu-id="e6ab3-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="e6ab3-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="e6ab3-203">callerIpAddress</span></span> |<span data-ttu-id="e6ab3-204">Dirección IP del usuario de Hola que ha realizado la operación de hello, notificación de UPN o notificación SPN según su disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="e6ab3-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="e6ab3-205">correlationId</span></span> |<span data-ttu-id="e6ab3-206">Normalmente un GUID en formato de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="e6ab3-207">Los eventos que comparten un correlationId pertenecen toohello misma acción.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="e6ab3-208">identidad</span><span class="sxs-lookup"><span data-stu-id="e6ab3-208">identity</span></span> |<span data-ttu-id="e6ab3-209">Blob JSON con descripciones de notificaciones y autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="e6ab3-210">authorization</span><span class="sxs-lookup"><span data-stu-id="e6ab3-210">authorization</span></span> |<span data-ttu-id="e6ab3-211">BLOB de propiedades de evento de hello RBAC.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="e6ab3-212">Normalmente incluye propiedades de "acción", "role" y "ámbito" Hola.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="e6ab3-213">level</span><span class="sxs-lookup"><span data-stu-id="e6ab3-213">level</span></span> |<span data-ttu-id="e6ab3-214">Nivel de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-214">Level of hello event.</span></span> <span data-ttu-id="e6ab3-215">Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose"</span><span class="sxs-lookup"><span data-stu-id="e6ab3-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="e6ab3-216">location</span><span class="sxs-lookup"><span data-stu-id="e6ab3-216">location</span></span> |<span data-ttu-id="e6ab3-217">Región de la ubicación que Hola ocurrida (o global).</span><span class="sxs-lookup"><span data-stu-id="e6ab3-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="e6ab3-218">propiedades</span><span class="sxs-lookup"><span data-stu-id="e6ab3-218">properties</span></span> |<span data-ttu-id="e6ab3-219">Conjunto de `<Key, Value>` pares (es decir, diccionario) que se describen los detalles de Hola de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="e6ab3-220">propiedades de Hola y el uso de estas propiedades pueden variar dependiendo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6ab3-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e6ab3-221">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6ab3-221">Next steps</span></span>
* [<span data-ttu-id="e6ab3-222">Descargar blobs para el análisis</span><span class="sxs-lookup"><span data-stu-id="e6ab3-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="e6ab3-223">Transmitir tooEvent de registro de actividad de hello centros</span><span class="sxs-lookup"><span data-stu-id="e6ab3-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="e6ab3-224">Obtenga más información acerca de hello registro de actividad</span><span class="sxs-lookup"><span data-stu-id="e6ab3-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

