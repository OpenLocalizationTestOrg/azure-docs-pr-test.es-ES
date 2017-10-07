---
title: "aaaRun una conmutación por error de prueba para VMware replicación tooAzure | Documentos de Microsoft"
description: "Resume los pasos de Hola que necesita para ejecutar una prueba de conmutación por error para replicar tooAzure mediante el servicio de Azure Site Recovery Hola de las máquinas virtuales de VMware."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bed934446f0c6940089bfae24a13de4fb1556a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-12-run-a-test-failover-tooazure-for-vmware-vms"></a>Paso 12: Ejecutar una tooAzure de conmutación por error de prueba para las máquinas virtuales de VMware

Este artículo describe cómo toorun una prueba de conmutación por error de local VMware virtual máquinas tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de comenzar

Antes de ejecutar una conmutación por error de prueba que se recomienda que compruebe las propiedades de la máquina virtual de Hola y realice los cambios necesite. puede tener acceso a propiedades de la máquina virtual de hello en **replican elementos**. Hola **Essentials** hoja muestra información sobre la configuración de máquinas y estado.

## <a name="managed-disk-considerations"></a>Consideraciones sobre discos administrados

[Discos administrados por](../virtual-machines/windows/managed-disks-overview.md) simplificar la administración de disco para máquinas virtuales de Azure, debido a que administra las cuentas de almacenamiento de hello asociadas con discos de máquina virtual de Hola. 

- Al habilitar la protección para una máquina virtual, datos de máquinas virtuales replican tooa cuenta de almacenamiento. Discos administrados se crean y adjunta toohello VM solo cuando se produce la conmutación por error.
- Discos administrados pueden crearse únicamente para máquinas virtuales implementadas mediante el modelo de administrador de recursos de Hola.  
- Con esta opción habilitada, solo se pueden seleccionar los conjuntos de disponibilidad de los grupos de recursos que tienen habilitada la opción **Usar discos administrados**. Las máquinas virtuales con discos administrados deben estar en conjuntos de disponibilidad con **discos administrados por uso** establecido demasiado**Sí**. Si no está habilitada la configuración de Hola para las máquinas virtuales, pueden seleccionarse conjuntos de disponibilidad solo en grupos de recursos sin discos administrados habilitados.
- Obtenga [más información](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) sobre discos administrados y conjuntos de disponibilidad.
- Si la cuenta de almacenamiento de hello que utiliza para la replicación se ha cifrado con cifrado de servicio de almacenamiento, no se puede crear discos administrados durante la conmutación por error. En este caso cualquiera no habilitar el uso de discos administrados, o deshabilite la protección de hello VM y volver a habilitar toouse una cuenta de almacenamiento que no tiene habilitado el cifrado. [Más información](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="network-considerations"></a>Consideraciones sobre la red

Puede establecer la dirección IP de destino de Hola para una máquina virtual de Azure creado después de la conmutación por error.

- Si no proporciona una dirección, Hola conmutado por error equipo usará DHCP.
- Si establece una dirección que no esté disponible en el momento de la conmutación por error, esta no funcionará.
- Hola la misma dirección IP de destino puede usarse para conmutación por error de prueba, si está disponible en la red de conmutación por error de prueba de Hola Hola dirección.
- número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de hello:

     - Si Hola algunos adaptadores de red de máquina de origen de Hola Hola igual o menor, número de Hola de adaptadores permitido para el tamaño de máquina de destino de hello, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.
     - Si número Hola de adaptadores para la máquina virtual de origen de hello supera número de hello permitido para el tamaño de destino de hello, se utilizará el tamaño máximo de hello destino.
     - Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un equipo de destino de Hola tendrá solo un adaptador.     
   - Si la máquina virtual de hello tiene varios adaptadores de red se conectarán todos toohello misma red.
   - Si la máquina virtual de hello tiene varios adaptadores de red, a continuación, Hola mostrado en la lista de hello deja de estar hello *predeterminado* adaptador de red de máquina virtual de Azure Hola.
 - Obtenga [más información](vmware-walkthrough-network.md) sobre direcciones IP.



## <a name="view-and-modify-vm-settings"></a>Vista y modificación de la configuración de una máquina virtual

Se recomienda que compruebe las propiedades de Hola de máquina de origen de hello antes de ejecutar una conmutación por error.

1. En **elementos protegidos**, haga clic en **replican elementos**y haga clic en hello máquina virtual.
2. Hola **replicadas elemento** panel, puede ver un resumen de información de máquina virtual, estado y puntos de recuperación disponible más recientes de Hola. Haga clic en **propiedades** tooview más detalles.
3. En **Compute and Network** (Proceso y red), puede:
    - Modifique el nombre de la máquina virtual de Azure de Hola. Hola nombre debe cumplir [requisitos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Especificar un [grupo de recursos] posterior a la conmutación por error.
    - Especifique un tamaño de destino para hello VM de Azure
    - Seleccione un [conjunto de disponibilidad](../virtual-machines/windows/tutorial-availability-sets.md).
    - Especifique si toouse [discos administrados por](#managed-disk-considerations). Seleccione **Sí**, si desea que tooattach discos administrados tooyour máquina en tooAzure de migración.
    - Ver o modificar la configuración de red, incluidos red/subred de hello en qué Hola VM de Azure se ubicarán después de la conmutación por error y la dirección IP de Hola que se va a asignar tooit.
4. En **discos**, puede ver información sobre el sistema operativo de Hola y Hola de discos de datos de máquina virtual.

## <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

Una vez que hayas configurado todo, ejecute un toomake de conmutación por error de prueba que todo funciona según lo previsto.

- Si desea que tooconnect tooAzure máquinas virtuales mediante RDP después de la conmutación por error, [preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - prueba de toofully necesita toocopy de Active Directory y DNS en el entorno de prueba. [Más información](site-recovery-active-directory.md#test-failover-considerations).
 - Para obtener información completa sobre la conmutación por error de prueba, lea [este artículo](site-recovery-test-failover-to-azure.md).
- Vea un vídeo introductorio rápido antes de empezar:


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


Ahora ejecute una conmutación por error:

1. toofail a través de un único equipo, en **configuración** > **replican elementos**, haga clic en hello VM > **+ conmutación por error de prueba** icono.

    ![Probar conmutación por error](./media/vmware-walkthrough-test-failover/test-failover.png)

2. toofail a través de una recuperación del plan, en **configuración** > **planes de recuperación**, plan de hello contextual > **conmutación por error de prueba**. un plan de recuperación, toocreate [, siga estas instrucciones](site-recovery-create-recovery-plans.md).  

3. En **conmutación por error de prueba**, seleccione toowhich de red de Azure Hola máquinas virtuales de Azure se conectará después de producirse la conmutación por error.

4. Haga clic en **Aceptar** conmutación por error de toobegin Hola. Pueda seguir el progreso haciendo clic en hello VM tooopen sus propiedades o en hello **conmutación por error de prueba** trabajo en nombre de almacén > **configuración** > **trabajos**  >  **Trabajos de recuperación del sitio**.

5. Una vez completada la conmutación por error de hello, también debe poder réplica de hello toosee máquina Azure aparecen en hello portal de Azure > **máquinas virtuales**. Debe asegurarse de que esa máquina virtual de hello es el tamaño adecuado de hello, que ha conectado toohello de red adecuada y que se está ejecutando.

6. Si preparado para las conexiones después de la conmutación por error, debe ser capaz de tooconnect toohello máquina virtual de Azure.

7. Cuando termine, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación. En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. Esto eliminará las máquinas virtuales de Hola que se crearon durante la conmutación por error de prueba.



## <a name="next-steps"></a>Pasos siguientes

- [Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.
- Si migra máquinas en lugar de replicar y conmutar por recuperación, [lea más](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Obtenga información sobre la conmutación por recuperación](site-recovery-failback-azure-to-vmware.md), toofail back y replicar máquinas virtuales de Azure nuevo sitio de toohello local principal.
