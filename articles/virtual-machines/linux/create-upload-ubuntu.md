---
title: aaaCreate y cargar un VHD de Ubuntu Linux en Azure
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contiene un sistema de operativo Ubuntu Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="0ff7d-103">Preparación de una máquina virtual Ubuntu para Azure</span><span class="sxs-lookup"><span data-stu-id="0ff7d-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="0ff7d-104">Imágenes oficiales de Ubuntu Cloud</span><span class="sxs-lookup"><span data-stu-id="0ff7d-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="0ff7d-105">Ahora Ubuntu publica VHD de Azure oficiales que se pueden descargar en [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="0ff7d-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="0ff7d-106">Si se necesita toobuild su propia imagen Ubuntu especializada para Azure, en lugar de usa el procedimiento manual de Hola por debajo de él toostart recomendada con estas conocidas trabajando discos duros virtuales y personalizar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="0ff7d-107">las versiones más recientes de imagen Hola siempre pueden encontrarse en hello ubicaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="0ff7d-108">Ubuntu 12.04/precisa: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="0ff7d-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="0ff7d-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="0ff7d-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="0ff7d-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="0ff7d-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ff7d-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0ff7d-111">Prerequisites</span></span>
<span data-ttu-id="0ff7d-112">En este artículo se da por supuesto que ya ha instalado un disco de duro virtual y tooa con sistema operativo Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="0ff7d-113">Varias herramientas existen archivos .vhd de toocreate, por ejemplo, una solución de virtualización como Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="0ff7d-114">Para obtener instrucciones, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ff7d-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="0ff7d-115">**Notas de instalación de Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="0ff7d-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="0ff7d-116">Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="0ff7d-117">no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="0ff7d-118">Puede convertir Hola disco tooVHD formato con el Administrador de Hyper-V u Hola cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="0ff7d-119">Al instalar el sistema de Linux Hola se recomienda que utilice particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones).</span><span class="sxs-lookup"><span data-stu-id="0ff7d-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="0ff7d-120">Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita toobe adjuntada tooanother VM para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="0ff7d-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="0ff7d-122">No configure una partición de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="0ff7d-123">agente de Linux de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="0ff7d-124">Para obtener más información acerca de este puede encontrarse en pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="0ff7d-125">Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="0ff7d-126">Pasos manuales</span><span class="sxs-lookup"><span data-stu-id="0ff7d-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="0ff7d-127">Antes de intentar toocreate su propia imagen de Ubuntu personalizada para Azure, considere la posibilidad de usando Hola pregeneradas y probar imágenes de [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="0ff7d-128">En el panel central de hello del Administrador de Hyper-V, seleccione máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="0ff7d-129">Haga clic en **conectar** tooopen ventana de hello para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="0ff7d-130">Reemplace repositorios actual de hello en repositorios de hello imagen toouse Ubuntu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="0ff7d-131">pasos de Hello varían ligeramente según la versión de Hola Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="0ff7d-132">Antes de editar `/etc/apt/sources.list`, es recomendable toomake una copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="0ff7d-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="0ff7d-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="0ff7d-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="0ff7d-136">Hello imágenes Ubuntu Azure están ahora siguiendo hello *habilitación de hardware* kernel (HWE).</span><span class="sxs-lookup"><span data-stu-id="0ff7d-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="0ff7d-137">Actualizar kernel más reciente de toohello de sistema operativo de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="0ff7d-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="0ff7d-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="0ff7d-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="0ff7d-141">**Consulte también:**</span><span class="sxs-lookup"><span data-stu-id="0ff7d-141">**See also:**</span></span>
    - [<span data-ttu-id="0ff7d-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="0ff7d-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="0ff7d-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="0ff7d-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="0ff7d-144">Modificar línea de arranque de kernel de Hola para los parámetros adicionales del núcleo de Grub tooinclude de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="0ff7d-145">toodo abrir este `/etc/default/grub` en un editor de texto, busque variable Hola denominada `GRUB_CMDLINE_LINUX_DEFAULT` (o agregarlo si es necesario) y editarlo hello tooinclude parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="0ff7d-146">Guarde este archivo y ciérrelo, y ejecute `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="0ff7d-147">Esto garantizará que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a obtener soporte técnico Azure con problemas de depuración.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="0ff7d-148">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="0ff7d-149">Esto suele ser el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-149">This is usually hello default.</span></span>

7. <span data-ttu-id="0ff7d-150">Instalar Hola agente Linux de Azure:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="0ff7d-151">Hola `walinuxagent` paquete puede quitar hello `NetworkManager` y `NetworkManager-gnome` paquetes y, si están instalados.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="0ff7d-152">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="0ff7d-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="0ff7d-153">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="0ff7d-154">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ff7d-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ff7d-155">Next steps</span></span>
<span data-ttu-id="0ff7d-156">Se está ahora listo toouse sus Ubuntu Linux disco duro virtual toocreate nuevas máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff7d-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="0ff7d-157">Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0ff7d-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="0ff7d-158">Referencias</span><span class="sxs-lookup"><span data-stu-id="0ff7d-158">References</span></span>
<span data-ttu-id="0ff7d-159">Kernel de habilitación de hardware (HWE) de Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0ff7d-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="0ff7d-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="0ff7d-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="0ff7d-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="0ff7d-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

