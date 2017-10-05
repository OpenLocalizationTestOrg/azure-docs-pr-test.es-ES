---
title: "Implementación de varias instancias de recursos de Azure | Microsoft Docs"
description: "Use la operación de copia y matrices en una plantilla del Administrador de recursos de Azure para iterar varias veces al implementar recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: ed8e3081d2b2e07938d7cf3aa5f95f6dde81bc66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="41140-103">Implementación de varias instancias de un recurso o una propiedad en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="41140-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="41140-104">En este tema se muestra cómo iterar en la plantilla de Azure Resource Manager para crear varias instancias de un recurso o varias instancias de una propiedad de un recurso.</span><span class="sxs-lookup"><span data-stu-id="41140-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="41140-105">Si tiene que agregar lógica a la plantilla que le permita especificar si se ha implementado un recurso, vea [Implementar recursos de forma condicional](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="41140-105">If you need to add logic to your template that enables you to specify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="41140-106">Iteración de recursos</span><span class="sxs-lookup"><span data-stu-id="41140-106">Resource iteration</span></span>
<span data-ttu-id="41140-107">Para crear varias instancias de un tipo de recurso, agregue un elemento `copy` al tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="41140-107">To create multiple instances of a resource type, add a `copy` element to the resource type.</span></span> <span data-ttu-id="41140-108">En el elemento de copia, especifique el número de iteraciones y un nombre para este bucle.</span><span class="sxs-lookup"><span data-stu-id="41140-108">In the copy element, you specify the number of iterations and a name for this loop.</span></span> <span data-ttu-id="41140-109">El valor de recuento debe ser un número entero positivo y no puede ser superior a 800.</span><span class="sxs-lookup"><span data-stu-id="41140-109">The count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="41140-110">Resource Manager crea los recursos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="41140-110">Resource Manager creates the resources in parallel.</span></span> <span data-ttu-id="41140-111">Por lo tanto, no se garantiza el orden en el que se crean.</span><span class="sxs-lookup"><span data-stu-id="41140-111">Therefore, the order in which they are created is not guaranteed.</span></span> <span data-ttu-id="41140-112">Para crear recursos iterados en secuencia, consulte [Copia en serie](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="41140-112">To create iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="41140-113">El recurso para crear varias veces tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="41140-113">The resource to create multiple times takes the following format:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="41140-114">Tenga en cuenta que el nombre de cada recurso incluye la función `copyIndex()`, que devuelve la iteración actual del bucle.</span><span class="sxs-lookup"><span data-stu-id="41140-114">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span></span> <span data-ttu-id="41140-115">`copyIndex()` es de base cero.</span><span class="sxs-lookup"><span data-stu-id="41140-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="41140-116">Así, en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="41140-116">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="41140-117">Crea estos nombres:</span><span class="sxs-lookup"><span data-stu-id="41140-117">Creates these names:</span></span>

* <span data-ttu-id="41140-118">storage0</span><span class="sxs-lookup"><span data-stu-id="41140-118">storage0</span></span>
* <span data-ttu-id="41140-119">storage1</span><span class="sxs-lookup"><span data-stu-id="41140-119">storage1</span></span>
* <span data-ttu-id="41140-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="41140-120">storage2.</span></span>

<span data-ttu-id="41140-121">Para desplazar el valor de índice, puede pasar un valor de la función copyIndex().</span><span class="sxs-lookup"><span data-stu-id="41140-121">To offset the index value, you can pass a value in the copyIndex() function.</span></span> <span data-ttu-id="41140-122">El número de iteraciones que se deben realizar todavía se especifica en el elemento copy, pero el valor de copyIndex se desplaza el valor especificado.</span><span class="sxs-lookup"><span data-stu-id="41140-122">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span></span> <span data-ttu-id="41140-123">Así, en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="41140-123">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="41140-124">Crea estos nombres:</span><span class="sxs-lookup"><span data-stu-id="41140-124">Creates these names:</span></span>

* <span data-ttu-id="41140-125">storage1</span><span class="sxs-lookup"><span data-stu-id="41140-125">storage1</span></span>
* <span data-ttu-id="41140-126">storage2</span><span class="sxs-lookup"><span data-stu-id="41140-126">storage2</span></span>
* <span data-ttu-id="41140-127">storage3</span><span class="sxs-lookup"><span data-stu-id="41140-127">storage3</span></span>

<span data-ttu-id="41140-128">La operación de copia es útil al trabajar con matrices, ya que puede iterar a través de cada elemento de la matriz.</span><span class="sxs-lookup"><span data-stu-id="41140-128">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span></span> <span data-ttu-id="41140-129">Use la función `length` en la matriz para especificar el número de iteraciones, y `copyIndex` para recuperar el índice actual de la matriz.</span><span class="sxs-lookup"><span data-stu-id="41140-129">Use the `length` function on the array to specify the count for iterations, and `copyIndex` to retrieve the current index in the array.</span></span> <span data-ttu-id="41140-130">Así, en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="41140-130">So, the following example:</span></span>

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

<span data-ttu-id="41140-131">Crea estos nombres:</span><span class="sxs-lookup"><span data-stu-id="41140-131">Creates these names:</span></span>

* <span data-ttu-id="41140-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="41140-132">storagecontoso</span></span>
* <span data-ttu-id="41140-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="41140-133">storagefabrikam</span></span>
* <span data-ttu-id="41140-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="41140-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="41140-135">Copia en serie</span><span class="sxs-lookup"><span data-stu-id="41140-135">Serial copy</span></span>

<span data-ttu-id="41140-136">Al usar el elemento de copia para crear varias instancias de un tipo de recurso, Resource Manager implementa esas instancias en paralelo de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="41140-136">When you use the copy element to create multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="41140-137">Sin embargo, es posible que quiera especificar que los recursos se implementen en secuencia.</span><span class="sxs-lookup"><span data-stu-id="41140-137">However, you may want to specify that the resources are deployed in sequence.</span></span> <span data-ttu-id="41140-138">Por ejemplo, al actualizar un entorno de producción, puede que quiera escalonar las actualizaciones para que solo una cantidad determinada se actualice al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="41140-138">For example, when updating a production environment, you may want to stagger the updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="41140-139">Resource Manager proporciona las propiedades sobre el elemento de copia que le permiten implementar varias instancias en serie.</span><span class="sxs-lookup"><span data-stu-id="41140-139">Resource Manager provides properties on the copy element that enable you to serially deploy multiple instances.</span></span> <span data-ttu-id="41140-140">En el elemento de copia, establezca `mode` en **serial** y `batchSize` en el número de instancias que se implementarán a la vez.</span><span class="sxs-lookup"><span data-stu-id="41140-140">In the copy element, set `mode` to **serial** and `batchSize` to the number of instances to deploy at a time.</span></span> <span data-ttu-id="41140-141">Con mode establecido en serial, Resource Manager crea una dependencia en las instancias anteriores del bucle, por lo que no se inicia ningún lote hasta que se completa el lote anterior.</span><span class="sxs-lookup"><span data-stu-id="41140-141">With serial mode, Resource Manager creates a dependency on earlier instances in the loop, so it does not start one batch until the previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="41140-142">La propiedad mode también acepta **parallel**, que es el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="41140-142">The mode property also accepts **parallel**, which is the default value.</span></span>

<span data-ttu-id="41140-143">Para probar la copia en serie sin crear recursos reales, use la siguiente plantilla, que implementa plantillas anidadas vacías:</span><span class="sxs-lookup"><span data-stu-id="41140-143">To test serial copy without creating actual resources, use the following template that deploys empty nested templates:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

<span data-ttu-id="41140-144">En el historial de implementación, observe que las implementaciones anidadas se procesan en secuencia.</span><span class="sxs-lookup"><span data-stu-id="41140-144">In the deployment history, notice that the nested deployments are processed in sequence.</span></span>

![implementación en serie](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="41140-146">Para un escenario más realista, en el ejemplo siguiente se implementan dos instancias a la vez de una VM de Linux a partir de una plantilla anidada:</span><span class="sxs-lookup"><span data-stu-id="41140-146">For a more realistic scenario, the following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for the Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for the Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for the Public IP used to access the Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a><span data-ttu-id="41140-147">Iteración de propiedades</span><span class="sxs-lookup"><span data-stu-id="41140-147">Property iteration</span></span>

<span data-ttu-id="41140-148">Para crear varios valores para una propiedad de un recurso, agregue una matriz `copy` en el elemento properties.</span><span class="sxs-lookup"><span data-stu-id="41140-148">To create multiple values for a property on a resource, add a `copy` array in the properties element.</span></span> <span data-ttu-id="41140-149">Esta matriz contiene objetos, y cada objeto tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="41140-149">This array contains objects, and each object has the following properties:</span></span>

* <span data-ttu-id="41140-150">nombre: el nombre de la propiedad para la que se van a crear varios valores</span><span class="sxs-lookup"><span data-stu-id="41140-150">name - the name of the property to create multiple values for</span></span>
* <span data-ttu-id="41140-151">recuento: el número de valores que se van a crear</span><span class="sxs-lookup"><span data-stu-id="41140-151">count - the number of values to create</span></span>
* <span data-ttu-id="41140-152">entrada: un objeto que contiene los valores que se van a asignar a la propiedad</span><span class="sxs-lookup"><span data-stu-id="41140-152">input - an object that contains the values to assign to the property</span></span>  

<span data-ttu-id="41140-153">En el ejemplo siguiente se muestra cómo aplicar `copy` a la propiedad dataDisks en una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="41140-153">The following example shows how to apply `copy` to the dataDisks property on a virtual machine:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="41140-154">Tenga en cuenta que, cuando se usa `copyIndex` dentro de una iteración de propiedad, debe proporcionar el nombre de la iteración.</span><span class="sxs-lookup"><span data-stu-id="41140-154">Notice that when using `copyIndex` inside a property iteration, you must provide the name of the iteration.</span></span> <span data-ttu-id="41140-155">No tiene que proporcionar el nombre cuando se usa con la iteración de recursos.</span><span class="sxs-lookup"><span data-stu-id="41140-155">You do not have to provide the name when used with resource iteration.</span></span>

<span data-ttu-id="41140-156">Resource Manager expande la matriz `copy` durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="41140-156">Resource Manager expands the `copy` array during deployment.</span></span> <span data-ttu-id="41140-157">El nombre de la matriz se convierte en el nombre de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="41140-157">The name of the array becomes the name of the property.</span></span> <span data-ttu-id="41140-158">Los valores de entrada se convierten en las propiedades del objeto.</span><span class="sxs-lookup"><span data-stu-id="41140-158">The input values become the object properties.</span></span> <span data-ttu-id="41140-159">La plantilla implementada se convierte en:</span><span class="sxs-lookup"><span data-stu-id="41140-159">The deployed template becomes:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="41140-160">Puede usar la iteración de recursos y propiedades conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="41140-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="41140-161">Haga referencia a la iteración de la propiedad por el nombre.</span><span class="sxs-lookup"><span data-stu-id="41140-161">Reference the property iteration by name.</span></span>

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

<span data-ttu-id="41140-162">Solo puede incluir un elemento de copia en las propiedades de cada recurso.</span><span class="sxs-lookup"><span data-stu-id="41140-162">You can only include one copy element in the properties for each resource.</span></span> <span data-ttu-id="41140-163">Para especificar un bucle de iteración para más de una propiedad, defina varios objetos en la matriz de copia.</span><span class="sxs-lookup"><span data-stu-id="41140-163">To specify an iteration loop for more than one property, define multiple objects in the copy array.</span></span> <span data-ttu-id="41140-164">Cada objeto se recorre en iteración por separado.</span><span class="sxs-lookup"><span data-stu-id="41140-164">Each object is iterated separately.</span></span> <span data-ttu-id="41140-165">Por ejemplo, para crear varias instancias de las propiedades `frontendIPConfigurations` y `loadBalancingRules` en un equilibrador de carga, defina los dos objetos en un solo elemento de copia:</span><span class="sxs-lookup"><span data-stu-id="41140-165">For example, to create multiple instances of both the `frontendIPConfigurations` property and the `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="41140-166">Dependencia de los recursos de un bucle</span><span class="sxs-lookup"><span data-stu-id="41140-166">Depend on resources in a loop</span></span>
<span data-ttu-id="41140-167">Especifique que un recurso se implemente después de otro recurso mediante el elemento `dependsOn`.</span><span class="sxs-lookup"><span data-stu-id="41140-167">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span></span> <span data-ttu-id="41140-168">Para implementar un recurso que dependa de la colección de recursos de un bucle, proporcione el nombre del bucle copy en el elemento dependsOn.</span><span class="sxs-lookup"><span data-stu-id="41140-168">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span></span> <span data-ttu-id="41140-169">En el ejemplo siguiente se muestra cómo implementar tres cuentas de almacenamiento antes de implementar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41140-169">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span></span> <span data-ttu-id="41140-170">La definición de la máquina virtual no se muestra.</span><span class="sxs-lookup"><span data-stu-id="41140-170">The full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="41140-171">Tenga en cuenta que el elemento copy tiene el nombre establecido en `storagecopy` y el elemento dependsOn para las máquinas virtuales también se establece en `storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="41140-171">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="41140-172">Creación de varias instancias de un recurso secundario</span><span class="sxs-lookup"><span data-stu-id="41140-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="41140-173">No puede usar un bucle copy en un recurso secundario.</span><span class="sxs-lookup"><span data-stu-id="41140-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="41140-174">Para crear varias instancias de un recurso que se define normalmente como anidado dentro de otro recurso, debe crear en su lugar dicho recurso como uno de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="41140-174">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="41140-175">La relación con el recurso principal se define a través de las propiedades type y name.</span><span class="sxs-lookup"><span data-stu-id="41140-175">You define the relationship with the parent resource through the type and name properties.</span></span>

<span data-ttu-id="41140-176">Por ejemplo, supongamos que suele definir un conjunto de datos como un recurso secundario dentro de una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="41140-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

<span data-ttu-id="41140-177">Para crear varias instancias de conjuntos de datos, muévalos fuera de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="41140-177">To create multiple instances of data sets, move it outside of the data factory.</span></span> <span data-ttu-id="41140-178">El conjunto de datos debe estar en el mismo nivel que la factoría de datos, pero seguirá siendo un recurso secundario de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="41140-178">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span></span> <span data-ttu-id="41140-179">La relación entre el conjunto de datos y la factoría de datos se conserva a través de los parámetros type y name.</span><span class="sxs-lookup"><span data-stu-id="41140-179">You preserve the relationship between data set and data factory through the type and name properties.</span></span> <span data-ttu-id="41140-180">Puesto que la propiedad de type ya no se puede inferir de su posición en la plantilla, debe proporcionar el nombre completo del tipo con el formato: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="41140-180">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="41140-181">Para establecer una relación de principal-secundario con una instancia de la factoría de datos, proporcione un nombre para el conjunto de datos que incluya el nombre de recurso principal.</span><span class="sxs-lookup"><span data-stu-id="41140-181">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span></span> <span data-ttu-id="41140-182">Utilice el formato: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="41140-182">Use the format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="41140-183">En el siguiente ejemplo se muestra la implementación:</span><span class="sxs-lookup"><span data-stu-id="41140-183">The following example shows the implementation:</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="41140-184">Implementar recursos de forma condicional</span><span class="sxs-lookup"><span data-stu-id="41140-184">Conditionally deploy resource</span></span>

<span data-ttu-id="41140-185">Para especificar si se ha implementado un recurso, use el elemento `condition`.</span><span class="sxs-lookup"><span data-stu-id="41140-185">To specify whether a resource is deployed, use the `condition` element.</span></span> <span data-ttu-id="41140-186">El valor de este elemento se resuelve como true o false.</span><span class="sxs-lookup"><span data-stu-id="41140-186">The value for this element resolves to true or false.</span></span> <span data-ttu-id="41140-187">Cuando el valor es true, el recurso se implementa.</span><span class="sxs-lookup"><span data-stu-id="41140-187">When the value is true, the resource is deployed.</span></span> <span data-ttu-id="41140-188">Cuando el valor es false, el recurso no se implementa.</span><span class="sxs-lookup"><span data-stu-id="41140-188">When the value is false, the resource is not deployed.</span></span> <span data-ttu-id="41140-189">Por ejemplo, para especificar si se implementa una nueva cuenta de almacenamiento o se usa una cuenta de almacenamiento existente, use:</span><span class="sxs-lookup"><span data-stu-id="41140-189">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="41140-190">Para obtener un ejemplo del uso de un recurso nuevo o existente, vea la [plantilla de condición nueva o existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="41140-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="41140-191">Para obtener un ejemplo del uso de una contraseña o clave SSH para implementar la máquina virtual, vea la [plantilla de condición de nombre de usuario o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="41140-191">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41140-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41140-192">Next steps</span></span>
* <span data-ttu-id="41140-193">Para obtener información sobre las secciones de una plantilla, consulte el artículo sobre cómo [crear plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="41140-193">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="41140-194">Para obtener información sobre cómo implementar la plantilla, consulte [Implementación de una aplicación con la plantilla del Administrador de recursos de Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="41140-194">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

