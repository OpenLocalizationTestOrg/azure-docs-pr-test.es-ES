---
title: aaaFailover en Site Recovery | Documentos de Microsoft
description: "Azure Site Recovery coordina la replicación hello, conmutación por error y recuperación de máquinas virtuales y servidores físicos. Obtenga información acerca de la conmutación por error tooAzure o un centro de datos secundaria."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>Conmutación por error en Site Recovery
Este artículo describe cómo protegen Site Recovery toofailover las máquinas virtuales y servidores físicos.

## <a name="prerequisites"></a>Requisitos previos
1. Antes de realizar una conmutación por error, realice una [probar conmutación por error](site-recovery-test-failover-to-azure.md) tooensure que todo funciona según lo previsto.
1. [Preparar la red de hello](site-recovery-network-design.md) en la ubicación de destino antes de realizar una conmutación por error.  


## <a name="run-a-failover"></a>Ejecución de la conmutación por error
Este procedimiento describe cómo toorun una conmutación por error para un [plan de recuperación](site-recovery-create-recovery-plans.md). También puede ejecutar Hola conmutación por error para un servidor físico o máquina virtual única de hello **replican elementos** página


![Conmutación por error](./media/site-recovery-failover/Failover.png)

1. Seleccione **Recovery Plans** > *nombreDePlanDeRecuperación*. Haga clic en **Conmutación por error**.
2. En hello **conmutación por error** pantalla, seleccione un **punto de recuperación** toofailover a. Puede usar uno de hello siguientes opciones:
    1.  **Última** (valor predeterminado): esta opción procesa primero todos los datos de Hola que se ha enviado tooSite recuperación servicio toocreate un punto de recuperación para cada máquina virtual antes de conmutar a tooit. Esta opción proporciona Hola menor RPO (objetivo de punto de recuperación) como máquina de virtual Hola creada después de conmutación por error tiene todos los datos de Hola que se ha replicado tooSite el servicio de recuperación cuando se activó la conmutación por error de Hola.
    1.  **Procesar más reciente**: esta opción se conmuta todas las máquinas virtuales de hello recuperación plan toohello último punto de recuperación que ya ha sido procesado por el servicio de Site Recovery. Cuando realiza una conmutación por error de prueba de una máquina virtual, también se muestra la marca de tiempo de punto de recuperación procesada más reciente de Hola. Si realiza una conmutación por error de un plan de recuperación, puede ir de máquina virtual de tooindividual y mirar **puntos de recuperación más reciente** icono tooget esta información. A medida que se empleó ningún tiempo tooprocess Hola datos sin procesar, esta opción proporciona una opción de conmutación por error bajo RTO (objetivo de tiempo de recuperación).
    1.  **Más reciente coherente con la aplicación**: esta opción se conmuta todas las máquinas virtuales Hola plan toohello más reciente aplicación coherente recuperación del punto de recuperación que ya ha sido procesado por el servicio de recuperación del sitio. Cuando realiza una conmutación por error de prueba de una máquina virtual, también se muestra la marca de tiempo del último punto de recuperación coherente con la aplicación hello. Si realiza una conmutación por error de un plan de recuperación, puede ir de máquina virtual de tooindividual y mirar **puntos de recuperación más reciente** icono tooget esta información.
    1.  **Latest multi-VM processed** (Últimas máquinas virtuales procesadas): esta opción solo está disponible para planes de recuperación que tienen al menos una máquina virtual con la coherencia para varias máquinas virtuales activada. Punto de máquinas virtuales que forman parte de una replicación grupo conmutación por error toohello recuperación más reciente comunes varias VM coherente. Otra máquinas virtuales conmutación por error tootheir más reciente procesado punto de recuperación.  
    1.  **Latest multi-VM app-consistent** (Últimas máquinas virtuales coherentes con la aplicación): esta opción solo está disponible para planes de recuperación que tienen al menos una máquina virtual con la coherencia para varias máquinas virtuales activada. Máquinas virtuales que forman parte de una replicación de grupo de conmutación por error toohello más reciente varias VM coherentes con la aplicación de punto de recuperación común. Otra máquinas virtuales conmutación por error tootheir más reciente coherente con la aplicación el punto de recuperación.
    1.  **Personalizado**: si está realizando la conmutación por error de prueba de una máquina virtual, puede usar este punto de recuperación concreto de opción toofailover tooa.

    > [!NOTE]
    > Hola opción toochoose un punto de recuperación sólo está disponible cuando se conmuta por error tooAzure.
    >
    >


1. Si algunas de las máquinas virtuales de Hola Hola plan de recuperación se han conmutado por error en una ejecución anterior y ahora hello las máquinas virtuales están activas en la ubicación de origen y de destino, puede usar **cambiar dirección** opción dirección de hello toodecide en debería ocurrir que conmutan por error de Hola.
1. Si está conmuta tooAzure y está habilitado el cifrado de datos para la nube de hello (se aplica solo cuando se protegieron máquinas virtuales Hyper-v desde un servidor de VMM), en **clave de cifrado** certificado Hola select que se emite cuando se habilitar el cifrado de datos durante la instalación en el servidor VMM Hola.
1. Seleccione **apagar la máquina antes de comenzar la conmutación por error** si desea Site Recovery tooattempt toodo un apagado de máquinas virtuales de origen antes de activar Hola conmutación por error. La conmutación por error continúa aunque se produzca un error de cierre.  

    > [!NOTE]
    > En el caso de máquinas virtuales de Hyper-v, esta opción también trata los datos locales de toosynchronize Hola que aún no se ha enviado toohello servicio antes de activar Hola conmutación por error.
    >
    >

1. Puede seguir el progreso de la conmutación por error de Hola en hello **trabajos** página. Incluso si se producen errores durante una conmutación por error no planeada, plan de recuperación de Hola se ejecuta hasta que se complete.
1. Después de la conmutación por error de hello, validar máquina virtual de hello mediante el registro en tooit. Si desea toogo otro punto de recuperación para la máquina virtual de hello, puede usar **cambiar punto de recuperación** opción.
1. Una vez que esté satisfecho con hello conmutado por máquina virtual, puede **confirmar** Hola conmutación por error. Esto elimina todos los puntos de recuperación de hello disponibles con el servicio de Hola y **cambiar punto de recuperación** opción ya no estará disponible.

## <a name="planned-failover"></a>Conmutación por error planeada
Además de la conmutación por error, las máquinas virtuales de Hyper-V protegidas con Site Recovery también son compatibles con la **Conmutación por error planeada**. Se trata de una opción de conmutación por error sin pérdida de datos. Cuando se desencadena una conmutación por error planeada, en primer lugar Hola origen máquinas virtuales se apagan, datos de hello aún se está sincronizada toobe sincronizado y, a continuación, se desencadena una conmutación por error.

> [!NOTE]
> Cuando se máquinas virtuales de Hyper-v de conmutación por error de un local tooanother de sitio local sitio, toocome toohello atrás local principal tiene toofirst **invertir la replicación** sitio de tooprimary atrás de máquina virtual de Hola y a continuación, desencadenar una conmutación por error. Si la máquina virtual principal de hello no está disponible, a continuación, antes de iniciar demasiado**invertir la replicación** tiene máquina virtual del toorestore Hola desde una copia de seguridad.   
>
>

## <a name="failover-job"></a>Trabajo de conmutación por error

![Conmutación por error](./media/site-recovery-failover/FailoverJob.png)

Cuando se desencadena una conmutación por error, se realizan estos pasos:

1. Comprobación de los requisitos previos: en este paso se garantiza que se cumplen todas las condiciones necesarias para la conmutación por error.
1. Conmutación por error: Este paso procesa los datos de Hola y sea listo para que se puede crear una máquina virtual de Azure fuera de ella. Si ha elegido **más reciente** punto de recuperación, este paso crea un punto de recuperación de datos de Hola que se ha enviado el servicio toohello.
1. Inicio: En este paso se crea una máquina virtual de Azure utilizando los datos de hello procesados en el paso anterior de Hola.

> [!WARNING]
> **No cancelar un curso en conmutación por error**: antes de inicia la conmutación por error, se detiene la replicación de la máquina virtual de Hola. Si se **cancelar** un trabajo de progreso, se detiene la conmutación por error pero la máquina virtual de hello no se iniciará tooreplicate. La replicación no se puede reiniciar.
>
>

## <a name="time-taken-for-failover-tooazure"></a>Tiempo de conmutación por error tooAzure

En algunos casos, conmutación por error de máquinas virtuales requiere un paso adicional intermedio que normalmente tarda aproximadamente 8 too10 minutos toocomplete. Estos casos son los siguientes:

* Máquinas virtuales de VMware con el servicio de movilidad de una versión anterior a 9.8
* Servidores físicos 
* Máquinas virtuales de VMware Linux
* Máquinas virtuales Hyper-V protegidas como servidores físicos
* Máquinas virtuales de VMware donde los siguientes controladores no están presentes como controladores de arranque 
    * storvsc 
    * vmbus 
    * storflt 
    * intelide 
    * atapi
* Máquinas virtuales de VMware que no tienen el servicio DHCP habilitado independientemente de si usan direcciones IP estáticas o DHCP

En hello todos los demás casos este paso intermedio no es necesaria y tiempo Hola de conmutación por error de hello es notablemente inferior. 





## <a name="using-scripts-in-failover"></a>Uso de scripts en la conmutación por error
Puede ser conveniente tooautomate determinadas acciones mientras realiza una conmutación por error. Puede utilizar secuencias de comandos o [runbooks de automatización de Azure](site-recovery-runbook-automation.md) en [planes de recuperación](site-recovery-create-recovery-plans.md) toodo que.

## <a name="other-considerations"></a>Otras consideraciones
* **Letra de unidad** : tooretain letra de unidad de hello en máquinas virtuales después de la conmutación por error puede establecer hello **directiva SAN** para hello virtual automático demasiado**OnlineAll**. [Más información](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>Pasos siguientes
Una vez que han conmutado máquinas virtuales y centro de datos local de hello está disponible, debe [ **volver a proteger** ](site-recovery-how-to-reprotect.md) centro de datos local de toohello hacer copia de máquinas virtuales de VMware.

Use [ **conmutación por error planeada** ](site-recovery-failback-from-azure-to-hyper-v.md) opción demasiado**conmutación por recuperación** tooon local realizar copia de máquinas virtuales de Hyper-v de Azure.

Si ha producido un error sobre un datos de local de tooanother de máquina virtual de Hyper-v está disponible center administrado por un centro de datos principal de hello y servidor VMM, a continuación, utilice **replicación inversa** opción toostart Hola replicación inversa toohello Centro de datos principal.
