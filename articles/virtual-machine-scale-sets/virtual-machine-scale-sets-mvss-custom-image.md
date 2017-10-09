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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="79cd4-103">Agregar que plantilla de conjunto de un tooan de imagen personalizada el escalado de Azure</span><span class="sxs-lookup"><span data-stu-id="79cd4-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="79cd4-104">Este artículo se muestra cómo hello toomodify [plantilla de conjunto de escala viable mínima](./virtual-machine-scale-sets-mvss-start.md) toodeploy de imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="79cd4-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="79cd4-105">Cambiar la definición de la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="79cd4-105">Change hello template definition</span></span>

<span data-ttu-id="79cd4-106">Se puede ver la plantilla de conjunto de escala viable mínima [aquí](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), y se puede ver la plantilla para la implementación de conjunto desde una imagen personalizada de escalas de hello [aquí](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="79cd4-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="79cd4-107">Examinemos Hola diff utiliza toocreate esta plantilla (`git diff minimum-viable-scale-set custom-image`) parte por parte:</span><span class="sxs-lookup"><span data-stu-id="79cd4-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="79cd4-108">Creación de una imagen de disco administrado</span><span class="sxs-lookup"><span data-stu-id="79cd4-108">Creating a managed disk image</span></span>

<span data-ttu-id="79cd4-109">Si ya tiene una imagen de disco administrado personalizada (un recurso del tipo `Microsoft.Compute/images`), puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="79cd4-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="79cd4-110">En primer lugar, agregamos un `sourceImageVhdUri` parámetro, que es Hola URI toohello generalizado blob en el almacenamiento de Azure que contiene toodeploy de imagen personalizada de Hola de.</span><span class="sxs-lookup"><span data-stu-id="79cd4-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


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

<span data-ttu-id="79cd4-111">A continuación, agregamos un recurso de tipo `Microsoft.Compute/images`, que se basa imagen de disco administrado Hola ubicado en el URI de BLOB de hello generalizado `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="79cd4-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="79cd4-112">Esta imagen debe estar en hello misma región que el conjunto de escalas de Hola que lo utilice.</span><span class="sxs-lookup"><span data-stu-id="79cd4-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="79cd4-113">En Propiedades de Hola de imagen de hello, especificamos tipo hello SO, ubicación Hola de blob de hello (de hello `sourceImageVhdUri` parámetro) y el tipo de cuenta de almacenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="79cd4-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

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

<span data-ttu-id="79cd4-114">Hola conjunto de escalado de recursos, agregamos un `dependsOn` cláusula que hace referencia toohello toomake de imagen personalizada que se crea la imagen de hello antes de que el conjunto de escalas de hello intente toodeploy desde esa imagen:</span><span class="sxs-lookup"><span data-stu-id="79cd4-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="79cd4-115">Imagen de disco administrado de Hola de toouse de propiedades de conjunto de cambio de escala</span><span class="sxs-lookup"><span data-stu-id="79cd4-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="79cd4-116">Hola `imageReference` de escala de hello establecer `storageProfile`, en lugar de especificar el publicador de hello, oferta, sku y versión de una imagen de plataforma, especificamos hello `id` de hello `Microsoft.Compute/images` recursos:</span><span class="sxs-lookup"><span data-stu-id="79cd4-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="79cd4-117">En este ejemplo, utilizamos hello `resourceId` creadas de identificador de recurso de función tooget Hola de imagen de Hola Hola mismo plantilla.</span><span class="sxs-lookup"><span data-stu-id="79cd4-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="79cd4-118">Si ha creado con antelación imagen de disco administrado hello, debe proporcionar Id. de Hola de esa imagen en su lugar.</span><span class="sxs-lookup"><span data-stu-id="79cd4-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="79cd4-119">Este identificador debe tener formato de hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="79cd4-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="79cd4-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79cd4-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
