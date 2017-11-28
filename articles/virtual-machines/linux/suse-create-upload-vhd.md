---
title: "Creación y carga de un VHD de SUSE Linux en Azure"
description: Aprenda a crear y cargar un disco duro virtual de Azure (VHD) que contiene un sistema operativo SUSE Linux.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: c829f5d9a90b4260c6f41b2d9e511a0c6cb48f18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="e48c8-103">Preparación de una máquina virtual SLES u openSUSE para Azure</span><span class="sxs-lookup"><span data-stu-id="e48c8-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="e48c8-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e48c8-104">Prerequisites</span></span>
<span data-ttu-id="e48c8-105">En este artículo se supone que ya ha instalado un sistema operativo Linux SUSE u openSUSE en un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="e48c8-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="e48c8-106">Existen varias herramientas para crear archivos .vhd; por ejemplo, una solución de virtualización como Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e48c8-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="e48c8-107">Para obtener instrucciones, consulte [Instalación del rol de Hyper-V y configuración de una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="e48c8-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="e48c8-108">Notas sobre la instalación de SLES/openSUSE</span><span class="sxs-lookup"><span data-stu-id="e48c8-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="e48c8-109">Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="e48c8-110">El formato VHDX no se admite en Azure, solo el **VHD fijo**.</span><span class="sxs-lookup"><span data-stu-id="e48c8-110">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="e48c8-111">Puede convertir el disco al formato VHD con el Administrador de Hyper-V o el cmdlet Convert-VHD.</span><span class="sxs-lookup"><span data-stu-id="e48c8-111">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="e48c8-112">Al instalar el sistema Linux se recomienda utilizar las particiones estándar en lugar de un LVM (que a menudo viene de forma predeterminada en muchas instalaciones).</span><span class="sxs-lookup"><span data-stu-id="e48c8-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="e48c8-113">De este modo se impedirá que el nombre del LVM entre en conflicto con las máquinas virtuales clonadas, especialmente si en algún momento hace falta adjuntar un disco de SO a otra máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="e48c8-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="e48c8-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.</span><span class="sxs-lookup"><span data-stu-id="e48c8-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="e48c8-115">No cree una partición de intercambio en el disco del SO.</span><span class="sxs-lookup"><span data-stu-id="e48c8-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="e48c8-116">El agente de Linux se puede configurar para crear un archivo de intercambio en el disco de recursos temporal.</span><span class="sxs-lookup"><span data-stu-id="e48c8-116">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="e48c8-117">Puede encontrar más información al respecto en los pasos que vienen a continuación.</span><span class="sxs-lookup"><span data-stu-id="e48c8-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="e48c8-118">El tamaño de todos los archivos VHD debe ser múltiplo de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e48c8-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="e48c8-119">Uso de SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="e48c8-119">Use SUSE Studio</span></span>
<span data-ttu-id="e48c8-120">[SUSE Studio](http://www.susestudio.com) puede crear y administrar fácilmente sus imágenes de SLES y openSUSE para Hyper-V y Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="e48c8-121">Este es el enfoque recomendado para personalizar sus propias imágenes SLES y openSUSE.</span><span class="sxs-lookup"><span data-stu-id="e48c8-121">This is the recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="e48c8-122">Como alternativa a la creación de su propio VHD, SUSE también publica imágenes de BYOS ("traiga su propia suscripción") para SLES en [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="e48c8-122">As an alternative to building your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="e48c8-123">Preparación de SUSE Linux Enterprise Server 11 SP4</span><span class="sxs-lookup"><span data-stu-id="e48c8-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="e48c8-124">Seleccione la máquina virtual en el panel central del Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e48c8-124">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="e48c8-125">Haga clic en **Conectar** para abrir la ventana de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e48c8-125">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="e48c8-126">Registre el sistema de SUSE Linux Enterprise para permitir que descargue actualizaciones e instale paquetes.</span><span class="sxs-lookup"><span data-stu-id="e48c8-126">Register your SUSE Linux Enterprise system to allow it to download updates and install packages.</span></span>
4. <span data-ttu-id="e48c8-127">Actualice el sistema con las revisiones más recientes:</span><span class="sxs-lookup"><span data-stu-id="e48c8-127">Update the system with the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="e48c8-128">Instale el Agente de Linux de Azure desde el repositorio SLES:</span><span class="sxs-lookup"><span data-stu-id="e48c8-128">Install the Azure Linux Agent from the SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="e48c8-129">Compruebe si waagent está establecido en "on" en chkconfig y, en caso contrario, puede habilitarlo para que se inicie automáticamente:</span><span class="sxs-lookup"><span data-stu-id="e48c8-129">Check if waagent is set to "on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="e48c8-130">Compruebe si el servicio waagent se está ejecutando y, en caso contrario, inícielo:</span><span class="sxs-lookup"><span data-stu-id="e48c8-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="e48c8-131">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-131">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="e48c8-132">Para ello, abra "/boot/grub/menu.lst" en un editor de texto y asegúrese de que el kernel predeterminado incluye los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="e48c8-132">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="e48c8-133">Así se asegurará de que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="e48c8-133">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="e48c8-134">Confirme que tanto /boot/grub/menu.lst como /etc/fstab hacen referencia a su UUID (by-uuid) en lugar de al identificador del disco (by-id).</span><span class="sxs-lookup"><span data-stu-id="e48c8-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference the disk using its UUID (by-uuid) instead of the disk ID (by-id).</span></span> 
   
    <span data-ttu-id="e48c8-135">Obtención del UUID del disco</span><span class="sxs-lookup"><span data-stu-id="e48c8-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="e48c8-136">Si se usa /dev/disk/by-id/, actualice /boot/grub/menu.lst y /etc/fstab con el valor by-uuid adecuado.</span><span class="sxs-lookup"><span data-stu-id="e48c8-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with the proper by-uuid value</span></span>
   
    <span data-ttu-id="e48c8-137">Antes del cambio</span><span class="sxs-lookup"><span data-stu-id="e48c8-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="e48c8-138">Después del cambio</span><span class="sxs-lookup"><span data-stu-id="e48c8-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="e48c8-139">Modifique las reglas udev a fin de impedir que se generen reglas estáticas para las interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="e48c8-139">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="e48c8-140">Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e48c8-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="e48c8-141">Se recomienda editar el archivo "/etc/sysconfig/network/dhcp" y cambiar el parámetro `DHCLIENT_SET_HOSTNAME` por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e48c8-141">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
    
     <span data-ttu-id="e48c8-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="e48c8-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="e48c8-143">En "/etc/sudoers", convierta en comentario o quite las líneas siguientes, si existen:</span><span class="sxs-lookup"><span data-stu-id="e48c8-143">In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
    
     <span data-ttu-id="e48c8-144">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span><span class="sxs-lookup"><span data-stu-id="e48c8-144">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="e48c8-145">Use este código junto con 'Defaults targetpw'!</span><span class="sxs-lookup"><span data-stu-id="e48c8-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="e48c8-146">Asegúrese de que el servidor SSH se haya instalado y configurado para iniciarse en el tiempo de arranque.</span><span class="sxs-lookup"><span data-stu-id="e48c8-146">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="e48c8-147">Este es normalmente el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e48c8-147">This is usually the default.</span></span>
14. <span data-ttu-id="e48c8-148">No cree espacio de intercambio en el disco del SO.</span><span class="sxs-lookup"><span data-stu-id="e48c8-148">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="e48c8-149">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio utilizando el disco de recursos local que se adjunta a la máquina virtual después de aprovisionarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-149">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="e48c8-150">Tenga en cuenta que el disco de recursos local es un disco *temporal* que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="e48c8-150">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="e48c8-151">Después de instalar el Agente de Linux de Azure (consulte el paso anterior), modifique apropiadamente los parámetros siguientes en /etc/waagent.conf:</span><span class="sxs-lookup"><span data-stu-id="e48c8-151">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="e48c8-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTA: Establezca este valor en lo que necesite que sea.</span><span class="sxs-lookup"><span data-stu-id="e48c8-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
15. <span data-ttu-id="e48c8-153">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="e48c8-153">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="e48c8-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="e48c8-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="e48c8-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="e48c8-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="e48c8-156">logout</span><span class="sxs-lookup"><span data-stu-id="e48c8-156">logout</span></span>
16. <span data-ttu-id="e48c8-157">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e48c8-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="e48c8-158">El VHD de Linux ya está listo para cargarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-158">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="e48c8-159">Preparación de openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="e48c8-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="e48c8-160">Seleccione la máquina virtual en el panel central del Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e48c8-160">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="e48c8-161">Haga clic en **Conectar** para abrir la ventana de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e48c8-161">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="e48c8-162">En el shell, ejecute el comando '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="e48c8-162">On the shell, run the command '`zypper lr`'.</span></span> <span data-ttu-id="e48c8-163">Si este comando devuelve una salida similar a la siguiente, los repositorios están configurados según lo esperado y no es necesario ningún ajuste (tenga en cuenta que los números de versión pueden variar):</span><span class="sxs-lookup"><span data-stu-id="e48c8-163">If this command returns output similar to the following, then the repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="e48c8-164">Si el comando devuelve el mensaje "No repositories defined...", utilice los comandos siguientes para agregar estos repositorios:</span><span class="sxs-lookup"><span data-stu-id="e48c8-164">If the command returns "No repositories defined..." then use the following commands to add these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="e48c8-165">Puede verificar entonces que se han agregado los repositorios al volver a ejecutar el comando '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="e48c8-165">You can then verify the repositories have been added by running the command '`zypper lr`' again.</span></span> <span data-ttu-id="e48c8-166">En caso de que no haya un repositorio de actualizaciones relevante habilitado, habilítelo con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e48c8-166">In case one of the relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="e48c8-167">Actualice el kernel a la versión más reciente disponible:</span><span class="sxs-lookup"><span data-stu-id="e48c8-167">Update the kernel to the latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="e48c8-168">O para actualizar el sistema con todos los parches más recientes:</span><span class="sxs-lookup"><span data-stu-id="e48c8-168">Or to update the system with all the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="e48c8-169">Instale el Agente de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-169">Install the Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="e48c8-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="e48c8-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="e48c8-171">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-171">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="e48c8-172">Para ello, abra "/boot/grub/menu.lst" en un editor de texto y asegúrese de que el kernel predeterminado incluye los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="e48c8-172">To do this, open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
     <span data-ttu-id="e48c8-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="e48c8-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="e48c8-174">Así se asegurará de que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="e48c8-174">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="e48c8-175">Además, elimine los parámetros siguientes de la línea de arranque de kernel, si es que están:</span><span class="sxs-lookup"><span data-stu-id="e48c8-175">In addition, remove the following parameters from the kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="e48c8-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="e48c8-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="e48c8-177">Se recomienda editar el archivo "/etc/sysconfig/network/dhcp" y cambiar el parámetro `DHCLIENT_SET_HOSTNAME` por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e48c8-177">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
   
     <span data-ttu-id="e48c8-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="e48c8-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="e48c8-179">**Importante:** en "/etc/sudoers", realice un comentario o quite las siguientes líneas si existen:</span><span class="sxs-lookup"><span data-stu-id="e48c8-179">**Important:** In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
   
     <span data-ttu-id="e48c8-180">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span><span class="sxs-lookup"><span data-stu-id="e48c8-180">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="e48c8-181">Use este código junto con 'Defaults targetpw'!</span><span class="sxs-lookup"><span data-stu-id="e48c8-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="e48c8-182">Asegúrese de que el servidor SSH se haya instalado y configurado para iniciarse en el tiempo de arranque.</span><span class="sxs-lookup"><span data-stu-id="e48c8-182">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="e48c8-183">Este es normalmente el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e48c8-183">This is usually the default.</span></span>
10. <span data-ttu-id="e48c8-184">No cree espacio de intercambio en el disco del SO.</span><span class="sxs-lookup"><span data-stu-id="e48c8-184">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="e48c8-185">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio utilizando el disco de recursos local que se adjunta a la máquina virtual después de aprovisionarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-185">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="e48c8-186">Tenga en cuenta que el disco de recursos local es un disco *temporal* que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="e48c8-186">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="e48c8-187">Después de instalar el Agente de Linux de Azure (consulte el paso anterior), modifique apropiadamente los parámetros siguientes en /etc/waagent.conf:</span><span class="sxs-lookup"><span data-stu-id="e48c8-187">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="e48c8-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTA: Establezca este valor en lo que necesite que sea.</span><span class="sxs-lookup"><span data-stu-id="e48c8-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
11. <span data-ttu-id="e48c8-189">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="e48c8-189">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="e48c8-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="e48c8-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="e48c8-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="e48c8-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="e48c8-192">logout</span><span class="sxs-lookup"><span data-stu-id="e48c8-192">logout</span></span>
12. <span data-ttu-id="e48c8-193">Asegúrese de que el Agente de Linux de Azure se ejecute al inicio:</span><span class="sxs-lookup"><span data-stu-id="e48c8-193">Ensure the Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="e48c8-194">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e48c8-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="e48c8-195">El VHD de Linux ya está listo para cargarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-195">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e48c8-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e48c8-196">Next steps</span></span>
<span data-ttu-id="e48c8-197">Ya está listo para usar el disco duro virtual de SUSE para crear nuevas máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="e48c8-197">You're now ready to use your SUSE Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="e48c8-198">Si es la primera vez que carga el archivo .vhd en Azure, consulte los pasos 2 y 3 de [Creación y carga de un disco duro virtual que contiene el sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e48c8-198">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

