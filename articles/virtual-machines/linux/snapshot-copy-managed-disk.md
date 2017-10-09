---
title: aaaCopy un administrado de Azure en disco para copia de seguridad | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una copia de un toouse de disco administrado de Azure para volver arriba o hacia la solución de problemas de disco emite."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="6c005-103">Creación de una copia de un VHD almacenado como un disco administrado de Azure mediante instantáneas administradas</span><span class="sxs-lookup"><span data-stu-id="6c005-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="6c005-104">Crear una instantánea de un disco administrado para copia de seguridad o crear un disco administrado desde la instantánea de Hola y adjuntarlo tootroubleshoot de máquina virtual de prueba tooa.</span><span class="sxs-lookup"><span data-stu-id="6c005-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="6c005-105">Una instantánea administrada es una copia completa a partir de un momento específico de un disco administrado de VM.</span><span class="sxs-lookup"><span data-stu-id="6c005-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="6c005-106">Crea una copia de solo lectura del VHD y, de forma predeterminada, se almacena como un Disco administrado estándar.</span><span class="sxs-lookup"><span data-stu-id="6c005-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="6c005-107">Para información sobre los precios, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="6c005-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="6c005-108">Usar cualquier hello tootake de CLI de Azure 2.0 portal o hello Azure una instantánea de hello disco administrado.</span><span class="sxs-lookup"><span data-stu-id="6c005-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="6c005-109">Usar Azure CLI 2.0 tootake una instantánea</span><span class="sxs-lookup"><span data-stu-id="6c005-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="6c005-110">Hello en el ejemplo siguiente se requiere hello Azure CLI 2.0 instalado y registrado en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c005-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="6c005-111">Hello pasos siguientes muestran cómo tooobtain y tome una instantánea de un sistema operativo administrado disco mediante hello `az snapshot create` comando con hello `--source-disk` parámetro.</span><span class="sxs-lookup"><span data-stu-id="6c005-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="6c005-112">Hello en el ejemplo siguiente se supone que existe una máquina virtual denominada `myVM` creado con un disco de sistema operativo administrado de hello `myResourceGroup` grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6c005-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="6c005-113">salida de Hello debe ser similar:</span><span class="sxs-lookup"><span data-stu-id="6c005-113">hello output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="6c005-114">Usar tootake portal Azure una instantánea</span><span class="sxs-lookup"><span data-stu-id="6c005-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="6c005-115">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c005-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6c005-116">A partir de hello superior izquierda, haga clic en **New** y busque **instantánea**.</span><span class="sxs-lookup"><span data-stu-id="6c005-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="6c005-117">En la hoja de la instantánea de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="6c005-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="6c005-118">Escriba un **nombre** para instantáneas de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c005-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="6c005-119">Seleccione una existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) o nombre de tipo hello para uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="6c005-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="6c005-120">Seleccione una ubicación del centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c005-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="6c005-121">Para **el disco de origen**, seleccione Hola toosnapshot administrado por disco.</span><span class="sxs-lookup"><span data-stu-id="6c005-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="6c005-122">Seleccione hello **tipo de cuenta** instantánea de toouse toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="6c005-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="6c005-123">Se recomienda **Standard_LRS**, a menos que necesite almacenarla en un disco de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="6c005-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="6c005-124">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6c005-124">Click **Create**.</span></span>

<span data-ttu-id="6c005-125">Si piensa toouse Hola instantánea toocreate un disco administrado y adjuntar una máquina virtual que necesita toobe alto rendimiento, use el parámetro hello `--sku Premium_LRS` con hello `az snapshot create` comando.</span><span class="sxs-lookup"><span data-stu-id="6c005-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="6c005-126">Esto crea la instantánea de Hola para que se almacena como un disco de Premium administrados.</span><span class="sxs-lookup"><span data-stu-id="6c005-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="6c005-127">Los Managed Disks Premium tienen un rendimiento mayor porque son discos de estado sólido (SSD), pero cuestan más que los discos estándar (HDD).</span><span class="sxs-lookup"><span data-stu-id="6c005-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


