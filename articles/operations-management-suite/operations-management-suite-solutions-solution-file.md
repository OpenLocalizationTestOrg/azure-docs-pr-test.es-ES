---
title: "soluciones de administración de aaaCreating en Operations Management Suite (OMS) | Documentos de Microsoft"
description: "Soluciones de administración de amplían la funcionalidad de Hola de Operations Management Suite (OMS) proporcionando escenarios de administración empaquetada que los clientes pueden agregar área de trabajo OMS tootheir.  Este artículo proporciona detalles sobre cómo puede crear toobe de soluciones de administración usan en su propio entorno o estará disponible tooyour clientes."
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
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="70b0f-104">Creación de archivos de solución de administración en Operations Management Suite (OMS) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="70b0f-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="70b0f-105">La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar.</span><span class="sxs-lookup"><span data-stu-id="70b0f-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="70b0f-106">Cualquier esquema que se describe a continuación es toochange de asunto.</span><span class="sxs-lookup"><span data-stu-id="70b0f-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="70b0f-107">Las soluciones de administración en Operations Management Suite (OMS) se implementan como [plantillas de Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="70b0f-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="70b0f-108">la tarea principal Hello para aprender cómo las soluciones de administración de tooauthor es aprender cómo demasiado[crear una plantilla de](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="70b0f-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="70b0f-109">Este artículo proporciona detalles únicos de plantillas que se utilizan para las soluciones y cómo tooconfigure recursos de solución típica.</span><span class="sxs-lookup"><span data-stu-id="70b0f-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="70b0f-110">Herramientas</span><span class="sxs-lookup"><span data-stu-id="70b0f-110">Tools</span></span>

<span data-ttu-id="70b0f-111">Puede usar cualquier toowork de editor de texto con archivos de solución, pero se recomienda que aprovecha las características de hello proporcionadas en Visual Studio o código de Visual Studio como se describe en los siguientes artículos de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="70b0f-112">Creación e implementación de grupos de recursos de Azure mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="70b0f-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="70b0f-113">Trabajo con plantillas de Azure Resource Manager en Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="70b0f-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="70b0f-114">sección Estructura</span><span class="sxs-lookup"><span data-stu-id="70b0f-114">Structure</span></span>
<span data-ttu-id="70b0f-115">estructura básica de Hola de un archivo de solución de administración es Hola igual que un [plantilla del Administrador de recursos](../azure-resource-manager/resource-group-authoring-templates.md#template-format) que es como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="70b0f-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="70b0f-116">Cada uno de hello las siguientes secciones describe los elementos de nivel superior de Hola y y su contenido en una solución.</span><span class="sxs-lookup"><span data-stu-id="70b0f-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="70b0f-117">parameters</span><span class="sxs-lookup"><span data-stu-id="70b0f-117">Parameters</span></span>
<span data-ttu-id="70b0f-118">[Parámetros](../azure-resource-manager/resource-group-authoring-templates.md#parameters) son valores que necesita de usuario de hello cuando instala la solución de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="70b0f-119">Hay parámetros estándar que tendrán todas las soluciones, y puede agregar parámetros adicionales según sea necesario para su solución particular.</span><span class="sxs-lookup"><span data-stu-id="70b0f-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="70b0f-120">Cómo los usuarios proporcionar valores de parámetro cuando instala la solución dependerá parámetro concreto de Hola y cómo se instala la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="70b0f-121">Cuando un usuario instala la solución de administración a través de hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) o [plantillas de inicio rápido de Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) son tooselect solicitada un [OMS área de trabajo y la cuenta de automatización ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="70b0f-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="70b0f-122">Éstos son valores de hello toopopulate utilizadas de cada uno de los parámetros estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="70b0f-123">no se solicita el usuario de Hello toodirectly proporcionar valores para parámetros estándar de hello, pero son valores tooprovide solicitadas para cualquier parámetro adicional.</span><span class="sxs-lookup"><span data-stu-id="70b0f-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="70b0f-124">Si instala la solución de usuario de hello [otro método](operations-management-suite-solutions.md#finding-and-installing-management-solutions), debe proporcionar un valor para todos los parámetros estándares y todos los parámetros adicionales.</span><span class="sxs-lookup"><span data-stu-id="70b0f-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="70b0f-125">A continuación se muestra un parámetro de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="70b0f-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="70b0f-126">Hello en la tabla siguiente describe los atributos de Hola de un parámetro.</span><span class="sxs-lookup"><span data-stu-id="70b0f-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="70b0f-127">Atributo</span><span class="sxs-lookup"><span data-stu-id="70b0f-127">Attribute</span></span> | <span data-ttu-id="70b0f-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="70b0f-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="70b0f-129">type</span><span class="sxs-lookup"><span data-stu-id="70b0f-129">type</span></span> |<span data-ttu-id="70b0f-130">Tipo de datos de parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="70b0f-130">Data type for hello parameter.</span></span> <span data-ttu-id="70b0f-131">control de entrada de Hola que se muestran para el usuario de hello depende de tipo de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="70b0f-132">bool: cuadro desplegable</span><span class="sxs-lookup"><span data-stu-id="70b0f-132">bool - Drop down box</span></span><br><span data-ttu-id="70b0f-133">string: cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="70b0f-133">string - Text box</span></span><br><span data-ttu-id="70b0f-134">int: cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="70b0f-134">int - Text box</span></span><br><span data-ttu-id="70b0f-135">Securestring: campo de contraseña</span><span class="sxs-lookup"><span data-stu-id="70b0f-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="70b0f-136">categoría</span><span class="sxs-lookup"><span data-stu-id="70b0f-136">category</span></span> |<span data-ttu-id="70b0f-137">Categoría opcional para el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="70b0f-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="70b0f-138">Parámetros en la misma categoría se agrupan de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="70b0f-139">control</span><span class="sxs-lookup"><span data-stu-id="70b0f-139">control</span></span> |<span data-ttu-id="70b0f-140">Funcionalidad adicional para los parámetros de cadena.</span><span class="sxs-lookup"><span data-stu-id="70b0f-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="70b0f-141">datetime: se muestra el control de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="70b0f-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="70b0f-142">GUID - valor Guid se genera automáticamente y no se muestra el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="70b0f-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="70b0f-143">description</span><span class="sxs-lookup"><span data-stu-id="70b0f-143">description</span></span> |<span data-ttu-id="70b0f-144">Descripción opcional para el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="70b0f-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="70b0f-145">Se muestran en un parámetro de toohello siguiente de globo de información.</span><span class="sxs-lookup"><span data-stu-id="70b0f-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="70b0f-146">Parámetros estándar</span><span class="sxs-lookup"><span data-stu-id="70b0f-146">Standard parameters</span></span>
<span data-ttu-id="70b0f-147">Hello tabla siguiente enumeran los parámetros estándar de Hola para todas las soluciones de administración.</span><span class="sxs-lookup"><span data-stu-id="70b0f-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="70b0f-148">Estos valores se rellenan para el usuario de hello en lugar de solicitar para ellos cuando se instala la solución de plantillas de Azure Marketplace o inicio rápido de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="70b0f-149">usuario de Hello debe proporcionar valores para ellos si se instala la solución de hello con otro método.</span><span class="sxs-lookup"><span data-stu-id="70b0f-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="70b0f-150">interfaz de usuario de Hello en plantillas de Azure Marketplace y de inicio rápido de hello espera nombres de parámetro de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="70b0f-151">Si utiliza distintos nombres de parámetro, a continuación, se pedirá usuario Hola para ellos y no se rellenarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="70b0f-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="70b0f-152">Parámetro</span><span class="sxs-lookup"><span data-stu-id="70b0f-152">Parameter</span></span> | <span data-ttu-id="70b0f-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="70b0f-153">Type</span></span> | <span data-ttu-id="70b0f-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="70b0f-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="70b0f-155">accountName</span><span class="sxs-lookup"><span data-stu-id="70b0f-155">accountName</span></span> |<span data-ttu-id="70b0f-156">string</span><span class="sxs-lookup"><span data-stu-id="70b0f-156">string</span></span> |<span data-ttu-id="70b0f-157">Nombre de la cuenta de Automation de Azure.</span><span class="sxs-lookup"><span data-stu-id="70b0f-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="70b0f-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="70b0f-158">pricingTier</span></span> |<span data-ttu-id="70b0f-159">string</span><span class="sxs-lookup"><span data-stu-id="70b0f-159">string</span></span> |<span data-ttu-id="70b0f-160">Plan de tarifa del área de trabajo de Log Analytics y de la cuenta de Automation de Azure.</span><span class="sxs-lookup"><span data-stu-id="70b0f-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="70b0f-161">regionId</span><span class="sxs-lookup"><span data-stu-id="70b0f-161">regionId</span></span> |<span data-ttu-id="70b0f-162">cadena</span><span class="sxs-lookup"><span data-stu-id="70b0f-162">string</span></span> |<span data-ttu-id="70b0f-163">Región de hello cuenta de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="70b0f-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="70b0f-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="70b0f-164">solutionName</span></span> |<span data-ttu-id="70b0f-165">cadena</span><span class="sxs-lookup"><span data-stu-id="70b0f-165">string</span></span> |<span data-ttu-id="70b0f-166">Nombre de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-166">Name of hello solution.</span></span>  <span data-ttu-id="70b0f-167">Si va a implementar la solución a través de plantillas de inicio rápido, a continuación, debe definir solutionName como un parámetro para que pueda definir una cadena en su lugar que requieren Hola usuario toospecify uno.</span><span class="sxs-lookup"><span data-stu-id="70b0f-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="70b0f-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="70b0f-168">workspaceName</span></span> |<span data-ttu-id="70b0f-169">string</span><span class="sxs-lookup"><span data-stu-id="70b0f-169">string</span></span> |<span data-ttu-id="70b0f-170">Nombre del área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="70b0f-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="70b0f-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="70b0f-171">workspaceRegionId</span></span> |<span data-ttu-id="70b0f-172">cadena</span><span class="sxs-lookup"><span data-stu-id="70b0f-172">string</span></span> |<span data-ttu-id="70b0f-173">Región del área de trabajo de análisis de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="70b0f-174">Aquí te mostramos estructura Hola de los parámetros estándar de Hola que puede copiar y pegar en el archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="70b0f-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

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
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="70b0f-175">Consulte tooparameter valores de otros elementos de solución de hello con sintaxis de hello **parámetros ('parameter name')**.</span><span class="sxs-lookup"><span data-stu-id="70b0f-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="70b0f-176">Por ejemplo, tooaccess Hola nombre de área de trabajo, usaría **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="70b0f-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="70b0f-177">variables</span><span class="sxs-lookup"><span data-stu-id="70b0f-177">Variables</span></span>
<span data-ttu-id="70b0f-178">[Las variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) son valores que se va a utilizar en el resto de Hola de solución de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="70b0f-179">Estos valores no son usuario toohello expuesto instalar Hola solución.</span><span class="sxs-lookup"><span data-stu-id="70b0f-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="70b0f-180">Únicamente son autor de hello tooprovide previsto con una única ubicación que pueden administrar los valores que se pueden usar varias veces a lo largo de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="70b0f-181">Debe colocar cualquier solución de tooyour específico de valores en variables como toohard lugar su codificación en hello **recursos** elemento.</span><span class="sxs-lookup"><span data-stu-id="70b0f-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="70b0f-182">Esto hace que el código de hello sea más legible y le permite tooeasily cambiar estos valores en versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="70b0f-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="70b0f-183">A continuación se muestra un ejemplo del elemento **variables** con parámetros típicos usados en las soluciones.</span><span class="sxs-lookup"><span data-stu-id="70b0f-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="70b0f-184">Consulte toovariable valores a través de la solución de hello con sintaxis de hello **variables ('variable name')**.</span><span class="sxs-lookup"><span data-stu-id="70b0f-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="70b0f-185">Por ejemplo, tooaccess Hola SolutionName variable, usaría **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="70b0f-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="70b0f-186">También puede definir variables complejas en varios conjuntos de valores.</span><span class="sxs-lookup"><span data-stu-id="70b0f-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="70b0f-187">Estas son especialmente útiles en soluciones de administración cuando se definen varias propiedades para diferentes tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="70b0f-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="70b0f-188">Por ejemplo, puede reestructurar las variables de solución de hello mostradas anteriormente toohello siguiente.</span><span class="sxs-lookup"><span data-stu-id="70b0f-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="70b0f-189">En este caso, consulte toovariable valores a través de la solución de hello con sintaxis de hello **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="70b0f-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="70b0f-190">Por ejemplo, tooaccess Hola variable de nombre de la solución, usaría **variables('Solution'). Nombre**.</span><span class="sxs-lookup"><span data-stu-id="70b0f-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="70b0f-191">Recursos</span><span class="sxs-lookup"><span data-stu-id="70b0f-191">Resources</span></span>
<span data-ttu-id="70b0f-192">[Recursos](../azure-resource-manager/resource-group-authoring-templates.md#resources) definen los recursos diferentes de Hola que instalará y configurará la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="70b0f-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="70b0f-193">Se trata de hello más grande y más complejo parte de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="70b0f-194">Puede obtener estructura hello y una descripción completa de los elementos de recurso de [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="70b0f-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="70b0f-195">Se detallan distintos recursos que se definirán normalmente en otros artículos en esta documentación.</span><span class="sxs-lookup"><span data-stu-id="70b0f-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="70b0f-196">Dependencias</span><span class="sxs-lookup"><span data-stu-id="70b0f-196">Dependencies</span></span>
<span data-ttu-id="70b0f-197">Hola **dependsOn** elementos especifica un [dependencia](../azure-resource-manager/resource-group-define-dependencies.md) en otro recurso.</span><span class="sxs-lookup"><span data-stu-id="70b0f-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="70b0f-198">Cuando se instala la solución de hello, no se crea un recurso hasta que todas sus dependencias se han creado.</span><span class="sxs-lookup"><span data-stu-id="70b0f-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="70b0f-199">Por ejemplo, puede que su solución [inicie un runbook](operations-management-suite-solutions-resources-automation.md#runbooks) cuando se instala mediante un [recurso de trabajo](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="70b0f-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="70b0f-200">recursos de trabajo de Hello sería depende Hola runbook recursos toomake seguro que se crea ese runbook Hola antes de que se crea el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="70b0f-201">Área de trabajo de OMS y cuenta de Automation</span><span class="sxs-lookup"><span data-stu-id="70b0f-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="70b0f-202">Las soluciones de administración requieren un [área de trabajo OMS](../log-analytics/log-analytics-manage-access.md) toocontain vistas y una [cuenta de automatización](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks y recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="70b0f-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="70b0f-203">Estos deben estar disponibles antes de hello recursos de solución de Hola se crean y no deben definirse en la solución de hello propio.</span><span class="sxs-lookup"><span data-stu-id="70b0f-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="70b0f-204">usuario de Hello le [especificar un área de trabajo y una cuenta de](operations-management-suite-solutions.md#oms-workspace-and-automation-account) cuando implementa la solución, pero como autor de hello debe considerar Hola después de puntos.</span><span class="sxs-lookup"><span data-stu-id="70b0f-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="70b0f-205">Recursos de solución</span><span class="sxs-lookup"><span data-stu-id="70b0f-205">Solution resource</span></span>
<span data-ttu-id="70b0f-206">Cada solución requiere una entrada de recurso en hello **recursos** elemento que define la propia solución Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="70b0f-207">Esto tendrá un tipo de **Microsoft.OperationsManagement/solutions** y tener Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="70b0f-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="70b0f-208">Esto incluye [parámetros estándar](#parameters) y [variables](#variables) que están toodefine normalmente se usan propiedades de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


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




### <a name="dependencies"></a><span data-ttu-id="70b0f-209">Dependencias</span><span class="sxs-lookup"><span data-stu-id="70b0f-209">Dependencies</span></span>
<span data-ttu-id="70b0f-210">recursos de solución de Hello deben tener un [dependencia](../azure-resource-manager/resource-group-define-dependencies.md) en todos los recursos de solución de hello puesto que necesiten tooexist antes de crear una solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="70b0f-211">Para ello, agrega una entrada para cada recurso en hello **dependsOn** elemento.</span><span class="sxs-lookup"><span data-stu-id="70b0f-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="70b0f-212">Propiedades</span><span class="sxs-lookup"><span data-stu-id="70b0f-212">Properties</span></span>
<span data-ttu-id="70b0f-213">recursos de solución de Hello tiene propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="70b0f-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="70b0f-214">Esto incluye recursos de hello al que hace referencia y contenido en la solución de Hola que define cómo se administran los recursos de hello después de instala la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="70b0f-215">Cada recurso de solución de hello debe aparecer en cualquier hello **referencedResources** o hello **containedResources** propiedad.</span><span class="sxs-lookup"><span data-stu-id="70b0f-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="70b0f-216">Propiedad</span><span class="sxs-lookup"><span data-stu-id="70b0f-216">Property</span></span> | <span data-ttu-id="70b0f-217">Descripción</span><span class="sxs-lookup"><span data-stu-id="70b0f-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="70b0f-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="70b0f-218">workspaceResourceId</span></span> |<span data-ttu-id="70b0f-219">Id. del área de trabajo de análisis de registros de hello en forma de hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nombre de área de trabajo\>*.</span><span class="sxs-lookup"><span data-stu-id="70b0f-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="70b0f-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="70b0f-220">referencedResources</span></span> |<span data-ttu-id="70b0f-221">Lista de recursos de solución de Hola que no se quitan cuando se quita la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="70b0f-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="70b0f-222">containedResources</span></span> |<span data-ttu-id="70b0f-223">Lista de recursos de solución de Hola que se deben eliminar cuando se quita la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="70b0f-224">ejemplo de Hola anterior es para una solución con un runbook, una programación y la vista.</span><span class="sxs-lookup"><span data-stu-id="70b0f-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="70b0f-225">programación de Hola y runbook son *que se hace referencia* en hello **propiedades** elemento por lo que no se quitan cuando se quita la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="70b0f-226">vista de Hello es *contenidos* por lo que se quita cuando se quita la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="70b0f-227">Plan</span><span class="sxs-lookup"><span data-stu-id="70b0f-227">Plan</span></span>
<span data-ttu-id="70b0f-228">Hola **plan** entidad de recursos de solución de hello tiene propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="70b0f-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="70b0f-229">Propiedad</span><span class="sxs-lookup"><span data-stu-id="70b0f-229">Property</span></span> | <span data-ttu-id="70b0f-230">Description</span><span class="sxs-lookup"><span data-stu-id="70b0f-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="70b0f-231">name</span><span class="sxs-lookup"><span data-stu-id="70b0f-231">name</span></span> |<span data-ttu-id="70b0f-232">Nombre de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-232">Name of hello solution.</span></span> |
| <span data-ttu-id="70b0f-233">versión</span><span class="sxs-lookup"><span data-stu-id="70b0f-233">version</span></span> |<span data-ttu-id="70b0f-234">Versión de solución de hello según lo determinado por el autor de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="70b0f-235">product</span><span class="sxs-lookup"><span data-stu-id="70b0f-235">product</span></span> |<span data-ttu-id="70b0f-236">Solución de hello tooidentify de cadena única.</span><span class="sxs-lookup"><span data-stu-id="70b0f-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="70b0f-237">publisher</span><span class="sxs-lookup"><span data-stu-id="70b0f-237">publisher</span></span> |<span data-ttu-id="70b0f-238">Publicador de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="70b0f-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="70b0f-239">Muestra</span><span class="sxs-lookup"><span data-stu-id="70b0f-239">Sample</span></span>
<span data-ttu-id="70b0f-240">Puede ver ejemplos de archivos de solución con un recurso de la solución en hello ubicaciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="70b0f-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="70b0f-241">Recursos de Automation</span><span class="sxs-lookup"><span data-stu-id="70b0f-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="70b0f-242">Recursos de búsqueda y alerta</span><span class="sxs-lookup"><span data-stu-id="70b0f-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="70b0f-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="70b0f-243">Next steps</span></span>
* <span data-ttu-id="70b0f-244">[Agregar las búsquedas guardadas y alertas](operations-management-suite-solutions-resources-searches-alerts.md) tooyour solución de administración.</span><span class="sxs-lookup"><span data-stu-id="70b0f-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="70b0f-245">[Agregar vistas](operations-management-suite-solutions-resources-views.md) tooyour solución de administración.</span><span class="sxs-lookup"><span data-stu-id="70b0f-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="70b0f-246">[Agregar runbooks y otros recursos de automatización](operations-management-suite-solutions-resources-automation.md) tooyour solución de administración.</span><span class="sxs-lookup"><span data-stu-id="70b0f-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="70b0f-247">Obtenga información acerca de los detalles de Hola de [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="70b0f-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="70b0f-248">Búsqueda de [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates) para obtener ejemplos de diferentes plantillas de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="70b0f-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
