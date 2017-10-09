---
title: "aaaFailback en Azure Site Recovery para las máquinas virtuales de Hyper-v | Documentos de Microsoft"
description: "Azure Site Recovery coordina la replicación hello, conmutación por error y recuperación de máquinas virtuales y servidores físicos. Obtenga información acerca de la conmutación por recuperación de centro de datos locales de tooon de Azure."
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
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 50cda9105de6b6fb23e4c62942fdaffc55c3efa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>Conmutación por recuperación en Site Recovery para máquinas virtuales de Hyper-V

Este artículo describe cómo se protegen las máquinas virtuales toofailback Site Recovery.

## <a name="prerequisites"></a>Requisitos previos
1. Asegúrese de que ese servidor de Hyper-V/server Hola sitio primario VMM está conectado.
2. Debe haber realizado **confirmar** en la máquina virtual de Hola.

## <a name="why-is-there-no-button-called-failback"></a>¿Por qué no hay ningún botón llamado conmutación por recuperación?
En el portal de hello, no hay ningún gesto explícito que se denomina conmutación por recuperación. Conmutación por recuperación es un paso que se vuelven a estar toohello de sitio primario. Por definición, conmutación por error es cuando se máquinas de virtuales Hola de conmutación por error de primary(on-premises) sitio toorecovery (Azure) y conmutación por recuperación al máquinas de virtuales Hola de conmutación por error de recuperación hacer copia de tooprimary.

Cuando se inicia una conmutación por error, hoja de hello le informa sobre dirección Hola de trabajo de Hola. Si dirección Hola procede tooOn-locales de Azure, es una conmutación por recuperación.

## <a name="why-is-there-only-a-planned-failover-gesture-toofailback"></a>¿Por qué hay sólo un toofailback de gesto de conmutación por error planeada?
Azure es un entorno de alta disponibilidad y las máquinas virtuales estarán siempre disponibles. Conmutación por recuperación es una actividad planeada debe decidir tootake un breve tiempo de inactividad para que las cargas de trabajo de hello pueden empezar a ejecutar en local de nuevo. No se prevé la pérdida de datos. Por lo tanto, hay solo un gesto de conmutación por error planeada, que se desactivará hello las máquinas virtuales en Azure, descargue los cambios más recientes de Hola y asegúrese de que no hay ninguna pérdida de datos.

## <a name="initiate-failback"></a>Inicio de la conmutación por recuperación
Después de la conmutación por error de ubicación de hello toosecondary principal, las máquinas virtuales replicadas no están protegidas por recuperación del sitio y ubicación secundaria Hola ahora está actuando como ubicación de active Hola. Siga estos procedimientos toofail toohello back-sitio principal original. Este procedimiento describe cómo toorun una conmutación por error planeada para una recuperación del plan. También puede ejecutar Hola conmutación por error para una sola máquina virtual en hello **máquinas virtuales** ficha.

1. Seleccione **Recovery Plans** > *nombreDePlanDeRecuperación*. Haga clic en **Conmutación por error** > **Planned Conmutación por error**.
2. En Hola ** confirmar conmutación por error planeada ** página, elija las ubicaciones de origen y destino de Hola. Tenga en cuenta dirección de conmutación por error de Hola. Si ha trabajado Hola conmutación por error de principal como esperar y todas las máquinas virtuales están en la ubicación secundaria hello es meramente informativos.
3. Si realiza la conmutación por recuperación desde Azure, seleccione la configuración en **Sincronización de datos**:

   * **Sincronizar datos antes de la conmutación por error (sincronizar solo cambios incrementales)**: esta opción reduce al mínimo el tiempo de inactividad de las máquinas virtuales, ya que realiza la sincronización sin apagarlas. Hola siguientes:
     * Fase 1: Toma instantáneas de máquina virtual de hello en Azure y copia host de Hyper-V local toohello. máquina de Hello continúa ejecutándose en Azure.
     * Fase 2: Apaga la máquina virtual de hello en Azure, para que no dar ningún cambio de nuevo. Hola último conjunto de cambios delta es servidor local de toohello transferidos y máquina virtual de hello local se haya iniciado.

    - **Sincronizar datos solo durante la conmutación por error (descarga completa)**: utilice esta opción si ha estado trabajando en Azure durante mucho tiempo. Esta opción es más rápida porque se espera que la mayoría de disco Hola ha cambiado y no es aconsejable toospend tiempo en el cálculo de suma de comprobación. Realiza una descarga del disco de Hola. También es útil cuando se ha eliminado la máquina virtual de hello en local.

    >[!NOTE]
    >Se recomienda usar esta opción si ha estado ejecutando Azure durante un tiempo (un mes o más) o se ha eliminado la máquina virtual de hello en local. Esta opción no realiza los cálculos de suma de comprobación.
    >
    >




4. Si está habilitado el cifrado de datos de nube de hello en **clave de cifrado** certificado Hola seleccione emitido cuando habilita el cifrado de datos durante la instalación del proveedor en el servidor VMM Hola.
5. Iniciar la conmutación por error de Hola. Puede seguir el progreso de la conmutación por error de Hola en hello **trabajos** ficha.
6. Si seleccionó Hola opción toosynchronize Hola datos antes de hello conmutación por error, una vez Hola inicial se completa la sincronización de datos y está listo tooshut hacia abajo hello las máquinas virtuales en Azure, haga clic en **trabajos** el nombre del trabajo de conmutación por error planeada **Completar la conmutación por error**. Esto apaga de Hola máquina de Azure, hello las transferencias cambia más reciente máquina virtual de toohello local e inicia Hola VM local.
7. Ahora puede iniciar sesión en hello toovalidate de máquina virtual está disponible según lo previsto.
8. máquina virtual de Hello está en un estado de confirmación pendiente. Haga clic en **confirmar** conmutación por error de toocommit Hola.
9. Ahora en orden de conmutación por recuperación de toocomplete hello, haga clic en **replicación inversa** toostart protección de máquina virtual de hello en el sitio primario de Hola.

## <a name="failback-tooan-alternate-location"></a>Ubicación alternativa de conmutación por recuperación tooan
Si ha implementado la protección entre un [sitio de Hyper-V y Azure](site-recovery-hyper-v-site-to-azure.md) tiene tooability toofailback de ubicación de Azure tooan alternativo en local. Esto es útil si necesita tooset de nuevo hardware local. Así es cómo debe hacerlo.

1. Si está configurando un hardware nuevo instalar Windows Server 2012 R2 y Hola rol de Hyper-V en el servidor de Hola.
2. Crear un conmutador de red virtual con el mismo nombre que tenía en el servidor original Hola de Hola.
3. Seleccione **elementos protegidos** -> **grupo de protección**  ->  <ProtectionGroupName>  ->  <VirtualMachineName> desee toofail atrás y seleccione **planificado Conmutación por error**.
4. En **Confirmar conmutación por error planeada** select **Crear máquina virtual local si no existe**.
5. En **nombre de Host** seleccione Hola nuevo servidor de host de Hyper-V que servirá de máquina virtual de tooplace Hola.
6. En la sincronización de datos, se recomienda que seleccione la opción de hello **sincronizar datos de hello antes de la conmutación por error de hello**. Así se reduce el tiempo de inactividad de las máquinas virtuales, ya que la sincronización se realiza sin apagarlas. Hola siguientes:

   * Fase 1: Toma instantáneas de máquina virtual de hello en Azure y copia host de Hyper-V local toohello. máquina de Hello continúa ejecutándose en Azure.
   * Fase 2: Apaga la máquina virtual de hello en Azure, para que no dar ningún cambio de nuevo. Hola último conjunto de cambios son servidor local de toohello transferidos y máquina virtual de hello local se haya iniciado.
7. Haga clic en hello marca de verificación toobegin Hola de conmutación por error (conmutación por recuperación).
8. Una vez finalizada la sincronización inicial de Hola y está listo tooshut hacia abajo de la máquina virtual de hello en Azure, haga clic en **trabajos** > <planned failover job> > **conmutación por error completa**. Esto apaga Hola máquina de Azure, máquina virtual local toohello de cambios más reciente de las transferencias hello y lo inicia.
9. Puede iniciar sesión en tooverify de máquina virtual local de Hola que todo funciona según lo previsto. A continuación, haga clic en **confirmar** conmutación por error de toofinish Hola.
10. Haga clic en **replicación inversa** toostart protección de máquina virtual de hello en local.

    > [!NOTE]
    > Si se cancela el trabajo de conmutación por recuperación de hello mientras se encuentra en el paso de sincronización de datos, Hola local VM estará en un estado dañado. Esto es porque la sincronización de datos copia los datos más recientes de Hola de discos de datos de Azure VM discos toohello local, y hasta que se complete la sincronización de hello, datos del disco hello no estén en un estado coherente. Si Hola VM local se inicia después de cancelar la sincronización de datos, no puede arrancar. Volver a activar la conmutación por error toocomplete Hola la sincronización de datos.
    >
    >



## <a name="next-steps"></a>Pasos siguientes

Cuando haya completado el trabajo de conmutación por recuperación de hello, **confirmar** máquina virtual de Hola. Confirmación elimina Hola máquina virtual de Azure y sus discos y prepara Hola VM toobe nuevamente protegido.

Después de **confirmar**, puede iniciar hello *replicación inversa*. Se iniciará la protección de máquina Hola de tooAzure atrás local. Tenga en cuenta Esto configurará sólo los cambios de hello replicar desde Hola máquina virtual se ha desactivado en Azure y, por lo que envía diferencial sólo cambia.
