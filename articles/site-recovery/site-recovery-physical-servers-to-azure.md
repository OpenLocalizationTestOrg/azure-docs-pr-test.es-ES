---
title: "Replicación de servidores físicos en Azure | Microsoft Docs"
description: "Se describe cómo implementar Azure Site Recovery para orquestar la replicación, la conmutación por error y la recuperación de servidores físicos de Windows o Linux locales en Azure mediante Azure Portal."
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
ms.openlocfilehash: a9655ce1540c788d02d178eb619d2051cddda1c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
---
# <a name="replicate-physical-machines-to-azure-by-using-site-recovery"></a>Replicar máquinas físicas en Azure mediante Site Recovery


En este artículo, se describe cómo replicar máquinas físicas locales en Azure mediante el servicio Azure Site Recovery en Azure Portal.

Si quiere migrar máquinas físicas a Azure (solo conmutación por error), lea [Migración a Azure con Site Recovery](site-recovery-migrate-to-azure.md) para obtener más información.

Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Requisitos previos

**Requisito de compatibilidad** | **Detalles**
--- | ---
**Las tablas de Azure** | Obtenga información sobre los [requisitos de Azure](site-recovery-prereq.md#azure-requirements)
**Servidor de configuración local** | Máquina local (física o máquina virtual de VMWare) con Windows Server 2012 R2 o versiones posteriores. Configure el servidor de configuración durante la implementación de Site Recovery.<br/><br/> De forma predeterminada, el servidor de procesos y el servidor de destino maestro también están instalados en esta máquina. Al escalar una verticalmente, podría necesitar un servidor de procesos independiente, con los mismos requisitos que el servidor de configuración.<br/><br/> Puede obtener más información sobre estos componentes en [Configuración del entorno de origen](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**Máquinas virtuales locales** | Las máquinas que quiera replicar deben ejecutar un [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) y cumplir los [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs** | El servidor de configuración necesita acceso a estas direcciones URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si tiene reglas de firewall basadas en direcciones IP, asegúrese de que permitan la comunicación con Azure.<br/></br> Permita los [intervalos IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) y el puerto HTTPS (443).<br/></br> Permita los intervalos de direcciones IP correspondientes a la región de Azure de su suscripción y del oeste de EE. UU. (se usan para Access Control y para Identity Management).<br/><br/> Permita esta dirección URL para la descarga de MySQL: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Servicio de movilidad** | Este servicio se instalará en cada máquina que quiera replicar.

## <a name="limitations"></a>Limitaciones

**Limitación** | **Detalles**
--- | ---
**Las tablas de Azure** | Las cuentas de almacenamiento y de red deben estar en la misma región que el almacén.<br/><br/> Si usa una cuenta de Premium Storage, también necesita una cuenta de almacenamiento estándar para almacenar los registros de replicación.<br/><br/> No se puede replicar en cuentas premium en el centro y sur de la India.
**Servidor de configuración local** | Si instala el servidor de configuración en una máquina virtual de VMware, el tipo de adaptador de máquina virtual debe ser VMXNET3. Si no lo es, [instale esta actualización](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Si usa una máquina virtual de VMware, debe instalar vSphere PowerCLI 6.0 en ella.<br/><br> La máquina no debe ser un controlador de dominio.<br/><br/> La máquina debe tener una dirección IP estática.<br/><br/> El nombre de host debe tener 15 caracteres o menos, y el sistema operativo debe estar en inglés.
**Máquinas replicadas** | Compruebe las [limitaciones de las VM de Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Si quiere habilitar la coherencia de múltiples máquinas virtuales, lo que permite que las máquinas que ejecuten la misma carga de trabajo se recuperen juntas en un punto de datos coherente, abra el puerto 20004 en la máquina.<br/><br/> Se admiten tipos específicos de [almacenamiento Linux](site-recovery-support-matrix-to-azure.md#support-for-storage).
**Conmutación por recuperación** | No se puede realizar la conmutación por recuperación a Azure en una máquina física. Si quiere poder realizar la conmutación por recuperación en la ubicación local después de la conmutación por error, necesitará un entorno de VMware para así poder realizar la conmutación por recuperación en una máquina virtual de VMware.


## <a name="set-up-azure"></a>Configuración de Azure

1. [Configure una red de Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. Las VM de Azure se colocarán en esta red cuando se creen después de la conmutación por error.

      b. Puede configurar una red en el modo de Azure [Resource Manager](../resource-manager-deployment-model.md) o en el clásico.

2. Configure una [cuenta de Azure Storage](../storage/storage-create-storage-account.md#create-a-storage-account) para los datos replicados.

    a. La cuenta puede ser estándar o [premium](../storage/storage-premium-storage.md).

    b. Puede configurar una cuenta en el modo de Resource Manager o en el clásico.

## <a name="prepare-the-configuration-server"></a>Preparar el servidor de configuración

1. Instale Windows Server 2012 R2 o una versión posterior en un servidor físico local o una máquina virtual de VMware.

2. Asegúrese de que la máquina tenga acceso a las direcciones URL que se indican en la sección [Requisitos previos](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Preparación para la instalación del Servicio de Movilidad

Si quiere insertar el servicio de movilidad en una máquina física, necesita una cuenta que el servidor de procesos pueda usar para acceder a las máquinas. La cuenta solo se usa para la instalación de inserción. Puede usar una cuenta local o de dominio:

  - Para Windows, si no utiliza una cuenta de dominio, debe deshabilitar el control de acceso de usuario remoto en la máquina local. Para ello, en el Registro, en **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, agregue la entrada DWORD **LocalAccountTokenFilterPolicy** con un valor de 1. Si desea agregar la entrada del Registro de Windows desde una interfaz de la línea de comandos, escriba:

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Para Linux, la cuenta debe ser un usuario raíz en el servidor Linux de origen.


## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-the-protection-goal"></a>Selección del objetivo de protección

Seleccione aquello que desea replicar y la ubicación en donde se va a realizar la replicación.

1. Haga clic en **Almacenes de Recovery Services** > **almacén**.
2. En el menú **Recurso**, haga clic en **Site Recovery** > **Preparar la infraestructura** > **Objetivo de protección**.

    ![Elegir objetivos](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. En **Objetivo de protección**, seleccione **En Azure** > **No virtualizado/Otro**.


## <a name="set-up-the-source-environment"></a>Configuración del entorno de origen

Configure el servidor de configuración, regístrelo en el almacén y detecte máquinas virtuales.

1. Haga clic en **Site Recovery** > **Preparar la infraestructura** > **Origen**.
2. Si no tiene un servidor de configuración, haga clic en **+Servidor de configuración**.

    ![Configurar origen](./media/site-recovery-vmware-to-azure/set-source1.png)

3. En **Agregar servidor**, compruebe que aparezca **Servidor de configuración** en **Tipo de servidor**.
4. Descargue el archivo de **instalación unificada de Site Recovery**.
5. Descargue la **clave de registro del almacén**. Se le solicitará cuando ejecute la instalación unificada. La clave será válida durante cinco días a partir del momento en que se genera.

   ![Configurar origen](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Ejecución de la instalación unificada de Site Recovery

Antes de empezar, haga lo siguiente:

- Vea un vídeo introductorio rápido (el vídeo describe cómo replicar máquinas virtuales de VMware, pero el proceso es similar para la replicación de máquinas físicas).

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- En la máquina del servidor de configuración, asegúrese de que el reloj del sistema está sincronizado con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Si hay una diferencia de 15 minutos, antes o después, se podría producir un error en la instalación.
- Ejecute la instalación como Administrador local en la máquina del servidor de configuración.
- Asegúrese de que TLS 1.0 está habilitado en la máquina.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> El servidor de configuración también se puede instalar [desde la línea de comandos](http://aka.ms/installconfigsrv).


## <a name="set-up-the-target-environment"></a>Configuración del entorno de destino

Antes de configurar el entorno de destino, asegúrese de tener una [cuenta y una red de Azure Storage](#set-up-azure).

1. Haga clic en **Preparar infraestructura** > **Destino** y seleccione la suscripción a Azure que quiere usar.
2. Especifique si el modelo de implementación de destino está basado en Resource Manager o si es el clásico.
3. Site Recovery comprueba que tenga una o más cuentas y redes de Azure Storage compatibles.

   ![Destino](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Si no creó una cuenta de almacenamiento ni una red, haga clic en **+Cuenta de almacenamiento** o **+Red** para crear una cuenta o red de Resource Manager en línea.

## <a name="set-up-replication-settings"></a>Configuración de las opciones de replicación

Antes de empezar, vea un vídeo introductorio rápido (el vídeo describe cómo replicar máquinas virtuales de VMware, pero el proceso es similar para la replicación de máquinas físicas).

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. Para crear una directiva de replicación, haga clic en **Site Recovery Infrastructure (Infraestructura de Site Recovery)** > **Directivas de replicación** > **+Directiva de replicación**.
2. En **Crear directiva de replicación**, especifique un nombre de directiva.
3. En **Umbral de RPO**, especifique el límite de RPO. Este valor especifica la frecuencia con que se crean puntos de recuperación de datos. Se genera una alerta cuando la replicación continua supera este límite.
4. En **Retención de punto de recuperación**, especifique (en horas) la duración del período de retención para cada punto de recuperación. Las máquinas virtuales replicadas se pueden recuperar a cualquier momento de un período. Se admite una retención de hasta 24 horas para máquinas replicadas en Premium Storage. Se admite una retención de hasta 72 horas para máquinas replicadas en almacenamiento estándar.
5. En **Frecuencia de instantánea coherente con la aplicación**, especifique la frecuencia (en minutos) con la que se crearán puntos de recuperación que contengan las instantáneas coherentes con la aplicación. Haga clic en **Aceptar** para crear la directiva.

    ![Directiva de replicación](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Cuando se crea una nueva directiva, esta se asocia automáticamente con el servidor de configuración. De forma predeterminada, se crea automáticamente una directiva correspondiente para la conmutación por recuperación. Por ejemplo, si la directiva de replicación es **rep-policy**, la directiva de conmutación por recuperación será **rep-policy-failback**. Esta directiva no se usa hasta que se inicie una conmutación por recuperación desde Azure.  


## <a name="plan-capacity"></a>Planeamiento de la capacidad

1. Ahora que tiene la infraestructura básica configurada, puede planear la capacidad y averiguar si necesitará recursos adicionales. [Más información](site-recovery-plan-capacity-vmware.md).
2. Seleccione **Sí** en **¿Completó el planeamiento de capacidad?** cuando haya terminado de planear la capacidad.

   ![Planificación de capacidad](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Preparación de las máquinas virtuales para la replicación

Todas las máquinas que desee replicar deben tener instalado el servicio de movilidad. Puede instalarlo de varias maneras:

- Instale el servicio con una instalación de inserción desde el servidor de procesos. Debe preparar las máquinas con antelación para usar este método.
- Instale el servicio con herramientas de implementación como System Center Configuration Manager o Desired State Configuration de Azure Automation.
- Instale el servicio manualmente.

[Más información](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>Habilitar replicación

Antes de comenzar:

- Su cuenta de usuario de Azure debe tener ciertos [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) para habilitar la replicación de una nueva máquina virtual en Azure.
- Cuando agregue o modifique máquinas virtuales, los cambios pueden tardar 15 minutos o más en aplicarse y aparecer en el portal.
- Puede comprobar la hora de la última detección de máquinas virtuales en **Servidores de configuración** > **Último contacto a las**.
- Para agregar máquinas virtuales sin esperar a la detección programada, resalte el servidor de configuración (no haga clic en él) y haga clic en **Actualizar**.
- Si se prepara una máquina virtual para la instalación de inserción, el servidor de procesos instala automáticamente el servicio de movilidad cuando habilita la replicación.
- Vea un vídeo introductorio rápido (el vídeo describe cómo replicar máquinas virtuales de VMware, pero el proceso es similar para la replicación de máquinas físicas).

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Excluir discos de la replicación

De manera predeterminada, se replican todos los discos de una máquina. Puede excluir discos de la replicación. Por ejemplo, es posible que no quiera replicar los discos con datos temporales o los datos que se actualizan cada vez que una máquina o aplicación se reinicia (por ejemplo, pagefile.sys o tempdb de SQL Server).

### <a name="replicate-vms"></a>Replicación de máquinas virtuales

1. Haga clic en **Replicar la aplicación** > **Origen**.
2. En **Origen**, seleccione **Local**.
3. En **Ubicación de origen**, seleccione el nombre del servidor de configuración.
4. En **Tipo de máquina**, seleccione **Máquinas físicas**.
5. En **Servidor de procesos**, elija el servidor de procesos. Si no creó ningún servidor de procesos adicional, este será el servidor de configuración. A continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/chooseVM.png)

6. En **Destino**, seleccione la **suscripción** y el **grupo de recursos** donde quiere crear las VM de Azure después de la conmutación por error. Elija el modelo de implementación que quiera usar en Azure (clásico o de Resource Manager) para las máquinas virtuales conmutadas por error.

7. Seleccione la cuenta de Azure Storage que desea usar para los datos de replicación. Si no desea usar una cuenta que ya haya configurado, puede crear una.

8. Seleccione la **red** y la **subred de Azure** a la que se conectarán las VM de Azure después de la conmutación por error. Seleccione la opción **Configurar ahora para las máquinas seleccionadas** con el fin de aplicar la configuración de red a todas las máquinas que seleccione para su protección. Seleccione **Configurar más tarde** para seleccionar la red de Azure por máquina. Si no desea usar una red existente, puede crear una.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/targetsettings.png)

9. En **Máquinas físicas**, haga clic en **Agregar máquina física** y escriba el **Nombre** y la **Dirección IP**. Elija el sistema operativo de la máquina que quiere replicar. Se tardará unos minutos hasta que las máquinas se detecten y se muestren en la lista.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/machineselect.png)

10. En **Propiedades** > **Configurar propiedades**, seleccione la cuenta que usará el servidor de procesos para instalar automáticamente el servicio de movilidad en la máquina.
11. De manera predeterminada se replican todos los discos. Haga clic en **Todos los discos** y desactive todos los discos que no quiera replicar. A continuación, haga clic en **Aceptar**. Puede establecer otras propiedades de las máquinas virtuales más adelante.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/configprop.png)

12. En **Configuración de la replicación** > **Establecer configuración de replicación**, compruebe que se haya seleccionado la directiva de replicación correcta. Si modifica una directiva, los cambios se aplicarán a la máquina que se replica y a las nuevas máquinas.
13. Habilite la **coherencia de múltiples VM** si desea recopilar las máquinas en un grupo de replicación y especifique un nombre para el grupo. y, a continuación, haga clic en **Aceptar**. Observe lo siguiente:

    a. Todas las máquinas de un grupo de replicación se replican al mismo tiempo y comparten puntos de recuperación coherentes con los bloqueos y con la aplicación cuando conmutan por error.

    b. Se recomienda que recopile las máquinas virtuales y los servidores físicos juntos para que reflejen las cargas de trabajo. La habilitación de la coherencia entre varias VM puede afectar al rendimiento de la carga de trabajo. Debe usarse únicamente si las máquinas ejecutan la misma carga de trabajo y necesita coherencia.

    ![Habilitar replicación](./media/site-recovery-physical-to-azure/policy.png)

14. Haga clic en **Enable Replication**. Puede hacer un seguimiento del progreso del trabajo **Habilitar protección** en **Configuración** > **Trabajos** > **Trabajos de Site Recovery**. La máquina estará preparada para la conmutación por error después de que finalice el trabajo **Finalizar la protección**.

Después de habilitar la replicación, se instalará el servicio de movilidad si configura la instalación de inserción. Después de instalar el servicio de movilidad por inserción en una máquina, se inicia un trabajo de protección y se produce un error. Debe reiniciar manualmente cada máquina después del error. Después, se vuelve a iniciar el trabajo de protección y se produce la replicación inicial.


### <a name="view-and-manage-azure-vm-properties"></a>Ver y administrar las propiedades de la máquina virtual de Azure

Se recomienda que compruebe las propiedades de máquina virtual y realice todos los cambios necesarios.

1. Haga clic en **Elementos replicados** y seleccione la máquina. En la hoja **Información esencial** se detalla la configuración y el estado de las máquinas.
2. En **Propiedades** puede ver la información de replicación y conmutación por error de la máquina virtual.
3. En **Compute y Network** > **Propiedades de Compute**, puede especificar el nombre y el tamaño de destino de la máquina virtual de Azure. Modifique el nombre para que cumpla con los [requisitos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) si es necesario.
4. Modifique la configuración de la red de destino, la subred y la dirección IP asignadas a la VM de Azure:

    a. Puede establecer la dirección IP de destino.

    b.  Si no proporciona ninguna dirección, la máquina conmutada por error usará DHCP.

    c. Si establece una dirección que no esté disponible en el momento de la conmutación por error, esta operación no funcionará.

    d. Se puede utilizar la misma dirección IP de destino para la conmutación por error de prueba si la dirección está disponible en la red.

    e. El número de adaptadores de red viene determinado por el tamaño que especifique para la máquina virtual de destino:

     - Si el número de adaptadores de red en la máquina de origen es igual o menor que el número de adaptadores permitido para el tamaño de la máquina de destino, el destino tiene el mismo número de adaptadores que el origen.
     - Si el número de adaptadores para la máquina virtual de origen supera el número permitido para el tamaño de destino, entonces se utilizará el tamaño máximo de destino.
     - Por ejemplo, si una máquina de origen tiene dos adaptadores de red y el tamaño de la máquina de destino admite cuatro, el equipo de destino tiene dos adaptadores. Si la máquina de origen tiene dos adaptadores pero el tamaño de destino compatible solo admite uno, la máquina de destino tiene solo un adaptador.     
   - Si la máquina virtual tiene varios adaptadores de red, todos ellos se conectan a la misma red.
   - Si la máquina virtual tiene varios adaptadores de red, el primero de ellos que se muestre en la lista se convertirá en el *predeterminado* en la VM de Azure.
5. En **Discos**, se ven el sistema operativo de la VM y los discos de datos replicados.

## <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

Una vez terminada la configuración, ejecute una conmutación por error de prueba para asegurarse de que todo funcione de la forma esperada. Vea un vídeo introductorio rápido antes de empezar.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. Para conmutar por error una sola máquina, en **Configuración** > **Elementos replicados**, haga clic en **Conmutación por error de prueba**.

    ![Probar conmutación por error](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. Para conmutar por error un plan de recuperación, en **Configuración** > **Planes de recuperación**, haga clic con el botón derecho en el plan > **Probar conmutación por error**. Para crear un plan de recuperación, [siga estas instrucciones](site-recovery-create-recovery-plans.md).  
3. En **Conmutación por error de prueba**, seleccione la red de Azure a la que se conectan las VM de Azure después de la conmutación por error.
4. Haga clic en **Aceptar** para iniciar la conmutación por error. Para realizar un seguimiento del progreso, haga clic en la VM para abrir sus propiedades o en el trabajo **Conmutación por error de prueba** en Nombre del almacén > **Configuración** > **Trabajos** > **Trabajos de Site Recovery**.
5. Cuando se complete la conmutación por error, debería ver la máquina de réplica de Azure en Azure Portal > **Máquinas virtuales**. Debe asegurarse de que la VM tiene el tamaño adecuado, que está conectada a la red correspondiente y que se está ejecutando.
6. Si se [preparó para las conexiones después de la conmutación por error](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), debe ser capaz de conectarse a la máquina virtual de Azure.
7. Cuando termine, haga clic en **Limpiar conmutación por error de prueba** en el plan de recuperación. En **Notas**, registre y guarde las observaciones asociadas a la conmutación por error de prueba. Con este paso, se eliminan las máquinas virtuales que se crearon durante la conmutación por error de prueba.

Para obtener más información, consulte el documento sobre la [conmutación por error de prueba a Azure](site-recovery-test-failover-to-azure.md).

## <a name="next-steps"></a>Pasos siguientes

Después de poner en funcionamiento la replicación, cuando se produce una interrupción, se conmuta por error a Azure y se crean máquinas virtuales de Azure a partir de los datos replicados. Entonces, puede acceder a cargas de trabajo y aplicaciones en Azure, hasta que conmute por recuperación a la ubicación principal cuando vuelva a funcionar de forma normal.

- [Obtenga más información](site-recovery-failover.md) sobre los diferentes tipos de conmutación por error y cómo ejecutarlos.
- Si migra máquinas en lugar de replicar y conmutar por recuperación, [lea más](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- Al replicar máquinas físicas, solo puede conmutar por recuperación a un entorno de VMWare. [Lea acerca de la conmutación por recuperación](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Avisos e información de software de terceros
Do Not Translate or Localize

The software and firmware running in the Microsoft product or service is based on or incorporates material from the projects listed below (collectively, “Third Party Code”). Microsoft is the not original author of the Third Party Code. The original copyright notice and license, under which Microsoft received such Third Party Code, are set forth below.

The information in Section A is regarding Third Party Code components from the projects listed below. Such licenses and information are provided for informational purposes only. This Third Party Code is being relicensed to you by Microsoft under Microsoft's software licensing terms for the Microsoft product or service.  

The information in Section B is regarding Third Party Code components that are being made available to you by Microsoft under the original licensing terms.

The complete file may be found on the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
