---
title: Referencia a una red virtual existente en una plantilla de conjunto de escalado de Azure | Microsoft Docs
description: "Obtenga información acerca de cómo tooadd un virtual red tooan plantilla de conjunto de escala de máquinas virtuales de Azure existente"
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
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>Agregar referencia tooan red virtual en una plantilla de conjunto de escalado de Azure

Este artículo se muestra cómo hello toomodify [plantilla de conjunto de escala viable mínima](./virtual-machine-scale-sets-mvss-start.md) toodeploy en una red virtual existente en lugar de crear uno nuevo.

## <a name="change-hello-template-definition"></a>Cambiar la definición de la plantilla de Hola

Se puede ver la plantilla de conjunto de escala viable mínima [aquí](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), y se puede ver la plantilla para la implementación de escala de Hola se ha establecido en una red virtual existente [aquí](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Examinemos Hola diff utiliza toocreate esta plantilla (`git diff minimum-viable-scale-set existing-vnet`) parte por parte:

Primero, agregamos un parámetro `subnetId`. Esta cadena se pasarán en configuración de conjunto de escalado de hello, permitiendo Hola conjunto de escalado de subred creada previamente de hello tooidentify toodeploy las máquinas virtuales en. Esta cadena debe tener formato de hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Por ejemplo, escala de hello toodeploy establecido en una red virtual existente con el nombre `myvnet`, subred `mysubnet`, grupo de recursos `myrg`, suscripciones y `00000000-0000-0000-0000-000000000000`, sería Hola subnetId: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

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

A continuación, podemos eliminar recursos de red virtual de Hola de hello `resources` matriz, ya que se está usando una red virtual existente y no es necesario toodeploy uno nuevo.

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

red virtual de Hello ya existe antes de implementa la plantilla de hello, así que no hay ninguna necesidad de toospecify una cláusula de dependsOn de escala de hello establezca toohello de red virtual. Por lo tanto, se eliminan estas líneas:

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

Por último, pasamos Hola `subnetId` parámetro establecido por el usuario de hello (en lugar de usar `resourceId` tooget Id. de Hola de una red virtual en hello misma implementación, que es la plantilla de conjunto de escala viable mínima Hola).

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




## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
