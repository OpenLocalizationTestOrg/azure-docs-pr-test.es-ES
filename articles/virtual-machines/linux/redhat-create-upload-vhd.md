---
title: aaaCreate y cargar un VHD de Red Hat Enterprise Linux para su uso en Azure | Documentos de Microsoft
description: "Obtenga información acerca de toocreate y cargar un Azure disco duro virtual (VHD) que contiene un sistema operativo de Red Hat Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Preparación de una máquina virtual basada en Red Hat para Azure
En este artículo, aprenderá cómo tooprepare una máquina virtual de Red Hat Enterprise Linux (RHEL) para su uso en Azure. versiones de Hola de RHEL que se tratan en este artículo son 6.7 + y 7.1 +. hipervisores Hola de preparación que se tratan en este artículo son la máquina virtual de Hyper-V, en función de kernel (KVM) y VMware. Para más información sobre los requisitos para poder participar en el programa de acceso a la nube de Red Hat, visite el sitio [web de acceso a la nube de Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) y [Ejecución de RHEL en Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Preparación de una máquina virtual basada en Red Hat desde el Administrador de Hyper-V

### <a name="prerequisites"></a>Requisitos previos
En esta sección se da por supuesto que ya ha obtenido un archivo ISO de sitio Web de Red Hat de Hola y Hola instalado RHEL imagen tooa disco duro virtual (VHD). Para obtener más información acerca de cómo toouse Administrador de Hyper-V tooinstall una imagen de sistema operativo, consulte [instalar Hola rol Hyper-V y configurar una máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

**Notas de instalación de RHEL**

* Azure no admite el formato VHDX Hola. Azure solo admite VHD fijo. Puede usar el Administrador de Hyper-V tooconvert Hola disco tooVHD formato o puede usar el cmdlet convert-vhd de Hola. Si usa VirtualBox, seleccione **tamaño fijo** diferencia predeterminado toohello asignadas dinámicamente opción al crear el disco de Hola.
* Azure solo admite máquinas virtuales de la generación 1. Puede convertir una máquina virtual de generación 1 desde el formato de archivo de disco duro virtual de VHDX toohello y de disco de tamaño fijo de tooa de expansión dinámica. No puede cambiar la generación de una máquina virtual. Para más información, consulte [¿Debería crear una máquina virtual de generación 1 o 2 en Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).
* tamaño máximo de Hola que se permite para hello VHD es 1.023 GB.
* Cuando se instala el sistema operativo de Linux de hello, se recomienda que utilice particiones estándar en lugar de administrador de volúmenes lógicos (LVM), que a menudo es valor predeterminado de Hola para muchas instalaciones. Este procedimiento evitará conflictos de nombres LVM con máquinas virtuales clonadas, especialmente si alguna vez necesita una máquina de virtual idéntica de sistema operativo disco tooanother tooattach para solucionar el problema. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se pueden utilizar en discos de datos.
* Se requiere la compatibilidad de kernel para el montaje de sistemas de archivos de formato de disco universal (UDF). En el primer arranque en Azure, Hola soportes en formato UDF que está adjunto toohello invitado pasa Hola aprovisionamiento configuración toohello máquina virtual de Linux. Hola agente Linux de Azure debe ser capaz de toomount Hola UDF archivo sistema tooread su configuración y aprovisionar la máquina virtual de Hola.
* Versiones de kernel de Linux Hola anteriores a 2.6.37 no admiten el acceso a memoria no uniforme (NUMA) en Hyper-V con mayores tamaños de máquina virtual. Este problema afecta principalmente distribuciones anteriores que usan hello en dirección ascendente kernel de Red Hat 2.6.32 y se ha corregido en RHEL 6.6 (kernel-2.6.32-504). Sistemas que ejecutan kernels personalizados que sean más antiguos que 2.6.37 o kernels basado en RHEL que sean más antiguos que 2.6.32-504 deben establecer hello `numa=off` parámetro de arranque en línea de comandos de kernel de hello en grub.conf. Para más información, consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* No configure una partición de intercambio en el disco del sistema operativo de Hola. Hola agente Linux puede ser toocreate configurado un archivo de intercambio en el disco de recursos temporal Hola.  Para obtener más información acerca de esto puede encontrarse en hello siguiendo los pasos.
* El tamaño de todos los VHD debe ser múltiplo de 1 MB.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Preparar una máquina virtual RHEL 6 desde el Administrador de Hyper-V

1. En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.

2. Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.

3. En RHEL 6, NetworkManager puede interferir con el agente de Linux de Azure de Hola. Desinstalar este paquete ejecutando Hola siguiente comando:
   
        # sudo rpm -e --nodeps NetworkManager

4. Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Mover Hola udev reglas tooavoid generar reglas estáticas de interfaz Ethernet de hello (o quitar). Estas reglas pueden causar problemas cuando clone una máquina virtual en Microsoft Azure o Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:

        # sudo chkconfig network on

8. Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras. Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo esta modificación, abra `/boot/grub/menu.lst` en un editor de texto y asegurarse de esa kernel predeterminada de hello incluye Hola parámetros siguientes:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Esto también se asegurará de que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.
    
    Además, se recomienda que quite Hola parámetros siguientes:
    
        rhgb quiet crashkernel=auto
    
    Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie.  Puede dejar hello `crashkernel` opción configurado si lo desea. Tenga en cuenta que este parámetro reduce la cantidad de Hola de memoria disponible en la máquina virtual Hola 128 MB o más. Esta configuración podría resultar problemática en tamaños de máquinas virtuales más pequeños.

    >[!Important]
    RHEL versión 6.5 y versiones anterior también debe establecer hello `numa=off` parámetro de kernel. Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

11. Asegúrese de ese servidor de shell seguro (SSH) Hola se instala y configura toostart al arrancar el sistema, que normalmente es el predeterminado de Hola. Modificar /etc/ssh/sshd_config tooinclude Hola después de línea:

        ClientAliveInterval 180

12. Instale Hola agente Linux de Azure con hello siguiente comando:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    El paquete de instalación hello WALinuxAgent quita Hola NetworkManager y paquetes de gnome NetworkManager si no se han quitado en el paso 3.

13. No cree el espacio de intercambio en el disco de sistema operativo de Hola.

    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure. Tenga en cuenta que Hola local recurso disco es temporal y que puede ser vaciada cuando se canceló el aprovisionamiento de máquina virtual de Hola. Después de instalar Agente Linux de Azure de hello en el paso anterior de hello, modifique Hola parámetros en /etc/waagent.conf siguientes correctamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. Anular el registro de suscripción de hello (si es necesario) mediante la ejecución de hello siguiente comando:

        # sudo subscription-manager unregister

15. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. Haga clic en **Acción**  >  **Apagar** en el Administrador de Hyper-V. El VHD de Linux está ahora listo toobe había cargado tooAzure.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Preparar una máquina virtual RHEL 7 desde el Administrador de Hyper-V

1. En el Administrador de Hyper-V, seleccione la máquina virtual de Hola.

2. Haga clic en **conectar** tooopen una ventana de consola para la máquina virtual de Hola.

3. Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:

        # sudo chkconfig network on

6. Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo esta modificación, abra `/etc/default/grub` en un editor de texto y editar hello `GRUB_CMDLINE_LINUX` parámetro. Por ejemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Esto también se asegurará de que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas. Esta configuración también desactiva Hola nuevas RHEL 7 convenciones de nomenclatura de NIC. Además, se recomienda que quite Hola parámetros siguientes:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie. Puede dejar hello `crashkernel` opción configurado si lo desea. Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.

8. Una vez que haya edición `/etc/default/grub`, ejecute hello después de la configuración del comando toorebuild Hola grub:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. Asegúrese de ese servidor SSH Hola se instala y configura toostart al arrancar el sistema, que normalmente es el predeterminado de Hola. Modificar `/etc/ssh/sshd_config` hello tooinclude después de línea:

        ClientAliveInterval 180

10. paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras. Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Instale Hola agente Linux de Azure con hello siguiente comando:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. No cree el espacio de intercambio en el disco de sistema operativo de Hola.

    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure. Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned. Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Si desea que toounregister Hola suscripción, ejecute hello siguiente comando:

        # sudo subscription-manager unregister

14. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Haga clic en **Acción**  >  **Apagar** en el Administrador de Hyper-V. El VHD de Linux está ahora listo toobe había cargado tooAzure.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>Preparación de una máquina virtual basada en Red Hat desde KVM
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>Preparar una máquina virtual RHEL 6 desde KVM

1. Descargar imagen KVM de Hola de RHEL 6 del sitio Web de Red Hat Hola.

2. Establezca una contraseña raíz.

    Generar una contraseña cifrada y copiar el resultado de hello de comando hello:

        # openssl passwd -1 changeme

    Establezca una contraseña raíz con guestfish:
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Segundo campo de Hola de cambio de usuario de la raíz de Hola de "!!" toohello contraseña cifrada.

3. Crear una máquina virtual en KVM de imagen de qcow2 Hola. Establecer tipo de disco de hello demasiado**qcow2**y establezca el modelo de dispositivo de interfaz de red virtual de hello demasiado**virtio**. A continuación, iniciar la máquina virtual de hello e inicie sesión como raíz.

4. Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Mover Hola udev reglas tooavoid generar reglas estáticas de interfaz Ethernet de hello (o quitar). Estas reglas pueden causar problemas cuando clone una máquina virtual en Azure o Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:

        # chkconfig network on

8. Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo esta configuración, abra `/boot/grub/menu.lst` en un editor de texto y asegurarse de esa kernel predeterminada de hello incluye Hola parámetros siguientes:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Esto también se asegurará de que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas.
    
    Además, se recomienda que quite Hola parámetros siguientes:
    
        rhgb quiet crashkernel=auto
    
    Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie. Puede dejar hello `crashkernel` opción configurado si lo desea. Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.

    >[!Important]
    RHEL versión 6.5 y versiones anterior también debe establecer hello `numa=off` parámetro de kernel. Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

10. Agregar tooinitramfs de módulos de Hyper-V:  

    Editar `/etc/dracut.conf`y agregue Hola siguen contenido:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Recompile initramfs:

        # dracut -f -v

11. Desinstale cloud-init:

        # yum remove cloud-init

12. Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema:

        # chkconfig sshd on

    Modificar /etc/ssh/sshd_config tooinclude Hola siguientes líneas:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras. Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Instale Hola agente Linux de Azure con hello siguiente comando:

        # yum install WALinuxAgent

        # chkconfig waagent on

15. Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure. Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned. Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes **/etc/waagent.conf** correctamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Anular el registro de suscripción de hello (si es necesario) mediante la ejecución de hello siguiente comando:

        # subscription-manager unregister

17. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Apague la máquina virtual de hello en KVM.

19. Convertir el formato de disco duro virtual de hello qcow2 imagen toohello.

    Convertir formato de hello imagen tooraw:

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Asegúrese de que el tamaño Hola de imagen raw de hello está alineado con 1 MB. En caso contrario, se redondea hacia arriba Hola tamaño tooalign con 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertir tooa de disco sin procesar de hello fijo-tamaño de disco duro virtual:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>Preparar una máquina virtual RHEL 7 desde KVM

1. Descargar imagen KVM de Hola de RHEL 7 de sitio Web de Red Hat Hola. Este procedimiento utiliza RHEL 7 como ejemplo de Hola.

2. Establezca una contraseña raíz.

    Generar una contraseña cifrada y copiar el resultado de hello de comando hello:

        # openssl passwd -1 changeme

    Establezca una contraseña raíz con guestfish:

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Segundo campo de Hola de cambio de usuario de la raíz de "!!" toohello contraseña cifrada.

3. Crear una máquina virtual en KVM de imagen de qcow2 Hola. Establecer tipo de disco de hello demasiado**qcow2**y establezca el modelo de dispositivo de interfaz de red virtual de hello demasiado**virtio**. A continuación, iniciar la máquina virtual de hello e inicie sesión como raíz.

4. Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:

        # chkconfig network on

7. Registrar la instalación de Red Hat suscripción tooenable de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo esta configuración, abra `/etc/default/grub` en un editor de texto y editar hello `GRUB_CMDLINE_LINUX` parámetro. Por ejemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Este comando también garantiza que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas. comando Hello también desactiva Hola nuevas RHEL 7 convenciones de nomenclatura de NIC. Además, se recomienda que quite Hola parámetros siguientes:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie. Puede dejar hello `crashkernel` opción configurado si lo desea. Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.

9. Una vez que haya edición `/etc/default/grub`, ejecute hello después de la configuración del comando toorebuild Hola grub:

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Agregue módulos de Hyper-V a initramfs.

    Edite `/etc/dracut.conf` y agregue contenido:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Recompile initramfs:

        # dracut -f -v

11. Desinstale cloud-init:

        # yum remove cloud-init

12. Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema:

        # systemctl enable sshd

    Modificar /etc/ssh/sshd_config tooinclude Hola siguientes líneas:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras. Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Instale Hola agente Linux de Azure con hello siguiente comando:

        # yum install WALinuxAgent

    Habilitar hello waagent servicio:

        # systemctl enable waagent.service

15. No cree el espacio de intercambio en el disco de sistema operativo de Hola.

    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure. Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned. Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Anular el registro de suscripción de hello (si es necesario) mediante la ejecución de hello siguiente comando:

        # subscription-manager unregister

17. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Apague la máquina virtual de hello en KVM.

19. Convertir el formato de disco duro virtual de hello qcow2 imagen toohello.

    Convertir formato de hello imagen tooraw:

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Asegúrese de que el tamaño Hola de imagen raw de hello está alineado con 1 MB. En caso contrario, se redondea hacia arriba Hola tamaño tooalign con 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertir tooa de disco sin procesar de hello fijo-tamaño de disco duro virtual:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>Preparación de una máquina virtual basada en Red Hat para VMware
### <a name="prerequisites"></a>Requisitos previos
En esta sección se supone que ya instaló una máquina virtual RHEL en VMware. Para obtener más información acerca de cómo tooinstall un sistema operativo en VMware, consulte [Guía de instalación de sistema operativo invitado de VMware](http://partnerweb.vmware.com/GOSIG/home.html).

* Cuando se instala el sistema operativo de Linux de hello, recomendamos que utilice particiones estándar en lugar de LVM, que suele ser predeterminado de Hola para muchas instalaciones. Esto evitará LVM nombre entra en conflicto con la máquina virtual clonada, especialmente si un disco del sistema operativo alguna vez necesita toobe adjunta tooanother virtual machine para solucionar el problema. Para los discos de datos se puede utilizar LVM o RAID si así se prefiere.
* No configure una partición de intercambio en el disco del sistema operativo de Hola. Puede configurar Hola Linux agente toocreate un archivo de intercambio en el disco de recursos temporal Hola. Puede buscar más información al respecto en los pasos de Hola que siguen.
* Cuando se crea el disco duro virtual de hello, seleccione **disco virtual del almacén como un único archivo**.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>Preparar una máquina virtual RHEL 6 desde VMware
1. En RHEL 6, NetworkManager puede interferir con el agente de Linux de Azure de Hola. Desinstalar este paquete ejecutando Hola siguiente comando:
   
        # sudo rpm -e --nodeps NetworkManager

2. Cree un archivo denominado **red** en hello/etc/sysconfig/directorio que contiene Hola siguiente texto:

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Mover Hola udev reglas tooavoid generar reglas estáticas de interfaz Ethernet de hello (o quitar). Estas reglas pueden causar problemas cuando clone una máquina virtual en Azure o Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:

        # sudo chkconfig network on

6. Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras. Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo, abra `/etc/default/grub` en un editor de texto y editar hello `GRUB_CMDLINE_LINUX` parámetro. Por ejemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   Esto también se asegurará de que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas. Además, se recomienda que quite Hola parámetros siguientes:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie. Puede dejar hello `crashkernel` opción configurado si lo desea. Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.

9. Agregar tooinitramfs de módulos de Hyper-V:

    Editar `/etc/dracut.conf`y agregue Hola siguen contenido:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Recompile initramfs:

        # dracut -f -v

10. Asegúrese de ese servidor SSH Hola se instala y configura toostart al arrancar el sistema, que normalmente es el predeterminado de Hola. Modificar `/etc/ssh/sshd_config` hello tooinclude después de línea:

    ClientAliveInterval 180

11. Instale Hola agente Linux de Azure con hello siguiente comando:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. No cree el espacio de intercambio en el disco de sistema operativo de Hola.

    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure. Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned. Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Anular el registro de suscripción de hello (si es necesario) mediante la ejecución de hello siguiente comando:

        # sudo subscription-manager unregister

14. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Apagar la máquina virtual de Hola y convertir el archivo .vhd de hello VMDK archivo tooa.

    Convertir formato de hello imagen tooraw:

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Asegúrese de que el tamaño Hola de imagen raw de hello está alineado con 1 MB. En caso contrario, se redondea hacia arriba Hola tamaño tooalign con 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertir tooa de disco sin procesar de hello fijo-tamaño de disco duro virtual:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>Preparar una máquina virtual RHEL 7 desde VMware
1. Crear o editar hello `/etc/sysconfig/network` de archivos y agregue Hola siguiente texto:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. Crear o editar hello `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos y agregue Hola siguiente texto:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. Asegúrese de que el servicio de red de Hola se iniciará al arrancar el sistema ejecutando el siguiente comando de hello:

        # sudo chkconfig network on

4. Registrar la instalación de Red Hat suscripción tooenable Hola de paquetes del repositorio RHEL Hola ejecutando Hola siguiente comando:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Modificar línea de arranque de kernel de hello en los parámetros de núcleo adicionales grub tooinclude de configuración de Azure. toodo esta modificación, abra `/etc/default/grub` en un editor de texto y editar hello `GRUB_CMDLINE_LINUX` parámetro. Por ejemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Esta configuración también garantiza que todos los mensajes de la consola se envían toohello primer puerto serie, que puede ayudar a Azure compatibilidad con la depuración de problemas. También desactiva Hola nuevas RHEL 7 convenciones de nomenclatura para la NIC. Además, se recomienda que quite Hola parámetros siguientes:
   
        rhgb quiet crashkernel=auto
   
    Arranque gráfica y silencioso no son útiles en un entorno de nube donde se desea que todos los toobe de registros de hello envía toohello de puerto serie. Puede dejar hello `crashkernel` opción configurado si lo desea. Tenga en cuenta que este parámetro reduce Hola de memoria disponible en la máquina virtual Hola 128 MB o más, lo que podría resultar problemática en tamaños de máquina virtual más pequeños.

6. Una vez que haya edición `/etc/default/grub`, ejecute hello después de la configuración del comando toorebuild Hola grub:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Agregar tooinitramfs de módulos de Hyper-V.

    Edite `/etc/dracut.conf`y agregue contenido:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Recompile initramfs:

        # dracut -f -v

8. Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema. Este valor suele ser predeterminada Hola. Modificar `/etc/ssh/sshd_config` hello tooinclude después de línea:

        ClientAliveInterval 180

9. paquete de Hello WALinuxAgent, `WALinuxAgent-<version>`, se ha insertado el repositorio de toohello Red Hat extras. Habilitar repositorio de extras Hola ejecutando Hola siguiente comando:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Instale Hola agente Linux de Azure con hello siguiente comando:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. No cree el espacio de intercambio en el disco de sistema operativo de Hola.

    Hola agente Linux de Azure puede configurar automáticamente el espacio de intercambio mediante el uso de disco del recurso local Hola que está adjunto toohello virtual machine después de aprovisionar la máquina virtual de hello en Azure. Tenga en cuenta que hello disco del recurso local es un disco temporal, y puede ser vaciada cuando máquina virtual de hello es deprovisioned. Después de instalar Hola agente Linux de Azure en el paso anterior de hello, modificar Hola parámetros en siguientes `/etc/waagent.conf` correctamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Si desea que toounregister Hola suscripción, ejecute hello siguiente comando:

        # sudo subscription-manager unregister

13. Ejecute hello después de la máquina virtual de comandos toodeprovision hello y prepararlo para el aprovisionamiento en Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Apagar la máquina virtual de Hola y convertir el formato de disco duro virtual de hello VMDK archivo toohello.

    Convertir formato de hello imagen tooraw:

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Asegúrese de que el tamaño Hola de imagen raw de hello está alineado con 1 MB. En caso contrario, se redondea hacia arriba Hola tamaño tooalign con 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertir tooa de disco sin procesar de hello fijo-tamaño de disco duro virtual:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>Preparación de una máquina virtual basada en Red Hat desde una imagen ISO con un archivo kickstart automáticamente
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>Preparar una máquina virtual RHEL 7 desde un archivo kickstart

1.  Crear un archivo que incluye Hola siguen contenido y guarde el archivo hello. Para obtener más información acerca de la instalación de comenzar, vea hello [ofrecen Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. Coloque el archivo de Hola que puedan acceder de sistema de la instalación de Hola.

3. En el Administrador de Hyper-V, cree una nueva máquina virtual. En hello **conectar disco duro Virtual** página, seleccione **adjuntar un disco duro virtual más tarde**y Hola completo Asistente para nueva máquina Virtual.

4. Abra Configuración de máquina virtual de hello:

    a.  Adjuntar una nueva máquina virtual de toohello de disco duro virtual. Asegúrese de que tooselect **formato VHD** y **tamaño fijo**.

    b.  Adjuntar instalación Hola unidad de DVD de ISO toohello.

    c.  Establecer Hola BIOS tooboot desde el CD.

5. Inicie la máquina virtual de Hola. Cuando aparezca la Guía de instalación de hello, presione **ficha** opciones de arranque de tooconfigure Hola.

6. ENTRAR `inst.ks=<hello location of hello kickstart file>` final Hola de opciones de arranque de hello y presione **ENTRAR**.

7. Espere Hola instalación toofinish. Cuando haya finalizado, máquina virtual de Hola se apagará automáticamente. El VHD de Linux está ahora listo toobe había cargado tooAzure.

## <a name="known-issues"></a>Problemas conocidos
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>no se pudieron incluir controladores de Hyper-V de Hello en disco RAM inicial de hello cuando se usa un hipervisor de Hyper-V

En algunos casos, instaladores de Linux no podrían incluir controladores de Hola para Hyper-V en hello inicial disco RAM (initrd o initramfs) a menos que detecte de Linux que se está ejecutando en un entorno de Hyper-V.

Cuando se usa un tooprepare del sistema (es decir, Virtualbox, Xen, etc.) de virtualización distinto la imagen de Linux, deberá toorebuild initrd tooensure que al menos Hola hv_vmbus y los módulos de kernel hv_storvsc están disponibles en el disco RAM inicial de Hola. Esto es un problema conocido al menos en sistemas que se basan en la distribución de Red Hat de nivel superior de Hola.

tooresolve este problema, agregue tooinitramfs de módulos de Hyper-V y vuelva a generarlo:

Editar `/etc/dracut.conf`y agregue Hola siguen contenido:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

Recompile initramfs:

        # dracut -f -v

Para obtener más información, vea la información de hello sobre [volver a generar initramfs](https://access.redhat.com/solutions/1958).

## <a name="next-steps"></a>Pasos siguientes
Se está ahora listo toouse sus Red Hat Enterprise Linux disco duro virtual toocreate nuevas máquinas virtuales en Azure. Si se trata de hello primera vez que se está cargando tooAzure de archivo .vhd de hello, consulte los pasos 2 y 3 en [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Para obtener más detalles sobre los hipervisores de Hola que están certificación toorun Red Hat Enterprise Linux, consulte [sitio Web de Red Hat hello](https://access.redhat.com/certified-hypervisors).
