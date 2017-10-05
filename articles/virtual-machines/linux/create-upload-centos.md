---
title: "Creación y carga de un VHD de Linux basado en CentOS en Azure"
description: Aprenda a crear y cargar un disco duro virtual de Azure (VHD) que contiene un sistema operativo Linux basado en CentOS.
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
ms.openlocfilehash: 010f4b05b35fa1f31c14f34a5fae9298fcd831e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="c7506-103">Preparación de una máquina virtual basada en CentOS para Azure</span><span class="sxs-lookup"><span data-stu-id="c7506-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="c7506-104">Preparación de una máquina virtual CentOS 6.x para Azure</span><span class="sxs-lookup"><span data-stu-id="c7506-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="c7506-105">Preparación de una máquina virtual CentOS 7.0+ para Azure</span><span class="sxs-lookup"><span data-stu-id="c7506-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="c7506-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c7506-106">Prerequisites</span></span>
<span data-ttu-id="c7506-107">En este artículo se supone que ya ha instalado un sistema operativo Linux CentOS (o un derivado similar) en un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="c7506-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="c7506-108">Existen varias herramientas para crear archivos .vhd; por ejemplo, una solución de virtualización como Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c7506-108">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="c7506-109">Para obtener instrucciones, consulte [Instalación del rol de Hyper-V y configuración de una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7506-109">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="c7506-110">**Notas de instalación de CentOS**</span><span class="sxs-lookup"><span data-stu-id="c7506-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="c7506-111">Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="c7506-112">El formato VHDX no se admite en Azure, solo el **VHD fijo**.</span><span class="sxs-lookup"><span data-stu-id="c7506-112">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="c7506-113">Puede convertir el disco al formato VHD con el Administrador de Hyper-V o el cmdlet Convert-VHD.</span><span class="sxs-lookup"><span data-stu-id="c7506-113">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="c7506-114">Si utiliza VirtualBox, deberá seleccionar **Tamaño fijo** en lugar del tamaño predeterminado asignado dinámicamente al crear el disco.</span><span class="sxs-lookup"><span data-stu-id="c7506-114">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="c7506-115">Al instalar el sistema Linux se *recomienda* utilizar las particiones estándar en lugar de un LVM (que a menudo viene de forma predeterminada en muchas instalaciones).</span><span class="sxs-lookup"><span data-stu-id="c7506-115">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="c7506-116">De este modo se impedirá que el nombre del LVM entre en conflicto con las máquinas virtuales clonadas, especialmente si en algún momento hace falta adjuntar un disco de SO a otra máquina virtual idéntica para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="c7506-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="c7506-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos.</span><span class="sxs-lookup"><span data-stu-id="c7506-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="c7506-118">Se requiere la compatibilidad de kernel para el montaje de sistemas de archivos UDF.</span><span class="sxs-lookup"><span data-stu-id="c7506-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="c7506-119">Al arrancar Azure la primera vez, la configuración de aprovisionamiento se pasa a la máquina virtual Linux a través de medios con formato UDF conectados al invitado.</span><span class="sxs-lookup"><span data-stu-id="c7506-119">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="c7506-120">El agente Linux de Azure debe poder montar el sistema de archivos UDF para leer su configuración y aprovisionar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7506-120">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="c7506-121">Las versiones de kernel de Linux inferiores a la versión 2.6.37 no admiten NUMA en Hyper-V con tamaños de VM más grandes.</span><span class="sxs-lookup"><span data-stu-id="c7506-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="c7506-122">Este problema afecta principalmente a las distribuciones anteriores que usan el kernel Red Hat 2.6.32 de canal de subida y se ha corregido en RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="c7506-122">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="c7506-123">Los sistemas que ejecutan kernels personalizados cuyas versiones son anteriores a la versión 2.6.37, o bien kernels basados en RHEL cuyas versiones son anteriores a la versión 2.6.32-504, deben establecer el parámetro de inicio `numa=off` en la línea de comandos de kernel en grub.conf.</span><span class="sxs-lookup"><span data-stu-id="c7506-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="c7506-124">Para obtener más información, consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="c7506-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="c7506-125">No cree una partición de intercambio en el disco del SO.</span><span class="sxs-lookup"><span data-stu-id="c7506-125">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="c7506-126">El agente de Linux se puede configurar para crear un archivo de intercambio en el disco de recursos temporal.</span><span class="sxs-lookup"><span data-stu-id="c7506-126">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="c7506-127">Puede encontrar más información al respecto en los pasos que vienen a continuación.</span><span class="sxs-lookup"><span data-stu-id="c7506-127">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="c7506-128">El tamaño de todos los archivos VHD debe ser múltiplo de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="c7506-128">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="c7506-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="c7506-129">CentOS 6.x</span></span>

1. <span data-ttu-id="c7506-130">En el Administrador de Hyper-V, seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7506-130">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="c7506-131">Haga clic en **Conectar** para abrir una ventana de consola de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7506-131">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="c7506-132">En CentOS 6, NetworkManager puede interferir con el Agente de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-132">In CentOS 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="c7506-133">Desinstale el paquete ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7506-133">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="c7506-134">Cree o edite el archivo `/etc/sysconfig/network` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="c7506-134">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="c7506-135">Cree o edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="c7506-135">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="c7506-136">Modifique las reglas udev a fin de impedir que se generen reglas estáticas para las interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="c7506-136">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="c7506-137">Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="c7506-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="c7506-138">Asegúrese de que el servicio de red se inicie en el arranque ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7506-138">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="c7506-139">Si desea utilizar los espejos OpenLogic hospedados en los centros de datos de Azure, sustituya el archivo `/etc/yum.repos.d/CentOS-Base.repo` por los siguientes repositorios.</span><span class="sxs-lookup"><span data-stu-id="c7506-139">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="c7506-140">Así se agregará también el repositorio **[openlogic]**, que incluye paquetes adicionales como el Agente de Linux de Azure:</span><span class="sxs-lookup"><span data-stu-id="c7506-140">This will also add the **[openlogic]** repository that includes additional packages such as the Azure Linux agent:</span></span>

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
    <span data-ttu-id="c7506-141">En el resto de esta guía se supondrá que usa al menos el repositorio `[openlogic]`, que se utilizará para instalar el agente de Linux de Azure siguiente.</span><span class="sxs-lookup"><span data-stu-id="c7506-141">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>


9. <span data-ttu-id="c7506-142">Agregue la línea siguiente a /etc/yum.conf:</span><span class="sxs-lookup"><span data-stu-id="c7506-142">Add the following line to /etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="c7506-143">Ejecute el siguiente comando para borrar los metadatos de yum actuales y actualizar el sistema con los últimos paquetes:</span><span class="sxs-lookup"><span data-stu-id="c7506-143">Run the following command to clear the current yum metadata and update the system with the latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="c7506-144">A menos que vaya a crear una imagen de una versión anterior de CentOS, se recomienda actualizar todos los paquetes a la versión más reciente:</span><span class="sxs-lookup"><span data-stu-id="c7506-144">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="c7506-145">Después de ejecutar este comando es posible que sea preciso reiniciar el equipo.</span><span class="sxs-lookup"><span data-stu-id="c7506-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="c7506-146">(Opcional) Instale los controladores para los servicios de integración de Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="c7506-146">(Optional) Install the drivers for the Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="c7506-147">El paso se **requiere** para CentOS 6.3 y las versiones anteriores, y opcional para las versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="c7506-147">The step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="c7506-148">Como alternativa, puede seguir las instrucciones de instalación manual de la [página de descarga de LIS](https://go.microsoft.com/fwlink/?linkid=403033) para instalar el RPM en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7506-148">Alternatively, you can follow the manual installation instructions on the [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) to install the RPM onto your VM.</span></span>
 
12. <span data-ttu-id="c7506-149">Instale el Agente de Linux de Azure y sus dependencias:</span><span class="sxs-lookup"><span data-stu-id="c7506-149">Install the Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="c7506-150">La instalación del paquete WALinuxAgent eliminará los paquetes NetworkManager y NetworkManager-gnome, si es que aún no se han eliminado, como se ha indicado en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="c7506-150">The WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="c7506-151">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-151">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="c7506-152">Para ello, abra `/boot/grub/menu.lst` en un editor de texto y asegúrese de que el kernel predeterminado incluye los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7506-152">To do this, open `/boot/grub/menu.lst` in a text editor and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="c7506-153">Así también se asegurará de que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="c7506-153">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="c7506-154">Además de lo anterior, se recomienda *quitar* los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7506-154">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="c7506-155">Los arranques gráfico y silencioso no resultan útiles en un entorno de nube, donde queremos que todos los registros se envíen al puerto serie.</span><span class="sxs-lookup"><span data-stu-id="c7506-155">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="c7506-156">Es posible dejar la opción `crashkernel` configurada si así se desea, pero tenga en cuenta que este parámetro reducirá la cantidad de memoria disponible en la máquina virtual en 128 MB o más, lo cual puede resultar problemático en tamaños de VM más reducidos.</span><span class="sxs-lookup"><span data-stu-id="c7506-156">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="c7506-157">CentOS 6.5 y las versiones anteriores también deben establecer el parámetro `numa=off` del kernel.</span><span class="sxs-lookup"><span data-stu-id="c7506-157">CentOS 6.5 and earlier must also set the kernel parameter `numa=off`.</span></span> <span data-ttu-id="c7506-158">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="c7506-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="c7506-159">Asegúrese de que el servidor SSH se haya instalado y configurado para iniciarse en el tiempo de arranque.</span><span class="sxs-lookup"><span data-stu-id="c7506-159">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="c7506-160">Este es normalmente el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="c7506-160">This is usually the default.</span></span>

15. <span data-ttu-id="c7506-161">No cree espacio de intercambio en el disco del SO.</span><span class="sxs-lookup"><span data-stu-id="c7506-161">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="c7506-162">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio utilizando el disco de recursos local que se adjunta a la máquina virtual después de aprovisionarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-162">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="c7506-163">Tenga en cuenta que el disco de recursos local es un disco *temporal* que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="c7506-163">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="c7506-164">Después de instalar el Agente de Linux de Azure (vea el paso anterior), modifique los parámetros siguientes en `/etc/waagent.conf` de la forma adecuada:</span><span class="sxs-lookup"><span data-stu-id="c7506-164">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="c7506-165">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="c7506-165">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="c7506-166">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c7506-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="c7506-167">El VHD de Linux ya está listo para cargarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-167">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="c7506-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="c7506-168">CentOS 7.0+</span></span>
<span data-ttu-id="c7506-169">**Cambios en CentOS 7 (y derivados similares)**</span><span class="sxs-lookup"><span data-stu-id="c7506-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="c7506-170">La preparación de una máquina virtual CentOS 7 para Azure es muy similar a CentOS 6, aunque hay varias diferencias importantes que es necesario tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="c7506-170">Preparing a CentOS 7 virtual machine for Azure is very similar to CentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="c7506-171">El paquete NetworkManager ya no entra en conflicto con el agente de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-171">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="c7506-172">Este paquete está instalado de manera predeterminada y recomendamos que no se quite.</span><span class="sxs-lookup"><span data-stu-id="c7506-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="c7506-173">GRUB2 se utiliza ahora como cargador de arranque predeterminado; por ello, el proceso de edición de los parámetros de kernel ha cambiado (ver más adelante).</span><span class="sxs-lookup"><span data-stu-id="c7506-173">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="c7506-174">XFS es ahora el sistema de archivos predeterminado.</span><span class="sxs-lookup"><span data-stu-id="c7506-174">XFS is now the default file system.</span></span> <span data-ttu-id="c7506-175">El sistema de archivos ext4 se puede seguir utilizando si así se desea.</span><span class="sxs-lookup"><span data-stu-id="c7506-175">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="c7506-176">**Pasos de configuración**</span><span class="sxs-lookup"><span data-stu-id="c7506-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="c7506-177">En el Administrador de Hyper-V, seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7506-177">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="c7506-178">Haga clic en **Conectar** para abrir una ventana de consola de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7506-178">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="c7506-179">Cree o edite el archivo `/etc/sysconfig/network` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="c7506-179">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="c7506-180">Cree o edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="c7506-180">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="c7506-181">Modifique las reglas udev a fin de impedir que se generen reglas estáticas para las interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="c7506-181">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="c7506-182">Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="c7506-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="c7506-183">Si desea utilizar los espejos OpenLogic hospedados en los centros de datos de Azure, sustituya el archivo `/etc/yum.repos.d/CentOS-Base.repo` por los siguientes repositorios.</span><span class="sxs-lookup"><span data-stu-id="c7506-183">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="c7506-184">De este modo se agregará también el repositorio **[openlogic]** que incluye paquetes para el agente de Linux de Azure:</span><span class="sxs-lookup"><span data-stu-id="c7506-184">This will also add the **[openlogic]** repository that includes packages for the Azure Linux agent:</span></span>
   
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
    <span data-ttu-id="c7506-185">En el resto de esta guía se supondrá que usa al menos el repositorio `[openlogic]`, que se utilizará para instalar el agente de Linux de Azure siguiente.</span><span class="sxs-lookup"><span data-stu-id="c7506-185">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>

7. <span data-ttu-id="c7506-186">Ejecute el comando siguiente para borrar los metadatos de yum actuales e instalar las actualizaciones:</span><span class="sxs-lookup"><span data-stu-id="c7506-186">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="c7506-187">A menos que vaya a crear una imagen de una versión anterior de CentOS, se recomienda actualizar todos los paquetes a la versión más reciente:</span><span class="sxs-lookup"><span data-stu-id="c7506-187">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="c7506-188">Después de ejecutar este comando es posible que sea preciso reiniciar el equipo.</span><span class="sxs-lookup"><span data-stu-id="c7506-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="c7506-189">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-189">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="c7506-190">Para ello, abra `/etc/default/grub` en un editor de texto y edite el parámetro `GRUB_CMDLINE_LINUX`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c7506-190">To do this, open `/etc/default/grub` in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="c7506-191">Así también se asegurará de que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="c7506-191">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="c7506-192">Esto también desactiva las nuevas convenciones de nomenclatura de CentOS 7 para NIC.</span><span class="sxs-lookup"><span data-stu-id="c7506-192">It also turns off the new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="c7506-193">Además de lo anterior, se recomienda *quitar* los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7506-193">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="c7506-194">Los arranques gráfico y silencioso no resultan útiles en un entorno de nube, donde queremos que todos los registros se envíen al puerto serie.</span><span class="sxs-lookup"><span data-stu-id="c7506-194">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="c7506-195">Es posible dejar la opción `crashkernel` configurada si así se desea, pero tenga en cuenta que este parámetro reducirá la cantidad de memoria disponible en la máquina virtual en 128 MB o más, lo cual puede resultar problemático en tamaños de VM más reducidos.</span><span class="sxs-lookup"><span data-stu-id="c7506-195">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

9. <span data-ttu-id="c7506-196">Una vez que termine de editar `/etc/default/grub` tal como se indicó antes, ejecute el comando siguiente para volver a compilar la configuración de GRUB:</span><span class="sxs-lookup"><span data-stu-id="c7506-196">Once you are done editing `/etc/default/grub` per above, run the following command to rebuild the grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="c7506-197">Si va a generar la imagen de **VMWare, VirtualBox o KVM**, asegúrese de que los controladores de Hyper-V se incluyen en initramfs:</span><span class="sxs-lookup"><span data-stu-id="c7506-197">If building the image from **VMWare, VirtualBox or KVM:** Ensure the Hyper-V drivers are included in the initramfs:</span></span>
   
   <span data-ttu-id="c7506-198">Edite `/etc/dracut.conf`y agregue contenido:</span><span class="sxs-lookup"><span data-stu-id="c7506-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="c7506-199">Vuelva a generar initramfs:</span><span class="sxs-lookup"><span data-stu-id="c7506-199">Rebuild the initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="c7506-200">Instale el Agente de Linux de Azure y sus dependencias:</span><span class="sxs-lookup"><span data-stu-id="c7506-200">Install the Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="c7506-201">No cree espacio de intercambio en el disco del SO.</span><span class="sxs-lookup"><span data-stu-id="c7506-201">Do not create swap space on the OS disk.</span></span>
   
   <span data-ttu-id="c7506-202">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio utilizando el disco de recursos local que se adjunta a la máquina virtual después de aprovisionarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-202">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="c7506-203">Tenga en cuenta que el disco de recursos local es un disco *temporal* que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="c7506-203">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="c7506-204">Después de instalar el Agente de Linux de Azure (vea el paso anterior), modifique los parámetros siguientes en `/etc/waagent.conf` de la forma adecuada:</span><span class="sxs-lookup"><span data-stu-id="c7506-204">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="c7506-205">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="c7506-205">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="c7506-206">Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c7506-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="c7506-207">El VHD de Linux ya está listo para cargarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-207">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7506-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7506-208">Next steps</span></span>
<span data-ttu-id="c7506-209">Ya está listo para usar el disco duro virtual de CentOS para crear nuevas máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7506-209">You're now ready to use your CentOS Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="c7506-210">Si es la primera vez que carga el archivo .vhd en Azure, consulte los pasos 2 y 3 de [Creación y carga de un disco duro virtual que contiene el sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c7506-210">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

