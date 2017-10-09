---
title: "aaaReplicate máquinas virtuales de Hyper-V tooAzure | Documentos de Microsoft"
description: "Describe cómo la replicación tooorchestrate, conmutación por error y recuperación de local Hyper-V VM tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>Replicar tooAzure de máquinas virtuales (sin WMM) de Hyper-V con Azure Site Recovery Hola portal de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Azure clásico](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell: administrador de recursos](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Este artículo describe cómo tooreplicate local tooAzure de máquinas virtuales de Hyper-V, con [Azure Site Recovery](site-recovery-overview.md) Hola portal de Azure. En esta implementación, las máquinas virtuales de Hyper-V no están administradas por System Center Virtual Machine Manager (VMM).

Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Si desea toomigrate máquinas tooAzure (sin conmutación por recuperación), obtenga más información en [este artículo](site-recovery-migrate-to-azure.md).



## <a name="deployment-steps"></a>Pasos de implementación

Siga estos pasos de implementación de hello artículo toocomplete:

1. [Obtener más información](site-recovery-components.md#hyper-v-to-azure) acerca de la arquitectura de Hola para esta implementación. Además, [conozca](site-recovery-hyper-v-azure-architecture.md) cómo funciona la replicación de Hyper-V en Site Recovery.
2. Compruebe los requisitos previos y las limitaciones.
3. Configure las cuentas de red y almacenamiento de Azure.
4. Prepare los hosts de Hyper-V.
5. Cree un almacén de Recovery Services. Hola almacén contiene valores de configuración y organiza la replicación.
6. Especifique la configuración de origen. Crear un sitio de Hyper-V que contiene hosts de Hyper-V de Hola y registrar sitio hello en el almacén de Hola. Instalar Hola proveedor de Azure Site Recovery y el agente de servicios de recuperación de Microsoft hello, en los hosts de Hyper-V de Hola.
7. Especifique la configuración de destino y replicación.
8. Habilitar la replicación de hello las máquinas virtuales.
9. Ejecutar un toomake de conmutación por error de prueba que todo funciona según lo previsto.



## <a name="prerequisites"></a>Requisitos previos


**Requisito** | **Detalles** |
--- | --- |
**Las tablas de Azure** | Obtenga información sobre los [requisitos de Azure](site-recovery-prereq.md#azure-requirements)
**Servidores locales** | [Obtener más información](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) sobre los requisitos para hosts de Hyper-V de hello en local.
**Máquinas virtuales de Hyper-V locales** | Las máquinas virtuales que desee tooreplicate debe estar en ejecución una [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)y cumplir con [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Direcciones URL de Azure** | Hosts de Hyper-V necesitan tener acceso a direcciones URL toothese:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.<br/></br> Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).<br/></br> Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).



## <a name="prepare-for-deployment"></a>Preparación de la implementación

tooprepare para la implementación que debe:

1. [Configurar una red de Azure](#set-up-an-azure-network) en la que las máquinas virtuales de Azure se encuentran cuando se crean después de la conmutación por error.
2. [Configurar una cuenta de almacenamiento de Azure](#set-up-an-azure-storage-account) para datos replicados.
3. [Prepare los hosts de Hyper-V de hello](#prepare-the-hyper-v-hosts) tooensure pueden tener acceso Hola requiere direcciones URL.

### <a name="set-up-an-azure-network"></a>Configurar una red de Azure

Configure una red de Azure. La necesitará para que las máquinas virtuales de Azure de hello cree después de conmutación por error están conectados tooa red.

* red de Hello debe formar parte de hello misma región que hello del almacén de servicios de recuperación.
* Según el modelo de recursos de Hola que desee toouse para conmutado por error máquinas virtuales de Azure, configurar el Hola con la red de Azure en [modo de administrador de recursos](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), o [modo clásico](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* Es recomendable configurar una red antes de empezar. Si no lo hace, deberá toodo durante la implementación de Site Recovery.
- Las cuentas de almacenamiento utilizadas por recuperación del sitio no pueden ser [movido](../azure-resource-manager/resource-group-move-resources.md) dentro de hello mismo, o entre distintas, suscripciones.


### <a name="set-up-an-azure-storage-account"></a>Configurar una cuenta de almacenamiento de Azure

- Necesita una cuenta de almacenamiento de Azure toohold datos replican tooAzure estándar o premium. [Almacenamiento premium](../storage/storage-premium-storage.md) se utiliza normalmente para las máquinas virtuales que necesitan un rendimiento de E/S alto y cargas de trabajo intensivas de baja latencia toohost E/S.
- Si desea que toouse un toostore de cuenta premium los datos replicados, también necesita un registros de replicación toostore de la cuenta de almacenamiento estándar que captura continua cambia datos tooon locales.
- Según el modelo de recursos de Hola que desee toouse para conmutado por error máquinas virtuales de Azure, configure una cuenta en [modo de administrador de recursos](../storage/storage-create-storage-account.md), o [modo clásico](../storage/storage-create-storage-account-classic-portal.md).
- Es recomendable configurar una cuenta de almacenamiento antes de empezar. Si no lo hace, necesita toodo durante la implementación de Site Recovery. Hola cuentas deben Hola misma región que hello del almacén de servicios de recuperación.
- No se puede mover cuentas de almacenamiento utilizan por Site Recovery en grupos de recursos dentro de hello misma suscripción, o a través de distintas suscripciones.


### <a name="prepare-hello-hyper-v-hosts"></a>Preparar los hosts de Hyper-V de Hola

* Asegúrese de que los hosts de Hyper-V de hello cumplen hello [requisitos previos](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).
- Asegúrese de que Hola hosts pueden obtener acceso a direcciones URL de hello necesario.


## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Nuevo** > **Supervisión y administración** > **Backup y Site Recovery (OMS)**.  

    ![Almacén nuevo](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. En **nombre**, especificar un almacén de hello tooidentify nombre descriptivo. Si tiene más de una suscripción, seleccione una de ellas.

4. [Cree un grupo de recursos nuevo](../azure-resource-manager/resource-group-template-deploy-portal.md) o seleccione uno que ya exista, y especifique una región de Azure. Las máquinas estén región toothis replicada. regiones de toocheck compatibles, consulte disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).

5. Si desea que tooquickly acceso Hola almacén de hello panel, haga clic en **Pin toodashboard**y, a continuación, haga clic en **crear**.

    ![Almacén nuevo](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

nuevo almacén de Hello aparece en hello **panel** > **todos los recursos** lista y, en Hola principal **servicios de recuperación de los almacenes de credenciales** hoja.



## <a name="select-hello-protection-goal"></a>Seleccione el objetivo de protección de Hola

Seleccione la acción que realizará tooreplicate, y donde quiera tooreplicate a.

1. Hola **servicios de recuperación de los almacenes de credenciales**, seleccione el almacén de Hola.
2. En **Introducción**, haga clic en **Site Recovery** > **Preparar infraestructura** > **Objetivo de protección**.

    ![Elegir objetivos](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. En **objetivo de protección**, seleccione **tooAzure**y seleccione **Sí, con Hyper-V**. Seleccione **No** tooconfirm no usa VMM. y, a continuación, haga clic en **Aceptar**.

    ![Elegir objetivos](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

Configurar el sitio de Hyper-V de hello, instalar Hola proveedor de Azure Site Recovery y el agente de servicios de recuperación de Azure de hello en hosts de Hyper-V y registrar sitio hello en el almacén de Hola.

1. En **Preparar infraestructura**, haga clic en **Origen**. Haga clic en un nuevo sitio de Hyper-V como un contenedor para los hosts de Hyper-V o clústeres, tooadd **+ sitio de Hyper-V**.

    ![Configurar origen](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. En **sitio Hyper-V crear**, especifique un nombre para el sitio de Hola. y, a continuación, haga clic en **Aceptar**. Ahora, seleccione el sitio de Hola que creó y, después, haga clic en **+ servidor Hyper-V** tooadd un sitio de toohello de servidor.

    ![Configurar origen](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. En **Agregar servidor** > **Tipo de servidor**, compruebe que se muestra **Hyper-V Server**.

    - Asegúrese de que ese servidor hello Hyper-V que desee tooadd cumple con hello [requisitos previos](#on-premises-prerequisites), y es capaz de tooaccess Hola direcciones URL especificadas.
    - Descargar archivo de instalación del proveedor de Azure Site Recovery de Hola. Ejecute este hello de tooinstall archivo proveedor y Hola agente de servicios de recuperación en cada host de Hyper-V.

    ![Configurar origen](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Instalar Hola proveedor y agente

1. Ejecutar el archivo de instalación de proveedor de hello en cada host agregado toohello Hyper-V sitio. Si va a realizar la instalación en un clúster de Hyper-V, ejecute el programa de instalación en cada nodo de clúster. Instalar y registrar los nodos de cada clúster de Hyper-V garantiza que las máquinas virtuales permanezcan protegidas incluso si se migran entre nodos.
2. En **Microsoft Update** puede optar por recibir actualizaciones para que las actualizaciones del proveedor se realicen según las directivas de Microsoft Update.
3. En **instalación**, acepte o modifique la ubicación de instalación de proveedor de hello predeterminada y haga clic en **instalar**.
4. En **configuración del almacén**, haga clic en **examinar** tooselect Hola almacén archivo de clave que ha descargado. Especifique la suscripción de Azure Site Recovery Hola, nombre del almacén de hello, y pertenece Hola Hyper-V sitio toowhich Hola Hyper-V server.

    ![Registro de servidor](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. En **configuración de Proxy**, especifique cómo Hola Hola que se ejecutan en hosts de Hyper-V conectará tooAzure Site Recovery por proveedor a internet.

    * Si desea que Hola proveedor tooconnect directamente seleccione **conectarse directamente tooAzure Site Recovery sin un proxy**.
    * Si el proxy existente requiere autenticación, o si desea toouse un proxy personalizado para la conexión del proveedor de hello, seleccione **conectar tooAzure Site Recovery con un servidor proxy**.
    * Si utiliza un proxy:
        - Especifique las credenciales, el puerto y la dirección de Hola
        - Hace que direcciones URL de hello descritas en hello [requisitos previos](#prerequisites) se permiten a través de proxy de Hola.

    ![Internet](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. Una vez finalizada la instalación, haga clic en **registrar** tooregister servidor de hello en el almacén de Hola.

    ![Ubicación de instalación](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. Después de que finalice el registro, Azure Site Recovery recupera metadatos del servidor de Hyper-V de Hola y Hola servidor se muestra en **infraestructura del sitio de recuperación** > **Hosts de Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Configurar el entorno de destino de Hola

Especifique la cuenta de almacenamiento de Azure de hello para la replicación y hello toowhich de red de Azure máquinas virtuales de Azure se conectará tras la conmutación por error.

1. Haga clic en **Preparar infraestructura** > **Destino**.
2. Seleccione la suscripción de Hola y el grupo de recursos de hello en el que desea toocreate Hola máquinas virtuales de Azure después de la conmutación por error. Elija Hola implementación modelo que quiere toouse en Azure (classic o recursos administración) de hello las máquinas virtuales.

3. Site Recovery comprueba que tiene una o más redes y cuentas de Azure Storage compatibles.

    - Si no tienes una cuenta de almacenamiento, haga clic en **+ almacenamiento** toocreate un insertado cuenta basada en el Administrador de recursos. Consulte los [requisitos de almacenamiento](site-recovery-prereq.md#azure-requirements).
    - Si no tiene una red de Azure, haga clic en **+ red** toocreate un insertado de red basada en el Administrador de recursos.

    ![Storage](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>Configuración de las opciones de replicación

1. toocreate una nueva directiva de replicación, haga clic en **preparar infraestructura** > **configuración de replicación** > **+ crear y asociar**.

    ![Red](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. En **Crear y asociar directiva**, especifique un nombre de directiva.
3. En **copiar frecuencia**, especifique la frecuencia con desea tooreplicate diferencias de datos después de la replicación inicial de hello (cada 30 segundos, 5 o 15 minutos).

    > [!NOTE]
    > No se admite una frecuencia de segundo 30 al replicar toopremium almacenamiento. limitación de Hello viene determinado por el número de Hola de instantáneas por blob (100) compatible con almacenamiento premium. [Más información](../storage/storage-premium-storage.md#snapshots-and-copy-blob).

4. En **retención de punto de recuperación**, especifique en horas cuánto tiempo es el período de retención de Hola para cada punto de recuperación. Las máquinas virtuales se pueden recuperar tooany punto dentro de una ventana.
5. En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (entre 1 y 12 horas) con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación.

    - Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de la máquina virtual completa de hello y una instantánea coherente con la aplicación que toma una instantánea de tiempo de punto de datos de la aplicación hello dentro de la máquina virtual de Hola.
    - Las instantáneas coherentes con la aplicación usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola.
    - Si habilita las instantáneas coherentes con la aplicación, afectará al rendimiento de Hola de aplicaciones que se ejecutan en máquinas virtuales de origen. Asegúrese de que el valor de hello especificado es menor que el número de Hola de puntos de recuperación adicionales que configure.

6. En **hora de inicio de la replicación inicial**, especifique cuándo toostart Hola la replicación inicial. se produce la replicación de Hello sobre el ancho de banda de internet por lo que conviene tooschedule que fuera de su horario ocupado. y, a continuación, haga clic en **Aceptar**.

    ![Directiva de replicación](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

Cuando se crea una nueva directiva, automáticamente tiene asociadas con el sitio de Hyper-V de Hola. Puede asociar un sitio de Hyper-V (hello las máquinas virtuales en ella y) con varias directivas de replicación en **replicación** > nombre de directiva > **asociar el sitio de Hyper-V**.

## <a name="capacity-planning"></a>Planificación de capacidad

Ahora que tiene la infraestructura básica configurada, puede planear la capacidad y averiguar si necesita recursos adicionales.

Recuperación de sitio proporciona un toohelp planificador de capacidad asignar los recursos adecuados de hello para el proceso, red y almacenamiento. Puede ejecutar planificador de hello en el modo rápido para realizar cálculos en función de un promedio de las máquinas virtuales, discos y almacenamiento, o en el modo detallado con números personalizados en el nivel de carga de trabajo de Hola. Antes de empezar, necesita realizar lo siguiente:

* Recopilar información sobre su entorno de replicación, incluidas las máquinas virtuales, discos por máquina virtual y almacenamiento por disco.
* Estimación Hola diarios (renovación) velocidad de cambio de los datos replicados. Puede usar hello [planificador de capacidad de réplica de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) toohelp para ello.

1. Haga clic en **descargar** toodownload Hola herramienta y, a continuación, ejecútelo. [Leer el artículo de hello](site-recovery-capacity-planner.md) que acompaña a la herramienta de Hola.
2. ¿Cuando haya terminado, seleccione **Sí** en **han ejecutado Hola Capacity Planner**?

   ![Planificación de capacidad](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

Más información sobre el [control del ancho de banda de red](#network-bandwidth-considerations)



## <a name="enable-replication"></a>Habilitar replicación

Antes de empezar, asegúrese de que la cuenta de usuario de Azure tiene Hola necesario [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una nueva tooAzure de máquina virtual.

Habilite la replicación para máquinas virtuales como sigue:          

1. Haga clic en **Replicar la aplicación** > **Origen**. Una vez haya configurado la replicación para hello la primera vez, puede hacer clic en **+ replicar** tooenable replicación para máquinas adicionales.

    ![Habilitar replicación](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. En **origen**, seleccione el sitio de Hyper-V de Hola. y, a continuación, haga clic en **Aceptar**.
3. En **destino**, seleccione la suscripción de almacén de Hola y Hola modelo de conmutación por error que desee toouse en Azure (classic o recurso management) después de la conmutación por error.
4. Seleccione la cuenta de almacenamiento de Hola que desee toouse. Si no tienes una cuenta que desee toouse, puede [crear uno](#set-up-an-azure-storage-account). y, a continuación, haga clic en **Aceptar**.
5. Seleccione hello Azure toowhich de red y subred de máquinas virtuales de Azure se conectará cuando se crean conmutación por error.

    - Seleccione tooapply Hola configuración tooall máquinas de la red se habilita para la replicación, **configurar ahora para las máquinas seleccionadas**.
    - Seleccione **configurar más adelante** tooselect hello Azure red por máquina.
    - Si no dispone de una red que desee toouse, puede [crear uno](#set-up-an-azure-network). Seleccione una subred si es posible. A continuación, haga clic en **Aceptar**.

   ![Habilitar replicación](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. En **máquinas virtuales** > **seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate. Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación. A continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. En **propiedades** > **configurar las propiedades**, seleccione sistema de operativo Hola Hola selecciona las máquinas virtuales y Hola disco del sistema operativo.
8. Comprueba cumple ese nombre de máquina virtual de Azure (nombre de destino) de hello [requisitos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. De forma predeterminada se seleccionan todos los discos de Hola de hello VM para la replicación, pero puede borrar discos tooexclude ellos.
    - Puede ser conveniente tooexclude discos tooreduce del ancho de banda. Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez que un equipo o en las aplicaciones se reinicia (por ejemplo, pagefile.sys o tempdb de Microsoft SQL Server). Puede excluir disco Hola de replicación por disco de hello anule su selección.
    - Solo se pueden excluir los discos básicos. Los discos del sistema operativo no se pueden excluir.
    - Se recomienda no excluir discos dinámicos. Site Recovery no se puede identificar si un disco duro virtual de una máquina virtual invitada es básico o dinámico. Si no se excluyen todos los discos de los volúmenes dinámicos dependientes, disco dinámico protegido de Hola se mostrará como un disco con errores cuando hello máquina virtual conmuta por error y datos de hello en ese disco no será accesibles.
        - Una vez habilitada la replicación, no puede agregar ni quitar discos para la replicación. Si desea que tooadd o excluir un disco, necesita protección toodisable Hola VM y, a continuación, volver a habilitarla.
        - No se produce una conmutación por recuperación de los discos que se crean manualmente en Azure. Por ejemplo, si se producirá un error en más de tres discos y cree dos directamente en la máquina virtual de Azure, solo Hola tres discos que se han conmutado por error desde Azure tooHyper-V. No se incluyen discos creados manualmente en la conmutación por recuperación, o en la replicación inversa de Hyper-V tooAzure.
        - Si excluye un disco que se necesita para una aplicación toooperate, después de la conmutación por error tooAzure debe toocreate puede ejecutarse manualmente en Azure, por lo que ese saludo replica aplicación. Como alternativa, puede integrar automatización de Azure en un plan de recuperación, disco de hello toocreate durante la conmutación por error de la máquina de Hola.

10. Haga clic en **Aceptar** toosave cambios. Puede establecer propiedades adicionales más adelante.

    ![Habilitar replicación](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. En **configuración de replicación** > **establecer configuración de replicación**, seleccione Directiva de replicación de Hola que desee tooapply para hello protegido máquinas virtuales. y, a continuación, haga clic en **Aceptar**. Puede modificar la directiva de replicación de hello en **directivas de replicación** > nombre de directiva > **modificar configuración**. Los cambios que aplique se utilizarán tanto para las máquinas que ya se estén replicando como para otras nuevas.


   ![Habilitar replicación](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **trabajos** > **trabajos de recuperación del sitio**. Después de hello **finalización de protección** ejecuciones del trabajo Hola máquina está lista para conmutación por error.

### <a name="view-and-manage-vm-properties"></a>Visualización y administración de las propiedades de la máquina virtual

Se recomienda que compruebe las propiedades de Hola de máquina de origen de Hola.

1. En **elementos protegidos**, haga clic en **replican elementos**y seleccione Hola máquina.

    ![Habilitar replicación](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. En **propiedades**, puede ver la replicación y Hola de información de conmutación por error de máquina virtual.

    ![Habilitar replicación](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. En **de proceso y de red** > **propiedades de proceso**, puede especificar el tamaño de nombre y de destino de la máquina virtual de Azure de Hola. Modificar Hola nombre toocomply requisitos de Azure si necesita. También puede ver y modificar la información acerca de la red de destino de hello, subred y dirección IP que se va a asignar toohello máquina virtual de Azure. Tenga en cuenta los siguiente hello:

   * Puede establecer la dirección IP de destino de Hola. Si no proporciona una dirección, Hola conmutado por error equipo usará DHCP. Si establece una dirección que no está disponible en la conmutación por error, se producirá un error en la conmutación por error de Hola. Hola la misma dirección IP de destino puede usarse para la conmutación por error si está disponible en la red de conmutación por error de prueba de Hola Hola dirección.
   * número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de hello, del siguiente modo:

     * Si el número de Hola de adaptadores de red en la máquina de origen de hello es menor o igual toohello de adaptadores permitidas para el tamaño de máquina de destino de hello, a continuación, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.
     * Si número Hola de adaptadores para la máquina virtual de origen de hello supera número Hola permitido para el tamaño de destino de hello después máximo de tamaño de destino de Hola se usará.
     * Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un equipo de destino de Hola tendrá solo un adaptador.     
     * Si Hola máquina virtual tiene varios adaptadores de red se conectarán todos toohello misma red.
     * Si la máquina virtual de hello tiene varios adaptadores de red, a continuación, Hola mostrado en la lista de hello deja de estar hello *predeterminado* adaptador de red de máquina virtual de Azure Hola.

     ![Habilitar replicación](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. En **discos**, puede ver el sistema operativo de Hola y Hola de discos de datos de máquina virtual que se replicarán.

#### <a name="managed-disks"></a>Discos administrados

En **de proceso y de red** > **propiedades de proceso**, puede establecer "Discos administrados por usar" configuración demasiado "Sí" para hello VM si desea que tooattach discos administrados tooyour máquina en tooAzure de migración. Discos administrados simplifica la administración de discos para máquinas virtuales de IaaS de Azure debido a que administra las cuentas de almacenamiento de hello asociadas con discos de máquina virtual de Hola. [Más información sobre discos administrados](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Discos administrados son toohello creado y adjunta máquina virtual sólo una tooAzure de conmutación por error. Al habilitar la protección, datos de máquinas locales seguirán tooreplicate toostorage cuentas.
   Discos administrados pueden crearse únicamente para máquinas virtuales implementadas mediante el modelo de implementación de administrador de recursos de Hola.

  > [!NOTE]
  > Conmutación por recuperación del entorno de Hyper-V de Azure tooon local no se admite actualmente para equipos con discos administrados. Establezca "Discos administrados por uso" demasiado "Sí" Si piensa toomigrate tooAzure de esta máquina.

   - Cuando se establece "Discos administrados por uso" demasiado "Sí", solo conjuntos de disponibilidad de grupo de recursos de hello con "Discos administrados por uso" conjunto demasiado "Sí" estaría disponibles para la selección. Esto es porque las máquinas virtuales con discos administrados sólo puede ser parte de los conjuntos de disponibilidad con el conjunto de propiedades de "Use administrado discos" demasiado "Sí". Asegúrese de crear conjuntos de disponibilidad con el conjunto de propiedades de "Use administrado discos" en función de los discos de intención toouse administrado en la conmutación por error. Del mismo modo, cuando se establece "Discos administrados por uso" demasiado "No", solo conjuntos de disponibilidad de grupo de recursos de hello con "Discos administrados por uso" propiedad establecida demasiado "No" estaría disponibles para la selección. [Más información sobre discos administrados y conjuntos de disponibilidad](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Si la cuenta de almacenamiento de hello usada para la replicación se cifró con cifrado de servicio de almacenamiento en cualquier momento en el tiempo, se producirá un error en la creación de discos administrados durante la conmutación por error. Se puede establecer "Discos administrados por uso" demasiado "No" y vuelva a intentar la conmutación por error o deshabilite la protección de máquina virtual de Hola y proteger tooa cuenta de almacenamiento que no tenía el cifrado del servicio de almacenamiento habilitado en cualquier momento en el tiempo.
  > [Más información sobre el Cifrado del servicio de Storage y los discos administrados](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Implementación de prueba de Hola

implementación de Hola de tootest, puede ejecutar una prueba de conmutación por error para una sola máquina virtual o un plan de recuperación que contiene una o más máquinas virtuales.

### <a name="before-you-start"></a>Antes de comenzar

 - Si desea que tooconnect tooAzure máquinas virtuales mediante RDP después de la conmutación por error, obtenga información acerca de [preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - prueba de toofully necesita toocopy de Active Directory y DNS en el entorno de prueba. [Más información](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

1. toofail a través de un único equipo, en **replican elementos**, haga clic en hello VM > **+ conmutación por error de prueba** icono.
2. toofail a través de una recuperación del plan, en **planes de recuperación**, plan de hello contextual > **conmutación por error de prueba**. un plan de recuperación, toocreate [, siga estas instrucciones](site-recovery-create-recovery-plans.md).
3. En **conmutación por error de prueba**, seleccione toowhich de red de Azure Hola máquinas virtuales de Azure se conectará después de producirse la conmutación por error.
4. Haga clic en **Aceptar** conmutación por error de toobegin Hola. Pueda seguir el progreso haciendo clic en hello VM tooopen sus propiedades o en hello **conmutación por error de prueba** trabajo en nombre de almacén > **trabajos** > **trabajos de recuperación del sitio**.
5. Una vez completada la conmutación por error de hello, también debe poder réplica de hello toosee máquina Azure aparecen en hello portal de Azure > **máquinas virtuales**. Debe asegurarse de que esa máquina virtual de hello es el tamaño adecuado de hello, que ha conectado toohello de red adecuada y que se está ejecutando.
6. Si preparado para las conexiones después de la conmutación por error, debe ser capaz de tooconnect toohello máquina virtual de Azure.
7. Una vez que haya terminado, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación. En **notas** registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. Esto eliminará máquinas virtuales de Hola que se crearon durante la conmutación por error de prueba.

Para obtener más información, lea hello [tooAzure de conmutación por error de prueba](site-recovery-test-failover-to-azure.md) artículo.



## <a name="monitor-hello-deployment"></a>Implementación de Hola de Monitor

Opciones de configuración de monitor hello, estado y el estado de la implementación de Site Recovery:

1. Haga clic en Hola de tooaccess de nombre de almacén de hello **Essentials** panel. En este panel puede realizar un seguimiento de los trabajos de Site Recovery, el estado de la replicación, los planes de recuperación, y el estado y los eventos del servidor.  

    ![Essentials](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. Hola **estado** mosaico puede supervisar servidores de sitio que están experimentando problemas y Hola eventos que ocurran Site Recovery en hello últimas 24 horas. Puede personalizar iconos de Essentials tooshow hello y las distribuciones que son más útil tooyou, incluido el estado de Hola de otros almacenes de copia de seguridad y recuperación de sitio.
3. Puede administrar y supervisar la replicación en hello **replican elementos**, **planes de recuperación**, y **trabajos de recuperación de sitio** iconos. Puede ver más detalles de los trabajos en **Trabajos** > **Trabajos de Site Recovery**.

## <a name="command-line-provider-and-agent-installation"></a>Instalación del agente y del proveedor de línea de comandos

Hola proveedor de Azure Site Recovery y el agente también pueden instalarse mediante Hola después de la línea de comandos. Este método puede ser proveedor de hello tooinstall usado en un núcleo de servidor para Windows Server 2012 R2.

1. Hola proveedor carpeta de instalación de archivos y registro tooa clave de descarga. Por ejemplo, C:\ASR.
2. Desde un símbolo del sistema con privilegios elevados, ejecute a estas instalador de proveedor de comandos tooextract hello:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Ejecute este comando tooinstall componentes hello:

            C:\ASR> setupdr.exe /i
4. A continuación, ejecute estos servidores de hello tooregister de comandos en el almacén de hello:

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
Donde:

* **/ Credenciales de**: parámetro obligatorio que especifica la ubicación de hello en qué Hola se encuentra el archivo de clave de registro  
* **/ FriendlyName**: parámetro obligatorio Nombre hello del servidor de host de Hyper-V de Hola que aparece en el portal de Azure Site Recovery Hola.
* **/proxyAddress**: parámetro opcional que especifica la dirección de saludo del servidor de proxy de Hola.
* **/proxyPort** : parámetro opcional que especifica el puerto de saludo del servidor de proxy de Hola.
* **/ proxyusername**: parámetro opcional que especifica el nombre de usuario de Proxy de hello (si el servidor proxy requiere autenticación).
* **/ proxypassword**: parámetro opcional que especifica Hola contraseña para autenticar con el servidor de proxy de hello (si el servidor proxy requiere autenticación).


## <a name="network-bandwidth-considerations"></a>Consideraciones sobre el ancho de banda de red
Puede usar hello [herramienta de planificación de capacidad de Hyper-V](site-recovery-capacity-planner.md) toocalculate de ancho de banda de Hola que necesita para la replicación (la replicación inicial y, a continuación, delta). cantidad de hello toocontrol de uso de ancho de banda para la replicación tiene algunas opciones:

* **Limitar ancho de banda**: tráfico de Hyper-V que replica tooAzure pasa a través de un host de Hyper-V específico. También puede limitar el ancho de banda en el servidor de host de Hola.
* **Ajustar el ancho de banda**: puede influir en el ancho de banda de hello utilizado para la replicación con un par de claves del registro.

### <a name="throttle-bandwidth"></a>Limitar el ancho de banda
1. Abra Hola MMC de copia de seguridad de Microsoft Azure complemento en el servidor de host de Hyper-V de Hola. De forma predeterminada un acceso directo para copia de seguridad de Microsoft Azure está disponible en el escritorio de Hola o en Agent\bin\wabadmin de servicios de recuperación de C:\Program Files\Microsoft Azure.
2. En el complemento hello, haga clic en **cambiar las propiedades de**.
3. En hello **limitación** ficha seleccione **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet**y establecer los límites de hello para el trabajo y no laborables horas. Intervalo válido es de 512 Kbps too102 Mbps por segundo.

    ![Limitar el ancho de banda](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

También puede usar hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitación. Aquí tiene un ejemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que no se requiere ninguna limitación.

### <a name="influence-network-bandwidth"></a>Control del uso de ancho de banda de red
1. En el registro de hello navegue demasiado**Backup\Replication de Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.
   * tráfico de ancho de banda de hello tooinfluence en un disco de la replicación, modificar Hola Hola de valor **UploadThreadsPerVM**, también puede crear la clave de hello si no existe.
   * ancho de banda de tooinfluence hello para el tráfico de la conmutación por recuperación de Azure, modifique el valor de hello **DownloadThreadsPerVM**.
2. valor predeterminado de Hello es 4. En una red de "sobreaprovisionada", estas claves del registro deben cambiarse de valores predeterminados de Hola. Hola máximo es 32. Supervisar el tráfico toooptimize Hola valor.

## <a name="next-steps"></a>Pasos siguientes

Después de la replicación inicial se ha completado y ha probado la implementación de hello, puede invocar las conmutaciones por error según sea necesario Hola. [Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.
