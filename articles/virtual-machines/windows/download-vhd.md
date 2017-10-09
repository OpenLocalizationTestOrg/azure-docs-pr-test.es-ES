---
title: aaaDownload un VHD de Windows de Azure | Documentos de Microsoft
description: Descargar un disco duro virtual de Windows con hello portal de Azure.
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="45dec-103">Descargar un VHD de Windows desde Azure</span><span class="sxs-lookup"><span data-stu-id="45dec-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="45dec-104">En este artículo, aprenderá cómo toodownload una [disco duro virtual (VHD) de Windows](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) archivo utilizasen Azure Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="45dec-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="45dec-105">Máquinas virtuales (VM) en uso Azure [discos](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como un toostore lugar un sistema operativo, aplicaciones y datos.</span><span class="sxs-lookup"><span data-stu-id="45dec-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="45dec-106">Todas las máquinas virtuales de Azure tienen al menos dos discos: un disco de sistema operativo Windows y un disco temporal.</span><span class="sxs-lookup"><span data-stu-id="45dec-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="45dec-107">disco del sistema operativo Hola se crea inicialmente desde una imagen, y el disco del sistema operativo de Hola y de imagen de Hola son discos duros virtuales almacenados en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="45dec-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="45dec-108">Las máquinas virtuales también pueden tener uno o más discos de datos que también se almacenan en discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="45dec-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="45dec-109">Detener Hola VM</span><span class="sxs-lookup"><span data-stu-id="45dec-109">Stop hello VM</span></span>

<span data-ttu-id="45dec-110">No se puede descargar un disco duro virtual de Azure si se adjunta tooa ejecutando la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="45dec-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="45dec-111">Debe toodownload VM de hello toostop un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="45dec-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="45dec-112">Si desea toouse un VHD como un [imagen](tutorial-custom-images.md) toocreate otras máquinas virtuales con discos nuevos, use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize Hola sistema operativo contenido en el archivo hello y, a continuación, detener Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="45dec-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="45dec-113">Hola toouse VHD como un disco para una nueva instancia de una máquina virtual existente o un disco de datos, solo necesita toostop y cancelar la asignación de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="45dec-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="45dec-114">toouse Hola VHD como una imagen toocreate otras máquinas virtuales, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="45dec-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="45dec-115">Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="45dec-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="45dec-116">[Conectar toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45dec-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="45dec-117">En hello VM, abra la ventana de símbolo de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="45dec-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="45dec-118">Cambie el directorio de hello demasiado*%windir%\system32\sysprep* y ejecute sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="45dec-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="45dec-119">En el cuadro de diálogo de la herramienta de preparación del sistema de hello, seleccione **sistema Out-of-Box experiencia inmediata (OOBE)**y asegúrese de que **generalizar** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="45dec-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="45dec-120">En Opciones de apagado, seleccione **Apagar** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="45dec-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="45dec-121">Hola toouse VHD como un disco para una nueva instancia de una máquina virtual existente o un disco de datos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="45dec-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="45dec-122">En el menú del concentrador Hola Hola portal de Azure, haga clic en **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="45dec-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="45dec-123">Seleccione Hola VM de hello lista.</span><span class="sxs-lookup"><span data-stu-id="45dec-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="45dec-124">En la hoja de Hola para hello VM, haga clic en **detener**.</span><span class="sxs-lookup"><span data-stu-id="45dec-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![Detención de la máquina virtual](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="45dec-126">Generación de dirección URL de SAS</span><span class="sxs-lookup"><span data-stu-id="45dec-126">Generate SAS URL</span></span>

<span data-ttu-id="45dec-127">archivo de disco duro virtual de hello toodownload, deberá toogenerate un [firma de acceso compartido (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dirección URL.</span><span class="sxs-lookup"><span data-stu-id="45dec-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="45dec-128">Cuando se genera la dirección URL de hello, una fecha de caducidad se asigna toohello URL.</span><span class="sxs-lookup"><span data-stu-id="45dec-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="45dec-129">En el menú de Hola de hoja de Hola para hello VM, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="45dec-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="45dec-130">Seleccionar disco de sistema operativo de Hola para hello VM y, a continuación, haga clic en **exportar**.</span><span class="sxs-lookup"><span data-stu-id="45dec-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="45dec-131">Establecer tiempo de expiración de Hola de dirección URL de hello demasiado*36000*.</span><span class="sxs-lookup"><span data-stu-id="45dec-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="45dec-132">Haga clic en **Generar dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="45dec-132">Click **Generate URL**.</span></span>

    ![Generar dirección URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="45dec-134">hora de expiración de Hello ha aumentado de hello predeterminado tooprovide suficiente tiempo toodownload Hola archivo VHD grande para un sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="45dec-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="45dec-135">Puede esperar a que un archivo de disco duro virtual que contenga tootake de sistema operativo de Windows Server de hello toodownload de varias horas dependiendo de la conexión.</span><span class="sxs-lookup"><span data-stu-id="45dec-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="45dec-136">Si va a descargar un disco duro virtual para un disco de datos, el tiempo predeterminado de hello es suficiente.</span><span class="sxs-lookup"><span data-stu-id="45dec-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="45dec-137">Descargar VHD</span><span class="sxs-lookup"><span data-stu-id="45dec-137">Download VHD</span></span>

1.  <span data-ttu-id="45dec-138">En dirección URL de Hola que generó, haga clic en archivo de disco duro virtual de hello de descarga.</span><span class="sxs-lookup"><span data-stu-id="45dec-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Descargar VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="45dec-140">Puede que necesite tooclick **guardar** en descarga de hello explorador toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="45dec-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="45dec-141">nombre predeterminado de Hello para el archivo de disco duro virtual de hello es *abcd*.</span><span class="sxs-lookup"><span data-stu-id="45dec-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Haga clic en Guardar en el Explorador de Hola](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="45dec-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45dec-143">Next steps</span></span>

- <span data-ttu-id="45dec-144">Obtenga información acerca de cómo demasiado[cargar un tooAzure del archivo de disco duro virtual](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45dec-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="45dec-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Creación de discos administrados a partir de discos no administrados en una cuenta de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="45dec-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="45dec-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Administrar discos de Azure con PowerShell).</span><span class="sxs-lookup"><span data-stu-id="45dec-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

