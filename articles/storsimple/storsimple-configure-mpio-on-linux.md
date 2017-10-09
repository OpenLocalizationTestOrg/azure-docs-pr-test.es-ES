---
title: aaaConfigure MPIO en el host de StorSimple Linux | Documentos de Microsoft
description: Configurar MPIO en el host de Linux tooa StorSimple conectado ejecutando 6.6 de CentOS
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>Configuración de MPIO en un host de StorSimple que ejecuta CentOS
Este artículo explica Hola pasos necesarios tooconfigure E/S de múltiples rutas (MPIO) en el servidor de host de Centos 6.6. servidor de host de Hello es tooyour conectado de dispositivo de StorSimple de Microsoft Azure para lograr alta disponibilidad a través de los iniciadores iSCSI. Se describe en la detección automática de detalle Hola de dispositivos de múltiples rutas de acceso y el programa de instalación específicos de hello sólo para volúmenes de StorSimple.

Este procedimiento es aplicable tooall modelos de Hola de dispositivos de la serie StorSimple 8000.

> [!NOTE]
> No se puede usar este procedimiento para un dispositivo virtual de StorSimple. Para obtener más información, vea cómo tooconfigure hospedar servidores del dispositivo virtual.
> 
> 

## <a name="about-multipathing"></a>Acerca de múltiples rutas
característica de múltiples rutas de Hello permite tooconfigure varias rutas de acceso de E/S entre un servidor host y un dispositivo de almacenamiento. Estas rutas de acceso de E/S son conexiones físicas de SAN que pueden incluir cables independientes, conmutadores, interfaces de red y controladores. Múltiples rutas agrega las rutas de E/S de hello, tooconfigure un nuevo dispositivo que está asociado con todas las rutas de acceso de hello agregado.

propósito de Hola de múltiples rutas tiene dos aspectos:

* **Alta disponibilidad**: proporciona una ruta de acceso alternativa si se produce un error en cualquier elemento de ruta de acceso de hello E/S (por ejemplo, un cable, conmutador, interfaz de red o controlador).
* **Equilibrio de carga**: dependiendo de su dispositivo de almacenamiento de configuración de hello, puede mejorar el rendimiento de hello detectando cargas en las rutas de acceso de E/S de Hola y reequilibrio dinámicamente las cargas.

### <a name="about-multipathing-components"></a>Acerca de los componentes de múltiples rutas
La característica de múltiples rutas en Linux consta de componentes del kernel y de componentes del espacio de usuario, como se indica más abajo.

* **Kernel**: componente principal de hello es hello *dispositivo asignador* que redistribuye i/OS y admite la conmutación por error para las rutas de acceso y grupos de la ruta de acceso.

* **Espacio de usuario**: se trata de *herramientas de múltiples rutas* que administrar detectar dispositivos indicando a módulo de múltiples rutas de acceso de dispositivo asignador de hello qué toodo. herramientas de Hola se componen de:
   
   * **Multipath**: muestra y configura los dispositivos con múltiples rutas.
   * **Multipathd**: daemon que se ejecuta de rutas de acceso de Hola de múltiples rutas y monitores.
   * **Nombre de Devmap**: proporciona un significativo tooudev de nombre de dispositivo para devmaps.
   * **Kpartx**: asigna devmaps lineal toodevice particiones toomake múltiples rutas mapas cargas.
   * **Multipath.conf**: archivo de configuración del demonio de múltiples rutas de acceso que es usado toooverwrite Hola configuración integrada tabla.

### <a name="about-hello-multipathconf-configuration-file"></a>Sobre el archivo de configuración de hello multipath.conf
archivo de configuración de Hello `/etc/multipath.conf` realiza muchos Hola múltiples rutas características configurables por el usuario. Hola `multipath` daemon de kernel hello y comando `multipathd` usar la información de este archivo. archivo Hello se consulta solo durante la configuración de Hola de dispositivos de múltiples rutas de Hola. Asegúrese de que todos los cambios se realizan antes de ejecutar hello `multipath` comando. Si modifica el archivo hello posteriormente, se necesita toostop e iniciar multipathd nuevo para hello cambios tootake efecto.

Hola multipath.conf tiene cinco secciones:

- **Valores predeterminados de nivel de sistema***(defaults)*: puede invalidar los valores predeterminados de nivel de sistema.
- **En la lista negra dispositivos** *(lista negra)*: puede especificar la lista de Hola de dispositivos que no deben controlarse mediante el asignador de dispositivo.
- **Generar una lista negra excepciones** *(blacklist_exceptions)*: puede identificar toobe de dispositivos específicos que se tratan como dispositivos de múltiples rutas, incluso si aparece en la lista negra de Hola.
- **Configuración específica del controlador de almacenamiento** *(dispositivos)*: puede especificar opciones de configuración que serán aplicado toodevices que tienen información de proveedor y producto.
- **Configuración específica del dispositivo** *(multipaths)*: puede usar esta configuración sección toofine ajustar Hola para cada LUN.

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>Configurar múltiples rutas en el host conectado tooLinux de StorSimple
Un host de Linux de StorSimple dispositivo conectado tooa puede configurarse para alta disponibilidad y equilibrio de carga. Por ejemplo, si el host de Linux de hello tiene dos interfaces conectadas toohello hello y SAN dispositivo tiene dos interfaces conectadas toohello SAN que estas interfaces se encuentran en Hola misma subred, a continuación, habrá 4 rutas disponibles. Sin embargo, si cada interfaz de datos en la interfaz de dispositivo y el host de Hola se encuentran en una subred IP diferente (y no enrutables), a continuación, las rutas de acceso de solo 2 estará disponibles. Puede configurar múltiples rutas tooautomatically detectar todas las rutas de acceso disponibles de hello, elegir un algoritmo de equilibrio de carga para esas rutas, aplicar opciones de configuración específicas para volúmenes de StorSimple solo y, a continuación, habilitar y comprobar múltiples rutas.

Hello siguiente procedimiento describe cómo tooconfigure de múltiples rutas cuando un dispositivo de StorSimple con dos interfaces de red está conectado tooa host con dos interfaces de red.

## <a name="prerequisites"></a>Requisitos previos
Esta sección describe los requisitos previos de configuración de hello para el servidor de CentOS y el dispositivo de StorSimple.

### <a name="on-centos-host"></a>En el host CentOS
1. Asegúrese de que el host CentOS tiene dos interfaces de red habilitadas. Escriba:
   
    `ifconfig`
   
    Hello en el ejemplo siguiente se muestra el resultado de hello cuando dos interfaces de red (`eth0` y `eth1`) están presentes en el host de Hola.
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. Instale *iSCSI-initiator-utils* en el servidor CentOS. Realizar Hola siguiendo los pasos tooinstall *utilidades de iniciador iSCSI*.
   
   1. Inicie sesión como `root` en el host CentOS.
   2. Instalar hello *utilidades de iniciador iSCSI*. Escriba:
      
       `yum install iscsi-initiator-utils`
   3. Después de hello *utilidades de iniciador iSCSI* está correctamente instalado, inicie el servicio iSCSI Hola. Escriba:
      
       `service iscsid start`
      
       En ocasiones, `iscsid` realmente no se puede iniciar y Hola `--force` opción puede ser necesaria
   4. tooensure que el iniciador iSCSI está habilitado durante el tiempo de arranque, use hello `chkconfig` servicio de hello tooenable de comandos.
      
       `chkconfig iscsi on`
   5. tooverify que estaba correctamente el programa de instalación, ejecute el comando de hello:
      
       `chkconfig --list | grep iscsi`
      
       A continuación se muestra una salida de ejemplo.
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       En hello ejemplo anterior, puede ver que el entorno de iSCSI se ejecutará en tiempo de arranque en ejecución niveles 2, 3, 4 y 5.
3. Instale *device-mapper-multipath*. Escriba:
   
    `yum install device-mapper-multipath`
   
    se iniciará la instalación de Hola. Tipo de **Y** toocontinue cuando se le pida confirmación.

### <a name="on-storsimple-device"></a>En el dispositivo de StorSimple
El dispositivo de StorSimple debe disponer de:

* Un mínimo de dos interfaces habilitadas para iSCSI. tooverify que dos interfaces están habilitadas para iSCSI en el dispositivo StorSimple, lleve a cabo Hola pasos de hello portal de Azure clásico para el dispositivo StorSimple:
  
  1. Inicie sesión en el portal clásico de hello para el dispositivo StorSimple.
  2. Seleccione el servicio StorSimple Manager, haga clic en **dispositivos** y elija el dispositivo de StorSimple específico de Hola. Haga clic en **configurar** y comprobar la configuración de interfaz de red de Hola. A continuación se muestra una captura de pantalla con dos interfaces de red habilitadas para iSCSI. En este caso DATA 2 y DATA 3, las dos interfaces de 10 GbE están habilitadas para iSCSI.
     
      ![Configuración de MPIO StorSimple DATA 2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configuración de MPIO StorSimple DATA 3](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      Hola **configurar** página
     
     1. Asegúrese de que ambas interfaces de red están habilitadas para iSCSI. Hola **habilitado para iSCSI** campo debe estar establecido demasiado**Sí**.
     2. Asegúrese de que las interfaces de red de hello tienen Hola velocidad del mismo, debe ser 1 GbE o 10 GbE.
     3. Anote las direcciones IPv4 de Hola de interfaces de hello habilitada para iSCSI y guardar para su uso posterior en el host de Hola.
* interfaces de iSCSI de Hello en el dispositivo de StorSimple deben ser accesibles desde el servidor de CentOS Hola.
      tooverify, necesita las direcciones IP tooprovide Hola de las interfaces de red habilitada para iSCSI de StorSimple en su servidor host. Hola comandos usados y Hola salida correspondiente con DATA2 (10.126.162.25) y DATA3 (10.126.162.26) se muestra a continuación:
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>Configuración de hardware
Se recomienda que se conectan en rutas de acceso independientes para la redundancia de la dos interfaces de red iSCSI Hola. Hola siguiente ilustración muestra la configuración de hardware recomendada de Hola para lograr alta disponibilidad y equilibrio de carga de múltiples rutas para el servidor de CentOS y el dispositivo de StorSimple.

![Configuración de hardware MPIO para StorSimple tooLinux host](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

Como se muestra en hello anterior figura:

* El dispositivo StorSimple está en una configuración activa-pasiva con dos controladores.
* Dos conmutadores de SAN son controladores de dispositivo de tooyour conectado.
* En el dispositivo StorSimple se habilitan dos iniciadores iSCSI.
* Dos interfaces de red están habilitadas en el host CentOS.

Hola por encima de configuración brindará 4 rutas de acceso independientes entre el host de hello y dispositivo si las interfaces de host y los datos de hello sean enrutables.

> [!IMPORTANT]
> * Recomendamos no combinar interfaces de red de 1 GbE y de 10 GbE para las múltiples rutas. Cuando se usan dos interfaces de red, ambas interfaces Hola deben ser Hola idéntico tipo.
> * En el dispositivo StorSimple, DATA0, DATA1, DATA4 y DATA5 son interfaces de 1 GbE mientras que DATA2 y DATA3 son interfaces de red de 10 GbE.|
> 
> 

## <a name="configuration-steps"></a>Pasos de configuración
pasos de configuración de Hola de múltiples rutas implican la configuración de rutas de acceso disponibles hello para la detección automática, especificar toouse algoritmo Hola equilibrio de carga, habilitar múltiples rutas y por último, comprobar la configuración de Hola. Cada uno de estos pasos se explica con detalle en las secciones siguientes de Hola.

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>Paso 1: Configuración de múltiples rutas para la detección automática
dispositivos de Hello compatible con múltiples rutas pueden detectar y configurar automáticamente.

1. Inicialice el archivo `/etc/multipath.conf` . Escriba:
   
     `mpathconf --enable`
   
    Hola encima comando creará una `sample/etc/multipath.conf` archivo.
2. Inicie el servicio de múltiples rutas. Escriba:
   
    `service multipathd start`
   
    Verá Hola después de salida:
   
    `Starting multipathd daemon:`
3. Habilite la detección automática de múltiples rutas. Escriba:
   
    `mpathconf --find_multipaths y`
   
    Esto modificará Hola sección de valores predeterminados de su `multipath.conf` tal y como se muestra a continuación:
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>Paso 2: Configuración de múltiples rutas para volúmenes de StorSimple
De forma predeterminada, todos los dispositivos son negros aparecen en el archivo de multipath.conf hello y se omitirán. Necesitará toocreate lista negra excepciones tooallow multirruta para volúmenes de los dispositivos de StorSimple.

1. Editar hello `/etc/mulitpath.conf` archivo. Escriba:
   
    `vi /etc/multipath.conf`
2. Busque la sección de blacklist_exceptions de hello en el archivo de multipath.conf Hola. El dispositivo de StorSimple debe toobe aparece como una excepción de la lista negra de esta sección. Puede quite la marca de comentario relevante líneas toomodify de este archivo, tal y como se muestra a continuación (use solo Hola modelo específico de dispositivo de Hola que esté utilizando):
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a>Paso 3: Configuración de múltiples rutas por round-robin
Este algoritmo de equilibrio de carga utiliza todos los controlador activo de hello toohello multipaths disponibles de forma equilibrada, round robin.

1. Editar hello `/etc/multipath.conf` archivo. Escriba:
   
    `vi /etc/multipath.conf`
2. En hello `defaults` Hola de conjunto, en una sección `path_grouping_policy` demasiado`multibus`. Hola `path_grouping_policy` especifica tooapply toounspecified multipaths de agrupación directiva de hello predeterminado ruta de acceso. sección de valores predeterminados de Hello tendrá un aspecto tal y como se muestra a continuación.
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> Hola valores más comunes de `path_grouping_policy` incluyen:
> 
> * conmutación por error = 1 ruta de acceso por grupo de prioridad
> * multibus = todas las rutas de acceso válidas en un grupo de prioridad
> 
> 

### <a name="step-4-enable-multipathing"></a>Paso 4: Habilitación de múltiples rutas
1. Reinicie hello `multipathd` daemon. Escriba:
   
    `service multipathd restart`
2. salida de Hello será tal y como se muestra a continuación:
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>Paso 5: Comprobación de múltiples rutas
1. En primer lugar, asegúrese de que iSCSI se establece conexión con el dispositivo de StorSimple de hello como sigue:
   
   a. Detecte su dispositivo StorSimple. Escriba:
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    salida de Hello cuando una dirección IP de DATA0 es 10.126.162.25 y el puerto 3260 se abre en el dispositivo de StorSimple de hello para el tráfico saliente iSCSI es tal y como se muestra a continuación:
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    Hola copia IQN del dispositivo de StorSimple, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, de hello anterior de salida.

   b. Conecte el dispositivo toohello usando el IQN de destino. dispositivo de StorSimple de Hello es destino de iSCSI Hola aquí. Escriba:

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    Hello en el ejemplo siguiente se muestra la salida con un IQN de destino de `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`. salida de Hello indica que se han conectado correctamente toohello dos interfaces de red habilitada para iSCSI en el dispositivo.

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    Si ve interfaz sólo un host y dos rutas de acceso aquí, deberá tooenable ambas interfaces hello en el host para iSCSI. Puede seguir hello [instrucciones en la documentación de Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).

2. Un volumen es servidor de CentOS de toohello expuesto desde el dispositivo de StorSimple Hola. Para obtener más información, consulte [paso 6: crear un volumen](storsimple-deployment-walkthrough.md#step-6-create-a-volume) a través de hello portal de Azure clásico en el dispositivo StorSimple.

3. Compruebe las rutas de acceso disponibles Hola. Escriba:

      ```
      multipath –l
      ```

      Hola de ejemplo siguiente muestra la salida de hello para dos interfaces de red en una interfaz de red de host único de StorSimple dispositivo conectado tooa con dos rutas de acceso disponibles.

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a>Solución de problemas de múltiples rutas
En esta sección se proporcionan algunos consejos útiles si surge algún problema durante la configuración de múltiples rutas.

P: No veo cambios hello en `multipath.conf` archivo surten efecto.

A. Si ha realizado cualquier toohello cambios `multipath.conf` archivo, necesitará que el servicio de múltiples rutas de toorestart Hola. Escriba el siguiente comando de hello:

    service multipathd restart

P: He habilitado dos interfaces de red en el host de Hola y dos interfaces de red en el dispositivo StorSimple Hola. Cuando la lista de rutas de acceso disponibles hello, veo dos rutas de acceso. Esperaba toosee cuatro rutas disponibles.

A. Asegúrese de que las rutas de acceso de hello dos se encuentran en hello misma subred y enrutables. Si son las interfaces de red de hello en distintas redes VLAN y no enrutables, verá dos rutas de acceso. Una manera de tooverify se trata de toomake seguro de que puede comunicarse con ambas interfaces de host de Hola desde una interfaz de red en el dispositivo StorSimple Hola. Necesitará demasiado[póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) como esta comprobación solo puede realizarse a través de una sesión de soporte técnico.

P: Cuando muestro las rutas de acceso disponibles, no aparece ninguna salida.

A. Por lo general, no ve las rutas de acceso de detectar sugiere un problema con el demonio de múltiples rutas de Hola y es más probable es que cualquier problema radica en hello `multipath.conf` archivo.

También sería conveniente comprobar que realmente puede ver algunos discos después de conectarse toohello destino, tal y como se recibe ninguna respuesta de anuncios de Hola múltiples rutas también puede significar que no tiene ningún disco.

* Usar hello después de bus SCSI de comando toorescan hello:
  
    `$ rescan-scsi-bus.sh `(part of sg3_utils package)
* Escriba Hola siguientes comandos:
  
    `$ dmesg | grep sd*`
     
     O
  
    `$ fdisk –l`
  
    Se devolverán los detalles de los discos agregados recientemente.
* toodetermine si se trata de un disco de StorSimple, usar hello siguientes comandos:
  
    `cat /sys/block/<DISK>/device/model`
  
    Esto devolverá una cadena, que determinará si es un disco de StorSimple.

Una causa menos probable pero posible también podría ser iscsid pid desusado. Usar hello siguientes comando toolog off de sesiones de iSCSI de hello:

    iscsiadm -m node --logout -p <Target_IP>

Repita este comando para todas las interfaces de red de hello conectado en el destino de iSCSI de hello, que es el dispositivo StorSimple. Una vez que ha cerrado la sesión de todas las sesiones de iSCSI de hello, utilice sesión iSCSI de hello iSCSI target IQN tooreestablish Hola. Escriba el siguiente comando de hello:

    iscsiadm -m node --login -T <TARGET_IQN>


P: No estoy seguro de si el dispositivo está en la lista blanca.

A. tooverify si el dispositivo está en la lista blanca, utilice Hola siguiente comando interactivo para solucionar problemas:

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


Para obtener más información, consulte demasiado[usar la solución de problemas de comando interactivo de múltiples rutas](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).

## <a name="list-of-useful-commands"></a>Lista de comandos útiles
| Cuando se le pida confirmación, escriba  | Comando | Description |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |Iniciar el servicio iSCSI |
| &nbsp; |`service iscsid stop` |Detener el servicio iSCSI |
| &nbsp; |`service iscsid restart` |Reiniciar el servicio iSCSI |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |Detección de destinos disponibles en hello especificado dirección |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |Inicie sesión en el destino de iSCSI toohello |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |Cierre la sesión de destino iSCSI de Hola |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |Imprimir el nombre del iniciador iSCSI |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |Comprobar estado de Hola de sesión de iSCSI de Hola y volumen detectados en el host de Hola |
| &nbsp; |`iscsi –m session` |Muestra todas las sesiones de iSCSI de hello establecidas entre el host de Hola y de dispositivo de StorSimple de Hola |
|  | | |
| **Múltiples rutas** |`service multipathd start` |Iniciar el daemon de múltiples rutas |
| &nbsp; |`service multipathd stop` |Detener el daemon de múltiples rutas |
| &nbsp; |`service multipathd restart` |Reiniciar el daemon de múltiples rutas |
| &nbsp; |`chkconfig multipathd on` </br> OR </br> `mpathconf –with_chkconfig y` |Habilitar múltiples rutas daemon toostart al arrancar el sistema |
| &nbsp; |`multipathd –k` |Inicie la consola interactiva de Hola para solucionar problemas |
| &nbsp; |`multipath –l` |Enumerar dispositivos y conexiones de múltiples rutas |
| &nbsp; |`mpathconf --enable` |Crear un archivo de ejemplo mulitpath.conf en `/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>Pasos siguientes
Como va a configurar MPIO en el host de Linux, también deberá toohello toorefer después de CentoS 6.6 documentos:

* [Configuración de MPIO en CentOS](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Guía de aprendizaje de Linux](http://linux-training.be/files/books/LinuxAdm.pdf)

