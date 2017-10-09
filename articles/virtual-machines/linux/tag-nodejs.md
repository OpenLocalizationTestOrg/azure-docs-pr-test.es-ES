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
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="8c4ed-103">¿Cómo tootag una máquina virtual de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="8c4ed-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="8c4ed-104">Este artículo describen distintas formas tootag una máquina virtual de Linux en Azure a través del modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c4ed-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="8c4ed-105">Las etiquetas son pares clave-valor definidos por el usuario que se pueden colocar directamente en un recurso o un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8c4ed-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="8c4ed-106">Azure admite actualmente hasta etiquetas de too15 por cada recurso y el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8c4ed-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="8c4ed-107">Etiquetas se pueden colocar en un recurso en tiempo de presentación de la creación o agregan tooan de recurso existente.</span><span class="sxs-lookup"><span data-stu-id="8c4ed-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="8c4ed-108">Tenga en cuenta los recursos creados a través del modelo de implementación de administrador de recursos de hello solo se admiten etiquetas.</span><span class="sxs-lookup"><span data-stu-id="8c4ed-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="8c4ed-109">Etiquetado con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="8c4ed-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="8c4ed-110">toobegin, [instalar y configurar hello Azure CLI](../../xplat-cli-azure-resource-manager.md) y asegúrese de que está en modo de administrador de recursos (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="8c4ed-110">toobegin, [install and configure hello Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="8c4ed-111">Puede ver todas las propiedades de una máquina Virtual determinada, incluidas las etiquetas de hello, utilizar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8c4ed-111">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="8c4ed-112">tooadd una nueva etiqueta de la máquina virtual a través de hello CLI de Azure, puede usar hello `azure vm set` comando junto con el parámetro de la etiqueta de hello **-t**:</span><span class="sxs-lookup"><span data-stu-id="8c4ed-112">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm set` command along with hello tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="8c4ed-113">tooremove todas las etiquetas, puede usar hello **– T** parámetro Hola `azure vm set` comando.</span><span class="sxs-lookup"><span data-stu-id="8c4ed-113">tooremove all tags, you can use hello **–T** parameter in hello `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="8c4ed-114">Ahora que se han aplicado etiquetas tooour recursos CLI de Azure y Hola Portal, echemos un vistazo a toosee de detalles de uso de hello etiquetas hello en el portal de facturación de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c4ed-114">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="8c4ed-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c4ed-115">Next steps</span></span>
* <span data-ttu-id="8c4ed-116">toolearn más información acerca de etiquetado de los recursos de Azure, consulte [Azure Resource Manager Overview] [ Azure Resource Manager Overview] y [tooorganize etiquetas utilizando los recursos de Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="8c4ed-116">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="8c4ed-117">toosee cómo etiquetas pueden ayudar a administrar el uso de recursos de Azure, consulte [descripción de la factura de Azure] [ Understanding your Azure Bill] y [obtener información sobre el consumo de recursos de Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="8c4ed-117">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
