---
title: el Administrador de recursos de aaaAzure estructura de plantilla y la sintaxis | Documentos de Microsoft
description: Describe la estructura de Hola y las propiedades de plantillas de Azure Resource Manager mediante la sintaxis declarativa de JSON.
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
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="90989-103">Comprender la estructura de Hola y la sintaxis de plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="90989-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="90989-104">Este tema describe la estructura de Hola de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="90989-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="90989-105">Muestra las diferentes secciones de Hola de propiedades de plantilla y Hola que están disponibles en dichas secciones.</span><span class="sxs-lookup"><span data-stu-id="90989-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="90989-106">plantilla de Hello consta de JSON y expresiones que puede utilizar valores de tooconstruct para su implementación.</span><span class="sxs-lookup"><span data-stu-id="90989-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="90989-107">Para obtener instrucciones detalladas sobre cómo crear una plantilla, consulte [Creación de la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="90989-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="90989-108">Formato de plantilla</span><span class="sxs-lookup"><span data-stu-id="90989-108">Template format</span></span>
<span data-ttu-id="90989-109">En la estructura más sencilla, una plantilla contiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="90989-109">In its simplest structure, a template contains hello following elements:</span></span>

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

| <span data-ttu-id="90989-110">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="90989-110">Element name</span></span> | <span data-ttu-id="90989-111">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="90989-111">Required</span></span> | <span data-ttu-id="90989-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="90989-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="90989-113">$schema</span><span class="sxs-lookup"><span data-stu-id="90989-113">$schema</span></span> |<span data-ttu-id="90989-114">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-114">Yes</span></span> |<span data-ttu-id="90989-115">Ubicación del archivo de esquema JSON de Hola que describe la versión de Hola de idioma de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="90989-116">Dirección URL de Hola de uso que se muestra en el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="90989-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="90989-117">contentVersion</span></span> |<span data-ttu-id="90989-118">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-118">Yes</span></span> |<span data-ttu-id="90989-119">Versión de plantilla de hello (por ejemplo, 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="90989-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="90989-120">Puede especificar cualquier valor para este elemento.</span><span class="sxs-lookup"><span data-stu-id="90989-120">You can provide any value for this element.</span></span> <span data-ttu-id="90989-121">Al implementar los recursos mediante la plantilla de hello, este valor puede ser usado toomake que dicha plantilla derecho Hola esté en uso.</span><span class="sxs-lookup"><span data-stu-id="90989-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="90989-122">parameters</span><span class="sxs-lookup"><span data-stu-id="90989-122">parameters</span></span> |<span data-ttu-id="90989-123">No</span><span class="sxs-lookup"><span data-stu-id="90989-123">No</span></span> |<span data-ttu-id="90989-124">Valores que se proporcionan cuando la implementación es ejecutan toocustomize implementación de los recursos.</span><span class="sxs-lookup"><span data-stu-id="90989-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="90989-125">variables</span><span class="sxs-lookup"><span data-stu-id="90989-125">variables</span></span> |<span data-ttu-id="90989-126">No</span><span class="sxs-lookup"><span data-stu-id="90989-126">No</span></span> |<span data-ttu-id="90989-127">Valores que se usan como fragmentos JSON en expresiones de idioma de plantilla de hello plantilla toosimplify.</span><span class="sxs-lookup"><span data-stu-id="90989-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="90989-128">resources</span><span class="sxs-lookup"><span data-stu-id="90989-128">resources</span></span> |<span data-ttu-id="90989-129">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-129">Yes</span></span> |<span data-ttu-id="90989-130">Tipos de servicios que se implementan o actualizan en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="90989-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="90989-131">outputs</span><span class="sxs-lookup"><span data-stu-id="90989-131">outputs</span></span> |<span data-ttu-id="90989-132">No</span><span class="sxs-lookup"><span data-stu-id="90989-132">No</span></span> |<span data-ttu-id="90989-133">Valores que se devuelven después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="90989-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="90989-134">Cada elemento contiene propiedades que pueden incluirse.</span><span class="sxs-lookup"><span data-stu-id="90989-134">Each element contains properties you can set.</span></span> <span data-ttu-id="90989-135">Hola siguiente ejemplo contiene sintaxis completa de Hola para una plantilla:</span><span class="sxs-lookup"><span data-stu-id="90989-135">hello following example contains hello full syntax for a template:</span></span>

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
                "description": "<description-of-hello parameter>" 
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

<span data-ttu-id="90989-136">Se examinan las secciones de Hola de plantilla de hello en mayor detalle más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="90989-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="90989-137">Expresiones y funciones</span><span class="sxs-lookup"><span data-stu-id="90989-137">Expressions and functions</span></span>
<span data-ttu-id="90989-138">sintaxis básica de Hola de plantilla de hello es JSON.</span><span class="sxs-lookup"><span data-stu-id="90989-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="90989-139">Sin embargo, las expresiones y funciones extienden los valores JSON de hello disponibles dentro de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="90989-140">Las expresiones se escriben a los literales de cadena JSON cuyo primer y últimos caracteres son corchetes hello: `[` y `]`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="90989-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="90989-141">valor de Hola de expresión de Hola se evalúa cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="90989-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="90989-142">Mientras se escribe como un literal de cadena, el resultado de hello de la evaluación de expresión de hello puede ser de un tipo diferente de JSON, como una matriz o un entero, dependiendo de la expresión real Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="90989-143">toohave iniciar una cadena literal con un corchete de cierre `[`, pero no hacer que se interpreta como una expresión, agregue una cadena de hello toostart corchete adicional con `[[`.</span><span class="sxs-lookup"><span data-stu-id="90989-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="90989-144">Por lo general, se usan expresiones con operaciones de tooperform de funciones para la configuración de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="90989-145">Al igual que en JavaScript, las llamadas de función tienen el formato `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="90989-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="90989-146">Hacer referencia a propiedades mediante operadores de hello [índice] y de puntos.</span><span class="sxs-lookup"><span data-stu-id="90989-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="90989-147">Hola de ejemplo siguiente muestra cómo toouse varias funciones al construir valores:</span><span class="sxs-lookup"><span data-stu-id="90989-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="90989-148">Para hello lista completa de las funciones de plantilla, consulte [funciones de plantilla de Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="90989-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="90989-149">parameters</span><span class="sxs-lookup"><span data-stu-id="90989-149">Parameters</span></span>
<span data-ttu-id="90989-150">En la sección de parámetros de Hola de plantilla de hello, especifique los valores que puede introducir al implementar Hola recursos.</span><span class="sxs-lookup"><span data-stu-id="90989-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="90989-151">Estos valores de parámetro permiten la implementación de hello toocustomize proporcionando los valores que se han adaptado en un entorno determinado (por ejemplo, desarrollo, prueba y producción).</span><span class="sxs-lookup"><span data-stu-id="90989-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="90989-152">No tiene parámetros de tooprovide en la plantilla, pero sin parámetros de la plantilla implementa siempre Hola mismos recursos con Hola los mismos nombres, ubicaciones y propiedades.</span><span class="sxs-lookup"><span data-stu-id="90989-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="90989-153">Definir parámetros con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="90989-153">You define parameters with hello following structure:</span></span>

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
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="90989-154">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="90989-154">Element name</span></span> | <span data-ttu-id="90989-155">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="90989-155">Required</span></span> | <span data-ttu-id="90989-156">Description</span><span class="sxs-lookup"><span data-stu-id="90989-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="90989-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="90989-157">parameterName</span></span> |<span data-ttu-id="90989-158">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-158">Yes</span></span> |<span data-ttu-id="90989-159">Nombre del parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="90989-159">Name of hello parameter.</span></span> <span data-ttu-id="90989-160">Debe ser un identificador válido de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="90989-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="90989-161">type</span><span class="sxs-lookup"><span data-stu-id="90989-161">type</span></span> |<span data-ttu-id="90989-162">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-162">Yes</span></span> |<span data-ttu-id="90989-163">Tipo del valor de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-163">Type of hello parameter value.</span></span> <span data-ttu-id="90989-164">Ver lista de Hola de tipos permitidos después de esta tabla.</span><span class="sxs-lookup"><span data-stu-id="90989-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="90989-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="90989-165">defaultValue</span></span> |<span data-ttu-id="90989-166">No</span><span class="sxs-lookup"><span data-stu-id="90989-166">No</span></span> |<span data-ttu-id="90989-167">Valor predeterminado para el parámetro hello, si no se proporciona ningún valor para el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="90989-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="90989-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="90989-168">allowedValues</span></span> |<span data-ttu-id="90989-169">No</span><span class="sxs-lookup"><span data-stu-id="90989-169">No</span></span> |<span data-ttu-id="90989-170">Matriz de valores permitidos para hello parámetro toomake seguro de que se proporciona el valor correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="90989-171">minValue</span><span class="sxs-lookup"><span data-stu-id="90989-171">minValue</span></span> |<span data-ttu-id="90989-172">No</span><span class="sxs-lookup"><span data-stu-id="90989-172">No</span></span> |<span data-ttu-id="90989-173">valor mínimo de Hola para parámetros de tipo int, este valor es inclusivo.</span><span class="sxs-lookup"><span data-stu-id="90989-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="90989-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="90989-174">maxValue</span></span> |<span data-ttu-id="90989-175">No</span><span class="sxs-lookup"><span data-stu-id="90989-175">No</span></span> |<span data-ttu-id="90989-176">valor máximo de Hola para parámetros de tipo int, este valor es inclusivo.</span><span class="sxs-lookup"><span data-stu-id="90989-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="90989-177">minLength</span><span class="sxs-lookup"><span data-stu-id="90989-177">minLength</span></span> |<span data-ttu-id="90989-178">No</span><span class="sxs-lookup"><span data-stu-id="90989-178">No</span></span> |<span data-ttu-id="90989-179">longitud mínima de Hola para cadenas, secureString y parámetros de tipo de matriz, este valor es inclusivo.</span><span class="sxs-lookup"><span data-stu-id="90989-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="90989-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="90989-180">maxLength</span></span> |<span data-ttu-id="90989-181">No</span><span class="sxs-lookup"><span data-stu-id="90989-181">No</span></span> |<span data-ttu-id="90989-182">longitud máxima de Hola para cadenas, secureString y parámetros de tipo de matriz, este valor es inclusivo.</span><span class="sxs-lookup"><span data-stu-id="90989-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="90989-183">description</span><span class="sxs-lookup"><span data-stu-id="90989-183">description</span></span> |<span data-ttu-id="90989-184">No</span><span class="sxs-lookup"><span data-stu-id="90989-184">No</span></span> |<span data-ttu-id="90989-185">Descripción del parámetro hello muestra toousers a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="90989-186">Hello valores y los tipos permitidos son:</span><span class="sxs-lookup"><span data-stu-id="90989-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="90989-187">**cadena**</span><span class="sxs-lookup"><span data-stu-id="90989-187">**string**</span></span>
* <span data-ttu-id="90989-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="90989-188">**secureString**</span></span>
* <span data-ttu-id="90989-189">**int**</span><span class="sxs-lookup"><span data-stu-id="90989-189">**int**</span></span>
* <span data-ttu-id="90989-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="90989-190">**bool**</span></span>
* <span data-ttu-id="90989-191">**objeto**</span><span class="sxs-lookup"><span data-stu-id="90989-191">**object**</span></span> 
* <span data-ttu-id="90989-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="90989-192">**secureObject**</span></span>
* <span data-ttu-id="90989-193">**matriz**</span><span class="sxs-lookup"><span data-stu-id="90989-193">**array**</span></span>

<span data-ttu-id="90989-194">toospecify un parámetro como opcional, proporcionan un defaultValue (puede ser una cadena vacía).</span><span class="sxs-lookup"><span data-stu-id="90989-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="90989-195">Si especifica un nombre de parámetro en la plantilla que coincide con un parámetro de plantilla de hello comando toodeploy Hola, no hay ambigüedad acerca de los valores de hello que proporcione.</span><span class="sxs-lookup"><span data-stu-id="90989-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="90989-196">El Administrador de recursos resuelve esta confusión mediante la adición de postfijo hello **FromTemplate** toohello parámetro de plantilla.</span><span class="sxs-lookup"><span data-stu-id="90989-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="90989-197">Por ejemplo, si incluye un parámetro denominado **ResourceGroupName** en la plantilla, entra en conflicto con hello **ResourceGroupName** parámetro Hola [ Nueva AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="90989-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="90989-198">Durante la implementación, son tooprovide solicitada un valor para **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="90989-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="90989-199">En general, debe evitar esta confusión por no nombrar parámetros con el mismo nombre como parámetros que se utilizan para las operaciones de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="90989-200">Todas las contraseñas, claves y otros secretos deben usar hello **secureString** tipo.</span><span class="sxs-lookup"><span data-stu-id="90989-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="90989-201">Si pasa datos confidenciales en un objeto JSON, use hello **secureObject** tipo.</span><span class="sxs-lookup"><span data-stu-id="90989-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="90989-202">No se pueden leer los parámetros con los tipos secureString o secureObject después de la implementación de recursos.</span><span class="sxs-lookup"><span data-stu-id="90989-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="90989-203">Por ejemplo, hello siguiente entrada en el historial de implementación de hello muestra hello valor para una cadena y un objeto, pero no para secureString y secureObject.</span><span class="sxs-lookup"><span data-stu-id="90989-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![Visualización de los valores de implementación](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="90989-205">Hola siguiente ejemplo se muestra cómo toodefine parámetros:</span><span class="sxs-lookup"><span data-stu-id="90989-205">hello following example shows how toodefine parameters:</span></span>

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

<span data-ttu-id="90989-206">Para cómo valores de parámetro de hello tooinput durante la implementación, consulte [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="90989-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="90989-207">variables</span><span class="sxs-lookup"><span data-stu-id="90989-207">Variables</span></span>
<span data-ttu-id="90989-208">En la sección de variables de hello, crear valores que se pueden utilizar a lo largo de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="90989-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="90989-209">No es necesario toodefine variables, pero a menudo simplifican la plantilla reduciendo expresiones complejas.</span><span class="sxs-lookup"><span data-stu-id="90989-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="90989-210">Defina variables con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="90989-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="90989-211">Hola siguiente ejemplo se muestra cómo toodefine una variable que se construye a partir de dos valores de parámetro:</span><span class="sxs-lookup"><span data-stu-id="90989-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="90989-212">ejemplo de Hola siguiente muestra una variable que es un tipo complejo de JSON y las variables que se construyen a partir de otras variables:</span><span class="sxs-lookup"><span data-stu-id="90989-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

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

## <a name="resources"></a><span data-ttu-id="90989-213">Recursos</span><span class="sxs-lookup"><span data-stu-id="90989-213">Resources</span></span>
<span data-ttu-id="90989-214">En la sección de recursos de hello, definir recursos de Hola que se implementa o se actualizan.</span><span class="sxs-lookup"><span data-stu-id="90989-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="90989-215">En esta sección puede resultar complicada porque debe entender Hola tipos que se va a implementar valores correctos de tooprovide Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="90989-216">Para saludo específico del recurso valores (el elemento apiVersion, tipo y propiedades) que necesita tooset, vea [definir los recursos en las plantillas de Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="90989-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="90989-217">Definir recursos con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="90989-217">You define resources with hello following structure:</span></span>

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

| <span data-ttu-id="90989-218">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="90989-218">Element name</span></span> | <span data-ttu-id="90989-219">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="90989-219">Required</span></span> | <span data-ttu-id="90989-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="90989-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="90989-221">condition</span><span class="sxs-lookup"><span data-stu-id="90989-221">condition</span></span> | <span data-ttu-id="90989-222">No</span><span class="sxs-lookup"><span data-stu-id="90989-222">No</span></span> | <span data-ttu-id="90989-223">Valor booleano que indica si se implementa el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="90989-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="90989-224">apiVersion</span></span> |<span data-ttu-id="90989-225">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-225">Yes</span></span> |<span data-ttu-id="90989-226">Versión de hello toouse de API de REST para crear recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="90989-227">type</span><span class="sxs-lookup"><span data-stu-id="90989-227">type</span></span> |<span data-ttu-id="90989-228">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-228">Yes</span></span> |<span data-ttu-id="90989-229">Tipo de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-229">Type of hello resource.</span></span> <span data-ttu-id="90989-230">Este valor es una combinación de espacio de nombres de hello del proveedor de recursos de Hola y el tipo de recurso de hello (como **Microsoft.Storage/storageaccounts**).</span><span class="sxs-lookup"><span data-stu-id="90989-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="90989-231">name</span><span class="sxs-lookup"><span data-stu-id="90989-231">name</span></span> |<span data-ttu-id="90989-232">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-232">Yes</span></span> |<span data-ttu-id="90989-233">Nombre del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-233">Name of hello resource.</span></span> <span data-ttu-id="90989-234">nombre de Hello debe seguir las restricciones de componente URI definidas en RFC3986.</span><span class="sxs-lookup"><span data-stu-id="90989-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="90989-235">Además, los servicios de Azure que exponen las partes toooutside de nombre de recurso de hello validan hello toomake de nombre seguro no es un intento de toospoof otra identidad.</span><span class="sxs-lookup"><span data-stu-id="90989-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="90989-236">location</span><span class="sxs-lookup"><span data-stu-id="90989-236">location</span></span> |<span data-ttu-id="90989-237">Varía</span><span class="sxs-lookup"><span data-stu-id="90989-237">Varies</span></span> |<span data-ttu-id="90989-238">Ubicaciones geográficas admitidas de hello proporcionan recursos.</span><span class="sxs-lookup"><span data-stu-id="90989-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="90989-239">Puede seleccionar cualquiera de las ubicaciones disponibles hello, pero normalmente tiene sentido toopick uno que sea tooyour cierre a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="90989-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="90989-240">Normalmente, también conviene recursos tooplace que interactúan entre sí en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="90989-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="90989-241">La mayoría de los tipos de recursos requieren una ubicación, pero algunos (por ejemplo, una asignación de roles) no la necesitan.</span><span class="sxs-lookup"><span data-stu-id="90989-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="90989-242">Consulte [Establecimiento de la ubicación para recursos en plantillas de Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="90989-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="90989-243">etiquetas</span><span class="sxs-lookup"><span data-stu-id="90989-243">tags</span></span> |<span data-ttu-id="90989-244">No</span><span class="sxs-lookup"><span data-stu-id="90989-244">No</span></span> |<span data-ttu-id="90989-245">Etiquetas que están asociadas con el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="90989-246">Consulte [Aplicación de etiquetas a recursos en plantillas de Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="90989-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="90989-247">comentarios</span><span class="sxs-lookup"><span data-stu-id="90989-247">comments</span></span> |<span data-ttu-id="90989-248">No</span><span class="sxs-lookup"><span data-stu-id="90989-248">No</span></span> |<span data-ttu-id="90989-249">Las notas para documentar recursos hello en la plantilla</span><span class="sxs-lookup"><span data-stu-id="90989-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="90989-250">copia</span><span class="sxs-lookup"><span data-stu-id="90989-250">copy</span></span> |<span data-ttu-id="90989-251">No</span><span class="sxs-lookup"><span data-stu-id="90989-251">No</span></span> |<span data-ttu-id="90989-252">Si se necesita más de una instancia, Hola número de recursos toocreate.</span><span class="sxs-lookup"><span data-stu-id="90989-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="90989-253">modo de saludo predeterminado es paralelo.</span><span class="sxs-lookup"><span data-stu-id="90989-253">hello default mode is parallel.</span></span> <span data-ttu-id="90989-254">Especificar el modo de serie cuando no desea que todos los ni Hola toodeploy recursos en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="90989-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="90989-255">Para más información, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="90989-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="90989-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="90989-256">dependsOn</span></span> |<span data-ttu-id="90989-257">No</span><span class="sxs-lookup"><span data-stu-id="90989-257">No</span></span> |<span data-ttu-id="90989-258">Recursos que se deben implementar antes de implementar este.</span><span class="sxs-lookup"><span data-stu-id="90989-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="90989-259">Administrador de recursos evalúa las dependencias de hello entre los recursos y se implementa en el orden correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="90989-260">Cuando no hay recursos dependientes entre sí, se implementan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="90989-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="90989-261">Hello valor puede ser una lista separada por comas de un recurso de nombres o identificadores únicos de recursos.</span><span class="sxs-lookup"><span data-stu-id="90989-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="90989-262">Solo los recursos de lista que se implementan en esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="90989-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="90989-263">Deben existir los recursos que no estén definidos en esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="90989-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="90989-264">Evite agregar dependencias innecesarias, ya que pueden ralentizar la implementación y crear dependencias circulares.</span><span class="sxs-lookup"><span data-stu-id="90989-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="90989-265">Para obtener instrucciones sobre la configuración de dependencias, consulte [Definición de dependencias en plantillas de Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="90989-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="90989-266">propiedades</span><span class="sxs-lookup"><span data-stu-id="90989-266">properties</span></span> |<span data-ttu-id="90989-267">No</span><span class="sxs-lookup"><span data-stu-id="90989-267">No</span></span> |<span data-ttu-id="90989-268">Opciones de configuración específicas de recursos.</span><span class="sxs-lookup"><span data-stu-id="90989-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="90989-269">valores de Hello para propiedades de Hola se Hola mismo como valores de hello que proporcione en el cuerpo de la solicitud de Hola Hola API de REST operación (método PUT) toocreate Hola recurso.</span><span class="sxs-lookup"><span data-stu-id="90989-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="90989-270">También puede especificar un toocreate de matriz de copia de varias instancias de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="90989-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="90989-271">Para más información, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="90989-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="90989-272">resources</span><span class="sxs-lookup"><span data-stu-id="90989-272">resources</span></span> |<span data-ttu-id="90989-273">No</span><span class="sxs-lookup"><span data-stu-id="90989-273">No</span></span> |<span data-ttu-id="90989-274">Recursos secundarios que dependen del recurso de Hola que se está definiendo.</span><span class="sxs-lookup"><span data-stu-id="90989-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="90989-275">Solo se proporcionan tipos de recursos que se permiten en esquema de Hola de recurso primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="90989-276">Hello nombre completo del tipo de recurso de hello secundario incluye tipo de recurso de hello primario, como **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="90989-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="90989-277">Dependencia de recurso de hello primario no está implícita.</span><span class="sxs-lookup"><span data-stu-id="90989-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="90989-278">Debe definirla explícitamente.</span><span class="sxs-lookup"><span data-stu-id="90989-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="90989-279">sección de recursos de Hello contiene una matriz de hello recursos toodeploy.</span><span class="sxs-lookup"><span data-stu-id="90989-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="90989-280">En cada recurso, puede definir también una matriz de recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="90989-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="90989-281">Por lo tanto, la sección de recursos podría tener una estructura como:</span><span class="sxs-lookup"><span data-stu-id="90989-281">Therefore, your resources section could have a structure like:</span></span>

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

<span data-ttu-id="90989-282">Para obtener más información sobre la definición de recursos secundarios, consulte [Establecimiento del nombre y el tipo de recurso secundario en la plantilla de Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="90989-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="90989-283">Hola **condición** elemento especifica si se implementa el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="90989-284">valor de Hola de este elemento resuelve tootrue o false.</span><span class="sxs-lookup"><span data-stu-id="90989-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="90989-285">Por ejemplo, toospecify si se implementa una nueva cuenta de almacenamiento, use:</span><span class="sxs-lookup"><span data-stu-id="90989-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="90989-286">Para obtener un ejemplo del uso de un recurso nuevo o existente, vea la [plantilla de condición nueva o existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="90989-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="90989-287">toospecify si se implementa una máquina virtual con una contraseña o clave SSH, definir dos versiones de la máquina virtual de hello en la plantilla y usar **condición** toodifferentiate uso.</span><span class="sxs-lookup"><span data-stu-id="90989-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="90989-288">Pasar un parámetro que especifica qué toodeploy escenario.</span><span class="sxs-lookup"><span data-stu-id="90989-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

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

<span data-ttu-id="90989-289">Para obtener un ejemplo del uso de una contraseña o una máquina virtual de toodeploy clave de SSH, consulte [plantilla de condición de nombre de usuario o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="90989-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="90989-290">Salidas</span><span class="sxs-lookup"><span data-stu-id="90989-290">Outputs</span></span>
<span data-ttu-id="90989-291">En la sección de salidas de hello, especifique los valores que se devuelven de la implementación.</span><span class="sxs-lookup"><span data-stu-id="90989-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="90989-292">Por ejemplo, podría devolver Hola URI tooaccess un recurso implementado.</span><span class="sxs-lookup"><span data-stu-id="90989-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="90989-293">Hello en el ejemplo siguiente se muestra hello estructura de una definición de salida:</span><span class="sxs-lookup"><span data-stu-id="90989-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="90989-294">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="90989-294">Element name</span></span> | <span data-ttu-id="90989-295">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="90989-295">Required</span></span> | <span data-ttu-id="90989-296">Descripción</span><span class="sxs-lookup"><span data-stu-id="90989-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="90989-297">outputName</span><span class="sxs-lookup"><span data-stu-id="90989-297">outputName</span></span> |<span data-ttu-id="90989-298">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-298">Yes</span></span> |<span data-ttu-id="90989-299">Nombre del valor de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="90989-299">Name of hello output value.</span></span> <span data-ttu-id="90989-300">Debe ser un identificador válido de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="90989-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="90989-301">type</span><span class="sxs-lookup"><span data-stu-id="90989-301">type</span></span> |<span data-ttu-id="90989-302">Sí</span><span class="sxs-lookup"><span data-stu-id="90989-302">Yes</span></span> |<span data-ttu-id="90989-303">Tipo de valor de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="90989-303">Type of hello output value.</span></span> <span data-ttu-id="90989-304">Los valores de salida admiten Hola mismo tipos como parámetros de entrada de plantilla.</span><span class="sxs-lookup"><span data-stu-id="90989-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="90989-305">value</span><span class="sxs-lookup"><span data-stu-id="90989-305">value</span></span> |<span data-ttu-id="90989-306">yes</span><span class="sxs-lookup"><span data-stu-id="90989-306">Yes</span></span> |<span data-ttu-id="90989-307">Expresión de lenguaje de plantilla que se evaluará y devolverá como valor de salida.</span><span class="sxs-lookup"><span data-stu-id="90989-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="90989-308">Hello en el ejemplo siguiente se muestra un valor que se devuelve en la sección de salidas de Hola.</span><span class="sxs-lookup"><span data-stu-id="90989-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="90989-309">Para más información sobre cómo trabajar con resultados, consulte [Uso compartido del estado con las plantillas de Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="90989-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="90989-310">Límites de plantilla</span><span class="sxs-lookup"><span data-stu-id="90989-310">Template limits</span></span>

<span data-ttu-id="90989-311">Limitar tamaño de saludo de la plantilla too1 MB y cada parámetro too64 KB de archivo.</span><span class="sxs-lookup"><span data-stu-id="90989-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="90989-312">límite de 1 MB de Hola aplica toohello estado final de la plantilla de hello después de que se ha ampliado con las definiciones de recursos iterativo y valores para las variables y parámetros.</span><span class="sxs-lookup"><span data-stu-id="90989-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="90989-313">También está limitado a:</span><span class="sxs-lookup"><span data-stu-id="90989-313">You are also limited to:</span></span>

* <span data-ttu-id="90989-314">256 parámetros</span><span class="sxs-lookup"><span data-stu-id="90989-314">256 parameters</span></span>
* <span data-ttu-id="90989-315">256 variables</span><span class="sxs-lookup"><span data-stu-id="90989-315">256 variables</span></span>
* <span data-ttu-id="90989-316">800 recursos (incluido el recuento de copia)</span><span class="sxs-lookup"><span data-stu-id="90989-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="90989-317">64 valores de salida</span><span class="sxs-lookup"><span data-stu-id="90989-317">64 output values</span></span>
* <span data-ttu-id="90989-318">24 576 caracteres en una expresión de plantilla</span><span class="sxs-lookup"><span data-stu-id="90989-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="90989-319">Puede superar algunos límites de plantilla utilizando una plantilla anidada.</span><span class="sxs-lookup"><span data-stu-id="90989-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="90989-320">Para más información, consulte [Uso de plantillas vinculadas en la implementación de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="90989-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="90989-321">número de hello tooreduce de parámetros, variables o salidas, puede combinar varios valores en un objeto.</span><span class="sxs-lookup"><span data-stu-id="90989-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="90989-322">Para más información, consulte [Objetos como parámetros](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="90989-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90989-323">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90989-323">Next steps</span></span>
* <span data-ttu-id="90989-324">tooview completa plantillas para muchos tipos distintos de soluciones, vea hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="90989-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="90989-325">Para obtener más información acerca de las funciones de Hola que puede utilizar desde dentro de una plantilla, consulte [funciones de plantilla de administrador de recursos de Azure](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="90989-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="90989-326">toocombine varias plantillas durante la implementación, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="90989-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="90989-327">Puede que tenga recursos toouse que existen dentro de otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="90989-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="90989-328">Este escenario es habitual al trabajar con cuentas de almacenamiento o redes virtuales que se comparten entre varios grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="90989-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="90989-329">Para obtener más información, vea hello [función resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="90989-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
