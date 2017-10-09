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
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="0c6fc-104">Convertir una plantilla de conjunto de escala conjunto plantilla tooa disco administrado escala</span><span class="sxs-lookup"><span data-stu-id="0c6fc-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="0c6fc-105">Los clientes con una plantilla de administrador de recursos para crear una escala establecida no utiliza disco administrado recomendable toomodify se toouse administra el disco.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="0c6fc-106">Este artículo se muestra cómo toodo, utilizando como ejemplo una solicitud de extracción de hello [plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates), un repositorio controlada por la Comunidad para las plantillas de administrador de recursos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="0c6fc-107">solicitud de extracción completa de Hola se puede ver aquí: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), y son partes importantes de Hola de diferencias de Hola a continuación, junto con una explicación:</span><span class="sxs-lookup"><span data-stu-id="0c6fc-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="0c6fc-108">Hacer que los discos de sistema operativo de hello administrados</span><span class="sxs-lookup"><span data-stu-id="0c6fc-108">Making hello OS disks managed</span></span>

<span data-ttu-id="0c6fc-109">En la comparación de Hola a continuación, podemos ver que lo hemos quitado varias propiedades variables de cuenta y disco toostorage relacionados.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="0c6fc-110">Tipo de cuenta de almacenamiento ya no es necesario (Standard_LRS es predeterminado de hello), pero todavía se puede especificar si quisiéramos.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="0c6fc-111">Standard_LRS y Premium_LRS son los únicos valores compatibles con los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="0c6fc-112">Nuevo sufijo de la cuenta de almacenamiento, la matriz de cadena única y el recuento de sa se utilizaron en los nombres de hello anterior plantilla toogenerate almacenamiento cuenta.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="0c6fc-113">Estas variables ya no son necesarias en la nueva plantilla de hello porque disco administrado crea automáticamente las cuentas de almacenamiento en nombre del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="0c6fc-114">De forma similar, el nombre del contenedor de vhd y el nombre del disco de sistema operativo ya no son necesarios porque disco administrado automáticamente nombres de discos y los contenedores de blobs de almacenamiento subyacente Hola.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="0c6fc-115">En hello diferencia siguiente, se puede ver que se han actualizado Hola calcular api versión too2016-04-30-versión preliminar, que es Hola primera versión requerida para soporte de disco administrado con conjuntos de escalas de.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="0c6fc-116">Tenga en cuenta que todavía podríamos usar discos no administrados en la nueva versión de api Hola con sintaxis antigua Hola si lo desea.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="0c6fc-117">En otras palabras, si se actualiza solo hello versión de api de proceso y no cambiar nada más, plantilla Hola debe seguir toowork como antes.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

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

<span data-ttu-id="0c6fc-118">En diferencias de Hola a continuación, podemos ver que estamos quitando recursos de cuenta de almacenamiento de Hola de matriz de recursos de hello completamente.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="0c6fc-119">Ya no se necesita, ya que el disco administrado lo crea automáticamente en nuestro nombre.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="0c6fc-120">En diferencias de Hola a continuación, se puede vea que estamos quitando Hola depende cláusula para hacer referencia de bucle de toohello de conjunto de escala de Hola que era la creación de cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="0c6fc-121">En la plantilla antigua de hello, esto se garantiza que las cuentas de almacenamiento de Hola se crearon antes de conjunto de escalas de hello inició la creación, pero esta cláusula no es necesaria con disco administrado.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="0c6fc-122">También quitar la propiedad de contenedores de vhd de Hola y Hola propiedad de nombre de disco de SO como estas propiedades se administran automáticamente bajo el paraguas de hello disco administrado.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="0c6fc-123">Si quisiéramos, podríamos agregar `"managedDisk": { "storageAccountType": "Premium_LRS" }` en la configuración de "osDisk" hello si deseamos que los discos de sistema operativo de premium.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="0c6fc-124">Solo las máquinas virtuales con en mayúscula o de minúscula ' Hola VM sku puede usar discos premium.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

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

<span data-ttu-id="0c6fc-125">No hay ninguna propiedad explícita en la configuración de conjunto de escala Hola para si toouse administrado o un disco no administrado.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="0c6fc-126">conjunto de escalas de Hello sabe qué toouse basándose en Propiedades de Hola que están presentes en el perfil de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="0c6fc-127">Por lo tanto, es importante cuando se modifica hello tooensure de plantilla que son propiedades de derecho de hello en perfil de almacenamiento de Hola de conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="0c6fc-128">Discos de datos</span><span class="sxs-lookup"><span data-stu-id="0c6fc-128">Data disks</span></span>

<span data-ttu-id="0c6fc-129">Con cambios de hello anteriores, Hola escala conjunto usa discos administrados para hello SO disco, pero ¿qué sucede con los discos de datos? tooadd los discos de datos, Agregar propiedad de Hola "dataDisks" en "storageProfile" en hello mismo nivel como "osDisk".</span><span class="sxs-lookup"><span data-stu-id="0c6fc-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="0c6fc-130">valor de propiedad de hello Hello es una lista JSON de objetos, cada uno de los cuales tiene propiedades "lun" (que debe ser exclusivo para cada disco de datos en una máquina virtual), "createOption" ("empty" es actualmente Hola solo es una opción admitida) y "diskSizeGB" (Hola a tamaño del disco de hello en gigabytes; debe ser mayor que 0 y menor que 1024) como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="0c6fc-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="0c6fc-131">Si especifica `n` discos de esta matriz, cada máquina virtual en la escala de hello establece Obtiene `n` discos de datos.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="0c6fc-132">Sin embargo, tenga en cuenta que estos discos de datos son dispositivos</span><span class="sxs-lookup"><span data-stu-id="0c6fc-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="0c6fc-133">sin formato.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-133">They are not formatted.</span></span> <span data-ttu-id="0c6fc-134">Es toohello cliente tooattach, Partition y formato Hola discos antes de usarlos.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="0c6fc-135">Si lo desea, podríamos también especificar `"managedDisk": { "storageAccountType": "Premium_LRS" }` en cada toospecify de objeto de disco de datos que debe ser un disco de datos premium.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="0c6fc-136">Solo las máquinas virtuales con en mayúscula o de minúscula ' Hola VM sku puede usar discos premium.</span><span class="sxs-lookup"><span data-stu-id="0c6fc-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="0c6fc-137">toolearn más sobre el uso de discos de datos con los conjuntos de escala, vea [este artículo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="0c6fc-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="0c6fc-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0c6fc-138">Next steps</span></span>
<span data-ttu-id="0c6fc-139">Por ejemplo plantillas de administrador de recursos mediante conjuntos de escalas, busque "vmss" Hola [repositorio de github de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="0c6fc-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="0c6fc-140">Para obtener información general, consulte hello [página de aterrizaje principal para conjuntos de escalas de](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="0c6fc-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

