---
title: "la replicación para máquinas virtuales de Azure tooanother región de Azure con Azure Site Recovery aaaEnable | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooenable replicación tooanother región de Azure para máquinas virtuales de Azure, mediante el servicio de Azure Site Recovery Hola"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>Paso 5: Habilitación de la replicación para máquinas virtuales de Azure


Después de configurar un [del almacén de servicios de recuperación](azure-to-azure-walkthrough-vault.md), use este artículo tooenable la replicación de máquinas virtuales (VM), región de Azure, tooanother con [Azure Site Recovery](site-recovery-overview.md). replicación de tooenable, se configuran los valores de origen y destino, compruebe la directiva de replicación de Hola y seleccione las máquinas virtuales que desee tooreplicate.

- Cuando termine de artículo hello, las máquinas virtuales de Azure debe replicar toohello región secundaria de Azure.
- Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> La replicación de VM de Azure se encuentra en una versión preliminar en este momento.


## <a name="select-hello-source"></a>Seleccionar origen de Hola 

1. En los almacenes de servicios de recuperación, haga clic en el nombre del almacén de hello > **+ replicar**.
2. En **Origen**, seleccione **Azure - VERSIÓN PRELIMINAR**.
2. En **ubicación de origen**, seleccione origen Hola región de Azure donde se están ejecutando las máquinas virtuales.
3. Seleccione hello **modelo de implementación de máquina virtual de Azure** para las máquinas virtuales: **el Administrador de recursos** o **clásico**.
4. Seleccione hello **grupo de recursos de origen** para máquinas virtuales del Administrador de recursos, o **servicio en la nube** para las VM clásicas.
5. Haga clic en **Aceptar** configuración de toosave Hola.

    ![Configurar origen de Hola](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a>Seleccione hello las máquinas virtuales

Recuperación del sitio recupera una lista de hello que máquinas virtuales asociadas con suscripciones de Hola y servicio de nube/grupo de recursos.

1. En **máquinas virtuales**, seleccione hello las máquinas virtuales que desee tooreplicate.
2. Haga clic en **Aceptar**.

    ![Selección de las máquinas virtuales](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>Definición de la configuración

Recuperación de sitio aprovisiona la configuración predeterminada para la región de destino de hello (basado en la configuración de región de código fuente de hello) y la directiva de replicación de hello:

   - **Ubicación de destino**: región de destino de Hola que desee toouse para recuperación ante desastres. Se recomienda que ubicación de destino de hello coincide con ubicación Hola de almacén de Site Recovery Hola.
   - **Grupo de recursos de destino**: grupo de recursos toowhich máquinas virtuales de Azure en la región de destino de hello pertenecerá después de la conmutación por error. De forma predeterminada, Site Recovery crea un nuevo grupo de recursos en la región de destino de hello con un sufijo "asr". 
   - **Red virtual de destino**: red de hello en las máquinas virtuales de Azure en Hola se ubicarán región de destino después de la conmutación por error. De forma predeterminada, Site Recovery crea una nueva red virtual (y las subredes) en la región de destino de hello con un sufijo "asr". Esta red esté asignada tooyour red de origen. Tenga en cuenta que puede asignar una dirección IP específica después de la conmutación por error de una máquina virtual, si necesita tooretain Hola igual de direcciones IP en las ubicaciones de origen y destino de Hola. 
   - **Almacenar en caché las cuentas de almacenamiento**: recuperación del sitio utiliza una cuenta de almacenamiento en región de origen de Hola. Cambios en máquinas virtuales de origen se envían toothis cuenta, antes de la ubicación de destino de replicación toohello. 
   - **Las cuentas de almacenamiento de destino**: de forma predeterminada, Site Recovery crea una nueva cuenta de almacenamiento en la región de destino de hello, origen de hello toomirror cuenta de almacenamiento de máquina virtual.
   -  **Conjuntos de disponibilidad de destino**: de forma predeterminada, Site Recovery crea un nuevo conjunto de disponibilidad en región de destino de hello, con el sufijo de "asr" Hola. 
   - **Nombre de la directiva de replicación**: Nombre de la directiva.
   - **Retención del punto de recuperación**: De forma predeterminada, Site Recovery conserva los puntos de recuperación durante 24 horas. Puede configurar un valor entre 1 y 72 horas.
   - **Frecuencia de instantáneas coherentes con la aplicación**: De forma predeterminada, Site Recovery toma una instantánea coherente con la aplicación cada 4 horas. Puede configurar cualquier valor entre 1 y 12 horas. Los datos se replican continuamente:
    - Los puntos de recuperación coherentes para el bloqueo mantienen una orden de escritura de datos coherente cuando se crea. Este tipo de punto de recuperación es generalmente es suficiente si la aplicación está diseñada toorecover desde un bloqueo sin incoherencias en los datos
    - Los puntos de recuperación coherentes para el bloqueo se generan cada pocos minutos. Mediante estos toofail de puntos de recuperación a través de y recuperar las máquinas virtuales proporcionan un objetivo de punto de recuperación (RPO) en orden de Hola de minutos.
    - Puntos de recuperación coherente con la aplicación (en coherencia toowrite orden de adición) asegúrese de que las aplicaciones de ejecución completen todas las operaciones y vaciar búferes toodisk (modo de inactividad de aplicación). Se recomienda usar estos puntos de recuperación para aplicaciones de base de datos como SQL Server, Oracle y Exchange.
        
    ![Definición de la configuración](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>Modificar la configuración

Si desea que la configuración de directiva de destino y la replicación toomodify, Hola siguientes:

1. tooview o modificar la configuración de destino, haga clic en **configuración**.
2. configuración de destino de toooverride Hola predeterminado, haga clic en **personalizar**. Puede especificar un grupo de recursos de destino, la red virtual, el conjunto de disponibilidad y la cuenta de almacenamiento de destino. Solo puede agregar conjuntos de disponibilidad si las máquinas virtuales que forman parte de un conjunto en la región de origen de Hola.

    ![Definición de la configuración](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. Haga clic en la configuración de puntos de recuperación y las instantáneas coherentes con la aplicación, replicación toooverride **personalizar** siguiente demasiado**directiva de replicación**.
 
    ![Definición de la configuración](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. Haga clic en recursos de destino de hello aprovisionamiento toostart **crear recursos de destino**. El aprovisionamiento tarda aproximadamente un minuto. No cierre la hoja de Hola durante el aprovisionamiento o tendrá toostart sobre.




## <a name="enable-replication"></a>Habilitar replicación

1. En **Configuración**, haga clic en **Habilitar replicación**. Esto permite la replicación inicial de hello máquinas virtuales que ha seleccionado. Estado de la replicación inicial puede tardar algún tiempo toorefresh. Haga clic en **actualizar** estado más reciente de tooget Hola.

2. Puede seguir el progreso del programa Hola a **habilitar la protección** de trabajo en **configuración** > **trabajos** > **trabajos de recuperación de sitio**.

3. En **configuración** > **replican elementos**, puede ver el estado de Hola de máquinas virtuales y Hola progreso de la replicación inicial. Haga clic en hello VM toodrill hacia abajo en su configuración.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 6: ejecutar una prueba de conmutación por error](azure-to-azure-walkthrough-test-failover.md)
