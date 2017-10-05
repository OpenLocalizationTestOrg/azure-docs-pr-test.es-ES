---
title: Procedimientos recomendados para crear plantillas de Resource Manager | Microsoft Docs
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
ms.openlocfilehash: a23301ba88279af3f7bf4d353ae808e9eeb0900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="ce934-103">Procedimientos recomendados para crear plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ce934-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="ce934-104">Estas instrucciones pueden ayudarle a crear plantillas de Azure Resource Manager confiables y fáciles de usar.</span><span class="sxs-lookup"><span data-stu-id="ce934-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="ce934-105">Estas instrucciones son solo sugerencias.</span><span class="sxs-lookup"><span data-stu-id="ce934-105">The guidelines are only suggestions.</span></span> <span data-ttu-id="ce934-106">No son requisitos, excepto si así se indica.</span><span class="sxs-lookup"><span data-stu-id="ce934-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="ce934-107">El escenario podría requerir una variación de uno de los siguientes enfoques o ejemplos.</span><span class="sxs-lookup"><span data-stu-id="ce934-107">Your scenario might require a variation of one of the following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="ce934-108">Nombres de recurso</span><span class="sxs-lookup"><span data-stu-id="ce934-108">Resource names</span></span>
<span data-ttu-id="ce934-109">Por lo general, trabaja con tres tipos de nombres de recursos en Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="ce934-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="ce934-110">Nombres de recurso que deben ser únicos.</span><span class="sxs-lookup"><span data-stu-id="ce934-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="ce934-111">Nombres de recursos que no deben ser únicos, pero elige proporcionar un nombre que pueda ayudarlo a identificar un recurso según el contexto.</span><span class="sxs-lookup"><span data-stu-id="ce934-111">Resource names that are not required to be unique, but you choose to provide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="ce934-112">Nombres de recurso que pueden ser genéricos.</span><span class="sxs-lookup"><span data-stu-id="ce934-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="ce934-113">Para obtener información sobre las restricciones de los nombres de recurso, consulte [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md)(Convenciones de nomenclatura recomendadas para los recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="ce934-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="ce934-114">Nombres de recurso únicos</span><span class="sxs-lookup"><span data-stu-id="ce934-114">Unique resource names</span></span>
<span data-ttu-id="ce934-115">Debe dar un nombre de recurso único para cualquier tipo de recurso que tenga un punto de conexión de acceso a datos.</span><span class="sxs-lookup"><span data-stu-id="ce934-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="ce934-116">Entre los tipos de recursos comunes que requieren un nombre único se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ce934-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="ce934-117">Azure Storage<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="ce934-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="ce934-118">Característica Web Apps de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ce934-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="ce934-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ce934-119">SQL Server</span></span>
* <span data-ttu-id="ce934-120">Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="ce934-120">Azure Key Vault</span></span>
* <span data-ttu-id="ce934-121">Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="ce934-121">Azure Redis Cache</span></span>
* <span data-ttu-id="ce934-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="ce934-122">Azure Batch</span></span>
* <span data-ttu-id="ce934-123">Administrador de tráfico de Azure</span><span class="sxs-lookup"><span data-stu-id="ce934-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="ce934-124">Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="ce934-124">Azure Search</span></span>
* <span data-ttu-id="ce934-125">HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="ce934-125">Azure HDInsight</span></span>

<span data-ttu-id="ce934-126"><sup>1</sup> Los nombres de las cuentas de almacenamiento deben estar en minúsculas, tener 24 caracteres o menos y no incluir guiones.</span><span class="sxs-lookup"><span data-stu-id="ce934-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="ce934-127">Si proporciona un parámetro para un nombre de recurso, debe proporcionar un nombre único cuando implementa el recurso.</span><span class="sxs-lookup"><span data-stu-id="ce934-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy the resource.</span></span> <span data-ttu-id="ce934-128">De manera opcional, puede crear una variable que usa la función [uniqueString()](resource-group-template-functions-string.md#uniquestring) para generar un nombre.</span><span class="sxs-lookup"><span data-stu-id="ce934-128">Optionally, you can create a variable that uses the [uniqueString()](resource-group-template-functions-string.md#uniquestring) function to generate a name.</span></span> 

<span data-ttu-id="ce934-129">También puede que quiera agregar un prefijo o sufijo al resultado **uniqueString**.</span><span class="sxs-lookup"><span data-stu-id="ce934-129">You also might want to add a prefix or suffix to the **uniqueString** result.</span></span> <span data-ttu-id="ce934-130">Modificar el nombre único podría ayudarlo a identificar más fácilmente el tipo de recurso a partir del nombre.</span><span class="sxs-lookup"><span data-stu-id="ce934-130">Modifying the unique name can help you more easily identify the resource type from the name.</span></span> <span data-ttu-id="ce934-131">Por ejemplo, puede generar un nombre único para una cuenta de almacenamiento si usa la variable siguiente:</span><span class="sxs-lookup"><span data-stu-id="ce934-131">For example, you can generate a unique name for a storage account by using the following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="ce934-132">Nombres de recurso para la identificación</span><span class="sxs-lookup"><span data-stu-id="ce934-132">Resource names for identification</span></span>
<span data-ttu-id="ce934-133">Algunos tipos de recursos a los que podría querer asignar un nombre, pero no es necesario que los nombres sean únicos.</span><span class="sxs-lookup"><span data-stu-id="ce934-133">Some resource types you might want to name, but their names do not have to be unique.</span></span> <span data-ttu-id="ce934-134">En el caso de estos tipos de recursos, puede proporcionar un nombre que identifique tanto el contexto del recurso como el tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="ce934-134">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span></span> <span data-ttu-id="ce934-135">Proporcione un nombre descriptivo que ayude a identificar el recurso en una lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="ce934-135">Provide a descriptive name that helps you identify the resource in a list of resources.</span></span> <span data-ttu-id="ce934-136">Si necesita usar un nombre de recurso distinto para implementaciones diferentes, puede usar un parámetro para el nombre:</span><span class="sxs-lookup"><span data-stu-id="ce934-136">If you need to use a different resource name for different deployments, you can use a parameter for the name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "The name of the VM to create."
        }
    }
}
```

<span data-ttu-id="ce934-137">Si no tiene que pasar ningún nombre durante la implementación, puede usar una variable:</span><span class="sxs-lookup"><span data-stu-id="ce934-137">If you do not need to pass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="ce934-138">También puede usar un valor codificado de forma rígida:</span><span class="sxs-lookup"><span data-stu-id="ce934-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="ce934-139">Nombres de recurso genéricos</span><span class="sxs-lookup"><span data-stu-id="ce934-139">Generic resource names</span></span>
<span data-ttu-id="ce934-140">En los tipos de recurso a los que tiene acceso mayoritariamente por medio de otro recurso, puede usar un nombre genérico que esté codificado de forma rígida en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span></span> <span data-ttu-id="ce934-141">Por ejemplo, puede establecer un nombre genérico estándar para reglas de firewall en un servidor SQL:</span><span class="sxs-lookup"><span data-stu-id="ce934-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="ce934-142">Parámetros</span><span class="sxs-lookup"><span data-stu-id="ce934-142">Parameters</span></span>
<span data-ttu-id="ce934-143">La información siguiente puede ser útil cuando se trabaja con parámetros:</span><span class="sxs-lookup"><span data-stu-id="ce934-143">The following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="ce934-144">Minimice el uso de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="ce934-144">Minimize your use of parameters.</span></span> <span data-ttu-id="ce934-145">Siempre que sea posible, use una variable o un valor literal.</span><span class="sxs-lookup"><span data-stu-id="ce934-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="ce934-146">Solo use parámetros en estos escenarios:</span><span class="sxs-lookup"><span data-stu-id="ce934-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="ce934-147">La configuración que desea para usar variaciones de la misma según el entorno (SKU, tamaño, capacidad).</span><span class="sxs-lookup"><span data-stu-id="ce934-147">Settings that you want to use variations of according to environment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="ce934-148">Nombres de recurso que desea especificar para facilitar la identificación.</span><span class="sxs-lookup"><span data-stu-id="ce934-148">Resource names that you want to specify for easy identification.</span></span>
   * <span data-ttu-id="ce934-149">Valores que usa con frecuencia para completar otras tareas (como un nombre de usuario administrador).</span><span class="sxs-lookup"><span data-stu-id="ce934-149">Values that you use frequently to complete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="ce934-150">Secretos (como contraseñas).</span><span class="sxs-lookup"><span data-stu-id="ce934-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="ce934-151">El número o matriz de valores que se usarán cuando cree varias instancias de un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="ce934-151">The number or array of values to use when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="ce934-152">Use una mezcla de mayúsculas y minúsculas para los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="ce934-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="ce934-153">Proporcione una descripción de cada parámetro en los metadatos:</span><span class="sxs-lookup"><span data-stu-id="ce934-153">Provide a description of every parameter in the metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "The type of the new storage account created to store the VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="ce934-154">Defina los valores predeterminados de los parámetros (excepto en el caso de contraseñas y claves SSH):</span><span class="sxs-lookup"><span data-stu-id="ce934-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "The type of the new storage account created to store the VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="ce934-155">Use **SecureString** para todas las contraseñas y secretos:</span><span class="sxs-lookup"><span data-stu-id="ce934-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "The value of the secret to store in the vault."
           }
       }
   }
   ```

* <span data-ttu-id="ce934-156">Siempre que sea posible, no use un parámetro para especificar la ubicación.</span><span class="sxs-lookup"><span data-stu-id="ce934-156">Whenever possible, don't use a parameter to specify location.</span></span> <span data-ttu-id="ce934-157">En lugar de ello, use la propiedad **location** del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ce934-157">Instead, use the **location** property of the resource group.</span></span> <span data-ttu-id="ce934-158">Si usa la expresión **resourceGroup().location** en todos los recursos, los recursos de la plantilla se implementan en la misma ubicación que el grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="ce934-158">By using the **resourceGroup().location** expression for all your resources, resources in the template are deployed in the same location as the resource group:</span></span>
   
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
   
   <span data-ttu-id="ce934-159">Si un tipo de recurso solo se admite en un número limitado de ubicaciones, puede que quiera especificar una ubicación válida directamente en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-159">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template.</span></span> <span data-ttu-id="ce934-160">Si debe usar un parámetro **location**, comparta el valor de ese parámetro al máximo con los recursos que probablemente estén en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="ce934-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely to be in the same location.</span></span> <span data-ttu-id="ce934-161">Con esto se minimiza la cantidad de veces que se les pide a los usuarios que proporcionen información de ubicación.</span><span class="sxs-lookup"><span data-stu-id="ce934-161">This minimizes the number of times users are asked to provide location information.</span></span>
* <span data-ttu-id="ce934-162">Evite usar un parámetro o una variable en la versión de API de un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="ce934-162">Avoid using a parameter or variable for the API version for a resource type.</span></span> <span data-ttu-id="ce934-163">Las propiedades y los valores de los recursos pueden variar en función del número de la versión.</span><span class="sxs-lookup"><span data-stu-id="ce934-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="ce934-164">La función IntelliSense en un editor de código no puede determinar el esquema correcto si la versión de API se establece como un parámetro o una variable.</span><span class="sxs-lookup"><span data-stu-id="ce934-164">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span></span> <span data-ttu-id="ce934-165">En lugar de ello, debe codificar de forma rígida la versión de la API en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-165">Instead, hard-code the API version in the template.</span></span>

## <a name="variables"></a><span data-ttu-id="ce934-166">variables</span><span class="sxs-lookup"><span data-stu-id="ce934-166">Variables</span></span>
<span data-ttu-id="ce934-167">La información siguiente puede ser útil cuando se trabaja con variables:</span><span class="sxs-lookup"><span data-stu-id="ce934-167">The following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="ce934-168">Use las variables para los valores que deba utilizar más de una vez en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-168">Use variables for values that you need to use more than once in a template.</span></span> <span data-ttu-id="ce934-169">Si un valor se usa solo una vez, codificarlo de forma rígida hace que la plantilla resulte más fácil de leer.</span><span class="sxs-lookup"><span data-stu-id="ce934-169">If a value is used only once, a hard-coded value makes your template easier to read.</span></span>
* <span data-ttu-id="ce934-170">No se puede usar la función [reference](resource-group-template-functions-resource.md#reference) en la sección **variables** de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-170">You cannot use the [reference](resource-group-template-functions-resource.md#reference) function in the **variables** section of the template.</span></span> <span data-ttu-id="ce934-171">La función **reference** deriva su valor desde el estado de tiempo de ejecución del recurso.</span><span class="sxs-lookup"><span data-stu-id="ce934-171">The **reference** function derives its value from the resource's runtime state.</span></span> <span data-ttu-id="ce934-172">Sin embargo, las variables se resuelven durante el análisis inicial de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-172">However, variables are resolved during the initial parsing of the template.</span></span> <span data-ttu-id="ce934-173">Construya valores que requieran la función **reference** directamente en las secciones **resources** u **outputs** de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-173">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span></span>
* <span data-ttu-id="ce934-174">Incluya variables para los nombres de recurso que deben ser únicos, como se describe en [Nombres de recurso](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="ce934-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="ce934-175">Puede agrupar las variables en objetos complejos.</span><span class="sxs-lookup"><span data-stu-id="ce934-175">You can group variables into complex objects.</span></span> <span data-ttu-id="ce934-176">Use el formato **variable.subentry** para hacer referencia un valor desde un objeto complejo.</span><span class="sxs-lookup"><span data-stu-id="ce934-176">Use the **variable.subentry** format to reference a value from a complex object.</span></span> <span data-ttu-id="ce934-177">Agrupar las variables puede ayudarlo a hacer seguimiento de variables relacionadas.</span><span class="sxs-lookup"><span data-stu-id="ce934-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="ce934-178">También mejora la legibilidad de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-178">It also improves readability of the template.</span></span> <span data-ttu-id="ce934-179">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce934-179">Here's an example:</span></span>
   
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
   > <span data-ttu-id="ce934-180">Los objetos complejos no pueden contener una expresión que haga referencia a un valor de un objeto complejo.</span><span class="sxs-lookup"><span data-stu-id="ce934-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="ce934-181">Defina una variable independiente para tal fin.</span><span class="sxs-lookup"><span data-stu-id="ce934-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="ce934-182">Para ejemplos avanzados de cómo usar objetos complejos como variables, consulte [Uso compartido de estado en plantillas de Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="ce934-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="ce934-183">Recursos</span><span class="sxs-lookup"><span data-stu-id="ce934-183">Resources</span></span>
<span data-ttu-id="ce934-184">La información siguiente puede ser útil cuando se trabaja con recursos:</span><span class="sxs-lookup"><span data-stu-id="ce934-184">The following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="ce934-185">Para ayudar a otros colaboradores a comprender el propósito del recurso, especifique **comments** para cada recurso de la plantilla:</span><span class="sxs-lookup"><span data-stu-id="ce934-185">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used to store the VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="ce934-186">Puede usar etiquetas para agregar metadatos a los recursos.</span><span class="sxs-lookup"><span data-stu-id="ce934-186">You can use tags to add metadata to resources.</span></span> <span data-ttu-id="ce934-187">Use metadatos para agregar información sobre los recursos.</span><span class="sxs-lookup"><span data-stu-id="ce934-187">Use metadata to add information about your resources.</span></span> <span data-ttu-id="ce934-188">Por ejemplo, puede agregar metadatos para registrar los detalles de facturación de un recurso.</span><span class="sxs-lookup"><span data-stu-id="ce934-188">For example, you can add metadata to record billing details for a resource.</span></span> <span data-ttu-id="ce934-189">Para obtener más información, vea [Uso de etiquetas para organizar los recursos de Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="ce934-189">For more information, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="ce934-190">Si usa un *punto de conexión público* en la plantilla (como un punto de conexión público de Azure Blob Storage), *no codifique de forma rígida* el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="ce934-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span></span> <span data-ttu-id="ce934-191">Use la función **reference** para recuperar dinámicamente el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="ce934-191">Use the **reference** function to dynamically retrieve the namespace.</span></span> <span data-ttu-id="ce934-192">Puede usar este enfoque para implementar la plantilla en diversos entornos de espacios de nombres públicos sin cambiar manualmente el punto de conexión de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-192">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span></span> <span data-ttu-id="ce934-193">Establezca la versión de API en la misma versión que usa para la cuenta de almacenamiento de la plantilla:</span><span class="sxs-lookup"><span data-stu-id="ce934-193">Set the API version to the same version that you are using for the storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="ce934-194">Si la cuenta de almacenamiento se implementa en la misma plantilla que se está creando, no necesita especificar el espacio de nombres del proveedor cuando haga referencia al recurso.</span><span class="sxs-lookup"><span data-stu-id="ce934-194">If the storage account is deployed in the same template that you are creating, you do not need to specify the provider namespace when you reference the resource.</span></span> <span data-ttu-id="ce934-195">La siguiente es la sintaxis simplificada:</span><span class="sxs-lookup"><span data-stu-id="ce934-195">This is the simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="ce934-196">Si tiene otros valores en la plantilla que estén configurados para usar un espacio de nombres público, cámbielos para que reflejen la misma función **reference**.</span><span class="sxs-lookup"><span data-stu-id="ce934-196">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span></span> <span data-ttu-id="ce934-197">Por ejemplo, puede establecer la propiedad **storageUri** del perfil de diagnóstico de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="ce934-197">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="ce934-198">También puede hacer referencia a una cuenta de almacenamiento existente que se encuentra en un grupo de recursos distinto:</span><span class="sxs-lookup"><span data-stu-id="ce934-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="ce934-199">Asigne direcciones IP públicas a una máquina virtual solo cuando lo requiera una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce934-199">Assign public IP addresses to a virtual machine only when an application requires it.</span></span> <span data-ttu-id="ce934-200">Para conectarse a una máquina virtual (VM) para la depuración o con fines administrativos, use reglas NAT de entrada, una puerta de enlace de red o Jumpbox.</span><span class="sxs-lookup"><span data-stu-id="ce934-200">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="ce934-201">Para obtener más información sobre cómo conectarse a máquinas virtuales, consulte:</span><span class="sxs-lookup"><span data-stu-id="ce934-201">For more information about connecting to virtual machines, see:</span></span>
   
   * [<span data-ttu-id="ce934-202">Ejecución de máquinas virtuales para una arquitectura de n niveles en Azure</span><span class="sxs-lookup"><span data-stu-id="ce934-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="ce934-203">Configuración de acceso a WinRM para máquinas virtuales en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ce934-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="ce934-204">Habilitación del acceso externo a la máquina virtual mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ce934-204">Allow external access to your VM by using the Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="ce934-205">Habilitación del acceso externo a la máquina virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce934-205">Allow external access to your VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="ce934-206">Habilitación del acceso externo a la máquina virtual Linux mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ce934-206">Allow external access to your Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="ce934-207">La propiedad **domainNameLabel** para las direcciones IP públicas debe ser única.</span><span class="sxs-lookup"><span data-stu-id="ce934-207">The **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="ce934-208">El valor **domainNameLabel** debe contener entre 3 y 63 caracteres y seguir las reglas especificadas por esta expresión regular: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="ce934-208">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="ce934-209">Como la función **uniqueString** genera una cadena de 13 caracteres, el parámetro **dnsPrefixString** se limita a no más de 50 caracteres:</span><span class="sxs-lookup"><span data-stu-id="ce934-209">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "The DNS label for the public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="ce934-210">Cuando agrega una contraseña a una extensión de script personalizada, use la propiedad **commandToExecute** en la propiedad **protectedSettings**:</span><span class="sxs-lookup"><span data-stu-id="ce934-210">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span></span>
   
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
   > <span data-ttu-id="ce934-211">Para garantizar que los secretos se cifran cuando se transmiten como parámetros a máquinas virtuales y extensiones, use la propiedad **protectedSettings** de las extensiones pertinentes.</span><span class="sxs-lookup"><span data-stu-id="ce934-211">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="ce934-212">Salidas</span><span class="sxs-lookup"><span data-stu-id="ce934-212">Outputs</span></span>
<span data-ttu-id="ce934-213">Si usa una plantilla para crear direcciones IP públicas incluyen una sección **outputs** que devuelve detalles de la dirección IP y el nombre de dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="ce934-213">If you use a template to create public IP addresses, include an **outputs** section that returns details of the IP address and the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="ce934-214">Puede usar valores de salida para recuperar fácilmente los detalles sobre las direcciones IP públicas y los nombres FQDN después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="ce934-214">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="ce934-215">Cuando haga referencia al recurso, use la versión de API que usó para crearlo:</span><span class="sxs-lookup"><span data-stu-id="ce934-215">When you reference the resource, use the API version that you used to create it:</span></span> 

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

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="ce934-216">Comparación entre plantilla única y plantillas anidadas</span><span class="sxs-lookup"><span data-stu-id="ce934-216">Single template vs. nested templates</span></span>
<span data-ttu-id="ce934-217">Para implementar la solución, puede utilizar una sola plantilla o una plantilla principal con varias plantillas anidadas.</span><span class="sxs-lookup"><span data-stu-id="ce934-217">To deploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="ce934-218">Las plantillas anidadas son comunes en escenarios más avanzados.</span><span class="sxs-lookup"><span data-stu-id="ce934-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="ce934-219">Usar una plantilla anidada le ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ce934-219">Using a nested template gives you the following advantages:</span></span>

* <span data-ttu-id="ce934-220">Puede descomponer una solución en componentes específicos.</span><span class="sxs-lookup"><span data-stu-id="ce934-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="ce934-221">Puede volver a usar plantillas anidadas con distintas plantillas principales.</span><span class="sxs-lookup"><span data-stu-id="ce934-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="ce934-222">Si elige usar plantillas anidadas, las siguientes instrucciones pueden ayudarlo a estandarizar el diseño de plantilla.</span><span class="sxs-lookup"><span data-stu-id="ce934-222">If you choose to use nested templates, the following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="ce934-223">Estas instrucciones se basan en [patrones para diseñar plantillas de Azure Resource Manager](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ce934-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="ce934-224">Se recomienda un diseño con las siguientes plantillas:</span><span class="sxs-lookup"><span data-stu-id="ce934-224">We recommend a design that has the following templates:</span></span>

* <span data-ttu-id="ce934-225">**Plantilla principal** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ce934-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="ce934-226">Úsela para los parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="ce934-226">Use for the input parameters.</span></span>
* <span data-ttu-id="ce934-227">**Plantilla de recursos compartidos**.</span><span class="sxs-lookup"><span data-stu-id="ce934-227">**Shared resources template**.</span></span> <span data-ttu-id="ce934-228">Úsela para implementar los recursos compartidos que todos los recursos usan (por ejemplo, conjuntos de disponibilidad y red virtual).</span><span class="sxs-lookup"><span data-stu-id="ce934-228">Use to deploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="ce934-229">Use la expresión **dependsOn** para asegurarse de que esta plantilla se implemente antes que otras.</span><span class="sxs-lookup"><span data-stu-id="ce934-229">Use the **dependsOn** expression to ensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="ce934-230">**Plantilla de recursos opcionales**.</span><span class="sxs-lookup"><span data-stu-id="ce934-230">**Optional resources template**.</span></span> <span data-ttu-id="ce934-231">Úsela para implementar condicionalmente recursos basados en un parámetro (por ejemplo, un jumpbox).</span><span class="sxs-lookup"><span data-stu-id="ce934-231">Use to conditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="ce934-232">**Plantilla de recursos de miembros**.</span><span class="sxs-lookup"><span data-stu-id="ce934-232">**Member resources template**.</span></span> <span data-ttu-id="ce934-233">Cada tipo de instancia dentro de una capa de aplicación tiene su propia configuración.</span><span class="sxs-lookup"><span data-stu-id="ce934-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="ce934-234">Dentro de un nivel, puede definir los distintos tipos de instancia.</span><span class="sxs-lookup"><span data-stu-id="ce934-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="ce934-235">(Por ejemplo, la primera instancia crea un clúster y se agregan instancias adicionales al clúster existente). Cada tipo de instancia tiene su propia plantilla de implementación.</span><span class="sxs-lookup"><span data-stu-id="ce934-235">(For example, the first instance creates a cluster, and additional instances are added to the existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="ce934-236">**Scripts**.</span><span class="sxs-lookup"><span data-stu-id="ce934-236">**Scripts**.</span></span> <span data-ttu-id="ce934-237">Se pueden aplicar scripts ampliamente reutilizables a cada tipo de instancia (por ejemplo, para inicializar y formatear discos adicionales).</span><span class="sxs-lookup"><span data-stu-id="ce934-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="ce934-238">Los scripts personalizados que crea con un fin de personalización específico son distintos, basados en el tipo de instancia.</span><span class="sxs-lookup"><span data-stu-id="ce934-238">Custom scripts that you create for a specific customization purpose are different, based on the instance type.</span></span>

![Plantilla anidada](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="ce934-240">Para más información, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ce934-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-to-nested-templates"></a><span data-ttu-id="ce934-241">Vinculación condicional a plantillas anidadas</span><span class="sxs-lookup"><span data-stu-id="ce934-241">Conditionally link to nested templates</span></span>
<span data-ttu-id="ce934-242">Puede usar un parámetro para vincularse condicionalmente a plantillas anidadas.</span><span class="sxs-lookup"><span data-stu-id="ce934-242">You can use a parameter to conditionally link to nested templates.</span></span> <span data-ttu-id="ce934-243">El parámetro pasa a formar parte del identificador URI de la plantilla:</span><span class="sxs-lookup"><span data-stu-id="ce934-243">The parameter becomes part of the URI for the template:</span></span>

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

## <a name="template-format"></a><span data-ttu-id="ce934-244">Formato de plantilla</span><span class="sxs-lookup"><span data-stu-id="ce934-244">Template format</span></span>
<span data-ttu-id="ce934-245">Es conveniente transferir la plantilla a través de un validador JSON.</span><span class="sxs-lookup"><span data-stu-id="ce934-245">It's a good practice to pass your template through a JSON validator.</span></span> <span data-ttu-id="ce934-246">Un validador puede ayudarle a quitar comas, paréntesis y corchetes extraños que pueden provocar un error durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="ce934-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="ce934-247">Pruebe [JSONLint](http://jsonlint.com/) o un paquete de linter para el entorno de edición de su preferencia (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="ce934-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="ce934-248">También es conveniente dar formato al JSON para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="ce934-248">It's also a good idea to format your JSON for better readability.</span></span> <span data-ttu-id="ce934-249">Puede utilizar un paquete de formateador de JSON para el editor local.</span><span class="sxs-lookup"><span data-stu-id="ce934-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="ce934-250">En Visual Studio, presione **Ctrl+K, Ctrl+D** para dar formato al documento.</span><span class="sxs-lookup"><span data-stu-id="ce934-250">In Visual Studio, to format the document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="ce934-251">En Visual Studio Code, presione **Alt+Mayús+F**.</span><span class="sxs-lookup"><span data-stu-id="ce934-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="ce934-252">Si el editor local no puede dar formato al documento, puede utilizar un [formateador en línea](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="ce934-252">If your local editor doesn't format the document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce934-253">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce934-253">Next steps</span></span>
* <span data-ttu-id="ce934-254">Para instrucciones sobre cómo diseñar la solución para las máquinas virtuales, consulte [Ejecución de una máquina virtual Windows en Azure](../guidance/guidance-compute-single-vm.md) y [Ejecución de una máquina virtual Linux en Azure](../guidance/guidance-compute-single-vm-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ce934-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="ce934-255">Si desea obtener instrucciones sobre cómo configurar una cuenta de almacenamiento, consulte [Lista de comprobación de rendimiento y escalabilidad de Azure Storage](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="ce934-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="ce934-256">Para información sobre cómo una empresa puede usar Resource Manager para administrar suscripciones de manera eficaz, consulte [Scaffold empresarial de Azure: gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ce934-256">To learn about how an enterprise can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

