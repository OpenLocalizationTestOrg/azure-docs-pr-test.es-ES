---
title: "¿aaaHow realiza el trabajo de tooAzure de replicación de Hyper-V en Azure Site Recovery? | Microsoft Docs"
description: "Este artículo proporciona información general de componentes y arquitectura que se usa al replicar locales tooAzure de máquinas virtuales de Hyper-V con el servicio de Azure Site Recovery Hola."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 3b64156307f37764a8315dec68cf297acf279530
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work-in-site-recovery"></a>¿Cómo funciona tooAzure de replicación de Hyper-V en Site Recovery?


Este artículo describen los componentes de Hola y procesos que tienen lugar al replicar máquinas virtuales de Hyper-V, tooAzure con hello local [Azure Site Recovery](site-recovery-overview.md) servicio.

Site Recovery puede replicar máquinas virtuales de Hyper-V en clústeres de Hyper-V y hosts independientes que se administren con o sin System Center Virtual Machine Manager (VMM).

Registrar cualquier comentario a la parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Componentes de la arquitectura

Hay una serie de componentes implicados al replicar las máquinas virtuales de Hyper-V tooAzure.

**Componente** | **Ubicación** | **Detalles**
--- | --- | ---
**Las tablas de Azure** | En Azure, necesitará una cuenta de Microsoft Azure, una cuenta de almacenamiento de Azure y una red de Azure. | Los datos replicados se almacenan en la cuenta de almacenamiento de Hola y máquinas virtuales de Azure se crean con datos saludo replican Cuando se produce la conmutación por error desde el sitio local.<br/><br/> Hola máquinas virtuales de Azure Conéctese toohello red virtual de Azure cuando se crean.
**Servidor VMM** | Los hosts de Hyper-V están ubicados en nubes de VMM | Si los hosts de Hyper-V se administran en nubes de VMM, debe registrar servidor VMM hello en hello que del almacén de servicios de recuperación.<br/><br/> En el servidor VMM de hello instala la replicación de tooorchestrate de proveedor de Site Recovery Hola con Azure.<br/><br/> Necesita lógica y redes de VM configurada tooconfigure la asignación de red. Una red de VM debe ser tooa vinculado red lógica que esté asociada con la nube de Hola.
**Host de Hyper-V** | Los host y clústeres de Hyper-V pueden implementarse con o sin un servidor de VMM. | Si no hay ningún servidor VMM, proveedor de Site Recovery se instala en la replicación de hello host tooorchestrate con Site Recovery a través de Hola Hola internet. Si hay un servidor de VMM, Hola proveedor está instalado en él y no en el host de Hola.<br/><br/> agente de servicios de recuperación de Hello está instalado en la replicación de datos de hello host toohandle.<br/><br/> Las comunicaciones de hello proveedor y agente de hello son seguro y está cifrado. También se cifran los datos replicados en el almacenamiento de Azure.
**Máquinas virtuales de Hyper-V** | Necesita una o varias máquinas virtuales que se ejecuten en un servidor host de Hyper-V. | Es necesario ninguna acción tooexplicitly instalado en las máquinas virtuales.

Obtenga información acerca de los requisitos previos de implementación de Hola y requisitos para cada uno de estos componentes en hello [matriz de compatibilidad](site-recovery-support-matrix-to-azure.md).

**Figura 1: Replicación de tooAzure del sitio de Hyper-V**

![Componentes](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Figura 2: Hyper-V en la replicación de tooAzure de nubes VMM**

![Componentes](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a>Proceso de replicación

**Figura 3: Proceso de replicación y la recuperación de tooAzure de replicación de Hyper-V**

![flujo de trabajo](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>Habilitar protección

1. Después de habilitar la protección de una máquina virtual de Hyper-V, Hola portal de Azure o de forma local, Hola **habilitar la protección** inicia.
2. Hello trabajo comprueba esa máquina Hola cumple los requisitos previos, antes de invocar hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset la replicación con la configuración de Hola que haya configurado.
3. trabajo de Hello inicia la replicación inicial mediante la invocación de hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) método, tooinitialize una réplica completa de la máquina virtual y tooAzure de discos virtuales de envío Hola la máquina virtual.
4. Puede supervisar el trabajo de Hola Hola **trabajos** ficha.      ![Lista Trabajos](media/site-recovery-hyper-v-azure-architecture/image1.png)![Detalles de Habilitar protección](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="replicate-hello-initial-data"></a>Replicar datos de saludo inicial

1. Cuando se desencadena la replicación inicial, se toma una [instantánea de la máquina virtual de Hyper-V](https://technet.microsoft.com/library/dd560637.aspx).
2. Discos duros virtuales están replicados uno por uno hasta que sean más tooAzure copiado todos los. Se puede tardar varios minutos, según Hola tamaño de máquina virtual y ancho de banda de red. toooptimize el uso de la red, consulte [cómo toomanage local uso de ancho de banda de red de tooAzure protección](https://support.microsoft.com/kb/3056159).
3. Si se producen cambios de disco mientras la replicación inicial está en curso, Hola Rastreador de replicación de réplica de Hyper-V realiza un seguimiento de los cambios como registros de replicación de Hyper-V (.hrl). Estos archivos se encuentran en hello misma carpeta que los discos de Hola. Cada disco tiene un archivo de .hrl asociados que se enviarán toosecondary almacenamiento.
4. archivos de instantáneas y de registro de Hello consumen recursos de disco mientras la replicación inicial está en curso.
5. Cuando finalice la replicación inicial de hello, se elimina la instantánea de la VM de Hola. Cambios realizados en el registro de hello en el disco de delta son disco primario con toohello combinada y sin sincronizar.


### <a name="finalize-protection"></a>Fin de la protección

1. Al finalizar la replicación inicial de hello, hello **finalizar la protección en la máquina virtual de hello** trabajo configura la red y otras configuraciones posteriores a la replicación, para que la máquina virtual de hello está protegida.
    ![Trabajo de finalización de la protección](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Si replica tooAzure, podría necesita una configuración de hello tootweak para la máquina virtual de Hola para que esté preparado para conmutación por error. En este momento puede ejecutar un toocheck de conmutación por error de prueba que todo funciona según lo previsto.

### <a name="replicate-hello-delta"></a>Replicar delta Hola

1. Después de la replicación inicial de hello, sincronización delta comienza, según la configuración de replicación.
2. Hola Rastreador de replicación de réplica de Hyper-V realiza un seguimiento Hola cambios tooa disco duro como archivos .hrl. Cada disco configurado para la replicación tiene un archivo .hrl asociado. Este registro se envía la cuenta de almacenamiento del cliente toohello una vez completada la replicación inicial. Cuando un registro está en tránsito tooAzure, se realiza el seguimiento de cambios de hello en el disco principal de hello en otro archivo de registro de hello mismo directorio.
3. Durante la replicación inicial y las diferencias, puede supervisar Hola VM Hola vista de máquina virtual. [Más información](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="synchronize-replication"></a>Sincronización de la replicación

1. Si se produce un error en la replicación diferencial y una replicación completa sería costosa en términos de ancho de banda o de tiempo, se marca una máquina virtual para la resincronización. Por ejemplo, si los archivos de .hrl Hola llegan a 50% del tamaño de disco de hello, a continuación, hello VM se marcarán para volver a sincronizar.
2.  Resincronización minimiza la cantidad de Hola de datos enviados por el cálculo de sumas de comprobación de Hola de origen y destino de máquinas virtuales y enviar solo Hola diferencias de datos. La resincronización utiliza un algoritmo de fragmentación de bloques fijos donde los archivos de origen y destino se dividen en fragmentos fijos. Las sumas de comprobación para cada fragmento se generan y, a continuación, en comparación con toodetermine que bloquea el destino de hello origen necesidad toobe toohello aplicada.
3. Una vez finalizada la resincronización, se debe reanudar la replicación diferencial normal. De forma predeterminada la resincronización es toorun programada automáticamente fuera del horario de oficina, pero puede volver a sincronizar una máquina virtual manualmente. Por ejemplo, si se produce una interrupción de la red o de otro tipo, la resincronización se puede reanudar. toodo, seleccione Hola VM en el portal de hello > **resincronizar**.

    ![Resincronización manual](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retry-logic"></a>Lógica de reintento

Si se produce un error de replicación, se realiza un reintento de forma predefinida. Esta lógica se puede clasificar en dos categorías:

**Categoría** | **Detalles**
--- | ---
**Errores irrecuperables** | No se realiza ningún reintento. El estado de la máquina virtual será **Crítico** y se requiere la intervención del administrador. Algunos ejemplos de estos errores son: divide la cadena de disco duro virtual; Estado no válido para la réplica de hello VM; Errores de autenticación de red: errores de autorización; Máquina virtual no se encontró errores (para servidores de Hyper-V independiente)
**Errores recuperables** | Reintentos posteriores ocurren cada intervalo de replicación, con un retroceso exponencial que aumenta el intervalo de reintento de Hola desde el inicio de hello del primer intento de Hola por 1, 2, 4, 8 y 10 minutos. Si el error persiste, reintente cada 30 minutos. Ejemplos: errores de red; errores de espacio insuficiente en disco; memoria insuficiente |



## <a name="failover-and-failback-process"></a>Proceso de conmutación por error y conmutación por recuperación

1. Puede ejecutar planeada o no planeada [conmutación por error](site-recovery-failover.md) de tooAzure de máquinas virtuales de Hyper-V local. Si se ejecuta una conmutación por error planeada, las máquinas virtuales de origen se apagan tooensure sin pérdida de datos.
2. Puede conmutar por error un único equipo, o crear [planes de recuperación](site-recovery-create-recovery-plans.md) tooorchestrate conmutación por error de varias máquinas.
4. Después de ejecutar Hola conmutación por error, debe ser hello toosee capaz de crear máquinas virtuales de réplica en Azure. Puede asignar una toohello de dirección IP virtual pública si es necesario.
5. A continuación, confirma toostart de conmutación por error de hello obtiene acceso a cargas de trabajo de Hola desde réplica Hola VM de Azure.
6. Cuando el sitio local principal esté disponible de nuevo, podrá realizar una [conmutación por recuperación](site-recovery-failback-from-azure-to-hyper-v.md). Iniciar una conmutación por error planeada desde Azure toohello de sitio primario. Para una conmutación por error planeada, puede toofailback seleccione toohello misma máquina virtual o tooan una ubicación alternativa y sincronizar no cambios entre Azure y local, tooensure pérdida de datos. Cuando las máquinas virtuales se crean en local, confirmar Hola conmutación por error.




## <a name="next-steps"></a>Pasos siguientes

Hola de revisión [matriz de compatibilidad](site-recovery-support-matrix-to-azure.md)
