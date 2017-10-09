---
title: aaaDeploy varias instancias de recursos de Azure | Documentos de Microsoft
description: "Usar operación de copia y matrices en un tooiterate de plantilla de Azure Resource Manager varias veces al implementar los recursos."
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
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="5100e-103">Implementación de varias instancias de un recurso o una propiedad en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5100e-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="5100e-104">Este tema muestra cómo tooiterate en su toocreate de plantilla de Azure Resource Manager varias instancias de un recurso, o varias instancias de una propiedad en un recurso.</span><span class="sxs-lookup"><span data-stu-id="5100e-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="5100e-105">Si necesita tooadd lógica tooyour plantilla que le permite toospecify si se implementa un recurso, vea [implementar de forma condicional recursos](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="5100e-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="5100e-106">Iteración de recursos</span><span class="sxs-lookup"><span data-stu-id="5100e-106">Resource iteration</span></span>
<span data-ttu-id="5100e-107">toocreate varias instancias de un tipo de recurso, agregue un `copy` tipo de recurso de toohello de elemento.</span><span class="sxs-lookup"><span data-stu-id="5100e-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="5100e-108">En el elemento de la copia de hello, especificar número de Hola de iteraciones y un nombre para este bucle.</span><span class="sxs-lookup"><span data-stu-id="5100e-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="5100e-109">el valor del recuento de Hello debe ser un entero positivo y no puede superar los 800.</span><span class="sxs-lookup"><span data-stu-id="5100e-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="5100e-110">El Administrador de recursos crea recursos de hello en paralelo.</span><span class="sxs-lookup"><span data-stu-id="5100e-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="5100e-111">Por lo tanto, no se garantiza el orden de hello en el que se crean.</span><span class="sxs-lookup"><span data-stu-id="5100e-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="5100e-112">toocreate recorren en iteración los recursos de secuencia, vea [serie copia](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="5100e-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="5100e-113">Hola recursos toocreate varias veces toma Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="5100e-113">hello resource toocreate multiple times takes hello following format:</span></span>

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

<span data-ttu-id="5100e-114">Tenga en cuenta que Hola nombre de cada recurso incluye hello `copyIndex()` función, que devuelve la iteración actual de hello en bucle Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="5100e-115">`copyIndex()` es de base cero.</span><span class="sxs-lookup"><span data-stu-id="5100e-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="5100e-116">Por lo tanto, Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5100e-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="5100e-117">Crea estos nombres:</span><span class="sxs-lookup"><span data-stu-id="5100e-117">Creates these names:</span></span>

* <span data-ttu-id="5100e-118">storage0</span><span class="sxs-lookup"><span data-stu-id="5100e-118">storage0</span></span>
* <span data-ttu-id="5100e-119">storage1</span><span class="sxs-lookup"><span data-stu-id="5100e-119">storage1</span></span>
* <span data-ttu-id="5100e-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="5100e-120">storage2.</span></span>

<span data-ttu-id="5100e-121">valor de índice de hello toooffset, puede pasar un valor en función de copyIndex() Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="5100e-122">Hello número de iteraciones tooperform todavía está especificada en el elemento de la copia de hello, pero valor Hola de copyIndex se desplaza por hello especificado valor.</span><span class="sxs-lookup"><span data-stu-id="5100e-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="5100e-123">Por lo tanto, Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5100e-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="5100e-124">Crea estos nombres:</span><span class="sxs-lookup"><span data-stu-id="5100e-124">Creates these names:</span></span>

* <span data-ttu-id="5100e-125">storage1</span><span class="sxs-lookup"><span data-stu-id="5100e-125">storage1</span></span>
* <span data-ttu-id="5100e-126">storage2</span><span class="sxs-lookup"><span data-stu-id="5100e-126">storage2</span></span>
* <span data-ttu-id="5100e-127">storage3</span><span class="sxs-lookup"><span data-stu-id="5100e-127">storage3</span></span>

<span data-ttu-id="5100e-128">operación de copia de Hello es útil al trabajar con matrices, ya que puede recorrer en iteración cada elemento de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="5100e-129">Hola de uso `length` función en hello matriz toospecify Hola un recuento de iteraciones, y `copyIndex` índice actual de hello tooretrieve de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="5100e-130">Por lo tanto, Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5100e-130">So, hello following example:</span></span>

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

<span data-ttu-id="5100e-131">Crea estos nombres:</span><span class="sxs-lookup"><span data-stu-id="5100e-131">Creates these names:</span></span>

* <span data-ttu-id="5100e-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="5100e-132">storagecontoso</span></span>
* <span data-ttu-id="5100e-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="5100e-133">storagefabrikam</span></span>
* <span data-ttu-id="5100e-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="5100e-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="5100e-135">Copia en serie</span><span class="sxs-lookup"><span data-stu-id="5100e-135">Serial copy</span></span>

<span data-ttu-id="5100e-136">Cuando usas Hola copiar elemento toocreate varias instancias de un tipo de recurso, el Administrador de recursos de forma predeterminada, implementa esas instancias en paralelo.</span><span class="sxs-lookup"><span data-stu-id="5100e-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="5100e-137">Sin embargo, puede que desee toospecify ese Hola recursos se implementan en secuencia.</span><span class="sxs-lookup"><span data-stu-id="5100e-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="5100e-138">Por ejemplo, al actualizar un entorno de producción, puede que desee toostagger Hola actualiza tan solo un número determinado se actualizan al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="5100e-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="5100e-139">Administrador de recursos proporciona propiedades de elemento de la copia de Hola que permiten tooserially implementan varias instancias.</span><span class="sxs-lookup"><span data-stu-id="5100e-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="5100e-140">En conjunto de elementos de la copia de hello, `mode` demasiado**serie** y `batchSize` toohello número de instancias toodeploy a la vez.</span><span class="sxs-lookup"><span data-stu-id="5100e-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="5100e-141">Con el modo de serie, el Administrador de recursos crea una dependencia en las instancias anteriores de bucle de hello, por lo que no se inicia un proceso por lotes hasta que se completa el lote anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="5100e-142">Hello propiedad mode también acepta **paralelo**, que es el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="5100e-143">tootest serie copia sin crear recursos reales, Hola de uso después de plantilla que implementa las plantillas anidadas vacías:</span><span class="sxs-lookup"><span data-stu-id="5100e-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="5100e-144">En el historial de implementación de hello, tenga en cuenta que Hola implementaciones anidadas se procesan en secuencia.</span><span class="sxs-lookup"><span data-stu-id="5100e-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![implementación en serie](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="5100e-146">Para un escenario más realista, Hola siguiente ejemplo implementa dos instancias en el momento de una VM de Linux desde una plantilla anidada:</span><span class="sxs-lookup"><span data-stu-id="5100e-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
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
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
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

## <a name="property-iteration"></a><span data-ttu-id="5100e-147">Iteración de propiedades</span><span class="sxs-lookup"><span data-stu-id="5100e-147">Property iteration</span></span>

<span data-ttu-id="5100e-148">toocreate varios valores para una propiedad en un recurso, agregue un `copy` matriz en elemento de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="5100e-149">Esta matriz contiene objetos, y cada objeto tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="5100e-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="5100e-150">nombre: nombre de Hola de hello propiedad toocreate varios valores para</span><span class="sxs-lookup"><span data-stu-id="5100e-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="5100e-151">número - número de Hola de toocreate de valores</span><span class="sxs-lookup"><span data-stu-id="5100e-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="5100e-152">entrada: un objeto que contiene la propiedad Hola valores tooassign toohello</span><span class="sxs-lookup"><span data-stu-id="5100e-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="5100e-153">Hola siguiente ejemplo se muestra cómo tooapply `copy` toohello dataDisks propiedad en una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="5100e-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="5100e-154">Tenga en cuenta que, cuando se usa `copyIndex` dentro de una iteración de la propiedad, debe proporcionar el nombre de Hola de iteración de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="5100e-155">No tiene nombre de hello tooprovide cuando se usa con la iteración de recursos.</span><span class="sxs-lookup"><span data-stu-id="5100e-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="5100e-156">El Administrador de recursos se expande hello `copy` matriz durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="5100e-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="5100e-157">nombre de Hola de matriz de Hola se convierte en nombre de Hola de propiedad Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="5100e-158">los valores de entrada de Hola se convierten en Propiedades del objeto Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-158">hello input values become hello object properties.</span></span> <span data-ttu-id="5100e-159">plantilla de Hello implementado se convierte en:</span><span class="sxs-lookup"><span data-stu-id="5100e-159">hello deployed template becomes:</span></span>

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

<span data-ttu-id="5100e-160">Puede usar la iteración de recursos y propiedades conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="5100e-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="5100e-161">Iteración de propiedad de Hola de referencia por su nombre.</span><span class="sxs-lookup"><span data-stu-id="5100e-161">Reference hello property iteration by name.</span></span>

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

<span data-ttu-id="5100e-162">Solo puede incluir un elemento de la copia en Propiedades de Hola para cada recurso.</span><span class="sxs-lookup"><span data-stu-id="5100e-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="5100e-163">toospecify un bucle de iteración de más de una propiedad, se definen varios objetos de matriz de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="5100e-164">Cada objeto se recorre en iteración por separado.</span><span class="sxs-lookup"><span data-stu-id="5100e-164">Each object is iterated separately.</span></span> <span data-ttu-id="5100e-165">Por ejemplo, toocreate varias instancias de ambos hello `frontendIPConfigurations` hello y propiedad `loadBalancingRules` propiedad en un equilibrador de carga, definir los objetos en un elemento de solo copia:</span><span class="sxs-lookup"><span data-stu-id="5100e-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="5100e-166">Dependencia de los recursos de un bucle</span><span class="sxs-lookup"><span data-stu-id="5100e-166">Depend on resources in a loop</span></span>
<span data-ttu-id="5100e-167">Especifica que se ha implementado un recurso después de otro recurso mediante el uso de hello `dependsOn` elemento.</span><span class="sxs-lookup"><span data-stu-id="5100e-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="5100e-168">toodeploy un recurso que dependa de colección de Hola de recursos en un bucle, proporcionar nombre Hola de bucle de copia de hello en el elemento dependsOn de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="5100e-169">Hola de ejemplo siguiente muestra cómo toodeploy tres cuentas de almacenamiento antes de implementar Hola Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="5100e-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="5100e-170">no se muestra la definición de máquina Virtual completa Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="5100e-171">Observe que ese elemento de la copia de hello tiene nombre establecido demasiado`storagecopy` y elemento de dependsOn de Hola para hello máquinas virtuales también se establece demasiado`storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="5100e-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="5100e-172">Creación de varias instancias de un recurso secundario</span><span class="sxs-lookup"><span data-stu-id="5100e-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="5100e-173">No puede usar un bucle copy en un recurso secundario.</span><span class="sxs-lookup"><span data-stu-id="5100e-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="5100e-174">toocreate varias instancias de un recurso que se define normalmente como anidados dentro de otro recurso, en su lugar, debe crear ese recurso como un recurso de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="5100e-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="5100e-175">Definir relación Hola con recurso primario de Hola a través de las propiedades de tipo y el nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="5100e-176">Por ejemplo, supongamos que suele definir un conjunto de datos como un recurso secundario dentro de una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5100e-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="5100e-177">toocreate varias instancias de conjuntos de datos, muévala fuera de la factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="5100e-178">Hola conjunto de datos debe estar en hello como factoría de datos de Hola de mismo nivel, pero sigue siendo un recurso secundario Hola factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5100e-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="5100e-179">Conservar la relación de hello entre factoría de datos a través de las propiedades de tipo y el nombre de Hola y el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="5100e-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="5100e-180">Puesto que ya no se puede inferir el tipo de su posición en la plantilla de hello, debe proporcionar el tipo hello completo en formato de hello: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="5100e-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="5100e-181">tooestablish una relación primaria-secundaria con una instancia de la factoría de datos de hello, proporcione un nombre para el conjunto de datos de Hola que incluye el nombre del recurso primario Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="5100e-182">Usar el formato de hello: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="5100e-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="5100e-183">Hello en el ejemplo siguiente se muestra hello implementación:</span><span class="sxs-lookup"><span data-stu-id="5100e-183">hello following example shows hello implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="5100e-184">Implementar recursos de forma condicional</span><span class="sxs-lookup"><span data-stu-id="5100e-184">Conditionally deploy resource</span></span>

<span data-ttu-id="5100e-185">toospecify si se implementa un recurso, usar hello `condition` elemento.</span><span class="sxs-lookup"><span data-stu-id="5100e-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="5100e-186">valor de Hola de este elemento resuelve tootrue o false.</span><span class="sxs-lookup"><span data-stu-id="5100e-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="5100e-187">Hola valor es true, se implementa el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="5100e-188">Hola valor es false, no se implementa el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="5100e-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="5100e-189">Por ejemplo, toospecify si se implementa una nueva cuenta de almacenamiento o se utiliza una cuenta de almacenamiento existente, use:</span><span class="sxs-lookup"><span data-stu-id="5100e-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="5100e-190">Para obtener un ejemplo del uso de un recurso nuevo o existente, vea la [plantilla de condición nueva o existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="5100e-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="5100e-191">Para obtener un ejemplo del uso de una contraseña o una máquina virtual de toodeploy clave de SSH, consulte [plantilla de condición de nombre de usuario o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="5100e-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5100e-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5100e-192">Next steps</span></span>
* <span data-ttu-id="5100e-193">Si desea toolearn sobre secciones de Hola de una plantilla, consulte [creación de plantillas de administrador de recursos de Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5100e-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5100e-194">toolearn cómo toodeploy la plantilla, vea [implementar una aplicación con la plantilla de administrador de recursos de Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5100e-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

