---
title: "Optimización del rendimiento de MySQL en Linux | Microsoft Docs"
description: "Aprenda a optimizar MySQL ejecutado en una máquina virtual (VM) de Azure con Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 8f2ec884fa98e989448ac11675e71f39aa21fa7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="16f42-103">Optimización del rendimiento de MySQL en máquinas virtuales de Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="16f42-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="16f42-104">Existen muchos factores que afectan al rendimiento de MySQL en Azure, tanto en la configuración de selección de software y hardware virtual.</span><span class="sxs-lookup"><span data-stu-id="16f42-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="16f42-105">Este artículo se centra en la optimización del rendimiento a través del almacenamiento, el sistema y las configuraciones de base de datos.</span><span class="sxs-lookup"><span data-stu-id="16f42-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16f42-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico.</span><span class="sxs-lookup"><span data-stu-id="16f42-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="16f42-107">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="16f42-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="16f42-108">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="16f42-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="16f42-109">Para más información sobre las optimizaciones de máquinas virtuales Linux con el modelo de Resource Manager, consulte [Optimización de la máquina virtual Linux en Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16f42-109">For information about Linux VM optimizations with the Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="16f42-110">Uso de RAID en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="16f42-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="16f42-111">El almacenamiento es el factor clave que afecta al rendimiento de la base de datos en entornos de nube.</span><span class="sxs-lookup"><span data-stu-id="16f42-111">Storage is the key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="16f42-112">En comparación con un solo disco, RAID puede proporcionar un acceso más rápido gracias a la simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="16f42-112">Compared to a single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="16f42-113">Para más información, consulte [Niveles RAID estándar](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="16f42-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="16f42-114">El rendimiento de E/S de disco, así como el tiempo de respuesta de las E/S pueden mejorarse con RAID.</span><span class="sxs-lookup"><span data-stu-id="16f42-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="16f42-115">Nuestras pruebas de laboratorio indican que es posible duplicar el rendimiento de E/S de disco. Asimismo, es posible reducir a la mitad el tiempo de respuesta de E/S de media cuando se duplica el número de discos RAID (de 2 a 4, de 4 a 8, etc.).</span><span class="sxs-lookup"><span data-stu-id="16f42-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when the number of RAID disks is doubled (from two to four, four to eight, etc.).</span></span> <span data-ttu-id="16f42-116">Consulte el [Apéndice A](#AppendixA) para más información.</span><span class="sxs-lookup"><span data-stu-id="16f42-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="16f42-117">Además de las E/S de disco, el rendimiento de MySQL mejora al aumentar el nivel de RAID.</span><span class="sxs-lookup"><span data-stu-id="16f42-117">In addition to disk I/O, MySQL performance improves when you increase the RAID level.</span></span>  <span data-ttu-id="16f42-118">Consulte el [Apéndice B](#AppendixB) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="16f42-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="16f42-119">También puede que desee considerar el tamaño del fragmento.</span><span class="sxs-lookup"><span data-stu-id="16f42-119">You might also want to consider the chunk size.</span></span> <span data-ttu-id="16f42-120">En general, cuando el tamaño de fragmento es mayor, obtiene una menor sobrecarga, especialmente para las operaciones de escritura de mayor envergadura.</span><span class="sxs-lookup"><span data-stu-id="16f42-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="16f42-121">Sin embargo, si el tamaño del fragmento es demasiado grande, podría agregar una sobrecarga adicional que impida que aproveche las ventajas de RAID.</span><span class="sxs-lookup"><span data-stu-id="16f42-121">However, when the chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="16f42-122">El tamaño predeterminado actual es de 512 KB. Este es el tamaño óptimo para los entornos de producción más generales.</span><span class="sxs-lookup"><span data-stu-id="16f42-122">The current default size is 512 KB, which is proven to be optimal for most general production environments.</span></span> <span data-ttu-id="16f42-123">Consulte el [Apéndice C](#AppendixC) para más información.</span><span class="sxs-lookup"><span data-stu-id="16f42-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="16f42-124">Existen límites en cuanto al número de discos que puede agregar para los distintos tipos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="16f42-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="16f42-125">Estos límites se detallan en [Tamaños de máquinas virtuales y servicios en la nube de Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="16f42-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="16f42-126">Necesitará 4 discos de datos conectados para seguir el ejemplo de RAID que se describe en este artículo, aunque puede optar por configurar RAID con menos discos.</span><span class="sxs-lookup"><span data-stu-id="16f42-126">You will need four attached data disks to follow the RAID example in this article, although you can choose to set up RAID with fewer disks.</span></span>  

<span data-ttu-id="16f42-127">En este artículo se da por supuesto que ya ha creado una máquina virtual Linux y que MYSQL está instalado y configurado.</span><span class="sxs-lookup"><span data-stu-id="16f42-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="16f42-128">Para más información sobre cómo empezar, consulte Instalación de MySQL en Azure.</span><span class="sxs-lookup"><span data-stu-id="16f42-128">For more information on getting started, see How to install MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="16f42-129">Configuración de RAID en Azure</span><span class="sxs-lookup"><span data-stu-id="16f42-129">Set up RAID on Azure</span></span>
<span data-ttu-id="16f42-130">Los siguientes pasos muestran cómo crear RAID en Azure mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="16f42-130">The following steps show how to create RAID on Azure by using the Azure portal.</span></span> <span data-ttu-id="16f42-131">También puede configurar RAID mediante scripts de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16f42-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="16f42-132">En este ejemplo, configuraremos RAID 0 con 4 discos.</span><span class="sxs-lookup"><span data-stu-id="16f42-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-to-your-virtual-machine"></a><span data-ttu-id="16f42-133">Incorporación de un disco de datos a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="16f42-133">Add a data disk to your virtual machine</span></span>
<span data-ttu-id="16f42-134">En Azure Portal, vaya al panel y seleccione la máquina virtual a la que quiere agregar un disco de datos.</span><span class="sxs-lookup"><span data-stu-id="16f42-134">In the Azure portal, go to the dashboard and select the virtual machine to which you want to add a data disk.</span></span> <span data-ttu-id="16f42-135">En este ejemplo, la máquina virtual es mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="16f42-135">In this example, the virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="16f42-136">Haga clic en **Discos** y luego haga clic en **Asociar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="16f42-136">Click **Disks** and then click **Attach New**.</span></span>

![Agregar disco a máquinas virtuales](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="16f42-138">Cree un nuevo disco de 500 GB.</span><span class="sxs-lookup"><span data-stu-id="16f42-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="16f42-139">Asegúrese de que **Preferencia de caché de host** esté establecida en **Ninguna**.</span><span class="sxs-lookup"><span data-stu-id="16f42-139">Make sure that **Host Cache Preference** is set to **None**.</span></span>  <span data-ttu-id="16f42-140">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="16f42-140">When you're finished, click **OK**.</span></span>

![Acoplar disco vacío](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="16f42-142">Esta acción agrega un disco vacío a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="16f42-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="16f42-143">Repita este paso tres veces más para que disponga de 4 discos de datos para RAID.</span><span class="sxs-lookup"><span data-stu-id="16f42-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="16f42-144">Puede ver las unidades agregadas en la máquina virtual examinando el registro de mensajes del kernel.</span><span class="sxs-lookup"><span data-stu-id="16f42-144">You can see the added drives in the virtual machine by looking at the kernel message log.</span></span> <span data-ttu-id="16f42-145">Por ejemplo, para ver esto en Ubuntu, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="16f42-145">For example, to see this on Ubuntu, use the following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-the-additional-disks"></a><span data-ttu-id="16f42-146">Crear RAID con los discos adicionales</span><span class="sxs-lookup"><span data-stu-id="16f42-146">Create RAID with the additional disks</span></span>
<span data-ttu-id="16f42-147">Los siguientes pasos describen cómo [configurar RAID de software en Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16f42-147">The following steps describe how to [configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="16f42-148">Si usa el sistema de archivos XFS, siga los pasos siguientes después de haber creado RAID.</span><span class="sxs-lookup"><span data-stu-id="16f42-148">If you are using the XFS file system, execute the following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="16f42-149">Para instalar XFS en Debian, Ubuntu o Linux Mint, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="16f42-149">To install XFS on Debian, Ubuntu, or Linux Mint, use the following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="16f42-150">Para instalar XFS en Fedora, CentOS o RHEL, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="16f42-150">To install XFS on Fedora, CentOS, or RHEL, use the following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="16f42-151">Configurar una nueva ruta de acceso de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="16f42-151">Set up a new storage path</span></span>
<span data-ttu-id="16f42-152">Use el comando siguiente para configurar una nueva ruta de acceso de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="16f42-152">Use the following command to set up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-the-original-data-to-the-new-storage-path"></a><span data-ttu-id="16f42-153">Copiar los datos originales en la nueva ruta de acceso de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="16f42-153">Copy the original data to the new storage path</span></span>
<span data-ttu-id="16f42-154">Use el comando siguiente para copiar los datos en la nueva ruta de acceso de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="16f42-154">Use the following command to copy data to the new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-the-data-disk"></a><span data-ttu-id="16f42-155">Modificar permisos para que MySQL pueda tener acceso (lectura y escritura) al disco de datos</span><span class="sxs-lookup"><span data-stu-id="16f42-155">Modify permissions so MySQL can access (read and write) the data disk</span></span>
<span data-ttu-id="16f42-156">Use el siguiente comando para modificar los permisos:</span><span class="sxs-lookup"><span data-stu-id="16f42-156">Use the following command to modify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-the-disk-io-scheduling-algorithm"></a><span data-ttu-id="16f42-157">Ajuste el algoritmo de programación de E/S de disco</span><span class="sxs-lookup"><span data-stu-id="16f42-157">Adjust the disk I/O scheduling algorithm</span></span>
<span data-ttu-id="16f42-158">Linux implementa cuatro tipos de algoritmos de programación de E/S:</span><span class="sxs-lookup"><span data-stu-id="16f42-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="16f42-159">Algoritmo NOOP (sin operación)</span><span class="sxs-lookup"><span data-stu-id="16f42-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="16f42-160">Algoritmo de fecha límite (fecha límite)</span><span class="sxs-lookup"><span data-stu-id="16f42-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="16f42-161">Algoritmo de cola justa (CFQ)</span><span class="sxs-lookup"><span data-stu-id="16f42-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="16f42-162">Algoritmo de período de presupuesto (antelación)</span><span class="sxs-lookup"><span data-stu-id="16f42-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="16f42-163">Puede seleccionar distintos programadores de E/S en distintos escenarios para optimizar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="16f42-163">You can select different I/O schedulers under different scenarios to optimize performance.</span></span> <span data-ttu-id="16f42-164">En un entorno de acceso completamente aleatorio, no hay una diferencia importante entre los algoritmos CFQ y de fecha límite en cuanto a rendimiento.</span><span class="sxs-lookup"><span data-stu-id="16f42-164">In a completely random access environment, there is not a significant difference between the CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="16f42-165">Se recomienda establecer el entorno de base de datos MySQL en Fecha límite para disponer de mayor estabilidad.</span><span class="sxs-lookup"><span data-stu-id="16f42-165">We recommend that you set the MySQL database environment to Deadline for stability.</span></span> <span data-ttu-id="16f42-166">Si hay un elevado volumen de E/S secuenciales, el algoritmo CFQ puede reducir el rendimiento de las E/S de disco.</span><span class="sxs-lookup"><span data-stu-id="16f42-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="16f42-167">Para SSD y otros equipos, el algoritmo NOOP o de Fecha límite puede ofrecer mayor rendimiento que el programador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="16f42-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than the default scheduler.</span></span>   

<span data-ttu-id="16f42-168">Antes del kernel 2.5, el algoritmo de programación de E/S predeterminado era el algoritmo de Fecha límite.</span><span class="sxs-lookup"><span data-stu-id="16f42-168">Prior to the kernel 2.5, the default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="16f42-169">A partir del kernel 2.6.18, CFQ se convirtió en el algoritmo de programación de E/S predeterminado.</span><span class="sxs-lookup"><span data-stu-id="16f42-169">Starting with the kernel 2.6.18, CFQ became the default I/O scheduling algorithm.</span></span>  <span data-ttu-id="16f42-170">Puede especificar este valor en el tiempo de arranque de kernel, o bien modificar esta configuración de forma dinámica cuando el sistema se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="16f42-170">You can specify this setting at kernel boot time or dynamically modify this setting when the system is running.</span></span>  

<span data-ttu-id="16f42-171">En el ejemplo siguiente se muestra cómo comprobar y establecer el programador predeterminado con el algoritmo NOOP en la familia de distribución Debian.</span><span class="sxs-lookup"><span data-stu-id="16f42-171">The following example demonstrates how to check and set the default scheduler to the NOOP algorithm in the Debian distribution family.</span></span>  

### <a name="view-the-current-io-scheduler"></a><span data-ttu-id="16f42-172">Visualización del programador de E/S actual</span><span class="sxs-lookup"><span data-stu-id="16f42-172">View the current I/O scheduler</span></span>
<span data-ttu-id="16f42-173">Ejecute el comando siguiente para ver el programador:</span><span class="sxs-lookup"><span data-stu-id="16f42-173">To view the scheduler run the following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="16f42-174">Se mostrará el la salida siguiente, que indica cuál es el programador actual:</span><span class="sxs-lookup"><span data-stu-id="16f42-174">You will see following output, which indicates the current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-the-current-device-devsda-of-the-io-scheduling-algorithm"></a><span data-ttu-id="16f42-175">Cambio del dispositivo actual (/dev/sda) del algoritmo de programación de E/S</span><span class="sxs-lookup"><span data-stu-id="16f42-175">Change the current device (/dev/sda) of the I/O scheduling algorithm</span></span>
<span data-ttu-id="16f42-176">Ejecute los comandos siguientes para cambiar el dispositivo actual:</span><span class="sxs-lookup"><span data-stu-id="16f42-176">Run the following commands to change the current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="16f42-177">Establecer este valor solo para /dev/sda no es útil.</span><span class="sxs-lookup"><span data-stu-id="16f42-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="16f42-178">Debe establecerse en todos los discos de datos en los que reside la base de datos.</span><span class="sxs-lookup"><span data-stu-id="16f42-178">It must be set on all data disks where the database resides.</span></span>  
>
>

<span data-ttu-id="16f42-179">Debería mostrarse el resultado siguiente, que indica que grub.cfg se ha vuelto a compilar correctamente y que se ha actualizado el programador predeterminado a NOOP:</span><span class="sxs-lookup"><span data-stu-id="16f42-179">You should see the following output, indicating that grub.cfg has been rebuilt successfully and that the default scheduler has been updated to NOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="16f42-180">Para la familia de distribución Red Hat, solo necesita el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="16f42-180">For the Red Hat distribution family, you need only the following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="16f42-181">Configurar las opciones de las operaciones de archivos de sistema</span><span class="sxs-lookup"><span data-stu-id="16f42-181">Configure system file operations settings</span></span>
<span data-ttu-id="16f42-182">Una práctica recomendada consiste en deshabilitar la característica de registro *atime* en el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="16f42-182">One best practice is to disable the *atime* logging feature on the file system.</span></span> <span data-ttu-id="16f42-183">Atime representa la última hora de acceso al archivo.</span><span class="sxs-lookup"><span data-stu-id="16f42-183">Atime is the last file access time.</span></span> <span data-ttu-id="16f42-184">Cada vez que se tiene acceso a un archivo, el sistema de archivos registra la marca de tiempo en el registro.</span><span class="sxs-lookup"><span data-stu-id="16f42-184">Whenever a file is accessed, the file system records the timestamp in the log.</span></span> <span data-ttu-id="16f42-185">Sin embargo, esta información no suele usarse.</span><span class="sxs-lookup"><span data-stu-id="16f42-185">However, this information is rarely used.</span></span> <span data-ttu-id="16f42-186">Por lo tanto, se puede deshabilitar si no es necesaria. Esto reducirá el tiempo total de acceso al disco.</span><span class="sxs-lookup"><span data-stu-id="16f42-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="16f42-187">Para deshabilitar el registro de atime, deberá modificar el archivo /etc/ fstab de la configuración del sistema y agregar la opción **noatime** .</span><span class="sxs-lookup"><span data-stu-id="16f42-187">To disable atime logging, you need to modify the file system configuration file /etc/ fstab and add the **noatime** option.</span></span>  

<span data-ttu-id="16f42-188">Por ejemplo, edite el archivo vim /etc/fstab agregando la opción noatime tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="16f42-188">For example, edit the vim /etc/fstab file, adding the noatime as shown in the following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by the Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add the “noatime” option below to disable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="16f42-189">A continuación, vuelva a montar el sistema de archivos con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="16f42-189">Then, remount the file system with the following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="16f42-190">Pruebe el resultado modificado.</span><span class="sxs-lookup"><span data-stu-id="16f42-190">Test the modified result.</span></span> <span data-ttu-id="16f42-191">Cuando se modifica el archivo de prueba, la hora de acceso no se actualiza.</span><span class="sxs-lookup"><span data-stu-id="16f42-191">When you modify the test file, the access time is not updated.</span></span> <span data-ttu-id="16f42-192">Los ejemplos siguientes muestran cómo se ve el código antes y después de la modificación.</span><span class="sxs-lookup"><span data-stu-id="16f42-192">The following examples show what the code looks like before and after modification.</span></span>

<span data-ttu-id="16f42-193">Antes:</span><span class="sxs-lookup"><span data-stu-id="16f42-193">Before:</span></span>        

![El código antes de la modificación del acceso.][5]

<span data-ttu-id="16f42-195">Después:</span><span class="sxs-lookup"><span data-stu-id="16f42-195">After:</span></span>

![El código después de la modificación del acceso.][6]

## <a name="increase-the-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="16f42-197">Aumentar el número máximo de identificadores del sistema para incrementar la simultaneidad</span><span class="sxs-lookup"><span data-stu-id="16f42-197">Increase the maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="16f42-198">MySQL es una base de datos de alta simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="16f42-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="16f42-199">El número predeterminado de identificadores simultáneos es de 1024 para Linux. Esta cantidad no siempre es suficiente.</span><span class="sxs-lookup"><span data-stu-id="16f42-199">The default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="16f42-200">Siga los pasos siguientes para aumentar los identificadores simultáneos máximos del sistema para permitir una elevada concurrencia de MySQL.</span><span class="sxs-lookup"><span data-stu-id="16f42-200">Use the following steps to increase the maximum concurrent handles of the system to support high concurrency of MySQL.</span></span>

### <a name="modify-the-limitsconf-file"></a><span data-ttu-id="16f42-201">Modificar el archivo limits.conf</span><span class="sxs-lookup"><span data-stu-id="16f42-201">Modify the limits.conf file</span></span>
<span data-ttu-id="16f42-202">Para aumentar los identificadores simultáneos máximos permitidos, agregue las cuatro líneas siguientes al archivo /etc/security/limits.conf.</span><span class="sxs-lookup"><span data-stu-id="16f42-202">To increase the maximum allowed concurrent handles, add the following four lines in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="16f42-203">Tenga en cuenta que 65536 es el número máximo que puede admitir el sistema.</span><span class="sxs-lookup"><span data-stu-id="16f42-203">Note that 65536 is the maximum number that the system can support.</span></span>   

    * <span data-ttu-id="16f42-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="16f42-204">soft nofile 65536</span></span>
    * <span data-ttu-id="16f42-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="16f42-205">hard nofile 65536</span></span>
    * <span data-ttu-id="16f42-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="16f42-206">soft nproc 65536</span></span>
    * <span data-ttu-id="16f42-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="16f42-207">hard nproc 65536</span></span>

### <a name="update-the-system-for-the-new-limits"></a><span data-ttu-id="16f42-208">Actualizar el sistema con los nuevos límites</span><span class="sxs-lookup"><span data-stu-id="16f42-208">Update the system for the new limits</span></span>
<span data-ttu-id="16f42-209">Ejecute los comandos siguientes para actualizar el sistema:</span><span class="sxs-lookup"><span data-stu-id="16f42-209">To update the system, run the following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-the-limits-are-updated-at-boot-time"></a><span data-ttu-id="16f42-210">Asegurarse de que los límites se actualizan durante el arranque</span><span class="sxs-lookup"><span data-stu-id="16f42-210">Ensure that the limits are updated at boot time</span></span>
<span data-ttu-id="16f42-211">Escriba los siguientes comandos de inicio en el archivo /etc/rc.local para que surtan efecto en tiempo de arranque.</span><span class="sxs-lookup"><span data-stu-id="16f42-211">Put the following startup commands in the /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="16f42-212">Optimización de la base de datos de MySQL</span><span class="sxs-lookup"><span data-stu-id="16f42-212">MySQL database optimization</span></span>
<span data-ttu-id="16f42-213">Para configurar MySQL en Azure, puede usar la misma estrategia de optimización del rendimiento que usa en una máquina local.</span><span class="sxs-lookup"><span data-stu-id="16f42-213">To configure MySQL on Azure, you can use the same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="16f42-214">Las principales reglas de optimización de E/S son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="16f42-214">The main I/O optimization rules are:</span></span>   

* <span data-ttu-id="16f42-215">Aumentar el tamaño de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="16f42-215">Increase the cache size.</span></span>
* <span data-ttu-id="16f42-216">Reducir el tiempo de respuesta de E/S.</span><span class="sxs-lookup"><span data-stu-id="16f42-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="16f42-217">Para optimizar la configuración del servidor MySQL, puede actualizar el archivo my.cnf, que es el archivo de configuración predeterminado tanto para los equipos cliente como servidor.</span><span class="sxs-lookup"><span data-stu-id="16f42-217">To optimize MySQL server settings, you can update the my.cnf file, which is the default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="16f42-218">Los elementos de configuración siguientes son los principales factores que influyen en el rendimiento de MySQL:</span><span class="sxs-lookup"><span data-stu-id="16f42-218">The following configuration items are the main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="16f42-219">**innodb_buffer_pool_size**: el grupo de búferes contiene los datos almacenados en el búfer, así como el índice.</span><span class="sxs-lookup"><span data-stu-id="16f42-219">**innodb_buffer_pool_size**: The buffer pool contains buffered data and the index.</span></span> <span data-ttu-id="16f42-220">Normalmente se establece en el 70 por ciento de memoria física.</span><span class="sxs-lookup"><span data-stu-id="16f42-220">This is usually set to 70 percent of physical memory.</span></span>
* <span data-ttu-id="16f42-221">**innodb_log_file_size**: este es el tamaño de registro de rehacer.</span><span class="sxs-lookup"><span data-stu-id="16f42-221">**innodb_log_file_size**: This is the redo log size.</span></span> <span data-ttu-id="16f42-222">Los registros de rehacer se usan para garantizar que las operaciones de escritura son rápidas, confiables y recuperables después de un bloqueo.</span><span class="sxs-lookup"><span data-stu-id="16f42-222">You use redo logs to ensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="16f42-223">Se establece en 512 MB, lo que proporcionará una cantidad de espacio suficiente para registrar las operaciones de escritura.</span><span class="sxs-lookup"><span data-stu-id="16f42-223">This is set to 512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="16f42-224">**max_connections**: a veces, las aplicaciones no cierran las conexiones correctamente.</span><span class="sxs-lookup"><span data-stu-id="16f42-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="16f42-225">Un valor mayor proporciona al servidor más tiempo para reciclar las conexiones inactivas.</span><span class="sxs-lookup"><span data-stu-id="16f42-225">A larger value will give the server more time to recycle idled connections.</span></span> <span data-ttu-id="16f42-226">El número máximo de conexiones es de 10,000, pero el máximo recomendado es de 5,000.</span><span class="sxs-lookup"><span data-stu-id="16f42-226">The maximum number of connections is 10,000, but the recommended maximum is 5,000.</span></span>
* <span data-ttu-id="16f42-227">**Innodb_file_per_table**: esta configuración habilita o deshabilita la posibilidad de que InnoDB almacene tablas en archivos independientes.</span><span class="sxs-lookup"><span data-stu-id="16f42-227">**Innodb_file_per_table**: This setting enables or disables the ability of InnoDB to store tables in separate files.</span></span> <span data-ttu-id="16f42-228">Si activa la opción se asegurará de que se pueden aplicar varias operaciones avanzadas de administración eficaces.</span><span class="sxs-lookup"><span data-stu-id="16f42-228">Turn on the option to ensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="16f42-229">Desde el punto de vista del rendimiento, puede acelerar la transmisión del espacio de tabla y optimizar el rendimiento de la administración de residuos.</span><span class="sxs-lookup"><span data-stu-id="16f42-229">From a performance point of view, it can speed up the table space transmission and optimize the debris management performance.</span></span> <span data-ttu-id="16f42-230">El valor recomendado para esta opción es ON.</span><span class="sxs-lookup"><span data-stu-id="16f42-230">The recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="16f42-231">Desde MySQL 5.6, el valor predeterminado es ON, por lo que no se requiere ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="16f42-231">From MySQL 5.6, the default setting is ON, so no action is required.</span></span> <span data-ttu-id="16f42-232">En el caso de las versiones anteriores, el valor predeterminado es OFF.</span><span class="sxs-lookup"><span data-stu-id="16f42-232">For earlier versions, the default setting is OFF.</span></span> <span data-ttu-id="16f42-233">Debe cambiar este valor antes de cargar los datos, ya que solo se ven afectadas las tablas recién creadas.</span><span class="sxs-lookup"><span data-stu-id="16f42-233">The setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="16f42-234">**innodb_flush_log_at_trx_commit**: el valor predeterminado es 1, con el ámbito establecido en 0~2.</span><span class="sxs-lookup"><span data-stu-id="16f42-234">**innodb_flush_log_at_trx_commit**: The default value is 1, with the scope set to 0~2.</span></span> <span data-ttu-id="16f42-235">El valor predeterminado es la opción más adecuada para la base de datos MySQL independiente.</span><span class="sxs-lookup"><span data-stu-id="16f42-235">The default value is the most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="16f42-236">El valor 2 permite una mayor integridad de datos y es adecuado para Master en clúster de MySQL.</span><span class="sxs-lookup"><span data-stu-id="16f42-236">The setting of 2 enables the most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="16f42-237">El valor 0 permite la pérdida de datos, lo que puede afectar a la confiabilidad (en algunos casos con un mejor rendimiento) y es adecuado para la opción de subordinado en clúster de MySQL.</span><span class="sxs-lookup"><span data-stu-id="16f42-237">The setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="16f42-238">**Innodb_log_buffer_size**: el búfer de registro permite que las transacciones se ejecuten sin tener que vaciar el registro en el disco antes de confirmar las transacciones.</span><span class="sxs-lookup"><span data-stu-id="16f42-238">**Innodb_log_buffer_size**: The log buffer allows transactions to run without having to flush the log to disk before the transactions commit.</span></span> <span data-ttu-id="16f42-239">Sin embargo, si hay un objeto binario de gran tamaño o un campo de texto, se consumirá la memoria caché rápidamente y se activará la E/S de discos frecuentes.</span><span class="sxs-lookup"><span data-stu-id="16f42-239">However, if there is large binary object or text field, the cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="16f42-240">Es mejor incrementar el tamaño del búfer si la variable de estado Innodb_log_waits no es 0.</span><span class="sxs-lookup"><span data-stu-id="16f42-240">It is better increase the buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="16f42-241">**query_cache_size**: la mejor opción es deshabilitarla desde el principio.</span><span class="sxs-lookup"><span data-stu-id="16f42-241">**query_cache_size**: The best option is to disable it from the outset.</span></span> <span data-ttu-id="16f42-242">Establezca query_cache_size en 0 (este es el valor predeterminado en MySQL 5.6) y use otros métodos para agilizar las consultas.</span><span class="sxs-lookup"><span data-stu-id="16f42-242">Set query_cache_size to 0 (this is the default setting in MySQL 5.6) and use other methods to speed up queries.</span></span>  

<span data-ttu-id="16f42-243">Consulte el [apéndice D](#AppendixD) para ver una comparación del rendimiento antes y después de la optimización.</span><span class="sxs-lookup"><span data-stu-id="16f42-243">See [Appendix D](#AppendixD) for a comparison of performance before and after the optimization.</span></span>

## <a name="turn-on-the-mysql-slow-query-log-for-analyzing-the-performance-bottleneck"></a><span data-ttu-id="16f42-244">Activar el registro de consultas lentas de MySQL para analizar el cuello de botella de rendimiento</span><span class="sxs-lookup"><span data-stu-id="16f42-244">Turn on the MySQL slow query log for analyzing the performance bottleneck</span></span>
<span data-ttu-id="16f42-245">El registro de consultas lentas de MySQL puede ayudarle a identificar las consultas lentas de MySQL.</span><span class="sxs-lookup"><span data-stu-id="16f42-245">The MySQL slow query log can help you identify the slow queries for MySQL.</span></span> <span data-ttu-id="16f42-246">Después de habilitar el registro de consultas lentas de MySQL, puede usar las herramientas de MySQL como **mysqldumpslow** para identificar el cuello de botella de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="16f42-246">After enabling the MySQL slow query log, you can use MySQL tools like **mysqldumpslow** to identify the performance bottleneck.</span></span>  

<span data-ttu-id="16f42-247">De manera predeterminada, no está habilitado.</span><span class="sxs-lookup"><span data-stu-id="16f42-247">By default, this is not enabled.</span></span> <span data-ttu-id="16f42-248">Activar el registro de consultas lentas puede consumir algunos recursos de CPU.</span><span class="sxs-lookup"><span data-stu-id="16f42-248">Turning on the slow query log might consume some CPU resources.</span></span> <span data-ttu-id="16f42-249">Se recomienda habilitar esta opción de forma temporal para solucionar los cuellos de botella de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="16f42-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="16f42-250">Para activar el registro de consultas lentas:</span><span class="sxs-lookup"><span data-stu-id="16f42-250">To turn on the slow query log:</span></span>

1. <span data-ttu-id="16f42-251">Modifique el archivo my.cnf file agregando las líneas siguientes al final:</span><span class="sxs-lookup"><span data-stu-id="16f42-251">Modify the my.cnf file by adding the following lines to the end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="16f42-252">Reinicie el servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="16f42-252">Restart the MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="16f42-253">Compruebe si la configuración surte efecto con el comando **show**.</span><span class="sxs-lookup"><span data-stu-id="16f42-253">Check whether the setting is taking effect by using the **show** command.</span></span>

![Registro de consultas lentas ON][7]   

![Resultados del registro de consultas lentas][8]

<span data-ttu-id="16f42-256">En este ejemplo, puede ver que se ha activado la característica de consulta lenta.</span><span class="sxs-lookup"><span data-stu-id="16f42-256">In this example, you can see that the slow query feature has been turned on.</span></span> <span data-ttu-id="16f42-257">De este modo, podrá usar la herramienta **mysqldumpslow** para determinar los cuellos de botella de rendimiento y optimizar el rendimiento como, por ejemplo, la adición de índices.</span><span class="sxs-lookup"><span data-stu-id="16f42-257">You can then use the **mysqldumpslow** tool to determine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="16f42-258">Apéndices</span><span class="sxs-lookup"><span data-stu-id="16f42-258">Appendices</span></span>
<span data-ttu-id="16f42-259">A continuación se muestran los datos de las pruebas de rendimiento de ejemplo obtenidos en un entorno de laboratorio de destino.</span><span class="sxs-lookup"><span data-stu-id="16f42-259">The following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="16f42-260">Estos datos proporcionan información general acerca de las tendencias de datos de rendimiento con distintos enfoques de optimización del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="16f42-260">They provide general background on the performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="16f42-261">Los resultados pueden variar con las distintas versiones de producto o entorno.</span><span class="sxs-lookup"><span data-stu-id="16f42-261">The results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="16f42-262"><a name="AppendixA"></a>Apéndice A</span><span class="sxs-lookup"><span data-stu-id="16f42-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="16f42-263">**Rendimiento del disco (E/S por segundo) con los distintos niveles de RAID**</span><span class="sxs-lookup"><span data-stu-id="16f42-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![E/S por segundo de disco con los distintos niveles de RAID][9]

<span data-ttu-id="16f42-265">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="16f42-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="16f42-266">La carga de trabajo de esta prueba usa 64 subprocesos para intentar alcanzar el límite superior de RAID.</span><span class="sxs-lookup"><span data-stu-id="16f42-266">The workload of this test uses 64 threads, trying to reach the upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="16f42-267"><a name="AppendixB"></a>Apéndice B</span><span class="sxs-lookup"><span data-stu-id="16f42-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="16f42-268">**Comparación de rendimiento de MySQL con los distintos niveles de RAID** </span><span class="sxs-lookup"><span data-stu-id="16f42-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="16f42-269">(sistema de archivos XFS)</span><span class="sxs-lookup"><span data-stu-id="16f42-269">(XFS file system)</span></span>

![Comparación de rendimiento de MySQL con los distintos niveles de RAID][10]  
![Comparación de rendimiento de MySQL con los distintos niveles de RAID][11]

<span data-ttu-id="16f42-272">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="16f42-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="16f42-273">**Comparación de rendimiento (OLTP) de MySQL con los distintos niveles de RAID**</span><span class="sxs-lookup"><span data-stu-id="16f42-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="16f42-274">![Comparación de rendimiento (OLTP) de MySQL con los distintos niveles de RAID][12]</span><span class="sxs-lookup"><span data-stu-id="16f42-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="16f42-275">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="16f42-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="16f42-276"><a name="AppendixC"></a>Apéndice C</span><span class="sxs-lookup"><span data-stu-id="16f42-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="16f42-277">**Comparación de rendimiento (E/S por segundo) de disco con distintos tamaños de fragmento**</span><span class="sxs-lookup"><span data-stu-id="16f42-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="16f42-278">(sistema de archivos XFS)</span><span class="sxs-lookup"><span data-stu-id="16f42-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="16f42-279">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="16f42-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="16f42-280">Los tamaños de archivo que se usan para esta prueba es de 30 GB y 1 GB, respectivamente, con el sistema de archivos XFS RAID 0 (4 discos).</span><span class="sxs-lookup"><span data-stu-id="16f42-280">The file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="16f42-281"><a name="AppendixD"></a>Apéndice D</span><span class="sxs-lookup"><span data-stu-id="16f42-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="16f42-282">**Comparación de rendimiento de MySQL antes y después de la optimización**</span><span class="sxs-lookup"><span data-stu-id="16f42-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="16f42-283">(sistema de archivos XFS)</span><span class="sxs-lookup"><span data-stu-id="16f42-283">(XFS File System)</span></span>

![Comparación de rendimiento de MySQL antes y después de la optimización][14]

<span data-ttu-id="16f42-285">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="16f42-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="16f42-286">**Los valores de configuración predeterminada y de optimización son los siguientes:**</span><span class="sxs-lookup"><span data-stu-id="16f42-286">**The configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="16f42-287">Parámetros</span><span class="sxs-lookup"><span data-stu-id="16f42-287">Parameters</span></span> | <span data-ttu-id="16f42-288">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="16f42-288">Default</span></span> | <span data-ttu-id="16f42-289">Optimización</span><span class="sxs-lookup"><span data-stu-id="16f42-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16f42-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="16f42-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="16f42-291">None</span><span class="sxs-lookup"><span data-stu-id="16f42-291">None</span></span> |<span data-ttu-id="16f42-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="16f42-292">7 GB</span></span> |
| <span data-ttu-id="16f42-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="16f42-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="16f42-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="16f42-294">5 MB</span></span> |<span data-ttu-id="16f42-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="16f42-295">512 MB</span></span> |
| <span data-ttu-id="16f42-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="16f42-296">**max_connections**</span></span> |<span data-ttu-id="16f42-297">100</span><span class="sxs-lookup"><span data-stu-id="16f42-297">100</span></span> |<span data-ttu-id="16f42-298">5.000</span><span class="sxs-lookup"><span data-stu-id="16f42-298">5000</span></span> |
| <span data-ttu-id="16f42-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="16f42-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="16f42-300">0</span><span class="sxs-lookup"><span data-stu-id="16f42-300">0</span></span> |<span data-ttu-id="16f42-301">1</span><span class="sxs-lookup"><span data-stu-id="16f42-301">1</span></span> |
| <span data-ttu-id="16f42-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="16f42-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="16f42-303">1</span><span class="sxs-lookup"><span data-stu-id="16f42-303">1</span></span> |<span data-ttu-id="16f42-304">2</span><span class="sxs-lookup"><span data-stu-id="16f42-304">2</span></span> |
| <span data-ttu-id="16f42-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="16f42-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="16f42-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="16f42-306">8 MB</span></span> |<span data-ttu-id="16f42-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="16f42-307">128 MB</span></span> |
| <span data-ttu-id="16f42-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="16f42-308">**query_cache_size**</span></span> |<span data-ttu-id="16f42-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="16f42-309">16 MB</span></span> |<span data-ttu-id="16f42-310">0</span><span class="sxs-lookup"><span data-stu-id="16f42-310">0</span></span> |

<span data-ttu-id="16f42-311">Para obtener [parámetros de configuración de optimización](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html) más detallados, consulte las [instrucciones oficiales de MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="16f42-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer to the [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="16f42-312">**Entorno de prueba**</span><span class="sxs-lookup"><span data-stu-id="16f42-312">**Test environment**</span></span>  

| <span data-ttu-id="16f42-313">Hardware</span><span class="sxs-lookup"><span data-stu-id="16f42-313">Hardware</span></span> | <span data-ttu-id="16f42-314">Detalles</span><span class="sxs-lookup"><span data-stu-id="16f42-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="16f42-315">CPU</span><span class="sxs-lookup"><span data-stu-id="16f42-315">CPU</span></span> |<span data-ttu-id="16f42-316">Procesador AMD Opteron(tm) 4171 HE/4 núcleos</span><span class="sxs-lookup"><span data-stu-id="16f42-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="16f42-317">Memoria</span><span class="sxs-lookup"><span data-stu-id="16f42-317">Memory</span></span> |<span data-ttu-id="16f42-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="16f42-318">14 GB</span></span> |
| <span data-ttu-id="16f42-319">Disco</span><span class="sxs-lookup"><span data-stu-id="16f42-319">Disk</span></span> |<span data-ttu-id="16f42-320">10 GB/disco</span><span class="sxs-lookup"><span data-stu-id="16f42-320">10 GB/disk</span></span> |
| <span data-ttu-id="16f42-321">SO</span><span class="sxs-lookup"><span data-stu-id="16f42-321">OS</span></span> |<span data-ttu-id="16f42-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="16f42-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

