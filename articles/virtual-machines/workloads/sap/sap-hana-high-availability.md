---
title: "Disponibilidad de SAP HANA en máquinas virtuales de Azure (VM) aaaHigh | Documentos de Microsoft"
description: "Establezca alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a>Alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

De forma local, puede usar cualquier replicación del sistema de archivos de HANA o usar almacenamiento compartido tooestablish alta disponibilidad para SAP HANA.
Actualmente solo se admite la configuración de la replicación del sistema de HANA en Azure. La replicación de SAP HANA se realiza con un nodo maestro y al menos uno subordinado. Toohello de cambios de datos en el nodo principal de hello son replica nodos de esclavo toohello forma sincrónica o asincrónica.

Este artículo describe cómo toodeploy hello las máquinas virtuales, configurar las máquinas virtuales de hello, instale Hola clúster framework, instalar y la configurar la replicación del sistema de SAP HANA.
En configuraciones de ejemplo de Hola, el número de instancia etc. 03 de comandos de instalación y se utiliza HDB de Id. de sistema de archivos de HANA.

Hola de lectura siguientes notas de SAP y documentos en primer lugar

* Nota de SAP [1928533], que incluye:
  * Lista de tamaños de máquina virtual de Azure que se admiten para la implementación de hello del software SAP.
  * Información importante sobre la capacidad para los tamaños de máquina virtual de Azure
  * Software de SAP admitido y combinaciones de sistema operativo y base de datos
  * Versión del kernel de SAP requerida para Windows y Linux en Microsoft Azure
* La nota de SAP [2015553] enumera los requisitos previos para las implementaciones de software de SAP admitidas por SAP en Azure.
* La nota de SAP [2205917] contiene configuraciones recomendadas del sistema operativo para SUSE Linux Enterprise Server para SAP Applications
* La nota de SAP [1944799] contiene guías de SAP HANA para SUSE Linux Enterprise Server para SAP Applications
* La nota de SAP [2178632] contiene información detallada sobre todas las métricas de supervisión notificadas para SAP en Azure.
* Nota de SAP [2191498] Hola necesario versión del agente de Host de SAP para Linux en Azure.
* La nota de SAP [2243692] incluye información acerca de las licencias de SAP en Linux en Azure.
* La nota de SAP [1984787] incluye información general sobre SUSE Linux Enterprise Server 12.
* Nota de SAP [1999351] información adicional de solución de problemas de hello Azure extensión de supervisión mejorada para SAP.
* La [WIKI de la comunidad SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene todas las notas de SAP que se necesitan para Linux.
* [Planeación e implementación de Azure Virtual Machines para SAP en Linux][planning-guide]
* [Implementación de Azure Virtual Machines para SAP en Linux (este artículo)][deployment-guide]
* [Implementación de DBMS de Azure Virtual Machines para SAP en Linux][dbms-guide]
* [SAP HANA SR rendimiento optimizado escenario] [ suse-hana-ha-guide] guía hello contiene todos los tooset de información necesaria la replicación del sistema de SAP HANA local. Esta guía sirve como orientación.

## <a name="deploying-linux"></a>Implementación de Linux

agente de recursos de Hola para SAP HANA se incluye en SUSE Linux Enterprise Server para aplicaciones de SAP.
Hello Azure Marketplace contiene una imagen para SUSE Linux Enterprise Server para el 12 de las aplicaciones de SAP con BYOS (poner su propia suscripción) que puede usar máquinas virtuales de la nueva toodeploy.

### <a name="manual-deployment"></a>Implementación manual

1. Creación de un grupo de recursos
1. Creación de una red virtual
1. Creación de dos cuentas de almacenamiento
1. Creación de un conjunto de disponibilidad  
   Establecimiento del dominio máximo de actualización
1. Creación de un equilibrador de carga (interno)  
   Selección de la red virtual del paso anterior
1. Creación de la máquina virtual 1  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES para SAP Applications 12 SP1 (BYOS)  
   Selección de la cuenta de almacenamiento 1  
   Selección del conjunto de disponibilidad  
1. Creación de la máquina virtual 2  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES para SAP Applications 12 SP1 (BYOS)  
   Selección de la cuenta de almacenamiento 2   
   Selección del conjunto de disponibilidad  
1. Incorporación de los discos de datos
1. Configure el equilibrador de carga de Hola
    1. Creación de un grupo de direcciones IP de front-end
        1. Abra el equilibrador de carga de hello, seleccione el grupo de direcciones IP de front-end y haga clic en Agregar
        1. Escriba el nombre de Hola Hola nuevo front-end del grupo de IP (por ejemplo hana-front-end)
       1. Haga clic en Aceptar
        1. Después de crea nuevo grupo IP de front-end hello, anote su dirección IP
    1. Creación de un grupo de back-end
        1. Abra el equilibrador de carga de hello, seleccione grupos back-end y haga clic en Agregar
        1. Escriba el nombre de Hola de nuevo grupo back-end de hello (por ejemplo hana-back-end)
        1. Haga clic en Agregar una máquina virtual
        1. Seleccione Hola conjunto de disponibilidad que creó anteriormente
        1. Seleccione las máquinas virtuales del clúster de SAP HANA Hola Hola
        1. Haga clic en Aceptar
    1. Creación de un sondeo de estado
       1. Abra el equilibrador de carga de hello, seleccione sondeos de mantenimiento y haga clic en Agregar
        1. Escriba el nombre de Hola de sondeo de estado nuevo de hello (por ejemplo hana-hp)
        1. Seleccione TCP como protocolo, puerto 625**03**, y mantenga el intervalo de 5 y el umbral incorrecto 2
        1. Haga clic en Aceptar
    1. Creación de reglas de equilibrio de carga
        1. Abra el equilibrador de carga de hello, seleccione las reglas de equilibrio de carga y haga clic en Agregar
        1. Escriba Hola nombre de regla de equilibrador de carga nueva hello (por ejemplo hana-lb-3**03**15)
        1. Dirección IP de Front-End Select hello, grupo back-end y estado de sondeo que ha creado anteriormente (por ejemplo hana-front-end)
        1. Conserve el protocolo TCP y escriba el puerto 3**03**15
        1. Aumentar el tiempo de espera inactivo too30 minutos
       1. **Asegúrese de que tooenable dirección IP flotante**
        1. Haga clic en Aceptar
        1. Repita los pasos de hello anteriormente para el puerto 3**03**17

### <a name="deploy-with-template"></a>Implementación con plantilla
Puede usar una de las plantillas de inicio rápido de hello en github toodeploy todos los recursos necesarios. plantilla de Hello implementa máquinas virtuales de hello, equilibrador de carga de hello, etcetera conjunto de disponibilidad. Siga estas plantillas de hello toodeploy de pasos:

1. Abra hello [plantilla de base de datos] [ template-multisid-db] o hello [convergente plantilla] [ template-converged] en hello Azure Portal plantilla de la base de datos de hello sólo crea Hola reglas de equilibrio de carga para una base de datos mientras que también se crea la plantilla convergente Hola Hola reglas de equilibrio de carga para un ASCS/SCS y la instancia ERS (solamente para Linux). Si tiene pensado tooinstall un sistema basadas en SAP NetWeaver y también desea tooinstall Hola ASCS/SCS a la instancia en hello mismo máquinas, use hello [convergente plantilla][template-converged].
1. Escriba Hola parámetros siguientes
    1. Identificador de sistema SAP  
       Especifique el sistema SAP de hello Id. de hello sistema SAP que desee tooinstall. Hola Id. se usará como prefijo para los recursos de Hola que se implementan.
    1. Tipo de pila (solo se aplica si usa Hola convergente plantilla)  
       Seleccione el tipo de pila de SAP NetWeaver Hola
    1. Tipo de sistema operativo  
       Seleccione una de las distribuciones de Linux de Hola. En este ejemplo, seleccione SLES 12 BYOS
    1. Tipo de base de datos  
       Seleccione HANA
    1. Tamaño del sistema SAP  
       cantidad de Hola de nuevo sistema de SAPS Hola proporcionará. Si no estás seguro de sistema de Hola de SAPS cuántos requerirá, póngase en contacto con su socio de tecnología de SAP o integrador de sistema
    1. Disponibilidad del sistema  
       Seleccione alta disponibilidad
    1. Nombre de usuario y contraseña del administrador  
       Se crea un nuevo usuario que pueden ser toolog usado en la máquina toohello.
    1. Subred nueva o existente  
       Determina si es necesario crear una red virtual y subred nuevas o si se debe usar una subred existente. Si ya tiene una red virtual que es la red local de tooyour conectado, seleccione existente.
    1. Identificador de subred  
    Id. de Hola de máquinas virtuales de hello subred toowhich Hola debe estar conectado a. Seleccione la subred de hello de la VPN o Express Route red virtual tooconnect Hola máquina virtual tooyour en red local. Id. de Hello suele ser algo parecido/subscriptions /`<subscription id`>/ResourceGroups /`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

## <a name="setting-up-linux-ha"></a>Configuración de la alta disponibilidad de Linux

Hola siguientes elementos tienen el prefijo cualquiera [A] - nodos tooall aplicables, toonode solo se aplica de - solo se aplica toonode 1 o [2]: [1] 2.

1. [A] SLES para SAP BYOS solo - repositorios de hello toouse capaz de registrar SLES toobe
1. [A] SLES solo para SAP BYOS: agregue el módulo de nube pública
1. [A] Actualice SLES
    ```bash
    sudo zypper update

    ```

1. [1] Habilite el acceso de SSH
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. [2] Habilite el acceso de SSH
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. [1] Habilite el acceso de SSH
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. [A] Instale la extensión de alta disponibilidad
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. [A] Configure el diseño del disco
    1. LVM  
    Por lo general, se recomienda toouse LVM para volúmenes que almacenan los datos y archivos de registro. ejemplo de Hola siguiente supone que máquinas virtuales de hello tiene cuatro discos de datos conectados que se deben toocreate usa dos volúmenes.
        * Crear volúmenes físicos de todos los discos que desea toouse.
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * Crear un grupo de volúmenes para los archivos de datos de hello, un grupo de volúmenes para los archivos de registro de hello y otro para el directorio compartido de Hola de SAP HANA
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * Crear volúmenes lógicos de Hola
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * Crear los directorios de montaje de Hola y copiar Hola UUID de todos los volúmenes lógicos
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * Crear las entradas de fstab de hello tres volúmenes lógicos
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    Inserte esta línea demasiado/etcetera/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * Montar volúmenes nuevos Hola
    <pre><code>
    sudo mount -a
    </code></pre>
    1. Discos sin formato  
       Para sistemas pequeños o de demostración, puede colocar los archivos de datos y de registro HANA en un disco. Hello siguientes comandos crean una partición en /dev/sdc y dele formato con xfs.
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a>Anote el Id. de Hola de /dev/sdc1
    sudo /sbin/blkid  sudo vi /etc/fstab
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. [A] Configure la resolución del nombre de todos los hosts  
    Puede usar un servidor DNS o modificar Hola/etc/hosts en todos los nodos. Este ejemplo muestra cómo toouse Hola archivo/etc/hosts.
   Reemplace la dirección IP de Hola y el nombre de host de Hola Hola siga los comandos
    ```bash
    sudo vi /etc/hosts
    ```
    Insertar Hola después líneas demasiado/etcetera/hosts. Cambiar toomatch de dirección y el nombre de host IP hello en el entorno    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. [1] Instale el clúster
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. [2] agregar nodo toocluster
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. [A] cambio hacluster contraseña toohello misma contraseña
    ```bash
    sudo passwd hacluster
    
    ```

1. [A] configurar corosync toouse otros tipos de transporte y agregar la lista de nodos. De lo contrario, el clúster no funcionará.
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    Agregar hello toohello contenido negrita el archivo siguiente.
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    A continuación, reinicie el servicio de hello corosync

    ```bash
    sudo service corosync restart
    
    ```

1. [A] Instale los paquetes de alta disponibilidad de HANA  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a>Instalación de SAP HANA

Siga el capítulo 4 de hello [Guía de SAP HANA SR rendimiento optimizado escenario] [ suse-hana-ha-guide] tooinstall replicación del sistema de SAP HANA.

1. [A] ejecutar hdblcm desde Hola HANA DVD
    * Elija la instalación -> 1
    * Seleccione los componentes adicionales para la instalación -> 1
    * Escriba la ruta de acceso de instalación [/hana/shared]: -> ENTRAR
    * Escriba el nombre del host local [..]: -> ENTRAR
    * ¿Desea que el sistema de toohello de tooadd hosts adicionales? (s/n) [n]: -> ENTRAR
    * Escriba el identificador del sistema de SAP HANA: <SID of HANA e.g. HDB>
    * Escriba el número de instancia [00]:   
  Número de instancia de HANA. Usar 03 si usa Hola plantilla de Azure o seguir el ejemplo de Hola anterior
    * Seleccione Database Mode (Modo de base de datos) / escriba el índice [1]: -> ENTRAR
    * Seleccione Uso del sistema / escriba el índice [4]:  
  Seleccione sistema Hola uso
    * Escriba la ubicación de los volúmenes de datos [/hana/data/HDB]: -> ENTRAR
    * Escriba la ubicación de los volúmenes de registros [/hana/log/HDB]: -> ENTRAR
    * ¿Restringir la asignación de memoria máxima? [n]: -> ENTRAR
    * Escriba el nombre de Host de certificado de Host '...' [...]: -> ENTRAR
    * Escriba la contraseña del usuario del agente de host de SAP (sapadm):
    * Confirme la contraseña del usuario del agente de host de SAP (sapadm):
    * Escriba la contraseña del administrador del sistema (hdbadm):
    * Confirme la contraseña del administrador del sistema (hdbadm):
    * Escriba el directorio principal del administrador de sistema [/usr/sap/HDB/home]: -> ENTRAR
    * Escriba el shell de inicio de sesión del administrador de sistema [/bin/sh]: -> ENTRAR
    * Escriba el identificador de usuario del administrador de sistema [1001]: -> ENTRAR
    * Escriba el identificador del grupo de usuarios (sapsys) [79]: -> ENTRAR
    * Escriba la contraseña del usuario (SYSTEM) de la base de datos:
    * Confirme la contraseña del usuario (SYSTEM) de la base de datos:
    * ¿Reiniciar el sistema tras el reinicio de la máquina? [n]: -> ENTRAR
    * ¿Desea toocontinue? (s/n):  
  Validar Hola resumen y escriba y toocontinue
1. [A] Actualice el agente de host de SAP  
  Descargue el archivo de agente de Host de SAP más reciente de Hola de hello [SAP Softwarecenter] [ sap-swcenter] y ejecución hello siguientes comando tooupgrade Hola agente. Reemplace Hola ruta de acceso toohello toopoint toohello archivo que descargó.
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. [1] Cree la replicación de HANA (como raíz)  
    Ejecutar el siguiente comando de Hola. Asegúrese de que tooreplace negrita cadenas (HDB de Id. de sistema de archivos de HANA y número de instancia 03) con valores de hello de la instalación de SAP HANA.
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. [A] Cree la entrada de almacén de claves (como raíz).
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. [1] Realice la copia de seguridad de la base de datos (como raíz).
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. [1] Cambie toohello sapsid usuario (por ejemplo hdbadm) y crear el sitio primario de Hola.
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. [2] Cambie toohello sapsid usuario (por ejemplo hdbadm) y crear sitio secundario de Hola.
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a>Configuración de la plataforma del clúster

Cambiar la configuración predeterminada de Hola

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Ahora se Hola archivo toohello clúster de carga
sudo crm configura la actualización de carga de crm-defaults.txt
</pre>

### <a name="create-stonith-device"></a>Creación de un dispositivo STONITH

dispositivo de Hello STONITH utiliza un tooauthorize de entidad de servicio en Microsoft Azure. Siga estos toocreate pasos una entidad de servicio.

1. Vaya demasiado<https://portal.azure.com>
1. Hoja de Azure Active Directory Hola abierto  
   Vaya tooProperties y anote Hola Id. de directorio. Se trata de hello **Id. de inquilino**.
1. Haga clic en Registros de aplicaciones
1. Haga clic en Agregar
1. Escriba un nombre, seleccione el tipo de aplicación "Aplicación web o API", escriba una dirección URL de inicio de sesión (por ejemplo, http://localhost) y haga clic en Crear
1. dirección URL de inicio de sesión de Hello no se usa y puede ser cualquier dirección URL válida
1. Seleccione Hola nueva aplicación y haga clic en las claves en la ficha de configuración de Hola
1. Escriba una descripción para la nueva clave, seleccione "Nunca expira" y haga clic en Guardar
1. Anote el valor de Hola. Se utiliza como hello **contraseña** para hello entidad de servicio
1. Anote Hola identificador de aplicación. Se utiliza como nombre de usuario de Hola (**Id. de inicio de sesión** en estos pasos hello) de hello entidad de servicio

Hola entidad de servicio no tiene permisos tooaccess los recursos de Azure de forma predeterminada. Necesita toostart de permisos de entidad de servicio de toogive hello y detener (desasignar) todas las máquinas virtuales del clúster de Hola.

1. Vaya toohttps://portal.azure.com
1. Abrir Hola a todos los módulos de recursos
1. Seleccione la máquina virtual de Hola
1. Haga clic en Control de acceso (IAM)
1. Haga clic en Agregar
1. Seleccione el rol de hello propietario
1. Escriba Hola nombre de aplicación Hola que creó anteriormente
1. Haga clic en Aceptar

Después de editar permisos de Hola para las máquinas virtuales de hello, puede configurar dispositivos STONITH hello en clúster de Hola.

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Ahora se Hola archivo toohello clúster de carga
sudo crm configura la actualización de carga de crm-fencing.txt
</pre>

### <a name="create-sap-hana-resources"></a>Creación de recursos de SAP HANA

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Ahora se Hola archivo toohello clúster de carga
sudo crm configura la actualización de carga de crm-saphanatop.txt
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Ahora se Hola archivo toohello clúster de carga
sudo crm configura la actualización de carga de crm-saphana.txt
</pre>

### <a name="test-cluster-setup"></a>Prueba de configuración del clúster
Hola siguiente capítulo describe cómo puede probar el programa de instalación. Todas las pruebas se supone que son raíz y maestro de SAP HANA Hola se está quedando hello saphanavm1 de máquina virtual.

#### <a name="fencing-test"></a>Prueba de vallado

Puede probar el programa de instalación de hello del agente de barrera de hello deshabilitando la interfaz de red de hello en el nodo saphanavm1.

<pre><code>
sudo ifdown eth0
</code></pre>

máquina virtual de Hello ahora debe obtener reinicia o detenido según la configuración del clúster.
Si establece hello stonith acción toooff, se detendrá la máquina virtual de Hola y recursos de hello están migrado toohello máquina virtual en ejecución.

Una vez que volver a iniciar máquina virtual de hello, Hola recursos de SAP HANA se producirá un error toostart como base de datos secundaria si establece AUTOMATED_REGISTER = "false". En este caso, necesita tooconfigure Hola HANA instancia secundarias mediante la ejecución de hello siguiente comando:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a>Prueba de una conmutación por error manual

Puede probar una conmutación por error manual Deteniendo el servicio de marcapasos de hello en el nodo saphanavm1.
<pre><code>
service pacemaker stop
</code></pre>

Después de la conmutación por error de hello, puede iniciar servicio Hola de nuevo. Hola recursos de SAP HANA en saphanavm1 se producirá un error toostart como base de datos secundaria si establece AUTOMATED_REGISTER = "false". En este caso, necesita tooconfigure Hola HANA instancia secundarias mediante la ejecución de hello siguiente comando:

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a>Prueba de una migración

Puede migrar el nodo principal de SAP HANA Hola ejecutando el siguiente comando de Hola
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

Esto debe migrar nodo maestro de SAP HANA hello y grupo de Hola que contenga hello toosaphanavm2 de dirección IP virtual.
Hola recursos de SAP HANA en saphanavm1 se producirá un error toostart como base de datos secundaria si establece AUTOMATED_REGISTER = "false". En este caso, necesita tooconfigure Hola HANA instancia secundarias mediante la ejecución de hello siguiente comando:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

migración de Hello crea restricciones de ubicación que necesitan toobe eliminarlos de nuevo.

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

También necesita toocleanup estado de Hola de recursos del nodo secundario de Hola

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a>Pasos siguientes
* [Planeación e implementación de Azure Virtual Machines para SAP][planning-guide]
* [Implementación de Azure Virtual Machines para SAP][deployment-guide]
* [Implementación de DBMS de Azure Virtual Machines para SAP][dbms-guide]
* toolearn tooestablish alta disponibilidad y el plan de recuperación ante desastres de SAP HANA en Azure (instancias grandes), vea [SAP HANA (instancias de gran tamaño) alta disponibilidad y recuperación ante desastres en Azure](hana-overview-high-availability-disaster-recovery.md). 
