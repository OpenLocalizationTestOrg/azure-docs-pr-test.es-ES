---
title: "Máquinas virtuales alta disponibilidad para SAP NetWeaver en SUSE Linux Enterprise Server para aplicaciones de SAP aaaAzure | Documentos de Microsoft"
description: "Guía de alta disponibilidad para SAP NetWeaver en SUSE Linux Enterprise Server para SAP Applications"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a>Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure en SUSE Linux Enterprise Server para SAP Applications

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
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

Este artículo describe cómo configurar las máquinas virtuales de hello toodeploy hello las máquinas virtuales, instalar el marco de trabajo de clúster de Hola e instalar un sistema SAP NetWeaver 7.50 alta disponibilidad.
En configuraciones de ejemplo de Hola, etcetera mediante comandos de instalación. se usa el número de instancia 00 de ASCS, el número de instancia 02 de ERS y NWS del identificador de sistema de SAP. Hello nombres de recursos de hello (por ejemplo, las máquinas virtuales, redes virtuales) en el ejemplo de Hola se asume que ha utilizado hello [convergente plantilla] [ template-converged] con recursos SAP sistema identificador NWS toocreate Hola.

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
* [Escenario de rendimiento optimizado para la replicación del sistema de SAP HANA][suse-hana-ha-guide]  
  Guía de Hello contiene todos los tooset de información necesaria la replicación del sistema de SAP HANA local. Esta guía sirve como orientación.
* [Alta el almacenamiento de NFS disponible con DRBD y marcapasos] [ suse-drbd-guide] guía hello contiene todos los tooset de la información necesaria de un servidor NFS de alta disponibilidad. Esta guía sirve como orientación.


## <a name="overview"></a>Información general

tooachieve la alta disponibilidad, SAP NetWeaver requiere un servidor NFS. servidor NFS de Hello está configurado en un clúster diferente y puede usarse en varios sistemas SAP.

![Información general sobre la alta disponibilidad de SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

Hola servidor NFS, SAP NetWeaver ASCS, SCS de SAP NetWeaver, SAP NetWeaver ERS y base de datos de SAP HANA Hola usar nombre del host virtual y direcciones IP virtuales. En Azure, un equilibrador de carga es toouse requiere una dirección IP virtual. Hello lista siguiente muestra configuración Hola Hola de equilibrador de carga.

### <a name="nfs-server"></a>Servidor NFS
* Configuración de front-end
  * Dirección IP 10.0.0.4
* Configuración de back-end
  * Conectado tooprimary interfaces de red de todas las máquinas virtuales que deben formar parte del clúster NFS de Hola
* Puerto de sondeo
  * Puerto 61000
* Reglas de equilibrio de carga
  * 2049 TCP 
  * 2049 UDP

### <a name="ascs"></a>(A)SCS
* Configuración de front-end
  * Dirección IP 10.0.0.10
* Configuración de back-end
  * Interfaces de red conectados tooprimary de todas las máquinas virtuales que deben formar parte del clúster de hello (A) SCS/ERS
* Puerto de sondeo
  * Puerto 620**&lt;nr&gt;**
* Reglas de equilibrio de carga
  * 32**&lt;nr&gt;** TCP
  * 36**&lt;nr&gt;** TCP
  * 39**&lt;nr&gt;** TCP
  * 81**&lt;nr&gt;** TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="ers"></a>ERS
* Configuración de front-end
  * Dirección IP 10.0.0.11
* Configuración de back-end
  * Interfaces de red conectados tooprimary de todas las máquinas virtuales que deben formar parte del clúster de hello (A) SCS/ERS
* Puerto de sondeo
  * Puerto 621**&lt;nr&gt;**
* Reglas de equilibrio de carga
  * 33**&lt;nr&gt;** TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="sap-hana"></a>SAP HANA
* Configuración de front-end
  * Dirección IP 10.0.0.12
* Configuración de back-end
  * Conectado tooprimary interfaces de red de todas las máquinas virtuales que debe formar parte del clúster HANA Hola
* Puerto de sondeo
  * Puerto 625**&lt;nr&gt;**
* Reglas de equilibrio de carga
  * 3**&lt;nr&gt;**15 TCP
  * 3**&lt;nr&gt;**17 TCP

## <a name="setting-up-a-highly-available-nfs-server"></a>Configuración de un servidor NFS de alta disponibilidad

### <a name="deploying-linux"></a>Implementación de Linux

Hello Azure Marketplace contiene una imagen para SUSE Linux Enterprise Server para el 12 de las aplicaciones de SAP que puede usar máquinas virtuales de la nueva toodeploy.
Puede usar una de las plantillas de inicio rápido de hello en github toodeploy todos los recursos necesarios. plantilla de Hello implementa máquinas virtuales de hello, equilibrador de carga de hello, etcetera conjunto de disponibilidad. Siga estas plantillas de hello toodeploy de pasos:

1. Abra hello [plantilla de servidor de archivos SAP] [ template-file-server] Hola portal de Azure   
1. Escriba Hola parámetros siguientes
   1. Prefijo de recurso  
      Escriba el prefijo Hola desea toouse. valor de Hola se usa como prefijo para los recursos de Hola que se implementan.
   2. Tipo de sistema operativo  
      Seleccione una de las distribuciones de Linux de Hola. En este ejemplo, seleccione SLES 12
   3. Nombre de usuario y contraseña del administrador  
      Se crea un nuevo usuario que pueden ser toolog usado en la máquina toohello.
   4. Identificador de subred  
      Id. de Hola de máquinas virtuales de hello subred toowhich Hola debe estar conectado a. Deje en blanco si desea toocreate una nueva red virtual o seleccione subred hello de la VPN o Express Route red virtual tooconnect Hola máquina virtual tooyour en red local. Id. de Hello suele ser algo parecido/subscriptions /**&lt;Id. de suscripción&gt;**/ResourceGroups /**&lt;nombre del grupo de recursos&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nombre de red virtual&gt;**/subnets/**&lt;nombre de subred&gt;**

### <a name="installation"></a>Instalación

Hello elementos siguientes tienen el prefijo cualquiera **[A]** -nodos tooall aplicables, **[1]** -solo es aplicable toonode 1 o **[2]** -solo es aplicable toonode 2.

1. **[A]** Actualice SLES

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** Habilite el acceso de SSH

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** Habilite el acceso de SSH

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** Habilite el acceso de SSH

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** Instale la extensión de alta disponibilidad
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** Configure la resolución nombres de host   

   Puede usar un servidor DNS o modificar Hola/etc/hosts en todos los nodos. Este ejemplo muestra cómo toouse Hola archivo/etc/hosts.
   Reemplace la dirección IP de Hola y el nombre de host de Hola Hola siga los comandos

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Insertar Hola después líneas demasiado/etcetera/hosts. Cambiar toomatch de dirección y el nombre de host IP hello en el entorno   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. **[1]** Instale el clúster
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Agregar nodo toocluster
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Cambio hacluster contraseña toohello misma contraseña

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Configurar corosync toouse otros tipos de transporte y agregar la lista de nodos. De lo contrario, el clúster no funcionará.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

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
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   A continuación, reinicie el servicio de hello corosync

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** Instale los componentes de drbd

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Crear una partición para el dispositivo de hello drbd

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** Cree configuraciones de LVM

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. **[A]**  Dispositivo drbd de crear Hola NFS

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   Insertar la configuración de hello para el nuevo dispositivo de drbd Hola y de salida

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   Crear un dispositivo de hello drbd e inícielo

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. **[1]** Omita la sincronización inicial

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Conjunto Hola el nodo principal

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Espere hasta que se sincronizan los nuevos dispositivos de drbd Hola

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Crear sistemas de archivos en hello drbd dispositivos

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a>Configuración de la plataforma del clúster

1. **[1]**  Cambiar la configuración predeterminada de Hola

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Configuración del clúster agregar Hola NFS drbd dispositivo toohello

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Servidor NFS que crear Hola

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Crear recursos de sistema de archivos NFS Hola

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Crear exportaciones NFS de Hola

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Crear un recurso de IP virtual y un sondeo de estado de equilibrador de carga interno de Hola

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

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

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Crear dispositivos de hello STONITH

Después de editar permisos de Hola para las máquinas virtuales de hello, puede configurar dispositivos STONITH hello en clúster de Hola.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Habilitar el uso de Hola de un dispositivo STONITH

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a>Configuración de (A)SCS

### <a name="deploying-linux"></a>Implementación de Linux

Hello Azure Marketplace contiene una imagen para SUSE Linux Enterprise Server para el 12 de las aplicaciones de SAP que puede usar máquinas virtuales de la nueva toodeploy. imagen de marketplace de Hello contiene a agente de recursos de Hola para SAP NetWeaver.

Puede usar una de las plantillas de inicio rápido de hello en github toodeploy todos los recursos necesarios. plantilla de Hello implementa máquinas virtuales de hello, equilibrador de carga de hello, etcetera conjunto de disponibilidad. Siga estas plantillas de hello toodeploy de pasos:

1. Abra hello [plantilla ASCS/SCS múltiples SID] [ template-multisid-xscs] o hello [convergente plantilla] [ template-converged] en plantilla solo de Hola Hola portal Azure ASCS/SCS crea reglas de equilibrio de carga de hello hello ASCS/SCS de SAP NetWeaver y instancias ERS (solamente para Linux), mientras que la plantilla convergente hello también crea reglas de equilibrio de carga de Hola para una base de datos (por ejemplo Microsoft SQL Server o SAP HANA). Si tiene pensado tooinstall un sistema basadas en SAP NetWeaver y también desea base de datos de tooinstall hello en Hola mismo máquinas, use hello [convergente plantilla][template-converged].
1. Escriba Hola parámetros siguientes
   1. Prefijo de recurso (solo la plantilla de varios ASCS/SCS de varios SID)  
      Escriba el prefijo Hola desea toouse. valor de Hola se usa como prefijo para los recursos de Hola que se implementan.
   3. Identificador del sistema SAP (solo la plantilla convergente)  
      Especifique el sistema SAP de hello Id. de hello sistema SAP que desee tooinstall. Hola identificador se usa como prefijo para los recursos de Hola que se implementan.
   4. Tipo de pila  
      Seleccione el tipo de pila de SAP NetWeaver Hola
   5. Tipo de sistema operativo  
      Seleccione una de las distribuciones de Linux de Hola. En este ejemplo, seleccione SLES 12 BYOS
   6. Tipo de base de datos  
      Seleccione HANA
   7. Tamaño del sistema SAP  
      proporciona la cantidad de Hola de nuevo sistema de SAPS Hola. Si no estás seguro de cuántos SAPS Hola sistema requiere, póngase en contacto con su socio de tecnología de SAP o integrador de sistema
   8. Disponibilidad del sistema  
      Seleccione alta disponibilidad
   9. Nombre de usuario y contraseña del administrador  
      Se crea un nuevo usuario que pueden ser toolog usado en la máquina toohello.
   10. Identificador de subred  
   Id. de Hola de máquinas virtuales de hello subred toowhich Hola debe estar conectado a.  Deje en blanco si desea toocreate una nueva red virtual o seleccione Hola la misma subred que utilizan o se crea como parte de la implementación de servidor NFS de Hola. Id. de Hello suele ser algo parecido/subscriptions /**&lt;Id. de suscripción&gt;**/ResourceGroups /**&lt;nombre del grupo de recursos&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nombre de red virtual&gt;**/subnets/**&lt;nombre de subred&gt;**

### <a name="installation"></a>Instalación

Hello elementos siguientes tienen el prefijo cualquiera **[A]** -nodos tooall aplicables, **[1]** -solo es aplicable toonode 1 o **[2]** -solo es aplicable toonode 2.

1. **[A]** Actualice SLES

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** Habilite el acceso de SSH

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** Habilite el acceso de SSH

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** Habilite el acceso de SSH

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** Instale la extensión de alta disponibilidad
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** Actualice los agentes de recursos de SAP  
   
   Una revisión para el paquete de agentes de recursos de hello es nueva configuración de Hola de toouse necesarios, que se describe en este artículo. Puede comprobar, si ya está instalada la revisión Hola con hello siguiente comando

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   salida de Hello debe ser similar a

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   Si el comando grep de hello no encuentra el parámetro IS_ERS hello, necesita revisión de hello tooinstall aparece en [página de descarga de hello SUSE](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. **[A]** Configure la resolución nombres de host   

   Puede usar un servidor DNS o modificar Hola/etc/hosts en todos los nodos. Este ejemplo muestra cómo toouse Hola archivo/etc/hosts.
   Reemplace la dirección IP de Hola y el nombre de host de Hola Hola siga los comandos

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Insertar Hola después líneas demasiado/etcetera/hosts. Cambiar toomatch de dirección y el nombre de host IP hello en el entorno   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. **[1]** Instale el clúster
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Agregar nodo toocluster
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Cambio hacluster contraseña toohello misma contraseña

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Configurar corosync toouse otros tipos de transporte y agregar la lista de nodos. De lo contrario, el clúster no funcionará.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

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
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   A continuación, reinicie el servicio de hello corosync

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** Instale los componentes de drbd

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Crear una partición para el dispositivo de hello drbd

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** Cree configuraciones de LVM

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. **[A]**  Dispositivo drbd de crear Hola SCS

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   Insertar la configuración de hello para el nuevo dispositivo de drbd Hola y de salida

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   Crear un dispositivo de hello drbd e inícielo

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. **[A]**  Dispositivo de crear Hola ERS drbd

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   Insertar la configuración de hello para el nuevo dispositivo de drbd Hola y de salida

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   Crear un dispositivo de hello drbd e inícielo

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. **[1]** Omita la sincronización inicial

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Conjunto Hola el nodo principal

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Espere hasta que se sincronizan los nuevos dispositivos de drbd Hola

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Crear sistemas de archivos en hello drbd dispositivos

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a>Configuración de la plataforma del clúster

**[1]**  Cambiar la configuración predeterminada de Hola

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a>Preparación de la instalación de SAP NetWeaver

1. **[A]**  Hola de crear los directorios compartidos

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. **[A]** Configure autofs
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Cree un archivo con

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   Reinicie nuevos recursos compartidos autofs toomount Hola

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. **[A]** Configure el archivo de intercambio
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Reiniciar Hola agente tooactivate Hola cambios

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a>Instalación de SAP NetWeaver ASCS/ERS

1. **[1]**  Crear un recurso de IP virtual y un sondeo de estado de equilibrador de carga interno de Hola

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Asegúrese de que el estado del clúster hello es correcto y que se hayan iniciado todos los recursos. No es importante en qué recursos de Hola de nodo se están ejecutando.

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. **[1]** Instale SAP NetWeaver ASCS  

   Instalar ASCS de SAP NetWeaver como raíz en el primer nodo de hello mediante un nombre de host virtual que se asigna la dirección IP de toohello de configuración de front-end de equilibrador de carga de Hola para hello ASCS por ejemplo <b>nws ascs</b>, <b>10.0.0.10</b>y número de instancia de Hola que usó para la sonda de Hola Hola de equilibrador de carga por ejemplo <b>00</b>.

   Puede usar hello sapinst parámetro SAPINST_REMOTE_ACCESS_USER tooallow una toosapinst tooconnect de usuario no es de raíz.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. **[1]**  Crear un recurso de IP virtual y un sondeo de estado de equilibrador de carga interno de Hola

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   Asegúrese de que el estado del clúster hello es correcto y que se hayan iniciado todos los recursos. No es importante en qué recursos de Hola de nodo se están ejecutando.

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. **[2]** Instale SAP NetWeaver ERS  

   Instalar ERS de SAP NetWeaver como raíz en el segundo nodo de hello mediante un nombre de host virtual que se asigna la dirección IP de toohello de configuración de front-end de equilibrador de carga de Hola para hello ERS por ejemplo <b>nws ers</b>, <b>10.0.0.11</b> y el número de instancia de Hola que usó para la sonda de Hola Hola de equilibrador de carga por ejemplo <b>02</b>.

   Puede usar hello sapinst parámetro SAPINST_REMOTE_ACCESS_USER tooallow una toosapinst tooconnect de usuario no es de raíz.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > Use SWPM SP 20 PL 05 o superior. Las versiones inferiores no establece permisos de hello correctamente y se producirá un error en la instalación de Hola.
   > 

1. **[1]**  Adaptar Hola ASCS/SCS y ERS instancia perfiles
 
   * Perfil ASCS/SCS

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * Perfil ERS

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. **[A]** Configure la conexión persistente

   la comunicación entre el servidor de aplicaciones de SAP NetWeaver de Hola y Hola ASCS/SCS Hola se enruta a través de un equilibrador de carga de software. equilibrador de carga de Hello desconecta las conexiones inactivas tras un tiempo de espera configurable. tooprevent esto necesita tooset un parámetro en el perfil de SAP NetWeaver ASCS/SCS de Hola y cambiar la configuración de sistema de Linux Hola. Consulte la [nota de SAP 1410736][1410736] para más información.
   
   Hola ASCS/SCS perfil parámetro enque/encni/set_so_keepalive ya se agregó en el último paso de Hola.

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. **[A]**  Configurar usuarios SAP de hello después de la instalación de Hola
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. **[1]**  Agregar ASCS y SAP ERS servicios toohello sapservice archivo hello

   Agregar nodo de segundo de hello ASCS servicio entry toohello y copia Hola ERS servicio entrada toohello primer nodo.

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. **[1]**  Crear recursos de clúster de hello SAP

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   Asegúrese de que el estado del clúster hello es correcto y que se hayan iniciado todos los recursos. No es importante en qué recursos de Hola de nodo se están ejecutando.

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

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

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Crear dispositivos de hello STONITH

Después de editar permisos de Hola para las máquinas virtuales de hello, puede configurar dispositivos STONITH hello en clúster de Hola.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Habilitar el uso de Hola de un dispositivo STONITH

Habilitar el uso de Hola de un dispositivo STONITH

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a>Instalar la base de datos

En este ejemplo, hay una replicación del sistema SAP HANA instalada y configurada. SAP HANA se ejecutará en el mismo clúster según hello ASCS/SCS de SAP NetWeaver y ERS de Hola. También puede instalar SAP HANA en un clúster dedicado. Consulte [Alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure][sap-hana-ha] para más información.

### <a name="prepare-for-sap-hana-installation"></a>Preparación de la instalación de SAP HANA

Por lo general, se recomienda usar LVM para volúmenes de almacén de datos y archivos de registro. Para realizar pruebas, también puede elegir los archivos de registro y datos de hello toostore directamente en un disco sin formato.

1. **[A]** LVM  
   ejemplo de Hola siguiente supone que máquinas virtuales de hello tiene cuatro discos de datos conectados que se deben toocreate usa dos volúmenes.
   
   Crear volúmenes físicos de todos los discos que desea toouse.
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   Crear un grupo de volúmenes para los archivos de datos de hello, un grupo de volúmenes para los archivos de registro de hello y otro para el directorio compartido de Hola de SAP HANA
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   Crear volúmenes lógicos de Hola
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   Crear los directorios de montaje de Hola y copiar Hola UUID de todos los volúmenes lógicos
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   Crear las entradas de autofs de hello tres volúmenes lógicos
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   Inserte esta línea toosudo vi /etc/auto.direct
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   Montar volúmenes nuevos Hola
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. **[A]** Discos sin formatos  

   Para sistemas pequeños o de demostración, puede colocar los archivos de datos y de registro HANA en un disco. Hello siguientes comandos crean una partición en /dev/sdc y dele formato con xfs.
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   Insertar este too/etc/auto.direct línea
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   Crear el directorio de destino de Hola y montar el disco de Hola.
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a>Instalación de SAP HANA

Hello pasos siguientes se basan capítulo 4 de hello [Guía de SAP HANA SR rendimiento optimizado escenario] [ suse-hana-ha-guide] tooinstall replicación del sistema de SAP HANA. Por favor, lea antes de continuar la instalación de Hola.

1. **[A]**  Ejecutar hdblcm desde Hola HANA DVD
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. **[A]** Actualice el agente de host de SAP

   Descargue el archivo de agente de Host de SAP más reciente de Hola de hello [SAP Softwarecenter] [ sap-swcenter] y ejecución hello siguientes comando tooupgrade Hola agente. Reemplace Hola ruta de acceso toohello toopoint toohello archivo que descargó.
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. **[1]** Cree la replicación de HANA (como raíz)  

   Ejecutar el siguiente comando de Hola. Asegúrese de que tooreplace negrita cadenas (HDB de Id. de sistema de archivos de HANA y número de instancia 03) con valores de hello de la instalación de SAP HANA.
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. **[A]** Cree la entrada de almacén de claves (como raíz)

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. **[1]** Realice la copia de seguridad de la base de datos (como raíz)

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. **[1]**  Cambiar de usuario de toohello HANA sapsid y crear el sitio primario de Hola.

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. **[2]**  Cambiar de usuario de toohello HANA sapsid y crear sitio secundario de Hola.

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. **[1]** Creación de recursos de clúster de SAP HANA

   En primer lugar, cree la topología de Hola.
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   A continuación, cree Hola recursos HANA
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Asegúrese de que el estado del clúster hello es correcto y que se hayan iniciado todos los recursos. No es importante en qué recursos de Hola de nodo se están ejecutando.

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. **[1]**  Instancia de base de datos de SAP NetWeaver de Hola de instalación

   Instancia de base de datos de SAP NetWeaver instalación hello como raíz con un nombre de host virtual que se asigna como dirección IP de toohello de configuración de front-end de equilibrador de carga de Hola para base de datos de hello <b>nws db</b> y <b>10.0.0.12</b>.

   Puede usar hello sapinst parámetro SAPINST_REMOTE_ACCESS_USER tooallow una toosapinst tooconnect de usuario no es de raíz.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a>Instalación del servidor de aplicaciones de SAP NetWeaver

Siga estos tooinstall pasos un servidor de aplicaciones de SAP. Hola pasos siguientes se supone que instalar servidores HANA y servidor de aplicaciones de hello en un servidor distinto de hello ASCS/SCS. En caso contrario, no son necesarios algunos pasos de hello debajo (por ejemplo, configurar la resolución de nombres de host).

1. Configure la resolución de nombres de host    
   Puede usar un servidor DNS o modificar Hola/etc/hosts en todos los nodos. Este ejemplo muestra cómo toouse Hola archivo/etc/hosts.
   Reemplace la dirección IP de Hola y el nombre de host de Hola Hola siga los comandos
   ```bash
   sudo vi /etc/hosts
   ```
   Insertar Hola después líneas demasiado/etcetera/hosts. Cambiar toomatch de dirección y el nombre de host IP hello en el entorno    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. Crear el directorio de hello sapmnt

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. Configure autofs
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Cree un nuevo archivo con

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   Reinicie nuevos recursos compartidos autofs toomount Hola

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. Configure el archivo de intercambio
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Reiniciar Hola agente tooactivate Hola cambios

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. Instale el servidor de aplicaciones de SAP NetWeaver

   Instale un servidor de aplicaciones de SAP NetWeaver principal o adicional.

   Puede usar hello sapinst parámetro SAPINST_REMOTE_ACCESS_USER tooallow una toosapinst tooconnect de usuario no es de raíz.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. Actualice el almacenamiento seguro de SAP HANA

   Hola de actualización segura de SAP HANA almacenar toopoint toohello nombre virtual del programa de instalación de replicación del sistema de SAP HANA Hola.
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a>Pasos siguientes
* [Planeación e implementación de Azure Virtual Machines para SAP][planning-guide]
* [Implementación de Azure Virtual Machines para SAP][deployment-guide]
* [Implementación de DBMS de Azure Virtual Machines para SAP][dbms-guide]
* toolearn tooestablish alta disponibilidad y el plan de recuperación ante desastres de SAP HANA en Azure (instancias grandes), vea [SAP HANA (instancias de gran tamaño) alta disponibilidad y recuperación ante desastres en Azure](hana-overview-high-availability-disaster-recovery.md).
* toolearn tooestablish alta disponibilidad y el plan de recuperación ante desastres de SAP HANA en máquinas virtuales de Azure, vea [disponibilidad alta de SAP HANA en máquinas virtuales de Azure (VM)][sap-hana-ha]
