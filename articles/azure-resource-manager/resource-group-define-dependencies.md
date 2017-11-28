---
title: "orden de implementación de aaaSet para recursos de Azure | Documentos de Microsoft"
description: "Describe cómo se implementan tooset un recurso como dependiente de otro recurso durante tooensure los recursos de implementación en el orden correcto de Hola."
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
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="01f15-103">Definir el criterio de Hola para implementar recursos en las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01f15-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="01f15-104">Para un recurso determinado, puede haber otros recursos que deben existir antes de implementan los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="01f15-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="01f15-105">Por ejemplo, un servidor SQL server debe existir antes de intentar toodeploy una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="01f15-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="01f15-106">Definir esta relación marcando un recurso como dependiente de hello otro recurso.</span><span class="sxs-lookup"><span data-stu-id="01f15-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="01f15-107">Definir una dependencia con hello **dependsOn** elemento, o mediante el uso de hello **referencia** función.</span><span class="sxs-lookup"><span data-stu-id="01f15-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="01f15-108">Administrador de recursos evalúa las dependencias de hello entre los recursos y se implementa en su orden dependiente.</span><span class="sxs-lookup"><span data-stu-id="01f15-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="01f15-109">Cuando no hay recursos dependientes entre sí, Administrador de recursos los implementa en paralelo.</span><span class="sxs-lookup"><span data-stu-id="01f15-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="01f15-110">Solo necesita toodefine dependencias de recursos que se implementan en hello misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="01f15-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="01f15-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="01f15-111">dependsOn</span></span>
<span data-ttu-id="01f15-112">Dentro de la plantilla, Hola dependsOn elemento le permite toodefine un recurso como una dependencia en uno o varios recursos.</span><span class="sxs-lookup"><span data-stu-id="01f15-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="01f15-113">Su valor puede ser una lista de nombres de recursos separados por coma.</span><span class="sxs-lookup"><span data-stu-id="01f15-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="01f15-114">Hello en el ejemplo siguiente se muestra un conjunto de escalas de máquina virtual que depende de un equilibrador de carga, la red virtual y un bucle que crea varias cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="01f15-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="01f15-115">Estos otros recursos no se muestran en el siguiente ejemplo de Hola, pero se necesitan tooexist en otra parte de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="01f15-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

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

<span data-ttu-id="01f15-116">En el anterior ejemplo de Hola, se incluye una dependencia en los recursos de Hola que se crean a través de un bucle de copia con el nombre **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="01f15-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="01f15-117">Para ver un ejemplo, consulte [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="01f15-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="01f15-118">Al definir las dependencias, puede incluir Hola recursos proveedor espacio de nombres y el recurso de tipo tooavoid ambigüedad.</span><span class="sxs-lookup"><span data-stu-id="01f15-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="01f15-119">Por ejemplo, tooclarify con formato de un equilibrador de carga y la red virtual que puede tener Hola de que mismos nombres de otros recursos, Hola de uso después:</span><span class="sxs-lookup"><span data-stu-id="01f15-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="01f15-120">Aunque puede ser toouse inclinada dependsOn toomap relaciones entre los recursos, es importante toounderstand ¿por qué se está realizando.</span><span class="sxs-lookup"><span data-stu-id="01f15-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="01f15-121">Por ejemplo, toodocument cómo están conectados entre sí en recursos, dependsOn no es el enfoque correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="01f15-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="01f15-122">No se pueden consultar los recursos que se definieron en el elemento dependsOn de hello después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="01f15-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="01f15-123">El uso de dependsOn podría llegar a repercutir en el tiempo de implementación, ya que Resource Manager no implementa dos recursos en paralelo que tengan una dependencia.</span><span class="sxs-lookup"><span data-stu-id="01f15-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="01f15-124">en su lugar use toodocument relaciones entre los recursos, [vincular los recursos](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="01f15-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="01f15-125">Recursos secundarios</span><span class="sxs-lookup"><span data-stu-id="01f15-125">Child resources</span></span>
<span data-ttu-id="01f15-126">propiedad de recursos de Hello permite recursos secundarios de toospecify que recursos toohello relacionados que se está definiendo.</span><span class="sxs-lookup"><span data-stu-id="01f15-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="01f15-127">Los recursos secundarios solo se pueden definir en cinco niveles de profundidad.</span><span class="sxs-lookup"><span data-stu-id="01f15-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="01f15-128">Es importante creado toonote que no es de una dependencia implícita entre un recurso secundario y el recurso primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="01f15-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="01f15-129">Si necesita hello toobe de recursos secundarios implementada después de recurso primario de hello, debe indicar explícitamente esa dependencia con la propiedad de dependsOn de Hola.</span><span class="sxs-lookup"><span data-stu-id="01f15-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="01f15-130">Cada recurso primario solo acepta determinados tipos de recursos como recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="01f15-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="01f15-131">Hola acepta tipos de recursos se especifican en hello [esquema de la plantilla](https://github.com/Azure/azure-resource-manager-schemas) de recurso primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="01f15-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="01f15-132">Hola nombre secundario del tipo de recurso incluye Hola de tipo de recurso de hello primario, como **Microsoft.Web/sites/config** y **Microsoft.Web/sites/extensions** son ambos recursos secundarios de hello  **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="01f15-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="01f15-133">Hola de ejemplo siguiente muestra un SQL server y la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="01f15-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="01f15-134">Tenga en cuenta que se define una dependencia explícita entre la base de datos SQL de Hola y SQL server, incluso si la base de datos de hello es un elemento secundario del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="01f15-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="01f15-135">función reference</span><span class="sxs-lookup"><span data-stu-id="01f15-135">reference function</span></span>
<span data-ttu-id="01f15-136">Hola [hacen referencia a función](resource-group-template-functions-resource.md#reference) permite una expresión tooderive su valor desde otros pares de nombre y valor JSON o recursos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="01f15-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="01f15-137">Las expresiones de referencia declaran implícitamente que un recurso depende de otro.</span><span class="sxs-lookup"><span data-stu-id="01f15-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="01f15-138">Hola de formato general es:</span><span class="sxs-lookup"><span data-stu-id="01f15-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="01f15-139">En el siguiente ejemplo de Hola, un punto de conexión de red CDN depende explícitamente de perfil de CDN Hola e implícitamente depende de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="01f15-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="01f15-140">Puede usar este elemento u Hola dependencias de toospecify de elemento dependsOn, pero no es necesario toouse ambos para hello mismo recurso dependiente.</span><span class="sxs-lookup"><span data-stu-id="01f15-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="01f15-141">Siempre que sea posible, utilice un tooavoid de referencia implícita agregando una dependencia innecesaria.</span><span class="sxs-lookup"><span data-stu-id="01f15-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="01f15-142">más información, consulte toolearn [hacen referencia a función](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="01f15-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="01f15-143">Recomendaciones para configurar las dependencias</span><span class="sxs-lookup"><span data-stu-id="01f15-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="01f15-144">La hora de decidir qué tooset dependencias, use Hola siguientes instrucciones:</span><span class="sxs-lookup"><span data-stu-id="01f15-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="01f15-145">Establezca el menor número de dependencias posible.</span><span class="sxs-lookup"><span data-stu-id="01f15-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="01f15-146">Establezca un recurso secundario como dependiente de su recurso principal.</span><span class="sxs-lookup"><span data-stu-id="01f15-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="01f15-147">Hola de uso **referencia** funcionar tooset implícita dependencias entre los recursos que necesitan tooshare una propiedad.</span><span class="sxs-lookup"><span data-stu-id="01f15-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="01f15-148">No agregue una dependencia explícita (**dependsOn**) cuando ya haya definido una dependencia implícita.</span><span class="sxs-lookup"><span data-stu-id="01f15-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="01f15-149">Este enfoque reduce el riesgo de Hola de que tengan dependencias innecesarias.</span><span class="sxs-lookup"><span data-stu-id="01f15-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="01f15-150">Establezca una dependencia cuando no se pueda **crear** un recurso sin la funcionalidad de otro recurso.</span><span class="sxs-lookup"><span data-stu-id="01f15-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="01f15-151">No establezca una dependencia si los recursos de hello interactúan solo después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="01f15-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="01f15-152">Permita dependencias en cascada sin establecerlas explícitamente.</span><span class="sxs-lookup"><span data-stu-id="01f15-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="01f15-153">Por ejemplo, la máquina virtual depende de una interfaz de red virtual, y depende de la interfaz de red virtual de hello en una red virtual y las direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="01f15-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="01f15-154">Por lo tanto, máquina virtual de hello es implementados tres todos los recursos, pero no establece explícitamente como dependiente de todos los recursos de tres máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="01f15-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="01f15-155">Este enfoque aclara el orden de dependencia de Hola y resulta más fácil de plantilla de hello toochange más adelante.</span><span class="sxs-lookup"><span data-stu-id="01f15-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="01f15-156">Si no se puede determinar un valor antes de la implementación, intente realizar la implementación de recursos de hello sin una dependencia.</span><span class="sxs-lookup"><span data-stu-id="01f15-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="01f15-157">Por ejemplo, si un valor de configuración requiere nombre de Hola de otro recurso, no necesitará una dependencia.</span><span class="sxs-lookup"><span data-stu-id="01f15-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="01f15-158">Esta guía no siempre funcionará porque algunos recursos comprueban la existencia de hello del programa Hola a otro recurso.</span><span class="sxs-lookup"><span data-stu-id="01f15-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="01f15-159">Si recibe un error, agregue una dependencia.</span><span class="sxs-lookup"><span data-stu-id="01f15-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="01f15-160">Resource Manager identifica dependencias circulares durante la validación de plantillas.</span><span class="sxs-lookup"><span data-stu-id="01f15-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="01f15-161">Si recibe un error que indica que existe una dependencia circular, evaluar su toosee plantilla si todas las dependencias no son necesarios y se pueden quitar.</span><span class="sxs-lookup"><span data-stu-id="01f15-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="01f15-162">Si quitar dependencias no funciona, puede evitar dependencias circulares moviendo algunas operaciones de implementación a los recursos secundarios que se implementan después de recursos de Hola que tienen una dependencia circular Hola.</span><span class="sxs-lookup"><span data-stu-id="01f15-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="01f15-163">Por ejemplo, suponga que va a implementar dos máquinas virtuales pero debe establecer las propiedades en cada uno de ellos que hacen referencia toohello otro.</span><span class="sxs-lookup"><span data-stu-id="01f15-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="01f15-164">Puede implementarlos en hello siguiente orden:</span><span class="sxs-lookup"><span data-stu-id="01f15-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="01f15-165">vm1</span><span class="sxs-lookup"><span data-stu-id="01f15-165">vm1</span></span>
2. <span data-ttu-id="01f15-166">vm2</span><span class="sxs-lookup"><span data-stu-id="01f15-166">vm2</span></span>
3. <span data-ttu-id="01f15-167">La extensión en vm1 depende de vm1 y vm2.</span><span class="sxs-lookup"><span data-stu-id="01f15-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="01f15-168">extensión de Hello establece valores en vm1 que obtiene de vm2.</span><span class="sxs-lookup"><span data-stu-id="01f15-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="01f15-169">La extensión en vm2 depende de vm1 y vm2.</span><span class="sxs-lookup"><span data-stu-id="01f15-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="01f15-170">extensión de Hello establece valores en vm2 que obtiene de vm1.</span><span class="sxs-lookup"><span data-stu-id="01f15-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="01f15-171">Para obtener información sobre cómo evaluar el orden de implementación de Hola y resolver errores de dependencia, vea [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="01f15-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01f15-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01f15-172">Next steps</span></span>
* <span data-ttu-id="01f15-173">toolearn acerca de cómo solucionar problemas de dependencias durante la implementación, consulte [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="01f15-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="01f15-174">toolearn acerca de cómo crear plantillas de Azure Resource Manager, consulte [crear plantillas](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="01f15-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="01f15-175">Para obtener una lista de funciones disponibles de hello en una plantilla, consulte [funciones de plantilla](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="01f15-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

