---
title: un disco duro virtual en Azure de Debian Linux aaaPrepare | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate Debian 7 & VHD 8 archivos para su implementación en Azure."
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
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="60fac-103">Preparar VHD en Debian de Azure</span><span class="sxs-lookup"><span data-stu-id="60fac-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="60fac-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="60fac-104">Prerequisites</span></span>
<span data-ttu-id="60fac-105">En esta sección se da por supuesto que ya ha instalado un sistema operativo Linux Debian desde un archivo .iso descargado de hello [sitio Web Debian](https://www.debian.org/distrib/) tooa disco duro.</span><span class="sxs-lookup"><span data-stu-id="60fac-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="60fac-106">Varias herramientas existen archivos .vhd de toocreate; Hyper-V es sólo un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="60fac-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="60fac-107">Para obtener instrucciones con Hyper-V, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="60fac-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="60fac-108">Notas de instalación</span><span class="sxs-lookup"><span data-stu-id="60fac-108">Installation notes</span></span>
* <span data-ttu-id="60fac-109">Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.</span><span class="sxs-lookup"><span data-stu-id="60fac-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="60fac-110">no se admite el formato VHDX más reciente de Hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="60fac-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="60fac-111">Puede convertir el formato de tooVHD de disco hello mediante el Administrador de Hyper-V o hello **convert-vhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60fac-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="60fac-112">Al instalar el sistema de Linux Hola se recomienda que utilice particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones).</span><span class="sxs-lookup"><span data-stu-id="60fac-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="60fac-113">Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita toobe adjuntada tooanother VM para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="60fac-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="60fac-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.</span><span class="sxs-lookup"><span data-stu-id="60fac-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="60fac-115">No configure una partición de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="60fac-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="60fac-116">agente de Linux de Azure de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.</span><span class="sxs-lookup"><span data-stu-id="60fac-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="60fac-117">Para obtener más información acerca de este puede encontrarse en pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="60fac-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="60fac-118">Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="60fac-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="60fac-119">Use Administración de Azure toocreate Debian discos duros virtuales</span><span class="sxs-lookup"><span data-stu-id="60fac-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="60fac-120">Hay herramientas disponibles para generar Debian discos duros virtuales de Azure, por ejemplo, hello [azure-administrar](https://github.com/credativ/azure-manage) secuencias de comandos de [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="60fac-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="60fac-121">Se trata de hello recomendada enfoque frente a crear una imagen desde el principio.</span><span class="sxs-lookup"><span data-stu-id="60fac-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="60fac-122">Por ejemplo, toocreate un VHD de 8 Debian ejecutar Hola seguir comandos de administración de azure toodownload (y las dependencias) y ejecutar secuencias de comandos de hello azure_build_image:</span><span class="sxs-lookup"><span data-stu-id="60fac-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="60fac-123">Preparación manual de un VHD Debian</span><span class="sxs-lookup"><span data-stu-id="60fac-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="60fac-124">En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="60fac-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="60fac-125">Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="60fac-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="60fac-126">Comentario de línea de Hola para **deb CD-ROM** en `/etc/apt/source.list` si configuras Hola VM contra un archivo ISO.</span><span class="sxs-lookup"><span data-stu-id="60fac-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="60fac-127">Editar hello `/etc/default/grub` archivo y modifique hello **GRUB_CMDLINE_LINUX** parámetro manera parámetros adicionales del núcleo de tooinclude de Azure.</span><span class="sxs-lookup"><span data-stu-id="60fac-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="60fac-128">Vuelva a grub hello y ejecute:</span><span class="sxs-lookup"><span data-stu-id="60fac-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="60fac-129">Agregue repositorios Azure too/etc/apt/sources.list de Debian para Debian 7 u 8:</span><span class="sxs-lookup"><span data-stu-id="60fac-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="60fac-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="60fac-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="60fac-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="60fac-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="60fac-132">Instalar Hola agente Linux de Azure:</span><span class="sxs-lookup"><span data-stu-id="60fac-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="60fac-133">Debian 7, resulta kernel de 3.16-based Hola de toorun necesario del repositorio de wheezy backports Hola.</span><span class="sxs-lookup"><span data-stu-id="60fac-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="60fac-134">En primer lugar, cree un archivo denominado /etc/apt/preferences.d/linux.pref con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="60fac-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="60fac-135">A continuación, ejecute "sudo apt-get instalar linux-image-amd64" tooinstall Hola nueva núcleo.</span><span class="sxs-lookup"><span data-stu-id="60fac-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="60fac-136">Cancelar el aprovisionamiento de máquina virtual de Hola y prepararlo para el aprovisionamiento en Azure y ejecute:</span><span class="sxs-lookup"><span data-stu-id="60fac-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="60fac-137">Haga clic en **Acción** -> Apagar en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="60fac-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="60fac-138">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="60fac-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60fac-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60fac-139">Next steps</span></span>
<span data-ttu-id="60fac-140">Se está ahora listo toouse sus disco duro Debian toocreate nuevas máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="60fac-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="60fac-141">Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60fac-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

