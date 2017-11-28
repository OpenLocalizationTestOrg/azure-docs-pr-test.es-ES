---
title: "Procedimiento para etiquetar una máquina virtual Linux en Azure | Microsoft Docs"
description: "Infórmese sobre el etiquetado de una máquina virtual Linux de Azure creada con el modelo de implementación de Resource Manager."
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
ms.openlocfilehash: f643001c85e127ae39e9869ffdc689bcac232ccb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="9c1cf-103">Etiquetado de una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="9c1cf-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="9c1cf-104">En este artículo se describen diferentes maneras de etiquetar una máquina virtual en Azure el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9c1cf-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="9c1cf-105">Las etiquetas son pares clave-valor definidos por el usuario que se pueden colocar directamente en un recurso o un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9c1cf-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="9c1cf-106">Actualmente, Azure admite un máximo de 15 etiquetas por recurso y grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9c1cf-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="9c1cf-107">Las etiquetas se pueden colocar en un recurso en el momento de su creación, o bien se pueden agregar a un recurso existente.</span><span class="sxs-lookup"><span data-stu-id="9c1cf-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="9c1cf-108">Tenga en cuenta que las etiquetas solo son compatibles con los recursos creados mediante el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9c1cf-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="9c1cf-109">Etiquetado con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9c1cf-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="9c1cf-110">Para comenzar, [instale y configure la CLI de Azure](../../xplat-cli-azure-resource-manager.md) y asegúrese de que está en modo de Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="9c1cf-110">To begin, [install and configure the Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="9c1cf-111">Con este comando es posible ver todas las propiedades de una máquina virtual dada, incluidas las etiquetas:</span><span class="sxs-lookup"><span data-stu-id="9c1cf-111">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="9c1cf-112">Para agregar una nueva etiqueta de máquina virtual a través de la CLI de Azure, puede usar el comando `azure vm set` junto con el parámetro de etiqueta **-t**:</span><span class="sxs-lookup"><span data-stu-id="9c1cf-112">To add a new VM tag through the Azure CLI, you can use the `azure vm set` command along with the tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="9c1cf-113">Para quitar todas las etiquetas, puede usar el parámetro **-T** en el comando `azure vm set`.</span><span class="sxs-lookup"><span data-stu-id="9c1cf-113">To remove all tags, you can use the **–T** parameter in the `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="9c1cf-114">Ahora que hemos aplicado etiquetas a nuestros recursos a través de PowerShell, la CLI de Azure y el portal, analicemos los datos de uso para ver las etiquetas del portal de facturación.</span><span class="sxs-lookup"><span data-stu-id="9c1cf-114">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="9c1cf-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c1cf-115">Next steps</span></span>
* <span data-ttu-id="9c1cf-116">Para obtener más información sobre el etiquetado de los recursos de Azure, consulte [Información general de Azure Resource Manager][Azure Resource Manager Overview] y [Uso de etiquetas para organizar los recursos de Azure][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="9c1cf-116">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="9c1cf-117">Para ver cómo las etiquetas pueden ayudarle a administrar el uso de los recursos de Azure, consulte [Comprender la factura de Microsoft Azure][Understanding your Azure Bill] y [Obtención de información sobre el consumo de recursos de Microsoft Azure][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="9c1cf-117">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
