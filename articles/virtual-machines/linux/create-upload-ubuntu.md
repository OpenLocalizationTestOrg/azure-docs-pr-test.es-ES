---
title: aaaCreate y cargar un VHD de Ubuntu Linux en Azure
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contiene un sistema de operativo Ubuntu Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Preparación de una máquina virtual Ubuntu para Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>Imágenes oficiales de Ubuntu Cloud
Ahora Ubuntu publica VHD de Azure oficiales que se pueden descargar en [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/). Si se necesita toobuild su propia imagen Ubuntu especializada para Azure, en lugar de usa el procedimiento manual de Hola por debajo de él toostart recomendada con estas conocidas trabajando discos duros virtuales y personalizar según sea necesario. las versiones más recientes de imagen Hola siempre pueden encontrarse en hello ubicaciones siguientes:

* Ubuntu 12.04/precisa: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por supuesto que ya ha instalado un disco de duro virtual y tooa con sistema operativo Ubuntu Linux. Varias herramientas existen archivos .vhd de toocreate, por ejemplo, una solución de virtualización como Hyper-V. Para obtener instrucciones, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

**Notas de instalación de Ubuntu**

* Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.
* no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.  Puede convertir Hola disco tooVHD formato con el Administrador de Hyper-V u Hola cmdlet convert-vhd.
* Al instalar el sistema de Linux Hola se recomienda que utilice particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones). Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita toobe adjuntada tooanother VM para solucionar problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.
* No configure una partición de intercambio en el disco del sistema operativo de Hola. agente de Linux de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.  Para obtener más información acerca de este puede encontrarse en pasos Hola.
* Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.

## <a name="manual-steps"></a>Pasos manuales
> [!NOTE]
> Antes de intentar toocreate su propia imagen de Ubuntu personalizada para Azure, considere la posibilidad de usando Hola pregeneradas y probar imágenes de [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) en su lugar.
> 
> 

1. En el panel central de hello del Administrador de Hyper-V, seleccione máquina virtual de Hola.

2. Haga clic en **conectar** tooopen ventana de hello para la máquina virtual de Hola.

3. Reemplace repositorios actual de hello en repositorios de hello imagen toouse Ubuntu Azure. pasos de Hello varían ligeramente según la versión de Hola Ubuntu.
   
    Antes de editar `/etc/apt/sources.list`, es recomendable toomake una copia de seguridad:
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. Hello imágenes Ubuntu Azure están ahora siguiendo hello *habilitación de hardware* kernel (HWE). Actualizar kernel más reciente de toohello de sistema operativo de hello ejecutando Hola siguientes comandos:

    Ubuntu 12.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **Consulte también:**
    - [https://wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Modificar línea de arranque de kernel de Hola para los parámetros adicionales del núcleo de Grub tooinclude de Azure. toodo abrir este `/etc/default/grub` en un editor de texto, busque variable Hola denominada `GRUB_CMDLINE_LINUX_DEFAULT` (o agregarlo si es necesario) y editarlo hello tooinclude parámetros siguientes:
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    Guarde este archivo y ciérrelo, y ejecute `sudo update-grub`. Esto garantizará que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a obtener soporte técnico Azure con problemas de depuración.

6. Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.  Esto suele ser el predeterminado de Hola.

7. Instalar Hola agente Linux de Azure:
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    Hola `walinuxagent` paquete puede quitar hello `NetworkManager` y `NetworkManager-gnome` paquetes y, si están instalados.

8. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V. El VHD de Linux está ahora listo toobe había cargado tooAzure.

## <a name="next-steps"></a>Pasos siguientes
Se está ahora listo toouse sus Ubuntu Linux disco duro virtual toocreate nuevas máquinas virtuales en Azure. Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="references"></a>Referencias
Kernel de habilitación de hardware (HWE) de Ubuntu

* [http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

