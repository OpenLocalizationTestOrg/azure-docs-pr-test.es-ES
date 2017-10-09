---
title: aaaReprotect desde el sitio local de Azure tooan | Documentos de Microsoft
description: "Después de la conmutación por error de máquinas virtuales tooAzure, puede iniciar un toobring de conmutación por recuperación local de tooon de espera de las máquinas virtuales. Obtenga información acerca de cómo tooreprotect antes de una conmutación por recuperación."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 94c86e79cba4cd3f0c5821fdd5509cca1d0e7820
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-azure-tooan-on-premises-site"></a>Vuelva a proteger de sitio local de Azure tooan



## <a name="overview"></a>Información general
Este artículo se describe cómo tooreprotect Azure máquinas virtuales desde el sitio de Azure tooan local. Siga las instrucciones de hello en este artículo cuando estés listo toofail realizar copia sus máquinas virtuales de VMware o servidores físicos de Windows/Linux después de que han conmutado de hello local sitio tooAzure (como se describe en [replicar VMware virtual equipos y servidores físicos tooAzure con Azure Site Recovery](site-recovery-failover.md)).

> [!WARNING]
> No se producirá un error después de [completar la migración](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), mover un grupo de recursos de máquina virtual tooanother o eliminar una máquina virtual de Azure.


Tras finaliza conmutada y hello máquinas virtuales se replican, puede iniciar una conmutación por recuperación en hello máquinas virtuales toobring les toohello al sitio local.

Enviar comentarios o preguntas al final de Hola de este artículo o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Para obtener una introducción rápida, vea Hola siguiendo el vídeo sobre cómo toofail a través de Azure tooan sitio local.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a>Requisitos previos
Al preparar las máquinas virtuales tooreprotect, tomar o considere la posibilidad de hello siguientes acciones de requisitos previos:

* Si administra un servidor vCenter hello las máquinas virtuales que desea toofail en, asegúrese de que dispone de hello [los permisos necesarios](site-recovery-vmware-to-azure-classic.md) para la detección de máquinas virtuales en servidores vCenter.

  > [!WARNING]
  > Si las instantáneas están presentes en hello en maestra destino o hello máquina virtual local, solo se produce un error. Puede eliminar las instantáneas de hello en el destino maestro Hola antes de continuar tooreprotect. las instantáneas de Hello en la máquina virtual de Hola se mezclan automáticamente durante un trabajo de reprotección.

* Antes de conmutar por recuperación, cree dos componentes adicionales:

  * **Servidor de procesos**: Hola [servidor de proceso](site-recovery-vmware-setup-azure-ps-resource-manager.md) recibe los datos de la máquina virtual de hello protegido en Azure y envía el sitio local de toohello de datos. Tiene una red de baja latencia entre el servidor de procesos de Hola y máquina virtual de hello protegido. Por lo tanto, puede tener un servidor de procesos local si está usando una conexión Azure ExpressRoute o un servidor de procesos basado en Azure y una VPN.
  
  * **Servidor de destino maestro**: servidor de destino maestro Hola recibe datos de conmutación por recuperación. servidor de administración local de Hola que ha creado tiene un servidor de destino maestro que se instala de forma predeterminada. Sin embargo, según volumen Hola de tráfico de conmutar por recuperación, deberá toocreate un servidor de destino maestro independiente de conmutación por recuperación.
    * [Una máquina virtual Linux necesita un servidor de destino maestro Linux](site-recovery-how-to-install-linux-master-target.md).
    * Una máquina virtual Windows necesita un servidor de destino maestro Windows. Hola local proceso servidor y maestro de equipos de destino puede utilizar de nuevo.

    destino maestro Hello tiene otros requisitos previos que se enumeran en [toocheck de acciones comunes en un destino maestro antes de reprotección](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server).

* Se necesita un servidor de configuración en local al conmutar por recuperación. Durante la conmutación por recuperación, máquina virtual de hello debe existir en la base de datos del servidor de configuración de Hola. En caso contrario, la conmutación por recuperación no será correcta. 

> [!IMPORTANT]
> Asegúrese de realizar una copia de seguridad programada periódica del servidor de configuración. Si se produce un desastre, restaure el servidor de hello con hello direcciones IP mismo modo que funcione la conmutación por recuperación.

* Conjunto hello `disk.EnableUUID=true` establecer en parámetros de configuración de Hola Hola maestro máquina virtual de destino en VMware. Si la fila no existe, agréguela. Esta configuración es tooprovide requiere un disco de máquina virtual de toohello coherente de UUID (VMDK) para que monta correctamente.

* *No se puede utilizar Storage vMotion en el servidor de destino maestro hello*. Esto puede causar hello toofail de conmutación por recuperación. máquina virtual de Hello no puede iniciar porque los discos de hello no tooit disponible. tooprevent este problema, los servidores de destino maestro de hello excluir de la lista de vMotion.

* Agregar un nuevo servidor de destino maestro toohello de unidad: una unidad de retención. Agregar una nueva unidad de Hola de disco y el formato.


### <a name="frequently-asked-questions"></a>Preguntas más frecuentes

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-tooreplicate-data-back-toohello-on-premises-site"></a>¿Por qué necesito una VPN S2S o un sitio local de ExpressRoute conexión tooreplicate datos toohello atrás?
Mientras que la replicación desde tooAzure local puede suceder a través de Internet de Hola o una conexión que tiene el emparejamiento público, conmutada y conmutación por recuperación de ExpressRoute requieren un sitio a sitio (S2S) datos de tooreplicate VPN. Proporcione red Hola para que Hola se conmutó por error de máquinas en Azure puede llegar a servidor de configuración de (ping) hello en local. También puede implementar un servidor de procesos en hello Azure red de máquina virtual de Hola se conmutó por error. Este servidor de procesos también debe ser capaz de toocommunicate con servidor de configuración de hello en local.

#### <a name="when-should-i-install-a-process-server-in-azure"></a>¿Cuándo se debe instalar un servidor de procesos en Azure?


máquinas virtuales de Hello en Azure que desea tooreprotect enviar el servidor de procesos de tooa de datos de replicación. Configurar la red para que las máquinas virtuales de hello en Azure puede alcanzar el servidor de procesos de Hola.

Puede implementar un servidor de procesos en Azure o usar servidor existente de hello procesos que usó durante la conmutación por error. Hola importante punto tooconsider es datos de saludo latencia toosend Hola desde máquinas virtuales de hello en servidor de proceso de Azure toohello.

Si tiene configurada una conexión ExpressRoute, puede usar un datos de toosend de servidor de proceso local porque hay poca latencia Hola entre la máquina virtual de Hola y servidor de procesos de Hola.

 ![Diagrama de la arquitectura de ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



Sin embargo, si tiene sólo una VPN S2S, se recomienda implementar el servidor de procesos de hello en Azure.

 ![Diagrama de la arquitectura de VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


Recuerde que la replicación se produce sólo a través de VPN de S2S de Hola u Hola privada de intercambio de tráfico de la red de ExpressRoute. Asegúrese de que hay suficiente ancho de banda disponible a través de ese canal de red.

Para más información sobre cómo instalar un servidor de procesos basado en Azure, vea [Administración de un servidor de procesos que se ejecuta en Azure](site-recovery-vmware-setup-azure-ps-resource-manager.md).

> [!TIP]
> Se recomienda usar un servidor de procesos basado en Azure durante la conmutación por recuperación. rendimiento de la replicación de Hello es mayor si el servidor de procesos de hello es toohello más cerca de la replicación de máquina virtual (máquina de Hola se conmutó por error en Azure). Sin embargo, durante la prueba de concepto (POC) o demostración, puede usar el servidor de procesos de local de hello junto con ExpressRoute con privada emparejamiento toocomplete hello más rápida de la prueba de concepto.



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a>¿Qué puertos se deben abrir en distintos componentes para que la reprotección funcione?

![Puertos para conmutación por error y conmutación por recuperación](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a>¿Qué servidor de destino maestro se debería usar para la reprotección?
Un servidor de destino maestro local es necesario tooreceive datos Hola del servidor de procesos y, a continuación, escribe VMDK toohello local de la máquina virtual. Si va a proteger máquinas virtuales Windows, necesita un servidor de destino maestro Windows. Puede volver a usar servidor de proceso local de Hola y de destino maestro<!-- !todo component -->. Para máquinas virtuales Linux, deberá tooset el un destino maestro de Linux locales adicionales.


Para más información sobre cómo instalar un servidor de destino maestro, vea:

* [Cómo Windows tooinstall maestro a servidor de destino](site-recovery-vmware-to-azure.md)
* [Cómo el servidor de destino de la principal de tooinstall Linux](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-hello-on-premises-esxi-host-during-failback"></a>¿Qué tipos de almacén de datos se admiten en el host ESXi de hello local durante la conmutación por recuperación?

Actualmente, Azure Site Recovery es compatible con errores haga copia solo el sistema de archivos de máquina virtual de tooa (VMFS) o el almacén de datos de vSAN. No se admiten los almacenes de datos NFS. Debido a la limitación toothis, selección de almacén de datos de Hola de entrada en hello reprotección pantalla está vacío en caso de hello de almacenes de datos NFS, o se muestra el almacén de datos de hello vSAN pero se produce un error durante el trabajo de Hola. Si tiene previsto volver toofail, puede crear un almacén de datos VMFS local y producirá un error tooit atrás. Esta conmutación por recuperación hará que una descarga completa de hello VMDK.

### <a name="common-things-toocheck-after-completing-installation-of-hello-master-target-server"></a>Common toocheck cosas después de completar la instalación del servidor de destino maestro Hola

* Si hello máquina virtual está presente en local Hola servidor vCenter, hello servidor de destino maestro debe tener acceso a VMDK toohello local de la máquina virtual. El acceso es necesario toowrite Hola replican datos toohello discos máquina virtual. Asegúrese de que el almacén de datos de esa Hola local máquina virtual está montado en el host de destino maestro Hola con acceso de lectura/escritura.

* Si la máquina virtual de hello no está presente en local en servidor de vCenter hello, Hola servicio Site Recovery debe toocreate una nueva máquina virtual durante conmutada. Esta máquina virtual se crea en el host ESX hello en que se crea el destino maestro Hola. Elija con cuidado, host ESX de Hola para que se cree la máquina virtual de conmutación por recuperación de hello en el host de Hola que desee.

* *No se puede utilizar Storage vMotion para servidor de destino maestro hello*. Esto puede causar hello toofail de conmutación por recuperación. máquina virtual de Hello no puede iniciar porque los discos de hello no tooit disponible.

  > [!WARNING]
  > Si un destino maestro se somete a una tarea de vMotion de almacenamiento después conmutada, discos de máquinas virtuales de hello protegido que son el destino maestro toohello adjunto migran toohello destino de la tarea de hello vMotion. Si intentas toofail después de esto, se produce un error en la desasociación del disco de hello porque no se encuentran los discos de Hola. A continuación, se convierte en discos de Hola de disco duro toofind en sus cuentas de almacenamiento. Necesita toofind ellos manualmente y conéctelas toohello virtual machine. Después de eso, puede arrancar máquina virtual de hello en local.

* Agregar un retención unidad tooyour existente Windows servidor de destino maestro. Agregar una nueva unidad de Hola de disco y el formato. unidad de retención de Hola es toostop usado Hola puntos en el tiempo cuando máquina virtual de hello replica sitio local de toohello back. Estos son algunos criterios de una unidad de retención. Sin estos criterios, unidad de hello no se mostrarán para el servidor de destino maestro Hola.

   * volume de Hello no se usa para ningún otro fin, como un destino de replicación.

   * volumen de Hello no está en modo de bloqueo.

   * Hola volumen no es un volumen de caché. instalación de destino maestro Hello no debe existir en ese volumen. volumen de instalación personalizada de Hello para el destino de servidor y maestro de proceso de hello no es válida para un volumen de retención. Cuando el servidor de procesos de Hola y de destino maestro están instalados en un volumen, Hola trata de un volumen de caché de destino maestro Hola.

   * tipo de sistema de archivos de Hola de hello volumen no es FAT o FAT32.

   * capacidad del volumen Hello es distinto de cero.

   * volumen de retención predeterminado de Hola para Windows es Hola R.

   * volumen de retención predeterminado de Hola para Linux es /mnt/retention.

  > [!IMPORTANT]
  > Debe tooadd una nueva unidad si está usando una máquina de servidor de configuración del servidor de proceso existente o una escala o un equipo de servidor de destino de proceso servidor/maestro. nueva unidad de Hello debe cumplir Hola anterior de requisitos. Si la unidad de retención de hello no está presente, no aparece en la lista de desplegable de selección de hello en el portal de Hola. Después de agregar un destino maestro de unidad toohello local, ocupa minutos too15 tooappear de unidad de hello en selección de hello en el portal de Hola. También puede actualizar el servidor de configuración de hello si unidad hello no aparece después de 15 minutos.

* Una máquina virtual Linux conmutada por error necesita un servidor de destino maestro Linux. Una máquina virtual Windows conmutada por error necesita un servidor de destino maestro Windows.

* Instalar las herramientas de VMware en el servidor de destino maestro Hola. Sin las herramientas de VMware hello, almacenes de datos de hello en host ESXi del destino maestro hello no se puede detectar.

* Habilitar hello `disk.EnableUUID=true` parámetro en la máquina de virtual de destino maestro hello mediante las propiedades de vCenter Hola. <!-- !todo Needs link. -->

* destino maestro Hola debe tener al menos un almacén de datos VMFS adjunta. Si no hay ninguno, Hola **Datastore** entrada en la página de reprotección Hola estará vacío y no puede continuar.

* servidor de destino maestro Hello no puede tener las instantáneas de discos de Hola. Si hay instantáneas, se produce un error en la reprotección y la conmutación por recuperación.

* destino maestro Hello no puede tener una controladora SCSI de Paravirtual. controlador de Hello solo puede ser un controlador de lógica de LSI. Sin ella, se produce un error en la reprotección.

<!--
### Failback policy
tooreplicate back tooon-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with hello configuration server during creation.
2. This policy is not editable.
3. hello set values of hello policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-tooreprotect"></a>Tooreprotect de pasos

> [!NOTE]
> Después de una máquina virtual arranca en Azure, tarda algún tiempo para el agente de hello servidor de configuración de tooregister toohello atrás (hacia arriba too15 minutos). Durante este tiempo, solo se produce un error y un mensaje de error indica que el agente hello no está instalado. Espere unos minutos y vuelva a intentar la reprotección.



1. En **almacén** > **replican elementos**, haga clic en la máquina virtual de Hola que se ha conmutado por error y, a continuación, seleccione **volver a proteger**. También puede hacer clic en hello equipo y seleccione **volver a proteger** de botones de comando de Hola.
2. En la hoja de hello, tenga en cuenta esa dirección Hola de protección, **locales de tooOn Azure**, ya está seleccionado.
3. En **servidor de destino maestro** y **servidor de proceso**, seleccione el servidor de destino maestro local de Hola y Hola servidor de procesos.
4. Para **Datastore**, seleccione Hola toowhich de almacén de datos que desee toorecover Hola discos locales. Esta opción se utiliza cuando se elimina la máquina virtual de hello local y necesita toocreate nuevos discos. Esta opción se omite si ya existen discos de hello, pero seguirá necesitando toospecify un valor.
5. Elija la unidad de retención de Hola.
6. Directiva de conmutación por recuperación de Hola se selecciona automáticamente.
7. Haga clic en **Aceptar** toobegin conmutada. Un trabajo comienza tooreplicate Hola virtual máquina desde el sitio de Azure toohello local. Puede realizar el seguimiento del progreso de hello en hello **trabajos** ficha.

Si desea que toorecover tooan ubicación alternativa (cuando se elimina la máquina virtual de hello local), seleccione la unidad de retención de Hola y almacén de datos que están configurados para el servidor de destino maestro Hola. Cuando se produce un error de sitio local de toohello atrás, hello VMware máquinas virtuales en uso de plan de protección de conmutación por recuperación de Hola Hola mismo almacén de datos como Hola maestro servidor de destino. Entonces se crea una nueva máquina virtual en vCenter.

Si desea toorecover Hola máquina virtual existente de Azure tooan máquina virtual local, Hola de montaje local de almacenes de datos de la máquina virtual con acceso de lectura/escritura en el host de ESXi del servidor de destino maestro Hola.
    ![Cuadro de diálogo Reproteger](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

También puede proteger en el nivel de Hola de un plan de recuperación. Solo se puede reproteger un grupo de replicación mediante un plan de recuperación. Cuando vuelva a efectuar mediante el uso de un plan de recuperación, necesita valores de hello tooprovide en todos los equipos protegidos.

> [!NOTE]
> Use Hola mismo tooreprotect de servidor de destino maestro en un grupo de replicación. Si utiliza un tooreprotect de servidor de destino maestro diferente un grupo de replicación, servidor hello no puede proporcionar un punto común en el tiempo.

> [!NOTE]
> máquina virtual de Hello local se ha desactivado durante conmutada. Esto ayuda a garantizar la coherencia de datos durante la replicación. No encender Hola máquina virtual una vez finalizada conmutada.

Después conmutada Hola se realiza correctamente, máquina virtual de hello deberá especificar un estado protegido.

## <a name="next-steps"></a>Pasos siguientes

Después de máquina virtual de hello ha entrado en un estado protegido, puede [iniciar una conmutación por recuperación](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back). 

Hola conmutación por recuperación se apagará de máquina virtual de hello en Azure y la máquina virtual de arranque Hola local. Esperar cierto tiempo de inactividad de la aplicación hello. Elija una hora para la conmutación por recuperación cuando la aplicación hello puede tolerar un tiempo de inactividad.

## <a name="common-problems"></a>Problemas comunes

* Si usa una plantilla toocreate las máquinas virtuales, asegúrese de que cada máquina virtual tiene su propio UUID para discos de Hola. Si Hola local conflictos de UUID de la máquina virtual con el de destino maestro Hola ya que ambos se crean desde Hola mismo plantilla, solo se produce un error. Implementar otro destino maestro que aún no ha creado de hello misma plantilla.

* Si realiza la detección de usuarios de solo lectura de vCenter y protege las máquinas virtuales, la protección se ejecutará correctamente y la conmutación por error funcionará. Durante la conmutada, se produce un error de conmutación por error porque no se pueden detectar Hola almacenes de datos. Un síntoma es que hello almacenes de datos no aparezcan durante conmutada. tooresolve este problema, puede actualizar la credencial de vCenter Hola con una cuenta adecuada que tiene permisos, y vuelva a intentar el trabajo de Hola. Para obtener más información, consulte [tooAzure de servidores físicos con Azure Site Recovery y de máquinas virtuales de VMware replicar](site-recovery-vmware-to-azure-classic.md).

* Al realizar la conmutación por una máquina virtual Linux y ejecutar de forma local, puede ver que ese paquete del Administrador de red de Hola se ha desinstalado del equipo de Hola. Esta desinstalación se produce porque el paquete del Administrador de red de Hola se quita cuando se recupera la máquina virtual de hello en Azure.

* Cuando una máquina virtual Linux se configura con una dirección IP estática y se ha conmutado tooAzure, dirección IP de hello obtenido de DHCP. Al conmutar tooon local, máquina virtual de hello continúa dirección IP de toouse DHCP tooacquire Hola. Manualmente iniciar sesión en la máquina de toohello y configurar dirección estática de hello IP dirección tooa atrás si es necesario. Una máquina virtual Windows puede adquirir su dirección IP estática de nuevo.

* Si usa las ediciones gratuitas de ESXi 5.5 o vSphere 6 Hypervisor, la conmutación por error se llevará a cabo correctamente, pero la conmutación por recuperación, no. tooenable conmutación por recuperación, licencia de evaluación del programa de actualización tooeither.

* Si no se puede alcanzar el servidor de configuración de Hola Hola del servidor de procesos, use el servidor de configuración de Telnet toocheck conectividad toohello en el puerto 443. También puede probar el servidor de configuración de tooping Hola Hola del servidor de procesos. Un servidor de procesos también debe tener un latido cuando llega el servidor de configuración de toohello conectado.

* Si está tratando de toofail tooan atrás alternativo vCenter, asegúrese de que se han detectado vCenter nuevo y el servidor de destino maestro de Hola. Un síntoma habitual es que Hola almacenes de datos no son accesibles o visibles en hello **Reproteger** cuadro de diálogo.

* No se puede no se pudo un servidor de Windows Server 2008 R2 SP1 está protegido como físico servidor local desde el sitio de Azure tooan local.
