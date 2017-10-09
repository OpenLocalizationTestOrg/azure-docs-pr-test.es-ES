---
title: procedimientos de aaaBest para crear plantillas de administrador de recursos | Documentos de Microsoft
description: Instrucciones para simplificar las plantillas del Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="a81ff-103">Procedimientos recomendados para crear plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a81ff-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="a81ff-104">Estas instrucciones pueden ayudarle a crear plantillas de Azure Resource Manager toouse fácil y confiable.</span><span class="sxs-lookup"><span data-stu-id="a81ff-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="a81ff-105">instrucciones de Hello son solo sugerencias.</span><span class="sxs-lookup"><span data-stu-id="a81ff-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="a81ff-106">No son requisitos, excepto si así se indica.</span><span class="sxs-lookup"><span data-stu-id="a81ff-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="a81ff-107">El escenario podría requerir una variación de uno de hello siguientes enfoques o ejemplos.</span><span class="sxs-lookup"><span data-stu-id="a81ff-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="a81ff-108">Nombres de recurso</span><span class="sxs-lookup"><span data-stu-id="a81ff-108">Resource names</span></span>
<span data-ttu-id="a81ff-109">Por lo general, trabaja con tres tipos de nombres de recursos en Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="a81ff-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="a81ff-110">Nombres de recurso que deben ser únicos.</span><span class="sxs-lookup"><span data-stu-id="a81ff-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="a81ff-111">Nombres de los recursos que no son necesarias toobe único, pero elija tooprovide un nombre que puede ayudarle a identificar un recurso basado en contexto.</span><span class="sxs-lookup"><span data-stu-id="a81ff-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="a81ff-112">Nombres de recurso que pueden ser genéricos.</span><span class="sxs-lookup"><span data-stu-id="a81ff-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="a81ff-113">Para obtener información sobre las restricciones de los nombres de recurso, consulte [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md)(Convenciones de nomenclatura recomendadas para los recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="a81ff-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="a81ff-114">Nombres de recurso únicos</span><span class="sxs-lookup"><span data-stu-id="a81ff-114">Unique resource names</span></span>
<span data-ttu-id="a81ff-115">Debe dar un nombre de recurso único para cualquier tipo de recurso que tenga un punto de conexión de acceso a datos.</span><span class="sxs-lookup"><span data-stu-id="a81ff-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="a81ff-116">Entre los tipos de recursos comunes que requieren un nombre único se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="a81ff-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="a81ff-117">Azure Storage<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a81ff-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="a81ff-118">Característica Web Apps de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a81ff-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="a81ff-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="a81ff-119">SQL Server</span></span>
* <span data-ttu-id="a81ff-120">Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="a81ff-120">Azure Key Vault</span></span>
* <span data-ttu-id="a81ff-121">Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="a81ff-121">Azure Redis Cache</span></span>
* <span data-ttu-id="a81ff-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="a81ff-122">Azure Batch</span></span>
* <span data-ttu-id="a81ff-123">Administrador de tráfico de Azure</span><span class="sxs-lookup"><span data-stu-id="a81ff-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="a81ff-124">Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="a81ff-124">Azure Search</span></span>
* <span data-ttu-id="a81ff-125">HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="a81ff-125">Azure HDInsight</span></span>

<span data-ttu-id="a81ff-126"><sup>1</sup> Los nombres de las cuentas de almacenamiento deben estar en minúsculas, tener 24 caracteres o menos y no incluir guiones.</span><span class="sxs-lookup"><span data-stu-id="a81ff-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="a81ff-127">Si proporciona un parámetro para un nombre de recurso, debe proporcionar un nombre único al implementar recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="a81ff-128">Si lo desea, puede crear una variable que utiliza hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate un nombre de función.</span><span class="sxs-lookup"><span data-stu-id="a81ff-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="a81ff-129">También podría desea tooadd un prefijo o sufijo toohello **uniqueString** resultado.</span><span class="sxs-lookup"><span data-stu-id="a81ff-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="a81ff-130">Nombre único de modificación Hola permite identificar más fácilmente Hola el tipo de recurso de nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="a81ff-131">Por ejemplo, puede generar un nombre único para una cuenta de almacenamiento mediante el uso de hello después de variable:</span><span class="sxs-lookup"><span data-stu-id="a81ff-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="a81ff-132">Nombres de recurso para la identificación</span><span class="sxs-lookup"><span data-stu-id="a81ff-132">Resource names for identification</span></span>
<span data-ttu-id="a81ff-133">Algunos tipos de recursos puede tooname, pero no es necesario toobe único en sus nombres.</span><span class="sxs-lookup"><span data-stu-id="a81ff-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="a81ff-134">Para estos tipos de recursos, puede proporcionar un nombre que identifica el contexto del recurso de Hola y el tipo de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="a81ff-135">Proporcione un nombre descriptivo que le ayuda a identificar los recursos de hello en una lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="a81ff-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="a81ff-136">Si necesita un nombre de recurso diferente para las distintas implementaciones de toouse, puede usar un parámetro de nombre de hello:</span><span class="sxs-lookup"><span data-stu-id="a81ff-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="a81ff-137">Si no es necesario toopass en un nombre durante la implementación, puede usar una variable:</span><span class="sxs-lookup"><span data-stu-id="a81ff-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="a81ff-138">También puede usar un valor codificado de forma rígida:</span><span class="sxs-lookup"><span data-stu-id="a81ff-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="a81ff-139">Nombres de recurso genéricos</span><span class="sxs-lookup"><span data-stu-id="a81ff-139">Generic resource names</span></span>
<span data-ttu-id="a81ff-140">Tipos de recursos que puede acceso principalmente a través de un recurso diferente, puede utilizar un nombre genérico que está codificado de forma rígida en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="a81ff-141">Por ejemplo, puede establecer un nombre genérico estándar para reglas de firewall en un servidor SQL:</span><span class="sxs-lookup"><span data-stu-id="a81ff-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="a81ff-142">parameters</span><span class="sxs-lookup"><span data-stu-id="a81ff-142">Parameters</span></span>
<span data-ttu-id="a81ff-143">Hello siguiente información puede ser útil al trabajar con parámetros:</span><span class="sxs-lookup"><span data-stu-id="a81ff-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="a81ff-144">Minimice el uso de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="a81ff-144">Minimize your use of parameters.</span></span> <span data-ttu-id="a81ff-145">Siempre que sea posible, use una variable o un valor literal.</span><span class="sxs-lookup"><span data-stu-id="a81ff-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="a81ff-146">Solo use parámetros en estos escenarios:</span><span class="sxs-lookup"><span data-stu-id="a81ff-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="a81ff-147">Configuración que desea que las variaciones de toouse de según tooenvironment (SKU, tamaño, la capacidad).</span><span class="sxs-lookup"><span data-stu-id="a81ff-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="a81ff-148">Nombres de los recursos que desea toospecify para facilitar su identificación.</span><span class="sxs-lookup"><span data-stu-id="a81ff-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="a81ff-149">Valores que se usa con frecuencia toocomplete otras tareas (por ejemplo, un nombre de usuario de administrador).</span><span class="sxs-lookup"><span data-stu-id="a81ff-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="a81ff-150">Secretos (como contraseñas).</span><span class="sxs-lookup"><span data-stu-id="a81ff-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="a81ff-151">número de Hola o matriz de valores toouse al crear varias instancias de un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a81ff-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="a81ff-152">Use una mezcla de mayúsculas y minúsculas para los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="a81ff-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="a81ff-153">Proporcione una descripción de cada parámetro en los metadatos de hello:</span><span class="sxs-lookup"><span data-stu-id="a81ff-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="a81ff-154">Defina los valores predeterminados de los parámetros (excepto en el caso de contraseñas y claves SSH):</span><span class="sxs-lookup"><span data-stu-id="a81ff-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="a81ff-155">Use **SecureString** para todas las contraseñas y secretos:</span><span class="sxs-lookup"><span data-stu-id="a81ff-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="a81ff-156">Siempre que sea posible, no utilice una ubicación de toospecify de parámetro.</span><span class="sxs-lookup"><span data-stu-id="a81ff-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="a81ff-157">En su lugar, use hello **ubicación** propiedad Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a81ff-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="a81ff-158">Mediante el uso de hello **resourceGroup () .location** expresión para todos los recursos, los recursos de plantilla de Hola se implementan en Hola la misma ubicación que el grupo de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="a81ff-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="a81ff-159">Si un tipo de recurso es compatible con solo un número limitado de ubicaciones, conviene toospecify una ubicación válida directamente en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="a81ff-160">Si tiene que utilizar un **ubicación** parámetro, compartir ese valor de parámetro tanto como sea posible con los recursos que son probable toobe Hola misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="a81ff-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="a81ff-161">Esto reduce el número de Hola de veces que se piden a los usuarios información sobre la ubicación tooprovide.</span><span class="sxs-lookup"><span data-stu-id="a81ff-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="a81ff-162">Evite el uso de un parámetro o variable de versión de API de Hola para un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a81ff-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="a81ff-163">Las propiedades y los valores de los recursos pueden variar en función del número de la versión.</span><span class="sxs-lookup"><span data-stu-id="a81ff-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="a81ff-164">IntelliSense en un editor de código no puede determinar el esquema correcto de hello cuando se establece la versión de la API de hello tooa parámetro o variable.</span><span class="sxs-lookup"><span data-stu-id="a81ff-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="a81ff-165">En su lugar, codificar Hola versión de API en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="a81ff-166">variables</span><span class="sxs-lookup"><span data-stu-id="a81ff-166">Variables</span></span>
<span data-ttu-id="a81ff-167">Hello siguiente información puede ser útil al trabajar con variables:</span><span class="sxs-lookup"><span data-stu-id="a81ff-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="a81ff-168">Usar variables para los valores que necesite toouse más de una vez en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="a81ff-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="a81ff-169">Si se usa un valor una sola vez, un valor codificado de forma rígida hace su tooread sea más fácil de plantilla.</span><span class="sxs-lookup"><span data-stu-id="a81ff-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="a81ff-170">No se puede usar hello [referencia](resource-group-template-functions-resource.md#reference) función Hola **variables** sección de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="a81ff-171">Hola **referencia** función deriva su valor de estado de tiempo de ejecución del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="a81ff-172">Sin embargo, las variables se resuelven durante el saludo inicial de análisis de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="a81ff-173">Generar valores que necesitan hello **referencia** función directamente en hello **recursos** o **genera** sección de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="a81ff-174">Incluya variables para los nombres de recurso que deben ser únicos, como se describe en [Nombres de recurso](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="a81ff-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="a81ff-175">Puede agrupar las variables en objetos complejos.</span><span class="sxs-lookup"><span data-stu-id="a81ff-175">You can group variables into complex objects.</span></span> <span data-ttu-id="a81ff-176">Hola de uso **variable.subentry** tooreference un valor de un objeto complejo de formato.</span><span class="sxs-lookup"><span data-stu-id="a81ff-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="a81ff-177">Agrupar las variables puede ayudarlo a hacer seguimiento de variables relacionadas.</span><span class="sxs-lookup"><span data-stu-id="a81ff-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="a81ff-178">También mejora la legibilidad de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-178">It also improves readability of hello template.</span></span> <span data-ttu-id="a81ff-179">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a81ff-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="a81ff-180">Los objetos complejos no pueden contener una expresión que haga referencia a un valor de un objeto complejo.</span><span class="sxs-lookup"><span data-stu-id="a81ff-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="a81ff-181">Defina una variable independiente para tal fin.</span><span class="sxs-lookup"><span data-stu-id="a81ff-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="a81ff-182">Para ejemplos avanzados de cómo usar objetos complejos como variables, consulte [Uso compartido de estado en plantillas de Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="a81ff-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="a81ff-183">Recursos</span><span class="sxs-lookup"><span data-stu-id="a81ff-183">Resources</span></span>
<span data-ttu-id="a81ff-184">Hello siguiente información puede ser útil cuando se trabaja con recursos:</span><span class="sxs-lookup"><span data-stu-id="a81ff-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="a81ff-185">toohelp otros colaboradores de entender Hola propósito del recurso de hello, especifique **comentarios** para cada recurso de plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="a81ff-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="a81ff-186">Puede utilizar etiquetas tooadd metadatos tooresources.</span><span class="sxs-lookup"><span data-stu-id="a81ff-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="a81ff-187">Usar metadatos tooadd información acerca de los recursos.</span><span class="sxs-lookup"><span data-stu-id="a81ff-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="a81ff-188">Por ejemplo, puede agregar detalles de facturación de toorecord de metadatos para un recurso.</span><span class="sxs-lookup"><span data-stu-id="a81ff-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="a81ff-189">Para obtener más información, consulte [mediante etiquetas tooorganize los recursos de Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="a81ff-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="a81ff-190">Si utiliza un *punto de conexión público* en la plantilla (por ejemplo, un Blob de Azure almacenamiento extremo público), *realice no codifique de forma rígida* Hola espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="a81ff-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="a81ff-191">Hola de uso **referencia** función toodynamically recuperar espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="a81ff-192">Puede usar este enfoque toodeploy Hola plantilla toodifferent espacio de nombres públicos los entornos sin cambiar el punto de conexión de hello en plantilla Hola manualmente.</span><span class="sxs-lookup"><span data-stu-id="a81ff-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="a81ff-193">Establecer Hola API versión toohello misma versión que está usando para la cuenta de almacenamiento de hello en la plantilla:</span><span class="sxs-lookup"><span data-stu-id="a81ff-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="a81ff-194">Si se implementa la cuenta de almacenamiento de Hola Hola misma plantilla que está creando, no es necesario espacio de nombres de proveedor de toospecify Hola al hacer referencia a recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="a81ff-195">Ésta es la sintaxis de hello simplificado:</span><span class="sxs-lookup"><span data-stu-id="a81ff-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="a81ff-196">Si tiene otros valores en la plantilla que están configurado toouse un espacio de nombres público, cambiar estos valores tooreflect Hola mismo **referencia** función.</span><span class="sxs-lookup"><span data-stu-id="a81ff-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="a81ff-197">Por ejemplo, puede establecer hello **storageUri** propiedad de perfil de diagnóstico de máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="a81ff-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="a81ff-198">También puede hacer referencia a una cuenta de almacenamiento existente que se encuentra en un grupo de recursos distinto:</span><span class="sxs-lookup"><span data-stu-id="a81ff-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="a81ff-199">Asignar automático público de virtual tooa de direcciones IP solo cuando una aplicación lo requiera.</span><span class="sxs-lookup"><span data-stu-id="a81ff-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="a81ff-200">tooconnect tooa máquina virtual (VM) para la depuración, o para la administración o con fines administrativos, use reglas NAT de entrada, una puerta de enlace de red virtual o un jumpbox.</span><span class="sxs-lookup"><span data-stu-id="a81ff-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="a81ff-201">Para obtener más información acerca de cómo conectar máquinas toovirtual, consulte:</span><span class="sxs-lookup"><span data-stu-id="a81ff-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * [<span data-ttu-id="a81ff-202">Ejecución de máquinas virtuales para una arquitectura de n niveles en Azure</span><span class="sxs-lookup"><span data-stu-id="a81ff-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="a81ff-203">Configuración de acceso a WinRM para máquinas virtuales en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a81ff-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="a81ff-204">Permitir el acceso externo tooyour VM con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a81ff-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="a81ff-205">Permitir el acceso externo tooyour máquina virtual con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a81ff-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="a81ff-206">Permitir el acceso externo tooyour VM de Linux con CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a81ff-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="a81ff-207">Hola **domainNameLabel** propiedad para las direcciones IP públicas debe ser único.</span><span class="sxs-lookup"><span data-stu-id="a81ff-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="a81ff-208">Hola **domainNameLabel** valor debe tener entre 3 y 63 caracteres y seguir reglas de hello especificadas por esta expresión regular: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="a81ff-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="a81ff-209">Dado que hello **uniqueString** función genera una cadena que es 13 caracteres, hello **dnsPrefixString** parámetro es limitado too50 caracteres:</span><span class="sxs-lookup"><span data-stu-id="a81ff-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="a81ff-210">Cuando se agrega una extensión de script personalizado de tooa de contraseña, utilice hello **commandToExecute** propiedad Hola **protectedSettings** propiedad:</span><span class="sxs-lookup"><span data-stu-id="a81ff-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="a81ff-211">tooensure que son secretos cifrados cuando se pasan como parámetros tooVMs y extensiones, usar hello **protectedSettings** propiedad de las extensiones pertinentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="a81ff-212">Salidas</span><span class="sxs-lookup"><span data-stu-id="a81ff-212">Outputs</span></span>
<span data-ttu-id="a81ff-213">Si utiliza una plantilla toocreate las direcciones IP públicas, incluya una **genera** sección que devuelve los detalles de dirección IP de Hola y el nombre de dominio completo (FQDN) de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="a81ff-214">Puede utilizar la salida valores tooeasily recuperar detalles acerca de FQDN y direcciones IP públicas después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="a81ff-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="a81ff-215">Al hacer referencia a recursos de hello, use versión Hola API que usa toocreate:</span><span class="sxs-lookup"><span data-stu-id="a81ff-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="a81ff-216">Comparación entre plantilla única y plantillas anidadas</span><span class="sxs-lookup"><span data-stu-id="a81ff-216">Single template vs. nested templates</span></span>
<span data-ttu-id="a81ff-217">toodeploy la solución, puede usar una única plantilla o una plantilla principal con varias plantillas anidadas.</span><span class="sxs-lookup"><span data-stu-id="a81ff-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="a81ff-218">Las plantillas anidadas son comunes en escenarios más avanzados.</span><span class="sxs-lookup"><span data-stu-id="a81ff-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="a81ff-219">Uso de un proporciona plantillas anidadas Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a81ff-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="a81ff-220">Puede descomponer una solución en componentes específicos.</span><span class="sxs-lookup"><span data-stu-id="a81ff-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="a81ff-221">Puede volver a usar plantillas anidadas con distintas plantillas principales.</span><span class="sxs-lookup"><span data-stu-id="a81ff-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="a81ff-222">Si elige plantillas toouse anidado, Hola siguiendo las directrices puede ayudarle a normalizar el diseño de plantilla.</span><span class="sxs-lookup"><span data-stu-id="a81ff-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="a81ff-223">Estas instrucciones se basan en [patrones para diseñar plantillas de Azure Resource Manager](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a81ff-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="a81ff-224">Se recomienda un diseño que tenga Hola siguientes plantillas:</span><span class="sxs-lookup"><span data-stu-id="a81ff-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="a81ff-225">**Plantilla principal** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="a81ff-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="a81ff-226">Se usa para los parámetros de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="a81ff-227">**Plantilla de recursos compartidos**.</span><span class="sxs-lookup"><span data-stu-id="a81ff-227">**Shared resources template**.</span></span> <span data-ttu-id="a81ff-228">Toodeploy de uso compartido de recursos que usan todos los demás recursos (por ejemplo, virtual red y disponibilidad conjuntos).</span><span class="sxs-lookup"><span data-stu-id="a81ff-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="a81ff-229">Hola de uso **dependsOn** tooensure de expresión que se implementa esta plantilla antes de otras plantillas.</span><span class="sxs-lookup"><span data-stu-id="a81ff-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="a81ff-230">**Plantilla de recursos opcionales**.</span><span class="sxs-lookup"><span data-stu-id="a81ff-230">**Optional resources template**.</span></span> <span data-ttu-id="a81ff-231">Use tooconditionally implementar recursos en función de un parámetro (por ejemplo, un jumpbox).</span><span class="sxs-lookup"><span data-stu-id="a81ff-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="a81ff-232">**Plantilla de recursos de miembros**.</span><span class="sxs-lookup"><span data-stu-id="a81ff-232">**Member resources template**.</span></span> <span data-ttu-id="a81ff-233">Cada tipo de instancia dentro de una capa de aplicación tiene su propia configuración.</span><span class="sxs-lookup"><span data-stu-id="a81ff-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="a81ff-234">Dentro de un nivel, puede definir los distintos tipos de instancia.</span><span class="sxs-lookup"><span data-stu-id="a81ff-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="a81ff-235">(Por ejemplo, Hola primera instancia crea un clúster y se agregan instancias adicionales toohello de clúster existente). Cada tipo de instancia tiene su propia plantilla de implementación.</span><span class="sxs-lookup"><span data-stu-id="a81ff-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="a81ff-236">**Scripts**.</span><span class="sxs-lookup"><span data-stu-id="a81ff-236">**Scripts**.</span></span> <span data-ttu-id="a81ff-237">Se pueden aplicar scripts ampliamente reutilizables a cada tipo de instancia (por ejemplo, para inicializar y formatear discos adicionales).</span><span class="sxs-lookup"><span data-stu-id="a81ff-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="a81ff-238">Scripts personalizados que se crean para un propósito específico personalización son diferentes, según el tipo de instancia Hola.</span><span class="sxs-lookup"><span data-stu-id="a81ff-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![Plantilla anidada](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="a81ff-240">Para más información, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a81ff-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="a81ff-241">Vincular condicionalmente toonested plantillas</span><span class="sxs-lookup"><span data-stu-id="a81ff-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="a81ff-242">Puede usar un parámetro tooconditionally vínculo toonested las plantillas.</span><span class="sxs-lookup"><span data-stu-id="a81ff-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="a81ff-243">parámetro Hello pasa a formar parte del programa Hola URI para la plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="a81ff-243">hello parameter becomes part of hello URI for hello template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="a81ff-244">Formato de plantilla</span><span class="sxs-lookup"><span data-stu-id="a81ff-244">Template format</span></span>
<span data-ttu-id="a81ff-245">Es una buena práctica toopass la plantilla a través de un validador de JSON.</span><span class="sxs-lookup"><span data-stu-id="a81ff-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="a81ff-246">Un validador puede ayudarle a quitar comas, paréntesis y corchetes extraños que pueden provocar un error durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="a81ff-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="a81ff-247">Pruebe [JSONLint](http://jsonlint.com/) o un paquete de linter para el entorno de edición de su preferencia (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="a81ff-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="a81ff-248">También es una buena idea tooformat su JSON para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="a81ff-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="a81ff-249">Puede utilizar un paquete de formateador de JSON para el editor local.</span><span class="sxs-lookup"><span data-stu-id="a81ff-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="a81ff-250">En Visual Studio, documentos de hello tooformat, presione **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="a81ff-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="a81ff-251">En Visual Studio Code, presione **Alt+Mayús+F**.</span><span class="sxs-lookup"><span data-stu-id="a81ff-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="a81ff-252">Si el editor local no dar formato a documentos de hello, puede usar un [formateador en línea](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="a81ff-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a81ff-253">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a81ff-253">Next steps</span></span>
* <span data-ttu-id="a81ff-254">Para instrucciones sobre cómo diseñar la solución para las máquinas virtuales, consulte [Ejecución de una máquina virtual Windows en Azure](../guidance/guidance-compute-single-vm.md) y [Ejecución de una máquina virtual Linux en Azure](../guidance/guidance-compute-single-vm-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a81ff-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="a81ff-255">Si desea obtener instrucciones sobre cómo configurar una cuenta de almacenamiento, consulte [Lista de comprobación de rendimiento y escalabilidad de Azure Storage](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="a81ff-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="a81ff-256">toolearn acerca de cómo una empresa puede usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise: regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a81ff-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

