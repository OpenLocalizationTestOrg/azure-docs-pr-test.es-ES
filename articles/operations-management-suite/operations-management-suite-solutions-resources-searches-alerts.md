---
title: "aaaSaved búsquedas y alertas en soluciones de OMS | Documentos de Microsoft"
description: "Soluciones de OMS incluirá, normalmente búsquedas guardadas en los datos de análisis de registros tooanalyze recopilados por solución Hola.  Se puede definir usuario de alertas toonotify Hola o tomar una acción en problema crítico de respuesta tooa automáticamente.  Este artículo describe cómo toodefine análisis de registros guarda las búsquedas y alertas en una plantilla de ARM por lo que pueden incluirse en soluciones de administración."
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
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="53452-105">Adición de análisis de registros guarda tooOMS búsquedas y alertas de solución de administración (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="53452-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="53452-106">La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar.</span><span class="sxs-lookup"><span data-stu-id="53452-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="53452-107">Cualquier esquema que se describe a continuación es toochange de asunto.</span><span class="sxs-lookup"><span data-stu-id="53452-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="53452-108">[Soluciones de administración de OMS](operations-management-suite-solutions.md) incluirá, normalmente [búsquedas guardadas](../log-analytics/log-analytics-log-searches.md) de datos de tooanalyze de análisis de registros recopilados por solución Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="53452-109">También pueden definir [alertas](../log-analytics/log-analytics-alerts.md) toonotify Hola usuario o tomar una acción en problema crítico de respuesta tooa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="53452-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="53452-110">Este artículo describe cómo toodefine análisis de registros guarda las búsquedas y alertas en un [plantilla de administración de recursos](../resource-manager-template-walkthrough.md) por lo que pueden incluirse en [soluciones de administración de](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="53452-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="53452-111">Hello ejemplos en este artículo usan parámetros y variables que están bien soluciones toomanagement necesarias o habituales y se describen en [crear soluciones de administración de Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="53452-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="53452-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="53452-112">Prerequisites</span></span>
<span data-ttu-id="53452-113">En este artículo se da por supuesto que ya está familiarizado con cómo demasiado[crear una solución de administración](operations-management-suite-solutions-creating.md) y la estructura de Hola de un [plantilla de ARM](../resource-group-authoring-templates.md) y el archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="53452-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="53452-114">Área de trabajo de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="53452-114">Log Analytics Workspace</span></span>
<span data-ttu-id="53452-115">Todos los recursos de Log Analytics están contenidos en un [área de trabajo](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="53452-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="53452-116">Como se describe en [OMS área de trabajo y la cuenta de automatización](operations-management-suite-solutions.md#oms-workspace-and-automation-account) área de trabajo de hello no se incluye en la solución de administración de hello, pero debe existir antes de instala la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="53452-117">Si no está disponible, se producirá un error en la instalación de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="53452-118">Hola de área de trabajo de hello llamo en nombre de Hola de cada recurso de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="53452-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="53452-119">Esto se hace en soluciones de hello con hello **área de trabajo** parámetro como en el siguiente ejemplo de un recurso de savedsearch de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="53452-120">Búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="53452-120">Saved Searches</span></span>
<span data-ttu-id="53452-121">Incluir [búsquedas guardadas](../log-analytics/log-analytics-log-searches.md) en un solución tooallow usuarios tooquery los datos recopilados por la solución.</span><span class="sxs-lookup"><span data-stu-id="53452-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="53452-122">Búsquedas guardadas aparecerá en **favoritos** en el portal de OMS de Hola y **búsquedas guardadas** Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="53452-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="53452-123">También es necesaria una búsqueda guardada para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="53452-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="53452-124">[Búsqueda de análisis de registros guardan](../log-analytics/log-analytics-log-searches.md) recursos tienen un tipo de `Microsoft.OperationalInsights/workspaces/savedSearches` y tener Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="53452-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="53452-125">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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



<span data-ttu-id="53452-126">En hello en la tabla siguiente se describen cada una de las propiedades de Hola de una búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="53452-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="53452-127">Propiedad</span><span class="sxs-lookup"><span data-stu-id="53452-127">Property</span></span> | <span data-ttu-id="53452-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="53452-129">categoría</span><span class="sxs-lookup"><span data-stu-id="53452-129">category</span></span> | <span data-ttu-id="53452-130">categoría de Hello para la búsqueda guardada de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-130">hello category for hello saved search.</span></span>  <span data-ttu-id="53452-131">Cualquier búsquedas guardadas en hello a menudo compartirán la misma solución una única categoría por lo que se agrupen en consola Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="53452-132">displayname</span><span class="sxs-lookup"><span data-stu-id="53452-132">displayname</span></span> | <span data-ttu-id="53452-133">Nombre toodisplay para hello búsqueda guardada en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="53452-134">query</span><span class="sxs-lookup"><span data-stu-id="53452-134">query</span></span> | <span data-ttu-id="53452-135">Toorun de consulta.</span><span class="sxs-lookup"><span data-stu-id="53452-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="53452-136">Puede que tenga caracteres de escape de toouse en la consulta de hello si incluye caracteres que pudieron interpretarse como JSON.</span><span class="sxs-lookup"><span data-stu-id="53452-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="53452-137">Por ejemplo, si la consulta era **OperationName:"Microsoft.Compute/virtualMachines/write tipo: AzureActivity"**, deben escribirse en el archivo de solución de hello como **OperationName tipo: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="53452-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="53452-138">Alertas</span><span class="sxs-lookup"><span data-stu-id="53452-138">Alerts</span></span>
<span data-ttu-id="53452-139">Las reglas de alerta que ejecutan una búsqueda guardada a intervalos regulares crean [alertas de Log Analytics](../log-analytics/log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="53452-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="53452-140">Si los resultados de Hola de consulta de hello coinciden con los criterios especificados, se crea un registro de alerta y se ejecutan una o varias acciones.</span><span class="sxs-lookup"><span data-stu-id="53452-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="53452-141">Reglas de alerta en una solución de administración se componen de hello después de tres recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="53452-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="53452-142">**Búsqueda guardada.**</span><span class="sxs-lookup"><span data-stu-id="53452-142">**Saved search.**</span></span>  <span data-ttu-id="53452-143">Define la búsqueda de registros de Hola que se va a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="53452-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="53452-144">Varias reglas de alerta pueden compartir una única búsqueda guardada.</span><span class="sxs-lookup"><span data-stu-id="53452-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="53452-145">**Programación.**</span><span class="sxs-lookup"><span data-stu-id="53452-145">**Schedule.**</span></span>  <span data-ttu-id="53452-146">Define la frecuencia con hello búsqueda de registros se va a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="53452-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="53452-147">Cada regla de alerta tendrá una única programación.</span><span class="sxs-lookup"><span data-stu-id="53452-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="53452-148">**Acción de alerta.**</span><span class="sxs-lookup"><span data-stu-id="53452-148">**Alert action.**</span></span>  <span data-ttu-id="53452-149">Cada regla de alerta tendrá un recurso de acción con un tipo de **alerta** que define los detalles de Hola de alerta de hello como criterios de Hola durante un registro de alerta se creará y Hola gravedad de la alerta.</span><span class="sxs-lookup"><span data-stu-id="53452-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="53452-150">recursos de la acción de Hello, opcionalmente, definirá una respuesta de correo electrónico y el runbook.</span><span class="sxs-lookup"><span data-stu-id="53452-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="53452-151">**Acción de webhook (opcional).**</span><span class="sxs-lookup"><span data-stu-id="53452-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="53452-152">Si la regla de alerta de hello llamará un webhook, entonces requiere un recurso de otra acción con un tipo de **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="53452-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="53452-153">Los recursos de búsquedas guardadas se han descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="53452-153">Saved search resources are described above.</span></span>  <span data-ttu-id="53452-154">Hello otros recursos se describen a continuación.</span><span class="sxs-lookup"><span data-stu-id="53452-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="53452-155">Recurso de programación</span><span class="sxs-lookup"><span data-stu-id="53452-155">Schedule resource</span></span>

<span data-ttu-id="53452-156">Una búsqueda guardada puede tener una o más programaciones y cada programación representa una regla de alerta independiente.</span><span class="sxs-lookup"><span data-stu-id="53452-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="53452-157">Hello programación definen con qué frecuencia hello búsqueda se ejecuta y Hola intervalo de tiempo sobre qué Hola se recuperan los datos.</span><span class="sxs-lookup"><span data-stu-id="53452-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="53452-158">Recursos de programación tienen un tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` y tener Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="53452-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="53452-159">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


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



<span data-ttu-id="53452-160">propiedades de Hola para programar los recursos se describen en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="53452-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="53452-161">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="53452-161">Element name</span></span> | <span data-ttu-id="53452-162">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="53452-162">Required</span></span> | <span data-ttu-id="53452-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="53452-164">enabled</span><span class="sxs-lookup"><span data-stu-id="53452-164">enabled</span></span>       | <span data-ttu-id="53452-165">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-165">Yes</span></span> | <span data-ttu-id="53452-166">Especifica si la alerta de hello está habilitada cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="53452-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="53452-167">interval</span><span class="sxs-lookup"><span data-stu-id="53452-167">interval</span></span>      | <span data-ttu-id="53452-168">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-168">Yes</span></span> | <span data-ttu-id="53452-169">¿Con qué frecuencia hello consulta se ejecuta en minutos.</span><span class="sxs-lookup"><span data-stu-id="53452-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="53452-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="53452-170">queryTimeSpan</span></span> | <span data-ttu-id="53452-171">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-171">Yes</span></span> | <span data-ttu-id="53452-172">Período de tiempo en minutos en relación con los resultados de tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="53452-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="53452-173">recursos de programación de Hello deben depender de hello búsqueda guardada para que se cree antes de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="53452-174">Acciones</span><span class="sxs-lookup"><span data-stu-id="53452-174">Actions</span></span>
<span data-ttu-id="53452-175">Hay dos tipos de recurso de acción especificado por hello **tipo** propiedad.</span><span class="sxs-lookup"><span data-stu-id="53452-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="53452-176">Una programación requiere uno **alerta** acción que define los detalles de Hola de regla de alerta de Hola y las acciones que se realizan cuando se crea una alerta.</span><span class="sxs-lookup"><span data-stu-id="53452-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="53452-177">También puede incluir un **Webhook** acción si debe llamarse a un webhook de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="53452-178">Los recursos de acción tienen un tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="53452-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="53452-179">Acciones de alerta</span><span class="sxs-lookup"><span data-stu-id="53452-179">Alert actions</span></span>

<span data-ttu-id="53452-180">Cada programación tendrá una acción **Alert**.</span><span class="sxs-lookup"><span data-stu-id="53452-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="53452-181">Esto define los detalles de Hola de alerta de hello y, opcionalmente, las acciones de notificación y la corrección.</span><span class="sxs-lookup"><span data-stu-id="53452-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="53452-182">Una notificación envía un correo electrónico tooone o más direcciones.</span><span class="sxs-lookup"><span data-stu-id="53452-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="53452-183">Una solución, inicia un runbook problema de automatización de Azure tooattempt tooremediate Hola detectado.</span><span class="sxs-lookup"><span data-stu-id="53452-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="53452-184">Acciones de alerta tienen Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="53452-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="53452-185">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



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

<span data-ttu-id="53452-186">propiedades de Hola de recursos de la acción de alerta se describen en hello las tablas siguientes.</span><span class="sxs-lookup"><span data-stu-id="53452-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="53452-187">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="53452-187">Element name</span></span> | <span data-ttu-id="53452-188">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="53452-188">Required</span></span> | <span data-ttu-id="53452-189">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="53452-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="53452-190">Type</span></span> | <span data-ttu-id="53452-191">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-191">Yes</span></span> | <span data-ttu-id="53452-192">Tipo de acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-192">Type of hello action.</span></span>  <span data-ttu-id="53452-193">Será **Alert** para las acciones de alerta.</span><span class="sxs-lookup"><span data-stu-id="53452-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="53452-194">Nombre</span><span class="sxs-lookup"><span data-stu-id="53452-194">Name</span></span> | <span data-ttu-id="53452-195">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-195">Yes</span></span> | <span data-ttu-id="53452-196">Nombre para mostrar de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-196">Display name for hello alert.</span></span>  <span data-ttu-id="53452-197">Este es el nombre de Hola que se muestra en la consola de hello para la regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="53452-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-198">Description</span></span> | <span data-ttu-id="53452-199">No</span><span class="sxs-lookup"><span data-stu-id="53452-199">No</span></span> | <span data-ttu-id="53452-200">Descripción opcional de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="53452-201">Severity</span><span class="sxs-lookup"><span data-stu-id="53452-201">Severity</span></span> | <span data-ttu-id="53452-202">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-202">Yes</span></span> | <span data-ttu-id="53452-203">Gravedad de registro y alerta Hola Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="53452-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="53452-204">**Critical)** (Crítico)</span><span class="sxs-lookup"><span data-stu-id="53452-204">**Critical**</span></span><br><span data-ttu-id="53452-205">**Warning (ADVERTENCIA)**</span><span class="sxs-lookup"><span data-stu-id="53452-205">**Warning**</span></span><br><span data-ttu-id="53452-206">**Informational** (Informativo)</span><span class="sxs-lookup"><span data-stu-id="53452-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="53452-207">Umbral</span><span class="sxs-lookup"><span data-stu-id="53452-207">Threshold</span></span>
<span data-ttu-id="53452-208">Esta sección es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="53452-208">This section is required.</span></span>  <span data-ttu-id="53452-209">Define propiedades de hello para el umbral de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="53452-210">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="53452-210">Element name</span></span> | <span data-ttu-id="53452-211">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="53452-211">Required</span></span> | <span data-ttu-id="53452-212">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="53452-213">Operador</span><span class="sxs-lookup"><span data-stu-id="53452-213">Operator</span></span> | <span data-ttu-id="53452-214">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-214">Yes</span></span> | <span data-ttu-id="53452-215">Operador para la comparación de Hola de hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="53452-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="53452-216">**gt = mayor que<br>lt = menor que**</span><span class="sxs-lookup"><span data-stu-id="53452-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="53452-217">Valor</span><span class="sxs-lookup"><span data-stu-id="53452-217">Value</span></span> | <span data-ttu-id="53452-218">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-218">Yes</span></span> | <span data-ttu-id="53452-219">resultados de Hello valor toocompare Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="53452-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="53452-220">MetricsTrigger</span></span>
<span data-ttu-id="53452-221">Esta sección es opcional.</span><span class="sxs-lookup"><span data-stu-id="53452-221">This section is optional.</span></span>  <span data-ttu-id="53452-222">Inclúyala para una alerta de unidades métricas.</span><span class="sxs-lookup"><span data-stu-id="53452-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="53452-223">Las alertas de unidades métricas están actualmente en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="53452-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="53452-224">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="53452-224">Element name</span></span> | <span data-ttu-id="53452-225">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="53452-225">Required</span></span> | <span data-ttu-id="53452-226">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="53452-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="53452-227">TriggerCondition</span></span> | <span data-ttu-id="53452-228">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-228">Yes</span></span> | <span data-ttu-id="53452-229">Especifica si el umbral de hello es número total de infracciones o infracciones consecutivas de hello después de valores:</span><span class="sxs-lookup"><span data-stu-id="53452-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="53452-230">**Total<br>Consecutive** (Total, Consecutivos)</span><span class="sxs-lookup"><span data-stu-id="53452-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="53452-231">Operador</span><span class="sxs-lookup"><span data-stu-id="53452-231">Operator</span></span> | <span data-ttu-id="53452-232">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-232">Yes</span></span> | <span data-ttu-id="53452-233">Operador para la comparación de Hola de hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="53452-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="53452-234">**gt = mayor que<br>lt = menor que**</span><span class="sxs-lookup"><span data-stu-id="53452-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="53452-235">Valor</span><span class="sxs-lookup"><span data-stu-id="53452-235">Value</span></span> | <span data-ttu-id="53452-236">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-236">Yes</span></span> | <span data-ttu-id="53452-237">Número de hello horas Hola criterios debe ser alerta de hello tootrigger cumpla.</span><span class="sxs-lookup"><span data-stu-id="53452-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="53452-238">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="53452-238">Throttling</span></span>
<span data-ttu-id="53452-239">Esta sección es opcional.</span><span class="sxs-lookup"><span data-stu-id="53452-239">This section is optional.</span></span>  <span data-ttu-id="53452-240">Incluya esta sección si desea que las alertas de toosuppress de hello misma regla para una cantidad de tiempo después de crea una alerta.</span><span class="sxs-lookup"><span data-stu-id="53452-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="53452-241">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="53452-241">Element name</span></span> | <span data-ttu-id="53452-242">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="53452-242">Required</span></span> | <span data-ttu-id="53452-243">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="53452-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="53452-244">DurationInMinutes</span></span> | <span data-ttu-id="53452-245">Sí, si hay una limitación de elementos incluida</span><span class="sxs-lookup"><span data-stu-id="53452-245">Yes if Throttling element included</span></span> | <span data-ttu-id="53452-246">Número de alertas de toosuppress de minutos después de que uno de Hola se crea la misma regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="53452-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="53452-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="53452-247">EmailNotification</span></span>
 <span data-ttu-id="53452-248">Esta sección es opcional incluir si desea Hola tooone de correo electrónico de alerta toosend o más destinatarios.</span><span class="sxs-lookup"><span data-stu-id="53452-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="53452-249">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="53452-249">Element name</span></span> | <span data-ttu-id="53452-250">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="53452-250">Required</span></span> | <span data-ttu-id="53452-251">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="53452-252">Recipients</span><span class="sxs-lookup"><span data-stu-id="53452-252">Recipients</span></span> | <span data-ttu-id="53452-253">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-253">Yes</span></span> | <span data-ttu-id="53452-254">Una lista delimitada por comas de correo electrónico direcciones toosend notificación cuando se crea una alerta como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="53452-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="53452-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="53452-256">Asunto</span><span class="sxs-lookup"><span data-stu-id="53452-256">Subject</span></span> | <span data-ttu-id="53452-257">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-257">Yes</span></span> | <span data-ttu-id="53452-258">Línea de asunto de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="53452-259">Datos adjuntos</span><span class="sxs-lookup"><span data-stu-id="53452-259">Attachment</span></span> | <span data-ttu-id="53452-260">No</span><span class="sxs-lookup"><span data-stu-id="53452-260">No</span></span> | <span data-ttu-id="53452-261">Los datos adjuntos no son compatibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="53452-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="53452-262">Si este elemento está incluido, debe ser **None** (Ninguno).</span><span class="sxs-lookup"><span data-stu-id="53452-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="53452-263">Corrección</span><span class="sxs-lookup"><span data-stu-id="53452-263">Remediation</span></span>
<span data-ttu-id="53452-264">Esta sección es opcional incluirlo si desea que un toostart de runbook de alerta de toohello de respuesta.</span><span class="sxs-lookup"><span data-stu-id="53452-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="53452-265">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="53452-265">Element name</span></span> | <span data-ttu-id="53452-266">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="53452-266">Required</span></span> | <span data-ttu-id="53452-267">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="53452-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="53452-268">RunbookName</span></span> | <span data-ttu-id="53452-269">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-269">Yes</span></span> | <span data-ttu-id="53452-270">Nombre de hello runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="53452-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="53452-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="53452-271">WebhookUri</span></span> | <span data-ttu-id="53452-272">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-272">Yes</span></span> | <span data-ttu-id="53452-273">URI del webhook Hola Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="53452-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="53452-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="53452-274">Expiry</span></span> | <span data-ttu-id="53452-275">No</span><span class="sxs-lookup"><span data-stu-id="53452-275">No</span></span> | <span data-ttu-id="53452-276">Fecha y hora en que Hola corrección expira.</span><span class="sxs-lookup"><span data-stu-id="53452-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="53452-277">Acciones de webhook</span><span class="sxs-lookup"><span data-stu-id="53452-277">Webhook actions</span></span>

<span data-ttu-id="53452-278">Acciones de Webhook iniciar un proceso mediante una llamada a una dirección URL y, opcionalmente, proporcionar un toobe de carga que envía.</span><span class="sxs-lookup"><span data-stu-id="53452-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="53452-279">Únicamente son acciones similares de tooRemediation salvo que están concebidos para webhooks que puede invocar procesos distintos de runbooks de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="53452-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="53452-280">También proporcionan opción adicional de Hola de proporcionar un proceso de carga toobe entregado toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="53452-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="53452-281">Si la alerta llamará un webhook, será necesario un recurso de acción con un tipo de **Webhook** en suma toohello **alerta** recursos de la acción.</span><span class="sxs-lookup"><span data-stu-id="53452-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

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

<span data-ttu-id="53452-282">propiedades de Hola de recursos de la acción de Webhook se describen en hello las tablas siguientes.</span><span class="sxs-lookup"><span data-stu-id="53452-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="53452-283">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="53452-283">Element name</span></span> | <span data-ttu-id="53452-284">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="53452-284">Required</span></span> | <span data-ttu-id="53452-285">Descripción</span><span class="sxs-lookup"><span data-stu-id="53452-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="53452-286">type</span><span class="sxs-lookup"><span data-stu-id="53452-286">type</span></span> | <span data-ttu-id="53452-287">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-287">Yes</span></span> | <span data-ttu-id="53452-288">Tipo de acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-288">Type of hello action.</span></span>  <span data-ttu-id="53452-289">Será **Webhook** para las acciones de webhook.</span><span class="sxs-lookup"><span data-stu-id="53452-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="53452-290">name</span><span class="sxs-lookup"><span data-stu-id="53452-290">name</span></span> | <span data-ttu-id="53452-291">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-291">Yes</span></span> | <span data-ttu-id="53452-292">Nombre para mostrar para la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-292">Display name for hello action.</span></span>  <span data-ttu-id="53452-293">Esto no se muestra en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="53452-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="53452-294">wehookUri</span></span> | <span data-ttu-id="53452-295">Sí</span><span class="sxs-lookup"><span data-stu-id="53452-295">Yes</span></span> | <span data-ttu-id="53452-296">URI de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="53452-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="53452-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="53452-297">customPayload</span></span> | <span data-ttu-id="53452-298">No</span><span class="sxs-lookup"><span data-stu-id="53452-298">No</span></span> | <span data-ttu-id="53452-299">Carga personalizada toobe enviado toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="53452-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="53452-300">formato de Hello dependerá de qué webhook Hola está esperando.</span><span class="sxs-lookup"><span data-stu-id="53452-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="53452-301">Muestra</span><span class="sxs-lookup"><span data-stu-id="53452-301">Sample</span></span>

<span data-ttu-id="53452-302">Aquí te mostramos un ejemplo de una solución que incluya incluye Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="53452-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="53452-303">Búsqueda guardada</span><span class="sxs-lookup"><span data-stu-id="53452-303">Saved search</span></span>
- <span data-ttu-id="53452-304">Schedule</span><span class="sxs-lookup"><span data-stu-id="53452-304">Schedule</span></span>
- <span data-ttu-id="53452-305">Acción de alerta</span><span class="sxs-lookup"><span data-stu-id="53452-305">Alert action</span></span>
- <span data-ttu-id="53452-306">Acción de webhook</span><span class="sxs-lookup"><span data-stu-id="53452-306">Webhook action</span></span>

<span data-ttu-id="53452-307">usos de ejemplo de Hola [parámetros de la solución estándar](operations-management-suite-solutions-solution-file.md#parameters) variables que normalmente se utilizarían en una solución como opone toohardcoding valores en las definiciones de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="53452-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

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
              "Description": "List of recipients for hello email alert separated by semicolon"
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


<span data-ttu-id="53452-308">Hola siguiente parámetro archivo proporciona valores de ejemplos para esta solución.</span><span class="sxs-lookup"><span data-stu-id="53452-308">hello following parameter file provides samples values for this solution.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="53452-309">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="53452-309">Next steps</span></span>
* <span data-ttu-id="53452-310">[Agregar vistas](operations-management-suite-solutions-resources-views.md) tooyour solución de administración.</span><span class="sxs-lookup"><span data-stu-id="53452-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="53452-311">[Agregar los runbooks de automatización y otros recursos](operations-management-suite-solutions-resources-automation.md) tooyour solución de administración.</span><span class="sxs-lookup"><span data-stu-id="53452-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>

