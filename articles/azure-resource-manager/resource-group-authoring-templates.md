---
title: Estructura y sintaxis de las plantillas de Azure Resource Manager | Microsoft Docs
description: Describe la estructura y las propiedades de plantillas de Azure Resource Manager mediante la sintaxis declarativa de JSON.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="057c7-103">Nociones sobre la estructura y la sintaxis de las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="057c7-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="057c7-104">En este tema se describe la estructura de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="057c7-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="057c7-105">Presenta las distintas secciones de una plantilla y las propiedades que están disponibles en esas secciones.</span><span class="sxs-lookup"><span data-stu-id="057c7-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="057c7-106">La plantilla consta de JSON y expresiones que puede usar para generar valores para su implementación.</span><span class="sxs-lookup"><span data-stu-id="057c7-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="057c7-107">Para obtener instrucciones detalladas sobre cómo crear una plantilla, consulte [Creación de la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="057c7-108">Formato de plantilla</span><span class="sxs-lookup"><span data-stu-id="057c7-108">Template format</span></span>
<span data-ttu-id="057c7-109">En la estructura más simple, una plantilla contiene los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="057c7-109">In its simplest structure, a template contains the following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="057c7-110">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="057c7-110">Element name</span></span> | <span data-ttu-id="057c7-111">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="057c7-111">Required</span></span> | <span data-ttu-id="057c7-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="057c7-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="057c7-113">$schema</span><span class="sxs-lookup"><span data-stu-id="057c7-113">$schema</span></span> |<span data-ttu-id="057c7-114">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-114">Yes</span></span> |<span data-ttu-id="057c7-115">Ubicación del archivo de esquema JSON que describe la versión del idioma de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="057c7-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="057c7-116">Use la dirección URL que se muestra en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="057c7-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="057c7-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="057c7-117">contentVersion</span></span> |<span data-ttu-id="057c7-118">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-118">Yes</span></span> |<span data-ttu-id="057c7-119">Versión de la plantilla (por ejemplo, 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="057c7-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="057c7-120">Puede especificar cualquier valor para este elemento.</span><span class="sxs-lookup"><span data-stu-id="057c7-120">You can provide any value for this element.</span></span> <span data-ttu-id="057c7-121">Al implementar los recursos con la plantilla, este valor se puede usar para asegurarse de que se está usando la plantilla correcta.</span><span class="sxs-lookup"><span data-stu-id="057c7-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="057c7-122">parameters</span><span class="sxs-lookup"><span data-stu-id="057c7-122">parameters</span></span> |<span data-ttu-id="057c7-123">No</span><span class="sxs-lookup"><span data-stu-id="057c7-123">No</span></span> |<span data-ttu-id="057c7-124">Valores que se proporcionan cuando se ejecuta la implementación para personalizar la implementación de recursos.</span><span class="sxs-lookup"><span data-stu-id="057c7-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="057c7-125">variables</span><span class="sxs-lookup"><span data-stu-id="057c7-125">variables</span></span> |<span data-ttu-id="057c7-126">No</span><span class="sxs-lookup"><span data-stu-id="057c7-126">No</span></span> |<span data-ttu-id="057c7-127">Valores que se usan como fragmentos JSON en la plantilla para simplificar expresiones de idioma de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="057c7-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="057c7-128">resources</span><span class="sxs-lookup"><span data-stu-id="057c7-128">resources</span></span> |<span data-ttu-id="057c7-129">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-129">Yes</span></span> |<span data-ttu-id="057c7-130">Tipos de servicios que se implementan o actualizan en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="057c7-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="057c7-131">outputs</span><span class="sxs-lookup"><span data-stu-id="057c7-131">outputs</span></span> |<span data-ttu-id="057c7-132">No</span><span class="sxs-lookup"><span data-stu-id="057c7-132">No</span></span> |<span data-ttu-id="057c7-133">Valores que se devuelven después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="057c7-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="057c7-134">Cada elemento contiene propiedades que pueden incluirse.</span><span class="sxs-lookup"><span data-stu-id="057c7-134">Each element contains properties you can set.</span></span> <span data-ttu-id="057c7-135">En el ejemplo siguiente, se muestra la sintaxis completa de una plantilla:</span><span class="sxs-lookup"><span data-stu-id="057c7-135">The following example contains the full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-the parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="057c7-136">Examinaremos las secciones de la plantilla con mayor detenimiento más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="057c7-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="057c7-137">Expresiones y funciones</span><span class="sxs-lookup"><span data-stu-id="057c7-137">Expressions and functions</span></span>
<span data-ttu-id="057c7-138">La sintaxis básica de la plantilla es JSON.</span><span class="sxs-lookup"><span data-stu-id="057c7-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="057c7-139">Sin embargo, las expresiones y funciones amplían los valores JSON disponibles en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="057c7-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="057c7-140">Las expresiones se escriben en los literales de cadena JSON cuyo primer y último caracteres son los corchetes `[` y `]`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="057c7-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="057c7-141">El valor de la expresión se evalúa cuando se implementa la plantilla.</span><span class="sxs-lookup"><span data-stu-id="057c7-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="057c7-142">Mientras se escribe como un literal de cadena, el resultado de evaluar la expresión puede ser de un tipo diferente de JSON, como una matriz o un entero, dependiendo de la expresión real.</span><span class="sxs-lookup"><span data-stu-id="057c7-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="057c7-143">Para que una cadena literal empiece con un corchete `[`, pero no se interprete como una expresión, agregue otro corchete para que la cadena comience con `[[`.</span><span class="sxs-lookup"><span data-stu-id="057c7-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="057c7-144">Normalmente, se usan expresiones con funciones para realizar operaciones con el fin de configurar la implementación.</span><span class="sxs-lookup"><span data-stu-id="057c7-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="057c7-145">Al igual que en JavaScript, las llamadas de función tienen el formato `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="057c7-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="057c7-146">Se hace referencia a las propiedades mediante los operadores dot e [index] .</span><span class="sxs-lookup"><span data-stu-id="057c7-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="057c7-147">En el ejemplo siguiente se muestra cómo utilizar algunas de las funciones para la construcción de valores:</span><span class="sxs-lookup"><span data-stu-id="057c7-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="057c7-148">Para obtener la lista completa de las funciones de plantilla, consulte [Funciones de la plantilla del Administrador de recursos de Azure](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="057c7-149">parameters</span><span class="sxs-lookup"><span data-stu-id="057c7-149">Parameters</span></span>
<span data-ttu-id="057c7-150">En la sección de parámetros de la plantilla, especifique los valores que el usuario puede introducir al implementar los recursos.</span><span class="sxs-lookup"><span data-stu-id="057c7-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="057c7-151">Estos valores de parámetros permiten personalizar la implementación al proporcionar valores que son específicos para un entorno concreto (por ejemplo, desarrollo, prueba y producción).</span><span class="sxs-lookup"><span data-stu-id="057c7-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="057c7-152">No tiene que especificar parámetros en la plantilla, pero sin parámetros la plantilla implementaría siempre los mismos recursos con los mismos nombres, ubicaciones y propiedades.</span><span class="sxs-lookup"><span data-stu-id="057c7-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="057c7-153">Defina recursos con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="057c7-153">You define parameters with the following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="057c7-154">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="057c7-154">Element name</span></span> | <span data-ttu-id="057c7-155">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="057c7-155">Required</span></span> | <span data-ttu-id="057c7-156">Description</span><span class="sxs-lookup"><span data-stu-id="057c7-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="057c7-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="057c7-157">parameterName</span></span> |<span data-ttu-id="057c7-158">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-158">Yes</span></span> |<span data-ttu-id="057c7-159">Nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="057c7-159">Name of the parameter.</span></span> <span data-ttu-id="057c7-160">Debe ser un identificador válido de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="057c7-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="057c7-161">type</span><span class="sxs-lookup"><span data-stu-id="057c7-161">type</span></span> |<span data-ttu-id="057c7-162">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-162">Yes</span></span> |<span data-ttu-id="057c7-163">Tipo del valor del parámetro.</span><span class="sxs-lookup"><span data-stu-id="057c7-163">Type of the parameter value.</span></span> <span data-ttu-id="057c7-164">Consulte la lista de tipos permitidos después de esta tabla.</span><span class="sxs-lookup"><span data-stu-id="057c7-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="057c7-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="057c7-165">defaultValue</span></span> |<span data-ttu-id="057c7-166">No</span><span class="sxs-lookup"><span data-stu-id="057c7-166">No</span></span> |<span data-ttu-id="057c7-167">Valor predeterminado del parámetro, si no se proporciona ningún valor.</span><span class="sxs-lookup"><span data-stu-id="057c7-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="057c7-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="057c7-168">allowedValues</span></span> |<span data-ttu-id="057c7-169">No</span><span class="sxs-lookup"><span data-stu-id="057c7-169">No</span></span> |<span data-ttu-id="057c7-170">Matriz de valores permitidos para el parámetro para asegurarse de que se proporciona el valor correcto.</span><span class="sxs-lookup"><span data-stu-id="057c7-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="057c7-171">minValue</span><span class="sxs-lookup"><span data-stu-id="057c7-171">minValue</span></span> |<span data-ttu-id="057c7-172">No</span><span class="sxs-lookup"><span data-stu-id="057c7-172">No</span></span> |<span data-ttu-id="057c7-173">El valor mínimo de parámetros de tipo int, este valor es inclusivo.</span><span class="sxs-lookup"><span data-stu-id="057c7-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="057c7-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="057c7-174">maxValue</span></span> |<span data-ttu-id="057c7-175">No</span><span class="sxs-lookup"><span data-stu-id="057c7-175">No</span></span> |<span data-ttu-id="057c7-176">El valor máximo de parámetros de tipo int, este valor es inclusivo.</span><span class="sxs-lookup"><span data-stu-id="057c7-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="057c7-177">minLength</span><span class="sxs-lookup"><span data-stu-id="057c7-177">minLength</span></span> |<span data-ttu-id="057c7-178">No</span><span class="sxs-lookup"><span data-stu-id="057c7-178">No</span></span> |<span data-ttu-id="057c7-179">La longitud mínima de los parámetros de tipo cadena, secureString y matriz, este valor es inclusivo.</span><span class="sxs-lookup"><span data-stu-id="057c7-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="057c7-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="057c7-180">maxLength</span></span> |<span data-ttu-id="057c7-181">No</span><span class="sxs-lookup"><span data-stu-id="057c7-181">No</span></span> |<span data-ttu-id="057c7-182">La longitud máxima de los parámetros de tipo cadena, secureString y matriz, este valor es inclusivo.</span><span class="sxs-lookup"><span data-stu-id="057c7-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="057c7-183">Description</span><span class="sxs-lookup"><span data-stu-id="057c7-183">description</span></span> |<span data-ttu-id="057c7-184">No</span><span class="sxs-lookup"><span data-stu-id="057c7-184">No</span></span> |<span data-ttu-id="057c7-185">Descripción del parámetro que se muestra a los usuarios a través del portal.</span><span class="sxs-lookup"><span data-stu-id="057c7-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="057c7-186">Los valores y tipos permitidos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="057c7-186">The allowed types and values are:</span></span>

* <span data-ttu-id="057c7-187">**cadena**</span><span class="sxs-lookup"><span data-stu-id="057c7-187">**string**</span></span>
* <span data-ttu-id="057c7-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="057c7-188">**secureString**</span></span>
* <span data-ttu-id="057c7-189">**int**</span><span class="sxs-lookup"><span data-stu-id="057c7-189">**int**</span></span>
* <span data-ttu-id="057c7-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="057c7-190">**bool**</span></span>
* <span data-ttu-id="057c7-191">**objeto**</span><span class="sxs-lookup"><span data-stu-id="057c7-191">**object**</span></span> 
* <span data-ttu-id="057c7-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="057c7-192">**secureObject**</span></span>
* <span data-ttu-id="057c7-193">**matriz**</span><span class="sxs-lookup"><span data-stu-id="057c7-193">**array**</span></span>

<span data-ttu-id="057c7-194">Para especificar un parámetro como opcional, proporcione un defaultValue (puede ser una cadena vacía).</span><span class="sxs-lookup"><span data-stu-id="057c7-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="057c7-195">Si especifica un nombre de parámetro en la plantilla que coincide con un parámetro en el comando para implementar la plantilla, hay una posible ambigüedad sobre los valores proporcionados.</span><span class="sxs-lookup"><span data-stu-id="057c7-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="057c7-196">Para resolver esta confusión, Resource Manager agrega el postfijo **FromTemplate** al parámetro de plantilla.</span><span class="sxs-lookup"><span data-stu-id="057c7-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="057c7-197">Por ejemplo, si incluye un parámetro llamado **ResourceGroupName** en la plantilla, entra en conflicto con el parámetro **ResourceGroupName** del cmdlet [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="057c7-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="057c7-198">Durante la implementación, se le pide que proporcione un valor para **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="057c7-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="057c7-199">Por lo general, debe evitar esta confusión no nombrando los parámetros con el mismo nombre que los parámetros utilizados para operaciones de implementación.</span><span class="sxs-lookup"><span data-stu-id="057c7-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="057c7-200">Todas las contraseñas, claves y otros secretos deben utilizar el tipo **secureString** .</span><span class="sxs-lookup"><span data-stu-id="057c7-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="057c7-201">Si pasa datos confidenciales en un objeto JSON, use el tipo **secureObject**.</span><span class="sxs-lookup"><span data-stu-id="057c7-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="057c7-202">No se pueden leer los parámetros con los tipos secureString o secureObject después de la implementación de recursos.</span><span class="sxs-lookup"><span data-stu-id="057c7-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="057c7-203">Por ejemplo, la siguiente entrada del historial de implementación muestra el valor de una cadena y un objeto, pero no de secureString y secureObject.</span><span class="sxs-lookup"><span data-stu-id="057c7-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![Visualización de los valores de implementación](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="057c7-205">En el ejemplo siguiente se muestra cómo definir los parámetros.</span><span class="sxs-lookup"><span data-stu-id="057c7-205">The following example shows how to define parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="057c7-206">Para más información acerca de cómo especificar los valores de los parámetros durante la implementación, consulte [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)(Implementación de aplicaciones con la plantilla de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="057c7-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="057c7-207">variables</span><span class="sxs-lookup"><span data-stu-id="057c7-207">Variables</span></span>
<span data-ttu-id="057c7-208">En la sección de variables, se crean valores que pueden usarse en toda la plantilla.</span><span class="sxs-lookup"><span data-stu-id="057c7-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="057c7-209">No es necesario definir las variables, pero a menudo simplifican la plantilla reduciendo expresiones complejas.</span><span class="sxs-lookup"><span data-stu-id="057c7-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="057c7-210">Defina variables con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="057c7-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="057c7-211">En el ejemplo siguiente se muestra cómo definir una variable que se construye a partir de dos valores de parámetro:</span><span class="sxs-lookup"><span data-stu-id="057c7-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="057c7-212">En el ejemplo siguiente se muestra una variable que es un tipo JSON complejo y las variables que se construyen a partir de otras variables:</span><span class="sxs-lookup"><span data-stu-id="057c7-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="057c7-213">resources</span><span class="sxs-lookup"><span data-stu-id="057c7-213">Resources</span></span>
<span data-ttu-id="057c7-214">En la sección de recursos, se define que los recursos se implementan o se actualizan.</span><span class="sxs-lookup"><span data-stu-id="057c7-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="057c7-215">Esta sección se puede complicar porque debe comprender los tipos que va a implementar para proporcionar los valores adecuados.</span><span class="sxs-lookup"><span data-stu-id="057c7-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="057c7-216">Para obtener información sobre los valores específicos de los recursos (apiVersion, type y properties) que se deben establecer, consulte [Define resources in Azure Resource Manager templates](/azure/templates/) (Definición de recursos en las plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="057c7-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="057c7-217">Defina recursos con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="057c7-217">You define resources with the following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="057c7-218">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="057c7-218">Element name</span></span> | <span data-ttu-id="057c7-219">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="057c7-219">Required</span></span> | <span data-ttu-id="057c7-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="057c7-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="057c7-221">condition</span><span class="sxs-lookup"><span data-stu-id="057c7-221">condition</span></span> | <span data-ttu-id="057c7-222">No</span><span class="sxs-lookup"><span data-stu-id="057c7-222">No</span></span> | <span data-ttu-id="057c7-223">Valor booleano que indica si el recurso se implementa.</span><span class="sxs-lookup"><span data-stu-id="057c7-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="057c7-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="057c7-224">apiVersion</span></span> |<span data-ttu-id="057c7-225">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-225">Yes</span></span> |<span data-ttu-id="057c7-226">Versión de la API de REST que debe usar para crear el recurso.</span><span class="sxs-lookup"><span data-stu-id="057c7-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="057c7-227">type</span><span class="sxs-lookup"><span data-stu-id="057c7-227">type</span></span> |<span data-ttu-id="057c7-228">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-228">Yes</span></span> |<span data-ttu-id="057c7-229">Tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="057c7-229">Type of the resource.</span></span> <span data-ttu-id="057c7-230">Este valor es una combinación del espacio de nombres del proveedor de recursos y el tipo de recurso (como **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="057c7-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="057c7-231">name</span><span class="sxs-lookup"><span data-stu-id="057c7-231">name</span></span> |<span data-ttu-id="057c7-232">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-232">Yes</span></span> |<span data-ttu-id="057c7-233">Nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="057c7-233">Name of the resource.</span></span> <span data-ttu-id="057c7-234">El nombre debe cumplir las restricciones de componente URI definidas en RFC3986.</span><span class="sxs-lookup"><span data-stu-id="057c7-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="057c7-235">Además, los servicios de Azure que exponen el nombre del recurso a partes externas validan el nombre para asegurarse de que no es un intento de suplantar otra identidad.</span><span class="sxs-lookup"><span data-stu-id="057c7-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="057c7-236">location</span><span class="sxs-lookup"><span data-stu-id="057c7-236">location</span></span> |<span data-ttu-id="057c7-237">Varía</span><span class="sxs-lookup"><span data-stu-id="057c7-237">Varies</span></span> |<span data-ttu-id="057c7-238">Ubicaciones geográficas compatibles del recurso proporcionado.</span><span class="sxs-lookup"><span data-stu-id="057c7-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="057c7-239">Puede seleccionar cualquiera de las ubicaciones disponibles, pero normalmente tiene sentido elegir aquella que esté más cerca de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="057c7-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="057c7-240">Normalmente, también tiene sentido colocar los recursos que interactúan entre sí en la misma región.</span><span class="sxs-lookup"><span data-stu-id="057c7-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="057c7-241">La mayoría de los tipos de recursos requieren una ubicación, pero algunos (por ejemplo, una asignación de roles) no la necesitan.</span><span class="sxs-lookup"><span data-stu-id="057c7-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="057c7-242">Consulte [Establecimiento de la ubicación para recursos en plantillas de Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="057c7-243">etiquetas</span><span class="sxs-lookup"><span data-stu-id="057c7-243">tags</span></span> |<span data-ttu-id="057c7-244">No</span><span class="sxs-lookup"><span data-stu-id="057c7-244">No</span></span> |<span data-ttu-id="057c7-245">Etiquetas asociadas al recurso.</span><span class="sxs-lookup"><span data-stu-id="057c7-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="057c7-246">Consulte [Aplicación de etiquetas a recursos en plantillas de Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="057c7-247">comentarios</span><span class="sxs-lookup"><span data-stu-id="057c7-247">comments</span></span> |<span data-ttu-id="057c7-248">No</span><span class="sxs-lookup"><span data-stu-id="057c7-248">No</span></span> |<span data-ttu-id="057c7-249">Notas para documentar los recursos de la plantilla</span><span class="sxs-lookup"><span data-stu-id="057c7-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="057c7-250">copia</span><span class="sxs-lookup"><span data-stu-id="057c7-250">copy</span></span> |<span data-ttu-id="057c7-251">No</span><span class="sxs-lookup"><span data-stu-id="057c7-251">No</span></span> |<span data-ttu-id="057c7-252">Si se necesita más de una instancia, el número de recursos que se crearán.</span><span class="sxs-lookup"><span data-stu-id="057c7-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="057c7-253">El modo predeterminado es paralelo.</span><span class="sxs-lookup"><span data-stu-id="057c7-253">The default mode is parallel.</span></span> <span data-ttu-id="057c7-254">Si no desea que todos los recursos se implementen al mismo tiempo, especifique el modo serie.</span><span class="sxs-lookup"><span data-stu-id="057c7-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="057c7-255">Para más información, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="057c7-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="057c7-256">dependsOn</span></span> |<span data-ttu-id="057c7-257">No</span><span class="sxs-lookup"><span data-stu-id="057c7-257">No</span></span> |<span data-ttu-id="057c7-258">Recursos que se deben implementar antes de implementar este.</span><span class="sxs-lookup"><span data-stu-id="057c7-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="057c7-259">Resource Manager evalúa las dependencias entre recursos y los implementa en su orden correcto.</span><span class="sxs-lookup"><span data-stu-id="057c7-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="057c7-260">Cuando no hay recursos dependientes entre sí, se implementan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="057c7-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="057c7-261">El valor puede ser una lista separada por comas de nombres de recursos o identificadores de recursos únicos.</span><span class="sxs-lookup"><span data-stu-id="057c7-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="057c7-262">Solo los recursos de lista que se implementan en esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="057c7-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="057c7-263">Deben existir los recursos que no estén definidos en esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="057c7-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="057c7-264">Evite agregar dependencias innecesarias, ya que pueden ralentizar la implementación y crear dependencias circulares.</span><span class="sxs-lookup"><span data-stu-id="057c7-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="057c7-265">Para obtener instrucciones sobre la configuración de dependencias, consulte [Definición de dependencias en plantillas de Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="057c7-266">propiedades</span><span class="sxs-lookup"><span data-stu-id="057c7-266">properties</span></span> |<span data-ttu-id="057c7-267">No</span><span class="sxs-lookup"><span data-stu-id="057c7-267">No</span></span> |<span data-ttu-id="057c7-268">Opciones de configuración específicas de recursos.</span><span class="sxs-lookup"><span data-stu-id="057c7-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="057c7-269">Los valores de las propiedades son exactamente los mismos valores que se especifican en el cuerpo de la solicitud de la operación de API de REST (método PUT) para crear el recurso.</span><span class="sxs-lookup"><span data-stu-id="057c7-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="057c7-270">También puede especificar una matriz de copia para crear varias instancias de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="057c7-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="057c7-271">Para más información, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="057c7-272">resources</span><span class="sxs-lookup"><span data-stu-id="057c7-272">resources</span></span> |<span data-ttu-id="057c7-273">No</span><span class="sxs-lookup"><span data-stu-id="057c7-273">No</span></span> |<span data-ttu-id="057c7-274">Recursos secundarios que dependen del recurso que se está definiendo.</span><span class="sxs-lookup"><span data-stu-id="057c7-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="057c7-275">Proporcione solo tipos de recursos que permita el esquema del recurso principal.</span><span class="sxs-lookup"><span data-stu-id="057c7-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="057c7-276">El tipo completo del recurso secundario incluye el tipo del recurso principal, por ejemplo, **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="057c7-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="057c7-277">La dependencia del recurso principal no está implícita.</span><span class="sxs-lookup"><span data-stu-id="057c7-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="057c7-278">Debe definirla explícitamente.</span><span class="sxs-lookup"><span data-stu-id="057c7-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="057c7-279">La sección de recursos contiene una matriz de los recursos para implementar.</span><span class="sxs-lookup"><span data-stu-id="057c7-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="057c7-280">En cada recurso, puede definir también una matriz de recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="057c7-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="057c7-281">Por lo tanto, la sección de recursos podría tener una estructura como:</span><span class="sxs-lookup"><span data-stu-id="057c7-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="057c7-282">Para obtener más información sobre la definición de recursos secundarios, consulte [Establecimiento del nombre y el tipo de recurso secundario en la plantilla de Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="057c7-283">El elemento **condition** especifica si el recurso se ha implementado.</span><span class="sxs-lookup"><span data-stu-id="057c7-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="057c7-284">El valor de este elemento se resuelve como true o false.</span><span class="sxs-lookup"><span data-stu-id="057c7-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="057c7-285">Por ejemplo, para especificar si se implementa una nueva cuenta de almacenamiento, use:</span><span class="sxs-lookup"><span data-stu-id="057c7-285">For example, to specify whether a new storage account is deployed, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="057c7-286">Para ver un ejemplo de uso de un recurso nuevo o existente, consulte la [plantilla de condición nueva o existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="057c7-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="057c7-287">Para especificar si una máquina virtual se implementa con una contraseña o una clave SSH, defina dos versiones de la máquina virtual en la plantilla y use **condition** para diferenciar el uso.</span><span class="sxs-lookup"><span data-stu-id="057c7-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="057c7-288">Pase un parámetro que especifica qué escenario se implementará.</span><span class="sxs-lookup"><span data-stu-id="057c7-288">Pass a parameter that specifies which scenario to deploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="057c7-289">Para ver un ejemplo de uso de una contraseña o una clave SSH para implementar la máquina virtual, consulte la [plantilla de condición de nombre de usuario o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="057c7-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="057c7-290">Salidas</span><span class="sxs-lookup"><span data-stu-id="057c7-290">Outputs</span></span>
<span data-ttu-id="057c7-291">En la sección de salidas, especifique valores que se devuelven de la implementación.</span><span class="sxs-lookup"><span data-stu-id="057c7-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="057c7-292">Por ejemplo, podría devolver el URI para acceder a un recurso implementado.</span><span class="sxs-lookup"><span data-stu-id="057c7-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="057c7-293">En el ejemplo siguiente se muestra la estructura de una definición de salida:</span><span class="sxs-lookup"><span data-stu-id="057c7-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="057c7-294">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="057c7-294">Element name</span></span> | <span data-ttu-id="057c7-295">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="057c7-295">Required</span></span> | <span data-ttu-id="057c7-296">Descripción</span><span class="sxs-lookup"><span data-stu-id="057c7-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="057c7-297">outputName</span><span class="sxs-lookup"><span data-stu-id="057c7-297">outputName</span></span> |<span data-ttu-id="057c7-298">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-298">Yes</span></span> |<span data-ttu-id="057c7-299">Nombre del valor de salida.</span><span class="sxs-lookup"><span data-stu-id="057c7-299">Name of the output value.</span></span> <span data-ttu-id="057c7-300">Debe ser un identificador válido de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="057c7-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="057c7-301">type</span><span class="sxs-lookup"><span data-stu-id="057c7-301">type</span></span> |<span data-ttu-id="057c7-302">Sí</span><span class="sxs-lookup"><span data-stu-id="057c7-302">Yes</span></span> |<span data-ttu-id="057c7-303">Tipo del valor de salida.</span><span class="sxs-lookup"><span data-stu-id="057c7-303">Type of the output value.</span></span> <span data-ttu-id="057c7-304">Los valores de salida admiten los mismos tipos que los parámetros de entrada de plantilla.</span><span class="sxs-lookup"><span data-stu-id="057c7-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="057c7-305">value</span><span class="sxs-lookup"><span data-stu-id="057c7-305">value</span></span> |<span data-ttu-id="057c7-306">yes</span><span class="sxs-lookup"><span data-stu-id="057c7-306">Yes</span></span> |<span data-ttu-id="057c7-307">Expresión de lenguaje de plantilla que se evaluará y devolverá como valor de salida.</span><span class="sxs-lookup"><span data-stu-id="057c7-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="057c7-308">En el ejemplo siguiente se muestra un valor que se devuelve en la sección de salidas.</span><span class="sxs-lookup"><span data-stu-id="057c7-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="057c7-309">Para más información sobre cómo trabajar con resultados, consulte [Uso compartido del estado con las plantillas de Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="057c7-310">Límites de plantilla</span><span class="sxs-lookup"><span data-stu-id="057c7-310">Template limits</span></span>

<span data-ttu-id="057c7-311">Limite el tamaño de la plantilla a 1 MB y cada archivo de parámetros a 64 KB.</span><span class="sxs-lookup"><span data-stu-id="057c7-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="057c7-312">El límite de 1 MB se aplica al estado final de la plantilla una vez se ha ampliado con definiciones de recursos iterativas y los valores de variables y parámetros.</span><span class="sxs-lookup"><span data-stu-id="057c7-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="057c7-313">También está limitado a:</span><span class="sxs-lookup"><span data-stu-id="057c7-313">You are also limited to:</span></span>

* <span data-ttu-id="057c7-314">256 parámetros</span><span class="sxs-lookup"><span data-stu-id="057c7-314">256 parameters</span></span>
* <span data-ttu-id="057c7-315">256 variables</span><span class="sxs-lookup"><span data-stu-id="057c7-315">256 variables</span></span>
* <span data-ttu-id="057c7-316">800 recursos (incluido el recuento de copia)</span><span class="sxs-lookup"><span data-stu-id="057c7-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="057c7-317">64 valores de salida</span><span class="sxs-lookup"><span data-stu-id="057c7-317">64 output values</span></span>
* <span data-ttu-id="057c7-318">24 576 caracteres en una expresión de plantilla</span><span class="sxs-lookup"><span data-stu-id="057c7-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="057c7-319">Puede superar algunos límites de plantilla utilizando una plantilla anidada.</span><span class="sxs-lookup"><span data-stu-id="057c7-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="057c7-320">Para más información, consulte [Uso de plantillas vinculadas en la implementación de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="057c7-321">Para reducir el número de parámetros, variables o salidas, puede combinar varios valores en un objeto.</span><span class="sxs-lookup"><span data-stu-id="057c7-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="057c7-322">Para más información, consulte [Objetos como parámetros](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="057c7-323">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="057c7-323">Next steps</span></span>
* <span data-ttu-id="057c7-324">Para ver plantillas completas de muchos tipos diferentes de soluciones, consulte [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="057c7-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="057c7-325">Para obtener información detallada sobre las funciones que se pueden usar dentro de una plantilla, consulte [Funciones de plantilla de Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="057c7-326">Para combinar varias plantillas en la implementación, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="057c7-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="057c7-327">Puede que necesite usar los recursos que existen dentro de un grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="057c7-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="057c7-328">Este escenario es habitual al trabajar con cuentas de almacenamiento o redes virtuales que se comparten entre varios grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="057c7-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="057c7-329">Para obtener más información, vea la [función resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="057c7-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
