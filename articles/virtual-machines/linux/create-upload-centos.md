---
title: aaaCreate y cargar un VHD de Linux-based CentOS en Azure
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contiene un sistema operativo basado en CentOS Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="4dd74-103">Preparación de una máquina virtual basada en CentOS para Azure</span><span class="sxs-lookup"><span data-stu-id="4dd74-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="4dd74-104">Preparación de una máquina virtual CentOS 6.x para Azure</span><span class="sxs-lookup"><span data-stu-id="4dd74-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="4dd74-105">Preparación de una máquina virtual CentOS 7.0+ para Azure</span><span class="sxs-lookup"><span data-stu-id="4dd74-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="4dd74-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4dd74-106">Prerequisites</span></span>
<span data-ttu-id="4dd74-107">En este artículo se da por supuesto que ya ha instalado una distribución de CentOS (o similar derivado) disco de duro virtual de tooa de sistema operativo de Linux.</span><span class="sxs-lookup"><span data-stu-id="4dd74-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="4dd74-108">Varias herramientas existen archivos .vhd de toocreate, por ejemplo, una solución de virtualización como Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4dd74-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="4dd74-109">Para obtener instrucciones, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="4dd74-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="4dd74-110">**Notas de instalación de CentOS**</span><span class="sxs-lookup"><span data-stu-id="4dd74-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="4dd74-111">Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.</span><span class="sxs-lookup"><span data-stu-id="4dd74-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="4dd74-112">no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.</span><span class="sxs-lookup"><span data-stu-id="4dd74-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="4dd74-113">Puede convertir Hola disco tooVHD formato con el Administrador de Hyper-V u Hola cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="4dd74-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="4dd74-114">Si usas VirtualBox Esto significa seleccionar **tamaño fijo** como opone predeterminado toohello asignada de forma dinámica al crear el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="4dd74-115">Al instalar el sistema de Linux de hello es *recomienda* utilizar particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones).</span><span class="sxs-lookup"><span data-stu-id="4dd74-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="4dd74-116">Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita tooanother toobe adjunta VM idéntico para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="4dd74-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="4dd74-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos.</span><span class="sxs-lookup"><span data-stu-id="4dd74-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="4dd74-118">Se requiere la compatibilidad de kernel para el montaje de sistemas de archivos UDF.</span><span class="sxs-lookup"><span data-stu-id="4dd74-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="4dd74-119">En el primer arranque en hello Azure configuración del aprovisionamiento pasa toohello VM de Linux a través de medios con formato UDF que está invitado toohello adjunto.</span><span class="sxs-lookup"><span data-stu-id="4dd74-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="4dd74-120">agente de Linux de Azure de Hello debe ser capaz de toomount Hola UDF archivo sistema tooread su configuración y aprovisionar Hola VM.</span><span class="sxs-lookup"><span data-stu-id="4dd74-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="4dd74-121">Las versiones de kernel de Linux inferiores a la versión 2.6.37 no admiten NUMA en Hyper-V con tamaños de VM más grandes.</span><span class="sxs-lookup"><span data-stu-id="4dd74-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="4dd74-122">Este problema afecta principalmente distribuciones anteriores mediante hello en dirección ascendente kernel de Red Hat 2.6.32 y se ha corregido en RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="4dd74-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="4dd74-123">Sistemas que ejecutan kernels personalizados anteriores a 2.6.37 o basado en RHEL kernels anteriores que se debe establecer 2.6.32-504 Hola parámetro de arranque `numa=off` en kernel Hola de línea de comandos en grub.conf.</span><span class="sxs-lookup"><span data-stu-id="4dd74-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="4dd74-124">Para obtener más información, consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="4dd74-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="4dd74-125">No configure una partición de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="4dd74-126">agente de Linux de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="4dd74-127">Para obtener más información acerca de este puede encontrarse en pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="4dd74-128">Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="4dd74-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="4dd74-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="4dd74-129">CentOS 6.x</span></span>

1. <span data-ttu-id="4dd74-130">En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="4dd74-131">Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="4dd74-132">De CentOS 6, NetworkManager puede interferir con el agente de Linux de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="4dd74-133">Desinstalar este paquete ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4dd74-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="4dd74-134">Crear o editar el archivo hello `/etc/sysconfig/network` y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="4dd74-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="4dd74-135">Crear o editar el archivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="4dd74-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="4dd74-136">Modificar udev reglas tooavoid generar reglas estáticas para hello interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="4dd74-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="4dd74-137">Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="4dd74-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="4dd74-138">Asegúrese de que se iniciará el servicio de red de hello al arrancar el sistema ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="4dd74-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="4dd74-139">Si desea que los reflejos de OpenLogic de hello toouse que se hospedan en hello centros de datos de Azure, a continuación, reemplace hello `/etc/yum.repos.d/CentOS-Base.repo` archivo con hello después repositorios.</span><span class="sxs-lookup"><span data-stu-id="4dd74-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="4dd74-140">También agregará hello **[openlogic]** repositorio que incluye paquetes adicionales como el agente de Linux de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="4dd74-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="4dd74-141">Hello resto de esta guía se presupone que usa al menos Hola `[openlogic]` repositorio, que será usado tooinstall Hola Linux de Azure agente siguiente.</span><span class="sxs-lookup"><span data-stu-id="4dd74-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="4dd74-142">Agregue Hola después too/etc/yum.conf línea:</span><span class="sxs-lookup"><span data-stu-id="4dd74-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="4dd74-143">Ejecute hello después comando tooclear Hola yum actualización y los metadatos hello sistema actual con los paquetes de saludo más recientes:</span><span class="sxs-lookup"><span data-stu-id="4dd74-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="4dd74-144">A menos que se va a crear una imagen de una versión anterior de CentOS, se recomienda tooupdate que Hola a todos los paquetes toohello más reciente:</span><span class="sxs-lookup"><span data-stu-id="4dd74-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="4dd74-145">Después de ejecutar este comando es posible que sea preciso reiniciar el equipo.</span><span class="sxs-lookup"><span data-stu-id="4dd74-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="4dd74-146">(Opcional) Instalar a controladores de Hola para hello servicios de integración de Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="4dd74-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="4dd74-147">paso de Hello es **necesario** para CentOS 6.3 y opcionales para versiones posteriores y anteriores.</span><span class="sxs-lookup"><span data-stu-id="4dd74-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="4dd74-148">Como alternativa, puede seguir las instrucciones de instalación manual de hello en hello [página de descarga de LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall Hola RPM en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4dd74-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="4dd74-149">Instalar Agente Linux de Azure de Hola y dependencias:</span><span class="sxs-lookup"><span data-stu-id="4dd74-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="4dd74-150">paquete de Hello WALinuxAgent quitará Hola NetworkManager y paquetes de gnome NetworkManager si no se quitan ya tal como se describe en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="4dd74-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="4dd74-151">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dd74-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4dd74-152">toodo, abra `/boot/grub/menu.lst` en un editor de texto y asegúrese de que kernel predeterminada de hello incluye Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="4dd74-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="4dd74-153">Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="4dd74-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="4dd74-154">Además toohello anterior, se recomienda demasiado*quitar* Hola siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="4dd74-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="4dd74-155">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="4dd74-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="4dd74-156">Hola `crashkernel` opción puede ser izquierda configurado si lo desea, pero tenga en cuenta que este parámetro reducirá la cantidad de Hola de memoria disponible en hello máquina virtual por medio de 128 MB o más, lo que puede ser problemático en tamaños VM de hello más pequeños.</span><span class="sxs-lookup"><span data-stu-id="4dd74-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="4dd74-157">CentOS 6.5 y versiones anteriores también deben establecer el parámetro de kernel de hello `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="4dd74-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="4dd74-158">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="4dd74-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="4dd74-159">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="4dd74-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="4dd74-160">Esto suele ser el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-160">This is usually hello default.</span></span>

15. <span data-ttu-id="4dd74-161">No cree el espacio de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="4dd74-162">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure.</span><span class="sxs-lookup"><span data-stu-id="4dd74-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="4dd74-163">Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="4dd74-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="4dd74-164">Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:</span><span class="sxs-lookup"><span data-stu-id="4dd74-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="4dd74-165">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="4dd74-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="4dd74-166">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4dd74-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="4dd74-167">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4dd74-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="4dd74-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="4dd74-168">CentOS 7.0+</span></span>
<span data-ttu-id="4dd74-169">**Cambios en CentOS 7 (y derivados similares)**</span><span class="sxs-lookup"><span data-stu-id="4dd74-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="4dd74-170">Preparar una máquina virtual de CentOS 7 de Azure es muy similar tooCentOS 6, sin embargo, hay algunas diferencias importantes que tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="4dd74-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="4dd74-171">Hola NetworkManager empaquetar ya no está en conflicto con el agente de Linux de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="4dd74-172">Este paquete está instalado de manera predeterminada y recomendamos que no se quite.</span><span class="sxs-lookup"><span data-stu-id="4dd74-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="4dd74-173">GRUB2 ahora se usa como Hola del cargador de arranque de forma predeterminada, por lo que el procedimiento de Hola para editar los parámetros de kernel ha cambiado (vea a continuación).</span><span class="sxs-lookup"><span data-stu-id="4dd74-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="4dd74-174">XFS es ahora el sistema de archivos predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-174">XFS is now hello default file system.</span></span> <span data-ttu-id="4dd74-175">sistema de archivos de Hello ext4 aún puede usarse si lo desea.</span><span class="sxs-lookup"><span data-stu-id="4dd74-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="4dd74-176">**Pasos de configuración**</span><span class="sxs-lookup"><span data-stu-id="4dd74-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="4dd74-177">En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="4dd74-178">Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="4dd74-179">Crear o editar el archivo hello `/etc/sysconfig/network` y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="4dd74-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="4dd74-180">Crear o editar el archivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="4dd74-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="4dd74-181">Modificar udev reglas tooavoid generar reglas estáticas para hello interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="4dd74-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="4dd74-182">Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="4dd74-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="4dd74-183">Si desea que los reflejos de OpenLogic de hello toouse que se hospedan en hello centros de datos de Azure, a continuación, reemplace hello `/etc/yum.repos.d/CentOS-Base.repo` archivo con hello después repositorios.</span><span class="sxs-lookup"><span data-stu-id="4dd74-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="4dd74-184">También agregará hello **[openlogic]** repositorio que incluye paquetes de agente de Linux de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="4dd74-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="4dd74-185">Hello resto de esta guía se presupone que usa al menos Hola `[openlogic]` repositorio, que será usado tooinstall Hola Linux de Azure agente siguiente.</span><span class="sxs-lookup"><span data-stu-id="4dd74-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="4dd74-186">Siguiente ejecución Hola comando tooclear Hola actual yum metadatos e instala las actualizaciones:</span><span class="sxs-lookup"><span data-stu-id="4dd74-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="4dd74-187">A menos que se va a crear una imagen de una versión anterior de CentOS, se recomienda tooupdate que Hola a todos los paquetes toohello más reciente:</span><span class="sxs-lookup"><span data-stu-id="4dd74-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="4dd74-188">Después de ejecutar este comando es posible que sea preciso reiniciar el equipo.</span><span class="sxs-lookup"><span data-stu-id="4dd74-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="4dd74-189">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dd74-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4dd74-190">toodo, abra `/etc/default/grub` en un Hola de editor y edición de texto `GRUB_CMDLINE_LINUX` parámetro, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4dd74-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="4dd74-191">Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="4dd74-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="4dd74-192">También desactiva Hola nuevas CentOS 7 convenciones de nomenclatura para la NIC.</span><span class="sxs-lookup"><span data-stu-id="4dd74-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="4dd74-193">Además toohello anterior, se recomienda demasiado*quitar* Hola siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="4dd74-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="4dd74-194">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="4dd74-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="4dd74-195">Hola `crashkernel` opción puede ser izquierda configurado si lo desea, pero tenga en cuenta que este parámetro reducirá la cantidad de Hola de memoria disponible en hello máquina virtual por medio de 128 MB o más, lo que puede ser problemático en tamaños VM de hello más pequeños.</span><span class="sxs-lookup"><span data-stu-id="4dd74-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="4dd74-196">Cuando acabes edición `/etc/default/grub` por encima, ejecute hello siguiente comando toorebuild Hola grub configuración:</span><span class="sxs-lookup"><span data-stu-id="4dd74-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="4dd74-197">Si la creación de imagen de Hola de **VMWare, VirtualBox o KVM:** hello initramfs incluye controladores de hello Hyper-V Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="4dd74-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="4dd74-198">Edite `/etc/dracut.conf`y agregue contenido:</span><span class="sxs-lookup"><span data-stu-id="4dd74-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="4dd74-199">Vuelva a generar Hola initramfs:</span><span class="sxs-lookup"><span data-stu-id="4dd74-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="4dd74-200">Instalar Agente Linux de Azure de Hola y dependencias:</span><span class="sxs-lookup"><span data-stu-id="4dd74-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="4dd74-201">No cree el espacio de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dd74-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="4dd74-202">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure.</span><span class="sxs-lookup"><span data-stu-id="4dd74-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="4dd74-203">Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="4dd74-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="4dd74-204">Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:</span><span class="sxs-lookup"><span data-stu-id="4dd74-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="4dd74-205">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="4dd74-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="4dd74-206">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4dd74-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="4dd74-207">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4dd74-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dd74-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4dd74-208">Next steps</span></span>
<span data-ttu-id="4dd74-209">Se está ahora listo toouse sus CentOS Linux disco duro virtual toocreate nuevas máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="4dd74-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="4dd74-210">Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4dd74-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

