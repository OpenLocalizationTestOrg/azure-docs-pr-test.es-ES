---
title: "aaaUsing API de REST de alerta de análisis de registros de OMS"
description: "Hola API de REST de alerta de análisis de registros permite toocreate y administrar las alertas en los análisis de registros que forma parte de Operations Management Suite (OMS).  Este artículo proporciona detalles de la API de Hola y varios ejemplos para realizar diferentes operaciones."
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
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="6f034-104">Creación y administración de reglas de alerta de Log Analytics con la API de REST</span><span class="sxs-lookup"><span data-stu-id="6f034-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="6f034-105">Hola API de REST de alerta de análisis de registros permite toocreate y administrar alertas de Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="6f034-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="6f034-106">Este artículo proporciona detalles de la API de Hola y varios ejemplos para realizar diferentes operaciones.</span><span class="sxs-lookup"><span data-stu-id="6f034-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="6f034-107">Hola API de REST de búsqueda de análisis de registros es RESTful y son accesibles a través de hello API de REST del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f034-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="6f034-108">En este documento encontrará ejemplos donde se accede a Hola API desde una línea de comandos de PowerShell con [ARMClient](https://github.com/projectkudu/ARMClient), una herramienta de línea de comandos de código abierto que simplifica la invocación Hola API del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f034-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="6f034-109">uso de Hola de ARMClient y PowerShell es una de muchas opciones tooaccess Hola API de búsqueda de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="6f034-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="6f034-110">Con estas herramientas pueden usar áreas de trabajo de hello API del Administrador de recursos de Azure RESTful toomake llamadas tooOMS y ejecutar comandos de búsqueda dentro de ellos.</span><span class="sxs-lookup"><span data-stu-id="6f034-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="6f034-111">Hola API darán como resultado tooyou de resultados de búsqueda en formato JSON, permitiéndole toouse resultados de la búsqueda de Hola de muchas formas distintas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f034-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6f034-112">Prerequisites</span></span>
<span data-ttu-id="6f034-113">Actualmente, solo se pueden crear alertas con una búsqueda guardada en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6f034-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="6f034-114">Puede hacer referencia a toohello [API de REST de búsqueda de registros](log-analytics-log-search-api.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="6f034-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="6f034-115">Programaciones</span><span class="sxs-lookup"><span data-stu-id="6f034-115">Schedules</span></span>
<span data-ttu-id="6f034-116">Una búsqueda guardada puede tener una o varias programaciones.</span><span class="sxs-lookup"><span data-stu-id="6f034-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="6f034-117">Hello programación define la frecuencia con hello búsqueda se ejecuta y se identifica el intervalo de tiempo de hello en los criterios que Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="6f034-118">Programaciones tienen propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f034-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="6f034-119">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6f034-119">Property</span></span> | <span data-ttu-id="6f034-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="6f034-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f034-121">Intervalo</span><span class="sxs-lookup"><span data-stu-id="6f034-121">Interval</span></span> |<span data-ttu-id="6f034-122">¿Con qué frecuencia hello búsqueda se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="6f034-122">How often hello search is run.</span></span> <span data-ttu-id="6f034-123">Se mide en minutos.</span><span class="sxs-lookup"><span data-stu-id="6f034-123">Measured in minutes.</span></span> |
| <span data-ttu-id="6f034-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="6f034-124">QueryTimeSpan</span></span> |<span data-ttu-id="6f034-125">intervalo de tiempo de Hello sobre qué Hola se evalúa los criterios.</span><span class="sxs-lookup"><span data-stu-id="6f034-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="6f034-126">Debe ser igual tooor mayor intervalo.</span><span class="sxs-lookup"><span data-stu-id="6f034-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="6f034-127">Se mide en minutos.</span><span class="sxs-lookup"><span data-stu-id="6f034-127">Measured in minutes.</span></span> |
| <span data-ttu-id="6f034-128">Versión</span><span class="sxs-lookup"><span data-stu-id="6f034-128">Version</span></span> |<span data-ttu-id="6f034-129">Hola versión de API que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="6f034-129">hello API version being used.</span></span>  <span data-ttu-id="6f034-130">Actualmente, esto siempre se debe establecer too1.</span><span class="sxs-lookup"><span data-stu-id="6f034-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="6f034-131">Por ejemplo, en una consulta de evento con un valor de Intervalo de 15 minutos y un valor de Timespan de 30 minutos,</span><span class="sxs-lookup"><span data-stu-id="6f034-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="6f034-132">En este caso, se ejecutaría consulta Hola cada 15 minutos, y se desencadenará una alerta si los criterios de hello sigue tooresolve tootrue durante un período de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="6f034-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="6f034-133">Recuperar programaciones</span><span class="sxs-lookup"><span data-stu-id="6f034-133">Retrieving schedules</span></span>
<span data-ttu-id="6f034-134">Hola uso obtener método tooretrieve todas las programaciones de una búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="6f034-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="6f034-135">Hola de uso obtener una programación determinada de una búsqueda guardada de método con un tooretrieve de Id. de programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="6f034-136">La siguiente es una respuesta de ejemplo de una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="6f034-137">Creación de una programación</span><span class="sxs-lookup"><span data-stu-id="6f034-137">Creating a schedule</span></span>
<span data-ttu-id="6f034-138">Utilice el método de Put de hello con un toocreate de identificador de programación único una nueva programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="6f034-139">Tenga en cuenta que dos programaciones no se han Hola mismo identificador incluso si están asociados con diferentes búsquedas guardadas.</span><span class="sxs-lookup"><span data-stu-id="6f034-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="6f034-140">Cuando se crea una programación en la consola de OMS hello, se crea un GUID para el identificador de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="6f034-141">nombre de Hola para búsquedas guardadas, las programaciones y acciones creadas con hello API de análisis de registros debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6f034-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="6f034-142">Edición de una programación</span><span class="sxs-lookup"><span data-stu-id="6f034-142">Editing a schedule</span></span>
<span data-ttu-id="6f034-143">Utilice el método de Put de hello con una programación existente toomodify que la programación de búsqueda de Id. de hello mismo guardado.</span><span class="sxs-lookup"><span data-stu-id="6f034-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="6f034-144">cuerpo de saludo de solicitud de hello debe incluir etag Hola de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="6f034-145">Eliminar programaciones</span><span class="sxs-lookup"><span data-stu-id="6f034-145">Deleting schedules</span></span>
<span data-ttu-id="6f034-146">Utilice el método de eliminación de hello con un toodelete de Id. de programación una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="6f034-147">Acciones</span><span class="sxs-lookup"><span data-stu-id="6f034-147">Actions</span></span>
<span data-ttu-id="6f034-148">Una programación puede tener varias acciones.</span><span class="sxs-lookup"><span data-stu-id="6f034-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="6f034-149">Una acción puede definir uno o más tooperform de procesos, como enviar un correo electrónico o iniciar un runbook, o bien puede definir un umbral que determina si los resultados de saludo de la búsqueda cumplen algunos criterios.</span><span class="sxs-lookup"><span data-stu-id="6f034-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="6f034-150">Algunas acciones definirá dos para que se realicen procesos de hello cuando se alcanza el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="6f034-151">Todas las acciones tienen propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f034-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="6f034-152">Los distintos tipos de alertas tienen diferentes propiedades adicionales, descritas aquí.</span><span class="sxs-lookup"><span data-stu-id="6f034-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="6f034-153">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6f034-153">Property</span></span> | <span data-ttu-id="6f034-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="6f034-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f034-155">Tipo</span><span class="sxs-lookup"><span data-stu-id="6f034-155">Type</span></span> |<span data-ttu-id="6f034-156">Tipo de acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-156">Type of hello action.</span></span>  <span data-ttu-id="6f034-157">Actualmente los valores posibles de hello son alerta y Webhook.</span><span class="sxs-lookup"><span data-stu-id="6f034-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="6f034-158">Nombre</span><span class="sxs-lookup"><span data-stu-id="6f034-158">Name</span></span> |<span data-ttu-id="6f034-159">Nombre para mostrar de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="6f034-160">Versión</span><span class="sxs-lookup"><span data-stu-id="6f034-160">Version</span></span> |<span data-ttu-id="6f034-161">Hola versión de API que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="6f034-161">hello API version being used.</span></span>  <span data-ttu-id="6f034-162">Actualmente, esto siempre se debe establecer too1.</span><span class="sxs-lookup"><span data-stu-id="6f034-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="6f034-163">Recuperar acciones</span><span class="sxs-lookup"><span data-stu-id="6f034-163">Retrieving actions</span></span>
<span data-ttu-id="6f034-164">Hola uso obtener método tooretrieve todas las acciones de una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="6f034-165">Hola uso obtener método con tooretrieve de Id. de acción de hello una acción concreta para una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="6f034-166">Crear o editar acciones</span><span class="sxs-lookup"><span data-stu-id="6f034-166">Creating or editing actions</span></span>
<span data-ttu-id="6f034-167">Utilice el método Put de hello con un identificador de acción que es único toohello programación toocreate una nueva acción.</span><span class="sxs-lookup"><span data-stu-id="6f034-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="6f034-168">Cuando se crea una acción en la consola de OMS hello, un GUID es para hello Id. de acción.</span><span class="sxs-lookup"><span data-stu-id="6f034-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="6f034-169">nombre de Hola para búsquedas guardadas, las programaciones y acciones creadas con hello API de análisis de registros debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6f034-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="6f034-170">Utilice el método Put de hello con una Id. de hello mismo guardado buscar toomodify que la programación de acciones existente.</span><span class="sxs-lookup"><span data-stu-id="6f034-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="6f034-171">cuerpo de saludo de solicitud de hello debe incluir etag Hola de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="6f034-172">formato de solicitud de Hola para crear una nueva acción varía según el tipo de acción para que estos ejemplos se proporcionan en secciones de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="6f034-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="6f034-173">Eliminar acciones</span><span class="sxs-lookup"><span data-stu-id="6f034-173">Deleting actions</span></span>
<span data-ttu-id="6f034-174">Utilice el método de eliminación de hello con toodelete de Id. de acción de hello una acción.</span><span class="sxs-lookup"><span data-stu-id="6f034-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="6f034-175">Acciones de alerta</span><span class="sxs-lookup"><span data-stu-id="6f034-175">Alert Actions</span></span>
<span data-ttu-id="6f034-176">Una programación debe tener una acción de alerta única y exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="6f034-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="6f034-177">Acciones de alerta tienen una o varias de las secciones de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f034-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="6f034-178">Cada una de ellas se describe con más detalle abajo.</span><span class="sxs-lookup"><span data-stu-id="6f034-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="6f034-179">Sección</span><span class="sxs-lookup"><span data-stu-id="6f034-179">Section</span></span> | <span data-ttu-id="6f034-180">Descripción</span><span class="sxs-lookup"><span data-stu-id="6f034-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f034-181">Umbral</span><span class="sxs-lookup"><span data-stu-id="6f034-181">Threshold</span></span> |<span data-ttu-id="6f034-182">Criterios cuando se ejecuta la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="6f034-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="6f034-183">EmailNotification</span></span> |<span data-ttu-id="6f034-184">Enviar correo electrónico de destinatarios toomultiple.</span><span class="sxs-lookup"><span data-stu-id="6f034-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="6f034-185">Corrección</span><span class="sxs-lookup"><span data-stu-id="6f034-185">Remediation</span></span> |<span data-ttu-id="6f034-186">Iniciar un runbook en automatización de Azure tooattempt toocorrect había identificado el problema.</span><span class="sxs-lookup"><span data-stu-id="6f034-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="6f034-187">Umbrales</span><span class="sxs-lookup"><span data-stu-id="6f034-187">Thresholds</span></span>
<span data-ttu-id="6f034-188">Una acción de alerta debe tener un umbral única y exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="6f034-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="6f034-189">Cuando los resultados de Hola de una búsqueda guardada coincide con umbral de hello en una acción asociada que la búsqueda, se ejecutan los demás procesos en esa acción.</span><span class="sxs-lookup"><span data-stu-id="6f034-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="6f034-190">Una acción también puede contener solo un umbral para que pueda usarse con acciones de otros tipos que no contienen umbrales.</span><span class="sxs-lookup"><span data-stu-id="6f034-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="6f034-191">Umbrales tienen propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f034-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="6f034-192">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6f034-192">Property</span></span> | <span data-ttu-id="6f034-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="6f034-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f034-194">operador</span><span class="sxs-lookup"><span data-stu-id="6f034-194">Operator</span></span> |<span data-ttu-id="6f034-195">Operador de comparación de umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="6f034-196">gt = Mayor que</span><span class="sxs-lookup"><span data-stu-id="6f034-196">gt = Greater Than</span></span> <br> <span data-ttu-id="6f034-197"> lt = Menor que</span><span class="sxs-lookup"><span data-stu-id="6f034-197">lt = Less Than</span></span> |
| <span data-ttu-id="6f034-198">Valor</span><span class="sxs-lookup"><span data-stu-id="6f034-198">Value</span></span> |<span data-ttu-id="6f034-199">Valor de umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-199">Value for hello threshold.</span></span> |

<span data-ttu-id="6f034-200">Por ejemplo, en una consulta de evento con un valor de Intervalo de 15 minutos, un valor de Timespan de 30 minutos y un valor de Threshold mayor que 10,</span><span class="sxs-lookup"><span data-stu-id="6f034-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="6f034-201">En este caso, se ejecutaría consulta Hola cada 15 minutos, y se desencadenará una alerta si devuelven 10 eventos que se crearon durante un período de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="6f034-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="6f034-202">La siguiente es una respuesta de ejemplo de una acción con un solo umbral.</span><span class="sxs-lookup"><span data-stu-id="6f034-202">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="6f034-203">Utilice el método de Put de hello con un toocreate de Id. de acción única una nueva acción de umbral para una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="6f034-204">Utilice el método de Put de hello con un toomodify de Id. de acción existente una acción de umbral para una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="6f034-205">cuerpo de saludo de solicitud de hello debe incluir etag Hola de acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="6f034-206">Notificación por correo electrónico</span><span class="sxs-lookup"><span data-stu-id="6f034-206">Email Notification</span></span>
<span data-ttu-id="6f034-207">Notificaciones de correo electrónico envían correo electrónico tooone o más destinatarios.</span><span class="sxs-lookup"><span data-stu-id="6f034-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="6f034-208">Incluyen propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f034-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="6f034-209">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6f034-209">Property</span></span> | <span data-ttu-id="6f034-210">Descripción</span><span class="sxs-lookup"><span data-stu-id="6f034-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f034-211">Recipients</span><span class="sxs-lookup"><span data-stu-id="6f034-211">Recipients</span></span> |<span data-ttu-id="6f034-212">Lista de direcciones de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="6f034-212">List of mail addresses.</span></span> |
| <span data-ttu-id="6f034-213">Asunto</span><span class="sxs-lookup"><span data-stu-id="6f034-213">Subject</span></span> |<span data-ttu-id="6f034-214">asunto Hola de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="6f034-215">Datos adjuntos</span><span class="sxs-lookup"><span data-stu-id="6f034-215">Attachment</span></span> |<span data-ttu-id="6f034-216">Actualmente no se admiten datos adjuntos, por lo que siempre aparecerá un valor “None”.</span><span class="sxs-lookup"><span data-stu-id="6f034-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="6f034-217">La siguiente es una respuesta de ejemplo de una acción de notificación de correo con un umbral.</span><span class="sxs-lookup"><span data-stu-id="6f034-217">Following is a sample response for an email notification action with a threshold.</span></span>  

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
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="6f034-218">Utilice el método de Put de hello con un toocreate de Id. de acción única una nueva acción de correo electrónico para una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="6f034-219">Hello en el ejemplo siguiente se crea una notificación por correo electrónico con un umbral para que se envía correo de hello cuando los resultados de Hola de hello búsqueda guardada superan el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="6f034-220">Utilice el método de Put de hello con un toomodify de Id. de acción una acción de correo electrónico existente para una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="6f034-221">cuerpo de saludo de solicitud de hello debe incluir etag Hola de acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="6f034-222">Acciones de corrección</span><span class="sxs-lookup"><span data-stu-id="6f034-222">Remediation actions</span></span>
<span data-ttu-id="6f034-223">Correcciones de iniciar un runbook en automatización de Azure que intente problema de hello toocorrect identificado por la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="6f034-224">Debe crear un webhook de runbook de hello utilizado en una acción de corrección y, a continuación, especificar URI Hola Hola WebhookUri propiedad.</span><span class="sxs-lookup"><span data-stu-id="6f034-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="6f034-225">Cuando se crea esta acción mediante la consola de OMS de hello, se crea automáticamente un webhook nuevo runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="6f034-226">Correcciones incluyen las propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f034-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="6f034-227">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6f034-227">Property</span></span> | <span data-ttu-id="6f034-228">Descripción</span><span class="sxs-lookup"><span data-stu-id="6f034-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f034-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="6f034-229">RunbookName</span></span> |<span data-ttu-id="6f034-230">Nombre de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-230">Name of hello runbook.</span></span> <span data-ttu-id="6f034-231">Debe coincidir con un runbook publicado en la cuenta de automatización de hello configurado en hello solución de automatización en el área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="6f034-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="6f034-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="6f034-232">WebhookUri</span></span> |<span data-ttu-id="6f034-233">URI de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="6f034-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="6f034-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="6f034-234">Expiry</span></span> |<span data-ttu-id="6f034-235">fecha de expiración de Hola y la hora de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="6f034-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="6f034-236">Si hello webhook no tiene una expiración, esto puede ser cualquier fecha futura válido.</span><span class="sxs-lookup"><span data-stu-id="6f034-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="6f034-237">La siguiente es una respuesta de ejemplo de una acción de corrección con un umbral.</span><span class="sxs-lookup"><span data-stu-id="6f034-237">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="6f034-238">Utilice el método de Put de hello con un toocreate de Id. de acción única una nueva acción de corrección para una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="6f034-239">Hello en el ejemplo siguiente se crea una solución con un umbral para que hello runbook se inicia cuando los resultados de Hola de hello búsqueda guardada sobrepasan el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="6f034-240">Utilice el método de Put de hello con un toomodify de Id. de acción existente una acción correctora para una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="6f034-241">cuerpo de saludo de solicitud de hello debe incluir etag Hola de acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="6f034-242">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6f034-242">Example</span></span>
<span data-ttu-id="6f034-243">Aquí te mostramos una toocreate una nueva alerta de correo electrónico de ejemplo completo.</span><span class="sxs-lookup"><span data-stu-id="6f034-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="6f034-244">En él, se crea una programación junto con una acción que contiene un umbral y un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="6f034-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="6f034-245">Acciones de webhook</span><span class="sxs-lookup"><span data-stu-id="6f034-245">Webhook actions</span></span>
<span data-ttu-id="6f034-246">Acciones de Webhook iniciar un proceso mediante una llamada a una dirección URL y, opcionalmente, proporcionar un toobe de carga que envía.</span><span class="sxs-lookup"><span data-stu-id="6f034-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="6f034-247">Únicamente son acciones similares de tooRemediation salvo que están concebidos para webhooks que puede invocar procesos distintos de runbooks de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f034-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="6f034-248">También proporcionan opción adicional de Hola de proporcionar un proceso de carga toobe entregado toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="6f034-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="6f034-249">Acciones de Webhook no tiene un umbral, pero en su lugar, se deben agregar programación tooa que tiene una acción con un umbral de alerta.</span><span class="sxs-lookup"><span data-stu-id="6f034-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="6f034-250">Puede agregar varias acciones de Webhook que todos se ejecutará cuando se cumpla el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="6f034-251">Acciones de Webhook incluyen las propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f034-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="6f034-252">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6f034-252">Property</span></span> | <span data-ttu-id="6f034-253">Descripción</span><span class="sxs-lookup"><span data-stu-id="6f034-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6f034-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="6f034-254">WebhookUri</span></span> |<span data-ttu-id="6f034-255">asunto Hola de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="6f034-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="6f034-256">CustomPayload</span></span> |<span data-ttu-id="6f034-257">Carga personalizada toobe enviado toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="6f034-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="6f034-258">formato de Hello dependerá de qué webhook Hola está esperando.</span><span class="sxs-lookup"><span data-stu-id="6f034-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="6f034-259">La siguiente es una respuesta de ejemplo de una acción de webhook y una acción de alerta asociada con un umbral.</span><span class="sxs-lookup"><span data-stu-id="6f034-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="6f034-260">Crear o editar una acción de webhook</span><span class="sxs-lookup"><span data-stu-id="6f034-260">Create or edit a webhook action</span></span>
<span data-ttu-id="6f034-261">Utilice el método de Put de hello con un toocreate de Id. de acción única una nueva acción de webhook para una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="6f034-262">Hello en el ejemplo siguiente se crea una acción de Webhook y una acción de alerta con un umbral de modo que hello webhook se desencadenará cuando los resultados de Hola de hello búsqueda guardada sobrepasan el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="6f034-263">Utilice el método de Put de hello con un toomodify de Id. de acción existente una acción de webhook para una programación.</span><span class="sxs-lookup"><span data-stu-id="6f034-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="6f034-264">cuerpo de saludo de solicitud de hello debe incluir etag Hola de acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f034-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="6f034-265">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6f034-265">Next steps</span></span>
* <span data-ttu-id="6f034-266">Hola de uso [búsquedas de registros de API de REST tooperform](log-analytics-log-search-api.md) en análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="6f034-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

