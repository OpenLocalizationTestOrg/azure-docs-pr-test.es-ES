---
title: Descargar un VHD desde Azure | Microsoft Docs
description: Descargue un VHD de Windows mediante Azure Portal.
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
ms.openlocfilehash: d8bf89a4b7c2a158302f9ba09a182a3d8d062adc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="d732f-103">Descargar un VHD de Windows desde Azure</span><span class="sxs-lookup"><span data-stu-id="d732f-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="d732f-104">En este artículo aprenderá a descargar un archivo de [disco duro virtual (VHD) de Windows](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) desde Azure mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d732f-104">In this article, you learn how to download a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using the Azure portal.</span></span> 

<span data-ttu-id="d732f-105">Las máquinas virtuales (VM) de Azure usan los [discos](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como la ubicación en la que almacenar un sistema operativo, aplicaciones y datos.</span><span class="sxs-lookup"><span data-stu-id="d732f-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="d732f-106">Todas las máquinas virtuales de Azure tienen al menos dos discos: un disco de sistema operativo Windows y un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="d732f-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="d732f-107">El disco de sistema operativo se crea inicialmente a partir de una imagen, y tanto el disco de sistema operativo como la imagen son VHD almacenados en una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d732f-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="d732f-108">Las máquinas virtuales también pueden tener uno o más discos de datos que también se almacenan en discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="d732f-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="d732f-109">Parada de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d732f-109">Stop the VM</span></span>

<span data-ttu-id="d732f-110">No se puede descargar un VHD desde Azure si está conectado a una máquina virtual en ejecución.</span><span class="sxs-lookup"><span data-stu-id="d732f-110">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="d732f-111">Debe detener la máquina virtual para descargar un VHD.</span><span class="sxs-lookup"><span data-stu-id="d732f-111">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="d732f-112">Si quiere usar un VHD como [imagen](tutorial-custom-images.md) para crear otras máquinas virtuales con discos nuevos, use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) para generalizar el sistema operativo incluido en el archivo y luego detenga la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d732f-112">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) to generalize the operating system contained in the file and then stop the VM.</span></span> <span data-ttu-id="d732f-113">Para usar el VHD como disco para una nueva instancia de una máquina virtual o un disco de datos existente, basta con detener y cancelar la asignación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d732f-113">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="d732f-114">Para usar el VHD como imagen para crear otras máquinas virtuales, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d732f-114">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="d732f-115">Si aún no lo ha hecho, inicie sesión en el [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d732f-115">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="d732f-116">[Conecte a la máquina virtual](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d732f-116">[Connect to the VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="d732f-117">En la máquina virtual, abra la ventana del símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="d732f-117">On the VM, open the Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="d732f-118">Cambie el directorio a *%windir%\system32\sysprep* y ejecute sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="d732f-118">Change the directory to *%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="d732f-119">En el cuadro de diálogo Herramienta de preparación del sistema, seleccione **Iniciar la configuración rápida (OOBE) del sistema** y asegúrese de que **Generalizar** está activado.</span><span class="sxs-lookup"><span data-stu-id="d732f-119">In the System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="d732f-120">En Opciones de apagado, seleccione **Apagar** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d732f-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="d732f-121">Para usar el VHD como disco para una nueva instancia de una máquina virtual o un disco de datos existente, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d732f-121">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="d732f-122">En el menú Concentrador de Azure Portal, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="d732f-122">On the Hub menu in the Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="d732f-123">Seleccione la máquina virtual en la lista.</span><span class="sxs-lookup"><span data-stu-id="d732f-123">Select the VM from the list.</span></span>
3.  <span data-ttu-id="d732f-124">En la hoja de la máquina virtual, haga clic en **Detener**.</span><span class="sxs-lookup"><span data-stu-id="d732f-124">On the blade for the VM, click **Stop**.</span></span>

    ![Detención de la máquina virtual](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="d732f-126">Generación de dirección URL de SAS</span><span class="sxs-lookup"><span data-stu-id="d732f-126">Generate SAS URL</span></span>

<span data-ttu-id="d732f-127">Para descargar el archivo de VHD, debe generar una dirección URL de [firma de acceso compartido (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d732f-127">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="d732f-128">Una vez generada la dirección URL, se asigna un tiempo de expiración a la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="d732f-128">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="d732f-129">En el menú de la hoja de la máquina virtual, haga clic en **Discos**.</span><span class="sxs-lookup"><span data-stu-id="d732f-129">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="d732f-130">Seleccione el disco de sistema operativo de la máquina virtual y luego haga clic en **Exportar**.</span><span class="sxs-lookup"><span data-stu-id="d732f-130">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="d732f-131">Establezca el tiempo de expiración de la dirección URL en *36000*.</span><span class="sxs-lookup"><span data-stu-id="d732f-131">Set the expiration time of the URL to *36000*.</span></span>
4.  <span data-ttu-id="d732f-132">Haga clic en **Generar dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="d732f-132">Click **Generate URL**.</span></span>

    ![Generar dirección URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="d732f-134">El tiempo de expiración se aumenta con respecto al valor predeterminado para proporcionar tiempo suficiente para descargar el archivo de VHD grande de un sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d732f-134">The expiration time is increased from the default to provide enough time to download the large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="d732f-135">Es de esperar que un archivo de VHD que contenga el sistema operativo Windows Server tarde varias horas en descargarse según la conexión.</span><span class="sxs-lookup"><span data-stu-id="d732f-135">You can expect a VHD file that contains the Windows Server operating system to take several hours to download depending on your connection.</span></span> <span data-ttu-id="d732f-136">Si va a descargar un VHD de un disco de datos, el tiempo predeterminado es suficiente.</span><span class="sxs-lookup"><span data-stu-id="d732f-136">If you are downloading a VHD for a data disk, the default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="d732f-137">Descargar VHD</span><span class="sxs-lookup"><span data-stu-id="d732f-137">Download VHD</span></span>

1.  <span data-ttu-id="d732f-138">En la dirección URL generada, haga clic en Descargar el archivo VHD.</span><span class="sxs-lookup"><span data-stu-id="d732f-138">Under the URL that was generated, click Download the VHD file.</span></span>

    ![Descarga de VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="d732f-140">Es posible que tenga que hacer clic en **Guardar** en el explorador para iniciar la descarga.</span><span class="sxs-lookup"><span data-stu-id="d732f-140">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="d732f-141">El nombre predeterminado del archivo de VHD es *abcd*.</span><span class="sxs-lookup"><span data-stu-id="d732f-141">The default name for the VHD file is *abcd*.</span></span>

    ![Haga clic en Guardar en el explorador](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="d732f-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d732f-143">Next steps</span></span>

- <span data-ttu-id="d732f-144">Más información sobre cómo [cargar un archivo de VHD en Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d732f-144">Learn how to [upload a VHD file to Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="d732f-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Creación de discos administrados a partir de discos no administrados en una cuenta de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="d732f-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="d732f-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Administrar discos de Azure con PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d732f-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

