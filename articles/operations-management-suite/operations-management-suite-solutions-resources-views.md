---
title: "Vistas de las soluciones de administración en Operations Management Suite (OMS) | Microsoft Docs"
description: "Normalmente, las soluciones de administración en Operations Management Suite (OMS) incluyen una o más vistas para visualizar los datos.  En este artículo se describe cómo exportar una vista creada por el Diseñador de vistas e incluirla en una solución de administración. "
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
ms.openlocfilehash: 533b5564a805e0b41f2b1a4ad92e12b133220952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="47af8-104">Vistas de las soluciones de administración en Operations Management Suite (OMS) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="47af8-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="47af8-105">La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar.</span><span class="sxs-lookup"><span data-stu-id="47af8-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="47af8-106">Cualquier esquema descrito a continuación está sujeto a cambios.</span><span class="sxs-lookup"><span data-stu-id="47af8-106">Any schema described below is subject to change.</span></span>    
>
>

<span data-ttu-id="47af8-107">[Normalmente, las soluciones de administración en Operations Management Suite (OMS)](operations-management-suite-solutions.md) incluyen una o más vistas para visualizar los datos.</span><span class="sxs-lookup"><span data-stu-id="47af8-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="47af8-108">En este artículo se describe cómo exportar una vista creada por el [Diseñador de vistas](../log-analytics/log-analytics-view-designer.md) e incluirla en una solución de administración.</span><span class="sxs-lookup"><span data-stu-id="47af8-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="47af8-109">En los ejemplos de este artículo se usan parámetros y variables que son necesarios o comunes para las soluciones de administración y se describen en [Creating management solutions in Operations Management Suite (OMS) (Creación de soluciones de administración en Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="47af8-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="47af8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="47af8-110">Prerequisites</span></span>
<span data-ttu-id="47af8-111">En este artículo se supone que ya está familiarizado con la manera de [crear una solución de administración](operations-management-suite-solutions-creating.md) y la estructura de un archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="47af8-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="47af8-112">Información general</span><span class="sxs-lookup"><span data-stu-id="47af8-112">Overview</span></span>
<span data-ttu-id="47af8-113">Para incluir una vista en una solución de administración, se crea un **recurso** para ella en el [archivo de solución](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="47af8-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="47af8-114">Sin embargo, el JSON que describe la configuración detallada de la vista detallada suele ser complejo y no algo que el autor de una solución típica podría crear manualmente.</span><span class="sxs-lookup"><span data-stu-id="47af8-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="47af8-115">El método más común es crear la vista mediante el [Diseñador de vistas](../log-analytics/log-analytics-view-designer.md), exportarla y luego agregar su configuración detallada a la solución.</span><span class="sxs-lookup"><span data-stu-id="47af8-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="47af8-116">Los pasos básicos para agregar una vista a una solución son los siguientes.</span><span class="sxs-lookup"><span data-stu-id="47af8-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="47af8-117">Cada uno de los pasos se describe en detalle en las secciones que aparecen a continuación.</span><span class="sxs-lookup"><span data-stu-id="47af8-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="47af8-118">Exportar la vista a un archivo.</span><span class="sxs-lookup"><span data-stu-id="47af8-118">Export the view to a file.</span></span>
2. <span data-ttu-id="47af8-119">Crear el recurso de la vista en la solución.</span><span class="sxs-lookup"><span data-stu-id="47af8-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="47af8-120">Agregue los detalles de la vista.</span><span class="sxs-lookup"><span data-stu-id="47af8-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="47af8-121">Exportar la vista a un archivo</span><span class="sxs-lookup"><span data-stu-id="47af8-121">Export the view to a file</span></span>
<span data-ttu-id="47af8-122">Siga las instrucciones del [Diseñador de vistas de Log Analytics](../log-analytics/log-analytics-view-designer.md) para exportar una vista a un archivo.</span><span class="sxs-lookup"><span data-stu-id="47af8-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="47af8-123">El archivo exportado tendrá el formato JSON con los mismo [elementos que el archivo de solución](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="47af8-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="47af8-124">El elemento **resources** de la vista tendrá un recurso con un tipo de **Microsoft.OperationalInsights/workspaces** que representa el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="47af8-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span></span>  <span data-ttu-id="47af8-125">Este elemento tendrá un subelemento con un tipo de **vistas** que representa la vista y contiene su configuración detallada.</span><span class="sxs-lookup"><span data-stu-id="47af8-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="47af8-126">Copiará los detalles de este elemento y luego copiará el elemento en la solución.</span><span class="sxs-lookup"><span data-stu-id="47af8-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="47af8-127">Crear el recurso de la vista en la solución</span><span class="sxs-lookup"><span data-stu-id="47af8-127">Create the view resource in the solution</span></span>
<span data-ttu-id="47af8-128">Agregue el siguiente recurso de vista al elemento **resources** del archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="47af8-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="47af8-129">Usa las variables que se describen a continuación y que también debe agregar.</span><span class="sxs-lookup"><span data-stu-id="47af8-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="47af8-130">Tenga en cuenta que las propiedades **Dashboard** y **OverviewTile** son marcadores de posición que sobrescribirá con las propiedades correspondientes desde el archivo de vista exportado.</span><span class="sxs-lookup"><span data-stu-id="47af8-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

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

<span data-ttu-id="47af8-131">Agregue las siguientes variables al elemento variables del archivo de solución y reemplace los valores por los de la solución.</span><span class="sxs-lookup"><span data-stu-id="47af8-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


<span data-ttu-id="47af8-132">Tenga en cuenta que podría copiar todo el recurso de vista desde el archivo de vista exportado, pero necesitaría realizar los siguientes cambios para que funcionara en su solución.</span><span class="sxs-lookup"><span data-stu-id="47af8-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="47af8-133">El **tipo** del recurso de vista debe cambiar de **vistas** a **Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="47af8-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="47af8-134">La propiedad **name** del recurso de vista se debe cambiar para incluir el nombre del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="47af8-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="47af8-135">La dependencia en el área de trabajo debe quitarse porque el recurso de área de trabajo no está definido en la solución.</span><span class="sxs-lookup"><span data-stu-id="47af8-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="47af8-136">La propiedad **DisplayName** se debe agregar a la vista.</span><span class="sxs-lookup"><span data-stu-id="47af8-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="47af8-137">Los valores **Id**, **Name** y **DisplayName** deben coincidir.</span><span class="sxs-lookup"><span data-stu-id="47af8-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="47af8-138">Los nombres de parámetro deben cambiarse para coincidir con el conjunto de parámetros necesario.</span><span class="sxs-lookup"><span data-stu-id="47af8-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="47af8-139">Las variables deben definirse en la solución y usarse en las propiedades adecuadas.</span><span class="sxs-lookup"><span data-stu-id="47af8-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

## <a name="add-the-view-details"></a><span data-ttu-id="47af8-140">Agregar los detalles de la vista</span><span class="sxs-lookup"><span data-stu-id="47af8-140">Add the view details</span></span>
<span data-ttu-id="47af8-141">El recurso de vista del archivo de vista exportado contendrá dos elementos en el elemento **properties** denominado **Dashboard** y **OverviewTile** que contienen la configuración detallada de la vista.</span><span class="sxs-lookup"><span data-stu-id="47af8-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="47af8-142">Copie los dos elementos y su contenido en el elemento **propiedades** del recurso de vista del archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="47af8-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="47af8-143">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="47af8-143">Example</span></span>
<span data-ttu-id="47af8-144">Por ejemplo, en el ejemplo siguiente se muestra un archivo de solución simple con una vista.</span><span class="sxs-lookup"><span data-stu-id="47af8-144">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="47af8-145">Los puntos suspensivos (...) se muestran para el contenido **Dashboard** y **OverviewTile** por motivos de espacio.</span><span class="sxs-lookup"><span data-stu-id="47af8-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="47af8-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="47af8-146">Next steps</span></span>
* <span data-ttu-id="47af8-147">Obtener información detallada sobre cómo crear [soluciones de administración](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="47af8-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="47af8-148">Incluir [runbooks de Automation en la solución de administración](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="47af8-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
