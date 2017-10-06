---
title: un disco duro virtual en Azure de Debian Linux aaaPrepare | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate Debian 7 & VHD 8 archivos para su implementación en Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a>Preparar VHD en Debian de Azure
## <a name="prerequisites"></a>Requisitos previos
En esta sección se da por supuesto que ya ha instalado un sistema operativo Linux Debian desde un archivo .iso descargado de hello [sitio Web Debian](https://www.debian.org/distrib/) tooa disco duro. Varias herramientas existen archivos .vhd de toocreate; Hyper-V es sólo un ejemplo. Para obtener instrucciones con Hyper-V, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](https://technet.microsoft.com/library/hh846766.aspx).

## <a name="installation-notes"></a>Notas de instalación
* Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.
* no se admite el formato VHDX más reciente de Hello en Azure. Puede convertir el formato de tooVHD de disco hello mediante el Administrador de Hyper-V o hello **convert-vhd** cmdlet.
* Al instalar el sistema de Linux Hola se recomienda que utilice particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones). Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita toobe adjuntada tooanother VM para solucionar problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.
* No configure una partición de intercambio en el disco del sistema operativo de Hola. agente de Linux de Azure de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola. Para obtener más información acerca de este puede encontrarse en pasos Hola.
* Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.

## <a name="use-azure-manage-toocreate-debian-vhds"></a>Use Administración de Azure toocreate Debian discos duros virtuales
Hay herramientas disponibles para generar Debian discos duros virtuales de Azure, por ejemplo, hello [azure-administrar](https://github.com/credativ/azure-manage) secuencias de comandos de [credativ](http://www.credativ.com/). Se trata de hello recomendada enfoque frente a crear una imagen desde el principio. Por ejemplo, toocreate un VHD de 8 Debian ejecutar Hola seguir comandos de administración de azure toodownload (y las dependencias) y ejecutar secuencias de comandos de hello azure_build_image:

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>Preparación manual de un VHD Debian
1. En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.
2. Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.
3. Comentario de línea de Hola para **deb CD-ROM** en `/etc/apt/source.list` si configuras Hola VM contra un archivo ISO.
4. Editar hello `/etc/default/grub` archivo y modifique hello **GRUB_CMDLINE_LINUX** parámetro manera parámetros adicionales del núcleo de tooinclude de Azure.
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. Vuelva a grub hello y ejecute:
   
        # sudo update-grub
6. Agregue repositorios Azure too/etc/apt/sources.list de Debian para Debian 7 u 8:
   
    **Debian 7.x "Wheezy"**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8.x "Jessie"**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. Instalar Hola agente Linux de Azure:
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Debian 7, resulta kernel de 3.16-based Hola de toorun necesario del repositorio de wheezy backports Hola. En primer lugar, cree un archivo denominado /etc/apt/preferences.d/linux.pref con hello siguiente contenido:
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    A continuación, ejecute "sudo apt-get instalar linux-image-amd64" tooinstall Hola nueva núcleo.
3. Cancelar el aprovisionamiento de máquina virtual de Hola y prepararlo para el aprovisionamiento en Azure y ejecute:
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. Haga clic en **Acción** -> Apagar en el Administrador de Hyper-V. El VHD de Linux está ahora listo toobe había cargado tooAzure.

## <a name="next-steps"></a>Pasos siguientes
Se está ahora listo toouse sus disco duro Debian toocreate nuevas máquinas virtuales en Azure. Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

