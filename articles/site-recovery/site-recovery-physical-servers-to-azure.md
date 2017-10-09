---
title: "aaaReplicate servidores físicos tooAzure | Documentos de Microsoft"
description: "Describe cómo replicación de tooorchestrate de toodeploy Azure Site Recovery, la conmutación por error y la recuperación de local tooAzure de servidores físicos de Windows/Linux mediante el uso de hello portal de Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>Replicar máquinas físicas tooAzure mediante el uso de Site Recovery


Este artículo describe cómo tooreplicate local tooAzure máquinas físicas mediante el uso de servicio de Azure Site Recovery Hola Hola portal de Azure.

Si desea toomigrate máquinas físicas tooAzure (solo conmutación por error), lectura [migrar tooAzure con Site Recovery](site-recovery-migrate-to-azure.md) toolearn más.

Envíe los comentarios y preguntas en parte inferior de este artículo o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Requisitos previos

**Requisito de compatibilidad** | **Detalles**
--- | ---
**Las tablas de Azure** | Obtenga información sobre los [requisitos de Azure](site-recovery-prereq.md#azure-requirements)
**Servidor de configuración local** | Máquina local (física o máquina virtual de VMWare) con Windows Server 2012 R2 o versiones posteriores. Configurar servidor de configuración de Hola durante la implementación de Site Recovery.<br/><br/> De forma predeterminada, servidor de procesos de Hola y el servidor de destino maestro también se instalan en este equipo. Al escalar verticalmente, tendrá que un servidor de procesos independiente y tendrá Hola mismos requisitos que el servidor de configuración de Hola.<br/><br/> Obtener más información sobre estos componentes en [configurar el entorno de origen de hello](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**Máquinas virtuales locales** | Equipos que desee tooreplicate debe estar en ejecución una [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) y cumplir con [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs** | servidor de configuración de Hello necesita tener acceso a direcciones URL toothese:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.<br/></br> Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) y Hola puerto HTTPS (443).<br/></br> Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para la administración de identidades y de control de acceso).<br/><br/> Permitir que esta dirección URL de descarga de MySQL de hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Servicio de movilidad** | Este servicio se instala en todos los equipos que desee tooreplicate.

## <a name="limitations"></a>Limitaciones

**Limitación** | **Detalles**
--- | ---
**Las tablas de Azure** | Cuentas de almacenamiento y de red deben estar en hello misma región que el almacén de Hola.<br/><br/> Si usa una cuenta de almacenamiento premium, también necesita un estándar almacenar registros de replicación toostore la cuenta.<br/><br/> No se puede replicar toopremium cuentas en el centro y sur de India.
**Servidor de configuración local** | Si instala el servidor de configuración de hello en una VM de VMware, Hola tipo de adaptador de máquina virtual debe ser VMXNET3. Si no lo es, [instale esta actualización](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Si usa una máquina virtual de VMware, debe instalar vSphere PowerCLI 6.0 en ella.<br/><br> máquina de Hello no debe ser un controlador de dominio.<br/><br/> máquina de Hello debe tener una dirección IP estática.<br/><br/> nombre de host de Hello debe ser de 15 caracteres o menos, y el sistema operativo de hello debe estar en inglés.
**Máquinas replicadas** | Compruebe las [limitaciones de las VM de Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Si desea que la coherencia de varias máquinas de tooenable, lo que permite ejecutar Hola recuperado de la misma toobe de carga de trabajo de máquinas datos coherentes tooa juntos punto, abrir el puerto 20004 en la máquina de Hola.<br/><br/> Se admiten tipos específicos de [almacenamiento Linux](site-recovery-support-matrix-to-azure.md#support-for-storage).
**Conmutación por recuperación** | No se puede suspender volver desde la máquina virtual de Azure tooa. Si desea toobe toofail capaz de atrás tooon local después de la conmutación por error, tendrá que un entorno de VMware para que se puede producir un error tooa back-VM de VMware.


## <a name="set-up-azure"></a>Configuración de Azure

1. [Configure una red de Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. Las VM de Azure se colocarán en esta red cuando se creen después de la conmutación por error.

      b. Puede configurar una red en el modo de Azure [Resource Manager](../resource-manager-deployment-model.md) o en el clásico.

2. Configure una [cuenta de Azure Storage](../storage/storage-create-storage-account.md#create-a-storage-account) para los datos replicados.

    a. Hola cuenta puede ser estándar o [premium](../storage/storage-premium-storage.md).

    b. Puede configurar una cuenta en el modo de Resource Manager o en el clásico.

## <a name="prepare-hello-configuration-server"></a>Preparar el servidor de configuración de Hola

1. Instale Windows Server 2012 R2 o una versión posterior en un servidor físico local o una máquina virtual de VMware.

2. Asegúrese de que máquina hello tiene acceso toohello direcciones URL en [requisitos previos](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Preparación para la instalación del Servicio de Movilidad

Si desea que el equipo físico tooa del servicio de movilidad de toopush hello, necesita una cuenta que puede usarse en hello proceso servidor tooaccess Hola máquinas. cuenta de Hello se usa solo para la instalación de inserción de Hola. Puede usar una cuenta local o de dominio:

  - Para Windows, si no usa una cuenta de dominio, debe toodisable control de acceso de usuarios remotos en el equipo local de Hola. toodo esto, en el registro de hello en **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, agregar una entrada DWORD hello **LocalAccountTokenFilterPolicy**, con un valor de 1. Si desea que entrada de registro de hello tooadd para Windows desde una interfaz de línea de comandos, escriba:

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Para Linux, cuenta de hello debe ser un usuario raíz Hola servidor de origen Linux.


## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>Seleccione el objetivo de protección de Hola

Seleccione en qué desea tooreplicate y donde quiera tooreplicate a.

1. Haga clic en **Almacenes de Recovery Services** > **almacén**.
2. En hello **recursos** menú, haga clic en **Site Recovery** > **preparar infraestructura** > **objetivo de protección**.

    ![Elegir objetivos](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. En **objetivo de protección**, seleccione **tooAzure** > **no virtualizados / otros**.


## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

Configurar el servidor de configuración de hello, registrar en el almacén de Hola y detectar máquinas virtuales.

1. Haga clic en **Site Recovery** > **Preparar la infraestructura** > **Origen**.
2. Si no tiene un servidor de configuración, haga clic en **+Servidor de configuración**.

    ![Configurar origen](./media/site-recovery-vmware-to-azure/set-source1.png)

3. En **Agregar servidor**, compruebe que aparezca **Servidor de configuración** en **Tipo de servidor**.
4. Descargar hello **configuración unificado de Site Recovery** archivo de instalación.
5. Descargar hello **clave de registro del almacén**. Se le solicitará cuando ejecute la instalación unificada. clave de Hello es válida durante cinco días después de generarlo.

   ![Configurar origen](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Ejecución de la instalación unificada de Site Recovery

Antes de empezar, Hola siguientes:

- Vea un vídeo introductorio rápido (Hola vídeo describe cómo procesa las máquinas virtuales de VMware tooreplicate pero hello es similar para la replicación de máquina física.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- En el equipo del servidor de configuración de hello, asegúrese de que el reloj del sistema de Hola se sincroniza con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Si hay una diferencia de 15 minutos, antes o después, se podría producir un error en la instalación.
- Ejecute el programa de instalación como administrador local en el equipo del servidor de configuración de Hola.
- Asegúrese de que TLS 1.0 está habilitada en el equipo de Hola.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> También se puede instalar el servidor de configuración de Hello [desde la línea de comandos de hello](http://aka.ms/installconfigsrv).


## <a name="set-up-hello-target-environment"></a>Configurar el entorno de destino de Hola

Antes de configurar el entorno de destino de hello, compruebe toomake Asegúrese de que tiene un [cuenta de almacenamiento de Azure y red](#set-up-azure).

1. Haga clic en **preparar infraestructura** > **destino**, y seleccione Hola desea toouse de suscripción de Azure.
2. Especifique si el modelo de implementación de destino está basado en Resource Manager o si es el clásico.
3. Recuperación de sitio comprueba toomake Asegúrese de que tiene una o más cuentas de almacenamiento de Azure compatible y redes.

   ![Destino](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Si no ha creado una cuenta de almacenamiento o red, haga clic en **+ cuenta de almacenamiento** o **+ red** toocreate un administrador de recursos cuenta o red en línea.

## <a name="set-up-replication-settings"></a>Configuración de las opciones de replicación

Antes de empezar, vea un vídeo introductorio rápido (Hola vídeo describe cómo procesa las máquinas virtuales de VMware tooreplicate pero hello es similar para la replicación de máquina física.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate una nueva directiva de replicación, haga clic en **infraestructura de Site Recovery** > **directivas de replicación** > **+ directiva de replicación**.
2. En **Crear directiva de replicación**, especifique un nombre de directiva.
3. En **umbral de RPO**, especifique el límite RPO de Hola. Este valor especifica la frecuencia con que se crean puntos de recuperación de datos. Se genera una alerta cuando la replicación continua supera este límite.
4. En **retención de punto de recuperación**, especifique cuánto tiempo (en horas) es el período de retención de Hola para cada punto de recuperación. Máquinas virtuales replicadas se pueden recuperar tooany punto en una ventana. Retención de horas se admite para el almacenamiento de máquinas replicada toopremium hasta too24. Retención de horas se admite para el almacenamiento de máquinas replicada toostandard hasta too72.
5. En **Frecuencia de instantánea coherente con la aplicación**, especifique la frecuencia (en minutos) con la que se crearán puntos de recuperación que contengan las instantáneas coherentes con la aplicación. Haga clic en **Aceptar** toocreate directiva de Hola.

    ![Directiva de replicación](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Cuando se crea una nueva directiva, se asocia automáticamente con el servidor de configuración de Hola. De forma predeterminada, se crea automáticamente una directiva correspondiente para la conmutación por recuperación. Por ejemplo, si hello directiva de replicación es **rep-policy**, directiva de conmutación por recuperación de hello es **rep-directiva de conmutación por recuperación**. Esta directiva no se usa hasta que se inicie una conmutación por recuperación desde Azure.  


## <a name="plan-capacity"></a>Planeamiento de la capacidad

1. Ahora que tiene la infraestructura básica configurada, puede planear la capacidad y averiguar si necesitará recursos adicionales. [Más información](site-recovery-plan-capacity-vmware.md).
2. Seleccione **Sí** en **¿Completó el planeamiento de capacidad?** cuando haya terminado de planear la capacidad.

   ![Planificación de capacidad](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Preparación de las máquinas virtuales para la replicación

Todos los equipos que desee tooreplicate debe tener instalado el servicio de movilidad de Hola. Puede instalar servicio de movilidad de Hola de varias maneras:

- Instalar servicio de hello con una instalación de inserción Hola del servidor de procesos. Necesita tooprepare máquinas en toouse por adelantado a este método.
- Instalar servicio de hello mediante herramientas de implementación, como System Center Configuration Manager o configuración de estado deseado de automatización de Azure.
- Instalar manualmente el servicio de Hola.

[Más información](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>Habilitar replicación

Antes de comenzar:

- Su cuenta de usuario de Azure necesita toohave determinados [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una nueva tooAzure de máquina virtual.
- Al agregar o modificar las máquinas virtuales, puede tardar minutos too15 o ya para cambios tootake efecto y les tooappear en el portal de Hola.
- Puede comprobar tiempo de hello descubrió por última vez para las máquinas virtuales en **servidores de configuración** > **último contacto a**.
- tooadd máquinas virtuales sin tener que esperar la detección programada de hello, servidor de configuración de hello resaltado (no haga clic en él) y haga clic en **actualizar**.
- Si una máquina virtual está preparada para la instalación de inserción, servidor de procesos de hello instala automáticamente servicio de movilidad de hello cuando se habilita la replicación.
- Vea un vídeo introductorio rápido (Hola vídeo describe cómo procesa las máquinas virtuales de VMware tooreplicate pero hello es similar para la replicación de máquina física.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Excluir discos de la replicación

De manera predeterminada, se replican todos los discos de una máquina. Puede excluir discos de la replicación. Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez un reinicio de aplicación o del equipo (por ejemplo, pagefile.sys o tempdb de SQL Server).

### <a name="replicate-vms"></a>Replicación de máquinas virtuales

1. Haga clic en **Replicar la aplicación** > **Origen**.
2. En **Origen**, seleccione **Local**.
3. En **ubicación de origen**, seleccione nombre de servidor de configuración de Hola.
4. En **Tipo de máquina**, seleccione **Máquinas físicas**.
5. En **servidor de proceso**, elija servidor de procesos de Hola. Si no ha creado ningún servidor de proceso adicional, este servidor es el servidor de configuración de Hola. y, a continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/chooseVM.png)

6. En **destino**, seleccione hello **suscripción** hello y **grupo de recursos** en el que desea toocreate Hola máquinas virtuales de Azure después de la conmutación por error. Elija Hola implementación modelo que desea toouse en Azure (clásico o el Administrador de recursos) para Hola conmutó por error las máquinas virtuales.

7. Seleccione la cuenta de almacenamiento de Azure de Hola que desee toouse para la replicación de datos. Si no desea toouse una cuenta que ya haya configurado, puede crear uno nuevo.

8. Seleccione hello **red Azure** y **subred** toowhich máquinas virtuales de Azure conectarse después de la conmutación por error. Seleccione **configurar ahora para las máquinas seleccionadas** tooapply Hola red configuración tooall máquinas que seleccione para la protección. Seleccione **configurar más adelante** tooselect hello Azure red por máquina. Si no desea toouse una red existente, puede crear uno.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/targetsettings.png)

9. En **máquinas físicas**, haga clic en **+ máquina física** y escriba hello **nombre** y **dirección IP**. Elija el sistema operativo de Hola de máquina de hello desea tooreplicate. Tarda unos minutos hasta que se detectan y se muestra en la lista de hello máquinas.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/machineselect.png)

10. En **propiedades** > **configurar las propiedades**, seleccione cuenta de hello toobe usa Hola proceso servidor tooautomatically instale servicio de movilidad de hello en la máquina de Hola.
11. De manera predeterminada se replican todos los discos. Haga clic en **todos los discos**y desactive los discos que no desea tooreplicate. y, a continuación, haga clic en **Aceptar**. Puede establecer otras propiedades de las máquinas virtuales más adelante.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/configprop.png)

12. En **configuración de replicación** > **establecer configuración de replicación**, compruebe que Hola correcto se selecciona la directiva de replicación. Si modifica una directiva, los cambios son toohello aplicada la replicación de máquina y toonew máquinas.
13. Habilitar **coherencia entre varias VM** si desea toogather máquinas en un grupo de replicación y especifique un nombre para el grupo de Hola. y, a continuación, haga clic en **Aceptar**. Observe lo siguiente:

    a. Todas las máquinas de un grupo de replicación se replican al mismo tiempo y comparten puntos de recuperación coherentes con los bloqueos y con la aplicación cuando conmutan por error.

    b. Se recomienda que recopile las máquinas virtuales y los servidores físicos juntos para que reflejen las cargas de trabajo. La habilitación de la coherencia entre varias VM puede afectar al rendimiento de la carga de trabajo. Se debe usar solo si las máquinas están ejecutando Hola la misma carga de trabajo y necesita la coherencia.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/policy.png)

14. Haga clic en **Enable Replication**. Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **configuración** > **trabajos** > **trabajos de recuperación de sitio**. Después de hello **finalización de protección** se ejecuta el trabajo, Hola máquina está lista para conmutación por error.

Después de habilitar la replicación, Hola Mobility service está instalado si configura la instalación de inserción. Una vez Hola servicio de movilidad inserción instalado en un equipo, un trabajo de protección se inicia y se produce un error. Después de un error de hello, necesita toomanually reiniciar cada máquina. A continuación, comienza de nuevo trabajo de protección de Hola y se produce la replicación inicial.


### <a name="view-and-manage-azure-vm-properties"></a>Ver y administrar las propiedades de la máquina virtual de Azure

Se recomienda que compruebe las propiedades de la máquina virtual de Hola y realizar cualquier cambio que necesite.

1. Haga clic en **replican elementos**y seleccione Hola máquina. Hola **Essentials** hoja muestra información sobre la configuración de máquinas y estado.
2. En **propiedades**, puede ver la replicación y Hola de información de conmutación por error de máquina virtual.
3. En **de proceso y de red** > **propiedades de proceso**, puede especificar el tamaño de nombre y de destino de la máquina virtual de Azure de Hola. Modificar Hola nombre toocomply con [requisitos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) si necesita.
4. Modificar la configuración de red de destino de hello, la subred y la dirección IP que se asigna toohello máquina virtual de Azure:

    a. Puede establecer la dirección IP de destino de Hola.

    b.  Si no proporciona una dirección, máquina se conmutó por error de hello usa DHCP.

    c. Si establece una dirección que no esté disponible en el momento de la conmutación por error, esta operación no funcionará.

    d. Hola la misma dirección IP de destino puede usarse para la conmutación por error si está disponible en la red de conmutación por error de prueba de Hola Hola dirección.

    e. número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de hello:

     - Si Hola algunos adaptadores de red de máquina de origen de Hola Hola igual o menor, número de Hola de adaptadores permitido para el tamaño de máquina de destino de hello, destino de hello tiene Hola mismo número de adaptadores como origen de Hola.
     - Si se supera el número de Hola de adaptadores para la máquina virtual de origen de Hola Hola permitidas para el tamaño de destino de hello, a continuación, se utiliza el tamaño máximo de hello destino.
     - Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino hello tiene dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero tamaño de destino de hello admite admite solo una, equipo de destino de hello tiene solo un adaptador.     
   - Si la máquina virtual de hello tiene varios adaptadores de red, todos ellos conectan toohello misma red.
   - Si máquina virtual de hello tiene varios adaptadores de red, hello mostrado en la lista de hello deja de estar hello *predeterminado* adaptador de red en hello VM de Azure.
5. En **discos**, puede ver los discos de datos de Hola que se replican y sistema operativo de la VM de Hola.

## <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

Una vez hayas configurado todo, ejecute un toomake de conmutación por error de prueba que todo funciona según lo previsto. Vea un vídeo introductorio rápido antes de empezar.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail a través de un único equipo, en **configuración** > **replican elementos**, haga clic en **conmutación por error de prueba**.

    ![Probar conmutación por error](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. toofail a través de una recuperación del plan, en **configuración** > **planes de recuperación**, plan de hello contextual > **conmutación por error de prueba**. un plan de recuperación, toocreate [, siga estas instrucciones](site-recovery-create-recovery-plans.md).  
3. En **conmutación por error de prueba**, seleccione toowhich de red de Azure Hola máquinas virtuales de Azure están conectados después de producirse la conmutación por error.
4. Haga clic en **Aceptar** conmutación por error de toobegin Hola. Puede seguir el progreso, haga clic en hello VM tooopen sus propiedades o haciendo clic en hello **conmutación por error de prueba** trabajo en nombre de almacén > **configuración** > **trabajos**  >  **Trabajos de recuperación del sitio**.
5. Una vez finalizada la conmutación por error de hello, también debe poder réplica de hello toosee máquina Azure aparecen en hello portal de Azure > **máquinas virtuales**. Asegúrese de que ese hello VM es el tamaño adecuado de hello, que ha conectado toohello de red adecuada y que se está ejecutando.
6. Si se [preparado para las conexiones después de la conmutación por error](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), debe ser capaz de tooconnect toohello máquina virtual de Azure.
7. Cuando haya terminado, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación. En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. Este paso elimina máquinas virtuales de Hola que se crearon durante la conmutación por error de prueba.

Para obtener más información, vea hello [tooAzure de conmutación por error de prueba](site-recovery-test-failover-to-azure.md) documento.

## <a name="next-steps"></a>Pasos siguientes

Después de desarrollar la replicación y en ejecución, cuando se produce una interrupción, conmutar por error tooAzure y máquinas virtuales de Azure se crean a partir de datos saludo replican. A continuación, puede acceder a las cargas de trabajo y las aplicaciones en Azure, hasta que se produce un error ubicación principal tooyour atrás cuando devuelve las operaciones de toonormal.

- [Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.
- Si migra máquinas en lugar de replicar y conmutar por recuperación, [lea más](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- Al replicar las máquinas virtuales, puede solo el entorno de VMware del tooa de conmutación por recuperación. [Lea acerca de la conmutación por recuperación](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Avisos e información de software de terceros
Do Not Translate or Localize

software de Hola y firmware que se ejecuta Hola técnico de Microsoft o servicio se basa en o incorpora material de hello proyectos enumerados a continuación (colectivamente, "código de terceros"). Microsoft no es autor original de Hola de hello código de terceros. Hola aviso de propiedad intelectual y licencia, en la que Microsoft ha recibido este código de terceros, se establecen estipulado más adelante.

información de Hello en la sección A se relacionados con código de terceros componentes de proyectos de Hola se enumeran a continuación. Such licenses and information are provided for informational purposes only. Este código de terceros se está tooyou relicensed por Microsoft en términos de los productos de Microsoft de Hola y servicio de licencias de software de Microsoft.  

información de Hello en la sección B se con respecto a los componentes de código de terceros que se están realizando tooyou disponible por parte de Microsoft bajo los términos de licencia original Hola.

archivo completa de Hello puede encontrarse en hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
