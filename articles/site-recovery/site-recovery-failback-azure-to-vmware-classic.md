---
title: "aaaFail realizar la copia de máquinas virtuales de VMware desde Azure en el portal clásico de hello | Documentos de Microsoft"
description: "Obtenga información sobre errores toohello atrás al sitio local después de la conmutación por error de máquinas virtuales de VMware y servidores físicos tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 7ca86e21-7a5d-45ab-8f4b-e42da90f199a
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 80bc3ab2708a5df953c6532b353da19a4c44ac34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site-classic-portal"></a>Frente a errores atrás máquinas virtuales de VMware y el sitio local de toohello servidores físicos (portal clásico)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-failback-azure-to-vmware.md)
> * [Portal de Azure clásico](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portal de Azure clásico (heredado)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Este artículo se describe cómo realizar toofail copia máquinas virtuales de Azure desde el sitio de Azure toohello local. Siga las instrucciones de hello en este artículo cuando estés listo toofail realizar copia sus máquinas virtuales de VMware o servidores físicos de Windows/Linux después de que han conmutado de hello local sitio tooAzure mediante este [tutorial](site-recovery-vmware-to-azure-classic.md).

## <a name="overview"></a>Información general
Este diagrama muestra la arquitectura de conmutación por recuperación de Hola para este escenario.

Esta arquitectura debe utilizarse cuando el servidor de procesos de hello es local y usa una ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Esta arquitectura debe utilizarse al servidor de procesos de hello es en Azure y tenga una VPN o una conexión ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

lista completa de hello toosee de puertos y diagrama de arquitectura de conmutación por recuperación de hello hacen referencia a imagen toohello siguiente

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Así es cómo funciona la conmutación por recuperación:

* Una vez haya conmutado tooAzure, se produce un error al sitio local tooyour back-algunas fases:
  * **Fase 1**: proteger máquinas virtuales de Azure de Hola para que inicien replicar máquinas virtuales de atrás tooVMware ejecutando en el sitio local. Habilitar solo mueve Hola VM a un grupo de protección de conmutación por recuperación que se creó automáticamente al crear grupo de protección de conmutación por error de Hola. Si agrega el plan de recuperación de conmutación por error protección grupo tooa grupo de protección de conmutación por recuperación de Hola se agregó también automáticamente toohello plan.  Durante la reprotección especifica cómo hacer copia de tooplan toofail.
  * **Fase 2**: después de que las máquinas virtuales de Azure se replican tooyour al sitio local, ejecutar un error en toofail de Azure.
  * **Fase 3**: cuando se produzca error volver los datos, proteger Hola máquinas virtuales locales que no pudo volver a para que se inicie replicar tooAzure.


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-toohello-original-or-alternate-location"></a>Conmutación por recuperación toohello original o en uno alternativa ubicación
Si produce un error en una VM VMware puede producir un error toohello atrás el mismo origen de máquina virtual si todavía existe en local. En este escenario sólo los cambios de delta de Hola se por error nuevo. Observe lo siguiente:

* Si conmutado servidores físicos, a continuación, conmutación por recuperación siempre es tooa nueva VM de VMware.
  * Antes de conmutar por recuperación una máquina física, tenga en cuenta lo siguiente:
  * Máquina física protegida se devolverán como una máquina Virtual cuando la conmutación por error desde Azure tooVMware
  * Asegúrese de que detectar al menos un servidor de destino maestro junto con toowhich de hosts ESX/ESXi necesario Hola necesita toofailback.
* Si no se vuelve toohello original VM Hola se necesita:

  * Si hello máquina virtual administrado por un servidor vCenter host ESX del destino de hello maestro debe tener el almacén de datos de access toohello máquinas virtuales.
  * Si está en un host ESX hello VM pero no está administrada por vCenter disco de duro Hola de hello VM debe ser en un almacén de datos accesible por host Hola del MT.
  * Si la máquina virtual está en un host ESX y no usa vCenter debe completar la detección de host ESX Hola de hello MT antes de que vuelva a proteger. Lo mismo se aplica si también conmuta por recuperación a servidores físicos.
  * Otra opción (si Hola local existe VM) es toodelete, antes de realizar una conmutación por recuperación. A continuación, conmutación por recuperación, a continuación, creará una nueva máquina virtual en el mismo host como host ESX de destino maestro Hola de Hola.
* Cuando datos de saludo de ubicación alternativa de conmutación por recuperación tooan estará toohello recuperada mismo hello y almacén de datos mismo host ESX usada por el servidor de destino maestro local Hola.

## <a name="prerequisites"></a>Requisitos previos
* Necesitará un entorno de VMware en la copia de la orden toofail máquinas virtuales de VMware y servidores físicos. Errores de back-tooa servidor físico no es compatible.
* En orden toofail atrás debe ha creado una red de Azure cuando configura inicialmente la protección. Conmutación por recuperación necesita una conexión VPN o ExpressRoute de hello Azure red en el que Hola máquinas virtuales de Azure son toohello encuentra un sitio local.
* Si las máquinas virtuales de hello desea toofail tooare atrás administrado por un servidor de vCenter necesitará toomake que tengan permisos de hello necesario para la detección de máquinas virtuales en servidores vCenter. [Más información](site-recovery-vmware-to-azure-classic.md).
* Si existen instantáneas en una máquina virtual, la reprotección dará error. Puede eliminar las instantáneas de Hola o discos de Hola.
* Antes de realizar conmutación por necesitará toocreate una serie de componentes:
  * **Cree un servidor de procesos en Azure**. Se trata de una máquina virtual de Azure que deberá toocreate y continuar la ejecución durante la conmutación por recuperación. Puede eliminar la máquina de hello una vez completada la conmutación por recuperación.
  * **Crear un servidor de destino maestro**: servidor de destino maestro Hola envía y recibe datos de conmutación por recuperación. servidor de administración de Hello creada de forma local tiene un servidor de destino maestro que se instala de forma predeterminada. Sin embargo, según volumen Hola de tráfico de back-error deberá toocreate un servidor de destino maestro independiente de conmutación por recuperación.
  * Si desea toocreate en un servidor de destino maestro adicionales que se ejecutan en Linux, deberá tooset una VM de Linux Hola antes de instalar el servidor de destino maestro de hello, tal y como se describe a continuación.
* El servidor de configuración es necesario localmente cuando realiza una conmutación por recuperación. Durante la conmutación por recuperación, máquina virtual de hello debe existir en hello configuración base de datos, un error que conmutación por recuperación no sea correcta. Por lo tanto, asegúrese de realizar una copia de seguridad programada periódica del servidor. En caso de un desastre, necesitará toorestore con hello misma dirección IP para que la conmutación por recuperación funcione.

## <a name="set-up-hello-process-server-in-azure"></a>Configurar el servidor de procesos de hello en Azure
Tendrá que tooinstall un servidor de proceso de Azure para que Hola máquinas virtuales de Azure puede enviar el servidor de destino maestro local tooon atrás de hello datos.

1. En el portal de Site Recovery hello > **servidores de configuración** seleccione tooadd un nuevo servidor de procesos.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. Especifique un nombre de servidor de procesos y escriba un nombre y una contraseña que usará tooconnect toohello máquina virtual de Azure como administrador. En **servidor de configuración** Seleccionar servidor de administración local de Hola y especificar hello Azure red qué Hola se debe implementar el servidor de procesos. Debe tratarse de red de hello en el que se encuentran las máquinas virtuales de Azure de Hola. Especifique una dirección IP única de subred seleccione hello y comenzar la implementación.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   Se desencadenará un servidor de procesos de trabajo toodeploy Hola

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Después de hello servidor de proceso se implementa en Azure puede iniciar sesión con credenciales de Hola que especificó. Hello primera vez que inicie sesión en el cuadro de diálogo del servidor de proceso de Hola se ejecutará. Tipo de dirección IP de Hola Hola local del servidor de administración y su frase de contraseña. Deje la configuración predeterminada del puerto 443 de Hola. También puede dejar hello 9443 número de puerto para la replicación de datos a menos que modifique específicamente esta configuración al configurar el servidor de administración local de Hola.

   > [!NOTE]
   > no será visible en el servidor de Hello **propiedades de la máquina virtual**. Solo es visible en hello **servidores** ficha toowhich de servidor de administración de Hola se ha registrado. Puede tardar acerca de 10 a 15 minutos para tooappear de servidor de proceso de Hola.
   >
   >

## <a name="set-up-hello-master-target-server-on-premises"></a>Configurar Hola destino maestro servidor local
servidor de destino maestro Hola recibe datos de conmutación por recuperación de saludo. Un servidor de destino maestro se instala automáticamente en el servidor de administración local de hello pero si está errores volver una gran cantidad de datos que tenga tooset de un servidor de destino maestro adicionales. Para ello, realice lo siguiente:

> [!NOTE]
> Si desea tooinstall un servidor de destino maestro en Linux, siga las instrucciones de hello en el procedimiento siguiente Hola.
>
>

1. Si está instalando el servidor de destino maestro de hello en Windows, abra la página de inicio rápido de Hola de máquina virtual en el que está instalando el servidor de destino maestro de Hola y descargar archivo de instalación de hello para el Asistente para configuración de Azure Site Recovery unificado de Hola de Hola.
2. Ejecute el programa de instalación y en **antes de comenzar** seleccione **agregar tooscale de servidores de proceso adicionales horizontalmente la implementación**.
3. Asistente de hello completa en hello misma manera que cuando se [configurar el servidor de administración de hello](site-recovery-vmware-to-azure-classic.md). En hello **detalles del servidor de configuración** página, especifique la dirección IP de Hola de este servidor de destino maestro y un saludo de tooaccess VM de frase de contraseña.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Configurar una VM de Linux como servidor de destino maestro de Hola
sistema operativo mínimo a tooset de servidor de administración de hello ejecutando el servidor de destino maestro de Hola como una máquina virtual, deberá tooinstall Hola ciento Linux) S 6.6, recuperar los Id. de SCSI de Hola para todos los discos duros SCSI, instalar algunos paquetes adicionales y aplicar algunos cambios personalizados.

#### <a name="install-centos-66"></a>Instalación de CentOS 6.6
1. Instalar sistema operativo mínimo de hello CentOS 6.6 en máquina virtual del servidor de administración de Hola. Tenga Hola ISO en un sistema de Hola de arranque y la unidad de DVD. Omitir Hola medios pruebas, seleccione inglés de Estados Unidos en lenguaje de hello, seleccione **básica de los dispositivos de almacenamiento**, compruebe que Hola unidad de disco duro no tiene ningún dato importante y haga clic en **Sí**, descartar los datos. Escriba nombre de host de Hola Hola del servidor de administración y seleccione el adaptador de red del servidor de Hola.  Hola **sistema de edición** cuadro de diálogo Seleccione ** conectarse automáticamente ** y agregue una dirección IP estática, la red y la configuración DNS. Especifique una zona horaria y un servidor de administración raíz contraseña tooaccess Hola.
2. Cuando se pregunte tipo hello de instalación que desea que seleccione **crear diseño personalizado** como partición de Hola. Tras hacer clic en **Siguiente** select **Gratis** y haga clic en Crear. Cree **/**,  **/var/crash** y **/home partitions** con **FS Type:** **ext4**. Crear la partición de intercambio de hello como **FS tipo: intercambio**.
3. Si se encuentran dispositivos ya existentes, aparecerá un mensaje de advertencia. Haga clic en **formato** unidad de hello tooformat con valores de la partición de Hola. Haga clic en **escritura cambiar toodisk** cambios en las particiones tooapply Hola.
4. Seleccione **cargador de arranque de instalación** > **siguiente** tooinstall cargador de arranque de hello en la partición raíz Hola.
5. Cuando la instalación se haya completado, haga clic en **Reiniciar**.

#### <a name="retrieve-hello-scsi-ids"></a>Recuperar los Id. de SCSI de Hola
1. Después de la instalación recuperar los Id. de SCSI de Hola para cada disco duro SCSI Hola máquina virtual. toodo esto apagar máquina virtual del servidor de administración de hello, en hello VM propiedades en VMware, haga clic en la entrada de la máquina virtual de hello > **modificar configuración** > **opciones**.
2. Seleccione **Avanzadas** > **General item** (Elemento general) y haga clic en **Configuration Parameters** (Parámetros de configuración). Esta opción estará de-active cuando Hola máquina se está ejecutando. toomake TI máquina Hola active debe cerrarse.
3. Si hello fila **disco. EnableUUID** existe Asegúrese de que el valor de Hola se establece demasiado**True** (con distinción entre mayúsculas y minúsculas). Si ya no se puede cancelar y probar el comando de SCSI de hello dentro de un sistema operativo invitado después de arrancar.
4. Si no existente haga clic en la fila de hello **Agregar fila** – y agregue con hello **True** valor. No utilice comillas dobles.

#### <a name="install-additional-packages"></a>Instalación de paquetes adicionales
Podrá necesita toodownload e instalar algunos paquetes adicionales.

1. Asegúrese de que servidor de destino maestro hello es toohello conectado internet.
2. Ejecutar este toodownload de comandos e instalar 15 paquetes del repositorio de CentOS hello: **# yum instalar – y xfsprogs perl lsscsi rsync wget kexec-tools**.
3. Si se ejecutan Hola máquinas de origen que va a proteger Linux wit Reiser XFS filesystem de raíz de Hola o dispositivo de arranque, a continuación, debe descargar e instalar paquetes adicionales como se indica a continuación:

   * # <a name="cd-usrlocal"></a># cd /usr/local
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>Aplicación de cambios personalizados
Realice Hola después cambios personalizados tooapply cuando se haya pasos posteriores a la instalación de hello completa y paquetes de saludo instalados:

1. Copie Hola RHEL 6-64 unificado agente binario toohello máquina virtual. Ejecute este comando toountar hello binario: **tar – zxvf<file name>**
2. Ejecutar permisos de toogive este comando: **# chmod 755./ApplyCustomChanges.sh**
3. Ejecutar script de Hola: **./ApplyCustomChanges.sh #**. Solo debería ejecutar script de Hola una vez. Reinicie el servidor de hello después de ejecutar script de Hola correctamente.

## <a name="run-hello-failback"></a>Ejecute hello conmutación por recuperación
### <a name="reprotect-hello-azure-vms"></a>Vuelva a proteger máquinas virtuales de Azure de Hola
1. En el portal de Site Recovery hello > **máquinas** Hola máquina virtual que se ha conmutado por error de ficha, seleccione y haga clic en **volver a proteger**.
2. En **servidor de destino maestro** y **servidor de procesos** seleccione servidor de destino maestro local de Hola y el servidor de proceso de máquina virtual de Azure de Hola.
3. Seleccione la cuenta de hello configurado para la conexión toohello máquina virtual.
4. Seleccione la versión de la conmutación por recuperación de Hola Hola del grupo de protección. Por ejemplo, si está protegido Hola VM en PG1, deberá tooselect PG1_Failback.
5. Si desea que la ubicación alternativa de toorecover tooan, seleccione unidad de retención de Hola y almacén de datos configurado para el servidor de destino maestro Hola. Cuando se produce un error toohello atrás local sitio Hola máquinas virtuales VMware plan de protección de conmutación por recuperación de hello usará Hola mismo almacén de datos como servidor de destino maestro Hola. Si desea que toorecover Hola réplica Azure VM toohello mismo local máquina virtual, máquina virtual ya debe de local de Hola se Hola mismo almacén de datos como Hola maestro servidor de destino. Si no hay ninguna máquina virtual local, se creará una nueva durante la reprotección.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. Tras hacer clic en **Aceptar** toobegin solo un trabajo comienza tooreplicate Hola VM desde el sitio de Azure toohello local. Puede realizar el seguimiento del progreso de hello en hello **trabajos** ficha.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-toohello-on-premises-site"></a>Ejecutar un sitio local de toohello de conmutación por error
Después de hello conmutada VM es la versión de la conmutación por recuperación de toohello ha movido de su grupo de protección y se agrega automáticamente el plan de recuperación de toohello destinadas hello tooAzure de conmutación por error, si hay alguno.

1. Hola **planes de recuperación** plan de recuperación de página Hola select que contiene grupo de conmutación por recuperación de Hola y haga clic en **conmutación por error** > **conmutación por error imprevista**.
2. En **confirmar conmutación por error** Compruebe la dirección de conmutación por error de hello (tooAzure) y seleccione el punto de recuperación de Hola que desee toouse para conmutación por error hello (más reciente). Si habilitó **varias VM** al configurar las propiedades de replicación puede recuperar la aplicación más reciente de toohello o punto de recuperación coherente para bloqueos. Haga clic en hello marca de verificación toostart Hola conmutación por error.
3. Durante la conmutación por error se apagará Hola máquinas virtuales de Azure Site Recovery. Después de comprobar que conmutación por recuperación se ha completado tal y como se esperaba que el usuario puede puede comprobar que Hola máquinas virtuales de Azure que se haya cerrado según lo previsto.

### <a name="reprotect-hello--on-premises-site"></a>Sitio local de hello, vuelva a proteger
Una vez completada la conmutación por recuperación los datos estarán en el sitio local de Hola, pero no estará protegidos. toostart replicación tooAzure nuevo Hola siguientes:

1. En el portal de Site Recovery hello > **máquinas** pestaña máquinas virtuales de hello select que no se han podido volver y haga clic en **volver a proteger**.
2. Después de comprobar que tooAzure de replicación está funcionando según lo previsto, en Azure puede eliminar Hola máquinas virtuales de Azure (actualmente no se ejecuta) que se recuperarán tras los errores.

### <a name="common-issues-in-failback"></a>Problemas comunes en la conmutación por recuperación
1. Si realiza la detección de usuarios de solo lectura de vCenter y protege las máquinas virtuales, se ejecutará correctamente y la conmutación por error funcionará. En tiempo de Hola de Reprotección, fallará porque no se pueden detectar Hola almacenes de datos. Como un síntoma no verá los almacenes de datos de hello aparece al volver a proteger. tooresolve esto, puede actualizar la credencial de vCenter Hola con la cuenta adecuada que tenga permisos y vuelva a intentar el trabajo de Hola. [Más información](site-recovery-vmware-to-azure-classic.md)
2. Cuando conmutación una VM de Linux y lo ejecuta en local, verá ese paquete del Administrador de red de Hola se desinstala del equipo de Hola. Esto es porque cuando se recupera la Hola VM en Azure, se quita el paquete del Administrador de red de Hola.
3. Cuando una máquina virtual se configura con la dirección IP estática y se ha conmutado tooAzure, dirección IP de Hola se adquiere a través de DHCP. Cuando la conmutación por error local tooOn atrás, Hola VM continúa dirección IP de toouse DHCP tooacquire Hola. Necesitará toomanually inicio de sesión en la máquina de Hola y establecer la dirección IP Hola realizar copia de tooStatic dirección si es necesario.
4. Si utiliza las ediciones gratuitas de ESXi 5.5 o vSphere Hypervisor 6, la conmutación por error se llevará a cabo correctamente, pero la conmutación por recuperación, no. Se conmutará a ned tooupgrade tooeither licencia de evaluación tooenable.

## <a name="failing-back-with-expressroute"></a>Conmutación por recuperación con ExpressRoute
Puede conmutar por recuperación a través de una conexión VPN o de Azure ExpressRoute. Si desea que toouse ExpressRoute Nota Hola a continuación:

* ExpressRoute se debe configurar en hello red virtual de Azure toowhich origen máquinas producirá un error en y en que las máquinas virtuales de Azure se encuentran después de producirse la conmutación por error de Hola.
* Los datos están replicado tooan cuenta de almacenamiento de Azure en un punto de conexión público. Debe configurar el emparejamiento público en ExpressRoute con el centro de datos de destino de Hola para replicación de Site Recovery toouse ExpressRoute.
