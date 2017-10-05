---
title: Uso de la API de REST de alertas de Log Analytics de OMS
description: "Con la API de REST de alertas de Log Analytics se pueden crear y administrar alertas de Log Analytics, que forma parte de Operations Management Suite (OMS).  En este artículo encontrará información detallada sobre la API y varios ejemplos para realizar distintas operaciones."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5ce72ffef4394bf3bbe39fa420c4fcaa965ae35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="c71c9-104">Creación y administración de reglas de alerta de Log Analytics con la API de REST</span><span class="sxs-lookup"><span data-stu-id="c71c9-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="c71c9-105">Con la API de REST de alertas de Log Analytics se pueden crear y administrar alertas de Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="c71c9-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="c71c9-106">En este artículo encontrará información detallada sobre la API y varios ejemplos para realizar distintas operaciones.</span><span class="sxs-lookup"><span data-stu-id="c71c9-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="c71c9-107">La API de REST de búsqueda de Log Analytics es de tipo RESTful y se puede obtener acceso a ella a través de la API de REST de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c71c9-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="c71c9-108">En este documento encontrará ejemplos donde se tiene acceso a la API desde una línea de comandos de PowerShell a través de [ARMClient](https://github.com/projectkudu/ARMClient), una herramienta de línea de comandos de código abierto que simplifica la tarea de invocar a la API de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c71c9-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="c71c9-109">El uso de ARMClient y PowerShell es una de las muchas opciones para tener acceso a la API de búsqueda de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c71c9-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="c71c9-110">Con estas herramientas, puede usar la API de Azure Resource Manager de RESTful para realizar llamadas a las áreas de trabajo de OMS y ejecutar comandos de búsqueda dentro de ellas.</span><span class="sxs-lookup"><span data-stu-id="c71c9-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="c71c9-111">La API generará resultados de búsqueda, en formato JSON, lo que le permite usar los resultados de búsqueda de muchas formas distintas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c71c9-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c71c9-112">Prerequisites</span></span>
<span data-ttu-id="c71c9-113">Actualmente, solo se pueden crear alertas con una búsqueda guardada en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c71c9-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="c71c9-114">Para obtener más información, consulte [API de búsqueda de registros de Log Analytics](log-analytics-log-search-api.md) .</span><span class="sxs-lookup"><span data-stu-id="c71c9-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="c71c9-115">Programaciones</span><span class="sxs-lookup"><span data-stu-id="c71c9-115">Schedules</span></span>
<span data-ttu-id="c71c9-116">Una búsqueda guardada puede tener una o varias programaciones.</span><span class="sxs-lookup"><span data-stu-id="c71c9-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="c71c9-117">La programación define la frecuencia con que se realiza la búsqueda y el intervalo de tiempo en el que se identifican los criterios.</span><span class="sxs-lookup"><span data-stu-id="c71c9-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="c71c9-118">Las programaciones tienen las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="c71c9-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="c71c9-119">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c71c9-119">Property</span></span> | <span data-ttu-id="c71c9-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="c71c9-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c71c9-121">Intervalo</span><span class="sxs-lookup"><span data-stu-id="c71c9-121">Interval</span></span> |<span data-ttu-id="c71c9-122">Frecuencia con que se realiza la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c71c9-122">How often the search is run.</span></span> <span data-ttu-id="c71c9-123">Se mide en minutos.</span><span class="sxs-lookup"><span data-stu-id="c71c9-123">Measured in minutes.</span></span> |
| <span data-ttu-id="c71c9-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="c71c9-124">QueryTimeSpan</span></span> |<span data-ttu-id="c71c9-125">Intervalo de tiempo en el que se evalúan los criterios.</span><span class="sxs-lookup"><span data-stu-id="c71c9-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="c71c9-126">Debe ser igual o mayor que Intervalo.</span><span class="sxs-lookup"><span data-stu-id="c71c9-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="c71c9-127">Se mide en minutos.</span><span class="sxs-lookup"><span data-stu-id="c71c9-127">Measured in minutes.</span></span> |
| <span data-ttu-id="c71c9-128">Versión</span><span class="sxs-lookup"><span data-stu-id="c71c9-128">Version</span></span> |<span data-ttu-id="c71c9-129">Versión de API en uso.</span><span class="sxs-lookup"><span data-stu-id="c71c9-129">The API version being used.</span></span>  <span data-ttu-id="c71c9-130">Actualmente, siempre debe estar establecida en 1.</span><span class="sxs-lookup"><span data-stu-id="c71c9-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="c71c9-131">Por ejemplo, en una consulta de evento con un valor de Intervalo de 15 minutos y un valor de Timespan de 30 minutos,</span><span class="sxs-lookup"><span data-stu-id="c71c9-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="c71c9-132">la consulta se ejecutaría cada 15 minutos y se desencadenaría una alerta si los criterios siguieran evaluándose como True durante un intervalo de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="c71c9-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="c71c9-133">Recuperar programaciones</span><span class="sxs-lookup"><span data-stu-id="c71c9-133">Retrieving schedules</span></span>
<span data-ttu-id="c71c9-134">Use el método Get para recuperar todas las programaciones de una búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="c71c9-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="c71c9-135">Use el método Get con un identificador de programación para recuperar una programación concreta de una búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="c71c9-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="c71c9-136">La siguiente es una respuesta de ejemplo de una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="c71c9-137">Creación de una programación</span><span class="sxs-lookup"><span data-stu-id="c71c9-137">Creating a schedule</span></span>
<span data-ttu-id="c71c9-138">Use el método Put con un identificador de programación único para crear una programación nueva.</span><span class="sxs-lookup"><span data-stu-id="c71c9-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="c71c9-139">Tenga en cuenta que dos programaciones no pueden tener el mismo identificador, aunque estén asociados a diferentes búsquedas guardadas.</span><span class="sxs-lookup"><span data-stu-id="c71c9-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="c71c9-140">Al crear una programación en la consola de OMS, se crea un GUID para el identificador de programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="c71c9-141">El nombre de todas las búsquedas guardadas, programaciones y acciones creadas con Log Analytics API debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c71c9-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="c71c9-142">Edición de una programación</span><span class="sxs-lookup"><span data-stu-id="c71c9-142">Editing a schedule</span></span>
<span data-ttu-id="c71c9-143">Utilice el método Put con un identificador de programación existente para modificar la programación de la misma búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="c71c9-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="c71c9-144">El cuerpo de la solicitud debe incluir el valor etag de la programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-144">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="c71c9-145">Eliminar programaciones</span><span class="sxs-lookup"><span data-stu-id="c71c9-145">Deleting schedules</span></span>
<span data-ttu-id="c71c9-146">Para eliminar una programación, use el método Delete con un identificador de programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-146">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="c71c9-147">Acciones</span><span class="sxs-lookup"><span data-stu-id="c71c9-147">Actions</span></span>
<span data-ttu-id="c71c9-148">Una programación puede tener varias acciones.</span><span class="sxs-lookup"><span data-stu-id="c71c9-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="c71c9-149">Una acción puede definir uno o varios procesos que se van a realizar (como enviar un correo o iniciar un Runbook), o bien puede definir un umbral que determina si los resultados de una búsqueda coinciden con algunos criterios.</span><span class="sxs-lookup"><span data-stu-id="c71c9-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="c71c9-150">Algunas acciones definen ambos aspectos, de forma que los procesos se realizan cuando se alcance el umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-150">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="c71c9-151">Todas las acciones tienen las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="c71c9-151">All actions have the properties in the following table.</span></span>  <span data-ttu-id="c71c9-152">Los distintos tipos de alertas tienen diferentes propiedades adicionales, descritas aquí.</span><span class="sxs-lookup"><span data-stu-id="c71c9-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="c71c9-153">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c71c9-153">Property</span></span> | <span data-ttu-id="c71c9-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="c71c9-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c71c9-155">Tipo</span><span class="sxs-lookup"><span data-stu-id="c71c9-155">Type</span></span> |<span data-ttu-id="c71c9-156">Tipo de la acción.</span><span class="sxs-lookup"><span data-stu-id="c71c9-156">Type of the action.</span></span>  <span data-ttu-id="c71c9-157">Actualmente, los valores posibles son Alert y Webhook.</span><span class="sxs-lookup"><span data-stu-id="c71c9-157">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="c71c9-158">Nombre</span><span class="sxs-lookup"><span data-stu-id="c71c9-158">Name</span></span> |<span data-ttu-id="c71c9-159">Nombre para mostrar de la alerta.</span><span class="sxs-lookup"><span data-stu-id="c71c9-159">Display name for the alert.</span></span> |
| <span data-ttu-id="c71c9-160">Versión</span><span class="sxs-lookup"><span data-stu-id="c71c9-160">Version</span></span> |<span data-ttu-id="c71c9-161">Versión de API en uso.</span><span class="sxs-lookup"><span data-stu-id="c71c9-161">The API version being used.</span></span>  <span data-ttu-id="c71c9-162">Actualmente, siempre debe estar establecida en 1.</span><span class="sxs-lookup"><span data-stu-id="c71c9-162">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="c71c9-163">Recuperar acciones</span><span class="sxs-lookup"><span data-stu-id="c71c9-163">Retrieving actions</span></span>
<span data-ttu-id="c71c9-164">Use el método Get para recuperar todas las acciones de una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-164">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="c71c9-165">Use el método Get con el identificador de una acción para recuperar esa acción concreta para una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-165">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="c71c9-166">Crear o editar acciones</span><span class="sxs-lookup"><span data-stu-id="c71c9-166">Creating or editing actions</span></span>
<span data-ttu-id="c71c9-167">Para crear una acción, use el método Put con un identificador de acción único de la programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-167">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="c71c9-168">Al crear una acción en la consola de OMS, se crea un GUID para el identificador de acción.</span><span class="sxs-lookup"><span data-stu-id="c71c9-168">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="c71c9-169">El nombre de todas las búsquedas guardadas, programaciones y acciones creadas con Log Analytics API debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c71c9-169">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="c71c9-170">Utilice el método Put con un identificador de acción existente para modificar la programación de la misma búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="c71c9-170">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="c71c9-171">El cuerpo de la solicitud debe incluir el valor etag de la programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-171">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="c71c9-172">El formato de solicitud para crear una acción varía según el tipo de acción. En las secciones siguientes se proporcionan ejemplos.</span><span class="sxs-lookup"><span data-stu-id="c71c9-172">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="c71c9-173">Eliminar acciones</span><span class="sxs-lookup"><span data-stu-id="c71c9-173">Deleting actions</span></span>
<span data-ttu-id="c71c9-174">Use el método Delete con el identificador de acción para eliminar esa acción.</span><span class="sxs-lookup"><span data-stu-id="c71c9-174">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="c71c9-175">Acciones de alerta</span><span class="sxs-lookup"><span data-stu-id="c71c9-175">Alert Actions</span></span>
<span data-ttu-id="c71c9-176">Una programación debe tener una acción de alerta única y exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="c71c9-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="c71c9-177">Las acciones de alerta tienen una o varias de las secciones de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="c71c9-177">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="c71c9-178">Cada una de ellas se describe con más detalle abajo.</span><span class="sxs-lookup"><span data-stu-id="c71c9-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="c71c9-179">Sección</span><span class="sxs-lookup"><span data-stu-id="c71c9-179">Section</span></span> | <span data-ttu-id="c71c9-180">Descripción</span><span class="sxs-lookup"><span data-stu-id="c71c9-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c71c9-181">Umbral</span><span class="sxs-lookup"><span data-stu-id="c71c9-181">Threshold</span></span> |<span data-ttu-id="c71c9-182">Criterios para establecer cuándo se va a ejecutar la acción.</span><span class="sxs-lookup"><span data-stu-id="c71c9-182">Criteria for when the action is run.</span></span> |
| <span data-ttu-id="c71c9-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="c71c9-183">EmailNotification</span></span> |<span data-ttu-id="c71c9-184">Se envía un correo electrónico a varios destinatarios.</span><span class="sxs-lookup"><span data-stu-id="c71c9-184">Send mail to multiple recipients.</span></span> |
| <span data-ttu-id="c71c9-185">Corrección</span><span class="sxs-lookup"><span data-stu-id="c71c9-185">Remediation</span></span> |<span data-ttu-id="c71c9-186">Se inicia un Runbook en Automatización de Azure para intentar corregir el problema detectado.</span><span class="sxs-lookup"><span data-stu-id="c71c9-186">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="c71c9-187">Umbrales</span><span class="sxs-lookup"><span data-stu-id="c71c9-187">Thresholds</span></span>
<span data-ttu-id="c71c9-188">Una acción de alerta debe tener un umbral única y exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="c71c9-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="c71c9-189">Cuando los resultados de una búsqueda guardada coinciden con el umbral de una acción asociada a esa búsqueda, se ejecutan los demás procesos de esa acción.</span><span class="sxs-lookup"><span data-stu-id="c71c9-189">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="c71c9-190">Una acción también puede contener solo un umbral para que pueda usarse con acciones de otros tipos que no contienen umbrales.</span><span class="sxs-lookup"><span data-stu-id="c71c9-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="c71c9-191">Los umbrales tienen las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="c71c9-191">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="c71c9-192">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c71c9-192">Property</span></span> | <span data-ttu-id="c71c9-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="c71c9-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c71c9-194">Operador</span><span class="sxs-lookup"><span data-stu-id="c71c9-194">Operator</span></span> |<span data-ttu-id="c71c9-195">Operador de la comparación de umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-195">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="c71c9-196">gt = Mayor que</span><span class="sxs-lookup"><span data-stu-id="c71c9-196">gt = Greater Than</span></span> <br> <span data-ttu-id="c71c9-197">lt = Menor que</span><span class="sxs-lookup"><span data-stu-id="c71c9-197">lt = Less Than</span></span> |
| <span data-ttu-id="c71c9-198">Valor</span><span class="sxs-lookup"><span data-stu-id="c71c9-198">Value</span></span> |<span data-ttu-id="c71c9-199">Valor del umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-199">Value for the threshold.</span></span> |

<span data-ttu-id="c71c9-200">Por ejemplo, en una consulta de evento con un valor de Intervalo de 15 minutos, un valor de Timespan de 30 minutos y un valor de Threshold mayor que 10,</span><span class="sxs-lookup"><span data-stu-id="c71c9-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="c71c9-201">la consulta se ejecutaría cada 15 minutos y se desencadenaría una alerta si devolviera 10 eventos creados durante un intervalo de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="c71c9-201">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="c71c9-202">La siguiente es una respuesta de ejemplo de una acción con un solo umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="c71c9-203">Use el método Put con un identificador de acción único para crear una acción de umbral para una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-203">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="c71c9-204">Use el método Put con un identificador de acción existente para modificar una acción de umbral para una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-204">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="c71c9-205">El cuerpo de la solicitud debe incluir el valor etag de la acción.</span><span class="sxs-lookup"><span data-stu-id="c71c9-205">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="c71c9-206">Notificación por correo electrónico</span><span class="sxs-lookup"><span data-stu-id="c71c9-206">Email Notification</span></span>
<span data-ttu-id="c71c9-207">Las notificaciones de correo electrónico envían correo a uno o más destinatarios.</span><span class="sxs-lookup"><span data-stu-id="c71c9-207">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="c71c9-208">Tienen las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="c71c9-208">They include the properties in the following table.</span></span>

| <span data-ttu-id="c71c9-209">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c71c9-209">Property</span></span> | <span data-ttu-id="c71c9-210">Descripción</span><span class="sxs-lookup"><span data-stu-id="c71c9-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c71c9-211">Recipients</span><span class="sxs-lookup"><span data-stu-id="c71c9-211">Recipients</span></span> |<span data-ttu-id="c71c9-212">Lista de direcciones de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c71c9-212">List of mail addresses.</span></span> |
| <span data-ttu-id="c71c9-213">Asunto</span><span class="sxs-lookup"><span data-stu-id="c71c9-213">Subject</span></span> |<span data-ttu-id="c71c9-214">Asunto del correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c71c9-214">The subject of the mail.</span></span> |
| <span data-ttu-id="c71c9-215">Datos adjuntos</span><span class="sxs-lookup"><span data-stu-id="c71c9-215">Attachment</span></span> |<span data-ttu-id="c71c9-216">Actualmente no se admiten datos adjuntos, por lo que siempre aparecerá un valor “None”.</span><span class="sxs-lookup"><span data-stu-id="c71c9-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="c71c9-217">La siguiente es una respuesta de ejemplo de una acción de notificación de correo con un umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="c71c9-218">Use el método Put con un identificador de acción único para crear una acción de correo electrónico para una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-218">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="c71c9-219">En el siguiente ejemplo se crea una notificación de correo electrónico con un umbral para que el correo se envíe cuando los resultados de la búsqueda guardada superen el umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-219">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="c71c9-220">Use el método Put con un identificador de acción existente para modificar una acción de correo electrónico para una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-220">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="c71c9-221">El cuerpo de la solicitud debe incluir el valor etag de la acción.</span><span class="sxs-lookup"><span data-stu-id="c71c9-221">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="c71c9-222">Acciones de corrección</span><span class="sxs-lookup"><span data-stu-id="c71c9-222">Remediation actions</span></span>
<span data-ttu-id="c71c9-223">Las correcciones inician un Runbook en Automatización de Azure que intenta corregir el problema identificado por la alerta.</span><span class="sxs-lookup"><span data-stu-id="c71c9-223">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="c71c9-224">Debe crear un webhook para el Runbook usado en una acción de corrección y, luego, especificar el URI en la propiedad WebhookUri.</span><span class="sxs-lookup"><span data-stu-id="c71c9-224">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="c71c9-225">Cuando esta acción se crea con la consola de OMS, se crea automáticamente un nuevo webhook para el Runbook.</span><span class="sxs-lookup"><span data-stu-id="c71c9-225">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

<span data-ttu-id="c71c9-226">Las correcciones tienen las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="c71c9-226">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="c71c9-227">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c71c9-227">Property</span></span> | <span data-ttu-id="c71c9-228">Descripción</span><span class="sxs-lookup"><span data-stu-id="c71c9-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c71c9-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="c71c9-229">RunbookName</span></span> |<span data-ttu-id="c71c9-230">Nombre del Runbook.</span><span class="sxs-lookup"><span data-stu-id="c71c9-230">Name of the runbook.</span></span> <span data-ttu-id="c71c9-231">Debe coincidir con un Runbook publicado en la cuenta de automatización que configuró en la solución de Automatización en el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="c71c9-231">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="c71c9-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="c71c9-232">WebhookUri</span></span> |<span data-ttu-id="c71c9-233">URI del webhook.</span><span class="sxs-lookup"><span data-stu-id="c71c9-233">URI of the webhook.</span></span> |
| <span data-ttu-id="c71c9-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="c71c9-234">Expiry</span></span> |<span data-ttu-id="c71c9-235">Fecha y hora de expiración del webhook.</span><span class="sxs-lookup"><span data-stu-id="c71c9-235">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="c71c9-236">Si el webhook no tiene una fecha expiración, puede ser cualquier fecha futura válida.</span><span class="sxs-lookup"><span data-stu-id="c71c9-236">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="c71c9-237">La siguiente es una respuesta de ejemplo de una acción de corrección con un umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="c71c9-238">Use el método Put con un identificador de acción único para crear una acción de corrección para una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-238">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="c71c9-239">En el siguiente ejemplo se crea una corrección con un umbral para que el Runbook se inicie cuando los resultados de la búsqueda guardada superen el umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-239">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="c71c9-240">Use el método Put con un identificador de acción existente para modificar una acción de corrección para una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-240">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="c71c9-241">El cuerpo de la solicitud debe incluir el valor etag de la acción.</span><span class="sxs-lookup"><span data-stu-id="c71c9-241">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="c71c9-242">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c71c9-242">Example</span></span>
<span data-ttu-id="c71c9-243">El siguiente es un ejemplo completo que ilustra cómo crear una alerta de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c71c9-243">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="c71c9-244">En él, se crea una programación junto con una acción que contiene un umbral y un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c71c9-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="c71c9-245">Acciones de webhook</span><span class="sxs-lookup"><span data-stu-id="c71c9-245">Webhook actions</span></span>
<span data-ttu-id="c71c9-246">Las acciones de webhook inician un proceso llamando a una dirección URL y, opcionalmente, proporcionando una carga que se va a enviar.</span><span class="sxs-lookup"><span data-stu-id="c71c9-246">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="c71c9-247">Son similares a las acciones de corrección, salvo por el hecho de que están pensadas para webhooks que pueden invocar procesos que no tienen que ver con Runbooks de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="c71c9-247">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="c71c9-248">También ofrecen la posibilidad extra de proporcionar una carga adicional para entregarla en el proceso remoto.</span><span class="sxs-lookup"><span data-stu-id="c71c9-248">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="c71c9-249">Las acciones de webhook no tienen umbral, sino que deben agregarse a una programación que tenga una acción de alerta con un umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-249">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="c71c9-250">Se pueden agregar varias acciones de webhook, y todas ellas se ejecutarán cuando se alcance el umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-250">You can add multiple Webhook actions that will all be run when the threshold is met.</span></span>

<span data-ttu-id="c71c9-251">Las acciones de webhook tienen las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="c71c9-251">Webhook actions include the properties in the following table.</span></span>

| <span data-ttu-id="c71c9-252">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c71c9-252">Property</span></span> | <span data-ttu-id="c71c9-253">Descripción</span><span class="sxs-lookup"><span data-stu-id="c71c9-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c71c9-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="c71c9-254">WebhookUri</span></span> |<span data-ttu-id="c71c9-255">Asunto del correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c71c9-255">The subject of the mail.</span></span> |
| <span data-ttu-id="c71c9-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="c71c9-256">CustomPayload</span></span> |<span data-ttu-id="c71c9-257">Carga personalizada que se va a enviar al webhook.</span><span class="sxs-lookup"><span data-stu-id="c71c9-257">Custom payload to be sent to the webhook.</span></span>  <span data-ttu-id="c71c9-258">El formato dependerá de lo que el webhook espere.</span><span class="sxs-lookup"><span data-stu-id="c71c9-258">The format will depend on what the webhook is expecting.</span></span> |

<span data-ttu-id="c71c9-259">La siguiente es una respuesta de ejemplo de una acción de webhook y una acción de alerta asociada con un umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="c71c9-260">Crear o editar una acción de webhook</span><span class="sxs-lookup"><span data-stu-id="c71c9-260">Create or edit a webhook action</span></span>
<span data-ttu-id="c71c9-261">Use el método Put con un identificador de acción único para crear una acción de webhook para una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-261">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="c71c9-262">En el siguiente ejemplo se crea una acción de webhook y una acción de alerta con un umbral para que el webhook se active cuando los resultados de la búsqueda guardada superen el umbral.</span><span class="sxs-lookup"><span data-stu-id="c71c9-262">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="c71c9-263">Use el método Put con un identificador de acción existente para modificar una acción de webhook para una programación.</span><span class="sxs-lookup"><span data-stu-id="c71c9-263">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="c71c9-264">El cuerpo de la solicitud debe incluir el valor etag de la acción.</span><span class="sxs-lookup"><span data-stu-id="c71c9-264">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="c71c9-265">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c71c9-265">Next steps</span></span>
* <span data-ttu-id="c71c9-266">Use la [API de búsqueda de registros de Log Analytics](log-analytics-log-search-api.md) en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c71c9-266">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

