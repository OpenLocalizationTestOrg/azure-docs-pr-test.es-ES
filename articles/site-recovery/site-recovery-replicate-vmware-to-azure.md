---
title: Replicar aplicaciones (VMware tooAzure) | Documentos de Microsoft
description: "Este artículo describe cómo ejecutar los equipos de tooset la replicación de memoria virtual de VMware en Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: asgang
ms.openlocfilehash: b07aabdacec521c7bd89e50f6a1427a774ff0287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-applications-running-on-vmware-vms-tooazure"></a>Replicar aplicaciones que se ejecutan en máquinas virtuales VMware tooAzure



Este artículo describe cómo ejecutar los equipos de tooset la replicación de memoria virtual de VMware en Azure.
## <a name="prerequisites"></a>Requisitos previos

artículo de Hola se supone que ya ha

1.  [Configuración del entorno de origen local](site-recovery-set-up-vmware-to-azure.md)
2.  [Configuración del entorno de destino en Azure](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>Habilitar replicación
#### <a name="before-you-start"></a>Antes de comenzar
Al replicar máquinas virtuales de VMware, tenga en cuenta que:

* Su cuenta de usuario de Azure necesita toohave determinados [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una nueva tooAzure de máquina virtual.
* Las máquinas virtuales de VMware se detectan cada 15 minutos. Puede tardar 15 minutos o más para ellos tooappear en portal de hello después de la detección. Del mismo modo, la detección podría tardar 15 minutos o más si agrega un servidor vCenter o host vSphere nuevos.
* Cambios en el entorno en la máquina virtual de hello (como la instalación de herramientas de VMware) pueden tardar 15 minutos o más toobe actualizado en el portal de Hola.
* Puede comprobar Hola último detectado tiempo para las máquinas virtuales de VMware en hello **último contacto a** field para hello vCenter server o host de vSphere, en hello **servidores de configuración** hoja.
* máquinas de tooadd para la replicación sin esperar la detección programada de hello, resalte el servidor de configuración de hello (no haga clic en él) y haga clic en hello **actualizar** botón.
* Cuando se habilita la replicación, si está preparado máquina hello, servidor de procesos de Hola instala automáticamente el servicio de movilidad de hello en él.


**Ahora habilite la replicación como sigue**:

1. Haga clic en **Paso 2: Replicar la aplicación** > **Origen**. Después de habilitar la replicación para hello la primera vez, haga clic en **+ replicar** en la replicación de tooenable de almacén de Hola para máquinas adicionales.
2. Hola **origen** hoja > **origen**, seleccione servidor de configuración de Hola.
3. En **Tipo de máquina**, seleccione **Máquinas virtuales** o **Máquinas físicas**.
4. En **vCenter/vSphere hipervisor**, seleccione servidor de vCenter Hola que administra el host de vSphere hello, o host Hola. Esta configuración es relevante si va a replicar máquinas físicas.
5. Seleccione el servidor de procesos de Hola. Si no ha creado ningún servidor de proceso adicionales esto será el nombre de Hola Hola del servidor de configuración. y, a continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. En **destino** seleccione suscripción de Hola y el grupo de recursos de Hola donde desea hello toocreate conmutado por error máquinas virtuales. Elija el modelo de implementación de Hola que desee toouse en Azure (classic o recurso management) para hello conmutado por error máquinas virtuales.
7. Seleccione la cuenta de almacenamiento de Azure de Hola que desee toouse para la replicación de datos. Observe lo siguiente:

   * Puede seleccionar una cuenta de almacenamiento Estándar o Premium. Si selecciona una cuenta de premium, necesitará una cuenta de almacenamiento estándar adicional toospecify para registros de replicación en curso. Cuentas deben estar en hello misma región que hello del almacén de servicios de recuperación.
   * Si desea toouse una cuenta de almacenamiento diferentes que los tiene, puede crear una*vínculo de marcador de posición para la creación de cuenta de almacenamiento con recursos el administrador que se explicará en getting started*. Haga clic en una cuenta de almacenamiento mediante el Administrador de recursos de toocreate **crear nuevo**. Si desea toocreate una cuenta de almacenamiento con el modelo clásico de hello, hace que [Hola portal de Azure](../storage/common/storage-create-storage-account.md).

8. Seleccione hello Azure toowhich de red y subred de máquinas virtuales de Azure se conectará, cuando se active después de la conmutación por error. Hola red debe estar en hello misma región que hello del almacén de servicios de recuperación. Seleccione **configurar ahora para las máquinas seleccionadas**, tooapply Hola red configuración tooall máquinas que seleccione para la protección. Seleccione **configurar más adelante** tooselect hello Azure red por máquina. Si no tiene una red, necesita demasiado[crear uno](#set-up-an-azure-network). Haga clic en una red mediante el Administrador de recursos, toocreate **crear nuevo**. Si desea toocreate una red con el modelo clásico de hello, hacerlo [Hola portal de Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Seleccione una subred si es posible. A continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. En **máquinas virtuales** > **seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate. Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación. A continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. En **propiedades** > **configurar las propiedades**, seleccione cuenta de hello que va a utilizar Hola proceso servidor tooautomatically instale servicio de movilidad de hello en la máquina de Hola.  
11. De manera predeterminada se replican todos los discos. discos tooexclude de la replicación, haga clic en **todos los discos** y desactive los discos que no desea tooreplicate.  y, a continuación, haga clic en **Aceptar**. Puede establecer propiedades adicionales más adelante. [Obtenga más información](site-recovery-exclude-disk.md) sobre cómo excluir discos.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. En **configuración de replicación** > **establecer configuración de replicación**, compruebe que Hola correcto se selecciona la directiva de replicación. Puede modificar la configuración de la directiva de replicación en **Configuración** > **Directivas de replicación** > nombre de directiva > **Editar configuración**. Cambios que aplique la directiva de tooa será tooreplicating aplicado y nuevas máquinas.
13. Habilitar **coherencia entre varias VM** si desea toogather máquinas en un grupo de replicación y especifique un nombre para el grupo de Hola. y, a continuación, haga clic en **Aceptar**. Observe lo siguiente:

    * Todas las máquinas de un grupo de replicación se replican al mismo tiempo y comparten puntos de recuperación coherentes con los bloqueos y coherentes con la aplicación cuando conmutan por error.
    * Se recomienda que recopile las máquinas virtuales y los servidores físicos juntos para que reflejen las cargas de trabajo. Habilitar la coherencia entre varias VM puede afectar al rendimiento de la carga de trabajo y solo debe usarse si las máquinas ejecutan Hola necesita la misma carga de trabajo y coherencia.

    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Haga clic en **Enable Replication**. Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **configuración** > **trabajos** > **trabajos de recuperación de sitio**. Después de hello **finalización de protección** ejecuciones del trabajo Hola máquina está lista para conmutación por error.

> [!NOTE]
> Si la máquina de hello está preparado para Hola de instalación de inserción cuando está habilitada la protección, se instalará el componente de servicio de movilidad. Después de hello componente está instalado en produce un error y máquina Hola que inicia un trabajo de protección. Después de un error de hello debe toomanually reiniciar cada máquina. Tras la protección de Hola de reinicio de hello trabajo comienza de nuevo y se produce la replicación inicial.
>
>

## <a name="view-and-manage-vm-properties"></a>Visualización y administración de las propiedades de la máquina virtual

Se recomienda que compruebe las propiedades de Hola de máquina de origen de Hola. Recuerde que ese nombre de máquina virtual de Azure Hola debe cumplir con los [requisitos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Haga clic en **configuración** > **replican elementos** > y seleccione Hola máquina. Hola **Essentials** hoja muestra información sobre la configuración de máquinas y estado.
2. En **propiedades**, puede ver la replicación y Hola de información de conmutación por error de máquina virtual.
3. En **de proceso y de red** > **propiedades de proceso**, puede especificar el tamaño de nombre y de destino de la máquina virtual de Azure de Hola. Modificar Hola nombre toocomply requisitos de Azure si necesita.
    ![Habilitar replicación](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  Puede seleccionar un [grupo de recursos](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) del cual la máquina formará parte de la conmutación por error posterior. Puede cambiar esta configuración en cualquier momento antes de una conmutación por error. POST conmutar por error, si migra Hola máquina tooa otro grupo de recursos, a continuación, se interrumpirá la configuración de protección de una máquina.
5. Puede seleccionar una [conjunto de disponibilidad](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) si su equipo requiere toobe formar parte de una publicación conmutación por error. Al seleccionar el conjunto de disponibilidad, tenga en cuenta lo siguiente:

    * Solo conjuntos de disponibilidad toohello pertenecientes especificado se enumerarán grupo de recursos  
    * Las máquinas con distintas redes virtuales no pueden formar parte del mismo conjunto de disponibilidad.
    * Solo las máquinas virtuales del mismo tamaño pueden formar parte del mismo conjunto de disponibilidad.
5. También puede ver y agregar información acerca de la red de destino de hello, subred y dirección IP que se va a asignar toohello máquina virtual de Azure.
6. En **discos**, puede ver el sistema operativo de Hola y Hola de discos de datos de máquina virtual que se replicarán.

### <a name="network-adapters-and-ip-addressing"></a>Adaptadores de red y direccionamiento IP 

- Puede establecer la dirección IP de destino de Hola. Si no proporciona una dirección, Hola conmutado por error equipo usará DHCP. Si establece una dirección que no está disponible en la conmutación por error, conmutación por error de hello no funcionará. Hola la misma dirección IP de destino puede usarse para la conmutación por error si está disponible en la red de conmutación por error de prueba de Hola Hola dirección.
- número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de hello, del siguiente modo:
    - Si el número de Hola de adaptadores de red en la máquina de origen de hello es menor o igual toohello de adaptadores permitidas para el tamaño de máquina de destino de hello, a continuación, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.
    - Si número Hola de adaptadores para la máquina virtual de origen de hello supera número Hola permitido para el tamaño de destino de hello después máximo de tamaño de destino de Hola se usará.
    - Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un equipo de destino de Hola tendrá solo un adaptador.
    - Si la máquina virtual de hello tiene varios adaptadores de red se conectarán todos toohello misma red.
    - Si la máquina virtual de hello tiene varios adaptadores de red, a continuación, Hola mostrado en la lista de hello deja de estar hello *predeterminado* adaptador de red de máquina virtual de Azure Hola.
   



## <a name="common-issues"></a>Problemas comunes

* Cada disco debe tener menos de 1 TB de tamaño.
* Hola SO disco debe ser un disco básico y dinámico no
* Generación 2/UEFI habilitada máquinas virtuales, familia del sistema operativo Hola debe ser Windows y disco de arranque debe ser inferior a 300GB

## <a name="next-steps"></a>Pasos siguientes

Una vez completada la protección de hello, puede intentar [una conmutación por error](site-recovery-failover.md) toocheck si la aplicación aparece en Azure o no.

En caso de que desee toodisable protección, consulte cómo demasiado[limpiar la configuración del registro y la protección](site-recovery-manage-registration-and-protection.md)
