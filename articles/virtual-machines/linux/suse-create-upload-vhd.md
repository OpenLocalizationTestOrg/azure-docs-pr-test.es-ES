---
title: aaaCreate y cargar un VHD de SUSE Linux en Azure
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contiene un sistema operativo SUSE Linux."
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
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="ef70b-103">Preparación de una máquina virtual SLES u openSUSE para Azure</span><span class="sxs-lookup"><span data-stu-id="ef70b-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="ef70b-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ef70b-104">Prerequisites</span></span>
<span data-ttu-id="ef70b-105">En este artículo se da por supuesto que ya ha instalado un SUSE o openSUSE disco de duro virtual de tooa de sistema operativo de Linux.</span><span class="sxs-lookup"><span data-stu-id="ef70b-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="ef70b-106">Varias herramientas existen archivos .vhd de toocreate, por ejemplo, una solución de virtualización como Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ef70b-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="ef70b-107">Para obtener instrucciones, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef70b-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="ef70b-108">Notas sobre la instalación de SLES/openSUSE</span><span class="sxs-lookup"><span data-stu-id="ef70b-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="ef70b-109">Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="ef70b-110">no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.</span><span class="sxs-lookup"><span data-stu-id="ef70b-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="ef70b-111">Puede convertir Hola disco tooVHD formato con el Administrador de Hyper-V u Hola cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="ef70b-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="ef70b-112">Al instalar el sistema de Linux Hola se recomienda que utilice particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones).</span><span class="sxs-lookup"><span data-stu-id="ef70b-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="ef70b-113">Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita toobe adjuntada tooanother VM para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="ef70b-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="ef70b-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.</span><span class="sxs-lookup"><span data-stu-id="ef70b-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="ef70b-115">No configure una partición de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="ef70b-116">agente de Linux de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="ef70b-117">Para obtener más información acerca de este puede encontrarse en pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="ef70b-118">Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="ef70b-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="ef70b-119">Uso de SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="ef70b-119">Use SUSE Studio</span></span>
<span data-ttu-id="ef70b-120">[SUSE Studio](http://www.susestudio.com) puede crear y administrar fácilmente sus imágenes de SLES y openSUSE para Hyper-V y Azure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="ef70b-121">Se trata de hello enfoque para personalizar sus propias imágenes SLES y openSUSE recomendado.</span><span class="sxs-lookup"><span data-stu-id="ef70b-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="ef70b-122">Como una alternativa toobuilding su propio VHD, SUSE también publica imágenes BYOS (poner su propia suscripción) para SLES en [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="ef70b-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="ef70b-123">Preparación de SUSE Linux Enterprise Server 11 SP4</span><span class="sxs-lookup"><span data-stu-id="ef70b-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="ef70b-124">En el panel central de hello del Administrador de Hyper-V, seleccione máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="ef70b-125">Haga clic en **conectar** tooopen ventana de hello para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="ef70b-126">Registrar su tooallow de sistema de SUSE Linux Enterprise se toodownload actualizaciones y paquetes de instalación.</span><span class="sxs-lookup"><span data-stu-id="ef70b-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="ef70b-127">Actualizar sistema Hola con las últimas revisiones de hello:</span><span class="sxs-lookup"><span data-stu-id="ef70b-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="ef70b-128">Instalar Hola agente Linux de Azure desde el repositorio SLES hello:</span><span class="sxs-lookup"><span data-stu-id="ef70b-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="ef70b-129">Compruebe si waagent se establece demasiado "on" en chkconfig y, si no es así, puede habilitarla para inicio automático:</span><span class="sxs-lookup"><span data-stu-id="ef70b-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="ef70b-130">Compruebe si el servicio waagent se está ejecutando y, en caso contrario, inícielo:</span><span class="sxs-lookup"><span data-stu-id="ef70b-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="ef70b-131">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ef70b-132">Abra este toodo "/ boot/grub/menu.lst" en un editor de texto y asegúrese de que kernel predeterminada de hello incluye Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="ef70b-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="ef70b-133">Esto garantizará que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="ef70b-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="ef70b-134">Confirme que fstab /boot/grub/menu.lst y/etcetera/ambos disco de Hola de referencia mediante su UUID (por uuid) en lugar de Hola de Id. de disco (según el id).</span><span class="sxs-lookup"><span data-stu-id="ef70b-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="ef70b-135">Obtención del UUID del disco</span><span class="sxs-lookup"><span data-stu-id="ef70b-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="ef70b-136">Si /dev/disk/by-id o que se utiliza, actualizar /boot/grub/menu.lst y/etcetera/fstab con el valor de correcto mediante el uuid de Hola</span><span class="sxs-lookup"><span data-stu-id="ef70b-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="ef70b-137">Antes del cambio</span><span class="sxs-lookup"><span data-stu-id="ef70b-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="ef70b-138">Después del cambio</span><span class="sxs-lookup"><span data-stu-id="ef70b-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="ef70b-139">Modificar udev reglas tooavoid generar reglas estáticas para hello interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="ef70b-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="ef70b-140">Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="ef70b-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="ef70b-141">Se recomienda archivo de hello tooedit "/ etcetera/sysconfig/red/dhcp" y cambiar hello `DHCLIENT_SET_HOSTNAME` parámetro toohello que sigue:</span><span class="sxs-lookup"><span data-stu-id="ef70b-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="ef70b-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="ef70b-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="ef70b-143">En "/ etcetera/sudoers", convierta en comentario o quite Hola siguiendo las líneas si existen:</span><span class="sxs-lookup"><span data-stu-id="ef70b-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="ef70b-144">Valor predeterminado es targetpw # pedir contraseña Hola Hola del usuario de destino, es decir, todos los ALL=(ALL) todos raíz # advertencia!</span><span class="sxs-lookup"><span data-stu-id="ef70b-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="ef70b-145">Use este código junto con 'Defaults targetpw'!</span><span class="sxs-lookup"><span data-stu-id="ef70b-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="ef70b-146">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="ef70b-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="ef70b-147">Esto suele ser el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-147">This is usually hello default.</span></span>
14. <span data-ttu-id="ef70b-148">No cree el espacio de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="ef70b-149">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="ef70b-150">Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="ef70b-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="ef70b-151">Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en /etc/waagent.conf siguientes correctamente:</span><span class="sxs-lookup"><span data-stu-id="ef70b-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="ef70b-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Nota: establezca este toowhatever necesita toobe.</span><span class="sxs-lookup"><span data-stu-id="ef70b-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="ef70b-153">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="ef70b-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="ef70b-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="ef70b-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="ef70b-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="ef70b-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="ef70b-156">logout</span><span class="sxs-lookup"><span data-stu-id="ef70b-156">logout</span></span>
16. <span data-ttu-id="ef70b-157">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ef70b-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="ef70b-158">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="ef70b-159">Preparación de openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="ef70b-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="ef70b-160">En el panel central de hello del Administrador de Hyper-V, seleccione máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="ef70b-161">Haga clic en **conectar** tooopen ventana de hello para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="ef70b-162">En el shell de hello, ejecute el comando de hello '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="ef70b-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="ef70b-163">Si este comando devuelve resultados similar toohello sigue, después, repositorios de Hola se configura como se esperaba: ajustes no son necesarios (tenga en cuenta que los números de versión pueden variar):</span><span class="sxs-lookup"><span data-stu-id="ef70b-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="ef70b-164">Si el comando de hello devuelve "Hay repositorios definidos..." usar, a continuación, hello después tooadd comandos estos repositorios:</span><span class="sxs-lookup"><span data-stu-id="ef70b-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="ef70b-165">A continuación, puede comprobar repositorios de Hola se agregaron mediante la ejecución de comando hello '`zypper lr`' nuevo.</span><span class="sxs-lookup"><span data-stu-id="ef70b-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="ef70b-166">En caso de que uno de los repositorios de actualización relevante de hello no está habilitado, habilite esta opción con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="ef70b-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="ef70b-167">Actualizar Hola kernel toohello versión más reciente disponible:</span><span class="sxs-lookup"><span data-stu-id="ef70b-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="ef70b-168">Sistema de hello tooupdate con todas las revisiones más recientes de Hola o:</span><span class="sxs-lookup"><span data-stu-id="ef70b-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="ef70b-169">Instalar Hola agente Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="ef70b-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="ef70b-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="ef70b-171">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ef70b-172">toodo, abra "/ boot/grub/menu.lst" en un editor de texto y asegúrese de que kernel predeterminada de hello incluye Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="ef70b-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="ef70b-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="ef70b-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="ef70b-174">Esto garantizará que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="ef70b-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="ef70b-175">Además, quitar Hola siguientes parámetros de línea de arranque de kernel Hola si existen:</span><span class="sxs-lookup"><span data-stu-id="ef70b-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="ef70b-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="ef70b-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="ef70b-177">Se recomienda archivo de hello tooedit "/ etcetera/sysconfig/red/dhcp" y cambiar hello `DHCLIENT_SET_HOSTNAME` parámetro toohello que sigue:</span><span class="sxs-lookup"><span data-stu-id="ef70b-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="ef70b-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="ef70b-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="ef70b-179">**Importante:** en "/ etcetera/sudoers", convierta en comentario o quitar Hola siguiendo las líneas si existen:</span><span class="sxs-lookup"><span data-stu-id="ef70b-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="ef70b-180">Valor predeterminado es targetpw # pedir contraseña Hola Hola del usuario de destino, es decir, todos los ALL=(ALL) todos raíz # advertencia!</span><span class="sxs-lookup"><span data-stu-id="ef70b-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="ef70b-181">Use este código junto con 'Defaults targetpw'!</span><span class="sxs-lookup"><span data-stu-id="ef70b-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="ef70b-182">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="ef70b-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="ef70b-183">Esto suele ser el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-183">This is usually hello default.</span></span>
10. <span data-ttu-id="ef70b-184">No cree el espacio de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef70b-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="ef70b-185">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="ef70b-186">Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="ef70b-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="ef70b-187">Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en /etc/waagent.conf siguientes correctamente:</span><span class="sxs-lookup"><span data-stu-id="ef70b-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="ef70b-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Nota: establezca este toowhatever necesita toobe.</span><span class="sxs-lookup"><span data-stu-id="ef70b-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="ef70b-189">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="ef70b-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="ef70b-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="ef70b-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="ef70b-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="ef70b-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="ef70b-192">logout</span><span class="sxs-lookup"><span data-stu-id="ef70b-192">logout</span></span>
12. <span data-ttu-id="ef70b-193">Asegúrese de hello que agente Linux de Azure se ejecuta en el inicio:</span><span class="sxs-lookup"><span data-stu-id="ef70b-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="ef70b-194">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ef70b-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="ef70b-195">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef70b-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ef70b-196">Next steps</span></span>
<span data-ttu-id="ef70b-197">Se está ahora listo toouse sus SUSE Linux disco duro virtual toocreate nuevas máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="ef70b-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="ef70b-198">Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef70b-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

