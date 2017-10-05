---
title: Descarga de un VHD de Linux desde Azure | Microsoft Docs
description: Descarga de un VHD de Linux mediante la CLI de Azure y Azure Portal.
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
ms.openlocfilehash: 3eb88478b43f8e3a36ae04bf3703f238e8cb1f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="1caa8-103">Descarga de un VHD de Linux desde Azure</span><span class="sxs-lookup"><span data-stu-id="1caa8-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="1caa8-104">En este artículo aprenderá a descargar un archivo de [disco duro virtual (VHD) de Linux](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) desde Azure mediante la CLI de Azure y Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1caa8-104">In this article, you learn how to download a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using the Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="1caa8-105">Las máquinas virtuales (VM) de Azure usan los [discos](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) como la ubicación en la que almacenar un sistema operativo, aplicaciones y datos.</span><span class="sxs-lookup"><span data-stu-id="1caa8-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="1caa8-106">Todas las máquinas virtuales de Azure tienen al menos dos discos: un disco de sistema operativo Windows y un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="1caa8-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="1caa8-107">El disco de sistema operativo se crea inicialmente a partir de una imagen, y tanto el disco de sistema operativo como la imagen son VHD almacenados en una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1caa8-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="1caa8-108">Las máquinas virtuales también pueden tener uno o más discos de datos que también se almacenan en discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="1caa8-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="1caa8-109">Si aún no lo ha hecho, instale la [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="1caa8-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="1caa8-110">Parada de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1caa8-110">Stop the VM</span></span>

<span data-ttu-id="1caa8-111">No se puede descargar un VHD desde Azure si está conectado a una máquina virtual en ejecución.</span><span class="sxs-lookup"><span data-stu-id="1caa8-111">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="1caa8-112">Debe detener la máquina virtual para descargar un VHD.</span><span class="sxs-lookup"><span data-stu-id="1caa8-112">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="1caa8-113">Si quiere usar un VHD como [imagen](tutorial-custom-images.md) para crear otras máquinas virtuales con discos nuevos, debe desaprovisionar y generalizar el sistema operativo incluido en el archivo y detener la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1caa8-113">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you need to deprovision and generalize the operating system contained in the file and stop the VM.</span></span> <span data-ttu-id="1caa8-114">Para usar el VHD como disco para una nueva instancia de una máquina virtual o un disco de datos existente, basta con detener y cancelar la asignación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1caa8-114">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="1caa8-115">Para usar el VHD como imagen para crear otras máquinas virtuales, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1caa8-115">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1. <span data-ttu-id="1caa8-116">Use SSH, el nombre de la cuenta y la dirección IP pública de la máquina virtual para conectarse a ella y desaprovisionarla.</span><span class="sxs-lookup"><span data-stu-id="1caa8-116">Use SSH, the account name, and the public IP address of the VM to connect to it and deprovision it.</span></span> <span data-ttu-id="1caa8-117">El parámetro +user también quita la última cuenta de usuario aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="1caa8-117">The +user parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="1caa8-118">Si está creando credenciales de cuenta en la máquina virtual, ignore este parámetro +user.</span><span class="sxs-lookup"><span data-stu-id="1caa8-118">If you are baking account credentials in to the VM, leave out this +user parameter.</span></span> <span data-ttu-id="1caa8-119">En el ejemplo siguiente se quita la última cuenta de usuario aprovisionada:</span><span class="sxs-lookup"><span data-stu-id="1caa8-119">The following example removes the last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="1caa8-120">Inicie sesión en su cuenta de Azure con [az login](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1caa8-120">Sign in to your Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="1caa8-121">Detenga y desasigne la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1caa8-121">Stop and deallocate the VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="1caa8-122">Generalice la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1caa8-122">Generalize the VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="1caa8-123">Para usar el VHD como disco para una nueva instancia de una máquina virtual o un disco de datos existente, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1caa8-123">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="1caa8-124">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1caa8-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="1caa8-125">En el menú del concentrador, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="1caa8-125">On the Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="1caa8-126">Seleccione la máquina virtual en la lista.</span><span class="sxs-lookup"><span data-stu-id="1caa8-126">Select the VM from the list.</span></span>
4.  <span data-ttu-id="1caa8-127">En la hoja de la máquina virtual, haga clic en **Detener**.</span><span class="sxs-lookup"><span data-stu-id="1caa8-127">On the blade for the VM, click **Stop**.</span></span>

    ![Detención de la máquina virtual](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="1caa8-129">Generación de dirección URL de SAS</span><span class="sxs-lookup"><span data-stu-id="1caa8-129">Generate SAS URL</span></span>

<span data-ttu-id="1caa8-130">Para descargar el archivo de VHD, debe generar una dirección URL de [firma de acceso compartido (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1caa8-130">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="1caa8-131">Una vez generada la dirección URL, se asigna un tiempo de expiración a la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="1caa8-131">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="1caa8-132">En el menú de la hoja de la máquina virtual, haga clic en **Discos**.</span><span class="sxs-lookup"><span data-stu-id="1caa8-132">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="1caa8-133">Seleccione el disco de sistema operativo de la máquina virtual y luego haga clic en **Exportar**.</span><span class="sxs-lookup"><span data-stu-id="1caa8-133">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="1caa8-134">Haga clic en **Generar dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="1caa8-134">Click **Generate URL**.</span></span>

    ![Generar dirección URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="1caa8-136">Descarga de VHD</span><span class="sxs-lookup"><span data-stu-id="1caa8-136">Download VHD</span></span>

1.  <span data-ttu-id="1caa8-137">En la dirección URL generada, haga clic en Descargar el archivo VHD.</span><span class="sxs-lookup"><span data-stu-id="1caa8-137">Under the URL that was generated, click Download the VHD file.</span></span>

    ![Descarga de VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="1caa8-139">Es posible que tenga que hacer clic en **Guardar** en el explorador para iniciar la descarga.</span><span class="sxs-lookup"><span data-stu-id="1caa8-139">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="1caa8-140">El nombre predeterminado del archivo de VHD es *abcd*.</span><span class="sxs-lookup"><span data-stu-id="1caa8-140">The default name for the VHD file is *abcd*.</span></span>

    ![Haga clic en Guardar en el explorador](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="1caa8-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1caa8-142">Next steps</span></span>

- <span data-ttu-id="1caa8-143">Obtenga información sobre cómo [cargar y crear una máquina virtual Linux a partir de un disco personalizado mediante la CLI de Azure 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1caa8-143">Learn how to [upload and create a Linux VM from custom disk with the Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="1caa8-144">[Administración de discos de Azure con la CLI de Azure](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1caa8-144">[Manage Azure disks the Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

