---
title: "aaaFailback máquinas virtuales de VMware desde Azure tooon-local | Documentos de Microsoft"
description: "Obtenga información sobre errores toohello atrás al sitio local después de la conmutación por error de máquinas virtuales de VMware y servidores físicos tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>Frente a errores atrás máquinas virtuales de VMware y el sitio local de servidores físicos toohello


Este artículo se describe cómo toofailback Azure máquinas virtuales desde el sitio de Azure toohello local. Siga las instrucciones de hello aquí cuando esté listo toofail realizar copias de sus máquinas virtuales de VMware o servidores físicos de Windows o Linux después de haber protegido volver a las máquinas con este [referencia](site-recovery-how-to-reprotect.md).

>[!NOTE]
>Si usas el portal de Azure clásico hello, consulte tooinstructions mencionado [aquí](site-recovery-failback-azure-to-vmware-classic.md) de arquitectura de tooAzure mejorada de VMware y [aquí](site-recovery-failback-azure-to-vmware-classic-legacy.md) para arquitectura de hello heredado

## <a name="overview"></a>Información general
diagramas de Hello en esta sección muestran la arquitectura de conmutación por recuperación de Hola para este escenario.

Cuando Hola servidor de procesos es local y se usa una conexión de ExpressRoute de Azure, use esta arquitectura:

![Diagrama de la arquitectura de ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Cuando hello es el servidor de procesos en Azure y tienen una VPN o una conexión ExpressRoute, use esta arquitectura:

![Diagrama de la arquitectura de VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Para obtener una lista completa de puertos y diagrama de arquitectura de conmutación por recuperación de hello, consulte toohello siguiente imagen:

![Lista de conmutación por error/recuperación de todos los puertos](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Después de que ha conmutado tooAzure, se producirá un error en sitio local de tooyour atrás en tres fases:

* **Fase 1**: proteger máquinas virtuales de Azure de Hola para que inicien replicar máquinas virtuales de VMware toohello espera que se ejecutan en el sitio local.
* **Fase 2**: una vez que las máquinas virtuales de Azure se tooyour replicados al sitio local, ejecutar una conmutación por error toofail copia de Azure.
* **Fase 3**: cuando se produzca error volver los datos, proteger Hola máquinas virtuales locales que no pudo volver a para que se inicie replicar tooAzure.

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>Generar un error toohello atrás de ubicación original o una ubicación alternativa
Después de conmutar una VM de VMware, puede producir un error toohello atrás el mismo origen de máquina virtual si todavía existe en local. En este escenario, solo los deltas de Hola se recuperarán tras los errores.

Si produce un error a través de servidores físicos, la conmutación por recuperación siempre es tooa nueva VM de VMware. Antes de conmutar por recuperación una máquina física, tenga en cuenta lo siguiente:
* Una máquina física protegida se devolverán como una máquina virtual cuando se conmuta de tooVMware de Azure. Una máquina física de Windows Server 2008 R2 SP1, si está protegido y conmutado por error tooAzure, no se recuperarán tras los errores. Una máquina de Windows Server 2008 R2 SP1 que se inició como una máquina virtual local será capaz de toofail back.
* Asegúrese de que detectar al menos un servidor de destino maestro junto con hello hosts ESX/ESXi necesarios que necesita toofail nuevo a.

Si se produce un error toohello atrás de la VM original, se necesita la siguiente de hello:

* Si hello máquina virtual está administrada por un servidor vCenter, hello ESX host del destino maestro debe tener el almacén de datos de access toohello máquinas virtuales.
* Si hello VM está en un host ESX, pero no está administrada por vCenter, disco duro de Hola de hello VM debe ser en un almacén de datos que sea accesible desde el host de hello del MT.
* Si la máquina virtual está en un host ESX y no usa vCenter, debería completar la detección de host ESX Hola de hello MT antes de que vuelva a proteger. Lo mismo se aplica si también conmuta por recuperación a servidores físicos.
* Otra opción (si Hola local existe VM) es toodelete, antes de realizar una conmutación por recuperación. Conmutación por recuperación, a continuación, crea una nueva máquina virtual en mismo host como host ESX de destino maestro Hola de Hola.

Cuando se produce un error de ubicación alternativa tooan atrás, datos de hello están toohello recuperada mismo hello y almacén de datos mismo host ESX usada por el servidor de destino maestro local Hola.

## <a name="prerequisites"></a>Requisitos previos
* toofail back máquinas virtuales de VMware y servidores físicos, necesita un entorno de VMware. Errores de back-tooa servidor físico no es compatible.
* toofail nuevo, debe haber creado una red de Azure cuando configura inicialmente la protección. Conmutación por recuperación necesita una conexión VPN o ExpressRoute de hello Azure red en el que Hola máquinas virtuales de Azure son toohello encuentra un sitio local.
* Si hello las máquinas virtuales que desea toofail copias tooare administrado por un servidor vCenter, asegúrese de que dispone de permisos de hello necesario para la detección de máquinas virtuales en servidores vCenter. Para obtener más información, consulte [tooAzure de servidores físicos con Azure Site Recovery y de máquinas virtuales de VMware replicar](site-recovery-vmware-to-azure-classic.md).
* Si existen instantáneas en una máquina virtual, la reprotección dará error. Puede eliminar las instantáneas de Hola o discos de Hola.
* Antes de realizar conmutación por recuperación, cree estos componentes:
  * **Cree un servidor de procesos en Azure**. Este componente es una máquina virtual de Azure que creará y mantendrá en ejecución durante la conmutación por recuperación. Puede eliminar Hola VM una vez completada la conmutación por recuperación.
  * **Crear un servidor de destino maestro**: servidor de destino maestro Hola envía y recibe datos de conmutación por recuperación. servidor de administración de Hola que había creada de forma local tiene un servidor de destino maestro que se instala de forma predeterminada. Sin embargo, según volumen Hola de tráfico de conmutar por recuperación, deberá toocreate un servidor de destino maestro independiente de conmutación por recuperación.
  * toocreate un servidor de destino maestro adicional que se ejecuta en Linux, configure Hola Linux VM antes de instalar el servidor de destino maestro de hello, tal y como se describe más adelante.
* El servidor de configuración es necesario localmente cuando realiza una conmutación por recuperación. Durante la conmutación por recuperación, máquina virtual de hello debe existir en la base de datos del servidor de configuración de Hola. Si la base de datos del servidor de configuración de hello no contiene ninguna máquina virtual, no se puede realizar la conmutación por recuperación. Por lo tanto, asegúrese de realizar copias de seguridad programadas periódicas del servidor. En un desastre, debe toorestore con hello direcciones IP mismo funciona dicha conmutación por recuperación.
* Establecer configuración de hello disk.enableUUID=true en **parámetros de configuración** del maestro de Hola de máquina virtual de VMware de destino. Si la fila no existe, agréguela. Esta opción es tooprovide requiere un archivo de disco (VMDK) coherente de identificador único universal (UUID) toohello máquina virtual donde se montó correctamente.
* Tenga en cuenta un "maestro de servidor de destino no puede ser vMotioned de almacenamiento" condición, lo que puede producir hello toofail de conmutación por recuperación. Hola máquina virtual no puede iniciarse porque discos hello no se realizan tooit disponible.
* Agregar una unidad, llamada a una unidad de retención, en el servidor de destino maestro Hola. Agregue un disco y formatear la unidad de Hola.

## <a name="failback-policy"></a>Directiva de conmutación por recuperación
tooreplicate atrás tooon local, necesita una directiva de conmutación por recuperación. Directiva de Hola se crea automáticamente cuando se crea una directiva de dirección hacia delante y se asocia automáticamente con el servidor de configuración de Hola. Esta directiva no es editable Directiva de Hello tiene Hola después de la configuración de replicación:

* Umbral RPO = 15 minutos
* Retención de punto de recuperación = 24 horas
* Frecuencia de las instantáneas coherentes con la aplicación = 60 minutos

 ![Configuración de replicación de la directiva de conmutación por recuperación de Hola](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>Configuración de un servidor de procesos en Azure
Instale un servidor de proceso de Azure para que las máquinas virtuales de Azure de hello pueda enviar Hola datos atrás toohello local de servidor de destino maestro.

Si ha protegido las máquinas virtuales como recursos clásicos (es decir, hello recupera VM en Azure es una máquina virtual que se creó mediante el modelo de implementación clásica de hello), necesitará un servidor de proceso de Azure. Si se han recuperado hello las máquinas virtuales con Azure Resource Manager como tipo de implementación de hello, Hola servidor de proceso debe tener el Administrador de recursos como tipo de implementación de Hola. Hello tipo de implementación se selecciona por hello Azure red virtual que se implementa Hola servidor de procesos.

1. En **almacén** > **configuración** > **infraestructura de recuperación de sitios** (en **administrar**) > **Servidores de configuración** (en **para VMware y máquinas físicas**), seleccione servidor de configuración de Hola.
2. Haga clic en **Servidor de procesos**.

  ![Botón Servidor de procesos](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. Elija toodeploy Hola servidor de procesos como **implementar un servidor de procesos en Azure de conmutación por recuperación**.
4. Seleccione la suscripción de Hola que se han recuperado hello las máquinas virtuales a.
5. Seleccione Hola red de Azure que se han recuperado hello las máquinas virtuales a. Hola toobe de necesidades de servidor de procesos en hello que igual de red para que Hola recupera las máquinas virtuales y hello servidor de procesos se pueden comunicar.
6. Si ha seleccionado un *modelo de implementación clásica* de red, crear una máquina virtual a través de hello Azure Marketplace y después instalar Hola servidor de procesos en ella.

 ![ventana de "Agregar servidor de procesos" Hello](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 Tal y como se va a crear servidor de procesos de Hola, preste siguiente toohello de atención:
 * Hola nombre de imagen de hello es *recuperación de sitio de Microsoft Azure proceso servidor V2*. Seleccione **clásico** como modelo de implementación de Hola.

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * Hola servidor de proceso correspondiente toohello las instrucciones de instalación en [tooAzure de servidores físicos con Azure Site Recovery y de máquinas virtuales de VMware replicar](site-recovery-vmware-to-azure-classic.md).
7. Si selecciona hello *el Administrador de recursos* Azure de red, implementar Hola proceso servidor proporcionando Hola siguiente información:

  * nombre de Hola Hola del grupo de recursos que desea que el servidor hello toodeploy
  * nombre de saludo del servidor de Hola
  * Un nombre de usuario y una contraseña para iniciar sesión en el servidor de toohello
  * cuenta de almacenamiento de Hola que desea que el servidor hello toodeploy
  * subred de Hola y de interfaz de red de Hola que desea tooconnect tooit
   >[!NOTE]
   >Debe crear su propio [interfaz de red](../virtual-network/virtual-networks-multiple-nics.md) (NIC) y selecciónelo durante la implementación de servidor de procesos de Hola.

    ![Escriba información en el cuadro de diálogo "Agregar servidor de procesos" hello](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. Haga clic en **Aceptar**. Esta acción desencadena un trabajo que crea una máquina de virtual del tipo de implementación de administrador de recursos durante la instalación del servidor de procesos de Hola. tooregister hello toohello Configuración servidor, el programa de instalación de ejecución Hola dentro de Hola VM siguiendo las instrucciones de hello en [tooAzure de servidores físicos con Azure Site Recovery y de máquinas virtuales de VMware replicar](site-recovery-vmware-to-azure-classic.md). También se desencadena una Hola de toodeploy servidor de procesos de trabajo.

  Hello servidor de proceso aparece en hello **servidores de configuración** > **asociados servidores** > **servidores de procesos** ficha.

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > Hello servidor de procesos no está visible en **propiedades de la máquina virtual**. Está visible solo en hello **servidores** ficha en el servidor de administración de Hola que esté registrada en. Pueden tardar 10 minutos too15 hello tooappear de servidor de procesos.


## <a name="set-up-hello-master-target-server-on-premises"></a>Configurar Hola destino maestro servidor local
servidor de destino maestro Hola recibe datos de conmutación por recuperación de saludo. servidor Hola se instala automáticamente en el servidor de administración local de hello, pero si está fallando volver demasiados datos, tendrá que tooset de un servidor de destino maestro adicionales. tooset seguridad un patrón tienen como destino server local, Hola siguientes:

> [!NOTE]
> tooset un servidor de destino maestro en Linux, omitir el procedimiento siguiente toohello. Usar solo CentOS 6.6 sistema operativo mínimo como Hola SO de destino maestro.

1. Si está configurando el servidor de destino maestro de hello en Windows, abra la página de inicio rápido de Hola de máquina virtual que se está instalando el servidor de destino maestro Hola Hola.
2. Descargue el archivo de instalación de hello para el Asistente para configuración de Azure Site Recovery unificado de Hola.
3. Ejecute el programa de instalación de hello y, en **antes de comenzar**, seleccione **agregar tooscale de servidores de procesos adicional horizontalmente la implementación**.
4. Asistente de hello completa en hello misma manera que cuando se [configurar el servidor de administración de hello](site-recovery-vmware-to-azure-classic.md). En hello **detalles del servidor de configuración** página, especifique Hola dirección IP del servidor de destino maestro de Hola y escriba un Hola de tooaccess VM de frase de contraseña.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Configurar una VM de Linux como servidor de destino maestro de Hola
tooset de servidor de administración de hello ejecutando el servidor de destino maestro hello como una VM de Linux, instale Hola CentOS 6.6 mínima para el sistema operativo. A continuación, recuperar los Id. de SCSI de Hola para todos los discos duros SCSI, instalar algunos paquetes adicionales y aplicar algunos cambios personalizados.

#### <a name="install-centos-66"></a>Instalación de CentOS 6.6

1. Instalar sistema operativo mínimo de hello CentOS 6.6 en máquina virtual del servidor de administración de Hola. Mantener Hola ISO en una unidad de DVD y Hola sistema de arranque. Omitir la comprobación de medios de Hola. Seleccione **inglés de Estados Unidos** como lenguaje de hello, seleccione **básica de los dispositivos de almacenamiento**, compruebe que Hola unidad de disco duro no tiene ningún dato importante, haga clic en **Sí**y se eliminará cualquier dato. Escriba nombre de host de Hola Hola del servidor de administración y seleccione el adaptador de red del servidor de Hola.  Hola **sistema de edición** cuadro de diálogo, seleccione **conectarse automáticamente**y, a continuación, agregue una dirección IP estática, la red y la configuración DNS. Especifique una zona horaria. tooaccess Hola servidor de administración, escriba la contraseña de la raíz de Hola.
2. Cuando se le pregunte qué tipo de instalación que desea, seleccione **crear diseño personalizado** como partición de Hola. Haga clic en **Siguiente**. Seleccione **Libre** y, a continuación, haga clic en **Crear**. Cree **/**, **/var/crash** y **/home partitions** con **FS Type:** **ext4**. Crear la partición de intercambio de hello como **FS tipo: intercambio**.
3. Si se encuentran dispositivos ya existentes, aparecerá un mensaje de advertencia. Haga clic en **formato** unidad de hello tooformat con valores de la partición de Hola. Haga clic en **escritura cambiar toodisk** cambios en las particiones tooapply Hola.
4. Seleccione **cargador de arranque de instalación** > **siguiente** tooinstall cargador de arranque de hello en la partición raíz Hola.
5. Una vez completada la instalación de hello, haga clic en **reiniciar**.

#### <a name="retrieve-hello-scsi-ids"></a>Recuperar los Id. de SCSI de Hola

1. Después de la instalación de hello, recuperar los Id. de SCSI de Hola para cada disco duro SCSI Hola máquina virtual. toodo apaga por lo tanto, de la máquina virtual del servidor de administración de Hola. En Propiedades de máquina virtual de hello en VMware, haga clic en entrada de la máquina virtual de hello > **modificar configuración** > **opciones**.
2. Seleccione **Avanzadas** > **General item** (Elemento general) y haga clic en **Configuration Parameters** (Parámetros de configuración). Esta opción no está disponible cuando se está ejecutando la máquina de Hola. Para la opción de hello toobe disponible, debe cerrarse máquina Hola.
3. Realice una de las siguientes de hello:
 * Si hello fila **disco. EnableUUID** existe, asegúrese de que el valor de Hola se establece demasiado**True** (con distinción entre mayúsculas y minúsculas). Si el valor de Hola se ha establecido tooTrue, puede cancelar y probar el comando de SCSI de hello dentro de un sistema operativo invitado después de arrancar.
 * Si hello fila **disco. EnableUUID** no existe, haga clic en **Agregar fila**y, a continuación, agréguelo con hello **True** valor. No utilice comillas dobles.

#### <a name="install-additional-packages"></a>Instalación de paquetes adicionales
Descargue e instale los paquetes adicionales.

1. Asegúrese de que el servidor de destino maestro hello es toohello conectado Internet.
2. toodownload y 15 paquetes de instalación del repositorio de CentOS hello, ejecute este comando: `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`.
3. Si las máquinas de origen Hola protege ejecutan Linux con un Reiser o XFS filesystem para dispositivo de arranque o raíz de hello, descargue e instale paquetes adicionales como se indica a continuación:

   * \# cd /usr/local
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \#rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * \#wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \#rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm
   * \#yum instalar (tooenable necesario paquetes de múltiples rutas de acceso en el servidor de destino maestro de hello) de dispositivo asignador-múltiples rutas

#### <a name="apply-custom-changes"></a>Aplicación de cambios personalizados
Después de haber completado los pasos posteriores a la instalación de Hola y paquetes de saludo instalado, se aplican cambios personalizados haciendo Hola siguiente:

1. Copie Hola RHEL 6-64 unificado agente binario toohello máquina virtual. Hola de toountar binario, ejecute este comando: `tar –zxvf <file name>`.
2. permisos de toogive, ejecute este comando: `# chmod 755 ./ApplyCustomChanges.sh`.
3. Ejecución hello después de la secuencia de comandos: `# ./ApplyCustomChanges.sh`. Ejecútelo una sola vez. Una vez que se ejecuta correctamente, reinicie el servidor de Hola.

## <a name="run-hello-failback"></a>Ejecute hello conmutación por recuperación
### <a name="reprotect-hello-azure-vms"></a>Vuelva a proteger máquinas virtuales de Azure de Hola
1. En **almacén**, en **replican elementos**, haga clic en hello máquina virtual que ha se ha conmutado por error y, a continuación, seleccione **volver a proteger**.
2. En la hoja de hello, puede ver esa dirección Hola de protección **locales de tooOn Azure** ya está seleccionado.
3. En **servidor de destino maestro** y **servidor de proceso**, seleccione el servidor de destino maestro local de Hola y Hola servidor de proceso de máquina virtual de Azure.
4. Hola seleccione almacén de datos que desea que los discos de hello toorecover locales. Utilice esta opción cuando Hola local se elimina la máquina virtual y deberá toocreate nuevos discos. Omitir la opción de hello si hello discos ya existen, pero seguirá necesitando toospecify un valor.
5. Utilice una retención de unidad toostop Hola puntos en el tiempo cuando Hola VM es replicada local tooon back. A continuación se enumeran algunos criterios de una unidad de retención. Sin estos criterios, unidades de hello no se muestra para el servidor de destino maestro Hola.

  * El volumen no debe utilizarse para ningún otro propósito (destino de replicación, etc.).
  * El volumen no debe estar en modo de bloqueo.
  * El volumen no debe ser el volumen de memoria caché. (instalación de destino maestro hello no debe existir en el volumen. Hola servidor de proceso más master volumen de instalación personalizada de destino no es apto para el volumen de retención. En este caso, Hola instalado a servidor de procesos más volumen de destino maestro es el volumen de caché de hello del destino maestro de Hola.)
  * no debe ser el tipo de sistema de archivo de Hello volumen FAT y FAT32.
  * capacidad del volumen Hola debe ser distinto de cero.
  * volumen de retención predeterminado de Hola para Windows es R.
  * volumen de retención predeterminado de Hola para Linux es /mnt/retention.

6. Directiva de conmutación por recuperación de Hola se selecciona automáticamente.
7. Tras hacer clic en **Aceptar** toobegin conmutada, un trabajo comienza tooreplicate Hola VM desde el sitio de Azure toohello local. Puede realizar el seguimiento del progreso de hello en hello **trabajos** ficha.

Si desea que la ubicación alternativa de toorecover tooan, seleccione unidad de retención de Hola y almacén de datos que están configurados para el servidor de destino maestro Hola. Cuando se produce un error de sitio local de toohello atrás, Hola máquinas virtuales de VMware en el plan de protección de conmutación por recuperación de hello usar hello mismo almacén de datos como servidor de destino maestro Hola. Si desea que toorecover Hola réplica Azure VM toohello mismo local máquina virtual, máquina virtual debe ya estar en Hola igual a local de hello almacén de datos como servidor de destino maestro Hola. Si no hay ninguna máquina virtual local, se creará una nueva durante la reprotección.

![Seleccione "Tooon locales de Azure" en el menú desplegable de Hola](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

También puede volver a proteger a nivel de un plan de recuperación. Si tiene un grupo de replicación, este solo se puede volver a proteger con un plan de recuperación. Cuando vuelva a efectuar mediante el uso de un plan de recuperación, utilice los valores anteriores de hello en todos los equipos protegidos.

> [!NOTE]
> Grupos de replicación deben protegerse con hello mismo destino maestro. Si se han vuelto a proteger con servidores de destino maestro distintos, no se puede determinar un momento dado común para ellos.

### <a name="run-a-failover-toohello-on-premises-site"></a>Ejecutar un sitio local de toohello de conmutación por error
Después de que se vuelva a efectuar Hola VM, puede iniciar una conmutación por error de Azure tooon local.

1. En la página de los elementos replicados de hello, haga clic en la máquina virtual de hello y, a continuación, seleccione **conmutación por error imprevista**.
2. En **confirmar conmutación por error**, compruebe la dirección de conmutación por error de hello (de Azure) y, a continuación, seleccione el punto de recuperación de Hola que quiere toouse de conmutación por error de hello (Hola más reciente o punto de recuperación más reciente coherente con la aplicación hello). Se produce un punto de recuperación coherente con la aplicación antes de punto más reciente de Hola en el tiempo y provocará la pérdida de datos.
3. Durante la conmutación por error, Site Recovery se cierra Hola máquinas virtuales de Azure. Después de comprobar que conmutación por recuperación se ha completado como se esperaba, puede comprobar tooensure que hello Azure VM que se haya cerrado según lo previsto.

### <a name="reprotect-hello-on-premises-site"></a>Sitio local de hello, vuelva a proteger
Una vez completada la conmutación por recuperación, se eliminan tooensure de máquina virtual de Hola de confirmación que Hola máquinas virtuales de recuperación en Azure. toodo por lo tanto, haga clic en el elemento de hello protegido y, a continuación, haga clic en **confirmar**. Esta acción desencadena un trabajo que quita hello las máquinas virtuales recuperada anterior en Azure.

Una vez completada la confirmación de hello, los datos deben estar en sitio local de hello, pero no estará protegido. toostart replicación tooAzure nuevo, Hola siguientes:

1. En **almacén**, en **configuración** > **replican elementos**, seleccione las máquinas virtuales de Hola que no se han podido volver y, a continuación, haga clic en **volver a proteger**.
2. Dele el valor Hola Hola servidor de procesos que necesita toobe utiliza toosend datos back-tooAzure.
3. Haga clic en **Aceptar**.

Una vez completada la conmutada hello, Hola VM replica tooAzure atrás y realiza una conmutación por error.

### <a name="resolve-common-failback-issues"></a>Resolución de problemas habituales de la conmutación por recuperación
* Si realiza la detección de usuarios de solo lectura de vCenter y protege las máquinas virtuales, se ejecutará correctamente y la conmutación por error funcionará. Durante la conmutada, se produce un error de conmutación por error porque no se pueden detectar Hola almacenes de datos. Como un síntoma, no verá Hola almacenes de datos muestran durante conmutada. tooresolve este problema, puede actualizar la credencial de vCenter Hola con una cuenta adecuada que tenga permisos y vuelva a intentar el trabajo de Hola. Para obtener más información, vea [máquinas virtuales de VMware replicar y tooAzure servidores físicos con Azure Site Recovery](site-recovery-vmware-to-azure-classic.md)
* Al realizar la conmutación por una VM de Linux y ejecutar de forma local, puede ver que ese paquete del Administrador de red de Hola se ha desinstalado del equipo de Hola. Esta desinstalación se produce porque el paquete del Administrador de red de Hola se quita cuando se recupera Hola VM en Azure.
* Cuando una máquina virtual se configura con una dirección IP estática y se ha conmutado tooAzure, dirección IP de Hola se adquiere a través de DHCP. Cuando la conmutación por error local tooon atrás, Hola VM continúa dirección IP de toouse DHCP tooacquire Hola. Manualmente, inicie sesión en toohello máquina y configurar la dirección estática del tooa atrás de dirección IP Hola si es necesario.
* Si utiliza las ediciones gratuitas de ESXi 5.5 o vSphere Hypervisor 6, la conmutación por error se llevará a cabo correctamente, pero la conmutación por recuperación, no. tooenable conmutación por recuperación, licencia de evaluación del programa de actualización tooeither.
* Si no se puede conectar con servidor de configuración de Hola de hello servidor de procesos, compruebe el servidor de configuración de conectividad toohello máquina de servidor de configuración de toohello de Telnet en el puerto 443. También puede probar el servidor de configuración de hello tooping de la máquina del servidor de procesos de Hola. Un servidor de procesos también debe tener un latido cuando llega el servidor de configuración de toohello conectado.
* Si está tratando de toofail tooan atrás alternativo vCenter, asegúrese de que la nueva vCenter está detectado y también se detecta ese servidor de destino maestro Hola. Un síntoma habitual es que Hola almacenes de datos no son accesibles o visibles en hello **Reproteger** cuadro de diálogo.
* Una máquina de WS2008R2SP1 que está protegida como una máquina física local no puede ser no se pudo desde Azure tooon local.

## <a name="fail-back-with-expressroute"></a>Conmutación por recuperación con ExpressRoute
Puede conmutar por recuperación a través de una conexión VPN o usando una conexión ExpressRoute. Si desea toouse una conexión ExpressRoute, observe Hola siguiente:

* Hola conexión ExpressRoute se debe configurar en la red virtual de Azure que tooand conmutar las máquinas de origen Hola Hola donde se encuentran Hola máquinas virtuales de Azure después de producirse la conmutación por error de Hola.
* Los datos están replicado tooan cuenta de almacenamiento de Azure en un punto de conexión público. toouse una conexión ExpressRoute, configurar el emparejamiento público en ExpressRoute con el centro de datos de destino de hello para la replicación de Site Recovery.
