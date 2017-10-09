---
title: aaaCreate y cargar un VHD de Linux en Azure
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contiene un sistema operativo Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>Información para las distribuciones no aprobadas
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

plataforma Windows Azure SLA Hello aplica máquinas toovirtual ejecutando Hola sistema operativo de Linux sólo cuando uno de hello [están aprobados distribuciones](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se utiliza. Todas las distribuciones de Linux que se proporcionan en hello Azure son Galería de imágenes están aprobados distribuciones con la configuración necesaria de Hola.

* [Linux en distribuciones aprobadas por Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Compatibilidad con las imágenes de Linux en Microsoft Azure](https://support.microsoft.com/kb/2941892)

Todas las distribuciones que se ejecuta en Azure deberá toomeet una serie de requisitos previos toohave un tooproperly ocasión se ejecuta en plataforma Hola.  En este artículo es una lista de ninguna manera completo como cada distribución es diferente; y es bastante posible que incluso si se cumplen todos los criterios de hello siguiente que seguirá siendo necesario toosignificantly retocar la tooensure de sistema de Linux que se ejecuta correctamente en la plataforma de Hola.

Por eso recomendamos que empiece con una de nuestras [distribuciones aprobadas de Linux en Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) cuando sea posible. Hello siguientes artículos le ayudará a cómo tooprepare Hola distintos con el respaldo de las distribuciones de Linux que se admiten en Azure:

* **[Distribuciones basadas en CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES y openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

resto de Hola de este artículo se centrará en instrucciones generales para ejecutar la distribución de Linux en Azure.

## <a name="general-linux-installation-notes"></a>Notas generales sobre la instalación de Linux
* no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.  Puede convertir Hola disco tooVHD formato con el Administrador de Hyper-V u Hola cmdlet convert-vhd. Si usas VirtualBox Esto significa seleccionar **tamaño fijo** como opone predeterminado toohello asignada de forma dinámica al crear el disco de Hola.
* Azure solo admite máquinas virtuales de la generación 1. Puede convertir una generación 1 máquina virtual desde el formato de archivo de disco duro virtual de VHDX toohello y de expansión dinámica tooa fijada de tamaño de disco. Sin embargo, no puede cambiar la generación de una máquina virtual. Para obtener más información, vea [¿Debería crear una máquina virtual de generación 1 o 2 en Hyper-V?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)
* Hola tamaño máximo permitido para hello VHD 1.023 GB.
* Al instalar el sistema de Linux de hello es *recomienda* utilizar particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones). Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita tooanother toobe adjunta VM idéntico para solucionar el problema. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos.
* Se requiere la compatibilidad de kernel para el montaje de sistemas de archivos UDF. En el primer arranque en hello Azure configuración del aprovisionamiento pasa toohello VM de Linux a través de medios con formato UDF que está invitado toohello adjunto. agente de Linux de Azure de Hello debe ser capaz de toomount Hola UDF archivo sistema tooread su configuración y aprovisionar Hola VM.
* Las versiones de kernel de Linux inferiores a la versión 2.6.37 no admiten NUMA en Hyper-V con tamaños de VM más grandes. Este problema afecta principalmente distribuciones anteriores mediante hello en dirección ascendente kernel de Red Hat 2.6.32 y se ha corregido en RHEL 6.6 (kernel-2.6.32-504). Sistemas que ejecutan kernels personalizados anteriores a 2.6.37 o basado en RHEL kernels anteriores que se debe establecer 2.6.32-504 Hola parámetro de arranque `numa=off` en kernel Hola de línea de comandos en grub.conf. Para obtener más información, consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* No configure una partición de intercambio en el disco del sistema operativo de Hola. agente de Linux de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.  Para obtener más información acerca de este puede encontrarse en pasos Hola.
* Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.

### <a name="installing-kernel-modules-without-hyper-v"></a>Instalación de los módulos de kernel sin Hyper-V
Azure se ejecuta en hipervisor de Hyper-V de hello, por lo que Linux requiere que ciertos módulos de kernel se instalan en orden toorun en Azure. Si tiene una máquina virtual que se creó fuera de Hyper-V, instaladores de Linux Hola pueden no incluir Hola controladores para Hyper-V en ramdisk inicial de hello (initrd o initramfs) a menos que detecte que se está ejecutando un entorno de Hyper-V. Cuando se usa un tooprepare del sistema (es decir, Virtualbox, KVM, etc.) de virtualización distinto de la imagen de Linux, puede que necesite toorebuild Hola initrd tooensure que al menos Hola `hv_vmbus` y `hv_storvsc` módulos kernel están disponibles en ramdisk inicial Hola.  Esto es un problema conocido al menos en sistemas basados en la distribución de Red Hat de nivel superior de Hola.

mecanismo de Hola para volver a generar Hola initrd o initramfs una imagen puede variar en función de distribución de Hola. Por favor, consulte la documentación de la distribución o de procedimiento correcto de Hola.  Este es un ejemplo de cómo toorebuild Hola initrd con hello `mkinitrd` utilidad:

En primer lugar, realizar copias de seguridad Hola existente initrd imagen:

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

A continuación, volver a generar Hola initrd con hello `hv_vmbus` y `hv_storvsc` módulos kernel:

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>Cambio de tamaño de los discos duros virtuales
Imágenes de disco duro virtual en Azure deben tener un too1MB virtual alineada con el tamaño.  Normalmente, los discos duros virtuales creados con Hyper-V ya deben alinearse correctamente.  Si Hola VHD no está alineada correctamente, a continuación, es posible que reciba un error mensaje similares toohello siguientes cuando se intente toocreate una *imagen* desde el disco duro virtual:

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy Esto puede cambiar el tamaño Hola máquina virtual mediante la consola de administrador de Hyper-V de Hola o hello [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) cmdlet de Powershell.  Si no se está ejecutando en un entorno de Windows, a continuación, se recomienda toouse qemu img tooconvert (si es necesario) y cambiar el tamaño de disco duro virtual de Hola.

> [!NOTE]
> Hay un problema conocido en versiones de qemu-img >= 2.2.1 que da como resultado un VHD con formato incorrecto. se ha solucionado el problema de Hello en QEMU 2.6. Se recomienda toouse qemu-img 2.2.0 o inferior o actualización too2.6 o superior. Referencia: https://bugs.launchpad.net/qemu/+bug/1490611.
> 
> 

1. Cambiar el tamaño de Hola VHD directamente con herramientas como `qemu-img` o `vbox-manage` puede dar lugar a un disco duro virtual no se pueda arrancar.  Por lo tanto, se recomienda toofirst convert Hola imagen de disco sin procesar de tooa de disco duro virtual.  Si ya se creó la imagen VM de hello como imagen de disco sin procesar (predeterminado de Hola para algunos hipervisores como KVM), a continuación, puede omitir este paso:
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. Calcular Hola necesaria de tamaño de tooensure de imagen de disco de Hola que Hola tamaño virtual es too1MB alineado.  Hola siguiente secuencia de comandos de shell de bash puede ayudarle con esto.  script de Hola usa "`qemu-img info`" toodetermine Hola virtual tamaño de imagen de disco de hello y, a continuación, calcula Hola tamaño toohello siguiente 1 MB:
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. Cambiar el tamaño de disco sin procesar de hello mediante $rounded_size como se establece en hello por encima de la secuencia de comandos:
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. Ahora, convierta tooa atrás de disco sin procesar de hello VHD de tamaño fijo:
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   O bien, con la versión de qemu **2.6 +** incluyen hello `force_size` opción:

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Requisitos para el kernel de Linux
Hello controladores de servicios de integración de Linux (LIS) para Hyper-V y Azure se aportan directamente toohello ascendente kernel de Linux. Muchas de las distribuciones que incluyen una versión reciente del kernel de Linux (por ejemplo, 3.x) ya tendrán estos controladores disponibles, o de lo contrario ofrecerán versiones con modificaciones de versiones anteriores de estos controladores con sus kernel.  Estos controladores se actualizan constantemente en el núcleo de nivel superior Hola con correcciones y características, por lo que siempre que sea posible, se recomienda toorun una [están aprobados distribución](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que incluyen estas correcciones y actualizaciones.

Si está ejecutando una variante de versiones de Red Hat Enterprise Linux **6.0 6.3**, necesitará controladores de tooinstall hello más recientes LIS para Hyper-V. pueden encontrar controladores de Hello [en esta ubicación](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409). A partir de RHEL **6.4 +** (y derivados) controladores LIS Hola ya están incluidos con kernel hello y por lo que ningún paquete de instalación adicionales es necesario toorun esos sistemas en Azure.

Si se requiere un kernel personalizado, es recomendable toouse una versión más reciente de kernel (es decir, **3.8 +**). Para los proveedores que mantienen su propios kernel o los distribuciones, algunos esfuerzo será necesario tooregularly de atrás Hola LIS controladores del kernel de hello kernel ascendente tooyour personalizado de.  Incluso si ya está ejecutando una versión de kernel relativamente recientes, se recomienda encarecidamente tookeep realizar un seguimiento de cualquier en dirección ascendente correcciones en Atrás y controladores LIS hello las según sea necesario. ubicación de Hola Hola LIS origen de archivos de controlador está disponible en hello [MANTENEDORES](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) archivo hello Linux kernel árbol de origen:

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

Como mínimo, ausencia de Hola de hello después revisiones famosos toocause problemas en Azure y por lo que estos deben incluirse en el núcleo de Hola. Esta lista no es exhaustiva ni está completa para todas las distribuciones:

* [ata_piix: aplazar controladores de discos toohello Hyper-V de forma predeterminada](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc: la cuenta para los paquetes en tránsito en la ruta de acceso de restablecimiento de Hola](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc: Evitar el uso de WRITE_SAME](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc: Deshabilita WRITE SAME para RAID y controladores del adaptador de host virtual](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc: Corrección de desreferenciación del puntero NULL](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc: Los errores de búfer de anillo pueden dar lugar a una inmovilización de E/S](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs: Protección contra la ejecución doble de __scsi_remove_device](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>Hola agente Linux de Azure
Hola [agente Linux de Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) se requiere tooproperly aprovisionar una máquina virtual de Linux en Azure. Puede obtener la versión más reciente de hello, problemas de archivos o enviar solicitudes de extracción en hello [repositorio de GitHub de agente de Linux](https://github.com/Azure/WALinuxAgent).

* agente de Linux Hola se libera bajo licencia de Apache 2.0 Hola. Número de distribuciones ya proporciona RPM o deb paquetes para agente de hello, y por lo que en algunos casos esto se puede instalar y actualizar con poco esfuerzo.
* Hola agente Linux de Azure requiere Python v2.6 +.
* agente de Hello también requiere el módulo de python pyasn1 de Hola. La mayoría de distribuciones lo proporcionan como un paquete independiente que se puede instalar.
* En algunos casos es posible que no sea compatible con NetworkManager Hola agente Linux de Azure. Muchos de los paquetes RPM/Deb Hola proporcionados por las distribuciones configuración NetworkManager como un paquete de waagent toohello de conflicto y, por tanto, desinstalarán NetworkManager al instalar paquetes de agente de Linux Hola.

## <a name="general-linux-system-requirements"></a>Requisitos generales del sistema Linux

* Modificar línea de arranque de kernel de hello en GRUB o GRUB2 hello tooinclude parámetros siguientes. Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas:
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.
  
    Además toohello anterior, se recomienda demasiado*quitar* Hola siguientes parámetros si existen:
  
        rhgb quiet crashkernel=auto
  
    Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie. Hola `crashkernel` opción puede ser izquierda configurado si lo desea, pero tenga en cuenta que este parámetro reducirá la cantidad de Hola de memoria disponible en hello máquina virtual por medio de 128 MB o más, lo que puede ser problemático en tamaños VM de hello más pequeños.

* Hola instalar Agente Linux de Azure
  
    Hola agente Linux de Azure es necesario para el aprovisionamiento de una imagen de Linux en Azure.  Número de distribuciones proporciona agente Hola como un paquete RPM o Deb (normalmente se denomina paquete hello 'WALinuxAgent' o 'walinuxagent').  Hello agente también se puede instalar manualmente siguiendo los pasos de Hola Hola [Guía de agente de Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

* Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.  Esto suele ser el predeterminado de Hola.

* No cree el espacio de intercambio en el disco del sistema operativo de Hola
  
    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure. Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned. Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en /etc/waagent.conf siguientes correctamente:
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* Como paso final, ejecute hello después de la máquina virtual de comandos toodeprovision hello:
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > En Virtualbox se puede ver Hola siguiente error después de ejecutar ' waagent-force - desaprovisionamiento ': `[Errno 5] Input/output error`. Este mensaje de error no es crítico, por lo que se puede omitir.
  > 
  > 

* A continuación, necesitará tooshut hacia abajo de la máquina virtual de Hola y cargar hello tooAzure de disco duro virtual.

