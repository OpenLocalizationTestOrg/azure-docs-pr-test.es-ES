---
title: "aaaHow tootag una máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Obtenga información sobre cómo etiquetar una máquina virtual de Linux de Azure creada en Azure con el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="c18c4-103">¿Cómo tootag una máquina virtual de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="c18c4-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="c18c4-104">Este artículo describen distintas formas tootag una máquina virtual de Linux en Azure a través del modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c18c4-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="c18c4-105">Las etiquetas son pares clave-valor definidos por el usuario que se pueden colocar directamente en un recurso o un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c18c4-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="c18c4-106">Azure admite actualmente hasta etiquetas de too15 por cada recurso y el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c18c4-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="c18c4-107">Etiquetas se pueden colocar en un recurso en tiempo de presentación de la creación o agregan tooan de recurso existente.</span><span class="sxs-lookup"><span data-stu-id="c18c4-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="c18c4-108">Tenga en cuenta los recursos creados a través del modelo de implementación de administrador de recursos de hello solo se admiten etiquetas.</span><span class="sxs-lookup"><span data-stu-id="c18c4-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="c18c4-109">Etiquetado con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c18c4-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="c18c4-110">toobegin, necesita hello más reciente [2.0 de CLI de Azure (vista previa)](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c18c4-110">toobegin, you need hello latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c18c4-111">También puede realizar estos pasos con hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c18c4-111">You can also perform these steps with hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c18c4-112">Puede ver todas las propiedades de una máquina Virtual determinada, incluidas las etiquetas de hello, utilizar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c18c4-112">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="c18c4-113">tooadd una nueva etiqueta de la máquina virtual a través de hello CLI de Azure, puede usar hello `azure vm update` comando junto con el parámetro de la etiqueta de hello **--establecer**:</span><span class="sxs-lookup"><span data-stu-id="c18c4-113">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm update` command along with hello tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="c18c4-114">etiquetas de tooremove, puede usar hello **--quitar** parámetro Hola `azure vm update` comando.</span><span class="sxs-lookup"><span data-stu-id="c18c4-114">tooremove tags, you can use hello **--remove** parameter in hello `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="c18c4-115">Ahora que se han aplicado etiquetas tooour recursos CLI de Azure y Hola Portal, echemos un vistazo a toosee de detalles de uso de hello etiquetas hello en el portal de facturación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c18c4-115">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="c18c4-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c18c4-116">Next steps</span></span>
* <span data-ttu-id="c18c4-117">toolearn más información acerca de etiquetado de los recursos de Azure, consulte [Azure Resource Manager Overview] [ Azure Resource Manager Overview] y [tooorganize etiquetas utilizando los recursos de Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="c18c4-117">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="c18c4-118">toosee cómo etiquetas pueden ayudar a administrar el uso de recursos de Azure, consulte [descripción de la factura de Azure] [ Understanding your Azure Bill] y [obtener información sobre el consumo de recursos de Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="c18c4-118">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
