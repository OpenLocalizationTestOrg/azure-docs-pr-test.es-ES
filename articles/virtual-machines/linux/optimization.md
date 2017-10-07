---
title: aaaOptimize la VM de Linux en Azure | Documentos de Microsoft
description: "Obtenga información acerca de algunos toomake de sugerencias de optimización que ha configurado la VM de Linux para un rendimiento óptimo en Azure"
keywords: "máquina virtual con linux,máquina virtual linux,máquina virtual con ubuntu"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a>Optimización de la máquina virtual Linux en Azure
Crear una máquina virtual (VM) de Linux es fácil toodo desde línea de comandos de Hola o desde el portal de Hola. Este tutorial muestra cómo tooensure ha configurado toooptimize su rendimiento en la plataforma de Microsoft Azure Hola. Este tema usa una VM de servidor Ubuntu, pero también puede crear máquinas virtuales Linux mediante [sus propias imágenes como plantillas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="prerequisites"></a>Requisitos previos
En este tema se da por supuesto que ya tiene una suscripción de Azure activa ([suscripción de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) y ya ha aprovisionado una VM en su suscripción de Azure. Asegúrese de que tiene más reciente hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooyour suscripción de Azure con [inicio de sesión de az](/cli/azure/#login) antes de [crear una máquina virtual](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-os-disk"></a>Disco de sistema operativo de Azure
Al crear la VM Linux en Azure, tiene dos discos asociados a ella. **/dev/sda** es el disco del SO y **/dev/sdb** es el disco temporal.  No utilice el disco del sistema operativo principal hello (**/dev/sda**) para todo excepto el sistema operativo de hello tal y como está optimizado para el tiempo de inicio rápido de VM y no proporciona un buen rendimiento de las cargas de trabajo. Desea tooattach uno o más discos tooyour VM tooget persistente y optimizado almacenamiento para los datos. 

## <a name="adding-disks-for-size-and-performance-targets"></a>Adición de discos para objetivos de rendimiento y tamaño
En función de hello tamaño de máquina virtual, puede adjuntar too16 discos adicionales en una serie a, 32 discos de la serie D y 64 discos en un equipo de la serie G - cada uno de ellos hasta too1 TB de tamaño. Agregue discos adicionales según sea necesario en función del espacio y los requisitos de IOPS. Cada disco tiene un objetivo de rendimiento de 500 IOps para el almacenamiento estándar y la too5000 de IOps por disco de almacenamiento Premium.  Para más información sobre los discos de Premium Storage, consulte [Discos de máquina virtual de Azure administrados y no administrados, y Premium Storage de alto rendimiento](../../storage/common/storage-premium-storage.md).

tooachieve Hola mayores IOps en discos de almacenamiento Premium que su configuración de caché se ha establecido tooeither **ReadOnly** o **ninguno**, debe deshabilitar **barreras** mientras sistema de archivos de montaje hello en Linux. No es necesario barreras porque Hola escribe tooPremium almacenamiento de discos de copia de seguridad son duraderos para esta configuración de caché.

* Si usa **reiserFS**, barreras deshabilitar mediante la opción de montaje de hello `barrier=none` (para habilitar las barreras, use `barrier=flush`)
* Si usa **ext3/ext4**, barreras deshabilitar mediante la opción de montaje de hello `barrier=0` (para habilitar las barreras, use `barrier=1`)
* Si usa **XFS**, barreras deshabilitar mediante la opción de montaje de hello `nobarrier` (para habilitar las barreras que existen, utilice opción de hello `barrier`)

## <a name="unmanaged-storage-account-considerations"></a>Consideraciones de la cuenta de almacenamiento no administrada
acción de Hello predeterminada cuando se crea una máquina virtual con hello Azure CLI 2.0 es toouse Azure administra discos.  Estos discos se controlan mediante la plataforma Windows Azure hello y no requieren ningún toostore los preparativos o ubicación ellos.  Los discos no administrados requieren una cuenta de almacenamiento y tienen algunas consideraciones de rendimiento adicionales.  Para más información acerca de los discos administrados, consulte [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Introducción a los discos administrados de Azure).  Hello siguiente sección describen las consideraciones de rendimiento solo al usar discos no administrados.  Hola de nuevo, de forma predeterminada y solución de almacenamiento recomendada es discos toouse administrado.

Si crea una máquina virtual con discos no administrados, asegúrese de que conectar discos de cuentas de almacenamiento que residen en hello misma región que la máquina virtual tooensure cercanos y minimizar la latencia de red.  Cada cuenta de almacenamiento estándar tiene un máximo de IOPS de 20 k y una capacidad de tamaño de 500 TB.  Este límite resuelve discos tooapproximately 40 que se usa mucho incluidos disco Hola OS y los discos de datos que cree. Para las cuentas de Almacenamiento premium, no hay ningún límite máximo de IOPS, pero hay un límite de tamaño de 32 TB. 

Al tratar con cargas de trabajo de e/s por segundo alto y ha elegido almacenamiento estándar para los discos, puede que tenga discos de hello toosplit a través de varios toomake de cuentas de almacenamiento seguro que no haya alcanzado Hola 20.000 IOps limitar las cuentas de almacenamiento estándar. La máquina virtual puede contener una combinación de discos de a través de diferentes cuentas de almacenamiento y tooachieve de tipos de cuenta de almacenamiento su configuración óptima.
 

## <a name="your-vm-temporary-drive"></a>Su unidad temporal de máquina virtual
De forma predeterminada, cuando se crea una VM, Azure proporciona un disco de SO (**/dev/sda**) y un disco temporal (**/dev/sdb**).  Todos los discos adicionales que se agreguen se mostrarán como **/dev/sdc**, **/dev/sdd**, **/dev/sde**, etc. Todos los datos del disco temporal (**/dev/sdb**) no son duraderos y se pueden perder si eventos específicos, como el cambio de tamaño de la VM, la reimplementación o el mantenimiento, fuerzan un reinicio de la VM.  tamaño de Hola y el tipo de disco temporal es tamaño VM toohello relacionados elegido durante la implementación. Todos unidad temporal de Hola de máquinas virtuales (serie DS, G y DS_V2) de tamaño de hello premium están respaldadas por una SSD local para obtener un rendimiento adicional de seguridad too48k e/s por segundo. 

## <a name="linux-swap-file"></a>Archivo de intercambio de Linux
Si la VM de Azure es de una imagen Ubuntu o CoreOS, a continuación, puede usar CustomData toosend una configuración de nube toocloud-init. Si [cargó una imagen personalizada de Linux](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que usa cloud-init, configure también particiones de intercambio mediante cloud-init.

En imágenes de nube Ubuntu, debe usar la partición de intercambio de nube init tooconfigure Hola. Para más información, consulte [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

Para las imágenes sin compatibilidad con la nube init, imágenes de máquina virtual que se implementan a partir de hello Azure Marketplace tienen un agente de Linux de VM integrado con hello SO. Este agente permite Hola VM toointeract con varios servicios de Azure. Suponiendo que haya implementado una imagen estándar de hello Azure Marketplace, sería necesario toodo Hola después toocorrectly configura los valores del archivo de intercambio de Linux:

Localizar y modificar las dos entradas de hello **/etc/waagent.conf** archivo. Controlar el tamaño del archivo de intercambio de Hola y la existencia de Hola de un archivo de intercambio dedicado. parámetros de Hello desea toomodify son `ResourceDisk.EnableSwap=N` y`ResourceDisk.SwapSizeMB=0` 

Cambiar Hola parámetros toohello después de configuración:

* ResourceDisk.EnableSwap=Y
* ResourceDisk.SwapSizeMB={size en MB toomeet sus necesidades} 

Una vez haya realizado Hola cambiar, necesita toorestart hello waagent o reiniciar la VM de Linux tooreflect esos cambios.  Sabrá cambios Hola se han implementado y se ha creado un archivo de intercambio cuando usas hello `free` comando tooview de espacio libre. el ejemplo siguiente se Hello tiene un archivo de intercambio de 512MB creado como resultado de la modificación de hello **waagent.conf** archivo:

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a>Algoritmo de programación de E/S para Almacenamiento premium
Con el kernel de Linux de hello 2.6.18, algoritmo de programación de E/S Hola predeterminado se cambió de fecha límite tooCFQ (completamente algoritmo de cola). Para patrones de E/S de acceso aleatorio, hay una diferencia insignificante en diferencias de rendimiento entre CFQ y Deadline.  Para discos basados en SSD donde patrón de E/S de disco de hello es básicamente secuencial, cambiar de nuevo toohello NOOP o fecha límite de algoritmo puede lograr un mejor rendimiento de E/S.

### <a name="view-hello-current-io-scheduler"></a>Programador de E/S de vista Hola actual
Usar hello siguiente comando:  

```bash
cat /sys/block/sda/queue/scheduler
```

Vea el siguiente resultado, lo que indica el programador actual Hola.  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a>Cambiar Hola actual dispositivo (/ dev/sda) del algoritmo de programación de E/S
Usar hello siguientes comandos:  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> Aplicar este valor solo para **/dev/sda** no es útil. Establecer en todos los discos de datos donde E/S secuenciales domina patrón de E/S de Hola.  

Debería ver Hola después de salida, lo que indica que **grub.cfg** se ha vuelto a generar correctamente y programador predeterminado Hola se ha actualizado tooNOOP.  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

Para la familia de distribución de Redhat hello, solo necesita Hola siguiente comando:   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a>Con RAID de Software tooachieve superior I / Ops
Si las cargas de trabajo requieren más IOps de lo que puede proporcionar un único disco, deberá toouse una configuración de RAID de software de varios discos. Dado que Azure ya realiza resistencia de disco en la capa de tejido local de hello, lograr mayor nivel de Hola de rendimiento de una configuración de creación de bandas RAID-0.  Aprovisionar y crear discos Hola entorno de Azure y conéctelas tooyour Linux VM antes de creación de particiones, dar formato y montar Hola unidades.  Para obtener más información acerca de cómo configurar una configuración RAID de software en la VM de Linux en azure puede encontrarse en hello  **[configuración RAID de Software en Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**  documento.

## <a name="next-steps"></a>Pasos siguientes
Recuerde que, como con todas las discusiones de optimización, es preciso tooperform pruebas antes y después de cada impacto de cambio toomeasure Hola Hola cambio tiene.  La optimización es un proceso paso a paso que tiene resultados diferentes en las distintas máquinas en su entorno.  Lo que funciona para una configuración puede no funcionar para otras.

Algunos recursos de tooadditional vínculos útiles: 

* [Almacenamiento premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../storage/common/storage-premium-storage.md)
* [Guía de usuario del Agente de Linux de Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Optimización del rendimiento de MySQL en máquinas virtuales de Azure con Linux](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configuración del software RAID en Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

