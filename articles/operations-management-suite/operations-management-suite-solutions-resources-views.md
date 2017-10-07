---
title: "aaaViews en soluciones de administración de Operations Management Suite (OMS) | Documentos de Microsoft"
description: "Soluciones de administración de Operations Management Suite (OMS) incluirá, normalmente una o más vistas toovisualize de datos.  En este artículo se describe cómo tooexport una vista creada por hello Diseñador de vistas e incluirla en una solución de administración. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="6834b-104">Vistas de las soluciones de administración en Operations Management Suite (OMS) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="6834b-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="6834b-105">La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar.</span><span class="sxs-lookup"><span data-stu-id="6834b-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="6834b-106">Cualquier esquema que se describe a continuación es toochange de asunto.</span><span class="sxs-lookup"><span data-stu-id="6834b-106">Any schema described below is subject toochange.</span></span>    
>
>

<span data-ttu-id="6834b-107">[Soluciones de administración de Operations Management Suite (OMS)](operations-management-suite-solutions.md) incluirá, normalmente una o más vistas toovisualize de datos.</span><span class="sxs-lookup"><span data-stu-id="6834b-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views toovisualize data.</span></span>  <span data-ttu-id="6834b-108">Este artículo describe cómo tooexport una vista creada por hello [Diseñador de vistas](../log-analytics/log-analytics-view-designer.md) e incluirla en una solución de administración.</span><span class="sxs-lookup"><span data-stu-id="6834b-108">This article describes how tooexport a view created by hello [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="6834b-109">Hello ejemplos en este artículo usan parámetros y variables que están bien soluciones toomanagement necesarias o habituales y se describen en [crear soluciones de administración de Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="6834b-109">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="6834b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6834b-110">Prerequisites</span></span>
<span data-ttu-id="6834b-111">En este artículo se da por supuesto que ya está familiarizado con cómo demasiado[crear una solución de administración](operations-management-suite-solutions-creating.md) y la estructura de Hola de un archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="6834b-111">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="6834b-112">Información general</span><span class="sxs-lookup"><span data-stu-id="6834b-112">Overview</span></span>
<span data-ttu-id="6834b-113">tooinclude una vista en una solución de administración, se crea un **recursos** para él en hello [archivo de solución](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="6834b-113">tooinclude a view in a management solution, you create a **resource** for it in hello [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="6834b-114">Hola JSON que describe la configuración detallada de la vista de hello es normalmente complejo aunque y no algo que un autor de la solución típica sería capaz de toocreate manualmente.</span><span class="sxs-lookup"><span data-stu-id="6834b-114">hello JSON that describes hello view's detailed configuration is typically complex though and not something that a typical solution author would be able toocreate manually.</span></span>  <span data-ttu-id="6834b-115">Hello método más común es vista de hello toocreate con hello [Diseñador de vistas](../log-analytics/log-analytics-view-designer.md), exportarlo y, a continuación, agregue su solución de toohello de configuración detallada.</span><span class="sxs-lookup"><span data-stu-id="6834b-115">hello most common method is toocreate hello view using hello [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration toohello solution.</span></span>

<span data-ttu-id="6834b-116">pasos básicos de Hello tooadd una solución de tooa de vista son los siguientes.</span><span class="sxs-lookup"><span data-stu-id="6834b-116">hello basic steps tooadd a view tooa solution are as follows.</span></span>  <span data-ttu-id="6834b-117">Cada paso se describe con más detalle en secciones de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="6834b-117">Each step is described in further detail in hello sections below.</span></span>

1. <span data-ttu-id="6834b-118">Exportar archivo de hello vista tooa.</span><span class="sxs-lookup"><span data-stu-id="6834b-118">Export hello view tooa file.</span></span>
2. <span data-ttu-id="6834b-119">Crear recursos de la vista de hello en soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="6834b-119">Create hello view resource in hello solution.</span></span>
3. <span data-ttu-id="6834b-120">Agregar detalles de la vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6834b-120">Add hello view details.</span></span>

## <a name="export-hello-view-tooa-file"></a><span data-ttu-id="6834b-121">Exportar archivo de hello vista tooa</span><span class="sxs-lookup"><span data-stu-id="6834b-121">Export hello view tooa file</span></span>
<span data-ttu-id="6834b-122">Siga las instrucciones de hello en [Diseñador de vistas de análisis de registro](../log-analytics/log-analytics-view-designer.md) tooexport un archivo de tooa de vista.</span><span class="sxs-lookup"><span data-stu-id="6834b-122">Follow hello instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) tooexport a view tooa file.</span></span>  <span data-ttu-id="6834b-123">Hello archivo exportado se puede en formato JSON con Hola mismo [elementos como archivo de solución de hello](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="6834b-123">hello exported file will be in JSON format with hello same [elements as hello solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="6834b-124">Hola **recursos** elemento del archivo de vista de hello tendrá un recurso con un tipo de **Microsoft.OperationalInsights/workspaces** que representa Hola área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="6834b-124">hello **resources** element of hello view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents hello OMS workspace.</span></span>  <span data-ttu-id="6834b-125">Este elemento tiene un elemento secundario con un tipo de **vistas** que representa la vista de Hola y contiene su configuración detallada.</span><span class="sxs-lookup"><span data-stu-id="6834b-125">This element will have a subelement with a type of **views** that represents hello view and contains its detailed configuration.</span></span>  <span data-ttu-id="6834b-126">Copiará los detalles de Hola de este elemento y, a continuación, copiarlo en la solución.</span><span class="sxs-lookup"><span data-stu-id="6834b-126">You will copy hello details of this element and then copy it into your solution.</span></span>

## <a name="create-hello-view-resource-in-hello-solution"></a><span data-ttu-id="6834b-127">Crear recursos de la vista de hello en soluciones de Hola</span><span class="sxs-lookup"><span data-stu-id="6834b-127">Create hello view resource in hello solution</span></span>
<span data-ttu-id="6834b-128">Agregar Hola después de ver recursos toohello **recursos** elemento de su archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="6834b-128">Add hello following view resource toohello **resources** element of your solution file.</span></span>  <span data-ttu-id="6834b-129">Usa las variables que se describen a continuación y que también debe agregar.</span><span class="sxs-lookup"><span data-stu-id="6834b-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="6834b-130">Tenga en cuenta que hello **panel** y **OverviewTile** propiedades son marcadores de posición que se sobrescribirá con las propiedades correspondientes del archivo de vista exportada Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="6834b-130">Note that hello **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with hello corresponding properties from hello exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="6834b-131">Agregue Hola siguiente variables toohello variables elemento de archivo de solución de Hola y reemplace toothose de valores de hello para la solución.</span><span class="sxs-lookup"><span data-stu-id="6834b-131">Add hello following variables toohello variables element of hello solution file and replace hello values toothose for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


<span data-ttu-id="6834b-132">Tenga en cuenta que podría copiar recursos de la vista completa de Hola desde el archivo de vista exportada, pero primero necesita hello toomake sigue cambios para toowork en la solución.</span><span class="sxs-lookup"><span data-stu-id="6834b-132">Note that you could copy hello entire view resource from your exported view file, but you would need toomake hello following changes for it toowork in your solution.</span></span>  

* <span data-ttu-id="6834b-133">Hola **tipo** para la vista de hello recurso necesita toobe cambió de **vistas** demasiado**Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="6834b-133">hello **type** for hello view resource needs toobe changed from **views** too**Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="6834b-134">Hola **nombre** propiedad para el recurso de la vista de hello necesita nombre de área de trabajo de toobe cambiado tooinclude Hola.</span><span class="sxs-lookup"><span data-stu-id="6834b-134">hello **name** property for hello view resource needs toobe changed tooinclude hello workspace name.</span></span>
* <span data-ttu-id="6834b-135">dependencia de Hello en el área de trabajo de hello debe toobe quitado ya recursos del área de trabajo de hello no se ha definido en la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="6834b-135">hello dependency on hello workspace needs toobe removed since hello workspace resource isn't defined in hello solution.</span></span>
* <span data-ttu-id="6834b-136">**DisplayName** propiedad necesidades toobe agregado toohello vista.</span><span class="sxs-lookup"><span data-stu-id="6834b-136">**DisplayName** property needs toobe added toohello view.</span></span>  <span data-ttu-id="6834b-137">Hola **identificador**, **nombre**, y **DisplayName** debe coincidir.</span><span class="sxs-lookup"><span data-stu-id="6834b-137">hello **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="6834b-138">Se deben cambiar los nombres de parámetro hello toomatch requiere el conjunto de parámetros.</span><span class="sxs-lookup"><span data-stu-id="6834b-138">Parameter names must be changed toomatch hello required set of parameters.</span></span>
* <span data-ttu-id="6834b-139">Las variables deben definirse en soluciones de Hola y utiliza en las propiedades adecuadas Hola.</span><span class="sxs-lookup"><span data-stu-id="6834b-139">Variables should be defined in hello solution and used in hello appropriate properties.</span></span>

## <a name="add-hello-view-details"></a><span data-ttu-id="6834b-140">Agregar detalles de la vista de Hola</span><span class="sxs-lookup"><span data-stu-id="6834b-140">Add hello view details</span></span>
<span data-ttu-id="6834b-141">recursos de la vista de Hola Hola exportan Vista archivo contendrá dos elementos de hello **propiedades** elemento denominado **panel** y **OverviewTile** que contienen Hola configuración detallada de la vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6834b-141">hello view resource in hello exported view file will contain two elements in hello **properties** element named **Dashboard** and **OverviewTile** which contain hello detailed configuration of hello view.</span></span>  <span data-ttu-id="6834b-142">Copie estos dos elementos y su contenido en hello **propiedades** elemento de recurso de la vista de hello en el archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="6834b-142">Copy these two elements and their contents into hello **properties** element of hello view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="6834b-143">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6834b-143">Example</span></span>
<span data-ttu-id="6834b-144">Por ejemplo, hello siguiente ejemplo muestra un archivo de solución sencilla con una vista.</span><span class="sxs-lookup"><span data-stu-id="6834b-144">For example, hello following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="6834b-145">Botón de puntos suspensivos (...) se muestran para hello **panel** y **OverviewTile** contenido por razones de espacio.</span><span class="sxs-lookup"><span data-stu-id="6834b-145">Ellipses (...) are shown for hello **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="6834b-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6834b-146">Next steps</span></span>
* <span data-ttu-id="6834b-147">Obtener información detallada sobre cómo crear [soluciones de administración](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="6834b-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="6834b-148">Incluir [runbooks de Automation en la solución de administración](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="6834b-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
