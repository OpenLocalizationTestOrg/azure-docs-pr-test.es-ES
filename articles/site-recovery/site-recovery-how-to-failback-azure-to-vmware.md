---
title: aaaHow toofail desde tooVMware Azure | Documentos de Microsoft
description: "Después de la conmutación por error de máquinas virtuales tooAzure, puede iniciar una conmutación por recuperación toobring máquinas virtuales atrás tooon local. Obtenga información acerca de pasos de Hola de cómo realizar copias de toofail."
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
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>Error de Azure tooan sitio local

Este artículo describe cómo realizar toofail copia máquinas virtuales de sitio local de toohello de máquinas virtuales de Azure. Siga las instrucciones de hello en este artículo toofail realizar copia sus máquinas virtuales de VMware o servidores físicos de Windows/Linux después de que han conmutado de hello local sitio tooAzure mediante el uso de hello [físicos y máquinas virtuales de VMware replicar tooAzure de servidores con Azure Site Recovery](site-recovery-vmware-to-azure-classic.md) tutorial.

> [!WARNING]
> Si tiene [completar la migración](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), recurso de tooanother de máquina virtual movida hello, o un grupo eliminado Hola máquina virtual de Azure, no podrá volver a continuación.

> [!NOTE]
> Si han conmutado máquinas virtuales de VMware no host de Hyper-v tooa de conmutación por recuperación.

## <a name="overview-of-failback"></a>Introducción a la conmutación por recuperación
Así es cómo funciona la conmutación por recuperación. Una vez se han conmutado tooAzure, se produce un error al sitio local tooyour back-algunas fases:

1. [Vuelva a proteger](site-recovery-how-to-reprotect.md) Hola máquinas virtuales en Azure para que inicien máquinas virtuales de tooreplicate tooVMware en el sitio local. Como parte de este proceso, también debe:
    1. Configurar un destino maestro local: uno de Windows para las máquinas virtuales Windows y un [destino maestro de Linux](site-recovery-how-to-install-linux-master-target.md) para las máquinas virtuales Linux.
    2. Configurar un [servidor de procesos](site-recovery-vmware-setup-azure-ps-resource-manager.md).
    3. Iniciar de nuevo la [protección](site-recovery-how-to-reprotect.md). Esto se desactivar la máquina virtual de hello local y sincronizará hello Azure los datos de la máquina virtual con hello discos locales.
5. Después de que las máquinas virtuales en Azure se replican tooyour al sitio local, iniciar por error a través del sitio de Azure toohello local.

Cuando se produzca error volver los datos, se vuelva a proteger máquinas virtuales de hello local que conmutación por recuperación a, por lo que se inicie tooreplicate tooAzure.

Para obtener una introducción rápida, vea Hola siguiendo el vídeo sobre cómo toofail a través de Azure tooan sitio local.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>Producirá un error en ubicación original o alternativa de toohello atrás

Si produce un error en una máquina virtual VMware, puede producir un error toohello atrás mismo origen local virtual machine si sigue estando existe. En este escenario, sólo los cambios de Hola se replican de nuevo. Este escenario se conoce como recuperación de ubicación original. Si la máquina virtual de hello local no existe, el escenario de hello es una recuperación en ubicación alternativa.

> [!NOTE]
> Puede que solo conmutación por recuperación toohello original vCenter y el servidor de configuración. No puede implementar un nuevo servidor de configuración y realizar la conmutación por recuperación usándolo. Además, no se puede agregar un servidor configuración de nueva vCenter toohello existente y la conmutación por recuperación en hello nueva vCenter.

#### <a name="original-location-recovery"></a>Recuperación de ubicación original

Si no espera toohello la máquina virtual original, se necesitan Hola condiciones siguientes:
* Si la máquina virtual de hello está administrado por un servidor vCenter, a continuación, hello ESX host del destino maestro debe tener el almacén de datos de access toohello de la máquina virtual.
* Si Hola se encuentra en un host ESX pero no está administrado por vCenter, debe ser Hola de disco de máquina virtual de hello en un almacén de datos puede tener acceso host de ese destino maestro Hola.
* Si la máquina virtual está en un host ESX y no usa vCenter, debe completar la detección de host ESX Hola de destino maestro Hola antes de que vuelva a proteger. Lo mismo se aplica si también conmuta por recuperación a servidores físicos.
* Puede producir un error tooa back-red de área de almacenamiento virtual (vSAN) o un disco que basa mapping (RDM) si discos Hola ya existen y son de máquina virtual de toohello conectado local de dispositivos raw.

#### <a name="alternate-location-recovery"></a>Recuperación de ubicación alternativa
Si la máquina virtual de hello local no existe antes de volver a proteger la máquina virtual de hello, escenario de Hola se denomina una recuperación en ubicación alternativa. flujo de trabajo de Hello reprotección crea máquina virtual de hello local de nuevo. Esto también hará que se produzca una descarga de datos completa.

* Cuando se produce un error de ubicación alternativa tooan atrás, máquina virtual de hello será toohello recuperada mismo host ESX en qué Hola se implementa el servidor de destino maestro. Hello almacén de datos que ha utilizado el disco de hello toocreate será Hola mismo almacén de datos que se ha seleccionado al volver a proteger la máquina virtual de Hola.
* Puede producir un error de almacén de datos de sistema (VMFS) de archivo nuevo solo máquina virtual de tooa. Si tiene un vSAN o RDM, la reprotección y la conmutación por recuperación no funcionarán.
* Reprotección implica a una transferencia de datos inicial grande seguida de cambios de Hola. Este proceso existe porque no existe la máquina virtual de hello en local. los datos completos de Hello deben toobe replican de nuevo. Esta reprotección también tardará más tiempo que la recuperación de ubicación original.
* No se puede suspender volver toovSAN o RDM basada en discos. En un almacén de datos VMFS solo pueden crearse discos de máquina virtual (VMDK) nuevos.

Puede un equipo físico, si tooAzure, ha conmutado por error nuevo solo como una máquina virtual de VMware (también denominado tooas P2A2V). Este flujo se encuentra en recuperación de ubicación alternativa de Hola.

* Un servidor físico de Windows Server 2008 R2 SP1, si protegido y conmutado por error tooAzure, no se recuperarán tras los errores.
* Asegúrese de que detectar al menos un destino maestro hello y servidor necesarios ESX/ESXi hosts toowhich necesita toofail de nuevo.

## <a name="have-you-completed-reprotection"></a>¿Ha completado la reprotección?
Antes de continuar, Hola completa vuelva a proteger pasos para que hello las máquinas virtuales están en un estado replicado y se puede iniciar un sitio de conmutación por error espera tooan local. Para obtener más información, consulte [cómo tooreprotect de Azure local tooon](site-recovery-how-to-reprotect.md).

## <a name="prerequisites"></a>Requisitos previos

* Para la conmutación por recuperación se necesita un servidor de configuración local. Durante la conmutación por recuperación, máquina virtual de hello debe existir en la base de datos del servidor de configuración de Hola o conmutación por recuperación no sea correcta. Por lo tanto, asegúrese de realizar una copia de seguridad programada periódica del servidor. Si se produjera un desastre, necesitará servidor de hello toorestore con hello misma dirección IP para toowork de conmutación por recuperación.
* servidor de destino maestro de Hello no debe tener todas las instantáneas antes de activar la conmutación por recuperación.

## <a name="steps-toofail-back"></a>Pasos toofail atrás

> [!IMPORTANT]
> Antes de iniciar la conmutación por recuperación, asegúrese de que ha completado solo de las máquinas virtuales de Hola. Hola las máquinas virtuales deben estar en un estado protegido y su estado de mantenimiento debe ser **Aceptar**. máquinas virtuales de tooreprotect hello, leer [cómo tooreprotect](site-recovery-how-to-reprotect.md).

1. Hola elementos replicados página, seleccione la máquina virtual de Hola y haga clic en tooselect **conmutación por error imprevista**.
2. En **confirmar conmutación por error**, compruebe la dirección de conmutación por error de hello (de Azure) y, a continuación, seleccione el punto de recuperación de hello (más reciente o más reciente coherente de aplicación hello) que quiere toouse de conmutación por error de Hola. punto coherente de aplicación Hola está detrás de punto más reciente de hello en el tiempo y provoca una pérdida de datos.
3. Durante la conmutación por error, Site Recovery se cierra hello las máquinas virtuales en Azure. Después de comprobar que conmutación por recuperación se ha completado como se esperaba, puede comprobar que las máquinas virtuales hello en Azure que se haya cerrado.

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>punto de recuperación de toowhat ¿por error máquinas virtuales de hello atrás?

Durante la conmutación por recuperación, tiene dos opciones toofail Hola atrás/recuperación de máquina virtual plan.

Si selecciona hello más reciente procesado en el tiempo, todas las máquinas virtuales conmutarán por error tootheir más reciente disponible punto en el tiempo. En caso de que hay un grupo de replicación en el plan de recuperación de hello, a continuación, cada máquina virtual del grupo de replicación de hello conmutarán por error tooits independientes último punto en el tiempo.

No se puede conmutar por recuperación una máquina virtual hasta que tenga al menos un punto de recuperación. No se puede conmutar por recuperación un plan de recuperación hasta que todas sus máquinas virtuales tengan al menos un punto de recuperación.

> [!NOTE]
> El punto de recuperación más reciente es un punto de recuperación preparadas para el bloqueo.

Si selecciona el punto de recuperación coherentes con la aplicación hello, una sola máquina virtual de conmutación por recuperación recuperará tooits último punto de recuperación consistente con las aplicaciones disponibles. En caso de hello de un plan de recuperación con un grupo de replicación, cada grupo de replicación recuperará tooits comunes punto de recuperación disponible.
Tenga en cuenta que los puntos de recuperación coherentes con la aplicación pueden ser anteriores en el tiempo, por lo que podrían perderse datos.

### <a name="what-happens-toovmware-tools-post-failback"></a>¿Qué ocurre tooVMware herramientas registrar conmutación por recuperación?

Durante la conmutación por error tooAzure, herramientas de VMware de hello no pueden estar ejecutándose en hello máquina virtual de Azure. En el caso de una máquina virtual de Windows, ASR deshabilita las herramientas de VMware Hola durante la conmutación por error. En el caso de máquina virtual de Linux, ASR desinstala las herramientas de VMware Hola durante la conmutación por error.

Durante la conmutación por recuperación de máquina virtual de Windows hello, las herramientas de VMware Hola se vuelven a habilitadas tras la conmutación por recuperación. De forma similar, para una máquina virtual de linux, las herramientas de VMware Hola se vuelven a instalar en la máquina de Hola durante la conmutación por recuperación.

## <a name="next-steps"></a>Pasos siguientes

Una vez finalizada la conmutación por recuperación, deberá toocommit tooensure de máquina virtual de Hola que recuperar máquinas virtuales en Azure se eliminan.

### <a name="commit"></a>Confirmación
Confirmación es hello tooremove necesario conmutado por error la máquina virtual de Azure.
Haga clic en el elemento de hello protegido y, a continuación, haga clic en **confirmar**. Un trabajo, eliminará Hola conmutado por error máquinas virtuales en Azure.

### <a name="reprotect-from-on-premises-tooazure"></a>Vuelva a proteger de tooAzure local

Una vez finalizada la confirmación, la máquina virtual está en el sitio local de Hola, pero no estará protegido. una vez más, toostart tooreplicate tooAzure Hola siguientes:

1. En **almacén** > **configuración** > **replican elementos**, seleccione Hola máquinas virtuales que no se han podido nuevo y, a continuación, haga clic en  **Volver a proteger**.
2. Proporcione a valor Hola Hola del servidor de procesos que necesita toobe utiliza toosend datos back-tooAzure.
3. Haga clic en **Aceptar** trabajos de reprotección de toobegin Hola.

> [!NOTE]
> Una vez que inicia una máquina virtual de locales, tarda algún tiempo para el agente de hello servidor de configuración de tooregister toohello atrás (hacia arriba too15 minutos). Durante este tiempo, vuelva a proteger produce un error y devuelve un mensaje de error que indica a que el agente hello no está instalado. Espere unos minutos y vuelva a intentarlo.

Después de hello, vuelva a proteger al término del trabajo, máquina virtual de hello está replicando tooAzure atrás y realiza una conmutación por error.

## <a name="common-issues"></a>Problemas comunes
Asegúrese de que vCenter Hola está en estado conectado antes de realizar una conmutación por recuperación. En caso contrario, desconectar discos y conectarlos toohello atrás máquina virtual se producirá un error.
