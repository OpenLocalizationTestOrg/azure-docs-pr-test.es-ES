---
title: "Establecimiento del orden de implementación de recursos de Azure | Microsoft Docs"
description: "Describe cómo establecer un recurso como dependiente de otro recurso durante la implementación para garantizar el orden de implementación correcto de los recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="4e340-103">Definición del orden de implementación de recursos en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4e340-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="4e340-104">Antes de proceder a la implementación de un recurso determinado, es posible que deban existir otros recursos.</span><span class="sxs-lookup"><span data-stu-id="4e340-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="4e340-105">Por ejemplo, debe existir un servidor SQL para intentar implementar una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="4e340-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="4e340-106">Esta relación se define al marcar un recurso como dependiente del otro.</span><span class="sxs-lookup"><span data-stu-id="4e340-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="4e340-107">Una dependencia se define con el elemento **dependsOn** o mediante la función **reference**.</span><span class="sxs-lookup"><span data-stu-id="4e340-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="4e340-108">Administrador de recursos evalúa las dependencias entre recursos y los implementa en su orden dependiente.</span><span class="sxs-lookup"><span data-stu-id="4e340-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="4e340-109">Cuando no hay recursos dependientes entre sí, Administrador de recursos los implementa en paralelo.</span><span class="sxs-lookup"><span data-stu-id="4e340-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="4e340-110">Solo tiene que definir las dependencias de recursos que se implementan en la misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="4e340-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="4e340-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="4e340-111">dependsOn</span></span>
<span data-ttu-id="4e340-112">Dentro de la plantilla, el elemento dependsOn permite definir un recurso como dependiente de uno o varios recursos.</span><span class="sxs-lookup"><span data-stu-id="4e340-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="4e340-113">Su valor puede ser una lista de nombres de recursos separados por coma.</span><span class="sxs-lookup"><span data-stu-id="4e340-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="4e340-114">En el ejemplo siguiente se muestra un conjunto de escalado de máquinas virtuales que depende de un equilibrador de carga, una red virtual y un bucle que crea varias cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4e340-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="4e340-115">Esos otros recursos no aparecen a continuación, pero tendrían que existir en otra ubicación de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="4e340-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="4e340-116">En el ejemplo anterior, se incluye una dependencia de los recursos que se crean a través de un bucle de copia denominado "**storageLoop**".</span><span class="sxs-lookup"><span data-stu-id="4e340-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="4e340-117">Para ver un ejemplo, consulte [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="4e340-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="4e340-118">Al definir las dependencias, puede incluir el espacio de nombres de proveedor de recursos y el tipo de recurso para evitar la ambigüedad.</span><span class="sxs-lookup"><span data-stu-id="4e340-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="4e340-119">Por ejemplo, para aclarar un equilibrador de carga y la red virtual que puede tener los mismos nombres que otros recursos, utilice el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="4e340-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="4e340-120">Si bien puede que se sienta tentado a usar dependsOn para asignar relaciones entre los recursos, es importante comprender por qué lo hace.</span><span class="sxs-lookup"><span data-stu-id="4e340-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="4e340-121">Por ejemplo, para documentar cómo están interconectados los recursos, dependsOn no es el enfoque correcto.</span><span class="sxs-lookup"><span data-stu-id="4e340-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="4e340-122">No se pueden consultar los recursos que se definieron en el elemento dependsOn después de realizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="4e340-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="4e340-123">El uso de dependsOn podría llegar a repercutir en el tiempo de implementación, ya que Resource Manager no implementa dos recursos en paralelo que tengan una dependencia.</span><span class="sxs-lookup"><span data-stu-id="4e340-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="4e340-124">Para documentar las relaciones entre los recursos, utilice en su lugar la [vinculación de recursos](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="4e340-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="4e340-125">Recursos secundarios</span><span class="sxs-lookup"><span data-stu-id="4e340-125">Child resources</span></span>
<span data-ttu-id="4e340-126">La propiedad resources permite especificar los recursos secundarios que están relacionados con el recurso que se está definiendo.</span><span class="sxs-lookup"><span data-stu-id="4e340-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="4e340-127">Los recursos secundarios solo se pueden definir en cinco niveles de profundidad.</span><span class="sxs-lookup"><span data-stu-id="4e340-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="4e340-128">Es importante tener en cuenta que no se crea una dependencia implícita entre un recurso secundario y el recurso primario.</span><span class="sxs-lookup"><span data-stu-id="4e340-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="4e340-129">Si necesita que el recurso secundario se implemente después del recurso primario, debe declarar explícitamente esa dependencia con la propiedad dependsOn.</span><span class="sxs-lookup"><span data-stu-id="4e340-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="4e340-130">Cada recurso primario solo acepta determinados tipos de recursos como recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="4e340-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="4e340-131">Los tipos de recursos que se aceptan se especifican en el [esquema de plantilla](https://github.com/Azure/azure-resource-manager-schemas) del recurso principal.</span><span class="sxs-lookup"><span data-stu-id="4e340-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="4e340-132">El nombre del tipo de recurso secundario incluye el nombre del tipo de recurso primario, por ejemplo, **Microsoft.Web/sites/config** y **Microsoft.Web/sites/extensions** son ambos recursos secundarios de **Microsoft.Web/Sites**.</span><span class="sxs-lookup"><span data-stu-id="4e340-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="4e340-133">En el ejemplo siguiente se muestran un servidor SQL y una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="4e340-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="4e340-134">Observe que se ha definido una dependencia explícita entre la base de datos SQL y el servidor SQL, a pesar de que la base de datos es un elemento secundario del servidor.</span><span class="sxs-lookup"><span data-stu-id="4e340-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="4e340-135">función reference</span><span class="sxs-lookup"><span data-stu-id="4e340-135">reference function</span></span>
<span data-ttu-id="4e340-136">La [función reference](resource-group-template-functions-resource.md#reference) permite que una expresión derive su valor de otros pares de valor y nombre JSON o de recursos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="4e340-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="4e340-137">Las expresiones de referencia declaran implícitamente que un recurso depende de otro.</span><span class="sxs-lookup"><span data-stu-id="4e340-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="4e340-138">El formato general es:</span><span class="sxs-lookup"><span data-stu-id="4e340-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="4e340-139">En el ejemplo siguiente, un punto de conexión de CDN depende explícitamente del perfil de CDN e implícitamente de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4e340-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="4e340-140">Puede usar este elemento o el elemento dependsOn para especificar las dependencias, pero no es necesario usar ambos para el mismo recurso dependiente.</span><span class="sxs-lookup"><span data-stu-id="4e340-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="4e340-141">Siempre que sea posible, use una referencia implícita para evitar agregar una dependencia innecesaria.</span><span class="sxs-lookup"><span data-stu-id="4e340-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="4e340-142">Para más información, consulte [función reference](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="4e340-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="4e340-143">Recomendaciones para configurar las dependencias</span><span class="sxs-lookup"><span data-stu-id="4e340-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="4e340-144">A la hora de decidir qué dependencias establecer, use las siguientes directrices:</span><span class="sxs-lookup"><span data-stu-id="4e340-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="4e340-145">Establezca el menor número de dependencias posible.</span><span class="sxs-lookup"><span data-stu-id="4e340-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="4e340-146">Establezca un recurso secundario como dependiente de su recurso principal.</span><span class="sxs-lookup"><span data-stu-id="4e340-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="4e340-147">Use la función **reference** para establecer dependencias implícitas entre recursos que necesiten compartir una propiedad.</span><span class="sxs-lookup"><span data-stu-id="4e340-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="4e340-148">No agregue una dependencia explícita (**dependsOn**) cuando ya haya definido una dependencia implícita.</span><span class="sxs-lookup"><span data-stu-id="4e340-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="4e340-149">Este enfoque reduce el riesgo de que se tengan dependencias innecesarias.</span><span class="sxs-lookup"><span data-stu-id="4e340-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="4e340-150">Establezca una dependencia cuando no se pueda **crear** un recurso sin la funcionalidad de otro recurso.</span><span class="sxs-lookup"><span data-stu-id="4e340-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="4e340-151">No establezca una dependencia si los recursos solo interactúan después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="4e340-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="4e340-152">Permita dependencias en cascada sin establecerlas explícitamente.</span><span class="sxs-lookup"><span data-stu-id="4e340-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="4e340-153">Por ejemplo, la máquina virtual depende de una interfaz de red virtual y la interfaz de red virtual depende de una red virtual y las direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="4e340-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="4e340-154">Por lo tanto, la máquina virtual se implementa después de los tres recursos, pero no establece explícitamente la máquina virtual como dependiente de los tres recursos.</span><span class="sxs-lookup"><span data-stu-id="4e340-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="4e340-155">Este enfoque aclara el orden de dependencia y facilita el cambio de la plantilla más adelante.</span><span class="sxs-lookup"><span data-stu-id="4e340-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="4e340-156">Si no se puede determinar un valor antes de la implementación, intente implementar el recurso sin una dependencia.</span><span class="sxs-lookup"><span data-stu-id="4e340-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="4e340-157">Por ejemplo, si un valor de configuración necesita el nombre de otro recurso, quizás no necesite una dependencia.</span><span class="sxs-lookup"><span data-stu-id="4e340-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="4e340-158">Esta guía no siempre funciona porque algunos recursos comprueban la existencia del otro recurso.</span><span class="sxs-lookup"><span data-stu-id="4e340-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="4e340-159">Si recibe un error, agregue una dependencia.</span><span class="sxs-lookup"><span data-stu-id="4e340-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="4e340-160">Resource Manager identifica dependencias circulares durante la validación de plantillas.</span><span class="sxs-lookup"><span data-stu-id="4e340-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="4e340-161">Si recibe un error que indica que existe una dependencia circular, evalúe la plantilla para ver si algunas dependencias no son necesarias y se pueden quitar.</span><span class="sxs-lookup"><span data-stu-id="4e340-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="4e340-162">Si no es suficiente con quitar dependencias, puede evitar dependencias circulares moviendo algunas operaciones de implementación a recursos secundarios que se implementan después de los recursos que tienen la dependencia circular.</span><span class="sxs-lookup"><span data-stu-id="4e340-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="4e340-163">Por ejemplo, suponga que va a implementar dos máquinas virtuales pero debe establecer propiedades en cada una que hagan referencia a la otra.</span><span class="sxs-lookup"><span data-stu-id="4e340-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="4e340-164">Puede implementarlas en el orden siguiente:</span><span class="sxs-lookup"><span data-stu-id="4e340-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="4e340-165">vm1</span><span class="sxs-lookup"><span data-stu-id="4e340-165">vm1</span></span>
2. <span data-ttu-id="4e340-166">vm2</span><span class="sxs-lookup"><span data-stu-id="4e340-166">vm2</span></span>
3. <span data-ttu-id="4e340-167">La extensión en vm1 depende de vm1 y vm2.</span><span class="sxs-lookup"><span data-stu-id="4e340-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="4e340-168">La extensión establece valores en vm1 que obtiene de vm2.</span><span class="sxs-lookup"><span data-stu-id="4e340-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="4e340-169">La extensión en vm2 depende de vm1 y vm2.</span><span class="sxs-lookup"><span data-stu-id="4e340-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="4e340-170">La extensión establece valores en vm2 que obtiene de vm1.</span><span class="sxs-lookup"><span data-stu-id="4e340-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="4e340-171">Para información sobre cómo evaluar el orden de implementación y resolver errores de dependencia, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4e340-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e340-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e340-172">Next steps</span></span>
* <span data-ttu-id="4e340-173">Para aprender a solucionar los problemas de dependencias durante la implementación, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4e340-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="4e340-174">Para más información sobre la creación de plantillas del Administrador de recursos de Azure, consulte [Creación de plantillas](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4e340-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="4e340-175">Para obtener una lista de las funciones disponibles en una plantilla, consulte [Funciones de plantilla](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="4e340-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

