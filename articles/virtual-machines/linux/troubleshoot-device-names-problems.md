---
title: "nombres de dispositivos de máquina virtual de aaaLinux se cambian en Azure | Documentos de Microsoft"
description: "Explica Hola ¿por qué se cambian los nombres de los dispositivos y proporcionan soluciones para este problema."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="75008-103">Solución de problemas: Se cambian los nombres de dispositivo de máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="75008-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="75008-104">Hola, se explica por qué se cambian los nombres de los dispositivos después de reiniciar una máquina virtual (VM) de Linux o volver a adjuntar discos Hola.</span><span class="sxs-lookup"><span data-stu-id="75008-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="75008-105">También proporciona soluciones de Hola para este problema.</span><span class="sxs-lookup"><span data-stu-id="75008-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="75008-106">Síntoma</span><span class="sxs-lookup"><span data-stu-id="75008-106">Symptom</span></span>

<span data-ttu-id="75008-107">Puede experimentar Hola los siguientes problemas al ejecutar máquinas virtuales de Linux en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="75008-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="75008-108">Hola VM produce un error tooboot después del reinicio.</span><span class="sxs-lookup"><span data-stu-id="75008-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="75008-109">Si los discos de datos se separa y volver a adjuntar, los nombres de dispositivos de Hola para discos cambian.</span><span class="sxs-lookup"><span data-stu-id="75008-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="75008-110">Se produce un error en una aplicación o un script que hace referencia a un disco con el nombre de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="75008-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="75008-111">Buscar ese Hola se cambia el nombre de dispositivo de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="75008-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="75008-112">Causa</span><span class="sxs-lookup"><span data-stu-id="75008-112">Cause</span></span>

<span data-ttu-id="75008-113">Rutas de acceso de dispositivo en Linux no se garantiza sean toobe coherente entre los distintos reinicios.</span><span class="sxs-lookup"><span data-stu-id="75008-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="75008-114">Los nombres de dispositivo constan de números principales (letras) y secundarios.</span><span class="sxs-lookup"><span data-stu-id="75008-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="75008-115">Cuando el controlador de dispositivo de almacenamiento de hello Linux detecta un nuevo dispositivo, asigna tooit de números de dispositivo principal y secundaria de intervalo disponible Hola.</span><span class="sxs-lookup"><span data-stu-id="75008-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="75008-116">Cuando se quita un dispositivo, los números de dispositivo de hello son liberado toobe volver a usar más adelante.</span><span class="sxs-lookup"><span data-stu-id="75008-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="75008-117">Hello problema se produce porque hello análisis en Linux programada por el subsistema de SCSI de hello de dispositivo realiza de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="75008-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="75008-118">nombres de ruta de acceso de dispositivo final Hola pueden variar entre los distintos reinicios.</span><span class="sxs-lookup"><span data-stu-id="75008-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="75008-119">Solución</span><span class="sxs-lookup"><span data-stu-id="75008-119">Solution</span></span>

<span data-ttu-id="75008-120">tooresolve este problema, utilice nombres persistente.</span><span class="sxs-lookup"><span data-stu-id="75008-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="75008-121">Hay cuatro toopersistent métodos nomenclatura - etiqueta de filesystem, uuid, por Id. y ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="75008-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="75008-122">Se recomienda etiqueta del sistema de archivos de Hola y métodos UUID para máquinas virtuales de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="75008-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="75008-123">Cualquier hello también proporciona la mayoría de las distribuciones **nofail** o **nobootwait** fstab opciones.</span><span class="sxs-lookup"><span data-stu-id="75008-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="75008-124">Estas opciones permiten un tooboot sistema aunque hello tiene un error toomount durante el inicio.</span><span class="sxs-lookup"><span data-stu-id="75008-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="75008-125">Consulte la documentación de la distribución de Hola para obtener más información acerca de estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="75008-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="75008-126">Para obtener más información acerca de cómo tooconfigure un toouse de VM de Linux un UUID cuando se agrega un disco de datos, vea [conectar toohello nuevo disco de VM de Linux toomount hello](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="75008-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="75008-127">Cuando se instala el agente de Linux de Azure de hello en una máquina virtual, usa Udev reglas tooconstruct un conjunto de vínculos simbólicos en **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="75008-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="75008-128">Estas reglas de Udev pueden ser utilizadas por aplicaciones y discos de tooidentify de secuencias de comandos están conectado toohello máquina virtual, su tipo y Hola LUN.</span><span class="sxs-lookup"><span data-stu-id="75008-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="75008-129">Más información</span><span class="sxs-lookup"><span data-stu-id="75008-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="75008-130">Identificar LUN de disco</span><span class="sxs-lookup"><span data-stu-id="75008-130">Identify disk LUNs</span></span>

<span data-ttu-id="75008-131">Una aplicación puede utilizar LUN toofind todos los discos de hello adjuntada y construir los vínculos simbólicos.</span><span class="sxs-lookup"><span data-stu-id="75008-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="75008-132">agente de Linux de Azure de Hola ahora incluye reglas de udev que configure los vínculos simbólicos de un dispositivo de toohello LUN, como sigue:</span><span class="sxs-lookup"><span data-stu-id="75008-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="75008-133">También se puede recuperar la información de LUN de invitado de Linux de hello con lsscsi o una herramienta similar como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="75008-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="75008-134">Esta información de LUN de invitado puede utilizarse con suscripción de Azure tooidentify Hola ubicación de los metadatos en el almacenamiento de Azure de disco duro virtual que almacena los datos de la partición de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="75008-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="75008-135">Por ejemplo, use Hola az cli:</span><span class="sxs-lookup"><span data-stu-id="75008-135">For example, use hello az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="75008-136">Detectar UUID del sistema de archivos mediante blkid</span><span class="sxs-lookup"><span data-stu-id="75008-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="75008-137">Un script o una aplicación puede leer la salida de hello de blkid o fuentes de información similares y crear vínculos simbólicos en **/dev** para su uso.</span><span class="sxs-lookup"><span data-stu-id="75008-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="75008-138">salida de Hello mostrará Hola UUID de todos los discos conectados toohello hello y VM dispositivo archivo toowhich están asociados:</span><span class="sxs-lookup"><span data-stu-id="75008-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="75008-139">reglas de udev de Hello waagent construcción un conjunto de vínculos simbólicos en **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="75008-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="75008-140">aplicación Hello puede utilizar esta información identificar el dispositivo de disco de arranque de Hola y el disco de recursos (efímero) Hola.</span><span class="sxs-lookup"><span data-stu-id="75008-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="75008-141">En Azure, las aplicaciones deben hacer referencia demasiado**/dev/disk/azure/root-part1** o **/dev/disk/azure-resource-part1** toodiscover estas particiones.</span><span class="sxs-lookup"><span data-stu-id="75008-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="75008-142">Si hay particiones adicionales desde la lista de blkid hello, residen en un disco de datos.</span><span class="sxs-lookup"><span data-stu-id="75008-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="75008-143">Las aplicaciones puedan mantener Hola UUID para estas particiones y usar una ruta de acceso como Hola por debajo del nombre de dispositivo de hello toodiscover en tiempo de ejecución:</span><span class="sxs-lookup"><span data-stu-id="75008-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="75008-144">Obtener reglas de almacenamiento de Azure más recientes de Hola</span><span class="sxs-lookup"><span data-stu-id="75008-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="75008-145">reglas de almacenamiento de Azure más recientes de toohello, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="75008-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="75008-146">Para obtener más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="75008-146">For more information, see hello following articles:</span></span>

- <span data-ttu-id="75008-147">[Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID) (Ubuntu: Uso de UUID)</span><span class="sxs-lookup"><span data-stu-id="75008-147">[Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID)</span></span>

- <span data-ttu-id="75008-148">[Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) (Red Hat: Nomenclatura persistente)</span><span class="sxs-lookup"><span data-stu-id="75008-148">[Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)</span></span>

- <span data-ttu-id="75008-149">[Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you) (Linux: ¿Qué pueden hacer los UUID por usted?)</span><span class="sxs-lookup"><span data-stu-id="75008-149">[Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you)</span></span>

- [<span data-ttu-id="75008-150">UDev: Introducción tooDevice administración en el sistema Linux moderna</span><span class="sxs-lookup"><span data-stu-id="75008-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

