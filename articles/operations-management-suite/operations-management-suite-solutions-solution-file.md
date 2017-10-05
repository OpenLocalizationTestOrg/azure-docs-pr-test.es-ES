---
title: "Creación de soluciones de administración en Operations Management Suite (OMS) | Microsoft Docs"
description: "Las soluciones de administración amplían la funcionalidad de Operations Management Suite (OMS) proporcionando escenarios de administración empaquetados que los clientes pueden agregar a su área de trabajo de OMS.  En este artículo se proporciona información sobre cómo crear soluciones de administración que se pueden usar en su propio entorno o ponerse a disposición de sus clientes."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee3462c13101d18921dc488b08c79e1e4e02ff3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="ab52a-104">Creación de archivos de solución de administración en Operations Management Suite (OMS) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="ab52a-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="ab52a-105">La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar.</span><span class="sxs-lookup"><span data-stu-id="ab52a-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="ab52a-106">Cualquier esquema descrito a continuación está sujeto a cambios.</span><span class="sxs-lookup"><span data-stu-id="ab52a-106">Any schema described below is subject to change.</span></span>  

<span data-ttu-id="ab52a-107">Las soluciones de administración en Operations Management Suite (OMS) se implementan como [plantillas de Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="ab52a-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="ab52a-108">La tarea principal para aprender a crear soluciones de administración es saber cómo [crear una plantilla](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ab52a-108">The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="ab52a-109">En este artículo se proporcionan detalles únicos de plantillas que se usan para soluciones y sobre cómo configurar recursos de solución típicos.</span><span class="sxs-lookup"><span data-stu-id="ab52a-109">This article provides unique details of templates used for solutions and how to configure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="ab52a-110">Herramientas</span><span class="sxs-lookup"><span data-stu-id="ab52a-110">Tools</span></span>

<span data-ttu-id="ab52a-111">Puede usar cualquier editor de texto para trabajar con archivos de solución, pero se recomienda aprovechar las características proporcionadas en Visual Studio o Visual Studio Code como se describe en los siguientes artículos.</span><span class="sxs-lookup"><span data-stu-id="ab52a-111">You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.</span></span>

- [<span data-ttu-id="ab52a-112">Creación e implementación de grupos de recursos de Azure mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ab52a-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="ab52a-113">Trabajo con plantillas de Azure Resource Manager en Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ab52a-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="ab52a-114">sección Estructura</span><span class="sxs-lookup"><span data-stu-id="ab52a-114">Structure</span></span>
<span data-ttu-id="ab52a-115">La estructura básica de un archivo de una solución de administración, que se muestra a continuación, es la misma que la de una [plantilla de Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#template-format).</span><span class="sxs-lookup"><span data-stu-id="ab52a-115">The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="ab52a-116">En cada una de las siguientes secciones se describen los elementos de nivel superior y su contenido en una solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-116">Each of the sections below describes the top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="ab52a-117">Parámetros</span><span class="sxs-lookup"><span data-stu-id="ab52a-117">Parameters</span></span>
<span data-ttu-id="ab52a-118">Los [parámetros](../azure-resource-manager/resource-group-authoring-templates.md#parameters) son valores que el usuario le debe proporcionar al instalar la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="ab52a-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.</span></span>  <span data-ttu-id="ab52a-119">Hay parámetros estándar que tendrán todas las soluciones, y puede agregar parámetros adicionales según sea necesario para su solución particular.</span><span class="sxs-lookup"><span data-stu-id="ab52a-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="ab52a-120">La manera en que los usuarios proporcionarán valores de parámetros al instalar la solución dependerá del parámetro particular y de cómo se instala la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-120">How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.</span></span>

<span data-ttu-id="ab52a-121">Cuando un usuario instala su solución de administración mediante plantillas de [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) o [de inicio rápido de Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions), se le pide que seleccione un [área de trabajo de OMS y una cuenta de Automation](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="ab52a-121">When a user installs your management solution through the [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted to select an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="ab52a-122">Estos se usan para rellenar los valores de cada uno de los parámetros estándar.</span><span class="sxs-lookup"><span data-stu-id="ab52a-122">These are used to populate the values of each of the standard parameters.</span></span>  <span data-ttu-id="ab52a-123">Al usuario no se le pide que proporcione valores directamente para los parámetros estándar, pero se le pide que proporcione valores para cualquier parámetro adicional.</span><span class="sxs-lookup"><span data-stu-id="ab52a-123">The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.</span></span>

<span data-ttu-id="ab52a-124">Cuando el usuario instala la solución [otro método](operations-management-suite-solutions.md#finding-and-installing-management-solutions), debe proporcionar un valor para todos los parámetros estándar y todos los parámetros adicionales.</span><span class="sxs-lookup"><span data-stu-id="ab52a-124">When the user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="ab52a-125">A continuación se muestra un parámetro de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ab52a-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="ab52a-126">En la tabla siguiente se describen los atributos de un parámetro.</span><span class="sxs-lookup"><span data-stu-id="ab52a-126">The following table describes the attributes of a parameter.</span></span>

| <span data-ttu-id="ab52a-127">Atributo</span><span class="sxs-lookup"><span data-stu-id="ab52a-127">Attribute</span></span> | <span data-ttu-id="ab52a-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="ab52a-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ab52a-129">type</span><span class="sxs-lookup"><span data-stu-id="ab52a-129">type</span></span> |<span data-ttu-id="ab52a-130">Tipo de datos para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="ab52a-130">Data type for the parameter.</span></span> <span data-ttu-id="ab52a-131">El control de entrada que se muestra para el usuario depende del tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="ab52a-131">The input control displayed for the user depends on the data type.</span></span><br><br><span data-ttu-id="ab52a-132">bool: cuadro desplegable</span><span class="sxs-lookup"><span data-stu-id="ab52a-132">bool - Drop down box</span></span><br><span data-ttu-id="ab52a-133">string: cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="ab52a-133">string - Text box</span></span><br><span data-ttu-id="ab52a-134">int: cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="ab52a-134">int - Text box</span></span><br><span data-ttu-id="ab52a-135">Securestring: campo de contraseña</span><span class="sxs-lookup"><span data-stu-id="ab52a-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="ab52a-136">categoría</span><span class="sxs-lookup"><span data-stu-id="ab52a-136">category</span></span> |<span data-ttu-id="ab52a-137">Categoría opcional para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="ab52a-137">Optional category for the parameter.</span></span>  <span data-ttu-id="ab52a-138">Los parámetros de la misma categoría se agrupan juntos.</span><span class="sxs-lookup"><span data-stu-id="ab52a-138">Parameters in the same category are grouped together.</span></span> |
| <span data-ttu-id="ab52a-139">control</span><span class="sxs-lookup"><span data-stu-id="ab52a-139">control</span></span> |<span data-ttu-id="ab52a-140">Funcionalidad adicional para los parámetros de cadena.</span><span class="sxs-lookup"><span data-stu-id="ab52a-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="ab52a-141">datetime: se muestra el control de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="ab52a-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="ab52a-142">guid: el valor del GUID se genera automáticamente y no se muestra el parámetro.</span><span class="sxs-lookup"><span data-stu-id="ab52a-142">guid - Guid value is automatically generated, and the parameter is not displayed.</span></span> |
| <span data-ttu-id="ab52a-143">Description</span><span class="sxs-lookup"><span data-stu-id="ab52a-143">description</span></span> |<span data-ttu-id="ab52a-144">Descripción opcional del parámetro.</span><span class="sxs-lookup"><span data-stu-id="ab52a-144">Optional description for the parameter.</span></span>  <span data-ttu-id="ab52a-145">Se muestra en un globo de información junto al parámetro.</span><span class="sxs-lookup"><span data-stu-id="ab52a-145">Displayed in an information balloon next to the parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="ab52a-146">Parámetros estándar</span><span class="sxs-lookup"><span data-stu-id="ab52a-146">Standard parameters</span></span>
<span data-ttu-id="ab52a-147">En la tabla siguiente se enumeran los parámetros estándar de todas las soluciones de administración.</span><span class="sxs-lookup"><span data-stu-id="ab52a-147">The following table lists the standard parameters for all management solutions.</span></span>  <span data-ttu-id="ab52a-148">Estos valores se rellenan para el usuario en lugar de pedírseles cuando se instala la solución desde las plantillas de Azure Marketplace o de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="ab52a-148">These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="ab52a-149">El usuario debe proporcionar los valores si la solución se instala con otro método.</span><span class="sxs-lookup"><span data-stu-id="ab52a-149">The user must provide values for them if the solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="ab52a-150">La interfaz de usuario de las plantillas de Azure Marketplace y de inicio rápido espera los nombres de parámetro en la tabla.</span><span class="sxs-lookup"><span data-stu-id="ab52a-150">The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.</span></span>  <span data-ttu-id="ab52a-151">Si usa nombres de parámetros diferentes, se le preguntarán al usuario y no se rellenarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ab52a-151">If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="ab52a-152">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ab52a-152">Parameter</span></span> | <span data-ttu-id="ab52a-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="ab52a-153">Type</span></span> | <span data-ttu-id="ab52a-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="ab52a-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ab52a-155">accountName</span><span class="sxs-lookup"><span data-stu-id="ab52a-155">accountName</span></span> |<span data-ttu-id="ab52a-156">string</span><span class="sxs-lookup"><span data-stu-id="ab52a-156">string</span></span> |<span data-ttu-id="ab52a-157">Nombre de la cuenta de Automation de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab52a-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="ab52a-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="ab52a-158">pricingTier</span></span> |<span data-ttu-id="ab52a-159">string</span><span class="sxs-lookup"><span data-stu-id="ab52a-159">string</span></span> |<span data-ttu-id="ab52a-160">Plan de tarifa del área de trabajo de Log Analytics y de la cuenta de Automation de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab52a-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="ab52a-161">regionId</span><span class="sxs-lookup"><span data-stu-id="ab52a-161">regionId</span></span> |<span data-ttu-id="ab52a-162">string</span><span class="sxs-lookup"><span data-stu-id="ab52a-162">string</span></span> |<span data-ttu-id="ab52a-163">Región de la cuenta de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ab52a-163">Region of the Azure Automation account.</span></span> |
| <span data-ttu-id="ab52a-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="ab52a-164">solutionName</span></span> |<span data-ttu-id="ab52a-165">string</span><span class="sxs-lookup"><span data-stu-id="ab52a-165">string</span></span> |<span data-ttu-id="ab52a-166">Nombre de la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-166">Name of the solution.</span></span>  <span data-ttu-id="ab52a-167">Si va a implementar la solución a través de plantillas de inicio rápido, debe definir solutionName como parámetro para poder definir una cadena en lugar de pedir al usuario que especifique una.</span><span class="sxs-lookup"><span data-stu-id="ab52a-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one.</span></span> |
| <span data-ttu-id="ab52a-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="ab52a-168">workspaceName</span></span> |<span data-ttu-id="ab52a-169">string</span><span class="sxs-lookup"><span data-stu-id="ab52a-169">string</span></span> |<span data-ttu-id="ab52a-170">Nombre del área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ab52a-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="ab52a-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="ab52a-171">workspaceRegionId</span></span> |<span data-ttu-id="ab52a-172">string</span><span class="sxs-lookup"><span data-stu-id="ab52a-172">string</span></span> |<span data-ttu-id="ab52a-173">Región del área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ab52a-173">Region of the Log Analytics workspace.</span></span> |


<span data-ttu-id="ab52a-174">Esta es la estructura de los parámetros estándar que puede copiar y pegar en el archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-174">Following is the structure of the standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of the Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of the Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="ab52a-175">Consulte los valores de parámetro de otros elementos de la solución con la sintaxis **parameters('nombre de parámetro')**.</span><span class="sxs-lookup"><span data-stu-id="ab52a-175">You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="ab52a-176">Por ejemplo, para tener acceso al nombre de área de trabajo, use **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="ab52a-176">For example, to access the workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="ab52a-177">Variables</span><span class="sxs-lookup"><span data-stu-id="ab52a-177">Variables</span></span>
<span data-ttu-id="ab52a-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) son valores que usará en el resto de la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="ab52a-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.</span></span>  <span data-ttu-id="ab52a-179">Estos valores no se exponen al usuario que instala la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-179">These values are not exposed to the user installing the solution.</span></span>  <span data-ttu-id="ab52a-180">Están destinados a proporcionar al creador una única ubicación donde pueda administrar los valores que pueden utilizarse varias veces a lo largo de la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-180">They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution.</span></span> <span data-ttu-id="ab52a-181">Debe colocar los valores específicos para su solución en variables en lugar de codificarlos de forma rígida en el elemento **resources**.</span><span class="sxs-lookup"><span data-stu-id="ab52a-181">You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.</span></span>  <span data-ttu-id="ab52a-182">De este modo, el código es más legible y los valores se pueden cambiar fácilmente en versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="ab52a-182">This makes the code more readable and allows you to easily change these values in later versions.</span></span>

<span data-ttu-id="ab52a-183">A continuación se muestra un ejemplo del elemento **variables** con parámetros típicos usados en las soluciones.</span><span class="sxs-lookup"><span data-stu-id="ab52a-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="ab52a-184">Consulte los valores de las variables a través de la solución con la sintaxis **variables('nombre de variable')**.</span><span class="sxs-lookup"><span data-stu-id="ab52a-184">You refer to variable values through the solution with the syntax **variables('variable name')**.</span></span>  <span data-ttu-id="ab52a-185">Por ejemplo, para tener acceso a la variable SolutionName, se usaría **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="ab52a-185">For example, to access the SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="ab52a-186">También puede definir variables complejas en varios conjuntos de valores.</span><span class="sxs-lookup"><span data-stu-id="ab52a-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="ab52a-187">Estas son especialmente útiles en soluciones de administración cuando se definen varias propiedades para diferentes tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="ab52a-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="ab52a-188">Por ejemplo, puede reestructurar las variables de solución mostradas anteriormente a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="ab52a-188">For example, you could restructure the solution variables shown above to the following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="ab52a-189">En este caso, consulte los valores de las variables a través de la solución con la sintaxis **variables('nombre de variable').property**.</span><span class="sxs-lookup"><span data-stu-id="ab52a-189">In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="ab52a-190">Por ejemplo, para tener acceso a la variable SolutionName, se usaría **variables('Solution').Name**.</span><span class="sxs-lookup"><span data-stu-id="ab52a-190">For example, to access the Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="ab52a-191">Recursos</span><span class="sxs-lookup"><span data-stu-id="ab52a-191">Resources</span></span>
<span data-ttu-id="ab52a-192">[Recursos](../azure-resource-manager/resource-group-authoring-templates.md#resources) define los diferentes recursos que instalará y configurará la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="ab52a-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="ab52a-193">Se trata de la parte más grande y compleja de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ab52a-193">This will be the largest and most complex portion of the template.</span></span>  <span data-ttu-id="ab52a-194">Puede obtener la estructura y la descripción completa de los elementos de recurso en [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="ab52a-194">You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="ab52a-195">Se detallan distintos recursos que se definirán normalmente en otros artículos en esta documentación.</span><span class="sxs-lookup"><span data-stu-id="ab52a-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="ab52a-196">Dependencias</span><span class="sxs-lookup"><span data-stu-id="ab52a-196">Dependencies</span></span>
<span data-ttu-id="ab52a-197">El elemento **dependsOn** especifica una [dependencia](../azure-resource-manager/resource-group-define-dependencies.md) en otro recurso.</span><span class="sxs-lookup"><span data-stu-id="ab52a-197">The **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="ab52a-198">Cuando se instala la solución, un recurso no se crea hasta que no se hayan creado todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="ab52a-198">When the solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="ab52a-199">Por ejemplo, puede que su solución [inicie un runbook](operations-management-suite-solutions-resources-automation.md#runbooks) cuando se instala mediante un [recurso de trabajo](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="ab52a-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="ab52a-200">El recurso de trabajo será dependiente del recurso de runbook para asegurarse de que el runbook se crea antes de que se cree el trabajo.</span><span class="sxs-lookup"><span data-stu-id="ab52a-200">The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="ab52a-201">Área de trabajo de OMS y cuenta de Automation</span><span class="sxs-lookup"><span data-stu-id="ab52a-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="ab52a-202">La mayoría de las soluciones requieren que un [área de trabajo de OMS](../log-analytics/log-analytics-manage-access.md) contenga vistas y que una [cuenta de Automation](../automation/automation-security-overview.md#automation-account-overview) contenga runbooks y recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="ab52a-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span>  <span data-ttu-id="ab52a-203">Estos deben estar disponibles antes de que se creen los recursos de la solución y no se deben definir en la propia solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-203">These must be available before the resources in the solution are created and should not be defined in the solution itself.</span></span>  <span data-ttu-id="ab52a-204">El usuario [especificará un área de trabajo y una cuenta](operations-management-suite-solutions.md#oms-workspace-and-automation-account) al implementar la solución, pero usted, como autor, debe tener en cuenta los siguientes puntos.</span><span class="sxs-lookup"><span data-stu-id="ab52a-204">The user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="ab52a-205">Recursos de solución</span><span class="sxs-lookup"><span data-stu-id="ab52a-205">Solution resource</span></span>
<span data-ttu-id="ab52a-206">Cada solución requiere una entrada de recursos en el elemento **resources** que define la propia solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-206">Each solution requires a resource entry in the **resources** element that defines the solution itself.</span></span>  <span data-ttu-id="ab52a-207">Esto tendrá un tipo de **Microsoft.OperationsManagement/solutions** y tener la siguiente estructura.</span><span class="sxs-lookup"><span data-stu-id="ab52a-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure.</span></span> <span data-ttu-id="ab52a-208">Esto incluye [parámetros estándar](#parameters) y [variables](#variables) que se usan normalmente para definir las propiedades de la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="ab52a-209">Dependencias</span><span class="sxs-lookup"><span data-stu-id="ab52a-209">Dependencies</span></span>
<span data-ttu-id="ab52a-210">El recurso de la solución debe tener un [dependencia](../azure-resource-manager/resource-group-define-dependencies.md) en todos los recursos de la solución, ya que estos deben existir antes de que se cree la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-210">The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.</span></span>  <span data-ttu-id="ab52a-211">Para ello, agregue una entrada para cada recurso en el elemento **dependsOn**.</span><span class="sxs-lookup"><span data-stu-id="ab52a-211">You do this by adding an entry for each resource in the **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="ab52a-212">Propiedades</span><span class="sxs-lookup"><span data-stu-id="ab52a-212">Properties</span></span>
<span data-ttu-id="ab52a-213">Este recurso de la solución tiene las propiedades de la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="ab52a-213">The solution resource has the properties in the following table.</span></span>  <span data-ttu-id="ab52a-214">Esto incluye los recursos a los que hace referencia la solución y contenidos en ella, que define cómo se administra el recurso después de instalar la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-214">This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.</span></span>  <span data-ttu-id="ab52a-215">Cada recurso de la solución debe aparecer en una de las propiedades **referencedResources** o **containedResources**.</span><span class="sxs-lookup"><span data-stu-id="ab52a-215">Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.</span></span>

| <span data-ttu-id="ab52a-216">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ab52a-216">Property</span></span> | <span data-ttu-id="ab52a-217">Descripción</span><span class="sxs-lookup"><span data-stu-id="ab52a-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ab52a-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="ab52a-218">workspaceResourceId</span></span> |<span data-ttu-id="ab52a-219">Identificador del área de trabajo de Log Analytics en el formulario *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nombre del espacio de trabajo\>*.</span><span class="sxs-lookup"><span data-stu-id="ab52a-219">ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="ab52a-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="ab52a-220">referencedResources</span></span> |<span data-ttu-id="ab52a-221">Lista de recursos de la solución que no se deben quitar cuando se quita la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-221">List of resources in the solution that should not be removed when the solution is removed.</span></span> |
| <span data-ttu-id="ab52a-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="ab52a-222">containedResources</span></span> |<span data-ttu-id="ab52a-223">Lista de recursos de la solución que debe quitarse cuando se quita la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-223">List of resources in the solution that should be removed when the solution is removed.</span></span> |

<span data-ttu-id="ab52a-224">El ejemplo anterior es para una solución con un runbook, una programación y una vista.</span><span class="sxs-lookup"><span data-stu-id="ab52a-224">The example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="ab52a-225">Se hace *referencia a la programación y al runbook* en el elemento **properties** de modo que no se quitan cuando se quita la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-225">The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.</span></span>  <span data-ttu-id="ab52a-226">La vista está *contenida*, por lo que se quita cuando se quita la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-226">The view is *contained* so it is removed when the solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="ab52a-227">Plan</span><span class="sxs-lookup"><span data-stu-id="ab52a-227">Plan</span></span>
<span data-ttu-id="ab52a-228">La entidad **plan** del recurso de la solución tiene las propiedades en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="ab52a-228">The **plan** entity of the solution resource has the properties in the following table.</span></span>

| <span data-ttu-id="ab52a-229">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ab52a-229">Property</span></span> | <span data-ttu-id="ab52a-230">Description</span><span class="sxs-lookup"><span data-stu-id="ab52a-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ab52a-231">name</span><span class="sxs-lookup"><span data-stu-id="ab52a-231">name</span></span> |<span data-ttu-id="ab52a-232">Nombre de la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-232">Name of the solution.</span></span> |
| <span data-ttu-id="ab52a-233">versión</span><span class="sxs-lookup"><span data-stu-id="ab52a-233">version</span></span> |<span data-ttu-id="ab52a-234">Versión de la solución según determine el autor.</span><span class="sxs-lookup"><span data-stu-id="ab52a-234">Version of the solution as determined by the author.</span></span> |
| <span data-ttu-id="ab52a-235">product</span><span class="sxs-lookup"><span data-stu-id="ab52a-235">product</span></span> |<span data-ttu-id="ab52a-236">Cadena única para identificar la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-236">Unique string to identify the solution.</span></span> |
| <span data-ttu-id="ab52a-237">publisher</span><span class="sxs-lookup"><span data-stu-id="ab52a-237">publisher</span></span> |<span data-ttu-id="ab52a-238">Publicador de la solución.</span><span class="sxs-lookup"><span data-stu-id="ab52a-238">Publisher of the solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="ab52a-239">Muestra</span><span class="sxs-lookup"><span data-stu-id="ab52a-239">Sample</span></span>
<span data-ttu-id="ab52a-240">Puede ver ejemplos de archivos de solución con un recurso de la solución en las siguientes ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="ab52a-240">You can view samples of solution files with a solution resource at the following locations.</span></span>

- [<span data-ttu-id="ab52a-241">Recursos de Automation</span><span class="sxs-lookup"><span data-stu-id="ab52a-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="ab52a-242">Recursos de búsqueda y alerta</span><span class="sxs-lookup"><span data-stu-id="ab52a-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="ab52a-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab52a-243">Next steps</span></span>
* <span data-ttu-id="ab52a-244">[Incorporación de búsquedas y alertas guardadas](operations-management-suite-solutions-resources-searches-alerts.md) a la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="ab52a-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) to your management solution.</span></span>
* <span data-ttu-id="ab52a-245">[Incorporación de vistas](operations-management-suite-solutions-resources-views.md) a la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="ab52a-245">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="ab52a-246">[Incorporación de runbooks de y otros recursos Automation](operations-management-suite-solutions-resources-automation.md) a la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="ab52a-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>
* <span data-ttu-id="ab52a-247">Obtenga más información en [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ab52a-247">Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="ab52a-248">Búsqueda de [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates) para obtener ejemplos de diferentes plantillas de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ab52a-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
