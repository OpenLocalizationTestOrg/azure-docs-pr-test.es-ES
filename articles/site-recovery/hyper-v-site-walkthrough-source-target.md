---
title: "aaaSet seguridad Hola origen y de destino para tooAzure de replicación de Hyper-V (sin System Center VMM) con Azure Site Recovery | Documentos de Microsoft"
description: "Resume Hola pasos tooset la configuración de origen y de destino para la replicación de almacenamiento de máquinas virtuales de Hyper-V tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a>Paso 8: Configurar origen de Hola y de destino para tooAzure de replicación de Hyper-V

Este artículo describe cómo tooconfigure de configuración de origen y de destino cuando se replican de manera local tooAzure de máquinas virtuales (sin System Center VMM) de Hyper-V, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

Configurar el sitio de Hyper-V de hello, instalar Hola proveedor de Azure Site Recovery y el agente de servicios de recuperación de Azure de hello en hosts de Hyper-V y registrar sitio hello en el almacén de Hola.

1. En **Preparar infraestructura**, haga clic en **Origen**. Haga clic en un nuevo sitio de Hyper-V como un contenedor para los hosts de Hyper-V o clústeres, tooadd **+ sitio de Hyper-V**.

    ![Configurar origen](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. En **sitio Hyper-V crear**, especifique un nombre para el sitio de Hola. y, a continuación, haga clic en **Aceptar**. Ahora, seleccione el sitio de Hola que creó y, después, haga clic en **+ servidor Hyper-V** tooadd un sitio de toohello de servidor.

    ![Configurar origen](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. En **Agregar servidor** > **Tipo de servidor**, compruebe que se muestra **Hyper-V Server**.

    - Asegúrese de que ese servidor hello Hyper-V que desee tooadd cumple con hello [requisitos previos](#on-premises-prerequisites), y es capaz de tooaccess Hola direcciones URL especificadas.
    - Descargar archivo de instalación del proveedor de Azure Site Recovery de Hola. Ejecute este hello de tooinstall archivo proveedor y Hola agente de servicios de recuperación en cada host de Hyper-V.

    ![Configurar origen](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Instalar Hola proveedor y agente

1. Ejecutar el archivo de instalación de proveedor de hello en cada host agregado toohello Hyper-V sitio. Si va a realizar la instalación en un clúster de Hyper-V, ejecute el programa de instalación en cada nodo de clúster. Instalar y registrar los nodos de cada clúster de Hyper-V garantiza que las máquinas virtuales permanezcan protegidas incluso si se migran entre nodos.
2. En **Microsoft Update** puede optar por recibir actualizaciones para que las actualizaciones del proveedor se realicen según las directivas de Microsoft Update.
3. En **instalación**, acepte o modifique la ubicación de instalación de proveedor de hello predeterminada y haga clic en **instalar**.
4. En **configuración del almacén**, haga clic en **examinar** tooselect Hola almacén archivo de clave que ha descargado. Especifique la suscripción de Azure Site Recovery Hola, nombre del almacén de hello, y pertenece Hola Hyper-V sitio toowhich Hola Hyper-V server.

    ![Registro de servidor](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. En **configuración de Proxy**, especifique cómo Hola Hola que se ejecutan en hosts de Hyper-V conectará tooAzure Site Recovery por proveedor a internet.

    * Si desea que Hola proveedor tooconnect directamente seleccione **conectarse directamente tooAzure Site Recovery sin un proxy**.
    * Si el proxy existente requiere autenticación, o si desea toouse un proxy personalizado para la conexión del proveedor de hello, seleccione **conectar tooAzure Site Recovery con un servidor proxy**.
    * Si utiliza un proxy:
        - Especifique las credenciales, el puerto y la dirección de Hola
        - Hace que direcciones URL de hello descritas en hello [requisitos previos](#prerequisites) se permiten a través de proxy de Hola.

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. Una vez finalizada la instalación, haga clic en **registrar** tooregister servidor de hello en el almacén de Hola.

    ![Ubicación de instalación](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. Después de que finalice el registro, Azure Site Recovery recupera metadatos del servidor de Hyper-V de Hola y Hola servidor se muestra en **infraestructura del sitio de recuperación** > **Hosts de Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Configurar el entorno de destino de Hola

Especifique la cuenta de almacenamiento de Azure de hello para la replicación y hello toowhich de red de Azure máquinas virtuales de Azure se conectará tras la conmutación por error.

1. Haga clic en **Preparar infraestructura** > **Destino**.
2. Seleccione la suscripción de Hola y el grupo de recursos de hello en el que desea toocreate Hola máquinas virtuales de Azure después de la conmutación por error. Elija Hola implementación modelo que quiere toouse en Azure (classic o recursos administración) de hello las máquinas virtuales.

3. Site Recovery comprueba que tiene una o más redes y cuentas de Azure Storage compatibles.

    - Si no tienes una cuenta de almacenamiento, haga clic en **+ almacenamiento** toocreate un insertado cuenta basada en el Administrador de recursos. 
    - Si no tiene una red de Azure, haga clic en **+ red** toocreate un insertado de red basada en el Administrador de recursos.






## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 9: configurar una directiva de replicación](hyper-v-site-walkthrough-replication.md)
