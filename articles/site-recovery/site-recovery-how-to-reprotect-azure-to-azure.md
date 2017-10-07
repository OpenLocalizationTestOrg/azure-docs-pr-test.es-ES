---
title: "aaaHow tooReprotect de conmutado por error máquinas virtuales de Azure espera tooprimary región de Azure | Documentos de Microsoft"
description: "Después de la conmutación por error de máquinas virtuales de tooanother de una región de Azure, puede usar máquinas de Azure Site Recovery tooprotect hello en dirección inversa. Obtenga información acerca de los pasos de hello cómo toodo una reprotección antes de una conmutación por error de nuevo."
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
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a>Reprotección de conmutado por región tooprimary atrás de región de Azure



>[!NOTE]
>
> La replicación de Site Recovery en máquinas virtuales de Azure se encuentra actualmente en versión preliminar.


## <a name="overview"></a>Información general
Cuando se [conmutación por error](site-recovery-failover.md) máquinas virtuales de Hola de tooanother de una región de Azure, hello las máquinas virtuales están en un estado desprotegido. Si desea que toobring les toohello de región principal, debe toofirst proteger máquinas virtuales de hello y, a continuación, la conmutación por error de nuevo. No hay ninguna diferencia entre cómo se conmuta por error en una dirección u otra. Del mismo modo, después de habilitar la protección de máquinas virtuales de hello, no hay ninguna diferencia entre hello reprotección posteriores conmutación por error o conmutación por recuperación de post.
flujos de trabajo de hello tooexplain de reprotección y tooavoid confusión, usaremos sitio primario Hola de máquinas de hello protegido como región Asia oriental y el sitio de recuperación de Hola de máquinas de hello como región sudeste asiático. Durante la conmutación por error, tendrá que toohello sudeste asiático región de conmutación por error Hola máquinas virtuales. Antes, conmutación por recuperación, deberá tooreprotect Hola máquinas de tooEast atrás del sudeste de Asia oriental. En este artículo se describe los pasos de hello en cómo tooreprotect.

> [!WARNING]
> Si tiene [completar la migración](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), recurso de tooanother de máquina virtual movida hello, o un grupo eliminado Hola máquina virtual de Azure, no podrá volver a continuación.

Una vez reprotección finaliza y replicar máquinas virtuales de hello protegido, puede iniciar una conmutación por error en toobring de máquinas virtuales de hello vuelven a región del Asia tooEast.

Enviar comentarios o preguntas al final de Hola de este artículo o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Requisitos previos
1. máquinas virtuales de Hello deben se han confirmado.
2. sitio de destino de Hello: en este caso hello Azure de Asia oriental región debe estar disponible y debe ser capaz de tooaccess o crear nuevos recursos en dicha región.

## <a name="steps-tooreprotect"></a>Tooreprotect de pasos

A continuación se Hola pasos tooreprotect una máquina virtual con los valores predeterminados de Hola.

1. En **almacén** > **replican elementos**, haga clic en la máquina virtual de Hola que se ha conmutado por error y, a continuación, seleccione **volver a proteger**. También puede hacer clic en hello equipo y seleccione **volver a proteger** de botones de comando de Hola.

![Haga clic en tooreprotect](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. En la hoja de hello, tenga en cuenta esa dirección Hola de protección, **sudeste de Asia tooEast asia**, ya está seleccionado.

![Volver a proteger la hoja](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. Hola de revisión **grupos, red, almacenamiento y disponibilidad conjuntos de recursos** información y haga clic en Aceptar. Si no hay ningún recurso marcado (nuevo), se creará como parte del programa Hola, vuelva a proteger.

Esto se desencadenador un trabajo, vuelva a proteger el trabajo que se va a inicializar primero sitio de destino de hello (mar en este caso) con datos más recientes de hello y una vez que se completa, se replicarán deltas de hello antes de la conmutación por error copia tooSoutheast Asia.

### <a name="reprotect-customization"></a>Volver a proteger la personalización
Si desea que toochoose hello extracción almacenamiento red cuenta u Hola durante, vuelva a proteger, puede hacerlo con hello personalizar opción proporcionada en la hoja de reprotección Hola.

![Opción de personalización](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

Puede personalizar Hola siguientes propiedades de máquina virtual de destino de durante reprotección.

![Personalizar la hoja](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|Propiedad |Notas  |
|---------|---------|
|Grupo de recursos de destino     | Puede elegir el grupo de recursos de destino toochange hello en el que se creará la máquina virtual de th. Como parte de Hola de reprotección, se eliminará la máquina virtual de destino de hello, por lo tanto, puede elegir un nuevo grupo de recursos en la que puede crear Hola VM posterior conmutación por error         |
|Red virtual de destino     | No se puede cambiar la red durante reprotección Hola. Hola toochange de red, la asignación de red Hola de puesta al día.         |
|Almacenamiento de destino     | Puede cambiar la cuenta de almacenamiento de hello toowhich Hola virtual machine será posterior creado conmutación por error.         |
|Almacenamiento en caché     | Puede especificar una cuenta de almacenamiento en caché que se usará durante la replicación. Si va con valores predeterminados de hello, se creará una nueva cuenta de almacenamiento de caché, si aún no existe.         |
|Conjunto de disponibilidad     |Si la máquina virtual de hello en Asia oriental forma parte de un conjunto de disponibilidad, puede elegir un conjunto de disponibilidad de la máquina virtual de destino de hello en sudeste de Asia. Los valores predeterminados buscará conjunto de disponibilidad SEA existente Hola e intente toouse lo. Durante la personalización, puede especificar un conjunto de disponibilidad completamente nuevo.         |


### <a name="what-happens-during-reprotect"></a>¿Qué ocurre durante la reprotección?

Simplemente como Hola después de habilitar la protección, los siguientes son artefactos de Hola que se crean si utiliza los valores predeterminados de Hola.
1. Una cuenta de almacenamiento de la memoria caché se crea en la región de Asia oriental Hola.
2. Si no existe la cuenta de almacenamiento de destino de hello (Hola original cuenta de almacenamiento de hello VM sudeste de Asia), se crea uno nuevo. nombre de Hello es la cuenta de almacenamiento de la máquina virtual de hello Asia oriental lleva el sufijo "asr".
3. Si no existe el conjunto de destinos AV de Hola y valores predeterminados de hello detectan que necesita toocreate establece una nueva AV, a continuación, se creará como parte del programa Hola a proteger el trabajo. Si ha personalizado hello, vuelva a proteger, a continuación, conjunto de AV de hello seleccionado se usará.
4.

siguiente Hola es lista Hola de pasos que se producen al activar un trabajo de reprotección. Se trata en el lado de destino de Hola Hola casos existe la máquina virtual.

1. Hola necesario artefactos se crean como parte de reprotección. Si ya existen, se vuelven a usar.
2. máquina virtual de Hello destino lado (sudeste de Asia) en primer lugar se ha desactivado, si se está ejecutando.
3. disco de Hello destino lado de la máquina virtual se copia con Azure Site Recovery en un contenedor como un blob de inicialización.
4. a continuación, se elimina la máquina virtual de Hello destino lado.
5. blob de inicialización de Hello usa tooreplicate de máquina virtual de origen actual de hello lado (Asia oriental). Esto garantiza que solo se repliquen los valores delta.
6. Hola cambios importantes entre el disco de origen de Hola y blob de inicialización de Hola se sincronizan. Esta operación puede tardar algún tiempo toocomplete.
7. Una vez que vuelva a proteger Hola trabajo se completa, comienza la replicación de datos de Hola que crea un punto de recuperación según la directiva de Hola.

> [!NOTE]
> No se puede proteger en un nivel de plan de recuperación. Solo se puede volver a proteger en un nivel de máquina virtual.

Después, vuelva a proteger Hola correcta, máquina virtual de hello pasará a un estado protegido.

## <a name="next-steps"></a>Pasos siguientes

Después de máquina virtual de hello ha entrado en un estado protegido, puede iniciar una conmutación por error. Hola conmutación por error se apagar la máquina virtual de hello en la región de Azure de Asia oriental y, a continuación, cree y arrancar máquina virtual de hello sudeste de Asia región. Por lo tanto, no hay un breve tiempo de inactividad de la aplicación hello. Por lo tanto, seleccione hora de Hola de conmutación por error cuando la aplicación puede tolerar un tiempo de inactividad. Se recomienda que pruebe primero la máquina virtual de conmutación por error hello toomake seguro de que viene a continuación correctamente, antes de iniciar una conmutación por error.

-   [Pasos tooinitiate probar conmutación por error de la máquina virtual de Hola](site-recovery-test-failover-to-azure.md)

-   [Conmutación por error tooinitiate de pasos de la máquina virtual de Hola](site-recovery-failover.md)
