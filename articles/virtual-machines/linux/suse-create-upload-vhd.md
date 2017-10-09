---
title: aaaCreate y cargar un VHD de SUSE Linux en Azure
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contiene un sistema operativo SUSE Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Preparación de una máquina virtual SLES u openSUSE para Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por supuesto que ya ha instalado un SUSE o openSUSE disco de duro virtual de tooa de sistema operativo de Linux. Varias herramientas existen archivos .vhd de toocreate, por ejemplo, una solución de virtualización como Hyper-V. Para obtener instrucciones, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="sles--opensuse-installation-notes"></a>Notas sobre la instalación de SLES/openSUSE
* Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.
* no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.  Puede convertir Hola disco tooVHD formato con el Administrador de Hyper-V u Hola cmdlet convert-vhd.
* Al instalar el sistema de Linux Hola se recomienda que utilice particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones). Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita toobe adjuntada tooanother VM para solucionar problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.
* No configure una partición de intercambio en el disco del sistema operativo de Hola. agente de Linux de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.  Para obtener más información acerca de este puede encontrarse en pasos Hola.
* Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.

## <a name="use-suse-studio"></a>Uso de SUSE Studio
[SUSE Studio](http://www.susestudio.com) puede crear y administrar fácilmente sus imágenes de SLES y openSUSE para Hyper-V y Azure. Se trata de hello enfoque para personalizar sus propias imágenes SLES y openSUSE recomendado.

Como una alternativa toobuilding su propio VHD, SUSE también publica imágenes BYOS (poner su propia suscripción) para SLES en [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>Preparación de SUSE Linux Enterprise Server 11 SP4
1. En el panel central de hello del Administrador de Hyper-V, seleccione máquina virtual de Hola.
2. Haga clic en **conectar** tooopen ventana de hello para la máquina virtual de Hola.
3. Registrar su tooallow de sistema de SUSE Linux Enterprise se toodownload actualizaciones y paquetes de instalación.
4. Actualizar sistema Hola con las últimas revisiones de hello:
   
        # sudo zypper update
5. Instalar Hola agente Linux de Azure desde el repositorio SLES hello:
   
        # sudo zypper install WALinuxAgent
6. Compruebe si waagent se establece demasiado "on" en chkconfig y, si no es así, puede habilitarla para inicio automático:
   
        # sudo chkconfig waagent on
7. Compruebe si el servicio waagent se está ejecutando y, en caso contrario, inícielo: 
   
        # sudo service waagent start
8. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. Abra este toodo "/ boot/grub/menu.lst" en un editor de texto y asegúrese de que kernel predeterminada de hello incluye Hola parámetros siguientes:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    Esto garantizará que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.
9. Confirme que fstab /boot/grub/menu.lst y/etcetera/ambos disco de Hola de referencia mediante su UUID (por uuid) en lugar de Hola de Id. de disco (según el id). 
   
    Obtención del UUID del disco
   
        # ls /dev/disk/by-uuid/
   
    Si /dev/disk/by-id o que se utiliza, actualizar /boot/grub/menu.lst y/etcetera/fstab con el valor de correcto mediante el uuid de Hola
   
    Antes del cambio
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    Después del cambio
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. Modificar udev reglas tooavoid generar reglas estáticas para hello interfaces Ethernet. Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. Se recomienda archivo de hello tooedit "/ etcetera/sysconfig/red/dhcp" y cambiar hello `DHCLIENT_SET_HOSTNAME` parámetro toohello que sigue:
    
     DHCLIENT_SET_HOSTNAME="no"
12. En "/ etcetera/sudoers", convierta en comentario o quite Hola siguiendo las líneas si existen:
    
     Valor predeterminado es targetpw # pedir contraseña Hola Hola del usuario de destino, es decir, todos los ALL=(ALL) todos raíz # advertencia! Use este código junto con 'Defaults targetpw'!
13. Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.  Esto suele ser el predeterminado de Hola.
14. No cree el espacio de intercambio en el disco del sistema operativo de Hola.
    
    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure. Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned. Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en /etc/waagent.conf siguientes correctamente:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Nota: establezca este toowhatever necesita toobe.
15. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
16. Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V. El VHD de Linux está ahora listo toobe había cargado tooAzure.

- - -
## <a name="prepare-opensuse-131"></a>Preparación de openSUSE 13.1+
1. En el panel central de hello del Administrador de Hyper-V, seleccione máquina virtual de Hola.
2. Haga clic en **conectar** tooopen ventana de hello para la máquina virtual de Hola.
3. En el shell de hello, ejecute el comando de hello '`zypper lr`'. Si este comando devuelve resultados similar toohello sigue, después, repositorios de Hola se configura como se esperaba: ajustes no son necesarios (tenga en cuenta que los números de versión pueden variar):
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    Si el comando de hello devuelve "Hay repositorios definidos..." usar, a continuación, hello después tooadd comandos estos repositorios:
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    A continuación, puede comprobar repositorios de Hola se agregaron mediante la ejecución de comando hello '`zypper lr`' nuevo. En caso de que uno de los repositorios de actualización relevante de hello no está habilitado, habilite esta opción con el comando siguiente:
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. Actualizar Hola kernel toohello versión más reciente disponible:
   
        # sudo zypper up kernel-default
   
    Sistema de hello tooupdate con todas las revisiones más recientes de Hola o:
   
        # sudo zypper update
5. Instalar Hola agente Linux de Azure.
   
   # <a name="sudo-zypper-install-walinuxagent"></a>sudo zypper install WALinuxAgent
6. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo, abra "/ boot/grub/menu.lst" en un editor de texto y asegúrese de que kernel predeterminada de hello incluye Hola parámetros siguientes:
   
     console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
   Esto garantizará que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas. Además, quitar Hola siguientes parámetros de línea de arranque de kernel Hola si existen:
   
     libata.atapi_enabled=0 reserve=0x1f0,0x8
7. Se recomienda archivo de hello tooedit "/ etcetera/sysconfig/red/dhcp" y cambiar hello `DHCLIENT_SET_HOSTNAME` parámetro toohello que sigue:
   
     DHCLIENT_SET_HOSTNAME="no"
8. **Importante:** en "/ etcetera/sudoers", convierta en comentario o quitar Hola siguiendo las líneas si existen:
   
     Valor predeterminado es targetpw # pedir contraseña Hola Hola del usuario de destino, es decir, todos los ALL=(ALL) todos raíz # advertencia! Use este código junto con 'Defaults targetpw'!
9. Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.  Esto suele ser el predeterminado de Hola.
10. No cree el espacio de intercambio en el disco del sistema operativo de Hola.
    
    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure. Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned. Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en /etc/waagent.conf siguientes correctamente:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Nota: establezca este toowhatever necesita toobe.
11. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
12. Asegúrese de hello que agente Linux de Azure se ejecuta en el inicio:
    
        # sudo systemctl enable waagent.service
13. Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V. El VHD de Linux está ahora listo toobe había cargado tooAzure.

## <a name="next-steps"></a>Pasos siguientes
Se está ahora listo toouse sus SUSE Linux disco duro virtual toocreate nuevas máquinas virtuales en Azure. Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

