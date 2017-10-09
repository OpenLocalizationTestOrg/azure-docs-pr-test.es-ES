---
title: rendimiento de MySQL en Linux aaaOptimize | Documentos de Microsoft
description: "Obtenga información acerca de cómo toooptimize MySQL ejecutando en una máquina virtual (VM) Azure ejecutan Linux."
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
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="2c137-103">Optimización del rendimiento de MySQL en máquinas virtuales de Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="2c137-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="2c137-104">Existen muchos factores que afectan al rendimiento de MySQL en Azure, tanto en la configuración de selección de software y hardware virtual.</span><span class="sxs-lookup"><span data-stu-id="2c137-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="2c137-105">Este artículo se centra en la optimización del rendimiento a través del almacenamiento, el sistema y las configuraciones de base de datos.</span><span class="sxs-lookup"><span data-stu-id="2c137-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c137-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico.</span><span class="sxs-lookup"><span data-stu-id="2c137-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="2c137-107">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="2c137-108">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="2c137-109">Para obtener información acerca de las optimizaciones de VM de Linux con el modelo del Administrador de recursos de hello, consulte [optimizar la VM de Linux en Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c137-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="2c137-110">Uso de RAID en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="2c137-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="2c137-111">El almacenamiento es el factor clave Hola que afecta al rendimiento de la base de datos en entornos de nube.</span><span class="sxs-lookup"><span data-stu-id="2c137-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="2c137-112">Tooa en comparación con uno de los discos, RAID puede proporcionar un acceso más rápido a través de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="2c137-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="2c137-113">Para más información, consulte [Niveles RAID estándar](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="2c137-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="2c137-114">El rendimiento de E/S de disco, así como el tiempo de respuesta de las E/S pueden mejorarse con RAID.</span><span class="sxs-lookup"><span data-stu-id="2c137-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="2c137-115">Nuestras pruebas de laboratorio muestran que se puede duplicar el rendimiento de E/S de disco y tiempo de respuesta de E/S puede reducirse a la mitad por término medio cuando se duplica el número Hola de discos RAID (de toofour dos, cuatro tooeight, etcetera).</span><span class="sxs-lookup"><span data-stu-id="2c137-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="2c137-116">Consulte el [Apéndice A](#AppendixA) para más información.</span><span class="sxs-lookup"><span data-stu-id="2c137-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="2c137-117">Además, la E/S de toodisk MySQL mejora el rendimiento al aumentar Hola nivel RAID.</span><span class="sxs-lookup"><span data-stu-id="2c137-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="2c137-118">Consulte el [Apéndice B](#AppendixB) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2c137-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="2c137-119">Puede que le interese el tamaño del fragmento de tooconsider Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="2c137-120">En general, cuando el tamaño de fragmento es mayor, obtiene una menor sobrecarga, especialmente para las operaciones de escritura de mayor envergadura.</span><span class="sxs-lookup"><span data-stu-id="2c137-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="2c137-121">Sin embargo, cuando el tamaño del fragmento de hello es demasiado grande, podría agregar una sobrecarga adicional que le impide al aprovechar la posibilidad de RAID.</span><span class="sxs-lookup"><span data-stu-id="2c137-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="2c137-122">tamaño predeterminado actual de Hello es 512 KB, lo que demuestra toobe óptimo para los entornos de producción más generales.</span><span class="sxs-lookup"><span data-stu-id="2c137-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="2c137-123">Consulte el [Apéndice C](#AppendixC) para más información.</span><span class="sxs-lookup"><span data-stu-id="2c137-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="2c137-124">Existen límites en cuanto al número de discos que puede agregar para los distintos tipos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2c137-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="2c137-125">Estos límites se detallan en [Tamaños de máquinas virtuales y servicios en la nube de Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c137-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="2c137-126">Necesitará cuatro datos adjuntos discos toofollow Hola RAID ejemplo en este artículo, aunque puede elegir tooset de RAID con menos discos.</span><span class="sxs-lookup"><span data-stu-id="2c137-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="2c137-127">En este artículo se da por supuesto que ya ha creado una máquina virtual Linux y que MYSQL está instalado y configurado.</span><span class="sxs-lookup"><span data-stu-id="2c137-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="2c137-128">Para obtener más información acerca de cómo empezar, vea cómo tooinstall MySQL en Azure.</span><span class="sxs-lookup"><span data-stu-id="2c137-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="2c137-129">Configuración de RAID en Azure</span><span class="sxs-lookup"><span data-stu-id="2c137-129">Set up RAID on Azure</span></span>
<span data-ttu-id="2c137-130">Hello pasos siguientes muestran cómo toocreate RAID en Azure mediante el uso de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2c137-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="2c137-131">También puede configurar RAID mediante scripts de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c137-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="2c137-132">En este ejemplo, configuraremos RAID 0 con 4 discos.</span><span class="sxs-lookup"><span data-stu-id="2c137-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="2c137-133">Agregar una máquina virtual de datos disco tooyour</span><span class="sxs-lookup"><span data-stu-id="2c137-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="2c137-134">Hola portal de Azure, vaya a Panel de toohello y seleccione hello toowhich de máquina virtual que desee tooadd un disco de datos.</span><span class="sxs-lookup"><span data-stu-id="2c137-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="2c137-135">En este ejemplo, la máquina virtual de hello es mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="2c137-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="2c137-136">Haga clic en **Discos** y luego haga clic en **Asociar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="2c137-136">Click **Disks** and then click **Attach New**.</span></span>

![Agregar disco a máquinas virtuales](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="2c137-138">Cree un nuevo disco de 500 GB.</span><span class="sxs-lookup"><span data-stu-id="2c137-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="2c137-139">Asegúrese de que **preferencia de caché de Host** se establece demasiado**ninguno**.</span><span class="sxs-lookup"><span data-stu-id="2c137-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="2c137-140">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2c137-140">When you're finished, click **OK**.</span></span>

![Acoplar disco vacío](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="2c137-142">Esta acción agrega un disco vacío a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2c137-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="2c137-143">Repita este paso tres veces más para que disponga de 4 discos de datos para RAID.</span><span class="sxs-lookup"><span data-stu-id="2c137-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="2c137-144">Puede ver Hola agrega las unidades en la máquina virtual de hello examinando el registro de mensajes de Hola kernel.</span><span class="sxs-lookup"><span data-stu-id="2c137-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="2c137-145">Por ejemplo, toosee esto en Ubuntu, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c137-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="2c137-146">Crear RAID con hello discos adicionales</span><span class="sxs-lookup"><span data-stu-id="2c137-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="2c137-147">Hello pasos siguientes describen cómo demasiado[configurar RAID de software en Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c137-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="2c137-148">Si está utilizando el sistema de archivos de hello XFS, ejecute hello siguientes pasos después de haber creado RAID.</span><span class="sxs-lookup"><span data-stu-id="2c137-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="2c137-149">tooinstall XFS en Debian, Ubuntu o lleva de Linux, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c137-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="2c137-150">tooinstall XFS en Fedora, CentOS o RHEL, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c137-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="2c137-151">Configurar una nueva ruta de acceso de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="2c137-151">Set up a new storage path</span></span>
<span data-ttu-id="2c137-152">Usar hello después comando tooset una nueva ruta de acceso de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="2c137-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="2c137-153">Copiar Hola datos toohello nuevo almacenamiento ruta de acceso original</span><span class="sxs-lookup"><span data-stu-id="2c137-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="2c137-154">Usar hello comando toocopy datos toohello nuevo almacenamiento la ruta de acceso:</span><span class="sxs-lookup"><span data-stu-id="2c137-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="2c137-155">Modificar los permisos por lo que puede tener acceso MySQL (lectura y escritura) disco de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="2c137-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="2c137-156">Use los siguientes comandos toomodify permisos de hello:</span><span class="sxs-lookup"><span data-stu-id="2c137-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="2c137-157">Ajustar la E/S de disco de hello algoritmo de programación</span><span class="sxs-lookup"><span data-stu-id="2c137-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="2c137-158">Linux implementa cuatro tipos de algoritmos de programación de E/S:</span><span class="sxs-lookup"><span data-stu-id="2c137-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="2c137-159">Algoritmo NOOP (sin operación)</span><span class="sxs-lookup"><span data-stu-id="2c137-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="2c137-160">Algoritmo de fecha límite (fecha límite)</span><span class="sxs-lookup"><span data-stu-id="2c137-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="2c137-161">Algoritmo de cola justa (CFQ)</span><span class="sxs-lookup"><span data-stu-id="2c137-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="2c137-162">Algoritmo de período de presupuesto (antelación)</span><span class="sxs-lookup"><span data-stu-id="2c137-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="2c137-163">Puede seleccionar a diferentes programadores de E/S en rendimiento de toooptimize escenarios diferentes.</span><span class="sxs-lookup"><span data-stu-id="2c137-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="2c137-164">En un entorno de acceso aleatorio por completo, no hay una diferencia significativa entre hello CFQ y algoritmos de fecha límite para el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2c137-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="2c137-165">Recomendamos que establezca tooDeadline de entorno de base de datos de MySQL de hello para la estabilidad.</span><span class="sxs-lookup"><span data-stu-id="2c137-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="2c137-166">Si hay un elevado volumen de E/S secuenciales, el algoritmo CFQ puede reducir el rendimiento de las E/S de disco.</span><span class="sxs-lookup"><span data-stu-id="2c137-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="2c137-167">De SSD y otros equipos, NOOP o fecha límite puede lograr un rendimiento mejor que el programador predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="2c137-168">Núcleo de toohello anteriores 2.5, Hola predeterminado E/S programación algoritmo es fecha límite.</span><span class="sxs-lookup"><span data-stu-id="2c137-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="2c137-169">A partir de kernel hello 2.6.18, CFQ pasara a ser de algoritmo de programación de E/S Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2c137-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="2c137-170">Puede especificar esta configuración en tiempo de arranque de kernel o modificar esta configuración de forma dinámica cuando se ejecuta el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="2c137-171">Hola siguiente ejemplo muestra cómo toocheck y establezca Hola predeterminado programador toohello NOOP el algoritmo de familia de distribución Debian Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="2c137-172">Programador de E/S de vista Hola actual</span><span class="sxs-lookup"><span data-stu-id="2c137-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="2c137-173">Programador de hello tooview ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c137-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="2c137-174">Se muestra después de salida, lo que indica el programador actual hello:</span><span class="sxs-lookup"><span data-stu-id="2c137-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="2c137-175">Cambiar Hola actual dispositivo (/ dev/sda) del algoritmo de programación de hello i/OS</span><span class="sxs-lookup"><span data-stu-id="2c137-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="2c137-176">Ejecute hello después de dispositivo actual de comandos toochange hello:</span><span class="sxs-lookup"><span data-stu-id="2c137-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="2c137-177">Establecer este valor solo para /dev/sda no es útil.</span><span class="sxs-lookup"><span data-stu-id="2c137-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="2c137-178">Debe establecerse en todos los discos de datos donde reside la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="2c137-179">Debería ver Hola después de salida, que indica que se ha recompilado grub.cfg correctamente y programador predeterminado Hola ha sido actualizada tooNOOP:</span><span class="sxs-lookup"><span data-stu-id="2c137-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="2c137-180">Para hello familia de distribución de Red Hat, necesita Hola solo el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c137-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="2c137-181">Configurar las opciones de las operaciones de archivos de sistema</span><span class="sxs-lookup"><span data-stu-id="2c137-181">Configure system file operations settings</span></span>
<span data-ttu-id="2c137-182">Una práctica recomendada es hello toodisable *atime* característica de registro en el sistema de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="2c137-183">Atime es Hola última hora de acceso de archivo.</span><span class="sxs-lookup"><span data-stu-id="2c137-183">Atime is hello last file access time.</span></span> <span data-ttu-id="2c137-184">Cada vez que se tiene acceso a un archivo, los registros de sistema de archivo Hola Hola marca de tiempo en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="2c137-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="2c137-185">Sin embargo, esta información no suele usarse.</span><span class="sxs-lookup"><span data-stu-id="2c137-185">However, this information is rarely used.</span></span> <span data-ttu-id="2c137-186">Por lo tanto, se puede deshabilitar si no es necesaria. Esto reducirá el tiempo total de acceso al disco.</span><span class="sxs-lookup"><span data-stu-id="2c137-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="2c137-187">toodisable atime registro, necesita toomodify Hola archivo sistema configuración archivo/etc / fstab y agregar hello **noatime** opción.</span><span class="sxs-lookup"><span data-stu-id="2c137-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="2c137-188">Por ejemplo, edite el archivo/etc/fstab de hello vim, agregando hello noatime tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="2c137-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="2c137-189">A continuación, vuelva a montar el sistema de archivos de hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c137-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="2c137-190">Hola de prueba modifica el resultado.</span><span class="sxs-lookup"><span data-stu-id="2c137-190">Test hello modified result.</span></span> <span data-ttu-id="2c137-191">Cuando se modifica el archivo de prueba de hello, no se actualiza la hora de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="2c137-192">Hola siguientes ejemplos se muestra el código de hello aspecto antes y después de la modificación.</span><span class="sxs-lookup"><span data-stu-id="2c137-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="2c137-193">Antes:</span><span class="sxs-lookup"><span data-stu-id="2c137-193">Before:</span></span>        

![El código antes de la modificación del acceso.][5]

<span data-ttu-id="2c137-195">Después:</span><span class="sxs-lookup"><span data-stu-id="2c137-195">After:</span></span>

![El código después de la modificación del acceso.][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="2c137-197">Aumentar Hola número máximo de identificadores de sistema de alta simultaneidad</span><span class="sxs-lookup"><span data-stu-id="2c137-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="2c137-198">MySQL es una base de datos de alta simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="2c137-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="2c137-199">número predeterminado de Hola de identificadores simultáneas es 1024 para Linux, que no siempre es suficiente.</span><span class="sxs-lookup"><span data-stu-id="2c137-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="2c137-200">Usar hello siguiendo los pasos tooincrease Hola máximo simultáneas identificadores de simultaneidad elevada toosupport de hello sistema de MySQL.</span><span class="sxs-lookup"><span data-stu-id="2c137-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="2c137-201">Modificar el archivo de hello limits.conf</span><span class="sxs-lookup"><span data-stu-id="2c137-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="2c137-202">Hola tooincrease máximo permitido identificadores simultáneas, agregue Hola después de cuatro líneas en el archivo de hello /etc/security/limits.conf.</span><span class="sxs-lookup"><span data-stu-id="2c137-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="2c137-203">Tenga en cuenta que 65536 es el número máximo de Hola que Hola sistema puede admitir.</span><span class="sxs-lookup"><span data-stu-id="2c137-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="2c137-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="2c137-204">soft nofile 65536</span></span>
    * <span data-ttu-id="2c137-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="2c137-205">hard nofile 65536</span></span>
    * <span data-ttu-id="2c137-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="2c137-206">soft nproc 65536</span></span>
    * <span data-ttu-id="2c137-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="2c137-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="2c137-208">Actualizar sistema de Hola para los nuevos límites de Hola</span><span class="sxs-lookup"><span data-stu-id="2c137-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="2c137-209">sistema de hello tooupdate, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="2c137-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="2c137-210">Asegúrese de que se actualizan los límites de Hola durante el arranque</span><span class="sxs-lookup"><span data-stu-id="2c137-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="2c137-211">Hola Put después de comandos de inicio en el archivo de hello /etc/rc.local por lo que aplicará al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="2c137-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="2c137-212">Optimización de la base de datos de MySQL</span><span class="sxs-lookup"><span data-stu-id="2c137-212">MySQL database optimization</span></span>
<span data-ttu-id="2c137-213">tooconfigure MySQL en Azure, puede usar Hola misma estrategia de optimización del rendimiento se usa en una máquina local.</span><span class="sxs-lookup"><span data-stu-id="2c137-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="2c137-214">Hola reglas de optimización de E/S principales son:</span><span class="sxs-lookup"><span data-stu-id="2c137-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="2c137-215">Aumentar el tamaño de la caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-215">Increase hello cache size.</span></span>
* <span data-ttu-id="2c137-216">Reducir el tiempo de respuesta de E/S.</span><span class="sxs-lookup"><span data-stu-id="2c137-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="2c137-217">configuración del servidor de MySQL de toooptimize, puede actualizar el archivo my.cnf de hello, que es el archivo de configuración predeterminado de Hola para equipos cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="2c137-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="2c137-218">Hello siguientes elementos de configuración son Hola factores principales que afectan al rendimiento de MySQL:</span><span class="sxs-lookup"><span data-stu-id="2c137-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="2c137-219">**innodb_buffer_pool_size**: grupo de búferes de hello contiene datos almacenados en búfer y el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="2c137-220">Normalmente, esto se establece too70 porcentaje de memoria física.</span><span class="sxs-lookup"><span data-stu-id="2c137-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="2c137-221">**innodb_log_file_size**: se trata de tamaño del registro de hello puesta al día.</span><span class="sxs-lookup"><span data-stu-id="2c137-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="2c137-222">Utilice tooensure de registros de puesta al día que las operaciones de escritura son rápidos, confiable y recuperable después de un bloqueo.</span><span class="sxs-lookup"><span data-stu-id="2c137-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="2c137-223">Esto se establece too512 MB, lo que le proporcionará una gran cantidad de espacio para las operaciones de escritura de registro.</span><span class="sxs-lookup"><span data-stu-id="2c137-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="2c137-224">**max_connections**: a veces, las aplicaciones no cierran las conexiones correctamente.</span><span class="sxs-lookup"><span data-stu-id="2c137-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="2c137-225">Un valor mayor Hola servidor tendrá más tiempo toorecycle ralentizó conexiones.</span><span class="sxs-lookup"><span data-stu-id="2c137-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="2c137-226">Hola número máximo de conexiones es 10 000, pero Hola recomienda máximo es 5000.</span><span class="sxs-lookup"><span data-stu-id="2c137-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="2c137-227">**Innodb_file_per_table**: esta configuración habilita o deshabilita la capacidad de Hola de InnoDB toostore tablas en archivos independientes.</span><span class="sxs-lookup"><span data-stu-id="2c137-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="2c137-228">Activar Hola opción tooensure que se pueden aplicar varias operaciones de administración avanzadas eficazmente.</span><span class="sxs-lookup"><span data-stu-id="2c137-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="2c137-229">Desde un punto de vista del rendimiento, puede acelerar la transmisión de espacio de tabla de Hola y optimizar el rendimiento de administración de restos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="2c137-230">Hola recomienda el valor de esta opción es ON.</span><span class="sxs-lookup"><span data-stu-id="2c137-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="2c137-231">Desde MySQL 5.6, saludo predeterminado es ON, por lo que no se requiere ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="2c137-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="2c137-232">Para las versiones anteriores, la configuración predeterminada de hello es OFF.</span><span class="sxs-lookup"><span data-stu-id="2c137-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="2c137-233">Hola debe cambiarse antes de que se cargan datos, porque solo las tablas recién creadas se ven afectadas.</span><span class="sxs-lookup"><span data-stu-id="2c137-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="2c137-234">**innodb_flush_log_at_trx_commit**: valor predeterminado de hello es 1, con hello ámbito establecido too0 ~ 2.</span><span class="sxs-lookup"><span data-stu-id="2c137-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="2c137-235">valor predeterminado de Hello es opción más adecuado de Hola para base de datos de MySQL independiente.</span><span class="sxs-lookup"><span data-stu-id="2c137-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="2c137-236">configuración de Hola de 2 habilita Hola mayoría integridad de los datos y es adecuado para Master en MySQL clúster.</span><span class="sxs-lookup"><span data-stu-id="2c137-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="2c137-237">valor de Hola de 0 permite pérdida de datos, lo que puede afectar la confiabilidad (en algunos casos con un mejor rendimiento) y es adecuado para esclavo en MySQL clúster.</span><span class="sxs-lookup"><span data-stu-id="2c137-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="2c137-238">**Innodb_log_buffer_size**: búfer de registro de hello permite toorun de transacciones sin necesidad de tooflush Hola registro toodisk antes de hello las transacciones se confirman.</span><span class="sxs-lookup"><span data-stu-id="2c137-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="2c137-239">Sin embargo, si no hay objeto binario grande o un campo de texto, caché Hola se consumirán rápidamente y se activará la E/S de disco frecuentes.</span><span class="sxs-lookup"><span data-stu-id="2c137-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="2c137-240">Es mejor aumentar tamaño de búfer de hello si la variable de estado de Innodb_log_waits no es 0.</span><span class="sxs-lookup"><span data-stu-id="2c137-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="2c137-241">**query_cache_size**: Hola mejor opción es toodisable desde el principio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="2c137-242">Establecer too0 query_cache_size (es decir, valor predeterminado de hello en MySQL 5.6) y usar otra toospeed métodos consultas.</span><span class="sxs-lookup"><span data-stu-id="2c137-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="2c137-243">Vea [apéndice D](#AppendixD) para ver una comparación de rendimiento antes y después de la optimización de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="2c137-244">Activar el registro de consultas lentas de MySQL de hello para el análisis del cuello de botella de rendimiento de Hola</span><span class="sxs-lookup"><span data-stu-id="2c137-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="2c137-245">registro de consultas lentas de MySQL de Hola puede ayudarle a identificar las consultas lentas de Hola de MySQL.</span><span class="sxs-lookup"><span data-stu-id="2c137-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="2c137-246">Después de habilitar el registro de consultas lentas de MySQL de hello, también puede usar herramientas de MySQL como **mysqldumpslow** tooidentify Hola cuello de botella.</span><span class="sxs-lookup"><span data-stu-id="2c137-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="2c137-247">De manera predeterminada, no está habilitado.</span><span class="sxs-lookup"><span data-stu-id="2c137-247">By default, this is not enabled.</span></span> <span data-ttu-id="2c137-248">Activar el registro de consultas lentas Hola puede consumir recursos de la CPU.</span><span class="sxs-lookup"><span data-stu-id="2c137-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="2c137-249">Se recomienda habilitar esta opción de forma temporal para solucionar los cuellos de botella de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2c137-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="2c137-250">tooturn en el registro de consultas lentas hello:</span><span class="sxs-lookup"><span data-stu-id="2c137-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="2c137-251">Modificar el archivo my.cnf de hello agregando Hola siguiente líneas toohello final:</span><span class="sxs-lookup"><span data-stu-id="2c137-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="2c137-252">Reinicie el servidor de MySQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c137-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="2c137-253">Compruebe si la configuración de hello es surten efecto mediante el uso de Hola **mostrar** comando.</span><span class="sxs-lookup"><span data-stu-id="2c137-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Registro de consultas lentas ON][7]   

![Resultados del registro de consultas lentas][8]

<span data-ttu-id="2c137-256">En este ejemplo, puede ver que esa característica de consultas lentas Hola se ha activado.</span><span class="sxs-lookup"><span data-stu-id="2c137-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="2c137-257">A continuación, puede usar hello **mysqldumpslow** herramienta toodetermine cuellos de botella de rendimiento y optimizar el rendimiento, como la adición de índices.</span><span class="sxs-lookup"><span data-stu-id="2c137-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="2c137-258">Apéndices</span><span class="sxs-lookup"><span data-stu-id="2c137-258">Appendices</span></span>
<span data-ttu-id="2c137-259">siguiente Hola es datos de prueba de rendimiento de ejemplo generados en un entorno de laboratorio de destino.</span><span class="sxs-lookup"><span data-stu-id="2c137-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="2c137-260">Proporcionan información general de tendencia de datos de rendimiento de hello diferentes enfoques de optimización del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2c137-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="2c137-261">Hola resultados podrían variar en diferentes versiones de entorno o el producto.</span><span class="sxs-lookup"><span data-stu-id="2c137-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="2c137-262"><a name="AppendixA"></a>Apéndice A</span><span class="sxs-lookup"><span data-stu-id="2c137-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="2c137-263">**Rendimiento del disco (E/S por segundo) con los distintos niveles de RAID**</span><span class="sxs-lookup"><span data-stu-id="2c137-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![E/S por segundo de disco con los distintos niveles de RAID][9]

<span data-ttu-id="2c137-265">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="2c137-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="2c137-266">carga de trabajo de Hola de esta prueba utiliza 64 subprocesos, tratando de límite superior de hello tooreach de RAID.</span><span class="sxs-lookup"><span data-stu-id="2c137-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="2c137-267"><a name="AppendixB"></a>Apéndice B</span><span class="sxs-lookup"><span data-stu-id="2c137-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="2c137-268">**Comparación de rendimiento de MySQL con los distintos niveles de RAID** </span><span class="sxs-lookup"><span data-stu-id="2c137-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="2c137-269">(sistema de archivos XFS)</span><span class="sxs-lookup"><span data-stu-id="2c137-269">(XFS file system)</span></span>

![Comparación de rendimiento de MySQL con los distintos niveles de RAID][10]  
![Comparación de rendimiento de MySQL con los distintos niveles de RAID][11]

<span data-ttu-id="2c137-272">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="2c137-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="2c137-273">**Comparación de rendimiento (OLTP) de MySQL con los distintos niveles de RAID**</span><span class="sxs-lookup"><span data-stu-id="2c137-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="2c137-274">![Comparación de rendimiento (OLTP) de MySQL con los distintos niveles de RAID][12]</span><span class="sxs-lookup"><span data-stu-id="2c137-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="2c137-275">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="2c137-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="2c137-276"><a name="AppendixC"></a>Apéndice C</span><span class="sxs-lookup"><span data-stu-id="2c137-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="2c137-277">**Comparación de rendimiento (E/S por segundo) de disco con distintos tamaños de fragmento**</span><span class="sxs-lookup"><span data-stu-id="2c137-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="2c137-278">(sistema de archivos XFS)</span><span class="sxs-lookup"><span data-stu-id="2c137-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="2c137-279">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="2c137-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="2c137-280">el tamaño de archivo Hello utilizados para esta prueba es 30 GB y 1 GB, respectivamente, con RAID 0 (4 discos) XFS sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="2c137-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="2c137-281"><a name="AppendixD"></a>Apéndice D</span><span class="sxs-lookup"><span data-stu-id="2c137-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="2c137-282">**Comparación de rendimiento de MySQL antes y después de la optimización**</span><span class="sxs-lookup"><span data-stu-id="2c137-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="2c137-283">(sistema de archivos XFS)</span><span class="sxs-lookup"><span data-stu-id="2c137-283">(XFS File System)</span></span>

![Comparación de rendimiento de MySQL antes y después de la optimización][14]

<span data-ttu-id="2c137-285">**Comandos de prueba**</span><span class="sxs-lookup"><span data-stu-id="2c137-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="2c137-286">**opción de configuración de Hola para predeterminado y la optimización es como sigue:**</span><span class="sxs-lookup"><span data-stu-id="2c137-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="2c137-287">parameters</span><span class="sxs-lookup"><span data-stu-id="2c137-287">Parameters</span></span> | <span data-ttu-id="2c137-288">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2c137-288">Default</span></span> | <span data-ttu-id="2c137-289">Optimización</span><span class="sxs-lookup"><span data-stu-id="2c137-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c137-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="2c137-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="2c137-291">None</span><span class="sxs-lookup"><span data-stu-id="2c137-291">None</span></span> |<span data-ttu-id="2c137-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="2c137-292">7 GB</span></span> |
| <span data-ttu-id="2c137-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="2c137-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="2c137-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="2c137-294">5 MB</span></span> |<span data-ttu-id="2c137-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="2c137-295">512 MB</span></span> |
| <span data-ttu-id="2c137-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="2c137-296">**max_connections**</span></span> |<span data-ttu-id="2c137-297">100</span><span class="sxs-lookup"><span data-stu-id="2c137-297">100</span></span> |<span data-ttu-id="2c137-298">5.000</span><span class="sxs-lookup"><span data-stu-id="2c137-298">5000</span></span> |
| <span data-ttu-id="2c137-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="2c137-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="2c137-300">0</span><span class="sxs-lookup"><span data-stu-id="2c137-300">0</span></span> |<span data-ttu-id="2c137-301">1</span><span class="sxs-lookup"><span data-stu-id="2c137-301">1</span></span> |
| <span data-ttu-id="2c137-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="2c137-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="2c137-303">1</span><span class="sxs-lookup"><span data-stu-id="2c137-303">1</span></span> |<span data-ttu-id="2c137-304">2</span><span class="sxs-lookup"><span data-stu-id="2c137-304">2</span></span> |
| <span data-ttu-id="2c137-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="2c137-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="2c137-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="2c137-306">8 MB</span></span> |<span data-ttu-id="2c137-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="2c137-307">128 MB</span></span> |
| <span data-ttu-id="2c137-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="2c137-308">**query_cache_size**</span></span> |<span data-ttu-id="2c137-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="2c137-309">16 MB</span></span> |<span data-ttu-id="2c137-310">0</span><span class="sxs-lookup"><span data-stu-id="2c137-310">0</span></span> |

<span data-ttu-id="2c137-311">Para obtener más [parámetros de configuración de optimización](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), consulte toohello [instrucciones oficiales de MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="2c137-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="2c137-312">**Entorno de prueba**</span><span class="sxs-lookup"><span data-stu-id="2c137-312">**Test environment**</span></span>  

| <span data-ttu-id="2c137-313">Hardware</span><span class="sxs-lookup"><span data-stu-id="2c137-313">Hardware</span></span> | <span data-ttu-id="2c137-314">Detalles</span><span class="sxs-lookup"><span data-stu-id="2c137-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="2c137-315">CPU</span><span class="sxs-lookup"><span data-stu-id="2c137-315">CPU</span></span> |<span data-ttu-id="2c137-316">Procesador AMD Opteron(tm) 4171 HE/4 núcleos</span><span class="sxs-lookup"><span data-stu-id="2c137-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="2c137-317">Memoria</span><span class="sxs-lookup"><span data-stu-id="2c137-317">Memory</span></span> |<span data-ttu-id="2c137-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="2c137-318">14 GB</span></span> |
| <span data-ttu-id="2c137-319">Disco</span><span class="sxs-lookup"><span data-stu-id="2c137-319">Disk</span></span> |<span data-ttu-id="2c137-320">10 GB/disco</span><span class="sxs-lookup"><span data-stu-id="2c137-320">10 GB/disk</span></span> |
| <span data-ttu-id="2c137-321">SO</span><span class="sxs-lookup"><span data-stu-id="2c137-321">OS</span></span> |<span data-ttu-id="2c137-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="2c137-322">Ubuntu 14.04.1 LTS</span></span> |

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

