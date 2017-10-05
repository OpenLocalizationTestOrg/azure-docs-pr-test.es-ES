---
title: "Creación y carga de un VHD de Red Hat Enterprise Linux para su uso en Azure | Microsoft Docs"
description: Aprenda a crear y cargar un disco duro virtual (VHD) de Azure que contiene un sistema operativo Red Hat Linux.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: b753c76b8c3d789c681d7fbff6aa07590b860be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="0e7fc-103">Preparación de una máquina virtual basada en Red Hat para Azure</span><span class="sxs-lookup"><span data-stu-id="0e7fc-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="0e7fc-104">En este artículo, aprenderá a preparar una máquina virtual de Red Hat Enterprise Linux (RHEL) para usarla en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="0e7fc-105">Las versiones de RHEL que se tratan en este artículo son 6.7 y 7.1.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-105">The versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="0e7fc-106">Los hipervisores de preparación que se tratan en este artículo son Hyper-V, máquina virtual basada en kernel (KVM) y VMware.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="0e7fc-107">Para más información sobre los requisitos para poder participar en el programa de acceso a la nube de Red Hat, visite el sitio [web de acceso a la nube de Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) y [Ejecución de RHEL en Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="0e7fc-108">Preparación de una máquina virtual basada en Red Hat desde el Administrador de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0e7fc-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0e7fc-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e7fc-109">Prerequisites</span></span>
<span data-ttu-id="0e7fc-110">En esta sección, se supone que ya obtuvo un archivo ISO en el sitio web de Red Hat y que ha instalado la imagen RHEL en un disco duro virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-110">This section assumes that you have already obtained an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span></span> <span data-ttu-id="0e7fc-111">Para más información acerca de cómo usar el Administrador de Hyper-V para instalar una imagen de sistema operativo, vea [Instalar Hyper-V y crear una máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-111">For more details about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="0e7fc-112">**Notas de instalación de RHEL**</span><span class="sxs-lookup"><span data-stu-id="0e7fc-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="0e7fc-113">Azure no admite el formato VHDX.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-113">Azure does not support the VHDX format.</span></span> <span data-ttu-id="0e7fc-114">Azure solo admite VHD fijo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="0e7fc-115">Puede usar el Administrador de Hyper-V para convertir el disco al formato VHD, o puede usar el cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-115">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span></span> <span data-ttu-id="0e7fc-116">Si usa VirtualBox, seleccione **Tamaño fijo** a diferencia de la opción predeterminada asignada dinámicamente al crear el disco.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-116">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span></span>
* <span data-ttu-id="0e7fc-117">Azure solo admite máquinas virtuales de la generación 1.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="0e7fc-118">Puede convertir una máquina virtual de generación 1 de VHDX para el formato de archivo VHD desde un disco de expansión dinámica a otro de tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-118">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span></span> <span data-ttu-id="0e7fc-119">No puede cambiar la generación de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="0e7fc-120">Para más información, consulte [¿Debería crear una máquina virtual de generación 1 o 2 en Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="0e7fc-121">El tamaño máximo permitido para los discos duros virtuales es de 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-121">The maximum size that's allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="0e7fc-122">Al instalar el sistema operativo Linux se recomienda usar las particiones estándar en lugar de Logical Volume Manager (LVM) que a menudo viene de forma predeterminada en muchas instalaciones.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-122">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span></span> <span data-ttu-id="0e7fc-123">Esta práctica evitará los conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si alguna vez necesita conectar un disco de sistema operativo a otra máquina virtual idéntica para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="0e7fc-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="0e7fc-125">Se requiere la compatibilidad de kernel para el montaje de sistemas de archivos de formato de disco universal (UDF).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="0e7fc-126">Al arrancar Azure la primera vez, los medios con formato UDF conectados al invitado pasan la configuración de aprovisionamiento a la máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-126">At first boot on Azure, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span></span> <span data-ttu-id="0e7fc-127">El agente Linux de Azure debe poder montar el sistema de archivos UDF para leer su configuración y aprovisionar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-127">The Azure Linux Agent must be able to mount the UDF file system to read its configuration and provision the virtual machine.</span></span>
* <span data-ttu-id="0e7fc-128">Las versiones del kernel de Linux anteriores a 2.6.37 no admiten el acceso a memoria no uniforme (NUMA) en Hyper-V con tamaños de máquina virtual mayores.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-128">Versions of the Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="0e7fc-129">Este problema afecta principalmente a las distribuciones anteriores que usan el kernel Red Hat 2.6.32 de canal de subida y se ha corregido en RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-129">This issue primarily impacts older distributions that use the upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="0e7fc-130">Los sistemas que ejecutan kernels personalizados cuyas versiones son anteriores a la versión 2.6.37, o bien kernels basados en RHEL cuyas versiones son anteriores a la versión 2.6.32-504, deben establecer el parámetro de inicio `numa=off` en la línea de comandos de kernel en grub.conf.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set the `numa=off` boot parameter on the kernel command line in grub.conf.</span></span> <span data-ttu-id="0e7fc-131">Para más información, consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="0e7fc-132">No configure una partición de intercambio en el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-132">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="0e7fc-133">El agente de Linux se puede configurar para crear un archivo de intercambio en el disco de recursos temporal.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-133">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="0e7fc-134">Puede encontrar más información al respecto en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-134">More information about this can be found in the following steps.</span></span>
* <span data-ttu-id="0e7fc-135">El tamaño de todos los VHD debe ser múltiplo de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="0e7fc-136">Preparar una máquina virtual RHEL 6 desde el Administrador de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0e7fc-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="0e7fc-137">En el Administrador de Hyper-V, seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-137">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="0e7fc-138">Haga clic en **Conectar** para abrir una ventana de consola de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-138">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="0e7fc-139">En RHEL 6, NetworkManager puede interferir en el Agente de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-139">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="0e7fc-140">Desinstale el paquete ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-140">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="0e7fc-141">Cree o edite el archivo `/etc/sysconfig/network` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-141">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="0e7fc-142">Cree o edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-142">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="0e7fc-143">Mueva (o elimine) las reglas udev para impedir que se generen reglas estáticas para la interfaz Ethernet.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-143">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="0e7fc-144">Estas reglas pueden causar problemas cuando clone una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="0e7fc-145">Asegúrese de que el servicio de red se inicia en el arranque ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-145">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="0e7fc-146">Registre la suscripción de Red Hat para habilitar la instalación de paquetes desde el repositorio RHEL ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-146">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="0e7fc-147">El paquete WALinuxAgent `WALinuxAgent-<version>` se ha insertado en el repositorio de extras de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-147">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="0e7fc-148">Habilite el repositorio de extras ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-148">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="0e7fc-149">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-149">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="0e7fc-150">Para realizar esta modificación, abra `/boot/grub/menu.lst` en un editor de texto y asegúrese de que el kernel predeterminado incluye los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-150">To do this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="0e7fc-151">Así también se asegurará de que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-151">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="0e7fc-152">Además, se recomienda quitar los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-152">In addition, we recommended that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="0e7fc-153">Los arranques gráfico y silencioso no resultan útiles en un entorno de nube, donde queremos que todos los registros se envíen al puerto serie.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-153">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="0e7fc-154">Puede dejar la opción `crashkernel` configurada si lo desea.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-154">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="0e7fc-155">Tenga en cuenta que este parámetro reduce la cantidad de memoria disponible en la máquina virtual unos 128 MB o más.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-155">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more.</span></span> <span data-ttu-id="0e7fc-156">Esta configuración podría resultar problemática en tamaños de máquinas virtuales más pequeños.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="0e7fc-157">RHEL 6.5 y las versiones anteriores también deben establecer el parámetro `numa=off` del kernel.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-157">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="0e7fc-158">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="0e7fc-159">Asegúrese de que el servidor Secure Shell (SSH) está instalado y configurado para iniciarse en el tiempo de arranque, que suele ser el predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-159">Ensure that the secure shell (SSH) server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="0e7fc-160">Modifique /etc/ssh/sshd_config para que incluya la siguiente línea:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-160">Modify /etc/ssh/sshd_config to include the following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="0e7fc-161">Instale el Agente de Linux de Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-161">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="0e7fc-162">La instalación del paquete WALinuxAgent elimina los paquetes NetworkManager y NetworkManager-gnome, si es que aún no se han quitado en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-162">Installing the WALinuxAgent package removes the NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="0e7fc-163">No cree espacio de intercambio en el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-163">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="0e7fc-164">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio usando el disco de recursos local que se adjunta a la máquina virtual, después de que la máquina virtual se aprovisione en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-164">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="0e7fc-165">Tenga en cuenta que el disco de recursos local es un disco temporal que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-165">Note that the local resource disk is a temporary disk and that it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="0e7fc-166">Después de instalar el agente de Linux de Azure en el paso anterior, modifique apropiadamente los parámetros siguientes en /etc/waagent.conf:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-166">After you install the Azure Linux Agent in the previous step, modify the following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

14. <span data-ttu-id="0e7fc-167">Para anular el registro de la suscripción (si es necesario), ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-167">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="0e7fc-168">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-168">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="0e7fc-169">Haga clic en **Acción**  >  **Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="0e7fc-170">El VHD de Linux ya está listo para cargarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-170">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="0e7fc-171">Preparar una máquina virtual RHEL 7 desde el Administrador de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0e7fc-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="0e7fc-172">En el Administrador de Hyper-V, seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-172">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="0e7fc-173">Haga clic en **Conectar** para abrir una ventana de consola de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-173">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="0e7fc-174">Cree o edite el archivo `/etc/sysconfig/network` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-174">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="0e7fc-175">Cree o edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-175">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="0e7fc-176">Asegúrese de que el servicio de red se inicia en el arranque ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-176">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="0e7fc-177">Registre la suscripción de Red Hat para habilitar la instalación de paquetes desde el repositorio RHEL ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-177">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="0e7fc-178">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-178">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="0e7fc-179">Para realizar esta modificación, abra `/etc/default/grub` en un editor de texto y edite el parámetro `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-179">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="0e7fc-180">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="0e7fc-181">Así también se asegurará de que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-181">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="0e7fc-182">Esta configuración también desactiva las nuevas convenciones de nomenclatura de RHEL 7 para NIC.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-182">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="0e7fc-183">Además, se recomienda quitar los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-183">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="0e7fc-184">Los arranques gráfico y silencioso no resultan útiles en un entorno de nube, donde queremos que todos los registros se envíen al puerto serie.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-184">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="0e7fc-185">Puede dejar la opción `crashkernel` configurada si lo desea.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-185">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="0e7fc-186">Tenga en cuenta que este parámetro reduce la cantidad de memoria disponible en la máquina virtual mediante 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-186">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="0e7fc-187">Una vez que termine de editar `/etc/default/grub`, ejecute el comando siguiente para recompilar la configuración de GRUB:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-187">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="0e7fc-188">Asegúrese de que el servidor SSH se haya instalado y configurado para iniciarse en el tiempo de arranque, que suele ser el predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-188">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="0e7fc-189">Modifique `/etc/ssh/sshd_config` para que incluya la siguiente línea:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-189">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="0e7fc-190">El paquete WALinuxAgent `WALinuxAgent-<version>` se ha insertado en el repositorio de extras de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-190">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="0e7fc-191">Habilite el repositorio de extras ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-191">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="0e7fc-192">Instale el Agente de Linux de Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-192">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="0e7fc-193">No cree espacio de intercambio en el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-193">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="0e7fc-194">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio usando el disco de recursos local que se adjunta a la máquina virtual, después de que la máquina virtual se aprovisione en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-194">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="0e7fc-195">Tenga en cuenta que el disco de recursos local es un disco temporal que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-195">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="0e7fc-196">Después de instalar el agente de Linux de Azure en el paso anterior, modifique apropiadamente los parámetros siguientes en `/etc/waagent.conf`:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-196">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="0e7fc-197">Si quiere anular el registro de la suscripción, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-197">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="0e7fc-198">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-198">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="0e7fc-199">Haga clic en **Acción**  >  **Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="0e7fc-200">El VHD de Linux ya está listo para cargarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-200">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="0e7fc-201">Preparación de una máquina virtual basada en Red Hat desde KVM</span><span class="sxs-lookup"><span data-stu-id="0e7fc-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="0e7fc-202">Preparar una máquina virtual RHEL 6 desde KVM</span><span class="sxs-lookup"><span data-stu-id="0e7fc-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="0e7fc-203">Descargue la imagen KVM de RHEL 6 desde el sitio web de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-203">Download the KVM image of RHEL 6 from the Red Hat website.</span></span>

2. <span data-ttu-id="0e7fc-204">Establezca una contraseña raíz.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-204">Set a root password.</span></span>

    <span data-ttu-id="0e7fc-205">Genere una contraseña cifrada y copie el resultado del comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-205">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="0e7fc-206">Establezca una contraseña raíz con guestfish:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="0e7fc-207">Cambie el segundo campo del usuario raíz de "!!"</span><span class="sxs-lookup"><span data-stu-id="0e7fc-207">Change the second field of the root user from "!!"</span></span> <span data-ttu-id="0e7fc-208">a la contraseña cifrada.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-208">to the encrypted password.</span></span>

3. <span data-ttu-id="0e7fc-209">Cree una máquina virtual en KVM a partir de la imagen qcow2.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-209">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="0e7fc-210">Establezca el tipo de disco en **qcow2** y el modelo de dispositivo de interfaz de red virtual en **virtio**.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-210">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="0e7fc-211">Después, inicie la máquina virtual e inicie sesión como raíz.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-211">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="0e7fc-212">Cree o edite el archivo `/etc/sysconfig/network` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-212">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="0e7fc-213">Cree o edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-213">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="0e7fc-214">Mueva (o elimine) las reglas udev para impedir que se generen reglas estáticas para la interfaz Ethernet.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-214">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="0e7fc-215">Estas reglas pueden causar problemas cuando clone una máquina virtual en Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="0e7fc-216">Asegúrese de que el servicio de red se inicia en el arranque ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-216">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="0e7fc-217">Registre la suscripción de Red Hat para habilitar la instalación de paquetes desde el repositorio RHEL ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-217">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="0e7fc-218">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-218">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="0e7fc-219">Para realizar esta configuración, abra `/boot/grub/menu.lst` en un editor de texto y asegúrese de que el kernel predeterminado incluye los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-219">To do this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="0e7fc-220">Así también se asegurará de que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-220">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="0e7fc-221">Además, se recomienda quitar los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-221">In addition, we recommend that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="0e7fc-222">Los arranques gráfico y silencioso no resultan útiles en un entorno de nube, donde queremos que todos los registros se envíen al puerto serie.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-222">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="0e7fc-223">Puede dejar la opción `crashkernel` configurada si lo desea.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-223">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="0e7fc-224">Tenga en cuenta que este parámetro reduce la cantidad de memoria disponible en la máquina virtual mediante 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-224">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="0e7fc-225">RHEL 6.5 y las versiones anteriores también deben establecer el parámetro `numa=off` del kernel.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-225">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="0e7fc-226">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="0e7fc-227">Agregue módulos de Hyper-V a initramfs:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-227">Add Hyper-V modules to initramfs:</span></span>  

    <span data-ttu-id="0e7fc-228">Edite `/etc/dracut.conf` y agregue el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-228">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="0e7fc-229">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="0e7fc-230">Desinstale cloud-init:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="0e7fc-231">Asegúrese de que el servidor SSH esté instalado y configurado para iniciarse en el tiempo de arranque:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-231">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="0e7fc-232">Modifique /etc/ssh/sshd_config para que incluya las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-232">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="0e7fc-233">El paquete WALinuxAgent `WALinuxAgent-<version>` se ha insertado en el repositorio de extras de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-233">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="0e7fc-234">Habilite el repositorio de extras ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-234">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="0e7fc-235">Instale el Agente de Linux de Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-235">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="0e7fc-236">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio usando el disco de recursos local que se adjunta a la máquina virtual, después de que la máquina virtual se aprovisione en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-236">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="0e7fc-237">Tenga en cuenta que el disco de recursos local es un disco temporal que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-237">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="0e7fc-238">Después de instalar el agente de Linux de Azure en el paso anterior, modifique apropiadamente los parámetros siguientes en **/etc/waagent.conf**:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-238">After you install the Azure Linux Agent in the previous step, modify the following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="0e7fc-239">Para anular el registro de la suscripción (si es necesario), ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-239">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="0e7fc-240">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-240">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="0e7fc-241">Apague la máquina virtual en KVM.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-241">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="0e7fc-242">Convierta la imagen qcow2 al formato VHD.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-242">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="0e7fc-243">Primero convierta la imagen al formato raw:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-243">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="0e7fc-244">Asegúrese de que el tamaño de la imagen sin procesar está alineado con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-244">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="0e7fc-245">De lo contrario, redondee hacia arriba el tamaño para alinear con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-245">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="0e7fc-246">Convierta el disco sin procesar en un disco duro virtual (VHD) de tamaño fijo:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-246">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="0e7fc-247">Preparar una máquina virtual RHEL 7 desde KVM</span><span class="sxs-lookup"><span data-stu-id="0e7fc-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="0e7fc-248">Descargue la imagen KVM de RHEL 7 desde el sitio web de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-248">Download the KVM image of RHEL 7 from the Red Hat website.</span></span> <span data-ttu-id="0e7fc-249">Este procedimiento utiliza RHEL 7 como el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-249">This procedure uses RHEL 7 as the example.</span></span>

2. <span data-ttu-id="0e7fc-250">Establezca una contraseña raíz.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-250">Set a root password.</span></span>

    <span data-ttu-id="0e7fc-251">Genere una contraseña cifrada y copie el resultado del comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-251">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="0e7fc-252">Establezca una contraseña raíz con guestfish:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="0e7fc-253">Cambie el segundo campo de usuario raíz de "!!"</span><span class="sxs-lookup"><span data-stu-id="0e7fc-253">Change the second field of root user from "!!"</span></span> <span data-ttu-id="0e7fc-254">a la contraseña cifrada.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-254">to the encrypted password.</span></span>

3. <span data-ttu-id="0e7fc-255">Cree una máquina virtual en KVM a partir de la imagen qcow2.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-255">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="0e7fc-256">Establezca el tipo de disco en **qcow2** y el modelo de dispositivo de interfaz de red virtual en **virtio**.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-256">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="0e7fc-257">Después, inicie la máquina virtual e inicie sesión como raíz.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-257">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="0e7fc-258">Cree o edite el archivo `/etc/sysconfig/network` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-258">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="0e7fc-259">Cree o edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-259">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="0e7fc-260">Asegúrese de que el servicio de red se inicia en el arranque ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-260">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="0e7fc-261">Registre la suscripción de RedHat para habilitar la instalación de paquetes desde el repositorio RHEL ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-261">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="0e7fc-262">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-262">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="0e7fc-263">Para realizar esta configuración, abra `/etc/default/grub` en un editor de texto y edite el parámetro `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-263">To do this configuration, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="0e7fc-264">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="0e7fc-265">Este comando también asegura que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-265">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="0e7fc-266">El comando también desactiva las nuevas convenciones de nomenclatura de RHEL 7 para NIC.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-266">The command also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="0e7fc-267">Además, se recomienda quitar los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-267">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="0e7fc-268">Los arranques gráfico y silencioso no resultan útiles en un entorno de nube, donde queremos que todos los registros se envíen al puerto serie.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-268">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="0e7fc-269">Puede dejar la opción `crashkernel` configurada si lo desea.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-269">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="0e7fc-270">Tenga en cuenta que este parámetro reduce la cantidad de memoria disponible en la máquina virtual mediante 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-270">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="0e7fc-271">Una vez que termine de editar `/etc/default/grub`, ejecute el comando siguiente para recompilar la configuración de GRUB:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-271">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="0e7fc-272">Agregue módulos de Hyper-V a initramfs.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="0e7fc-273">Edite `/etc/dracut.conf` y agregue contenido:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="0e7fc-274">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="0e7fc-275">Desinstale cloud-init:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="0e7fc-276">Asegúrese de que el servidor SSH esté instalado y configurado para iniciarse en el tiempo de arranque:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-276">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="0e7fc-277">Modifique /etc/ssh/sshd_config para que incluya las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-277">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="0e7fc-278">El paquete WALinuxAgent `WALinuxAgent-<version>` se ha insertado en el repositorio de extras de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-278">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="0e7fc-279">Habilite el repositorio de extras ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-279">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="0e7fc-280">Instale el Agente de Linux de Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-280">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="0e7fc-281">Habilite el servicio waagent:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-281">Enable the waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="0e7fc-282">No cree espacio de intercambio en el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-282">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="0e7fc-283">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio usando el disco de recursos local que se adjunta a la máquina virtual, después de que la máquina virtual se aprovisione en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-283">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="0e7fc-284">Tenga en cuenta que el disco de recursos local es un disco temporal que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-284">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="0e7fc-285">Después de instalar el agente de Linux de Azure en el paso anterior, modifique apropiadamente los parámetros siguientes en `/etc/waagent.conf`:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-285">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="0e7fc-286">Para anular el registro de la suscripción (si es necesario), ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-286">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="0e7fc-287">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-287">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="0e7fc-288">Apague la máquina virtual en KVM.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-288">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="0e7fc-289">Convierta la imagen qcow2 al formato VHD.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-289">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="0e7fc-290">Primero convierta la imagen al formato raw:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-290">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="0e7fc-291">Asegúrese de que el tamaño de la imagen sin procesar está alineado con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-291">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="0e7fc-292">De lo contrario, redondee hacia arriba el tamaño para alinear con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-292">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="0e7fc-293">Convierta el disco sin procesar en un disco duro virtual (VHD) de tamaño fijo:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-293">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="0e7fc-294">Preparación de una máquina virtual basada en Red Hat para VMware</span><span class="sxs-lookup"><span data-stu-id="0e7fc-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="0e7fc-295">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e7fc-295">Prerequisites</span></span>
<span data-ttu-id="0e7fc-296">En esta sección se supone que ya instaló una máquina virtual RHEL en VMware.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="0e7fc-297">Para más información acerca de cómo instalar un sistema operativo en VMware, consulte [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html)(Guía de instalación de sistema operativo invitado de VMware).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-297">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="0e7fc-298">Al instalar el sistema Linux se recomienda usar las particiones estándar en lugar de un LVM, que a menudo viene de forma predeterminada en muchas instalaciones.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-298">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span></span> <span data-ttu-id="0e7fc-299">De este modo se impedirá que el nombre del LVM entre en conflicto con las máquinas virtuales clonadas, especialmente si en algún momento hace falta adjuntar un disco de sistema operativo a otra máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span></span> <span data-ttu-id="0e7fc-300">Para los discos de datos se puede utilizar LVM o RAID si así se prefiere.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="0e7fc-301">No configure una partición de intercambio en el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-301">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="0e7fc-302">Es posible configurar el agente de Linux para crear un archivo de intercambio en el disco de recursos temporal.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-302">You can configure the Linux agent to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="0e7fc-303">Puede encontrar más información al respecto en los pasos a continuación.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-303">You can find more information about this in the steps that follow.</span></span>
* <span data-ttu-id="0e7fc-304">Cuando cree el disco duro virtual, seleccione **Almacenar disco virtual como un solo archivo**.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-304">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="0e7fc-305">Preparar una máquina virtual RHEL 6 desde VMware</span><span class="sxs-lookup"><span data-stu-id="0e7fc-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="0e7fc-306">En RHEL 6, NetworkManager puede interferir en el Agente de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-306">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="0e7fc-307">Desinstale el paquete ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-307">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="0e7fc-308">Cree un archivo llamado **network** en el directorio /etc/sysconfig/ que contenga el texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-308">Create a file named **network** in the /etc/sysconfig/ directory that contains the following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="0e7fc-309">Cree o edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-309">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="0e7fc-310">Mueva (o elimine) las reglas udev para impedir que se generen reglas estáticas para la interfaz Ethernet.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-310">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="0e7fc-311">Estas reglas pueden causar problemas cuando clone una máquina virtual en Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="0e7fc-312">Asegúrese de que el servicio de red se inicia en el arranque ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-312">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="0e7fc-313">Registre la suscripción de Red Hat para habilitar la instalación de paquetes desde el repositorio RHEL ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-313">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="0e7fc-314">El paquete WALinuxAgent `WALinuxAgent-<version>` se ha insertado en el repositorio de extras de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-314">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="0e7fc-315">Habilite el repositorio de extras ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-315">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="0e7fc-316">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-316">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="0e7fc-317">Para ello, abra `/etc/default/grub` en un editor de texto y edite el parámetro `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-317">To do this, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="0e7fc-318">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="0e7fc-319">Así también se asegurará de que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-319">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="0e7fc-320">Además, se recomienda quitar los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-320">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="0e7fc-321">Los arranques gráfico y silencioso no resultan útiles en un entorno de nube, donde queremos que todos los registros se envíen al puerto serie.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-321">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="0e7fc-322">Puede dejar la opción `crashkernel` configurada si lo desea.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-322">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="0e7fc-323">Tenga en cuenta que este parámetro reduce la cantidad de memoria disponible en la máquina virtual mediante 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-323">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="0e7fc-324">Agregue módulos de Hyper-V a initramfs:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-324">Add Hyper-V modules to initramfs:</span></span>

    <span data-ttu-id="0e7fc-325">Edite `/etc/dracut.conf` y agregue el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-325">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="0e7fc-326">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="0e7fc-327">Asegúrese de que el servidor SSH se haya instalado y configurado para iniciarse en el tiempo de arranque, que suele ser el predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-327">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="0e7fc-328">Modifique `/etc/ssh/sshd_config` para que incluya la siguiente línea:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-328">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    <span data-ttu-id="0e7fc-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="0e7fc-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="0e7fc-330">Instale el Agente de Linux de Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-330">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="0e7fc-331">No cree espacio de intercambio en el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-331">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="0e7fc-332">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio usando el disco de recursos local que se adjunta a la máquina virtual, después de que la máquina virtual se aprovisione en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-332">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="0e7fc-333">Tenga en cuenta que el disco de recursos local es un disco temporal que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-333">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="0e7fc-334">Después de instalar el agente de Linux de Azure en el paso anterior, modifique apropiadamente los parámetros siguientes en `/etc/waagent.conf`:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-334">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="0e7fc-335">Para anular el registro de la suscripción (si es necesario), ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-335">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="0e7fc-336">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-336">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="0e7fc-337">Apague la máquina virtual y convierta el archivo VMDK en un archivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-337">Shut down the virtual machine, and convert the VMDK file to a .vhd file.</span></span>

    <span data-ttu-id="0e7fc-338">Primero convierta la imagen al formato raw:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-338">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="0e7fc-339">Asegúrese de que el tamaño de la imagen sin procesar está alineado con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-339">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="0e7fc-340">De lo contrario, redondee hacia arriba el tamaño para alinear con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-340">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="0e7fc-341">Convierta el disco sin procesar en un disco duro virtual (VHD) de tamaño fijo:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-341">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="0e7fc-342">Preparar una máquina virtual RHEL 7 desde VMware</span><span class="sxs-lookup"><span data-stu-id="0e7fc-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="0e7fc-343">Cree o edite el archivo `/etc/sysconfig/network` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-343">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="0e7fc-344">Cree o edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-344">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="0e7fc-345">Asegúrese de que el servicio de red se inicia en el arranque ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-345">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="0e7fc-346">Registre la suscripción de Red Hat para habilitar la instalación de paquetes desde el repositorio RHEL ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-346">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="0e7fc-347">Modifique la línea de arranque de kernel de su configuración grub para que incluya parámetros de kernel adicionales para Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-347">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="0e7fc-348">Para realizar esta modificación, abra `/etc/default/grub` en un editor de texto y edite el parámetro `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-348">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="0e7fc-349">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="0e7fc-350">Esta configuración también asegura que todos los mensajes de la consola se envían al primer puerto serie, lo que puede ayudar al soporte técnico de Azure con los problemas de depuración de errores.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-350">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="0e7fc-351">Esto también desactiva las nuevas convenciones de nomenclatura de RHEL 7 para NIC.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-351">It also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="0e7fc-352">Además, se recomienda quitar los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-352">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="0e7fc-353">Los arranques gráfico y silencioso no resultan útiles en un entorno de nube, donde queremos que todos los registros se envíen al puerto serie.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-353">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="0e7fc-354">Puede dejar la opción `crashkernel` configurada si lo desea.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-354">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="0e7fc-355">Tenga en cuenta que este parámetro reduce la cantidad de memoria disponible en la máquina virtual mediante 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-355">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="0e7fc-356">Una vez que termine de editar `/etc/default/grub`, ejecute el comando siguiente para recompilar la configuración de GRUB:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-356">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="0e7fc-357">Agregue módulos de Hyper-V a initramfs.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-357">Add Hyper-V modules to initramfs.</span></span>

    <span data-ttu-id="0e7fc-358">Edite `/etc/dracut.conf`y agregue contenido:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="0e7fc-359">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="0e7fc-360">Asegúrese de que el servidor SSH se haya instalado y configurado para iniciarse en el tiempo de arranque.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-360">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="0e7fc-361">Esta configuración es normalmente el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-361">This setting is usually the default.</span></span> <span data-ttu-id="0e7fc-362">Modifique `/etc/ssh/sshd_config` para que incluya la siguiente línea:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-362">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="0e7fc-363">El paquete WALinuxAgent `WALinuxAgent-<version>` se ha insertado en el repositorio de extras de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-363">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="0e7fc-364">Habilite el repositorio de extras ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-364">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="0e7fc-365">Instale el Agente de Linux de Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-365">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="0e7fc-366">No cree espacio de intercambio en el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-366">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="0e7fc-367">El Agente de Linux de Azure puede configurar automáticamente un espacio de intercambio usando el disco de recursos local que se adjunta a la máquina virtual, después de que la máquina virtual se aprovisione en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-367">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="0e7fc-368">Tenga en cuenta que el disco de recursos local es un disco temporal que debe vaciarse cuando la máquina virtual se desaprovisiona.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-368">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="0e7fc-369">Después de instalar el agente de Linux de Azure en el paso anterior, modifique apropiadamente los parámetros siguientes en `/etc/waagent.conf`:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-369">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

12. <span data-ttu-id="0e7fc-370">Si quiere anular el registro de la suscripción, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-370">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="0e7fc-371">Ejecute los comandos siguientes para desaprovisionar la máquina virtual y prepararla para aprovisionarse en Azure:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-371">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="0e7fc-372">Apague la máquina virtual y convierta el archivo VMDK al formato VHD.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-372">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span></span>

    <span data-ttu-id="0e7fc-373">Primero convierta la imagen al formato raw:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-373">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="0e7fc-374">Asegúrese de que el tamaño de la imagen sin procesar está alineado con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-374">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="0e7fc-375">De lo contrario, redondee hacia arriba el tamaño para alinear con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-375">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="0e7fc-376">Convierta el disco sin procesar en un disco duro virtual (VHD) de tamaño fijo:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-376">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="0e7fc-377">Preparación de una máquina virtual basada en Red Hat desde una imagen ISO con un archivo kickstart automáticamente</span><span class="sxs-lookup"><span data-stu-id="0e7fc-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="0e7fc-378">Preparar una máquina virtual RHEL 7 desde un archivo kickstart</span><span class="sxs-lookup"><span data-stu-id="0e7fc-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="0e7fc-379">Cree un archivo kickstart que incluye el contenido siguiente y guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-379">Create a kickstart file that includes the following content, and save the file.</span></span> <span data-ttu-id="0e7fc-380">Para obtener información más detallada sobre la instalación de Kickstart, consulte la [guía de instalación de Kickstart](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-380">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run the Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear the MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down the machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable the root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set the cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build the grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. <span data-ttu-id="0e7fc-381">Coloque el archivo kickstart donde el sistema de la instalación puede acceder a él.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-381">Place the kickstart file where the installation system can access it.</span></span>

3. <span data-ttu-id="0e7fc-382">En el Administrador de Hyper-V, cree una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="0e7fc-383">En la página **Conectar disco duro virtual**, seleccione **Exponer un disco duro virtual más adelante** y complete el Asistente para crear nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-383">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="0e7fc-384">Abra la configuración de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-384">Open the virtual machine settings:</span></span>

    <span data-ttu-id="0e7fc-385">a.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-385">a.</span></span>  <span data-ttu-id="0e7fc-386">Cargue un nuevo disco duro virtual en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-386">Attach a new virtual hard disk to the virtual machine.</span></span> <span data-ttu-id="0e7fc-387">Asegúrese de seleccionar **Formato VHD** y **Tamaño fijo**.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-387">Make sure to select **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="0e7fc-388">b.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-388">b.</span></span>  <span data-ttu-id="0e7fc-389">Adjunte la imagen ISO de instalación a la unidad de DVD.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-389">Attach the installation ISO to the DVD drive.</span></span>

    <span data-ttu-id="0e7fc-390">c.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-390">c.</span></span>  <span data-ttu-id="0e7fc-391">Configure el BIOS para que arranque desde el CD.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-391">Set the BIOS to boot from CD.</span></span>

5. <span data-ttu-id="0e7fc-392">Inicie la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-392">Start the virtual machine.</span></span> <span data-ttu-id="0e7fc-393">Cuando aparezca la guía de instalación, presione la tecla **Tab** para configurar las opciones de arranque.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-393">When the installation guide appears, press **Tab** to configure the boot options.</span></span>

6. <span data-ttu-id="0e7fc-394">Escriba `inst.ks=<the location of the kickstart file>` al final de las opciones de arranque y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-394">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="0e7fc-395">Espere hasta que la instalación se complete.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-395">Wait for the installation to finish.</span></span> <span data-ttu-id="0e7fc-396">Cuando haya finalizado, la máquina virtual se apagará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-396">When it's finished, the virtual machine will be shut down automatically.</span></span> <span data-ttu-id="0e7fc-397">El VHD de Linux ya está listo para cargarse en Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-397">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="0e7fc-398">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="0e7fc-398">Known issues</span></span>
### <a name="the-hyper-v-driver-could-not-be-included-in-the-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="0e7fc-399">El controlador de Hyper-V no se pudo incluir en el disco RAM inicial al usar un hipervisor de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0e7fc-399">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="0e7fc-400">En algunos casos, los instaladores de Linux pueden no incluir los controladores de Hyper-V en el disco RAM inicial (initrd o initramfs) a menos que Linux detecte que se está ejecutando un entorno de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-400">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="0e7fc-401">Cuando utilice un sistema de virtualización diferente (es decir, Virtualbox, KVM, etc.) para preparar su imagen de Linux, puede que necesite recompilar initrd para asegurarse de que al menos los módulos kernel hv_vmbus y hv_storvsc kernel están disponibles en el disco RAM inicial.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span></span> <span data-ttu-id="0e7fc-402">Esto es un problema conocido al menos en sistemas basados en el nivel superior de distribución de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-402">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="0e7fc-403">Para resolver este problema, agregue los módulos de Hyper-V en initramfs y recompilarlo:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-403">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span></span>

<span data-ttu-id="0e7fc-404">Edite `/etc/dracut.conf` y agregue el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-404">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="0e7fc-405">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="0e7fc-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="0e7fc-406">Para obtener más detalles, consulte la información sobre cómo [recompilar initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-406">For more details, see the information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e7fc-407">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e7fc-407">Next steps</span></span>
<span data-ttu-id="0e7fc-408">Ya está listo para usar el disco duro virtual de Red Hat Enterprise Linux para crear nuevas máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e7fc-408">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="0e7fc-409">Si es la primera vez que carga el archivo .vhd en Azure, consulte los pasos 2 y 3 de [Creación y carga de un disco duro virtual que contiene el sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-409">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="0e7fc-410">Para obtener información más detallada sobre los hipervisores certificados para ejecutar Red Hat Enterprise Linux, visite el [sitio web de Red Hat](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="0e7fc-410">For more details about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
