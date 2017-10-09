---
title: Referencia a una imagen personalizada en una plantilla de conjunto de escalado de Azure | Microsoft Docs
description: "Obtenga información acerca de cómo tooadd personalizado imagen tooan plantilla de conjunto de escalas de máquina Virtual de Azure existente"
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>Agregar que plantilla de conjunto de un tooan de imagen personalizada el escalado de Azure

Este artículo se muestra cómo hello toomodify [plantilla de conjunto de escala viable mínima](./virtual-machine-scale-sets-mvss-start.md) toodeploy de imagen personalizada.

## <a name="change-hello-template-definition"></a>Cambiar la definición de la plantilla de Hola

Se puede ver la plantilla de conjunto de escala viable mínima [aquí](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), y se puede ver la plantilla para la implementación de conjunto desde una imagen personalizada de escalas de hello [aquí](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Examinemos Hola diff utiliza toocreate esta plantilla (`git diff minimum-viable-scale-set custom-image`) parte por parte:

### <a name="creating-a-managed-disk-image"></a>Creación de una imagen de disco administrado

Si ya tiene una imagen de disco administrado personalizada (un recurso del tipo `Microsoft.Compute/images`), puede omitir esta sección.

En primer lugar, agregamos un `sourceImageVhdUri` parámetro, que es Hola URI toohello generalizado blob en el almacenamiento de Azure que contiene toodeploy de imagen personalizada de Hola de.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

A continuación, agregamos un recurso de tipo `Microsoft.Compute/images`, que se basa imagen de disco administrado Hola ubicado en el URI de BLOB de hello generalizado `sourceImageVhdUri`. Esta imagen debe estar en hello misma región que el conjunto de escalas de Hola que lo utilice. En Propiedades de Hola de imagen de hello, especificamos tipo hello SO, ubicación Hola de blob de hello (de hello `sourceImageVhdUri` parámetro) y el tipo de cuenta de almacenamiento de hello:

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

Hola conjunto de escalado de recursos, agregamos un `dependsOn` cláusula que hace referencia toohello toomake de imagen personalizada que se crea la imagen de hello antes de que el conjunto de escalas de hello intente toodeploy desde esa imagen:

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>Imagen de disco administrado de Hola de toouse de propiedades de conjunto de cambio de escala

Hola `imageReference` de escala de hello establecer `storageProfile`, en lugar de especificar el publicador de hello, oferta, sku y versión de una imagen de plataforma, especificamos hello `id` de hello `Microsoft.Compute/images` recursos:

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

En este ejemplo, utilizamos hello `resourceId` creadas de identificador de recurso de función tooget Hola de imagen de Hola Hola mismo plantilla. Si ha creado con antelación imagen de disco administrado hello, debe proporcionar Id. de Hola de esa imagen en su lugar. Este identificador debe tener formato de hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
