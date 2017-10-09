---
title: "aaaReplicate máquinas virtuales VMware tooAzure | Documentos de Microsoft"
description: "Resume los pasos de Hola que necesita para la replicación de las cargas de trabajo que se ejecuta en máquinas virtuales VMware tooAzure storage"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>Replicar tooAzure de máquinas virtuales de VMware con Site Recovery

> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-vmware-to-azure.md)
> * [Azure clásico](site-recovery-vmware-to-azure-classic.md)


Este artículo describe cómo tooreplicate local tooAzure de máquinas virtuales de VMware, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Si desea que las máquinas virtuales de VMware de toomigrate tooAzure (solo conmutación por error), lectura [este artículo](site-recovery-migrate-to-azure.md) toolearn más.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="deployment-steps"></a>Pasos de implementación

Esto es lo necesita toodo:

1. Compruebe los requisitos previos y las limitaciones.
2. Configure las cuentas de red y almacenamiento de Azure.
3. Preparar la máquina local de Hola que desea toodeploy como servidor de configuración de Hola.
4. Preparar cuentas de VMware toobe utilizadas para la detección automática de máquinas virtuales y, opcionalmente, para la instalación de inserción de hello servicio de movilidad.
4. Cree un almacén de Recovery Services. Hola almacén contiene valores de configuración y organiza la replicación.
5. Especifique la configuración de origen, destino y replicación.
6. Implementar el servicio de movilidad de hello en máquinas virtuales que desee tooreplicate.
7. Habilitar la replicación de hello las máquinas virtuales.
7. Ejecutar un toomake de conmutación por error de prueba que todo funciona según lo previsto.

## <a name="prerequisites"></a>Requisitos previos

**Requisito de compatibilidad** | **Detalles**
--- | ---
**Las tablas de Azure** | Aprenda acerca de los [requisitos de Azure](site-recovery-prereq.md#azure-requirements)
**Servidor de configuración local** | Necesita una máquina virtual de VMware con Windows Server 2012 R2 o posterior. Configure este servidor durante la implementación de Site Recovery.<br/><br/> Proceso predeterminado de hello server y servidor de destino maestro también se instalan en esta máquina virtual. Al escalar verticalmente, tendrá que un servidor de procesos independiente y tendrá Hola mismos requisitos que el servidor de configuración de Hola.<br/><br/> Aprenda más sobre estos componentes [aquí](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**Servidores de VMware locales** | Uno o más servidores de VMware vSphere, con 6.0, 5.5 o 5.1 y las últimas actualizaciones. Servidores deben ubicarse en hello misma red que el servidor de configuración de hello (o servidor de procesos independiente).<br/><br/> Se recomienda un vCenter toomanage Servers, ejecuta 6.0 o 5.5 con las actualizaciones más recientes de Hola. Solo se admiten las características que estén disponibles en 5.5 cuando se implementa la versión 6.0.
**Máquinas virtuales locales** | Las máquinas virtuales que desee tooreplicate debe estar en ejecución una [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)y cumplir con [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). Las máquinas virtuales deberían ejecutar las herramientas de VMware.
**URLs** | servidor de configuración de Hello necesita tener acceso a direcciones URL toothese:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.<br/></br> Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).<br/></br> Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).<br/><br/> Permitir que esta dirección URL de descarga de MySQL de hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Servicio de movilidad** | Instalado en cada máquina virtual replicada.




## <a name="limitations"></a>Limitaciones

**Limitación** | **Detalles**
--- | ---
**Las tablas de Azure** | Cuentas de almacenamiento y de red deben estar en hello misma región que el almacén de Hola<br/><br/> Si usa una cuenta de almacenamiento premium, también necesita un estándar almacenar registros de replicación de toostore de cuenta<br/><br/> No se puede replicar toopremium cuentas en el centro y sur de India.
**Servidor de configuración local** | El tipo de adaptador de máquina virtual de VMware debe ser VMXNET3. Si no lo es, [instale esta actualización](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Se debe instalar vSphere PowerCLI 6.0.<br/><br> máquina de Hello no debe ser un controlador de dominio. máquina de Hello debe tener una dirección IP estática.<br/><br/> nombre de host de Hello debe ser de 15 caracteres o menos, y el sistema operativo debe estar en inglés.
**VMware** | Solo se admiten las características de la versión 5.5 en vCenter 6.0. Site Recovery no admite las nuevas características de vCenter y vSphere 6.0, como Cross vCenter vMotion, volúmenes virtuales y DRS de almacenamiento.
**VM** | Compruebe las [limitaciones de máquinas virtuales de Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> No se pueden replicar máquinas virtuales con discos cifrados ni tampoco con arranque UEFI/EFI.<br/><br> No se admiten los clústeres de disco compartido. Si una VM de origen hello tiene la formación de equipos, se convierte tooa único NIC después de la conmutación por error.<br/><br/> Si las máquinas virtuales tengan un disco iSCSI, Site Recovery lo convierte archivos de disco duro virtual tooa después de la conmutación por error. Si el destino de iSCSI de hello pueda tener acceso mediante Hola VM de Azure, se conecta tooit y ve y Hola VHD. Si esto ocurre, desconecte el destino de iSCSI de Hola.<br/><br/> Si desea que la coherencia de varias máquinas de tooenable, lo que permite a máquinas virtuales que ejecutan Hola mismo toobe de carga de trabajo recuperado datos coherentes tooa juntos punto, abrir el puerto 20004 en hello VM.<br/><br/> Windows debe instalarse en la unidad C de Hola. debe ser el disco del sistema operativo de Hello básicos y no dinámicos. disco de datos de Hello puede ser dinámico.<br/><br/> Los archivos / etc/hosts de Linux en máquinas virtuales deben contener entradas que asignan nombre de host local de hello tooIP direcciones asociado con todos los adaptadores de red. Hola, nombre de host, los puntos de montaje, nombre de dispositivo, las rutas de acceso del sistema y los nombres de archivo (/ etcetera; / usr) debe estar en inglés solamente.<br/><br/> Se admiten tipos específicos de [almacenamiento Linux](site-recovery-support-matrix-to-azure.md#support-for-storage).<br/><br/>Crear o establecer **disk.enableUUID=true** en la configuración de máquina virtual de Hola. Esto proporciona un toohello UUID coherente VMDK, por lo que se monta correctamente y garantiza que los cambios diferenciales solo se transfieren local tooon back-durante la conmutación por recuperación, sin replicación completa.

## <a name="set-up-azure"></a>Configuración de Azure

1. [Configure una red de Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - Las máquinas virtuales de Azure se colocarán en esta red cuando se creen después de la conmutación por error.
    - Puede configurar una red en el modo de [Resource Manager](../resource-manager-deployment-model.md) o en el clásico.

2. Configure una [cuenta de Azure Storage](../storage/storage-create-storage-account.md#create-a-storage-account) para los datos replicados.
    - Hola cuenta puede ser estándar o [premium](../storage/storage-premium-storage.md).
    - Puede configurar una red en el modo de Resource Manager o en el clásico.

3. [Preparar una cuenta](#prepare-for-automatic-discovery-and-push-installation) en servidor de vCenter Hola o hosts de vSphere, por lo que ese Site Recovery puede detectar automáticamente las máquinas virtuales de VMware.

## <a name="prepare-hello-configuration-server"></a>Preparar el servidor de configuración de Hola

1. Instale Windows Server 2012 R2 o posterior en una máquina virtual de VMware.
2. Asegúrese de que Hola máquina virtual tiene acceso toohello direcciones URL en [requisitos previos](#prerequisites).
3. Instale [VMware vSphere PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1).


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>Preparación de la detección automática y la instalación de inserción

- **Preparar una cuenta para la detección automática de**: servidor de proceso de recuperación del sitio de hello detecta automáticamente las máquinas virtuales. toodo, credenciales de necesidades de recuperación del sitio que pueden tener acceso a servidores vCenter y los hosts de ESXi vSphere.

    1. toouse una cuenta dedicada, cree un rol (nivel Hola vCenter, con estos [permisos](#vmware-account-permissions). Asígnele un nombre como **Azure_Site_Recovery**.
    2. A continuación, cree un usuario en el servidor de host/vCenter vSphere de Hola y asignar a Hola rol toohello usuario. Especifique esta cuenta de usuario durante la implementación de Site Recovery.

- **Preparar un Hola de toopush cuenta servicio de movilidad**: si desea tooVMs de servicio de movilidad de hello toopush, necesita una cuenta que puede usarse por Hola proceso servidor tooaccess Hola máquina virtual. cuenta de Hello solo se utiliza para la instalación de inserción de Hola. Puede usar una cuenta local o de dominio:

    - Para Windows, si no usa una cuenta de dominio, debe toodisable control de acceso de usuarios remotos en el equipo local de Hola. toodo, Hola registrar con **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, agregar una entrada DWORD hello **LocalAccountTokenFilterPolicy**, con un valor de 1.
    - Si desea que entrada de registro de hello tooadd de Windows desde una CLI, escriba:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Para Linux, la cuenta de hello debe ser raíz Hola servidor de origen Linux.

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>Seleccione el objetivo de protección de Hola

Seleccione la acción que realizará tooreplicate, y donde quiera tooreplicate a.

1. Haga clic en **Almacenes de Recovery Services** > almacén.
2. Hola recurso de menú, haga clic en **Site Recovery** > **paso 1: preparar la infraestructura** > **objetivo de protección**.

    ![Elegir objetivos](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. En **objetivo de protección**, seleccione **tooAzure** > **Sí, con el hipervisor de VMware vSphere**.

    ![Elegir objetivos](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

Configurar el servidor de configuración de hello, registrar en el almacén de Hola y detectar máquinas virtuales.

1. Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Origen**.
2. Si no tiene un servidor de configuración, haga clic en **+Servidor de configuración**.

    ![Configurar origen](./media/site-recovery-vmware-to-azure/set-source1.png)
3. En **Agregar servidor**, compruebe que aparezca **Servidor de configuración** en **Tipo de servidor**.
4. Descargue el archivo de instalación de configuración de Site Recovery unificado de Hola.
5. Descargue la clave de registro del almacén de Hola. Se le solicitará cuando ejecute la instalación unificada. clave de Hello es válida durante cinco días después de generarlo.

   ![Configurar origen](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Ejecución de la instalación unificada de Site Recovery

Realice la siguiente Hola antes de iniciar después ejecutar el programa de instalación unificada tooinstall servidor de configuración de hello, servidor de procesos de Hola y servidor de destino maestro Hola.
    - Vea un vídeo introductorio rápido

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - En la máquina virtual del servidor de configuración de hello, asegúrese de que el reloj del sistema de Hola se sincroniza con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deben ser iguales. Si hay una diferencia de 15 minutos, antes o después, se podría producir un error en la instalación.
    - Ejecute el programa de instalación como administrador Local en la máquina virtual del servidor de configuración de Hola.
    - Asegúrese de que TLS 1.0 está habilitado en hello máquina virtual.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> También se puede instalar el servidor de configuración de Hello [desde la línea de comandos de hello](http://aka.ms/installconfigsrv).



### <a name="add-hello-account-for-automatic-discovery"></a>Agregar cuenta de hello para la detección automática

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>Conectar servidores tooVMware

Conecte toovSphere ESXi hosts o servidores vCenter, máquinas virtuales de VMware toodiscover.

- Si Agregar servidor de vCenter Hola o hosts de vSphere con una cuenta sin privilegios de administrador en el servidor de hello, cuenta de hello necesita estos privilegios habilitados:
    - Centro de datos, Almacén de datos, Carpeta, Host, Red, Recurso, Máquina virtual, vSphere Distributed Switch.
    - servidor de vCenter Hola necesita permisos de vistas de almacenamiento.
- Al agregar servidores de VMware, se pueden tardar 15 minutos o más para ellos tooappear en el portal de Hola.
tooallow Azure Site Recovery toodiscover máquinas virtuales que ejecutan en su entorno local, debe tooconnect el servidor VMware vCenter o hosts de ESXi vSphere con Site Recovery.

Seleccione **+ vCenter** toostart conectar un servidor VMware vCenter o un host de VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

Recuperación del sitio conecta a servidores de tooVMware mediante Hola especifica la configuración y detecta las máquinas virtuales.

## <a name="set-up-hello-target"></a>Establecer el destino de Hola

Antes de configurar el entorno de destino de hello, compruebe que tiene un [cuenta de almacenamiento de Azure y red](#set-up-azure)

1. Haga clic en **preparar infraestructura** > **destino**, y seleccione Hola desea toouse de suscripción de Azure.
2. Especifique si el modelo de implementación de destino está basado en Resource Manager o si es el clásico.
3. Site Recovery comprueba que tiene una o más cuentas de almacenamiento y redes compatibles.

   ![Destino](./media/site-recovery-vmware-to-azure/gs-target.png)
4. Si no ha creado una cuenta de almacenamiento o red, haga clic en **+ cuenta de almacenamiento** o **+ red**, toocreate un administrador de recursos cuenta o red en línea.

## <a name="set-up-replication-settings"></a>Configuración de las opciones de replicación

Vea un vídeo introductorio rápido antes de empezar:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate una nueva directiva de replicación, haga clic en **infraestructura de Site Recovery** > **directivas de replicación** > **+ directiva de replicación**.
2. En **Crear directiva de replicación**, especifique un nombre de directiva.
3. En **umbral de RPO**, especifique el límite RPO de Hola. Este valor especifica la frecuencia con que se crean puntos de recuperación de datos. Se genera una alerta cuando la replicación continua supera este límite.
4. En **retención de punto de recuperación**, especifique cuánto tiempo (en horas) es el período de retención de Hola para cada punto de recuperación. Máquinas virtuales replicadas se pueden recuperar tooany punto en una ventana. Seguridad too24 retención de horas es compatible con máquinas replicadas toopremium almacenamiento y 72 horas para el almacenamiento estándar.
5. En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (en minutos) con la que se crearán puntos de recuperación que contengan las instantáneas coherentes con la aplicación. Haga clic en **Aceptar** toocreate directiva de Hola.

    ![Directiva de replicación](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. Cuando se crea una nueva directiva automáticamente está asociada con el servidor de configuración de Hola. De forma predeterminada, se crea automáticamente una directiva correspondiente para la conmutación por recuperación. Por ejemplo, si hello directiva de replicación es **rep-policy** será la directiva de conmutación por recuperación de hello **rep-directiva de conmutación por recuperación**. Esta directiva no se usa hasta que se inicie una conmutación por recuperación desde Azure.  



## <a name="plan-capacity"></a>Planeamiento de la capacidad

1. Ahora que tiene la infraestructura básica configurada, puede planear la capacidad y averiguar si necesitará recursos adicionales. [Más información](site-recovery-plan-capacity-vmware.md).
2. Seleccione **Sí** en **¿Completó el planeamiento de capacidad?** cuando haya terminado de planear la capacidad.

   ![Planificación de capacidad](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Preparación de las máquinas virtuales para la replicación

servicio de movilidad de Hello debe estar instalado en todas las máquinas virtuales de VMware que desea tooreplicate. Puede instalar servicio de movilidad de Hola de varias maneras:

1. Instalar con una instalación de inserción Hola del servidor de procesos. Necesita tooprepare toouse de máquinas virtuales a este método.
2. Instálelo con herramientas de implementación como System Center Configuration Manager o DSC de Azure Automation.
3.  Instálelo manualmente.

[Más información](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Habilitar replicación

Antes de comenzar:

- Su cuenta de usuario de Azure necesita toohave determinados [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una nueva tooAzure de máquina virtual.
- Al agregar o modificar las máquinas virtuales, puede tardar minutos too15 o ya cambios tootake efecto y les tooappear en el portal de Hola.
- Puede comprobar tiempo de hello descubrió por última vez para las máquinas virtuales en **servidores de configuración** > **último contacto a**.
- tooadd máquinas virtuales sin tener que esperar la detección programada de hello, servidor de configuración de hello resaltado (no haga clic en él) y haga clic en **actualizar**.
- Si una máquina virtual está preparada para la instalación de inserción, servidor de procesos de hello instala automáticamente servicio de movilidad de hello cuando se habilita la replicación.


### <a name="exclude-disks-from-replication"></a>Excluir discos de la replicación

De manera predeterminada, se replican todos los discos de una máquina. Puede excluir discos de la replicación. Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez que una máquina o reinicia la aplicación (por ejemplo, pagefile.sys o tempdb de SQL Server).

### <a name="replicate-vms"></a>Replicación de máquinas virtuales

Vea un vídeo introductorio rápido antes de empezar

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Haga clic en **Paso 2: Replicar la aplicación** > **Origen**.
2. En **origen**, seleccione servidor de configuración de Hola.
3. En **Tipo de máquina**, seleccione **Máquinas virtuales**.
4. En **vCenter/vSphere hipervisor**, seleccione servidor de vCenter Hola que administra el host de vSphere hello, o host Hola.
5. Seleccione el servidor de procesos de Hola. Si no ha creado ningún servidor de proceso adicionales esto será el servidor de configuración de Hola. y, a continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. En **destino**, seleccione la suscripción de Hola y Hola grupo de recursos en el que desea hello toocreate conmutado por error las máquinas virtuales. Elija el modelo de implementación de Hola que desee toouse en Azure (clásico o recurso de administración), para hello conmutado por error las máquinas virtuales.


7. Seleccione la cuenta de almacenamiento de Azure de Hola que desee toouse para la replicación de datos. Si no desea toouse una cuenta que ya haya configurado, puede crear uno nuevo.

8. Seleccione hello Azure toowhich de red y subred de máquinas virtuales de Azure se conectará, cuando se crean después de la conmutación por error. Seleccione **configurar ahora para las máquinas seleccionadas**, tooapply Hola red configuración tooall máquinas que seleccione para la protección. Seleccione **configurar más adelante** tooselect hello Azure red por máquina. Si no desea toouse una red existente, puede crear uno.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. En **máquinas virtuales** > **seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate. Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación. A continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. En **propiedades** > **configurar las propiedades**, seleccione cuenta de hello que va a utilizar Hola proceso servidor tooautomatically instale servicio de movilidad de hello en la máquina de Hola.
11. De manera predeterminada se replican todos los discos. Haga clic en **todos los discos** y desactive los discos que no desea tooreplicate. y, a continuación, haga clic en **Aceptar**. Puede establecer otras propiedades de las máquinas virtuales más adelante.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. En **configuración de replicación** > **establecer configuración de replicación**, compruebe que Hola correcto se selecciona la directiva de replicación. Si modifica una directiva, cambios será máquina tooreplicating aplicados y toonew máquinas.
12. Habilitar **coherencia entre varias VM** si desea toogather máquinas en un grupo de replicación y especifique un nombre para el grupo de Hola. y, a continuación, haga clic en **Aceptar**. Observe lo siguiente:

    * Todas las máquinas de un grupo de replicación se replican al mismo tiempo y comparten puntos de recuperación coherentes con los bloqueos y con la aplicación cuando conmutan por error.
    * Se recomienda que recopile las máquinas virtuales y los servidores físicos juntos para que reflejen las cargas de trabajo. Habilitar la coherencia entre varias VM puede afectar al rendimiento de la carga de trabajo y solo debe usarse si las máquinas ejecutan Hola necesita la misma carga de trabajo y coherencia.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. Haga clic en **Enable Replication**. Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **configuración** > **trabajos** > **trabajos de recuperación de sitio**. Después de hello **finalización de protección** ejecuciones del trabajo Hola máquina está lista para conmutación por error.

### <a name="view-and-manage-vm-properties"></a>Visualización y administración de las propiedades de la máquina virtual

Se recomienda que compruebe las propiedades de la máquina virtual de Hola y realizar cualquier cambio que necesite.

1. Haga clic en **replican elementos** > y seleccione Hola máquina. Hola **Essentials** hoja muestra información sobre la configuración de máquinas y estado.
2. En **propiedades**, puede ver la replicación y Hola de información de conmutación por error de máquina virtual.
3. En **de proceso y de red** > **propiedades de proceso**, puede especificar el tamaño de nombre y de destino de la máquina virtual de Azure de Hola. Modificar Hola nombre toocomply con [requisitos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) si necesita.
4. Modificar la configuración de red de destino de hello, subred y dirección IP que se va a asignar toohello máquina virtual de Azure:

   - Puede establecer la dirección IP de destino de Hola.

    - Si no proporciona una dirección, Hola conmutado por error equipo usará DHCP.
    - Si establece una dirección que no esté disponible en el momento de la conmutación por error, esta no funcionará.
    - Hola la misma dirección IP de destino puede usarse para conmutación por error de prueba, si está disponible en la red de conmutación por error de prueba de Hola Hola dirección.

   - número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de hello:

     - Si Hola algunos adaptadores de red de máquina de origen de Hola Hola igual o menor, número de Hola de adaptadores permitido para el tamaño de máquina de destino de hello, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.
     - Si número Hola de adaptadores para la máquina virtual de origen de hello supera número de hello permitido para el tamaño de destino de hello, se utilizará el tamaño máximo de hello destino.
     - Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un equipo de destino de Hola tendrá solo un adaptador.     
   - Si la máquina virtual de hello tiene varios adaptadores de red se conectarán todos toohello misma red.
   - Si la máquina virtual de hello tiene varios adaptadores de red, a continuación, Hola mostrado en la lista de hello deja de estar hello *predeterminado* adaptador de red de máquina virtual de Azure Hola.
4. En **discos**, puede ver el sistema operativo de la VM de Hola y datos de hello discos que se replicarán.

#### <a name="managed-disks"></a>Discos administrados

En **de proceso y de red** > **propiedades de proceso**, puede establecer "Discos administrados por usar" configuración demasiado "Sí" para hello VM si desea que tooattach discos administrados tooyour máquina en tooAzure de conmutación por error. Discos administrados simplifica la administración de discos para máquinas virtuales de IaaS de Azure debido a que administra las cuentas de almacenamiento de hello asociadas con discos de máquina virtual de Hola. [Más información sobre discos administrados](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Discos administrados son toohello creado y adjunta máquina virtual sólo una tooAzure de conmutación por error. Al habilitar la protección, datos de máquinas locales seguirán tooreplicate toostorage cuentas.  Discos administrados pueden crearse únicamente para máquinas virtuales implementadas mediante el modelo de implementación de administrador de recursos de Hola.  

   - Cuando se establece "Discos administrados por uso" demasiado "Sí", solo conjuntos de disponibilidad de grupo de recursos de hello con "Discos administrados por uso" conjunto demasiado "Sí" estaría disponibles para la selección. Esto es porque las máquinas virtuales con discos administrados sólo puede ser parte de los conjuntos de disponibilidad con el conjunto de propiedades de "Use administrado discos" demasiado "Sí". Asegúrese de crear conjuntos de disponibilidad con el conjunto de propiedades de "Use administrado discos" en función de los discos de intención toouse administrado en la conmutación por error.  Del mismo modo, cuando se establece "Discos administrados por uso" demasiado "No", solo conjuntos de disponibilidad de grupo de recursos de hello con "Discos administrados por uso" propiedad establecida demasiado "No" estaría disponibles para la selección. [Más información sobre discos administrados y conjuntos de disponibilidad](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Si la cuenta de almacenamiento de hello usada para la replicación se cifró con cifrado de servicio de almacenamiento en cualquier momento en el tiempo, se producirá un error en la creación de discos administrados durante la conmutación por error. Se puede establecer "Discos administrados por uso" demasiado "No" y vuelva a intentar la conmutación por error o deshabilite la protección de máquina virtual de Hola y proteger tooa cuenta de almacenamiento que no tenía el cifrado del servicio de almacenamiento habilitado en cualquier momento en el tiempo.
  > [Más información sobre el Cifrado del servicio de Storage y los discos administrados](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba


Una vez que hayas configurado todo, ejecute un toomake de conmutación por error de prueba que todo funciona según lo previsto. Vea un vídeo introductorio rápido antes de empezar
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail a través de un único equipo, en **configuración** > **replican elementos**, haga clic en hello VM > **+ conmutación por error de prueba** icono.

    ![Probar conmutación por error](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. toofail a través de una recuperación del plan, en **configuración** > **planes de recuperación**, plan de hello contextual > **conmutación por error de prueba**. un plan de recuperación, toocreate [, siga estas instrucciones](site-recovery-create-recovery-plans.md).  

1. En **conmutación por error de prueba**, seleccione toowhich de red de Azure Hola máquinas virtuales de Azure se conectará después de producirse la conmutación por error.

1. Haga clic en **Aceptar** conmutación por error de toobegin Hola. Pueda seguir el progreso haciendo clic en hello VM tooopen sus propiedades o en hello **conmutación por error de prueba** trabajo en nombre de almacén > **configuración** > **trabajos**  >  **Trabajos de recuperación del sitio**.

1. Una vez completada la conmutación por error de hello, también debe poder réplica de hello toosee máquina Azure aparecen en hello portal de Azure > **máquinas virtuales**. Debe asegurarse de que esa máquina virtual de hello es el tamaño adecuado de hello, que ha conectado toohello de red adecuada y que se está ejecutando.

1. Si se [preparado para las conexiones después de la conmutación por error](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), debe ser capaz de tooconnect toohello máquina virtual de Azure.

1. Una vez que haya terminado, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación. En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. Esto eliminará las máquinas virtuales de Hola que se crearon durante la conmutación por error de prueba.

[Más información](site-recovery-test-failover-to-azure.md) sobre las conmutaciones por error de prueba.


## <a name="vmware-account-permissions"></a>Permisos de cuenta de VMware

Recuperación del sitio necesita acceso tooVMware para tooautomatically de servidor de proceso de hello detectar máquinas virtuales y conmutación por error y conmutación por recuperación de máquinas virtuales.

- **Migrar**: si solo desea toomigrate tooAzure de máquinas virtuales VMware, sin nunca producen errores en ellos volver, puede usar una cuenta de VMware con un rol de solo lectura. Este rol puede ejecutar la conmutación por error, pero no puede apagar las máquinas de origen protegidas. Esto no es necesario para la migración.
- **Replicación/recuperación**: si desea que la cuenta de hello de toodeploy replicación completa (replicate, conmutación por error, conmutación por recuperación) debe ser capaz de toorun operaciones como la creación y eliminación de discos, encendido etcetera de máquinas virtuales.
- **Detección automática**: se requiere al menos una cuenta de solo lectura.


**Task** | **Cuenta/rol necesarios** | **Permisos** | **Detalles**
--- | --- | --- | ---
**El servidor de procesos detecta automáticamente máquinas virtuales de VMware** | Necesita al menos un usuario de solo lectura. | Objeto de centro de datos –> propagar tooChild objeto, rol = solo lectura | Usuario asignado a nivel de centro de datos y tiene acceso tooall Hola objetos en el centro de datos de Hola.<br/><br/> acceso toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** objeto, los objetos secundarios toohello (hosts de vSphere, almacenes de datos, las máquinas virtuales y redes).
**Conmutación por error** | Necesita al menos un usuario de solo lectura. | Objeto de centro de datos –> propagar tooChild objeto, rol = solo lectura | Usuario asignado a nivel de centro de datos y tiene acceso tooall Hola objetos en el centro de datos de Hola.<br/><br/> acceso toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** toohello los objetos secundarios (hosts de vSphere, almacenes de datos, las máquinas virtuales y redes) del objeto.<br/><br/> Es útil para la migración, pero no para la replicación completa, la conmutación por error o la conmutación por recuperación.
**Conmutación por error y conmutación por recuperación** | Se recomienda crear un rol (Azure_Site_Recovery) con los permisos necesario de hello y, a continuación, asignar Hola rol tooa VMware usuario o grupo | Objeto de centro de datos –> propagar tooChild objeto, rol = Azure_Site_Recovery<br/><br/> Almacén de datos -> Asignar espacio, examinar almacén de datos, operaciones de archivo de bajo nivel, quitar archivo, actualizar archivos de máquina virtual<br/><br/> Red -> Asignación de red<br/><br/> Recursos -> grupo de VM asignar tooresource, migrar apagado de máquina virtual, migrar encendidos VM<br/><br/> Tareas -> Crear tarea, actualizar tarea<br/><br/> Máquina virtual -> Configuración<br/><br/> Máquina virtual -> Interactuar -> Responder a pregunta, conexión de dispositivos, configurar soporte de CD, Configurar soporte de disquete, apagar, encender, instalación de herramientas de VMware<br/><br/> Máquina virtual -> Inventario -> Crear, registrar, anular registro<br/><br/> Máquina virtual -> Aprovisionamiento -> Permitir descarga de máquina virtual, permitir carga de archivos de máquina virtual<br/><br/> Máquina virtual -> Instantáneas -> Quitar instantáneas | Usuario asignado a nivel de centro de datos y tiene acceso tooall Hola objetos en el centro de datos de Hola.<br/><br/> acceso toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** objeto, los objetos secundarios toohello (hosts de vSphere, almacenes de datos, las máquinas virtuales y redes).


## <a name="next-steps"></a>Pasos siguientes

Después de desarrollar la replicación y en ejecución, cuando se produce una interrupción, conmutar por error tooAzure y máquinas virtuales de Azure se crean a partir de datos saludo replican. A continuación, puede acceder a las cargas de trabajo y las aplicaciones en Azure, hasta que se produce un error ubicación principal tooyour atrás cuando devuelve las operaciones de toonormal.

- [Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.
- Si migra máquinas en lugar de replicar y conmutar por recuperación, [lea más](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Obtenga información sobre la conmutación por recuperación](site-recovery-failback-azure-to-vmware.md), toofail back y replicar máquinas virtuales de Azure nuevo sitio de toohello local principal.

## <a name="third-party-software-notices-and-information"></a>Avisos e información de software de terceros
Do Not Translate or Localize

software de Hola y firmware que se ejecuta Hola técnico de Microsoft o servicio se basa en o incorpora material de hello proyectos enumerados a continuación (colectivamente, "código de terceros").  Microsoft es hello autor no original del programa Hola a código de terceros.  Hola aviso de propiedad intelectual y licencia, en la que Microsoft ha recibido este código de terceros, se establecen estipulado más adelante.

información de Hello en la sección A se con respecto a otro código de terceros componentes de proyectos de Hola se enumeran a continuación. Such licenses and information are provided for informational purposes only.  Este código de terceros se está tooyou relicensed por Microsoft en términos de los productos de Microsoft de Hola y servicio de licencias de software de Microsoft.  

información de Hello en la sección B se con respecto a los componentes de código de terceros que se están realizando tooyou disponible por parte de Microsoft bajo los términos de licencia original Hola.

podrá encontrar más completa del archivo Hello en hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
