---
title: "Conversión de una plantilla de conjunto de escalado de Azure Resource Manager para usar un disco administrado | Microsoft Docs"
description: "Conversión de una plantilla de conjunto de escalado en una plantilla de conjunto de escalado de un disco administrado."
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
ms.openlocfilehash: 2f5cb85703888c5056611d466f508547ee72e44b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="convert-a-scale-set-template-to-a-managed-disk-scale-set-template"></a><span data-ttu-id="18e0e-104">Conversión de una plantilla de conjunto de escalado en una plantilla de conjunto de escalado de un disco administrado</span><span class="sxs-lookup"><span data-stu-id="18e0e-104">Convert a scale set template to a managed disk scale set template</span></span>

<span data-ttu-id="18e0e-105">Los clientes con una plantilla de Resource Manager para crear un conjunto de escalado no sin usar un disco administrado pueden modificarla para usar un disco administrado.</span><span class="sxs-lookup"><span data-stu-id="18e0e-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span></span> <span data-ttu-id="18e0e-106">En este artículo se muestra cómo hacerlo, para lo que usa como ejemplo una solicitud de incorporación de cambios de las [plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates), un repositorio controlada por la comunidad para las plantillas de Resource Manager de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="18e0e-106">This article shows how to do this, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="18e0e-107">La solicitud de incorporación de cambios completa se puede ver aquí: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), y las partes relevantes de la diferencia pueden encontrarse a continuación, junto con una explicación:</span><span class="sxs-lookup"><span data-stu-id="18e0e-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span></span>

## <a name="making-the-os-disks-managed"></a><span data-ttu-id="18e0e-108">Administración de los discos de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="18e0e-108">Making the OS disks managed</span></span>

<span data-ttu-id="18e0e-109">En las diferencias siguientes, se puede ver que se han quitado varias variables relacionadas con las propiedades del disco y de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18e0e-109">In the diff below, we can see that we have removed several variables related to storage account and disk properties.</span></span> <span data-ttu-id="18e0e-110">El tipo de cuenta de almacenamiento ya no es necesario (Standard_LRS es el valor predeterminado), pero se puede especificar si se desea.</span><span class="sxs-lookup"><span data-stu-id="18e0e-110">Storage account type is no longer necessary (Standard_LRS is the default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="18e0e-111">Standard_LRS y Premium_LRS son los únicos valores compatibles con los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="18e0e-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="18e0e-112">El sufijo de la nueva cuenta de almacenamiento, la matriz de cadena única y el recuento de sa se utilizaban en la plantilla antigua para generar nombres de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18e0e-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span></span> <span data-ttu-id="18e0e-113">Estas variables no son necesarias en la nueva plantilla, ya que el disco administrado crea automáticamente cuentas de almacenamiento en nombre del cliente.</span><span class="sxs-lookup"><span data-stu-id="18e0e-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span></span> <span data-ttu-id="18e0e-114">De igual forma, el nombre del contenedor de VHD y el nombre del disco de sistema operativo no son necesarios, porque el disco administrado asigna automáticamente nombres a los discos y contenedores de blobs de almacenamiento subyacentes.</span><span class="sxs-lookup"><span data-stu-id="18e0e-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="18e0e-115">En las diferencias siguientes, se puede ver que se ha actualizado la versión de la API de proceso a la 2016-04-30-preview, que es la primera versión requerida para el soporte de disco administrado con conjuntos de escalado.</span><span class="sxs-lookup"><span data-stu-id="18e0e-115">In the diff below, we can see that we updated the compute api version to 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="18e0e-116">Tenga en cuenta que, si se desea, se pueden usar discos no administrados en la nueva versión de la API con la sintaxis anterior.</span><span class="sxs-lookup"><span data-stu-id="18e0e-116">Note that we could still use unmanaged disks in the new api version with the old syntax if desired.</span></span> <span data-ttu-id="18e0e-117">En otras palabras, si se actualiza la versión de la API de proceso, pero no se cambia nada más, no debería haber ningún cambio en el funcionamiento de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="18e0e-117">In other words, if we only update the compute api version and don't change anything else, the template should continue to work as before.</span></span>

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

<span data-ttu-id="18e0e-118">En las diferencias siguientes, se puede ver que se quita totalmente el recurso de la cuenta de almacenamiento de la matriz de recursos.</span><span class="sxs-lookup"><span data-stu-id="18e0e-118">In the diff below, we can see that we are removing the storage account resource from the resources array completely.</span></span> <span data-ttu-id="18e0e-119">Ya no se necesita, ya que el disco administrado lo crea automáticamente en nuestro nombre.</span><span class="sxs-lookup"><span data-stu-id="18e0e-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="18e0e-120">En las diferencias siguientes, se puede ver que lo que se quita depende de la cláusula a la que se hace referencia desde el conjunto de escalado hasta el bucle que ha creado las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18e0e-120">In the diff below, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span></span> <span data-ttu-id="18e0e-121">En la plantilla antigua, esto garantizaba que las cuentas de almacenamiento se creaban antes de que el conjunto de escalado comenzara la creación, pero esta cláusula no es necesaria con el disco administrado.</span><span class="sxs-lookup"><span data-stu-id="18e0e-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="18e0e-122">También se quitan tanto la propiedad de contenedores de VHD como la propiedad de nombre de disco de sistema operativo, ya que estas propiedades las controla automáticamente el disco administrado.</span><span class="sxs-lookup"><span data-stu-id="18e0e-122">We also remove the vhd containers property, and the os disk name property as these properties are automatically handled under the hood by managed disk.</span></span> <span data-ttu-id="18e0e-123">Podríamos agregar `"managedDisk": { "storageAccountType": "Premium_LRS" }` en la configuración de "osDisk" si deseáramos discos de sistema operativo Premium.</span><span class="sxs-lookup"><span data-stu-id="18e0e-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="18e0e-124">Las únicas máquinas virtuales que pueden usar discos Premium son las que tienen una "s" mayúscula o minúscula en la SKU de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="18e0e-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

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

<span data-ttu-id="18e0e-125">No hay ninguna propiedad explícita en la configuración del conjunto de escalado relativa al uso de un disco administrado o no administrado.</span><span class="sxs-lookup"><span data-stu-id="18e0e-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span></span> <span data-ttu-id="18e0e-126">El conjunto de escalado sabe cuál se debe usar gracias a las propiedades del perfil de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18e0e-126">The scale set knows which to use based on the properties that are present in the storage profile.</span></span> <span data-ttu-id="18e0e-127">Por consiguiente, al modificar la plantilla es importante asegurarse de que el perfil de almacenamiento del conjunto de escalado contiene las propiedades correctas.</span><span class="sxs-lookup"><span data-stu-id="18e0e-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="18e0e-128">Discos de datos</span><span class="sxs-lookup"><span data-stu-id="18e0e-128">Data disks</span></span>

<span data-ttu-id="18e0e-129">Con los cambios anteriores, el conjunto de escalado utiliza discos administrados para el disco del SO, pero ¿y para los discos de datos?</span><span class="sxs-lookup"><span data-stu-id="18e0e-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span></span> <span data-ttu-id="18e0e-130">Para agregar discos de datos, agregue la propiedad "dataDisks" en "storageProfile" al mismo nivel que "osDisk".</span><span class="sxs-lookup"><span data-stu-id="18e0e-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span></span> <span data-ttu-id="18e0e-131">El valor de la propiedad es una lista JSON de objetos, cada uno de los cuales tiene propiedades "lun" (que deben ser únicas para cada disco de datos de una máquina virtual), "createOption" ("empty" es actualmente la única opción admitida) y "diskSizeGB" (el tamaño del disco en gigabytes; debe ser mayor que 0 y menor que 1024) como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="18e0e-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="18e0e-132">Si especifica `n` discos en esta matriz, cada máquina virtual del conjunto de escalado obtiene `n` discos de datos.</span><span class="sxs-lookup"><span data-stu-id="18e0e-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span></span> <span data-ttu-id="18e0e-133">Sin embargo, tenga en cuenta que estos discos de datos son dispositivos</span><span class="sxs-lookup"><span data-stu-id="18e0e-133">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="18e0e-134">sin formato.</span><span class="sxs-lookup"><span data-stu-id="18e0e-134">They are not formatted.</span></span> <span data-ttu-id="18e0e-135">Es responsabilidad del cliente conectar los discos, crearles particiones y formatearlos antes de usarlos.</span><span class="sxs-lookup"><span data-stu-id="18e0e-135">It is up to the customer to attach, paritition, and format the disks before using them.</span></span> <span data-ttu-id="18e0e-136">Opcionalmente, también se puede especificar `"managedDisk": { "storageAccountType": "Premium_LRS" }` en cada objeto del disco de datos para especificar que debe ser un disco de datos Premium.</span><span class="sxs-lookup"><span data-stu-id="18e0e-136">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span></span> <span data-ttu-id="18e0e-137">Las únicas máquinas virtuales que pueden usar discos Premium son las que tienen una "s" mayúscula o minúscula en la SKU de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="18e0e-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

<span data-ttu-id="18e0e-138">Para más información acerca del uso de discos de datos con conjuntos de escalado, consulte [este artículo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="18e0e-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="18e0e-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18e0e-139">Next steps</span></span>
<span data-ttu-id="18e0e-140">Para las plantillas de Azure Resource Manager de ejemplo que usan conjuntos de escalado, busque "vmss" en el [repositorio de GitHub de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="18e0e-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="18e0e-141">Para obtener información general, consulte la [página de destino principal de los conjuntos de escalado](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="18e0e-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

