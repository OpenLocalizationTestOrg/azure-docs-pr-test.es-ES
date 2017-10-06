---
title: aplicaciones de aaaReplicate (Azure tooAzure) | Documentos de Microsoft
description: "Este artículo describe cómo ejecutar los equipos de tooset la replicación de memoria virtual en una región de Azure demasiado otra región de Azure."
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
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a>Replicar máquinas virtuales de Azure tooanother región de Azure



>[!NOTE]
>
> La replicación de Site Recovery en máquinas virtuales de Azure se encuentra actualmente en versión preliminar.

Este artículo describe cómo ejecutar los equipos de tooset la replicación de memoria virtual en una región de Azure tooanother región de Azure.

## <a name="prerequisites"></a>Requisitos previos

* artículo de Hola se supone que ya sabe algo acerca de Site Recovery y almacén de servicios de recuperación. Deberá toohave un pre "Almacén de servicios de recuperación" creado.

    >[!NOTE]
    >
    > Se recomienda que cree Hola "Almacén de servicios de recuperación" en ubicación Hola donde desea que su tooreplicate de máquinas virtuales. Por ejemplo, si la ubicación de destino es "Centro de EE. UU.", cree el almacén en "Centro de EE. UU.".

* Si usan reglas de grupos de seguridad de red (NSG) o la conectividad a internet firewall proxy toocontrol acceso toooutbound en hello máquinas virtuales de Azure, asegúrese de que Hola de lista blanca de direcciones requiere direcciones URL o direcciones IP. Consulte demasiado[documento de orientación de las redes](./site-recovery-azure-to-azure-networking-guidance.md) para obtener más detalles.

* Si tiene una ExpressRoute o una conexión VPN entre hello y local del origen de ubicación de Azure, siga [consideraciones sobre la recuperación de sitio de ExpressRoute de Azure tooon local / configuración de VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) documento.

* Su cuenta de usuario de Azure necesita toohave determinados [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una máquina virtual de Azure.

* Su suscripción de Azure debe estar habilitado toocreate las máquinas virtuales en la ubicación de destino de hello desea toouse como región de recuperación ante desastres. Puede ponerse en contacto con soporte técnico tooenable Hola necesario cuota.

## <a name="enable-replication-from-azure-site-recovery-vault"></a>Habilitar la replicación desde el almacén de Azure Site Recovery
De esta ilustración, se replicará máquinas virtuales en ejecución en toohello de ubicación de Azure de 'Asia oriental' hello ' sudeste asiático ' ubicación. pasos de Hello son los siguientes:

 Haga clic en **+ replicar** en la replicación de tooenable de almacén de Hola para las máquinas virtuales de Hola.

1. **Origen:** hace referencia toohello punto de origen de máquinas de Hola que en este caso es **Azure**.

2. **Ubicación de origen:** es Hola región de Azure desde donde desea tooprotect las máquinas virtuales. En esta ilustración, ubicación de origen de hello constituye 'Asia oriental'

3. **Modelo de implementación:** hace referencia toohello modelo de implementación de Azure de máquinas de origen Hola. Puede seleccionar cualquier clásico o el Administrador de recursos y máquinas que pertenecen toohello específicos del modelo se mostrarán para la protección en el paso siguiente Hola.

      >[!NOTE]
      >
      > Solo puede replicar una máquina virtual clásica y recuperarla como máquina virtual clásica. No puede recuperarla como una máquina virtual de Resource Manager.

4. **Grupo de recursos:** lo del toowhich de grupo de recursos de hello las máquinas virtuales de origen pertenecen. Hola todas las máquinas virtuales en el grupo de recursos seleccionado Hola se enumerarán para la protección en el paso siguiente de saludo.

    ![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

En **máquinas virtuales > Seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate. Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación. A continuación, haga clic en Aceptar.
    ![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)


En la sección Configuración puede configurar las propiedades del sitio de destino

1. **Ubicación de destino:** se trata de ubicación de Hola donde se replicarán los datos de la máquina virtual de origen. Dependiendo de la ubicación de los equipos seleccionados, Site Recovery proporcionará que Hola lista de regiones de destino adecuado.

    > [!TIP]
    > Se recomienda la ubicación de destino de tookeep igual a partir de la recuperación del almacén de servicios.

2. **Grupo de recursos de destino:** es toowhich de grupo de recursos de hello pertenecerá todas sus máquinas virtuales replicadas. De forma predeterminada ASR creará un nuevo grupo de recursos en la región de destino de hello con nombre con sufijo "asr". En caso de que existe el grupo de recursos ya creado por ASR, se volverá a usar. También puede elegir toocustomize tal como se muestra en la siguiente sección de Hola.    
3. **Red Virtual de destino:** de forma predeterminada, ASR creará una nueva red virtual en la región de destino de hello con nombre con sufijo "asr". Esto será asignada tooyour red de origen y se usará para todas las protecciones futuras.

    > [!NOTE]
    > [Compruebe los detalles de la red](site-recovery-network-mapping-azure-to-azure.md) tooknow más información acerca de la asignación de red.

4. **Las cuentas de almacenamiento de destino:** de forma predeterminada, ASR creará Hola nueva la cuenta de almacenamiento destino imitando la configuración de almacenamiento de máquina virtual de origen. En caso de que ya exista la cuenta de almacenamiento creada por ASR, se volverá a usar.

5. **Almacenar en caché las cuentas de almacenamiento:** ASR necesita la cuenta de almacenamiento adicional denominada almacenamiento en caché en la región de origen de Hola. Todos los Hola los cambios que ocurren en hello máquinas virtuales de origen se realiza el seguimiento y envían toocache cuenta de almacenamiento antes de replicar esos ubicación de destino de toohello.

6. **Conjunto de disponibilidad:** de forma predeterminada, ASR creará un nuevo conjunto de disponibilidad en la región de destino de hello con nombre con sufijo "asr". En caso de que ya exista el conjunto de disponibilidad creado por ASR, se volverá a usar.

7.  **Directiva de replicación:** define opciones de configuración de Hola para recuperación punto retención historial y aplicación instantánea coherente con la frecuencia. De forma predeterminada, ASR creará una nueva directiva de replicación con la configuración predeterminada "24 horas" para la retención del punto de recuperación y "60 minutos" para la frecuencia de instantánea coherente con la aplicación.

    ![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a>Personalizar los recursos de destino

En caso de que desea que los valores predeterminados de Hola de toochange que se utiliza ASR, puede cambiar la configuración de hello según sus necesidades.

1. **Personalizar:** haga clic en él toochange Hola parámetro predeterminado utilizado por ASR.

2. **Grupo de recursos de destino:** puede seleccionar grupo de recursos de hello en lista de Hola de todos los grupos de recursos de hello existentes en la ubicación de destino de hello dentro de suscripción de Hola.

3. **Red Virtual de destino:** encontrará la lista de Hola de todas las redes virtuales de hello en la ubicación de destino de Hola.

4. **Conjunto de disponibilidad:** solo puede agregar disponibilidad conjuntos de configuración toohello las máquinas virtuales que forman parte de la disponibilidad en la región de origen.

5. **Cuentas de almacenamiento de destino:**

![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Haga clic en **Crear recurso de destino** y en Habilitar replicación


Una vez que se protegen las máquinas virtuales se puede comprobar el estado de Hola de mantenimiento de máquinas virtuales en **elementos de replicación**

>[!NOTE]
>Durante el saludo momento de la replicación inicial podría una posibilidad de que el estado toma toorefresh de tiempo y no ver progreso durante algún tiempo. Puede hacer clic en el botón de actualización de hello en la parte superior de Hola de estado más reciente de hello hoja tooget Hola.
>

![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a>Pasos siguientes
- [Más información](site-recovery-test-failover-to-azure.md) sobre la ejecución de una conmutación por error de prueba.
- [Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.
- Obtenga más información sobre [con planes de recuperación](site-recovery-create-recovery-plans.md) tooreduce RTO.
- Más información sobre la [reprotección de máquinas virtuales de Azure](site-recovery-how-to-reprotect.md) después de una conmutación por error.
