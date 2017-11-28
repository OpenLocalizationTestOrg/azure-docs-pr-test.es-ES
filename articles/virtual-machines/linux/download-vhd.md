---
title: aaaDownload un VHD de Linux de Azure | Documentos de Microsoft
description: Descargar un VHD de Linux con hello Azure CLI y Hola portal de Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="22aec-103">Descarga de un VHD de Linux desde Azure</span><span class="sxs-lookup"><span data-stu-id="22aec-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="22aec-104">En este artículo, aprenderá cómo toodownload una [disco duro virtual (VHD) de Linux](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Hola de archivo de Azure mediante Azure CLI y portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="22aec-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="22aec-105">Máquinas virtuales (VM) en uso Azure [discos](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) como un toostore lugar un sistema operativo, aplicaciones y datos.</span><span class="sxs-lookup"><span data-stu-id="22aec-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="22aec-106">Todas las máquinas virtuales de Azure tienen al menos dos discos: un disco de sistema operativo Windows y un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="22aec-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="22aec-107">disco del sistema operativo Hola se crea inicialmente desde una imagen, y el disco del sistema operativo de Hola y de imagen de Hola son discos duros virtuales almacenados en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="22aec-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="22aec-108">Las máquinas virtuales también pueden tener uno o más discos de datos que también se almacenan en discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="22aec-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="22aec-109">Si aún no lo ha hecho, instale la [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="22aec-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="22aec-110">Detener Hola VM</span><span class="sxs-lookup"><span data-stu-id="22aec-110">Stop hello VM</span></span>

<span data-ttu-id="22aec-111">No se puede descargar un disco duro virtual de Azure si se adjunta tooa ejecutando la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22aec-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="22aec-112">Debe toodownload VM de hello toostop un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="22aec-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="22aec-113">Si desea toouse un VHD como un [imagen](tutorial-custom-images.md) toocreate otras máquinas virtuales con discos nuevos, necesita toodeprovision y generalizar el sistema de operativo Hola contenido en hello de archivos y detener Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22aec-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="22aec-114">Hola toouse VHD como un disco para una nueva instancia de una máquina virtual existente o un disco de datos, solo necesita toostop y cancelar la asignación de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22aec-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="22aec-115">toouse Hola VHD como una imagen toocreate otras máquinas virtuales, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="22aec-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="22aec-116">Utilizar SSH, nombre de la cuenta de hello y dirección IP pública de Hola de hello VM tooconnect tooit y Cancelar.</span><span class="sxs-lookup"><span data-stu-id="22aec-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="22aec-117">Hola + usuario parámetro también elimina la última cuenta de usuario aprovisionado Hola.</span><span class="sxs-lookup"><span data-stu-id="22aec-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="22aec-118">Si se conversión credenciales de la cuenta en toohello VM, deje esta + parámetro de usuario.</span><span class="sxs-lookup"><span data-stu-id="22aec-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="22aec-119">Hello en el ejemplo siguiente se quita Hola último usuario aprovisionado cuenta:</span><span class="sxs-lookup"><span data-stu-id="22aec-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="22aec-120">Inicie sesión en tooyour Azure cuenta con [inicio de sesión de az](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="22aec-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="22aec-121">Detener y cancelar la asignación Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22aec-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="22aec-122">Generalice Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22aec-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="22aec-123">Hola toouse VHD como un disco para una nueva instancia de una máquina virtual existente o un disco de datos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="22aec-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="22aec-124">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="22aec-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="22aec-125">En el menú del concentrador hello, haga clic en **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="22aec-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="22aec-126">Seleccione Hola VM de hello lista.</span><span class="sxs-lookup"><span data-stu-id="22aec-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="22aec-127">En la hoja de Hola para hello VM, haga clic en **detener**.</span><span class="sxs-lookup"><span data-stu-id="22aec-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![Detención de la máquina virtual](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="22aec-129">Generación de dirección URL de SAS</span><span class="sxs-lookup"><span data-stu-id="22aec-129">Generate SAS URL</span></span>

<span data-ttu-id="22aec-130">archivo de disco duro virtual de hello toodownload, deberá toogenerate un [firma de acceso compartido (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dirección URL.</span><span class="sxs-lookup"><span data-stu-id="22aec-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="22aec-131">Cuando se genera la dirección URL de hello, una fecha de caducidad se asigna toohello URL.</span><span class="sxs-lookup"><span data-stu-id="22aec-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="22aec-132">En el menú de Hola de hoja de Hola para hello VM, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="22aec-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="22aec-133">Seleccionar disco de sistema operativo de Hola para hello VM y, a continuación, haga clic en **exportar**.</span><span class="sxs-lookup"><span data-stu-id="22aec-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="22aec-134">Haga clic en **Generar dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="22aec-134">Click **Generate URL**.</span></span>

    ![Generar dirección URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="22aec-136">Descargar VHD</span><span class="sxs-lookup"><span data-stu-id="22aec-136">Download VHD</span></span>

1.  <span data-ttu-id="22aec-137">En dirección URL de Hola que generó, haga clic en archivo de disco duro virtual de hello de descarga.</span><span class="sxs-lookup"><span data-stu-id="22aec-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Descargar VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="22aec-139">Puede que necesite tooclick **guardar** en descarga de hello explorador toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="22aec-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="22aec-140">nombre predeterminado de Hello para el archivo de disco duro virtual de hello es *abcd*.</span><span class="sxs-lookup"><span data-stu-id="22aec-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Haga clic en Guardar en el Explorador de Hola](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="22aec-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="22aec-142">Next steps</span></span>

- <span data-ttu-id="22aec-143">Obtenga información acerca de cómo demasiado[cargar y crear una VM Linux desde disco personalizado con hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22aec-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="22aec-144">[Administrar discos Azure hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22aec-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

