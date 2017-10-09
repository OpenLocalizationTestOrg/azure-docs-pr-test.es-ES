---
title: aaaCreate y cargar un disco duro virtual de Oracle Linux | Documentos de Microsoft
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contenga un sistema operativo de Linux de Oracle."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="47da0-103">Preparación de una máquina virtual Oracle Linux para Azure</span><span class="sxs-lookup"><span data-stu-id="47da0-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="47da0-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="47da0-104">Prerequisites</span></span>
<span data-ttu-id="47da0-105">En este artículo se da por supuesto que ya ha instalado un disco de duro virtual y tooa con sistema operativo Linux de Oracle.</span><span class="sxs-lookup"><span data-stu-id="47da0-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="47da0-106">Varias herramientas existen archivos .vhd de toocreate, por ejemplo, una solución de virtualización como Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="47da0-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="47da0-107">Para obtener instrucciones, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="47da0-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="47da0-108">Notas sobre la instalación de Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="47da0-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="47da0-109">Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.</span><span class="sxs-lookup"><span data-stu-id="47da0-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="47da0-110">El kernel compatible Red Hat de Oracle y su UEK3 (Unbreakable Enterprise Kernel) se admiten en Hyper-V y Azure.</span><span class="sxs-lookup"><span data-stu-id="47da0-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="47da0-111">Para obtener mejores resultados, ten kernel más reciente de tooupdate seguro toohello al preparar el disco duro virtual de Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="47da0-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="47da0-112">UEK2 de Oracle no se admite en Hyper-V y Azure incluya controladores Hola necesario.</span><span class="sxs-lookup"><span data-stu-id="47da0-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="47da0-113">no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.</span><span class="sxs-lookup"><span data-stu-id="47da0-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="47da0-114">Puede convertir Hola disco tooVHD formato con el Administrador de Hyper-V u Hola cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="47da0-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="47da0-115">Al instalar el sistema de Linux Hola se recomienda que utilice particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones).</span><span class="sxs-lookup"><span data-stu-id="47da0-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="47da0-116">Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita toobe adjuntada tooanother VM para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="47da0-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="47da0-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.</span><span class="sxs-lookup"><span data-stu-id="47da0-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="47da0-118">NUMA no se admite para los tamaños más grandes de VM debido a errores de tooa en versiones de kernel de Linux anteriores a 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="47da0-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="47da0-119">Este problema principalmente los impactos distribuciones utilizando Hola rojo ascendente kernel Hat 2.6.32.</span><span class="sxs-lookup"><span data-stu-id="47da0-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="47da0-120">Instalación manual de agente de Linux de Azure de hello (waagent) deshabilitará automáticamente NUMA en configuración de GRUB hello para el kernel de Linux Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="47da0-121">Para obtener más información acerca de este puede encontrarse en pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="47da0-122">No configure una partición de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="47da0-123">agente de Linux de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="47da0-124">Para obtener más información acerca de este puede encontrarse en pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="47da0-125">Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="47da0-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="47da0-126">Asegúrese de que ese hello `Addons` repositorio está habilitado.</span><span class="sxs-lookup"><span data-stu-id="47da0-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="47da0-127">Editar archivo hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) o `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) y cambie la línea hello `enabled=0` demasiado`enabled=1` en **[ol6_addons]** o **[ol7_addons]** en este archivo.</span><span class="sxs-lookup"><span data-stu-id="47da0-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="47da0-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="47da0-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="47da0-129">Debe completar pasos de configuración específica de sistema operativo de Hola para hello toorun de máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="47da0-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="47da0-130">En el panel central de hello del Administrador de Hyper-V, seleccione máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="47da0-131">Haga clic en **conectar** tooopen ventana de hello para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="47da0-132">Desinstala NetworkManager con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="47da0-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="47da0-133">**Nota:** si Hola paquete ya no está instalado, este comando generará un error con un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="47da0-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="47da0-134">Se espera que esto sea así.</span><span class="sxs-lookup"><span data-stu-id="47da0-134">This is expected.</span></span>
4. <span data-ttu-id="47da0-135">Cree un archivo denominado **red** en hello `/etc/sysconfig/` directorio que contiene Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="47da0-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="47da0-136">Cree un archivo denominado **ifcfg eth0** en hello `/etc/sysconfig/network-scripts/` directorio que contiene Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="47da0-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="47da0-137">Modificar udev reglas tooavoid generar reglas estáticas para hello interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="47da0-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="47da0-138">Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="47da0-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="47da0-139">Asegúrese de que se iniciará el servicio de red de hello al arrancar el sistema ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="47da0-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="47da0-140">Instalar python pyasn1 ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="47da0-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="47da0-141">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="47da0-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="47da0-142">Abra este toodo "/ boot/grub/menu.lst" en un editor de texto y asegúrese de que kernel predeterminada de hello incluye Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="47da0-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="47da0-143">Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="47da0-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="47da0-144">Esto deshabilitará NUMA debido a errores de tooa en kernel compatible de Red Hat de Oracle.</span><span class="sxs-lookup"><span data-stu-id="47da0-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="47da0-145">Además toohello anterior, se recomienda demasiado*quitar* Hola siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="47da0-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="47da0-146">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="47da0-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="47da0-147">Hola `crashkernel` opción puede ser izquierda configurado si lo desea, pero tenga en cuenta que este parámetro reducirá la cantidad de Hola de memoria disponible en hello máquina virtual por medio de 128 MB o más, lo que puede ser problemático en tamaños VM de hello más pequeños.</span><span class="sxs-lookup"><span data-stu-id="47da0-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="47da0-148">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="47da0-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="47da0-149">Esto suele ser el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-149">This is usually hello default.</span></span>
11. <span data-ttu-id="47da0-150">Instalar Agente Linux de Azure Hola ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="47da0-151">versión más reciente de Hello es 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="47da0-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="47da0-152">Tenga en cuenta que el paquete de instalación hello WALinuxAgent quitará Hola NetworkManager y paquetes de gnome NetworkManager si no se quitan ya tal como se describe en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="47da0-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="47da0-153">No cree el espacio de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="47da0-154">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure.</span><span class="sxs-lookup"><span data-stu-id="47da0-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="47da0-155">Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="47da0-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="47da0-156">Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en /etc/waagent.conf siguientes correctamente:</span><span class="sxs-lookup"><span data-stu-id="47da0-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="47da0-157">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="47da0-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="47da0-158">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="47da0-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="47da0-159">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="47da0-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="47da0-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="47da0-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="47da0-161">**Cambios en Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="47da0-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="47da0-162">Preparar una máquina virtual de Oracle Linux 7 de Azure es muy similar tooOracle Linux 6, sin embargo, hay algunas diferencias importantes que tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="47da0-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="47da0-163">Kernel compatible de Red Hat de Hola y UEK3 de Oracle se admiten en Azure.</span><span class="sxs-lookup"><span data-stu-id="47da0-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="47da0-164">se recomienda el kernel de UEK3 Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="47da0-165">Hola NetworkManager empaquetar ya no está en conflicto con el agente de Linux de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="47da0-166">Este paquete está instalado de manera predeterminada y recomendamos que no se quite.</span><span class="sxs-lookup"><span data-stu-id="47da0-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="47da0-167">GRUB2 ahora se usa como Hola del cargador de arranque de forma predeterminada, por lo que el procedimiento de Hola para editar los parámetros de kernel ha cambiado (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="47da0-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="47da0-168">XFS es ahora el sistema de archivos predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-168">XFS is now hello default file system.</span></span> <span data-ttu-id="47da0-169">sistema de archivos de Hello ext4 aún puede usarse si lo desea.</span><span class="sxs-lookup"><span data-stu-id="47da0-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="47da0-170">**Pasos de configuración**</span><span class="sxs-lookup"><span data-stu-id="47da0-170">**Configuration steps**</span></span>

1. <span data-ttu-id="47da0-171">En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="47da0-172">Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="47da0-173">Cree un archivo denominado **red** en hello `/etc/sysconfig/` directorio que contiene Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="47da0-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="47da0-174">Cree un archivo denominado **ifcfg eth0** en hello `/etc/sysconfig/network-scripts/` directorio que contiene Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="47da0-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="47da0-175">Modificar udev reglas tooavoid generar reglas estáticas para hello interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="47da0-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="47da0-176">Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="47da0-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="47da0-177">Asegúrese de que se iniciará el servicio de red de hello al arrancar el sistema ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="47da0-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="47da0-178">Instalar paquete de python pyasn1 Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="47da0-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="47da0-179">Siguiente ejecución Hola comando tooclear Hola actual yum metadatos e instala las actualizaciones:</span><span class="sxs-lookup"><span data-stu-id="47da0-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="47da0-180">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="47da0-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="47da0-181">toodo este abra "/ etcetera/predeterminado/grub" en un Hola de editor y edición de texto `GRUB_CMDLINE_LINUX` parámetro, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="47da0-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="47da0-182">Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="47da0-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="47da0-183">También desactiva Hola nuevas OEL 7 convenciones de nomenclatura para la NIC.</span><span class="sxs-lookup"><span data-stu-id="47da0-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="47da0-184">Además toohello anterior, se recomienda demasiado*quitar* Hola siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="47da0-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="47da0-185">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="47da0-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="47da0-186">Hola `crashkernel` opción puede ser izquierda configurado si lo desea, pero tenga en cuenta que este parámetro reducirá la cantidad de Hola de memoria disponible en hello máquina virtual por medio de 128 MB o más, lo que puede ser problemático en tamaños VM de hello más pequeños.</span><span class="sxs-lookup"><span data-stu-id="47da0-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="47da0-187">Cuando acabes edición "/ etcetera/predeterminado/grub" por encima, ejecute hello siguiente comando toorebuild Hola grub configuración:</span><span class="sxs-lookup"><span data-stu-id="47da0-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="47da0-188">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="47da0-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="47da0-189">Esto suele ser el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-189">This is usually hello default.</span></span>
12. <span data-ttu-id="47da0-190">Instale Hola agente Linux de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="47da0-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="47da0-191">No cree el espacio de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="47da0-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="47da0-192">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure.</span><span class="sxs-lookup"><span data-stu-id="47da0-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="47da0-193">Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="47da0-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="47da0-194">Después de instalar Hola agente Linux de Azure (vea el paso anterior de hello), modificar Hola parámetros en /etc/waagent.conf siguientes correctamente:</span><span class="sxs-lookup"><span data-stu-id="47da0-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="47da0-195">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="47da0-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="47da0-196">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="47da0-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="47da0-197">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="47da0-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47da0-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="47da0-198">Next steps</span></span>
<span data-ttu-id="47da0-199">Se está ahora listo toouse sus Oracle Linux .vhd toocreate nuevas máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="47da0-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="47da0-200">Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47da0-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

