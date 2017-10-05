---
title: Preparar un VHD de Debian Linux en Azure | Microsoft Docs
description: Aprenda a crear archivos de VHD en Debian 7 y 8 para implementarlos en Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 63970d162c12984d6476bf0b9fc4ab70160eccdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="1f03b-103">Preparar VHD en Debian de Azure</span><span class="sxs-lookup"><span data-stu-id="1f03b-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="1f03b-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1f03b-104">Prerequisites</span></span>
<span data-ttu-id="1f03b-105">En esta sección, se supone que ya instaló en un sistema operativo Debian Linux desde un archivo .iso que obtuvo del [sitio web Debian](https://www.debian.org/distrib/) y que descargó a un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="1f03b-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from the [Debian website](https://www.debian.org/distrib/) to a virtual hard disk.</span></span> <span data-ttu-id="1f03b-106">Existen varias herramientas para crear archivos .vhd; Hyper-V es solo un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1f03b-106">Multiple tools exist to create .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="1f03b-107">Para obtener instrucciones acerca de cómo usar Hyper-V, consulte [Instalación del rol de Hyper-V y configuración de una máquina virtual](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f03b-107">For instructions using Hyper-V, see [Install the Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="1f03b-108">Notas de instalación</span><span class="sxs-lookup"><span data-stu-id="1f03b-108">Installation notes</span></span>
* <span data-ttu-id="1f03b-109">Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.</span><span class="sxs-lookup"><span data-stu-id="1f03b-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="1f03b-110">el reciente formato VHDX no se admite en Azure.</span><span class="sxs-lookup"><span data-stu-id="1f03b-110">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="1f03b-111">Puede convertir el disco al formato VHD con el Administrador de Hyper-V o el cmdlet **convert-vhd** .</span><span class="sxs-lookup"><span data-stu-id="1f03b-111">You can convert the disk to VHD format using Hyper-V Manager or the **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="1f03b-112">Al instalar el sistema Linux se recomienda utilizar las particiones estándar en lugar de un LVM (que a menudo viene de forma predeterminada en muchas instalaciones).</span><span class="sxs-lookup"><span data-stu-id="1f03b-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="1f03b-113">De este modo se impedirá que el nombre del LVM entre en conflicto con las máquinas virtuales clonadas, especialmente si en algún momento hace falta adjuntar un disco de SO a otra máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="1f03b-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="1f03b-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.</span><span class="sxs-lookup"><span data-stu-id="1f03b-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="1f03b-115">No cree una partición de intercambio en el disco del SO.</span><span class="sxs-lookup"><span data-stu-id="1f03b-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="1f03b-116">El agente de Linux de Azure se puede configurar para crear un archivo de intercambio en el disco de recursos temporal.</span><span class="sxs-lookup"><span data-stu-id="1f03b-116">The Azure Linux agent can be configured to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="1f03b-117">Puede encontrar más información al respecto en los pasos que vienen a continuación.</span><span class="sxs-lookup"><span data-stu-id="1f03b-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="1f03b-118">El tamaño de todos los archivos VHD debe ser múltiplo de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1f03b-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-to-create-debian-vhds"></a><span data-ttu-id="1f03b-119">Uso de Azure-Manage para crear VHD Debian</span><span class="sxs-lookup"><span data-stu-id="1f03b-119">Use Azure-Manage to create Debian VHDs</span></span>
<span data-ttu-id="1f03b-120">Hay herramientas disponibles para generar VHD Debian para Azure, como los scripts [azure-manage](https://github.com/credativ/azure-manage) de [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="1f03b-120">There are tools available for generating Debian VHDs for Azure, such as the [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="1f03b-121">Este es el enfoque recomendado, en lugar de crear una imagen desde el principio.</span><span class="sxs-lookup"><span data-stu-id="1f03b-121">This is the recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="1f03b-122">Por ejemplo, para crear un VHD Debian 8, ejecute los comandos siguientes para descargar azure-manage (y sus dependencias) y ejecute el script azure_build_image:</span><span class="sxs-lookup"><span data-stu-id="1f03b-122">For example, to create a Debian 8 VHD run the following commands to download azure-manage (and dependencies) and run the azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="1f03b-123">Preparación manual de un VHD Debian</span><span class="sxs-lookup"><span data-stu-id="1f03b-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="1f03b-124">En el Administrador de Hyper-V, seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f03b-124">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="1f03b-125">Haga clic en **Conectar** para abrir una ventana de consola de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f03b-125">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="1f03b-126">Comente la línea de **deb cdrom** en `/etc/apt/source.list` si configura la máquina virtual con un archivo ISO.</span><span class="sxs-lookup"><span data-stu-id="1f03b-126">Comment out the line for **deb cdrom** in `/etc/apt/source.list` if you set up the VM against an ISO file.</span></span>
4. <span data-ttu-id="1f03b-127">Edite el archivo `/etc/default/grub` y modifique el parámetro **GRUB_CMDLINE_LINUX** tal como se muestra a continuación para incluir parámetros de kernel adicionales de Azure.</span><span class="sxs-lookup"><span data-stu-id="1f03b-127">Edit the `/etc/default/grub` file and modify the **GRUB_CMDLINE_LINUX** parameter as follows to include additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="1f03b-128">Recompile el sistema GRUB y ejecute:</span><span class="sxs-lookup"><span data-stu-id="1f03b-128">Rebuild the grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="1f03b-129">Agregue repositorios de Azure de Debian a /etc/apt/sources.list (Debian 7 u 8):</span><span class="sxs-lookup"><span data-stu-id="1f03b-129">Add Debian's Azure repositories to /etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="1f03b-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="1f03b-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="1f03b-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="1f03b-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="1f03b-132">Instale el Agente de Linux de Azure:</span><span class="sxs-lookup"><span data-stu-id="1f03b-132">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="1f03b-133">En el caso de Debian 7, se requiere que se ejecute el kernel basado en 3.16 desde el repositorio wheezy-backports.</span><span class="sxs-lookup"><span data-stu-id="1f03b-133">For Debian 7, it is required to run the 3.16-based kernel from the wheezy-backports repository.</span></span> <span data-ttu-id="1f03b-134">En primer lugar, cree un archivo llamado /etc/apt/preferences.d/linux.pref con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="1f03b-134">First create a file called /etc/apt/preferences.d/linux.pref with the following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="1f03b-135">A continuación, ejecute "sudo apt-get install linux-image-amd64" para instalar el nuevo kernel.</span><span class="sxs-lookup"><span data-stu-id="1f03b-135">Then run "sudo apt-get install linux-image-amd64" to install the new kernel.</span></span>
3. <span data-ttu-id="1f03b-136">Desaprovisione la máquina virtual, prepárela para aprovisionarla en Azure y ejecute:</span><span class="sxs-lookup"><span data-stu-id="1f03b-136">Deprovision the virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="1f03b-137">Haga clic en **Acción** -> Apagar en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1f03b-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="1f03b-138">El VHD de Linux ya está listo para cargarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="1f03b-138">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f03b-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1f03b-139">Next steps</span></span>
<span data-ttu-id="1f03b-140">Ya está listo para usar el disco duro virtual de Debian para crear nuevas máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="1f03b-140">You're now ready to use your Debian virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="1f03b-141">Si es la primera vez que carga el archivo .vhd en Azure, consulte los pasos 2 y 3 de [Creación y carga de un disco duro virtual que contiene el sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f03b-141">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

