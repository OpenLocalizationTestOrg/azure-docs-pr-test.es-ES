---
title: "aaaHow tootag un recurso de máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información sobre cómo etiquetar una máquina virtual de Windows creada en Azure con el modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="942c7-103">¿Cómo tootag una máquina virtual de Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="942c7-103">How tootag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="942c7-104">Este artículo describen distintas formas tootag una máquina virtual de Windows en Azure a través del modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="942c7-104">This article describes different ways tootag a Windows virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="942c7-105">Las etiquetas son pares clave-valor definidos por el usuario que se pueden colocar directamente en un recurso o un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="942c7-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="942c7-106">Azure admite actualmente hasta etiquetas de too15 por cada recurso y el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="942c7-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="942c7-107">Etiquetas se pueden colocar en un recurso en tiempo de presentación de la creación o agregan tooan de recurso existente.</span><span class="sxs-lookup"><span data-stu-id="942c7-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="942c7-108">Tenga en cuenta que los recursos creados a través del modelo de implementación de administrador de recursos de hello solo se admiten etiquetas.</span><span class="sxs-lookup"><span data-stu-id="942c7-108">Please note that tags are supported for resources created via hello Resource Manager deployment model only.</span></span> <span data-ttu-id="942c7-109">Si desea tootag una máquina virtual Linux, consulte [cómo tootag una máquina virtual de Linux en Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="942c7-109">If you want tootag a Linux virtual machine, see [How tootag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="942c7-110">Etiquetado con PowerShell</span><span class="sxs-lookup"><span data-stu-id="942c7-110">Tagging with PowerShell</span></span>
<span data-ttu-id="942c7-111">toocreate, agregar y eliminar etiquetas a través de PowerShell, primero debe tooset seguridad su [entorno de PowerShell con el Administrador de recursos de Azure][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="942c7-111">toocreate, add, and delete tags through PowerShell, you first need tooset up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="942c7-112">Una vez haya completado el programa de instalación de hello, puede colocar etiquetas en los recursos de proceso, red y almacenamiento en la creación o después de crea el recurso de Hola a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="942c7-112">Once you have completed hello setup, you can place tags on Compute, Network, and Storage resources at creation or after hello resource is created via PowerShell.</span></span> <span data-ttu-id="942c7-113">En este artículo se centrará en la visualización y edición de etiquetas en máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="942c7-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="942c7-114">En primer lugar, navegue tooa Máquina Virtual a través de hello `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="942c7-114">First, navigate tooa Virtual Machine through hello `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="942c7-115">Si la máquina Virtual ya contiene etiquetas, a continuación, verá todas las etiquetas de hello en el recurso:</span><span class="sxs-lookup"><span data-stu-id="942c7-115">If your Virtual Machine already contains tags, you will then see all hello tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="942c7-116">Si desea que las etiquetas tooadd a través de PowerShell, puede usar hello `Set-AzureRmResource` comando.</span><span class="sxs-lookup"><span data-stu-id="942c7-116">If you would like tooadd tags through PowerShell, you can use hello `Set-AzureRmResource` command.</span></span> <span data-ttu-id="942c7-117">Tenga en cuenta que si actualiza las etiquetas a través de PowerShell, se actualizan todas ellas en conjunto.</span><span class="sxs-lookup"><span data-stu-id="942c7-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="942c7-118">Por lo que si va a agregar un recurso de tooa de etiqueta que ya tiene etiquetas, necesitará tooinclude todas las etiquetas de Hola que desee toobe colocado en el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="942c7-118">So if you are adding one tag tooa resource that already has tags, you will need tooinclude all hello tags that you want toobe placed on hello resource.</span></span> <span data-ttu-id="942c7-119">A continuación se muestra un ejemplo de cómo tooadd adicional etiquetas tooa recursos mediante Cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="942c7-119">Below is an example of how tooadd additional tags tooa resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="942c7-120">Este primer cmdlet establece todas etiquetas Hola colocadas en *MyTestVM* toohello *$tags* variable, con hello `Get-AzureRmResource` y `Tags` propiedad.</span><span class="sxs-lookup"><span data-stu-id="942c7-120">This first cmdlet sets all of hello tags placed on *MyTestVM* toohello *$tags* variable, using hello `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="942c7-121">Hola segundo comando muestra etiquetas de Hola para hello dada variable.</span><span class="sxs-lookup"><span data-stu-id="942c7-121">hello second command displays hello tags for hello given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="942c7-122">Hola tercer comando agrega una etiqueta adicional toohello *$tags* variable.</span><span class="sxs-lookup"><span data-stu-id="942c7-122">hello third command adds an additional tag toohello *$tags* variable.</span></span> <span data-ttu-id="942c7-123">Tenga en cuenta use Hola de hello  **+=**  tooappend Hola toohello de par clave/valor nuevo *$tags* lista.</span><span class="sxs-lookup"><span data-stu-id="942c7-123">Note hello use of hello **+=** tooappend hello new key/value pair toohello *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="942c7-124">comando cuarto Hola establece todas las etiquetas de hello definidas en Hola de *$tags* toohello variable tiene recursos.</span><span class="sxs-lookup"><span data-stu-id="942c7-124">hello fourth command sets all of hello tags defined in hello *$tags* variable toohello given resource.</span></span> <span data-ttu-id="942c7-125">En este caso, es MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="942c7-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="942c7-126">comando quinto Hello muestra todas las etiquetas de hello en recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="942c7-126">hello fifth command displays all of hello tags on hello resource.</span></span> <span data-ttu-id="942c7-127">Como puede ver, *ubicación* ahora está definida como una etiqueta con *MyLocation* como valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="942c7-127">As you can see, *Location* is now defined as a tag with *MyLocation* as hello value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="942c7-128">Obtenga más información sobre toolearn etiquetado a través de PowerShell, desproteger hello [Cmdlets de recurso de Azure][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="942c7-128">toolearn more about tagging through PowerShell, check out hello [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="942c7-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="942c7-129">Next steps</span></span>
* <span data-ttu-id="942c7-130">toolearn más información acerca de etiquetado de los recursos de Azure, consulte [Azure Resource Manager Overview] [ Azure Resource Manager Overview] y [tooorganize etiquetas utilizando los recursos de Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="942c7-130">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="942c7-131">toosee cómo etiquetas pueden ayudar a administrar el uso de recursos de Azure, consulte [descripción de la factura de Azure] [ Understanding your Azure Bill] y [obtener información sobre el consumo de recursos de Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="942c7-131">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
