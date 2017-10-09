---
title: aaaConvert una escala de Azure Resource Manager establezca disco administrado de plantilla toouse | Documentos de Microsoft
description: Convertir una plantilla de conjunto de escala conjunto plantilla tooa disco administrado escala.
keywords: "conjuntos de escalado de máquinas virtuales"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>Convertir una plantilla de conjunto de escala conjunto plantilla tooa disco administrado escala

Los clientes con una plantilla de administrador de recursos para crear una escala establecida no utiliza disco administrado recomendable toomodify se toouse administra el disco. Este artículo se muestra cómo toodo, utilizando como ejemplo una solicitud de extracción de hello [plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates), un repositorio controlada por la Comunidad para las plantillas de administrador de recursos de ejemplo. solicitud de extracción completa de Hola se puede ver aquí: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), y son partes importantes de Hola de diferencias de Hola a continuación, junto con una explicación:

## <a name="making-hello-os-disks-managed"></a>Hacer que los discos de sistema operativo de hello administrados

En la comparación de Hola a continuación, podemos ver que lo hemos quitado varias propiedades variables de cuenta y disco toostorage relacionados. Tipo de cuenta de almacenamiento ya no es necesario (Standard_LRS es predeterminado de hello), pero todavía se puede especificar si quisiéramos. Standard_LRS y Premium_LRS son los únicos valores compatibles con los discos administrados. Nuevo sufijo de la cuenta de almacenamiento, la matriz de cadena única y el recuento de sa se utilizaron en los nombres de hello anterior plantilla toogenerate almacenamiento cuenta. Estas variables ya no son necesarias en la nueva plantilla de hello porque disco administrado crea automáticamente las cuentas de almacenamiento en nombre del cliente de Hola. De forma similar, el nombre del contenedor de vhd y el nombre del disco de sistema operativo ya no son necesarios porque disco administrado automáticamente nombres de discos y los contenedores de blobs de almacenamiento subyacente Hola.

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


En hello diferencia siguiente, se puede ver que se han actualizado Hola calcular api versión too2016-04-30-versión preliminar, que es Hola primera versión requerida para soporte de disco administrado con conjuntos de escalas de. Tenga en cuenta que todavía podríamos usar discos no administrados en la nueva versión de api Hola con sintaxis antigua Hola si lo desea. En otras palabras, si se actualiza solo hello versión de api de proceso y no cambiar nada más, plantilla Hola debe seguir toowork como antes.

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

En diferencias de Hola a continuación, podemos ver que estamos quitando recursos de cuenta de almacenamiento de Hola de matriz de recursos de hello completamente. Ya no se necesita, ya que el disco administrado lo crea automáticamente en nuestro nombre.

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

En diferencias de Hola a continuación, se puede vea que estamos quitando Hola depende cláusula para hacer referencia de bucle de toohello de conjunto de escala de Hola que era la creación de cuentas de almacenamiento. En la plantilla antigua de hello, esto se garantiza que las cuentas de almacenamiento de Hola se crearon antes de conjunto de escalas de hello inició la creación, pero esta cláusula no es necesaria con disco administrado. También quitar la propiedad de contenedores de vhd de Hola y Hola propiedad de nombre de disco de SO como estas propiedades se administran automáticamente bajo el paraguas de hello disco administrado. Si quisiéramos, podríamos agregar `"managedDisk": { "storageAccountType": "Premium_LRS" }` en la configuración de "osDisk" hello si deseamos que los discos de sistema operativo de premium. Solo las máquinas virtuales con en mayúscula o de minúscula ' Hola VM sku puede usar discos premium.

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

No hay ninguna propiedad explícita en la configuración de conjunto de escala Hola para si toouse administrado o un disco no administrado. conjunto de escalas de Hello sabe qué toouse basándose en Propiedades de Hola que están presentes en el perfil de almacenamiento de Hola. Por lo tanto, es importante cuando se modifica hello tooensure de plantilla que son propiedades de derecho de hello en perfil de almacenamiento de Hola de conjunto de escalas de Hola.


## <a name="data-disks"></a>Discos de datos

Con cambios de hello anteriores, Hola escala conjunto usa discos administrados para hello SO disco, pero ¿qué sucede con los discos de datos? tooadd los discos de datos, Agregar propiedad de Hola "dataDisks" en "storageProfile" en hello mismo nivel como "osDisk". valor de propiedad de hello Hello es una lista JSON de objetos, cada uno de los cuales tiene propiedades "lun" (que debe ser exclusivo para cada disco de datos en una máquina virtual), "createOption" ("empty" es actualmente Hola solo es una opción admitida) y "diskSizeGB" (Hola a tamaño del disco de hello en gigabytes; debe ser mayor que 0 y menor que 1024) como en el siguiente ejemplo de Hola: 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

Si especifica `n` discos de esta matriz, cada máquina virtual en la escala de hello establece Obtiene `n` discos de datos. Sin embargo, tenga en cuenta que estos discos de datos son dispositivos sin formato. Es toohello cliente tooattach, Partition y formato Hola discos antes de usarlos. Si lo desea, podríamos también especificar `"managedDisk": { "storageAccountType": "Premium_LRS" }` en cada toospecify de objeto de disco de datos que debe ser un disco de datos premium. Solo las máquinas virtuales con en mayúscula o de minúscula ' Hola VM sku puede usar discos premium.

toolearn más sobre el uso de discos de datos con los conjuntos de escala, vea [este artículo](./virtual-machine-scale-sets-attached-disks.md).


## <a name="next-steps"></a>Pasos siguientes
Por ejemplo plantillas de administrador de recursos mediante conjuntos de escalas, busque "vmss" Hola [repositorio de github de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).

Para obtener información general, consulte hello [página de aterrizaje principal para conjuntos de escalas de](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

