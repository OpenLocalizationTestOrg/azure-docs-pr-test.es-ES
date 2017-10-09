---
title: aaaCreate y cargar un VHD de Linux-based CentOS en Azure
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contiene un sistema operativo basado en CentOS Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Preparación de una máquina virtual basada en CentOS para Azure
* [Preparación de una máquina virtual CentOS 6.x para Azure](#centos-6x)
* [Preparación de una máquina virtual CentOS 7.0+ para Azure](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por supuesto que ya ha instalado una distribución de CentOS (o similar derivado) disco de duro virtual de tooa de sistema operativo de Linux. Varias herramientas existen archivos .vhd de toocreate, por ejemplo, una solución de virtualización como Hyper-V. Para obtener instrucciones, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

**Notas de instalación de CentOS**

* Consulte también [Notas generales sobre la instalación de Linux](create-upload-generic.md#general-linux-installation-notes) para obtener más consejos sobre la preparación de Linux para Azure.
* no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.  Puede convertir Hola disco tooVHD formato con el Administrador de Hyper-V u Hola cmdlet convert-vhd. Si usas VirtualBox Esto significa seleccionar **tamaño fijo** como opone predeterminado toohello asignada de forma dinámica al crear el disco de Hola.
* Al instalar el sistema de Linux de hello es *recomienda* utilizar particiones estándar en lugar de LVM (a menudo predeterminado de Hola para muchas instalaciones). Esto evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si un disco del sistema operativo alguna vez necesita tooanother toobe adjunta VM idéntico para solucionar el problema. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos.
* Se requiere la compatibilidad de kernel para el montaje de sistemas de archivos UDF. En el primer arranque en hello Azure configuración del aprovisionamiento pasa toohello VM de Linux a través de medios con formato UDF que está invitado toohello adjunto. agente de Linux de Azure de Hello debe ser capaz de toomount Hola UDF archivo sistema tooread su configuración y aprovisionar Hola VM.
* Las versiones de kernel de Linux inferiores a la versión 2.6.37 no admiten NUMA en Hyper-V con tamaños de VM más grandes. Este problema afecta principalmente distribuciones anteriores mediante hello en dirección ascendente kernel de Red Hat 2.6.32 y se ha corregido en RHEL 6.6 (kernel-2.6.32-504). Sistemas que ejecutan kernels personalizados anteriores a 2.6.37 o basado en RHEL kernels anteriores que se debe establecer 2.6.32-504 Hola parámetro de arranque `numa=off` en kernel Hola de línea de comandos en grub.conf. Para obtener más información, consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* No configure una partición de intercambio en el disco del sistema operativo de Hola. agente de Linux de Hello puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.  Para obtener más información acerca de este puede encontrarse en pasos Hola.
* Todos de hello discos duros virtuales deben tener que sean múltiplos de 1 MB.

## <a name="centos-6x"></a>CentOS 6.x

1. En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.

2. Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.

3. De CentOS 6, NetworkManager puede interferir con el agente de Linux de Azure de Hola. Desinstalar este paquete ejecutando Hola siguiente comando:
   
        # sudo rpm -e --nodeps NetworkManager

4. Crear o editar el archivo hello `/etc/sysconfig/network` y agregue Hola siguiente texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Crear o editar el archivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue Hola siguiente texto:
   
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
   
        # sudo chkconfig network on

8. Si desea que los reflejos de OpenLogic de hello toouse que se hospedan en hello centros de datos de Azure, a continuación, reemplace hello `/etc/yum.repos.d/CentOS-Base.repo` archivo con hello después repositorios.  También agregará hello **[openlogic]** repositorio que incluye paquetes adicionales como el agente de Linux de Azure de hello:

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    Hello resto de esta guía se presupone que usa al menos Hola `[openlogic]` repositorio, que será usado tooinstall Hola Linux de Azure agente siguiente.


9. Agregue Hola después too/etc/yum.conf línea:
    
        http_caching=packages

10. Ejecute hello después comando tooclear Hola yum actualización y los metadatos hello sistema actual con los paquetes de saludo más recientes:
    
        # yum clean all

    A menos que se va a crear una imagen de una versión anterior de CentOS, se recomienda tooupdate que Hola a todos los paquetes toohello más reciente:

        # sudo yum -y update

    Después de ejecutar este comando es posible que sea preciso reiniciar el equipo.

11. (Opcional) Instalar a controladores de Hola para hello servicios de integración de Linux (LIS).
   
    >[!IMPORTANT]
    paso de Hello es **necesario** para CentOS 6.3 y opcionales para versiones posteriores y anteriores.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    Como alternativa, puede seguir las instrucciones de instalación manual de hello en hello [página de descarga de LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall Hola RPM en la máquina virtual.
 
12. Instalar Agente Linux de Azure de Hola y dependencias:
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    paquete de Hello WALinuxAgent quitará Hola NetworkManager y paquetes de gnome NetworkManager si no se quitan ya tal como se describe en el paso 3.


13. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo, abra `/boot/grub/menu.lst` en un editor de texto y asegúrese de que kernel predeterminada de hello incluye Hola parámetros siguientes:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.
    
    Además toohello anterior, se recomienda demasiado*quitar* Hola siguientes parámetros:
    
        rhgb quiet crashkernel=auto
    
    Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.  Hola `crashkernel` opción puede ser izquierda configurado si lo desea, pero tenga en cuenta que este parámetro reducirá la cantidad de Hola de memoria disponible en hello máquina virtual por medio de 128 MB o más, lo que puede ser problemático en tamaños VM de hello más pequeños.

    >[!Important]
    CentOS 6.5 y versiones anteriores también deben establecer el parámetro de kernel de hello `numa=off`. Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

14. Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.  Esto suele ser el predeterminado de Hola.

15. No cree el espacio de intercambio en el disco del sistema operativo de Hola.
    
    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure. Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned. Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. Haga clic en **Acción -> Apagar** en el Administrador de Hyper-V. El VHD de Linux está ahora listo toobe había cargado tooAzure.


- - -
## <a name="centos-70"></a>CentOS 7.0+
**Cambios en CentOS 7 (y derivados similares)**

Preparar una máquina virtual de CentOS 7 de Azure es muy similar tooCentOS 6, sin embargo, hay algunas diferencias importantes que tener en cuenta:

* Hola NetworkManager empaquetar ya no está en conflicto con el agente de Linux de Azure de Hola. Este paquete está instalado de manera predeterminada y recomendamos que no se quite.
* GRUB2 ahora se usa como Hola del cargador de arranque de forma predeterminada, por lo que el procedimiento de Hola para editar los parámetros de kernel ha cambiado (vea a continuación).
* XFS es ahora el sistema de archivos predeterminado de Hola. sistema de archivos de Hello ext4 aún puede usarse si lo desea.

**Pasos de configuración**

1. En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.

2. Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.

3. Crear o editar el archivo hello `/etc/sysconfig/network` y agregue Hola siguiente texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Crear o editar el archivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue Hola siguiente texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Modificar udev reglas tooavoid generar reglas estáticas para hello interfaces Ethernet. Estas reglas pueden causar problemas al clonar una máquina virtual en Microsoft Azure o Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. Si desea que los reflejos de OpenLogic de hello toouse que se hospedan en hello centros de datos de Azure, a continuación, reemplace hello `/etc/yum.repos.d/CentOS-Base.repo` archivo con hello después repositorios.  También agregará hello **[openlogic]** repositorio que incluye paquetes de agente de Linux de Azure de hello:
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    Hello resto de esta guía se presupone que usa al menos Hola `[openlogic]` repositorio, que será usado tooinstall Hola Linux de Azure agente siguiente.

7. Siguiente ejecución Hola comando tooclear Hola actual yum metadatos e instala las actualizaciones:
   
        # sudo yum clean all

    A menos que se va a crear una imagen de una versión anterior de CentOS, se recomienda tooupdate que Hola a todos los paquetes toohello más reciente:

        # sudo yum -y update

    Después de ejecutar este comando es posible que sea preciso reiniciar el equipo.

8. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo, abra `/etc/default/grub` en un Hola de editor y edición de texto `GRUB_CMDLINE_LINUX` parámetro, por ejemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Esto garantizará también todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas. También desactiva Hola nuevas CentOS 7 convenciones de nomenclatura para la NIC. Además toohello anterior, se recomienda demasiado*quitar* Hola siguientes parámetros:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie. Hola `crashkernel` opción puede ser izquierda configurado si lo desea, pero tenga en cuenta que este parámetro reducirá la cantidad de Hola de memoria disponible en hello máquina virtual por medio de 128 MB o más, lo que puede ser problemático en tamaños VM de hello más pequeños.

9. Cuando acabes edición `/etc/default/grub` por encima, ejecute hello siguiente comando toorebuild Hola grub configuración:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Si la creación de imagen de Hola de **VMWare, VirtualBox o KVM:** hello initramfs incluye controladores de hello Hyper-V Asegúrese de que:
   
   Edite `/etc/dracut.conf`y agregue contenido:
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Vuelva a generar Hola initramfs:
   
        # sudo dracut –f -v

11. Instalar Agente Linux de Azure de Hola y dependencias:

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. No cree el espacio de intercambio en el disco del sistema operativo de Hola.
   
   Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio con el disco del recurso local Hola que está adjunto toohello VM después de aprovisionar en Azure. Tenga en cuenta ese disco del recurso local hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned. Después de instalar Hola agente Linux de Azure (vea el paso anterior), modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:
   
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

## <a name="next-steps"></a>Pasos siguientes
Se está ahora listo toouse sus CentOS Linux disco duro virtual toocreate nuevas máquinas virtuales en Azure. Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

