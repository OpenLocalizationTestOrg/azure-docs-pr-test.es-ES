---
title: Referencia a una red virtual existente en una plantilla de conjunto de escalado de Azure | Microsoft Docs
description: "Obtenga información sobre cómo agregar una red virtual a una plantilla de un conjunto de escalado de máquinas virtuales de Microsoft Azure existente"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: 28117d467b491704aed8d45e5eba42530579dfa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-reference-to-an-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="95227-103">Incorporación de una referencia a una red virtual existente en una plantilla de conjunto de escalado de Azure</span><span class="sxs-lookup"><span data-stu-id="95227-103">Add reference to an existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="95227-104">En este artículo se muestra cómo modificar la [plantilla de conjunto de escalado mínimo viable](./virtual-machine-scale-sets-mvss-start.md) para realizar la implementación en una red virtual existente en lugar de crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="95227-104">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to deploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="95227-105">Cambio de la definición de la plantilla</span><span class="sxs-lookup"><span data-stu-id="95227-105">Change the template definition</span></span>

<span data-ttu-id="95227-106">Nuestra plantilla de conjunto de escalado mínimo viable se puede ver [aquí](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), y nuestra plantilla para implementar el conjunto de escalado en una red virtual se puede ver [aquí](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="95227-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="95227-107">Vamos a examinar la diferencia usada para crear esta plantilla (`git diff minimum-viable-scale-set existing-vnet`) paso a paso:</span><span class="sxs-lookup"><span data-stu-id="95227-107">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="95227-108">Primero, agregamos un parámetro `subnetId`.</span><span class="sxs-lookup"><span data-stu-id="95227-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="95227-109">Esta cadena se pasa a la configuración del conjunto de escalado, lo que permite que el conjunto de escalado identifique la subred creada anteriormente en la que implementar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="95227-109">This string will be passed into the scale set configuration, allowing the scale set to identify the pre-created subnet to deploy virtual machines into.</span></span> <span data-ttu-id="95227-110">Esta cadena debe tener el formato: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="95227-110">This string must be of the form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="95227-111">Por ejemplo, para implementar el conjunto de escalado en una red virtual existente con el nombre `myvnet`, la subred `mysubnet`, el grupo de recursos `myrg` y la suscripción `00000000-0000-0000-0000-000000000000`, el valor de subnetId sería: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="95227-111">For instance, to deploy the scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, the subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

<span data-ttu-id="95227-112">A continuación, podemos eliminar el recurso de red virtual de la matriz `resources`, dado que usamos una red virtual existente y no necesitamos implementar una nueva.</span><span class="sxs-lookup"><span data-stu-id="95227-112">Next, we can delete the virtual network resource from the `resources` array, since we are using an existing virtual network and don't need to deploy a new one.</span></span>

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

<span data-ttu-id="95227-113">La red virtual ya existe antes de que se implemente la plantilla, así que no es necesario especificar una cláusula dependsOn entre el conjunto de escalado y la red virtual.</span><span class="sxs-lookup"><span data-stu-id="95227-113">The virtual network already exists before the template is deployed, so there is no need to specify a dependsOn clause from the scale set to the virtual network.</span></span> <span data-ttu-id="95227-114">Por lo tanto, se eliminan estas líneas:</span><span class="sxs-lookup"><span data-stu-id="95227-114">Thus, we delete these lines:</span></span>

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

<span data-ttu-id="95227-115">Por último, se pasa el parámetro `subnetId` definido por el usuario (en lugar de usar `resourceId` para obtener el id. de una red virtual en la misma implementación, que es lo que hace la plantilla de conjunto de escalado mínimo viable).</span><span class="sxs-lookup"><span data-stu-id="95227-115">Finally, we pass in the `subnetId` parameter set by the user (instead of using `resourceId` to get the id of a vnet in the same deployment, which is what the minimum viable scale set template does).</span></span>

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a><span data-ttu-id="95227-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95227-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
