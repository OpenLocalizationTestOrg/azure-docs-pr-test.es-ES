---
title: aaaCreate y cargar un VHD de Red Hat Enterprise Linux para su uso en Azure | Documentos de Microsoft
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contiene un sistema operativo de Red Hat Linux."
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
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="345a6-103">Preparación de una máquina virtual basada en Red Hat para Azure</span><span class="sxs-lookup"><span data-stu-id="345a6-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="345a6-104">En este artículo, aprenderá cómo tooprepare una máquina virtual de Red Hat Enterprise Linux (RHEL) para su uso en Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="345a6-105">versiones de Hola de RHEL que se tratan en este artículo son 6.7 + y 7.1 +.</span><span class="sxs-lookup"><span data-stu-id="345a6-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="345a6-106">hipervisores Hola de preparación que se tratan en este artículo son la máquina virtual de Hyper-V, en función de kernel (KVM) y VMware.</span><span class="sxs-lookup"><span data-stu-id="345a6-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="345a6-107">Para más información sobre los requisitos para poder participar en el programa de acceso a la nube de Red Hat, visite el sitio [web de acceso a la nube de Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) y [Ejecución de RHEL en Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="345a6-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="345a6-108">Preparación de una máquina virtual basada en Red Hat desde el Administrador de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="345a6-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="345a6-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="345a6-109">Prerequisites</span></span>
<span data-ttu-id="345a6-110">En esta sección se da por supuesto que ya ha obtenido un archivo ISO de sitio Web de Red Hat de Hola y Hola instalado RHEL imagen tooa disco duro virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="345a6-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="345a6-111">Para obtener más información acerca de cómo toouse Administrador de Hyper-V tooinstall una imagen de sistema operativo, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="345a6-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="345a6-112">**Notas de instalación de RHEL**</span><span class="sxs-lookup"><span data-stu-id="345a6-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="345a6-113">Azure no admite el formato VHDX Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="345a6-114">Azure solo admite VHD fijo.</span><span class="sxs-lookup"><span data-stu-id="345a6-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="345a6-115">Puede usar el Administrador de Hyper-V tooconvert Hola disco tooVHD formato o puede usar el cmdlet convert-vhd de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="345a6-116">Si usa VirtualBox, seleccione **tamaño fijo** diferencia predeterminado toohello asignadas dinámicamente opción al crear el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="345a6-117">Azure solo admite máquinas virtuales de la generación 1.</span><span class="sxs-lookup"><span data-stu-id="345a6-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="345a6-118">Puede convertir una máquina virtual de generación 1 desde el formato de archivo de disco duro virtual de VHDX toohello y de disco de tamaño fijo de tooa de expansión dinámica.</span><span class="sxs-lookup"><span data-stu-id="345a6-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="345a6-119">No puede cambiar la generación de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="345a6-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="345a6-120">Para más información, consulte [¿Debería crear una máquina virtual de generación 1 o 2 en Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="345a6-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="345a6-121">tamaño máximo de Hola que se permite para hello VHD es 1.023 GB.</span><span class="sxs-lookup"><span data-stu-id="345a6-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="345a6-122">Cuando se instala el sistema operativo de Linux de hello, se recomienda que utilice particiones estándar en lugar de administrador de volúmenes lógicos (LVM), que a menudo es valor predeterminado de Hola para muchas instalaciones.</span><span class="sxs-lookup"><span data-stu-id="345a6-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="345a6-123">Este procedimiento evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si alguna vez necesita una máquina de virtual idéntica de sistema operativo disco tooanother tooattach para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="345a6-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="345a6-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos.</span><span class="sxs-lookup"><span data-stu-id="345a6-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="345a6-125">Se requiere la compatibilidad de kernel para el montaje de sistemas de archivos de formato de disco universal (UDF).</span><span class="sxs-lookup"><span data-stu-id="345a6-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="345a6-126">En el primer arranque en Azure, Hola soportes en formato UDF que está adjunto toohello invitado pasa Hola aprovisionamiento configuración toohello máquina virtual de Linux.</span><span class="sxs-lookup"><span data-stu-id="345a6-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="345a6-127">Hola agente Linux de Azure debe ser capaz de toomount Hola UDF archivo sistema tooread su configuración y aprovisionar la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="345a6-128">Versiones de kernel de Linux Hola anteriores a 2.6.37 no admiten el acceso a memoria no uniforme (NUMA) en Hyper-V con mayores tamaños de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="345a6-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="345a6-129">Este problema afecta principalmente distribuciones anteriores que usan hello en dirección ascendente kernel de Red Hat 2.6.32 y se ha corregido en RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="345a6-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="345a6-130">Sistemas que ejecutan kernels personalizados que sean más antiguos que 2.6.37 o kernels basado en RHEL que sean más antiguos que 2.6.32-504 deben establecer hello `numa=off` parámetro de arranque en línea de comandos de kernel de hello en grub.conf.</span><span class="sxs-lookup"><span data-stu-id="345a6-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="345a6-131">Para más información, consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="345a6-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="345a6-132">No configure una partición de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="345a6-133">Hola agente Linux puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="345a6-134">Para obtener más información acerca de esto puede encontrarse en hello siguiendo los pasos.</span><span class="sxs-lookup"><span data-stu-id="345a6-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="345a6-135">El tamaño de todos los VHD debe ser múltiplo de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="345a6-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="345a6-136">Preparar una máquina virtual RHEL 6 desde el Administrador de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="345a6-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="345a6-137">En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="345a6-138">Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="345a6-139">En RHEL 6, NetworkManager puede interferir con el agente de Linux de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="345a6-140">Desinstalar este paquete ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="345a6-141">Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="345a6-142">Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="345a6-143">Mover Hola udev reglas tooavoid generar reglas estáticas de interfaz Ethernet de hello (o quitar).</span><span class="sxs-lookup"><span data-stu-id="345a6-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="345a6-144">Estas reglas pueden causar problemas cuando clone una máquina virtual en Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="345a6-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="345a6-145">Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="345a6-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="345a6-146">Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="345a6-147">paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="345a6-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="345a6-148">Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="345a6-149">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="345a6-150">toodo esta modificación, abra `/boot/grub/menu.lst` en un editor de texto y asegurarse de esa kernel predeterminada de hello incluye Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="345a6-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="345a6-151">Esto también se asegurará de que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="345a6-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="345a6-152">Además, se recomienda que quite Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="345a6-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="345a6-153">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="345a6-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="345a6-154">Puede dejar hello `crashkernel` opción configurado si lo desea.</span><span class="sxs-lookup"><span data-stu-id="345a6-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="345a6-155">Tenga en cuenta que este parámetro reduce la cantidad de Hola de memoria disponible en la máquina virtual Hola 128 MB o más.</span><span class="sxs-lookup"><span data-stu-id="345a6-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="345a6-156">Esta configuración podría resultar problemática en tamaños de máquinas virtuales más pequeños.</span><span class="sxs-lookup"><span data-stu-id="345a6-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="345a6-157">RHEL versión 6.5 y versiones anterior también debe establecer hello `numa=off` parámetro de kernel.</span><span class="sxs-lookup"><span data-stu-id="345a6-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="345a6-158">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="345a6-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="345a6-159">Asegúrese de ese servidor de shell seguro (SSH) Hola se instala y configura toostart al arrancar el sistema, que normalmente es el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="345a6-160">Modificar /etc/ssh/sshd_config tooinclude Hola después de línea:</span><span class="sxs-lookup"><span data-stu-id="345a6-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="345a6-161">Instale Hola agente Linux de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="345a6-162">El paquete de instalación hello WALinuxAgent quita Hola NetworkManager y paquetes de gnome NetworkManager si no se han quitado en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="345a6-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="345a6-163">No cree el espacio de intercambio en el disco de sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="345a6-164">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="345a6-165">Tenga en cuenta que Hola local recurso disco es temporal y que puede ser vaciada cuando se canceló el aprovisionamiento de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="345a6-166">Después de instalar Agente Linux de Azure de hello en el paso anterior de hello, modifique Hola parámetros en /etc/waagent.conf siguientes correctamente:</span><span class="sxs-lookup"><span data-stu-id="345a6-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="345a6-167">Anular el registro de suscripción de hello (si es necesario) mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="345a6-168">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="345a6-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="345a6-169">Haga clic en **Acción**  >  **Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="345a6-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="345a6-170">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="345a6-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="345a6-171">Preparar una máquina virtual RHEL 7 desde el Administrador de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="345a6-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="345a6-172">En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="345a6-173">Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="345a6-174">Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="345a6-175">Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="345a6-176">Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="345a6-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="345a6-177">Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="345a6-178">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="345a6-179">toodo esta modificación, abra `/etc/default/grub` en un editor de texto y editar hello `GRUB_CMDLINE_LINUX` parámetro.</span><span class="sxs-lookup"><span data-stu-id="345a6-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="345a6-180">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="345a6-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="345a6-181">Esto también se asegurará de que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="345a6-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="345a6-182">Esta configuración también desactiva Hola nuevas RHEL 7 convenciones de nomenclatura de NIC.</span><span class="sxs-lookup"><span data-stu-id="345a6-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="345a6-183">Además, se recomienda que quite Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="345a6-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="345a6-184">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="345a6-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="345a6-185">Puede dejar hello `crashkernel` opción configurado si lo desea.</span><span class="sxs-lookup"><span data-stu-id="345a6-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="345a6-186">Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="345a6-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="345a6-187">Una vez que haya edición `/etc/default/grub`, ejecute hello después de la configuración del comando toorebuild Hola grub:</span><span class="sxs-lookup"><span data-stu-id="345a6-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="345a6-188">Asegúrese de ese servidor SSH Hola se instala y configura toostart al arrancar el sistema, que normalmente es el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="345a6-189">Modificar `/etc/ssh/sshd_config` hello tooinclude después de línea:</span><span class="sxs-lookup"><span data-stu-id="345a6-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="345a6-190">paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="345a6-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="345a6-191">Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="345a6-192">Instale Hola agente Linux de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="345a6-193">No cree el espacio de intercambio en el disco de sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="345a6-194">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="345a6-195">Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="345a6-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="345a6-196">Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:</span><span class="sxs-lookup"><span data-stu-id="345a6-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="345a6-197">Si desea que toounregister Hola suscripción, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="345a6-198">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="345a6-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="345a6-199">Haga clic en **Acción**  >  **Apagar** en el Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="345a6-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="345a6-200">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="345a6-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="345a6-201">Preparación de una máquina virtual basada en Red Hat desde KVM</span><span class="sxs-lookup"><span data-stu-id="345a6-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="345a6-202">Preparar una máquina virtual RHEL 6 desde KVM</span><span class="sxs-lookup"><span data-stu-id="345a6-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="345a6-203">Descargar imagen KVM de Hola de RHEL 6 del sitio Web de Red Hat Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="345a6-204">Establezca una contraseña raíz.</span><span class="sxs-lookup"><span data-stu-id="345a6-204">Set a root password.</span></span>

    <span data-ttu-id="345a6-205">Generar una contraseña cifrada y copiar el resultado de hello de comando hello:</span><span class="sxs-lookup"><span data-stu-id="345a6-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="345a6-206">Establezca una contraseña raíz con guestfish:</span><span class="sxs-lookup"><span data-stu-id="345a6-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="345a6-207">Segundo campo de Hola de cambio de usuario de la raíz de Hola de "!!"</span><span class="sxs-lookup"><span data-stu-id="345a6-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="345a6-208">toohello contraseña cifrada.</span><span class="sxs-lookup"><span data-stu-id="345a6-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="345a6-209">Crear una máquina virtual en KVM de imagen de qcow2 Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="345a6-210">Establecer tipo de disco de hello demasiado**qcow2**y establezca el modelo de dispositivo de interfaz de red virtual de hello demasiado**virtio**.</span><span class="sxs-lookup"><span data-stu-id="345a6-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="345a6-211">A continuación, iniciar la máquina virtual de hello e inicie sesión como raíz.</span><span class="sxs-lookup"><span data-stu-id="345a6-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="345a6-212">Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="345a6-213">Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="345a6-214">Mover Hola udev reglas tooavoid generar reglas estáticas de interfaz Ethernet de hello (o quitar).</span><span class="sxs-lookup"><span data-stu-id="345a6-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="345a6-215">Estas reglas pueden causar problemas cuando clone una máquina virtual en Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="345a6-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="345a6-216">Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="345a6-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="345a6-217">Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="345a6-218">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="345a6-219">toodo esta configuración, abra `/boot/grub/menu.lst` en un editor de texto y asegurarse de esa kernel predeterminada de hello incluye Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="345a6-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="345a6-220">Esto también se asegurará de que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="345a6-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="345a6-221">Además, se recomienda que quite Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="345a6-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="345a6-222">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="345a6-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="345a6-223">Puede dejar hello `crashkernel` opción configurado si lo desea.</span><span class="sxs-lookup"><span data-stu-id="345a6-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="345a6-224">Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="345a6-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="345a6-225">RHEL versión 6.5 y versiones anterior también debe establecer hello `numa=off` parámetro de kernel.</span><span class="sxs-lookup"><span data-stu-id="345a6-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="345a6-226">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="345a6-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="345a6-227">Agregar tooinitramfs de módulos de Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="345a6-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="345a6-228">Editar `/etc/dracut.conf`y agregue Hola siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="345a6-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="345a6-229">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="345a6-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="345a6-230">Desinstale cloud-init:</span><span class="sxs-lookup"><span data-stu-id="345a6-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="345a6-231">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema:</span><span class="sxs-lookup"><span data-stu-id="345a6-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="345a6-232">Modificar /etc/ssh/sshd_config tooinclude Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="345a6-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="345a6-233">paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="345a6-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="345a6-234">Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="345a6-235">Instale Hola agente Linux de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="345a6-236">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="345a6-237">Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="345a6-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="345a6-238">Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes **/etc/waagent.conf** correctamente:</span><span class="sxs-lookup"><span data-stu-id="345a6-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="345a6-239">Anular el registro de suscripción de hello (si es necesario) mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="345a6-240">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="345a6-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="345a6-241">Apague la máquina virtual de hello en KVM.</span><span class="sxs-lookup"><span data-stu-id="345a6-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="345a6-242">Convertir el formato de disco duro virtual de hello qcow2 imagen toohello.</span><span class="sxs-lookup"><span data-stu-id="345a6-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="345a6-243">Convertir formato de hello imagen tooraw:</span><span class="sxs-lookup"><span data-stu-id="345a6-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="345a6-244">Asegúrese de que el tamaño Hola de imagen raw de hello está alineado con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="345a6-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="345a6-245">En caso contrario, se redondea hacia arriba Hola tamaño tooalign con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="345a6-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="345a6-246">Convertir tooa de disco sin procesar de hello fijo-tamaño de disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="345a6-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="345a6-247">Preparar una máquina virtual RHEL 7 desde KVM</span><span class="sxs-lookup"><span data-stu-id="345a6-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="345a6-248">Descargar imagen KVM de Hola de RHEL 7 de sitio Web de Red Hat Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="345a6-249">Este procedimiento utiliza RHEL 7 como ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="345a6-250">Establezca una contraseña raíz.</span><span class="sxs-lookup"><span data-stu-id="345a6-250">Set a root password.</span></span>

    <span data-ttu-id="345a6-251">Generar una contraseña cifrada y copiar el resultado de hello de comando hello:</span><span class="sxs-lookup"><span data-stu-id="345a6-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="345a6-252">Establezca una contraseña raíz con guestfish:</span><span class="sxs-lookup"><span data-stu-id="345a6-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="345a6-253">Segundo campo de Hola de cambio de usuario de la raíz de "!!"</span><span class="sxs-lookup"><span data-stu-id="345a6-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="345a6-254">toohello contraseña cifrada.</span><span class="sxs-lookup"><span data-stu-id="345a6-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="345a6-255">Crear una máquina virtual en KVM de imagen de qcow2 Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="345a6-256">Establecer tipo de disco de hello demasiado**qcow2**y establezca el modelo de dispositivo de interfaz de red virtual de hello demasiado**virtio**.</span><span class="sxs-lookup"><span data-stu-id="345a6-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="345a6-257">A continuación, iniciar la máquina virtual de hello e inicie sesión como raíz.</span><span class="sxs-lookup"><span data-stu-id="345a6-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="345a6-258">Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="345a6-259">Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="345a6-260">Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="345a6-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="345a6-261">Registrar la instalación de Red Hat suscripción tooenable de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="345a6-262">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="345a6-263">toodo esta configuración, abra `/etc/default/grub` en un editor de texto y editar hello `GRUB_CMDLINE_LINUX` parámetro.</span><span class="sxs-lookup"><span data-stu-id="345a6-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="345a6-264">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="345a6-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="345a6-265">Este comando también garantiza que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="345a6-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="345a6-266">comando Hello también desactiva Hola nuevas RHEL 7 convenciones de nomenclatura de NIC.</span><span class="sxs-lookup"><span data-stu-id="345a6-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="345a6-267">Además, se recomienda que quite Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="345a6-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="345a6-268">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="345a6-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="345a6-269">Puede dejar hello `crashkernel` opción configurado si lo desea.</span><span class="sxs-lookup"><span data-stu-id="345a6-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="345a6-270">Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="345a6-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="345a6-271">Una vez que haya edición `/etc/default/grub`, ejecute hello después de la configuración del comando toorebuild Hola grub:</span><span class="sxs-lookup"><span data-stu-id="345a6-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="345a6-272">Agregue módulos de Hyper-V a initramfs.</span><span class="sxs-lookup"><span data-stu-id="345a6-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="345a6-273">Edite `/etc/dracut.conf` y agregue contenido:</span><span class="sxs-lookup"><span data-stu-id="345a6-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="345a6-274">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="345a6-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="345a6-275">Desinstale cloud-init:</span><span class="sxs-lookup"><span data-stu-id="345a6-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="345a6-276">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema:</span><span class="sxs-lookup"><span data-stu-id="345a6-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="345a6-277">Modificar /etc/ssh/sshd_config tooinclude Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="345a6-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="345a6-278">paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="345a6-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="345a6-279">Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="345a6-280">Instale Hola agente Linux de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="345a6-281">Habilitar hello waagent servicio:</span><span class="sxs-lookup"><span data-stu-id="345a6-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="345a6-282">No cree el espacio de intercambio en el disco de sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="345a6-283">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="345a6-284">Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="345a6-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="345a6-285">Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:</span><span class="sxs-lookup"><span data-stu-id="345a6-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="345a6-286">Anular el registro de suscripción de hello (si es necesario) mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="345a6-287">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="345a6-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="345a6-288">Apague la máquina virtual de hello en KVM.</span><span class="sxs-lookup"><span data-stu-id="345a6-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="345a6-289">Convertir el formato de disco duro virtual de hello qcow2 imagen toohello.</span><span class="sxs-lookup"><span data-stu-id="345a6-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="345a6-290">Convertir formato de hello imagen tooraw:</span><span class="sxs-lookup"><span data-stu-id="345a6-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="345a6-291">Asegúrese de que el tamaño Hola de imagen raw de hello está alineado con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="345a6-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="345a6-292">En caso contrario, se redondea hacia arriba Hola tamaño tooalign con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="345a6-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="345a6-293">Convertir tooa de disco sin procesar de hello fijo-tamaño de disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="345a6-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="345a6-294">Preparación de una máquina virtual basada en Red Hat para VMware</span><span class="sxs-lookup"><span data-stu-id="345a6-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="345a6-295">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="345a6-295">Prerequisites</span></span>
<span data-ttu-id="345a6-296">En esta sección se supone que ya instaló una máquina virtual RHEL en VMware.</span><span class="sxs-lookup"><span data-stu-id="345a6-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="345a6-297">Para obtener más información acerca de cómo tooinstall un sistema operativo en VMware, consulte [Guía de instalación de sistema operativo invitado de VMware](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="345a6-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="345a6-298">Cuando se instala el sistema operativo de Linux de hello, recomendamos que utilice particiones estándar en lugar de LVM, que suele ser predeterminado de Hola para muchas instalaciones.</span><span class="sxs-lookup"><span data-stu-id="345a6-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="345a6-299">Esto evitará LVM nombre entra en conflicto con la máquina virtual clonada, especialmente si un disco del sistema operativo alguna vez necesita toobe adjunta tooanother virtual machine para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="345a6-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="345a6-300">Para los discos de datos se puede utilizar LVM o RAID si así se prefiere.</span><span class="sxs-lookup"><span data-stu-id="345a6-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="345a6-301">No configure una partición de intercambio en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="345a6-302">Puede configurar Hola Linux agente toocreate un archivo de intercambio en el disco de recursos temporal Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="345a6-303">Puede buscar más información al respecto en los pasos de Hola que siguen.</span><span class="sxs-lookup"><span data-stu-id="345a6-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="345a6-304">Cuando se crea el disco duro virtual de hello, seleccione **disco virtual del almacén como un único archivo**.</span><span class="sxs-lookup"><span data-stu-id="345a6-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="345a6-305">Preparar una máquina virtual RHEL 6 desde VMware</span><span class="sxs-lookup"><span data-stu-id="345a6-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="345a6-306">En RHEL 6, NetworkManager puede interferir con el agente de Linux de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="345a6-307">Desinstalar este paquete ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="345a6-308">Cree un archivo denominado **red** en hello/etc/sysconfig/directorio que contiene Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="345a6-309">Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="345a6-310">Mover Hola udev reglas tooavoid generar reglas estáticas de interfaz Ethernet de hello (o quitar).</span><span class="sxs-lookup"><span data-stu-id="345a6-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="345a6-311">Estas reglas pueden causar problemas cuando clone una máquina virtual en Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="345a6-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="345a6-312">Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="345a6-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="345a6-313">Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="345a6-314">paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="345a6-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="345a6-315">Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="345a6-316">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="345a6-317">toodo, abra `/etc/default/grub` en un editor de texto y editar hello `GRUB_CMDLINE_LINUX` parámetro.</span><span class="sxs-lookup"><span data-stu-id="345a6-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="345a6-318">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="345a6-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="345a6-319">Esto también se asegurará de que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="345a6-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="345a6-320">Además, se recomienda que quite Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="345a6-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="345a6-321">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="345a6-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="345a6-322">Puede dejar hello `crashkernel` opción configurado si lo desea.</span><span class="sxs-lookup"><span data-stu-id="345a6-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="345a6-323">Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="345a6-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="345a6-324">Agregar tooinitramfs de módulos de Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="345a6-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="345a6-325">Editar `/etc/dracut.conf`y agregue Hola siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="345a6-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="345a6-326">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="345a6-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="345a6-327">Asegúrese de ese servidor SSH Hola se instala y configura toostart al arrancar el sistema, que normalmente es el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="345a6-328">Modificar `/etc/ssh/sshd_config` hello tooinclude después de línea:</span><span class="sxs-lookup"><span data-stu-id="345a6-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="345a6-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="345a6-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="345a6-330">Instale Hola agente Linux de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="345a6-331">No cree el espacio de intercambio en el disco de sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="345a6-332">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="345a6-333">Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="345a6-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="345a6-334">Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:</span><span class="sxs-lookup"><span data-stu-id="345a6-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="345a6-335">Anular el registro de suscripción de hello (si es necesario) mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="345a6-336">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="345a6-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="345a6-337">Apagar la máquina virtual de Hola y convertir el archivo .vhd de hello VMDK archivo tooa.</span><span class="sxs-lookup"><span data-stu-id="345a6-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="345a6-338">Convertir formato de hello imagen tooraw:</span><span class="sxs-lookup"><span data-stu-id="345a6-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="345a6-339">Asegúrese de que el tamaño Hola de imagen raw de hello está alineado con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="345a6-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="345a6-340">En caso contrario, se redondea hacia arriba Hola tamaño tooalign con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="345a6-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="345a6-341">Convertir tooa de disco sin procesar de hello fijo-tamaño de disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="345a6-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="345a6-342">Preparar una máquina virtual RHEL 7 desde VMware</span><span class="sxs-lookup"><span data-stu-id="345a6-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="345a6-343">Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="345a6-344">Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="345a6-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="345a6-345">Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="345a6-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="345a6-346">Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="345a6-347">Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="345a6-348">toodo esta modificación, abra `/etc/default/grub` en un editor de texto y editar hello `GRUB_CMDLINE_LINUX` parámetro.</span><span class="sxs-lookup"><span data-stu-id="345a6-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="345a6-349">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="345a6-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="345a6-350">Esta configuración también garantiza que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.</span><span class="sxs-lookup"><span data-stu-id="345a6-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="345a6-351">También desactiva Hola nuevas RHEL 7 convenciones de nomenclatura para la NIC.</span><span class="sxs-lookup"><span data-stu-id="345a6-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="345a6-352">Además, se recomienda que quite Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="345a6-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="345a6-353">Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.</span><span class="sxs-lookup"><span data-stu-id="345a6-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="345a6-354">Puede dejar hello `crashkernel` opción configurado si lo desea.</span><span class="sxs-lookup"><span data-stu-id="345a6-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="345a6-355">Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.</span><span class="sxs-lookup"><span data-stu-id="345a6-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="345a6-356">Una vez que haya edición `/etc/default/grub`, ejecute hello después de la configuración del comando toorebuild Hola grub:</span><span class="sxs-lookup"><span data-stu-id="345a6-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="345a6-357">Agregar tooinitramfs de módulos de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="345a6-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="345a6-358">Edite `/etc/dracut.conf`y agregue contenido:</span><span class="sxs-lookup"><span data-stu-id="345a6-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="345a6-359">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="345a6-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="345a6-360">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="345a6-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="345a6-361">Este valor suele ser predeterminada Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-361">This setting is usually hello default.</span></span> <span data-ttu-id="345a6-362">Modificar `/etc/ssh/sshd_config` hello tooinclude después de línea:</span><span class="sxs-lookup"><span data-stu-id="345a6-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="345a6-363">paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="345a6-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="345a6-364">Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="345a6-365">Instale Hola agente Linux de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="345a6-366">No cree el espacio de intercambio en el disco de sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="345a6-367">Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="345a6-368">Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="345a6-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="345a6-369">Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:</span><span class="sxs-lookup"><span data-stu-id="345a6-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="345a6-370">Si desea que toounregister Hola suscripción, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="345a6-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="345a6-371">Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:</span><span class="sxs-lookup"><span data-stu-id="345a6-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="345a6-372">Apagar la máquina virtual de Hola y convertir el formato de disco duro virtual de hello VMDK archivo toohello.</span><span class="sxs-lookup"><span data-stu-id="345a6-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="345a6-373">Convertir formato de hello imagen tooraw:</span><span class="sxs-lookup"><span data-stu-id="345a6-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="345a6-374">Asegúrese de que el tamaño Hola de imagen raw de hello está alineado con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="345a6-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="345a6-375">En caso contrario, se redondea hacia arriba Hola tamaño tooalign con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="345a6-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="345a6-376">Convertir tooa de disco sin procesar de hello fijo-tamaño de disco duro virtual:</span><span class="sxs-lookup"><span data-stu-id="345a6-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="345a6-377">Preparación de una máquina virtual basada en Red Hat desde una imagen ISO con un archivo kickstart automáticamente</span><span class="sxs-lookup"><span data-stu-id="345a6-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="345a6-378">Preparar una máquina virtual RHEL 7 desde un archivo kickstart</span><span class="sxs-lookup"><span data-stu-id="345a6-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="345a6-379">Crear un archivo que incluye Hola siguen contenido y guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="345a6-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="345a6-380">Para obtener más información acerca de la instalación de comenzar, vea hello [ofrecen Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="345a6-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
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

        # Clear hello MBR
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

        # Power down hello machine after install
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

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
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

2. <span data-ttu-id="345a6-381">Coloque el archivo de Hola que puedan acceder de sistema de la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="345a6-382">En el Administrador de Hyper-V, cree una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="345a6-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="345a6-383">En hello **conectar disco duro Virtual** página, seleccione **adjuntar un disco duro virtual más tarde**y Hola completo Asistente para nueva máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="345a6-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="345a6-384">Abra Configuración de máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="345a6-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="345a6-385">a.</span><span class="sxs-lookup"><span data-stu-id="345a6-385">a.</span></span>  <span data-ttu-id="345a6-386">Adjuntar una nueva máquina virtual de toohello de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="345a6-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="345a6-387">Asegúrese de que tooselect **formato VHD** y **tamaño fijo**.</span><span class="sxs-lookup"><span data-stu-id="345a6-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="345a6-388">b.</span><span class="sxs-lookup"><span data-stu-id="345a6-388">b.</span></span>  <span data-ttu-id="345a6-389">Adjuntar instalación Hola unidad de DVD de ISO toohello.</span><span class="sxs-lookup"><span data-stu-id="345a6-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="345a6-390">c.</span><span class="sxs-lookup"><span data-stu-id="345a6-390">c.</span></span>  <span data-ttu-id="345a6-391">Establecer Hola BIOS tooboot desde el CD.</span><span class="sxs-lookup"><span data-stu-id="345a6-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="345a6-392">Inicie la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-392">Start hello virtual machine.</span></span> <span data-ttu-id="345a6-393">Cuando aparezca la Guía de instalación de hello, presione **ficha** opciones de arranque de tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="345a6-394">ENTRAR `inst.ks=<hello location of hello kickstart file>` final Hola de opciones de arranque de hello y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="345a6-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="345a6-395">Espere Hola instalación toofinish.</span><span class="sxs-lookup"><span data-stu-id="345a6-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="345a6-396">Cuando haya finalizado, máquina virtual de Hola se apagará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="345a6-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="345a6-397">El VHD de Linux está ahora listo toobe había cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="345a6-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="345a6-398">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="345a6-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="345a6-399">no se pudieron incluir controladores de Hyper-V de Hello en disco RAM inicial de hello cuando se usa un hipervisor de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="345a6-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="345a6-400">En algunos casos, instaladores de Linux no podrían incluir controladores de Hola para Hyper-V en hello inicial disco RAM (initrd o initramfs) a menos que detecte de Linux que se está ejecutando en un entorno de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="345a6-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="345a6-401">Cuando se usa un tooprepare del sistema (es decir, Virtualbox, Xen, etc.) de virtualización distinto la imagen de Linux, deberá toorebuild initrd tooensure que al menos Hola hv_vmbus y los módulos de kernel hv_storvsc están disponibles en el disco RAM inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="345a6-402">Esto es un problema conocido al menos en sistemas que se basan en la distribución de Red Hat de nivel superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="345a6-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="345a6-403">tooresolve este problema, agregue tooinitramfs de módulos de Hyper-V y vuelva a generarlo:</span><span class="sxs-lookup"><span data-stu-id="345a6-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="345a6-404">Editar `/etc/dracut.conf`y agregue Hola siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="345a6-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="345a6-405">Recompile initramfs:</span><span class="sxs-lookup"><span data-stu-id="345a6-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="345a6-406">Para obtener más información, vea la información de hello sobre [volver a generar initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="345a6-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="345a6-407">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="345a6-407">Next steps</span></span>
<span data-ttu-id="345a6-408">Se está ahora listo toouse sus Red Hat Enterprise Linux disco duro virtual toocreate nuevas máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="345a6-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="345a6-409">Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="345a6-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="345a6-410">Para obtener más detalles sobre los hipervisores de Hola que están certificación toorun Red Hat Enterprise Linux, consulte [sitio Web de Red Hat hello](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="345a6-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
