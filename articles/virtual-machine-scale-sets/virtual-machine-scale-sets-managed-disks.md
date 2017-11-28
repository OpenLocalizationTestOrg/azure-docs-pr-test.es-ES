---
title: "aaaUsing administrar discos con Azure escala conjuntos de máquinas virtuales | Documentos de Microsoft"
description: "Obtenga información acerca de cómo y por qué toouse administrar discos con conjuntos de escalas de máquina virtual"
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
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="18053-103">Conjuntos de escalado de máquinas virtuales y discos administrados</span><span class="sxs-lookup"><span data-stu-id="18053-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="18053-104">Los [conjuntos de escalado de máquinas virtuales](/azure/virtual-machine-scale-sets/) de Azure admiten máquinas virtuales con discos administrados.</span><span class="sxs-lookup"><span data-stu-id="18053-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="18053-105">El uso de discos administrados con conjuntos de escalado resulta ventajoso de varias maneras, como por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18053-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="18053-106">Ya no necesita toopre-crear y administrar discos de hello SO de toostore de cuentas de almacenamiento para las máquinas virtuales del conjunto de escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="18053-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="18053-107">Puede asociar el conjunto de escalas de toohello de discos de datos administrados.</span><span class="sxs-lookup"><span data-stu-id="18053-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="18053-108">Con discos administrados, un conjunto de escalado puede tener una capacidad tan alta como 1000 máquinas virtuales, si se basa en una imagen de plataforma o 100 máquinas virtuales, si se basa en una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="18053-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="18053-109">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="18053-109">Get started</span></span>

<span data-ttu-id="18053-110">Una manera sencilla de tooget a trabajar con conjuntos de escalas de disco administrado es toodeploy de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="18053-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="18053-111">Para obtener más información, consulte [este artículo](./virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="18053-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="18053-112">Otra manera simple tooget iniciado es toouse [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy una escala configurada.</span><span class="sxs-lookup"><span data-stu-id="18053-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="18053-113">Hello en el ejemplo siguiente se muestra cómo toocreate una Ubuntu basada escala establecida con 10 máquinas virtuales, cada uno con un disco de 50 GB y 100 GB de datos:</span><span class="sxs-lookup"><span data-stu-id="18053-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="18053-114">Como alternativa, también puede buscar en hello [repositorio de GitHub de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) en las carpetas que contienen `vmss` toosee pregeneradas ejemplos de plantillas que implementación conjuntos de escalado.</span><span class="sxs-lookup"><span data-stu-id="18053-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="18053-115">tootell las plantillas que ya está usando discos administrados, puede hacer referencia demasiado[esta lista](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="18053-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18053-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18053-116">Next steps</span></span>

<span data-ttu-id="18053-117">Para más información sobre los discos administrados en general, consulte [este artículo](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18053-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="18053-118">toosee modo tooconvert establece una escala de tooprovision de plantilla de administrador de recursos con administra los discos, consulte [este artículo](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="18053-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="18053-119">Hello mismas plantillas de administrador de recursos de toohello modificaciones aplican toohello API de REST de Azure.</span><span class="sxs-lookup"><span data-stu-id="18053-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="18053-120">toolearn más sobre el uso de discos de datos administrados con conjuntos de escalado, consulte [este artículo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="18053-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="18053-121">toobegin trabajar con conjuntos de gran escala, consulte demasiado[este artículo](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="18053-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


