---
title: "¿aaaHow realiza el trabajo de tooAzure de replicación de Hyper-V en Site Recovery? | Microsoft Docs"
description: "En este artículo se proporciona información general sobre cómo funciona la replicación de Hyper-V en Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-architecture-hyper-v-to-azure
ms.openlocfilehash: e982806b4d6cdec2f71f82d8c73c17cc50ad3c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work"></a>¿Cómo funciona tooAzure de replicación de Hyper-V?

Lea esta arquitectura de artículo toounderstand Hola y flujos de trabajo para tooAzure de replicación de Hyper-V con hello [Azure Site Recovery](site-recovery-overview.md) servicio.

Registrar cualquier comentario a la parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Puede replicar Hola siguientes tooAzure:
- **Hyper-V con VMM**: máquinas virtuales ubicadas en hosts de Hyper-V locales que se administran en nubes de System Center Virtual MAchine Manager (VMM). Los hosts pueden ejecutar cualquier [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Puede replicar máquinas virtuales de Hyper-V que ejecuten cualquier sistema operativo invitado [compatible con Hyper-V y Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).
- **Hyper-V sin VMM**: máquinas virtuales locales que se encuentran en hosts de Hyper-V que no se administran en nubes de VMM. Hosts pueden ejecutar cualquiera de hello [los sistemas operativos compatibles](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). Puede replicar máquinas virtuales de Hyper-V que ejecuten cualquier sistema operativo invitado [compatible con Hyper-V y Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="architectural-components"></a>Componentes de la arquitectura

**Ámbito** | **Componente** | **Detalles**
--- | --- | ---
**Las tablas de Azure** | En Azure, necesitará una cuenta de Microsoft Azure, una cuenta de almacenamiento de Azure y una red de Azure. | Las de almacenamiento y red pueden basarse en cuentas de Resource Manager o cuentas clásicas.<br/><br/> Los datos replicados se almacenan en la cuenta de almacenamiento de Hola y máquinas virtuales de Azure se crean con datos saludo replican Cuando se produce la conmutación por error desde el sitio local.<br/><br/> Hola máquinas virtuales de Azure Conéctese toohello red virtual de Azure cuando se crean.
**Servidor VMM** | Hosts de Hyper-V ubicados en nubes de VMM | Si los hosts de Hyper-V se administran en nubes de VMM, debe registrar servidor VMM hello en hello que del almacén de servicios de recuperación.<br/><br/> En el servidor VMM de hello instala la replicación de tooorchestrate de proveedor de Site Recovery Hola con Azure.<br/><br/> Necesita lógica y redes de VM configurada tooconfigure la asignación de red. Una red de VM debe ser tooa vinculado red lógica que esté asociada con la nube de Hola.
**Host de Hyper-V** | Los servidores de Hyper-V pueden implementarse con o sin servidor de VMM. | Si no hay ningún servidor VMM, proveedor de Site Recovery se instala en la replicación de hello host tooorchestrate con Site Recovery a través de Hola Hola internet. Si hay un servidor de VMM, Hola proveedor está instalado en él y no en el host de Hola.<br/><br/> agente de servicios de recuperación de Hello está instalado en la replicación de datos de hello host toohandle.<br/><br/> Las comunicaciones de hello proveedor y agente de hello son seguro y está cifrado. También se cifran los datos replicados en el almacenamiento de Azure.
**Máquinas virtuales de Hyper-V** | Necesita uno o más máquinas virtuales en el servidor de host de Hyper-V de Hola. | Es necesario ninguna acción tooexplicitly instalado en máquinas virtuales

## <a name="deployment-steps"></a>Pasos de implementación

1. **Azure**: configurar Hola de componentes de Azure. Se recomienda que configure las cuentas de almacenamiento y de red antes de comenzar la implementación de Site Recovery.
2. **Almacén**: cree un almacén de Recovery Services para Site Recovery y configúrelo, incluidas las opciones de origen y de destino, una directiva de replicación, finalmente, habilite la replicación.
3. **Origen y destino**:
    - **Hosts de Hyper-V en nubes de VMM**: como parte de la especificación de configuración de origen, descargar e instalar hello Azure Site Recovery Provider en el servidor VMM de Hola y el agente de servicios de recuperación de Azure de hello en cada host de Hyper-V. origen de Hello será el servidor VMM de Hola. destino de Hello es Azure.
    - Hosts de Hyper-V sin WMM: cuando se especifica la configuración del código fuente, descargar e instalar Hola proveedor y el agente en cada host de Hyper-V. Durante la implementación recopilar hosts hello en un sitio de Hyper-V y especificar este sitio como origen de Hola. destino de Hello es Azure.

    ![Replicación de Hyper-V o VMM tooAzure](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png) ![tooAzure de replicación de sitio de Hyper-V](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)


4. **Directiva de replicación**: crear una directiva de replicación de sitio de Hyper-V de Hola o de nube de VMM. Directiva de Hello es máquinas virtuales de tooall aplicado ubicadas en hosts en el sitio de Hola o en la nube.
5. **Habilitación de la replicación**: habilite la replicación de máquinas virtuales de Hyper-V. Se produce la replicación inicial según la configuración de directiva de replicación de Hola. Se realiza el seguimiento de cambios de datos y la replicación de diferencias cambios tooAzure comienza después de que finalice la replicación inicial de Hola. Las marcas de revisión de un elemento se conservan en un archivo .hrl.
6. **Probar la conmutación por error**: ejecutar una toomake de conmutación por error de prueba que todo funciona según lo previsto.

Más información acerca de la implementación:
- [Empezar a trabajar con tooAzure de replicación de máquina virtual de Hyper-V - con VMM](site-recovery-vmm-to-azure.md)
- [Empezar a trabajar con tooAzure de replicación de máquina virtual de Hyper-V - sin VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="hyper-v-replication-workflow"></a>Flujo de trabajo de replicación de Hyper-V

### <a name="enable-protection"></a>Habilitar protección

1. Después de habilitar la protección de una máquina virtual de Hyper-V, Hola portal de Azure o de forma local, Hola **habilitar la protección** inicia.
2. Hello trabajo comprueba esa máquina Hola cumple los requisitos previos, antes de invocar hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset la replicación con la configuración de Hola que haya configurado.
3. trabajo de Hello inicia la replicación inicial mediante la invocación de hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) método, tooinitialize una réplica completa de la máquina virtual y tooAzure de discos virtuales de envío Hola la máquina virtual.
4. Puede supervisar el trabajo de Hola Hola **trabajos** ficha.      ![Lista Trabajos](media/site-recovery-hyper-v-azure-architecture/image1.png)![Detalles de Habilitar protección](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="initial-replication"></a>Replicación inicial

1. Cuando se desencadena la replicación inicial, se toma una [instantánea de la máquina virtual de Hyper-V](https://technet.microsoft.com/library/dd560637.aspx).
2. Discos duros virtuales están replicados uno por uno hasta que sean más tooAzure copiado todos los. Se puede tardar varios minutos, según Hola tamaño de máquina virtual y ancho de banda de red. toooptimize el uso de la red, consulte [cómo toomanage local uso de ancho de banda de red de tooAzure protección](https://support.microsoft.com/kb/3056159).
3. Si se producen cambios de disco mientras la replicación inicial está en curso, Hola Rastreador de replicación de réplica de Hyper-V realiza un seguimiento de los cambios como registros de replicación de Hyper-V (.hrl). Estos archivos se encuentran en hello misma carpeta que los discos de Hola. Cada disco tiene un archivo de .hrl asociados que se enviarán toosecondary almacenamiento.
4. archivos de instantáneas y de registro de Hello consumen recursos de disco mientras la replicación inicial está en curso.
5. Cuando finalice la replicación inicial de hello, se elimina la instantánea de la VM de Hola. Cambios realizados en el registro de hello en el disco de delta son disco primario con toohello combinada y sin sincronizar.


### <a name="finalize-protection"></a>Fin de la protección

1. Al finalizar la replicación inicial de hello, hello **finalizar la protección en la máquina virtual de hello** trabajo configura la red y otras configuraciones posteriores a la replicación, para que la máquina virtual de hello está protegida.
    ![Trabajo de finalización de la protección](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Si replica tooAzure, podría necesita una configuración de hello tootweak para la máquina virtual de Hola para que esté preparado para conmutación por error. En este momento puede ejecutar un toocheck de conmutación por error de prueba que todo funciona según lo previsto.

### <a name="delta-replication"></a>Replicación diferencial

1. Después de la replicación inicial de hello, sincronización delta comienza, según la configuración de replicación.
2. Hola Rastreador de replicación de réplica de Hyper-V realiza un seguimiento Hola cambios tooa disco duro como archivos .hrl. Cada disco configurado para la replicación tiene un archivo .hrl asociado. Este registro se envía la cuenta de almacenamiento del cliente toohello una vez completada la replicación inicial. Cuando un registro está en tránsito tooAzure, se realiza el seguimiento de cambios de hello en el disco principal de hello en otro archivo de registro de hello mismo directorio.
3. Durante la replicación inicial y las diferencias, puede supervisar Hola VM Hola vista de máquina virtual. [Más información](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="replication-synchronization"></a>Sincronización de las replicaciones

1. Si se produce un error en la replicación diferencial y una replicación completa sería costosa en términos de ancho de banda o de tiempo, se marca una máquina virtual para la resincronización. Por ejemplo, si los archivos de .hrl Hola llegan a 50% del tamaño de disco de hello, a continuación, hello VM se marcarán para volver a sincronizar.
2.  Resincronización minimiza la cantidad de Hola de datos enviados por el cálculo de sumas de comprobación de Hola de origen y destino de máquinas virtuales y enviar solo Hola diferencias de datos. La resincronización utiliza un algoritmo de fragmentación de bloques fijos donde los archivos de origen y destino se dividen en fragmentos fijos. Las sumas de comprobación para cada fragmento se generan y, a continuación, en comparación con toodetermine que bloquea el destino de hello origen necesidad toobe toohello aplicada.
3. Una vez finalizada la resincronización, se debe reanudar la replicación diferencial normal. De forma predeterminada la resincronización es toorun programada automáticamente fuera del horario de oficina, pero puede volver a sincronizar una máquina virtual manualmente. Por ejemplo, si se produce una interrupción de la red o de otro tipo, la resincronización se puede reanudar. toodo, seleccione Hola VM en el portal de hello > **resincronizar**.

    ![Resincronización manual](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retries"></a>Reintentos

Si se produce un error de replicación, se realiza un reintento de forma predefinida. Esta lógica se puede clasificar en dos categorías:

**Categoría** | **Detalles**
--- | ---
**Errores irrecuperables** | No se realiza ningún reintento. El estado de la máquina virtual será **Crítico** y se requiere la intervención del administrador. Algunos ejemplos de estos errores son: divide la cadena de disco duro virtual; Estado no válido para la réplica de hello VM; Errores de autenticación de red: errores de autorización; Máquina virtual no se encontró errores (para servidores de Hyper-V independiente)
**Errores recuperables** | Reintentos posteriores ocurren cada intervalo de replicación, con un retroceso exponencial que aumenta el intervalo de reintento de Hola desde el inicio de hello del primer intento de Hola por 1, 2, 4, 8 y 10 minutos. Si el error persiste, reintente cada 30 minutos. Ejemplos: errores de red; errores de espacio insuficiente en disco; memoria insuficiente |

## <a name="protection-and-recovery-lifecycle"></a>Ciclo de vida de la protección y la recuperación

![flujo de trabajo](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

## <a name="next-steps"></a>Pasos siguientes

- [Comprobación de los requisitos previos de implementación](site-recovery-prereq.md)
- Solución de problemas con:
    - [Supervisión y solución de problemas de protección](site-recovery-monitoring-and-troubleshooting.md)
    - [Ayuda del soporte técnico de Microsoft](site-recovery-monitoring-and-troubleshooting.md#reach-out-for-microsoft-support)
    - [Errores comunes y soluciones](site-recovery-monitoring-and-troubleshooting.md#common-azure-site-recovery-errors-and-their-resolutions)
