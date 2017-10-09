---
title: "Replicar máquinas virtuales de Azure entre regiones de Azure para las necesidades de recuperación ante desastres: tooAzure Azure | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooreplicate máquinas virtuales de Azure entre regiones de Azure (Azure en Azure) con el servicio de Azure Site Recovery de Hola para las necesidades de recuperación ante desastres."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Replicación de máquinas virtuales de Azure entre regiones con Azure Site Recovery

>[!NOTE]
>
> La replicación de Azure Site Recovery en máquinas virtuales (VM) de Azure está actualmente en versión preliminar.

Este artículo describe cómo tooreplicate máquinas virtuales de Azure entre regiones de Azure mediante el uso de Hola [Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="disaster-recovery-in-azure"></a>Recuperación ante desastres en Azure

Características y capacidades de infraestructura de Azure integrada contribuyen tooa estrategia de disponibilidad sólido y flexible para cargas de trabajo que se ejecutan en máquinas virtuales de Azure. Sin embargo, hay muchas razones por qué necesita tooplan para la recuperación ante desastres entre regiones de Azure por sí mismo:

- Directrices de cumplimiento del toomeet que necesita para aplicaciones específicas y las cargas de trabajo que requieren una continuidad del negocio y la estrategia de recuperación (BCDR).
- Desea tooprotect de capacidad de Hola y recuperar máquinas virtuales basándose en sus decisiones de negocios y no solo de Azure basado en la funcionalidad de Azure integrada.
- Necesitará tootest conmutación por error y recuperación según sus necesidades empresariales y cumplimiento de normas, sin tener impacto en producción.
- Es necesario toofail sobre toohello región de recuperación en caso de hello de un desastre y producirá un error de región de origen original toohello atrás sin problemas.

Use la recuperación del sitio para toohelp de replicación de máquina virtual de Azure en Azure puede realizar todas estas tareas.


## <a name="why-use-site-recovery"></a>¿Por qué usar Site Recovery?      

Site Recovery ofrece una manera sencilla de tooreplicate máquinas virtuales de Azure entre regiones:

- **Implementación automática**. A diferencia de un modelo de replicación activo / activo, no es necesario para una infraestructura cara y compleja en la región secundaria Hola. Cuando se habilita la replicación, Site Recovery crea automáticamente los recursos de hello necesario en la región de destino de hello, en función de la configuración de la región de origen.
- **Controla de las regiones**. Con la recuperación del sitio, puede replicar desde cualquier región tooany otra dentro de un continente. En comparación con esto, el almacenamiento con redundancia geográfica con acceso de lectura replica de forma asincrónica solo entre [regiones emparejadas](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) estándar. Almacenamiento con redundancia geográfica con acceso de lectura proporciona datos de toohello de acceso de solo lectura en la región de destino de Hola.
- **Replicación automatizada**. Site Recovery proporciona replicación continua automatizada. Con un solo clic es posible desencadenar la conmutación por error y por recuperación.
- **RTO y RPO**. Recuperación de sitio aprovecha la infraestructura de red de Azure de Hola que conecta las regiones tookeep RTO y el RPO muy baja.
- **Prueba**. Puede ejecutar maniobras de recuperación ante desastres con conmutaciones por error de prueba a petición, como y cuando sea necesario, sin que las cargas de trabajo de producción o la replicación en curso se vean afectadas.
- **Planes de recuperación**. Puede utilizar la conmutación por error el tooorchestrate de planes de recuperación y conmutación por recuperación de aplicación completo Hola se ejecuta en varias máquinas virtuales. característica de plan de recuperación de Hello tiene integración enriquecida de primera clase con runbooks de automatización de Azure.


## <a name="deployment-summary"></a>Resumen de implementación

Este es un resumen de lo que necesita toodo tooset la replicación de máquinas virtuales entre las regiones de Azure:

1. Cree un almacén de Recovery Services. almacén de Hello contiene valores de configuración y organiza la replicación.
2. Habilitar la replicación de hello máquinas virtuales de Azure.
3. Ejecutar un toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.

>[!IMPORTANT]
>
> Puede comprobar hello [matriz de compatibilidad para la replicación de máquina virtual de Azure](./site-recovery-support-matrix-azure-to-azure.md).

>[!IMPORTANT]
>
> Para obtener información sobre cómo tooconfigure Hola requiere conectividad de red saliente para máquinas virtuales de Azure para la replicación de Site Recovery, vea hello [documento de guía de red](./site-recovery-azure-to-azure-networking-guidance.md).

### <a name="before-you-start"></a>Antes de comenzar

* Su cuenta de usuario de Azure necesita toohave determinados [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una máquina virtual de Azure.
* Su suscripción de Azure debe ser máquinas virtuales de toocreate habilitado en la ubicación de destino de Hola que desea toouse como región de recuperación ante desastres de Hola. Póngase en contacto con soporte técnico tooenable Hola necesario cuota.

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Le recomendamos que cree el almacén de servicios de recuperación de hello en ubicación de Hola donde desea que su tooreplicate de máquinas virtuales. Por ejemplo, si la ubicación de destino es hello centro nos, crear almacén de hello en **Central US**.

## <a name="enable-replication"></a>Habilitar replicación

En **servicios de recuperación de los almacenes de credenciales**, haga clic en el nombre del almacén de Hola. En el almacén de hello, haga clic en hello **+ replicar** botón.

### <a name="step-1-configure-hello-source"></a>Paso 1. Configurar origen de Hola
1. En **Origen**, seleccione **Azure - VERSIÓN PRELIMINAR**.
2. En **ubicación de origen**, seleccione origen Hola región de Azure donde se están ejecutando las máquinas virtuales.
3. Modelo de implementación de hello SELECT de las máquinas virtuales: **el Administrador de recursos** o **clásico**.
4. Seleccione hello **grupo de recursos de origen** para las máquinas virtuales del Administrador de recursos o **servicio en la nube** para las VM clásicas.

    ![Configurar origen de Hola](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>Paso 2: Selección de máquinas virtuales

* Seleccione hello las máquinas virtuales que desee tooreplicate y, a continuación, haga clic en **Aceptar**.

    ![Selección de las máquinas virtuales](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>Paso 3: Definición de la configuración

1. predeterminado de hello toooverride configuración de destino y especifique la configuración de Hola de su elección, haga clic en **personalizar**. Para más información, consulte [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources) (Personalización de los recursos de destino).

    ![Definición de la configuración](./media/site-recovery-azure-to-azure/settings.png)


2. De forma predeterminada, Site Recovery crea una directiva de replicación que toma cada 4 horas instantáneas coherentes con la aplicación y conserva los puntos de recuperación durante 24 horas. toocreate una directiva con distintos valores, haga clic en **personalizar** siguiente demasiado**directiva de replicación**.

    ![Personalización de la directiva](./media/site-recovery-azure-to-azure/customize-policy.png)

3. Haga clic en recursos de destino de hello aprovisionamiento toostart **crear recursos de destino**. El aprovisionamiento tarda aproximadamente un minuto. No cierre la hoja de Hola durante el aprovisionamiento, o si debe toostart sobre.

4. replicación tootrigger de hello seleccionado VM, haga clic en **habilitar la replicación**.

5. Puede seguir el progreso del programa Hola a **habilitar la protección** de trabajo en **configuración** > **trabajos** > **trabajos de recuperación de sitio**.

6. En **configuración** > **replican elementos**, puede ver el estado de Hola de máquinas virtuales y Hola progreso de la replicación inicial. Haga clic en hello VM toodrill hacia abajo en su configuración.

## <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

Una vez configurado todo, ejecute un toomake de conmutación por error de prueba que todo funciona según lo esperado:

1. toofail a través de un único equipo, en **configuración** > **replican elementos**, haga clic en hello VM **+ conmutación por error de prueba** icono.

2. toofail a través de una recuperación del plan, en **configuración** > **planes de recuperación**, plan de hello contextual **conmutación por error de prueba**. un plan de recuperación, toocreate [, siga estas instrucciones](site-recovery-create-recovery-plans.md). 

3. En **conmutación por error de prueba**, seleccione toowhich de red virtual de Azure de destino de hello máquinas virtuales de Azure están conectados después de producirse la conmutación por error de Hola.

4. toostart Hola conmutación por error, haga clic en **Aceptar**. tootrack de progreso, haga clic en hello VM tooopen sus propiedades. O puede hacer clic en hello **conmutación por error de prueba** trabajo en el nombre del almacén de hello > **configuración** > **trabajos** > **detrabajosderecuperacióndesitio**.

5. Después de hello conmutación por error finaliza, réplica de hello máquina de Azure aparece en hello portal de Azure > **máquinas virtuales**. Asegúrese de que ese hello VM es el tamaño adecuado de hello, que ha conectado toohello de red adecuada y que se está ejecutando.

6. Hola toodelete las máquinas virtuales que se crearon durante la conmutación por error de prueba hello, haga clic en **conmutación por error de prueba de limpieza** en hello replicar Hola o elemento de plan de recuperación. En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. 

[Más información](site-recovery-test-failover-to-azure.md) sobre las conmutaciones por error de prueba.


## <a name="next-steps"></a>Pasos siguientes

Después de probar la implementación de hello:

- [Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.
- Obtenga más información sobre [con planes de recuperación](site-recovery-create-recovery-plans.md) tooreduce RTO.
