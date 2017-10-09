---
title: aaaCreate y cargar un disco duro virtual de Oracle Linux | Documentos de Microsoft
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contenga un sistema operativo de Linux de Oracle."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Preparación de una máquina virtual Oracle Linux para Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por supuesto que ya ha instalado un disco de duro virtual y tooa con sistema operativo Linux de Oracle. Varias herramientas existen archivos .vhd de toocreate, por ejemplo, una solución de virtualización como Hyper-V. Para obtener instrucciones, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="oracle-linux-installation-notes"></a>Notas sobre la instalación de Oracle Linux
* Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.
* El kernel compatible Red Hat de Oracle y su UEK3 (Unbreakable Enterprise Kernel) se admiten en Hyper-V y Azure. Para obtener mejores resultados, ten kernel más reciente de tooupdate seguro toohello al preparar el disco duro virtual de Oracle Linux.
* UEK2 de Oracle no se admite en Hyper-V y Azure incluya controladores Hola necesario.
* no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.  Puede convertir Hola disco tooVHD formato con el Administrador de Hyper-V u Hola cmdlet convert-vhd.
* Al instalar el sistema de Linux Hola se recomienda que utilice particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones). Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita toobe adjuntada tooanother VM para solucionar problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos si así se prefiere.
* NUMA no se admite para los tamaños más grandes de VM debido a errores de tooa en versiones de kernel de Linux anteriores a 2.6.37. Este problema principalmente los impactos distribuciones utilizando Hola rojo ascendente kernel Hat 2.6.32. Instalación manual de agente de Linux de Azure de hello (waagent) deshabilitará automáticamente NUMA en configuración de GRUB hello para el kernel de Linux Hola. Para obtener más información acerca de este puede encontrarse en pasos Hola.
* No configure una partición de intercambio en el disco del sistema operativo de Hola. agente de Linux de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.  Para obtener más información acerca de este puede encontrarse en pasos Hola.
* Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.
* Asegúrese de que ese hello `Addons` repositorio está habilitado. Editar archivo hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) o `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) y cambie la línea hello `enabled=0` demasiado`enabled=1` en **[ol6_addons]** o **[ol7_addons]** en este archivo.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4+
Debe completar pasos de configuración específica de sistema operativo de Hola para hello toorun de máquina virtual en Azure.

1. En el panel central de hello del Administrador de Hyper-V, seleccione máquina virtual de Hola.
2. Haga clic en **conectar** tooopen ventana de hello para la máquina virtual de Hola.
3. Desinstala NetworkManager con hello siguiente comando:
   
        # sudo rpm -e --nodeps NetworkManager
   
    **Nota:** si Hola paquete ya no está instalado, este comando generará un error con un mensaje de error. Se espera que esto sea así.
4. Cree un archivo denominado **red** en hello `/etc/sysconfig/` directorio que contiene Hola siguiente texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. Cree un archivo denominado **ifcfg eth0** en hello `/etc/sysconfig/network-scripts/` directorio que contiene Hola siguiente texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. Modificar udev reglas tooavoid generar reglas estáticas para hello interfaces Ethernet. Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. Asegúrese de que se iniciará el servicio de red de hello al arrancar el sistema ejecutando el siguiente comando de hello:
   
        # chkconfig network on
8. Instalar python pyasn1 ejecutando Hola siguiente comando:
   
        # sudo yum install python-pyasn1
9. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. Abra este toodo "/ boot/grub/menu.lst" en un editor de texto y asegúrese de que kernel predeterminada de hello incluye Hola parámetros siguientes:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas. Esto deshabilitará NUMA debido a errores de tooa en kernel compatible de Red Hat de Oracle.
   
   Además toohello anterior, se recomienda demasiado*quitar* Hola siguientes parámetros:
   
        rhgb quiet crashkernel=auto
   
   Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.
   
   Hola `crashkernel` opción puede ser izquierda configurado si lo desea, pero tenga en cuenta que este parámetro reducirá la cantidad de Hola de memoria disponible en hello máquina virtual por medio de 128 MB o más, lo que puede ser problemático en tamaños VM de hello más pequeños.
10. Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.  Esto suele ser el predeterminado de Hola.
11. Instalar Agente Linux de Azure Hola ejecutando el siguiente comando de Hola. versión más reciente de Hello es 2.0.15.
    
        # sudo yum install WALinuxAgent
    
    Tenga en cuenta que el paquete de instalación hello WALinuxAgent quitará Hola NetworkManager y paquetes de gnome NetworkManager si no se quitan ya tal como se describe en el paso 2.
12. No cree el espacio de intercambio en el disco del sistema operativo de Hola.
    
    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure. Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned. Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en /etc/waagent.conf siguientes correctamente:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V. El VHD de Linux está ahora listo toobe había cargado tooAzure.

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0+
**Cambios en Oracle Linux 7**

Preparar una máquina virtual de Oracle Linux 7 de Azure es muy similar tooOracle Linux 6, sin embargo, hay algunas diferencias importantes que tener en cuenta:

* Kernel compatible de Red Hat de Hola y UEK3 de Oracle se admiten en Azure.  se recomienda el kernel de UEK3 Hola.
* Hola NetworkManager empaquetar ya no está en conflicto con el agente de Linux de Azure de Hola. Este paquete está instalado de manera predeterminada y recomendamos que no se quite.
* GRUB2 ahora se usa como Hola del cargador de arranque de forma predeterminada, por lo que el procedimiento de Hola para editar los parámetros de kernel ha cambiado (vea a continuación).
* XFS es ahora el sistema de archivos predeterminado de Hola. sistema de archivos de Hello ext4 aún puede usarse si lo desea.

**Pasos de configuración**

1. En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.
2. Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.
3. Cree un archivo denominado **red** en hello `/etc/sysconfig/` directorio que contiene Hola siguiente texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. Cree un archivo denominado **ifcfg eth0** en hello `/etc/sysconfig/network-scripts/` directorio que contiene Hola siguiente texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Modificar udev reglas tooavoid generar reglas estáticas para hello interfaces Ethernet. Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. Asegúrese de que se iniciará el servicio de red de hello al arrancar el sistema ejecutando el siguiente comando de hello:
   
        # sudo chkconfig network on
7. Instalar paquete de python pyasn1 Hola ejecutando Hola siguiente comando:
   
        # sudo yum install python-pyasn1
8. Siguiente ejecución Hola comando tooclear Hola actual yum metadatos e instala las actualizaciones:
   
        # sudo yum clean all
        # sudo yum -y update
9. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo este abra "/ etcetera/predeterminado/grub" en un Hola de editor y edición de texto `GRUB_CMDLINE_LINUX` parámetro, por ejemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas. También desactiva Hola nuevas OEL 7 convenciones de nomenclatura para la NIC. Además toohello anterior, se recomienda demasiado*quitar* Hola siguientes parámetros:
   
       rhgb quiet crashkernel=auto
   
   Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.
   
   Hola `crashkernel` opción puede ser izquierda configurado si lo desea, pero tenga en cuenta que este parámetro reducirá la cantidad de Hola de memoria disponible en hello máquina virtual por medio de 128 MB o más, lo que puede ser problemático en tamaños VM de hello más pequeños.
10. Cuando acabes edición "/ etcetera/predeterminado/grub" por encima, ejecute hello siguiente comando toorebuild Hola grub configuración:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.  Esto suele ser el predeterminado de Hola.
12. Instale Hola agente Linux de Azure con hello siguiente comando:
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. No cree el espacio de intercambio en el disco del sistema operativo de Hola.
    
    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure. Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned. Después de instalar Hola agente Linux de Azure (vea el paso anterior de hello), modificar Hola parámetros en /etc/waagent.conf siguientes correctamente:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V. El VHD de Linux está ahora listo toobe había cargado tooAzure.

## <a name="next-steps"></a>Pasos siguientes
Se está ahora listo toouse sus Oracle Linux .vhd toocreate nuevas máquinas virtuales en Azure. Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

