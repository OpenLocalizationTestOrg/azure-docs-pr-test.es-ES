---
title: "Búsquedas y alertas guardadas en soluciones de OMS | Microsoft Docs"
description: "Las soluciones de OMS suelen incluir búsquedas guardadas en Log Analytics para analizar los datos recopilados por la solución.  Pueden definir asimismo alertas para notificar al usuario o realizar automáticamente una acción en respuesta a un problema crítico.  En este artículo se describe cómo definir las búsquedas y alertas guardadas de Log Analytics en una plantilla de ARM para que puedan incluirse en soluciones de administración."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a><span data-ttu-id="fb638-105">Incorporación de las búsquedas y las alertas guardadas de Log Analytics en la solución de administración de OMS (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="fb638-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="fb638-106">La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar.</span><span class="sxs-lookup"><span data-stu-id="fb638-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="fb638-107">Cualquier esquema descrito a continuación está sujeto a cambios.</span><span class="sxs-lookup"><span data-stu-id="fb638-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="fb638-108">Las [soluciones de administración de OMS](operations-management-suite-solutions.md) suelen incluir [búsquedas guardadas](../log-analytics/log-analytics-log-searches.md) en Log Analytics para analizar los datos recopilados por la solución.</span><span class="sxs-lookup"><span data-stu-id="fb638-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="fb638-109">Pueden definir asimismo [alertas](../log-analytics/log-analytics-alerts.md) para notificar al usuario o realizar automáticamente una acción en respuesta a un problema crítico.</span><span class="sxs-lookup"><span data-stu-id="fb638-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="fb638-110">En este artículo se describe cómo definir las búsquedas y alertas guardadas de Log Analytics en una [plantilla de Resource Management](../resource-manager-template-walkthrough.md) para que puedan incluirse en [soluciones de administración](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="fb638-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fb638-111">En los ejemplos de este artículo se usan parámetros y variables que son necesarios o comunes para las soluciones de administración y se describen en [Creating management solutions in Operations Management Suite (OMS) (Creación de soluciones de administración en Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="fb638-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="fb638-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb638-112">Prerequisites</span></span>
<span data-ttu-id="fb638-113">En este artículo se supone que ya está familiarizado con la manera de [crear una solución de administración](operations-management-suite-solutions-creating.md) y la estructura de una [plantilla de ARM](../resource-group-authoring-templates.md) y un archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="fb638-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="fb638-114">Área de trabajo de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fb638-114">Log Analytics Workspace</span></span>
<span data-ttu-id="fb638-115">Todos los recursos de Log Analytics están contenidos en un [área de trabajo](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="fb638-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="fb638-116">Como se describe en [el área de trabajo de OMS y la cuenta de Automation](operations-management-suite-solutions.md#oms-workspace-and-automation-account), el área de trabajo no está incluido en la solución de administración pero debe existir antes de que se instale la solución.</span><span class="sxs-lookup"><span data-stu-id="fb638-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="fb638-117">Si no está disponible, se producirá un error en la instalación de la solución.</span><span class="sxs-lookup"><span data-stu-id="fb638-117">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="fb638-118">El nombre del área de trabajo es el nombre de cada recurso de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb638-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="fb638-119">Esto se hace en la solución con el parámetro **workspace** tal como se muestra en el siguiente ejemplo de un recurso de savedsearch.</span><span class="sxs-lookup"><span data-stu-id="fb638-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="fb638-120">Búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="fb638-120">Saved Searches</span></span>
<span data-ttu-id="fb638-121">Incluya [búsquedas guardadas](../log-analytics/log-analytics-log-searches.md) en una solución para permitir a los usuarios consultar los datos recopilados por la solución.</span><span class="sxs-lookup"><span data-stu-id="fb638-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="fb638-122">Las búsquedas guardadas aparecerán en **Favoritos** en el portal de OMS y en **Búsquedas guardadas** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fb638-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span></span>  <span data-ttu-id="fb638-123">También es necesaria una búsqueda guardada para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="fb638-124">Los recursos de [búsquedas guardadas de Log Analytics](../log-analytics/log-analytics-log-searches.md) tienen un tipo de `Microsoft.OperationalInsights/workspaces/savedSearches` y presentan la siguiente estructura.</span><span class="sxs-lookup"><span data-stu-id="fb638-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span>  <span data-ttu-id="fb638-125">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="fb638-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="fb638-126">En la tabla siguiente se describe cada una de las propiedades de una búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="fb638-126">Each of the properties of a saved search are described in the following table.</span></span> 

| <span data-ttu-id="fb638-127">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fb638-127">Property</span></span> | <span data-ttu-id="fb638-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fb638-129">categoría</span><span class="sxs-lookup"><span data-stu-id="fb638-129">category</span></span> | <span data-ttu-id="fb638-130">Categoría de la búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="fb638-130">The category for the saved search.</span></span>  <span data-ttu-id="fb638-131">Las búsquedas guardadas en la misma solución comparten a menudo una única categoría por lo que están agrupadas juntas en la consola.</span><span class="sxs-lookup"><span data-stu-id="fb638-131">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="fb638-132">displayname</span><span class="sxs-lookup"><span data-stu-id="fb638-132">displayname</span></span> | <span data-ttu-id="fb638-133">Nombre para mostrar de la búsqueda guardada en el portal.</span><span class="sxs-lookup"><span data-stu-id="fb638-133">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="fb638-134">query</span><span class="sxs-lookup"><span data-stu-id="fb638-134">query</span></span> | <span data-ttu-id="fb638-135">La consulta que se ejecutará.</span><span class="sxs-lookup"><span data-stu-id="fb638-135">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="fb638-136">Puede que necesite utilizar caracteres de escape en la consulta si incluye caracteres que puedan interpretarse como JSON.</span><span class="sxs-lookup"><span data-stu-id="fb638-136">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="fb638-137">Por ejemplo, si la consulta era **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, en el archivo de solución debe escribirse como **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="fb638-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="fb638-138">Alertas</span><span class="sxs-lookup"><span data-stu-id="fb638-138">Alerts</span></span>
<span data-ttu-id="fb638-139">Las reglas de alerta que ejecutan una búsqueda guardada a intervalos regulares crean [alertas de Log Analytics](../log-analytics/log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="fb638-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="fb638-140">Si los resultados de la consulta coinciden con los criterios especificados, se crea un registro de alertas y se ejecutan una o varias acciones.</span><span class="sxs-lookup"><span data-stu-id="fb638-140">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="fb638-141">Las reglas de alerta en una solución de administración se componen de los tres siguientes recursos.</span><span class="sxs-lookup"><span data-stu-id="fb638-141">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="fb638-142">**Búsqueda guardada.**</span><span class="sxs-lookup"><span data-stu-id="fb638-142">**Saved search.**</span></span>  <span data-ttu-id="fb638-143">Define la búsqueda de registros que se va a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="fb638-143">Defines the log search that will be run.</span></span>  <span data-ttu-id="fb638-144">Varias reglas de alerta pueden compartir una única búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="fb638-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="fb638-145">**Programación.**</span><span class="sxs-lookup"><span data-stu-id="fb638-145">**Schedule.**</span></span>  <span data-ttu-id="fb638-146">Define la frecuencia con la que se va a ejecutar la búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="fb638-146">Defines how often the log search will be run.</span></span>  <span data-ttu-id="fb638-147">Cada regla de alerta tendrá una única programación.</span><span class="sxs-lookup"><span data-stu-id="fb638-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="fb638-148">**Acción de alerta.**</span><span class="sxs-lookup"><span data-stu-id="fb638-148">**Alert action.**</span></span>  <span data-ttu-id="fb638-149">Cada regla de alerta tendrá un único recurso de acción con un tipo de **alerta** que define los detalles de la alerta, como los criterios de cuándo se creará un registro de alertas y la gravedad de la alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-149">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span></span>  <span data-ttu-id="fb638-150">El recurso de acción definirá, opcionalmente, una respuesta de correo electrónico y de runbook.</span><span class="sxs-lookup"><span data-stu-id="fb638-150">The action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="fb638-151">**Acción de webhook (opcional).**</span><span class="sxs-lookup"><span data-stu-id="fb638-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="fb638-152">Si la regla de alerta llama a un webhook, se requiere un recurso de acción adicional con un tipo de **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="fb638-152">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="fb638-153">Los recursos de búsquedas guardadas se han descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb638-153">Saved search resources are described above.</span></span>  <span data-ttu-id="fb638-154">Los demás recursos se describen a continuación.</span><span class="sxs-lookup"><span data-stu-id="fb638-154">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="fb638-155">Recurso de programación</span><span class="sxs-lookup"><span data-stu-id="fb638-155">Schedule resource</span></span>

<span data-ttu-id="fb638-156">Una búsqueda guardada puede tener una o más programaciones y cada programación representa una regla de alerta independiente.</span><span class="sxs-lookup"><span data-stu-id="fb638-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="fb638-157">La programación define la frecuencia con la que se realiza la búsqueda y el intervalo de tiempo durante el que se recuperan los datos.</span><span class="sxs-lookup"><span data-stu-id="fb638-157">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="fb638-158">Los recursos de programación tienen un tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` y presentan la siguiente estructura.</span><span class="sxs-lookup"><span data-stu-id="fb638-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> <span data-ttu-id="fb638-159">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="fb638-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="fb638-160">En la tabla siguiente se describen las propiedades para los recursos de programación.</span><span class="sxs-lookup"><span data-stu-id="fb638-160">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="fb638-161">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="fb638-161">Element name</span></span> | <span data-ttu-id="fb638-162">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fb638-162">Required</span></span> | <span data-ttu-id="fb638-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fb638-164">enabled</span><span class="sxs-lookup"><span data-stu-id="fb638-164">enabled</span></span>       | <span data-ttu-id="fb638-165">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-165">Yes</span></span> | <span data-ttu-id="fb638-166">Especifica si la alerta está habilitada cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="fb638-166">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="fb638-167">interval</span><span class="sxs-lookup"><span data-stu-id="fb638-167">interval</span></span>      | <span data-ttu-id="fb638-168">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-168">Yes</span></span> | <span data-ttu-id="fb638-169">Frecuencia con la que se ejecuta la consulta en minutos.</span><span class="sxs-lookup"><span data-stu-id="fb638-169">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="fb638-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="fb638-170">queryTimeSpan</span></span> | <span data-ttu-id="fb638-171">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-171">Yes</span></span> | <span data-ttu-id="fb638-172">Período de tiempo en minutos en el que se evalúan los resultados.</span><span class="sxs-lookup"><span data-stu-id="fb638-172">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="fb638-173">El recurso de programación debe depender de la búsqueda guardada para que se cree antes de la programación.</span><span class="sxs-lookup"><span data-stu-id="fb638-173">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="fb638-174">Acciones</span><span class="sxs-lookup"><span data-stu-id="fb638-174">Actions</span></span>
<span data-ttu-id="fb638-175">Hay dos tipos de recursos de acción especificados por la propiedad **Type**.</span><span class="sxs-lookup"><span data-stu-id="fb638-175">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="fb638-176">Una programación requiere una acción **Alert** que define los detalles de la regla de alerta y las acciones que se realizan cuando se crea una alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-176">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="fb638-177">También puede incluir una acción **Webhook** si se debe llamar a un webhook desde la alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-177">It may also include a **Webhook** action if a webhook should be called from the alert.</span></span>  

<span data-ttu-id="fb638-178">Los recursos de acción tienen un tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="fb638-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="fb638-179">Acciones de alerta</span><span class="sxs-lookup"><span data-stu-id="fb638-179">Alert actions</span></span>

<span data-ttu-id="fb638-180">Cada programación tendrá una acción **Alert**.</span><span class="sxs-lookup"><span data-stu-id="fb638-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="fb638-181">Esto define los detalles de la alerta y, opcionalmente, las acciones de notificación y corrección.</span><span class="sxs-lookup"><span data-stu-id="fb638-181">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="fb638-182">Una notificación envía un mensaje de correo electrónico a una o varias direcciones.</span><span class="sxs-lookup"><span data-stu-id="fb638-182">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="fb638-183">Una corrección inicia un runbook en Azure Automation para intentar corregir el problema detectado.</span><span class="sxs-lookup"><span data-stu-id="fb638-183">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

<span data-ttu-id="fb638-184">Las acciones de alerta tienen la siguiente estructura.</span><span class="sxs-lookup"><span data-stu-id="fb638-184">Alert actions have the following structure.</span></span>  <span data-ttu-id="fb638-185">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="fb638-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="fb638-186">En las tablas siguientes se describen las propiedades para los recursos de acción de alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-186">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="fb638-187">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="fb638-187">Element name</span></span> | <span data-ttu-id="fb638-188">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fb638-188">Required</span></span> | <span data-ttu-id="fb638-189">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fb638-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="fb638-190">Type</span></span> | <span data-ttu-id="fb638-191">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-191">Yes</span></span> | <span data-ttu-id="fb638-192">Tipo de la acción.</span><span class="sxs-lookup"><span data-stu-id="fb638-192">Type of the action.</span></span>  <span data-ttu-id="fb638-193">Será **Alert** para las acciones de alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="fb638-194">Nombre</span><span class="sxs-lookup"><span data-stu-id="fb638-194">Name</span></span> | <span data-ttu-id="fb638-195">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-195">Yes</span></span> | <span data-ttu-id="fb638-196">Nombre para mostrar de la alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-196">Display name for the alert.</span></span>  <span data-ttu-id="fb638-197">Es el nombre que se muestra en la consola para la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-197">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="fb638-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-198">Description</span></span> | <span data-ttu-id="fb638-199">No</span><span class="sxs-lookup"><span data-stu-id="fb638-199">No</span></span> | <span data-ttu-id="fb638-200">Descripción opcional de la alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-200">Optional description of the alert.</span></span> |
| <span data-ttu-id="fb638-201">Gravedad</span><span class="sxs-lookup"><span data-stu-id="fb638-201">Severity</span></span> | <span data-ttu-id="fb638-202">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-202">Yes</span></span> | <span data-ttu-id="fb638-203">Gravedad del registro de alertas según los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="fb638-203">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="fb638-204">**Critical)** (Crítico)</span><span class="sxs-lookup"><span data-stu-id="fb638-204">**Critical**</span></span><br><span data-ttu-id="fb638-205">**Warning (ADVERTENCIA)**</span><span class="sxs-lookup"><span data-stu-id="fb638-205">**Warning**</span></span><br><span data-ttu-id="fb638-206">**Informational** (Informativo)</span><span class="sxs-lookup"><span data-stu-id="fb638-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="fb638-207">Umbral</span><span class="sxs-lookup"><span data-stu-id="fb638-207">Threshold</span></span>
<span data-ttu-id="fb638-208">Esta sección es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="fb638-208">This section is required.</span></span>  <span data-ttu-id="fb638-209">Define las propiedades para el umbral de alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-209">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="fb638-210">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="fb638-210">Element name</span></span> | <span data-ttu-id="fb638-211">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fb638-211">Required</span></span> | <span data-ttu-id="fb638-212">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fb638-213">Operador</span><span class="sxs-lookup"><span data-stu-id="fb638-213">Operator</span></span> | <span data-ttu-id="fb638-214">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-214">Yes</span></span> | <span data-ttu-id="fb638-215">Operador para la comparación según los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb638-215">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="fb638-216">**gt = mayor que<br>lt = menor que**</span><span class="sxs-lookup"><span data-stu-id="fb638-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="fb638-217">Valor</span><span class="sxs-lookup"><span data-stu-id="fb638-217">Value</span></span> | <span data-ttu-id="fb638-218">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-218">Yes</span></span> | <span data-ttu-id="fb638-219">Valor para comparar los resultados.</span><span class="sxs-lookup"><span data-stu-id="fb638-219">The value to compare the results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="fb638-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="fb638-220">MetricsTrigger</span></span>
<span data-ttu-id="fb638-221">Esta sección es opcional.</span><span class="sxs-lookup"><span data-stu-id="fb638-221">This section is optional.</span></span>  <span data-ttu-id="fb638-222">Inclúyala para una alerta de unidades métricas.</span><span class="sxs-lookup"><span data-stu-id="fb638-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="fb638-223">Las alertas de unidades métricas están actualmente en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="fb638-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="fb638-224">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="fb638-224">Element name</span></span> | <span data-ttu-id="fb638-225">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fb638-225">Required</span></span> | <span data-ttu-id="fb638-226">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fb638-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="fb638-227">TriggerCondition</span></span> | <span data-ttu-id="fb638-228">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-228">Yes</span></span> | <span data-ttu-id="fb638-229">Especifica si el umbral es para el número total de infracciones o para infracciones consecutivas con los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="fb638-229">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="fb638-230">**Total<br>Consecutive** (Total, Consecutivos)</span><span class="sxs-lookup"><span data-stu-id="fb638-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="fb638-231">Operador</span><span class="sxs-lookup"><span data-stu-id="fb638-231">Operator</span></span> | <span data-ttu-id="fb638-232">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-232">Yes</span></span> | <span data-ttu-id="fb638-233">Operador para la comparación según los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb638-233">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="fb638-234">**gt = mayor que<br>lt = menor que**</span><span class="sxs-lookup"><span data-stu-id="fb638-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="fb638-235">Valor</span><span class="sxs-lookup"><span data-stu-id="fb638-235">Value</span></span> | <span data-ttu-id="fb638-236">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-236">Yes</span></span> | <span data-ttu-id="fb638-237">Número de veces que se deben cumplir los criterios para desencadenar la alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-237">Number of the times the criteria must be met to trigger the alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="fb638-238">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="fb638-238">Throttling</span></span>
<span data-ttu-id="fb638-239">Esta sección es opcional.</span><span class="sxs-lookup"><span data-stu-id="fb638-239">This section is optional.</span></span>  <span data-ttu-id="fb638-240">Incluya esta sección si desea suprimir alertas en la misma regla durante cierto tiempo después de crear una alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-240">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="fb638-241">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="fb638-241">Element name</span></span> | <span data-ttu-id="fb638-242">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fb638-242">Required</span></span> | <span data-ttu-id="fb638-243">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fb638-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="fb638-244">DurationInMinutes</span></span> | <span data-ttu-id="fb638-245">Sí, si hay una limitación de elementos incluida</span><span class="sxs-lookup"><span data-stu-id="fb638-245">Yes if Throttling element included</span></span> | <span data-ttu-id="fb638-246">Número de minutos para suprimir alertas después de crear una en la misma regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-246">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="fb638-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="fb638-247">EmailNotification</span></span>
 <span data-ttu-id="fb638-248">Esta sección es opcional. Inclúyala si desea que la alerta envíe un mensaje de correo electrónico a uno o varios destinatarios.</span><span class="sxs-lookup"><span data-stu-id="fb638-248">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="fb638-249">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="fb638-249">Element name</span></span> | <span data-ttu-id="fb638-250">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fb638-250">Required</span></span> | <span data-ttu-id="fb638-251">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fb638-252">Recipients</span><span class="sxs-lookup"><span data-stu-id="fb638-252">Recipients</span></span> | <span data-ttu-id="fb638-253">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-253">Yes</span></span> | <span data-ttu-id="fb638-254">Lista delimitada por comas de direcciones de correo electrónico para envío de notificación cuando se crea una alerta, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="fb638-254">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="fb638-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="fb638-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="fb638-256">Asunto</span><span class="sxs-lookup"><span data-stu-id="fb638-256">Subject</span></span> | <span data-ttu-id="fb638-257">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-257">Yes</span></span> | <span data-ttu-id="fb638-258">Línea del asunto del mensaje de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="fb638-258">Subject line of the mail.</span></span> |
| <span data-ttu-id="fb638-259">Datos adjuntos</span><span class="sxs-lookup"><span data-stu-id="fb638-259">Attachment</span></span> | <span data-ttu-id="fb638-260">No</span><span class="sxs-lookup"><span data-stu-id="fb638-260">No</span></span> | <span data-ttu-id="fb638-261">Los datos adjuntos no son compatibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="fb638-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="fb638-262">Si este elemento está incluido, debe ser **None** (Ninguno).</span><span class="sxs-lookup"><span data-stu-id="fb638-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="fb638-263">Corrección</span><span class="sxs-lookup"><span data-stu-id="fb638-263">Remediation</span></span>
<span data-ttu-id="fb638-264">Esta sección es opcional. Inclúyala si desea que se inicie un runbook en respuesta a la alerta.</span><span class="sxs-lookup"><span data-stu-id="fb638-264">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="fb638-265">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="fb638-265">Element name</span></span> | <span data-ttu-id="fb638-266">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fb638-266">Required</span></span> | <span data-ttu-id="fb638-267">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fb638-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="fb638-268">RunbookName</span></span> | <span data-ttu-id="fb638-269">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-269">Yes</span></span> | <span data-ttu-id="fb638-270">Nombre del runbook que se va a iniciar.</span><span class="sxs-lookup"><span data-stu-id="fb638-270">Name of the runbook to start.</span></span> |
| <span data-ttu-id="fb638-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="fb638-271">WebhookUri</span></span> | <span data-ttu-id="fb638-272">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-272">Yes</span></span> | <span data-ttu-id="fb638-273">URI del webhook para el runbook.</span><span class="sxs-lookup"><span data-stu-id="fb638-273">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="fb638-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="fb638-274">Expiry</span></span> | <span data-ttu-id="fb638-275">No</span><span class="sxs-lookup"><span data-stu-id="fb638-275">No</span></span> | <span data-ttu-id="fb638-276">Fecha y hora a la que expira la corrección.</span><span class="sxs-lookup"><span data-stu-id="fb638-276">Date and time that the remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="fb638-277">Acciones de webhook</span><span class="sxs-lookup"><span data-stu-id="fb638-277">Webhook actions</span></span>

<span data-ttu-id="fb638-278">Las acciones de webhook inician un proceso llamando a una dirección URL y, opcionalmente, proporcionando una carga que se va a enviar.</span><span class="sxs-lookup"><span data-stu-id="fb638-278">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="fb638-279">Son similares a las acciones de corrección, salvo por el hecho de que están pensadas para webhooks que pueden invocar procesos que no tienen que ver con Runbooks de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb638-279">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="fb638-280">También ofrecen la posibilidad extra de proporcionar una carga adicional para entregarla en el proceso remoto.</span><span class="sxs-lookup"><span data-stu-id="fb638-280">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="fb638-281">Si la alerta llama a un webhook, necesitará un recurso de acción con un tipo de **Webhook**, además del recurso de acción **Alert**.</span><span class="sxs-lookup"><span data-stu-id="fb638-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="fb638-282">En las tablas siguientes se describen las propiedades para los recursos de acción de Webhook.</span><span class="sxs-lookup"><span data-stu-id="fb638-282">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="fb638-283">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="fb638-283">Element name</span></span> | <span data-ttu-id="fb638-284">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fb638-284">Required</span></span> | <span data-ttu-id="fb638-285">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb638-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fb638-286">type</span><span class="sxs-lookup"><span data-stu-id="fb638-286">type</span></span> | <span data-ttu-id="fb638-287">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-287">Yes</span></span> | <span data-ttu-id="fb638-288">Tipo de la acción.</span><span class="sxs-lookup"><span data-stu-id="fb638-288">Type of the action.</span></span>  <span data-ttu-id="fb638-289">Será **Webhook** para las acciones de webhook.</span><span class="sxs-lookup"><span data-stu-id="fb638-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="fb638-290">name</span><span class="sxs-lookup"><span data-stu-id="fb638-290">name</span></span> | <span data-ttu-id="fb638-291">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-291">Yes</span></span> | <span data-ttu-id="fb638-292">Nombre para mostrar de la acción.</span><span class="sxs-lookup"><span data-stu-id="fb638-292">Display name for the action.</span></span>  <span data-ttu-id="fb638-293">Esto no se muestra en la consola.</span><span class="sxs-lookup"><span data-stu-id="fb638-293">This is not displayed in the console.</span></span> |
| <span data-ttu-id="fb638-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="fb638-294">wehookUri</span></span> | <span data-ttu-id="fb638-295">Sí</span><span class="sxs-lookup"><span data-stu-id="fb638-295">Yes</span></span> | <span data-ttu-id="fb638-296">URI del webhook.</span><span class="sxs-lookup"><span data-stu-id="fb638-296">Uri for the webhook.</span></span> |
| <span data-ttu-id="fb638-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="fb638-297">customPayload</span></span> | <span data-ttu-id="fb638-298">No</span><span class="sxs-lookup"><span data-stu-id="fb638-298">No</span></span> | <span data-ttu-id="fb638-299">Carga personalizada que se va a enviar al webhook.</span><span class="sxs-lookup"><span data-stu-id="fb638-299">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="fb638-300">El formato dependerá de lo que el webhook espere.</span><span class="sxs-lookup"><span data-stu-id="fb638-300">The format will depend on what the webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="fb638-301">Muestra</span><span class="sxs-lookup"><span data-stu-id="fb638-301">Sample</span></span>

<span data-ttu-id="fb638-302">A continuación se muestra un ejemplo de una solución que incluye los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="fb638-302">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="fb638-303">Búsqueda guardada</span><span class="sxs-lookup"><span data-stu-id="fb638-303">Saved search</span></span>
- <span data-ttu-id="fb638-304">Schedule</span><span class="sxs-lookup"><span data-stu-id="fb638-304">Schedule</span></span>
- <span data-ttu-id="fb638-305">Acción de alerta</span><span class="sxs-lookup"><span data-stu-id="fb638-305">Alert action</span></span>
- <span data-ttu-id="fb638-306">Acción de webhook</span><span class="sxs-lookup"><span data-stu-id="fb638-306">Webhook action</span></span>

<span data-ttu-id="fb638-307">En el ejemplo se utilizan variables de [parámetros de solución estándar](operations-management-suite-solutions-solution-file.md#parameters) que se suelen utilizar en una solución en lugar de codificar valores en las definiciones de recursos.</span><span class="sxs-lookup"><span data-stu-id="fb638-307">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for the email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="fb638-308">El siguiente archivo de parámetros proporciona valores de ejemplo para esta solución.</span><span class="sxs-lookup"><span data-stu-id="fb638-308">The following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="fb638-309">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb638-309">Next steps</span></span>
* <span data-ttu-id="fb638-310">[Incorporación de vistas](operations-management-suite-solutions-resources-views.md) a la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="fb638-310">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="fb638-311">[Incorporación de runbooks de Automation y otros recursos](operations-management-suite-solutions-resources-automation.md) a la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="fb638-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>

