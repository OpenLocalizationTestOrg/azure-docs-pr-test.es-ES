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
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>¿Cómo tooreset contraseñas locales de Linux en máquinas virtuales de Azure

Este artículo detallan contraseñas Linux Máquina Virtual (VM) de varios métodos tooreset local. Si la cuenta de usuario de hello ha expirado o simplemente desea toocreate una nueva cuenta, puede usar Hola siguiendo métodos toocreate una nueva cuenta de administrador local y volver a tener acceso toohello máquina virtual.

## <a name="symptoms"></a>Síntomas

No se puede registrar en toohello VM y recibirá un mensaje que indica la contraseña Hola que usó no es correcta. Además, no puede usar VMAgent tooreset la contraseña en hello Portal de Azure. 

## <a name="manual-password-reset-procedure"></a>Procedimiento de restablecimiento de contraseña manual

1.  Eliminar Hola VM y mantener discos Hola adjuntada.

2.  Adjuntar Hola unidad de sistema operativo como un tooanother de disco de datos temporales VM Hola misma ubicación.

3.  Ejecute hello siga comando SSH en hello temporal VM toobecome un superusuario.


    ~~~~
    sudo su
    ~~~~

4.  Ejecutar **fdisk -l** o vistazo Hola de toofind registros de sistema adjuntó recientemente el disco. Busque toomount de nombre de unidad de Hola. A continuación, en hello VM temporales, buscar en hello pertinente archivo de registro.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    Hola te mostramos la salida de ejemplo de comando grep de hello:

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Cree un punto de montaje denominado **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Montar el disco de SO hello en punto de montaje de Hola. Suele ser preciso toomount sdc1 o sdc2. Esto dependerá de Hola que aloja la partición en el directorio /etc desde el disco de máquina roto Hola.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  Realice una copia de seguridad antes de realizar cambios:

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  Restablecer la contraseña del usuario de Hola que necesita:

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Hola de movimiento modifica archivos toohello ubicación correcta Hola dividido el disco de la máquina.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    cd / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
