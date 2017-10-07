---
title: "contraseña aaaHow tooreset de Linux local en máquinas virtuales de Azure | Documentos de Microsoft"
description: "Introducir Hola pasos tooreset Hola Linux contraseña local en la máquina virtual de Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: 3827e32186c5f034d9bb6fc502dc26708b52a00a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="ff586-103">¿Cómo tooreset contraseñas locales de Linux en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="ff586-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="ff586-104">Este artículo detallan contraseñas Linux Máquina Virtual (VM) de varios métodos tooreset local.</span><span class="sxs-lookup"><span data-stu-id="ff586-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="ff586-105">Si la cuenta de usuario de hello ha expirado o simplemente desea toocreate una nueva cuenta, puede usar Hola siguiendo métodos toocreate una nueva cuenta de administrador local y volver a tener acceso toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ff586-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="ff586-106">Síntomas</span><span class="sxs-lookup"><span data-stu-id="ff586-106">Symptoms</span></span>

<span data-ttu-id="ff586-107">No se puede registrar en toohello VM y recibirá un mensaje que indica la contraseña Hola que usó no es correcta.</span><span class="sxs-lookup"><span data-stu-id="ff586-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="ff586-108">Además, no puede usar VMAgent tooreset la contraseña en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff586-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="ff586-109">Procedimiento de restablecimiento de contraseña manual</span><span class="sxs-lookup"><span data-stu-id="ff586-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="ff586-110">Eliminar Hola VM y mantener discos Hola adjuntada.</span><span class="sxs-lookup"><span data-stu-id="ff586-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="ff586-111">Adjuntar Hola unidad de sistema operativo como un tooanother de disco de datos temporales VM Hola misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="ff586-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="ff586-112">Ejecute hello siga comando SSH en hello temporal VM toobecome un superusuario.</span><span class="sxs-lookup"><span data-stu-id="ff586-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="ff586-113">Ejecutar **fdisk -l** o vistazo Hola de toofind registros de sistema adjuntó recientemente el disco.</span><span class="sxs-lookup"><span data-stu-id="ff586-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="ff586-114">Busque toomount de nombre de unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff586-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="ff586-115">A continuación, en hello VM temporales, buscar en hello pertinente archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="ff586-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="ff586-116">Hola te mostramos la salida de ejemplo de comando grep de hello:</span><span class="sxs-lookup"><span data-stu-id="ff586-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="ff586-117">Cree un punto de montaje denominado **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="ff586-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="ff586-118">Montar el disco de SO hello en punto de montaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff586-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="ff586-119">Suele ser preciso toomount sdc1 o sdc2.</span><span class="sxs-lookup"><span data-stu-id="ff586-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="ff586-120">Esto dependerá de Hola que aloja la partición en el directorio /etc desde el disco de máquina roto Hola.</span><span class="sxs-lookup"><span data-stu-id="ff586-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="ff586-121">Realice una copia de seguridad antes de realizar cambios:</span><span class="sxs-lookup"><span data-stu-id="ff586-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="ff586-122">Restablecer la contraseña del usuario de Hola que necesita:</span><span class="sxs-lookup"><span data-stu-id="ff586-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="ff586-123">Hola de movimiento modifica archivos toohello ubicación correcta Hola dividido el disco de la máquina.</span><span class="sxs-lookup"><span data-stu-id="ff586-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="ff586-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="ff586-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
