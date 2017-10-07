---
title: "aaaBefore iniciar la replicación de máquinas virtuales de Azure tooanother región | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tootake antes de la replicación de máquinas virtuales de Azure entre regiones de Azure, mediante el servicio de Azure Site Recovery Hola"
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
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a>Paso 2: antes de comenzar

Una vez que haya revisado hello [arquitectura](azure-to-azure-walkthrough-architecture.md) para la replicación de máquinas virtuales (VM) Azure entre regiones de Azure con [Azure Site Recovery](site-recovery-overview.md), use este los requisitos previos de artículo tooverify. 

- Cuando termine de artículo hello, debe tener una clara comprensión de lo que necesita la implementación de hello toomake de trabajo y ha completado los pasos de requisitos previos de Hola.
- Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>
> La replicación de VM de Azure se encuentra en una versión preliminar en este momento.



## <a name="support-recommendations"></a>Recomendaciones de compatibilidad

Tabla de hello revisión siguiente.

**Componente** | **Requisito**
--- | ---
**Almacén de Recovery Services** | Le recomendamos que cree un almacén de servicios de recuperación de destino de hello región de Azure que quiere toouse de recuperación ante desastres. Por ejemplo, si desea que las máquinas virtuales de origen de tooreplicate en UU tooCentral EE. UU., crear almacén Hola zona horaria del Pacífico Central.
**Suscripción de Azure** | Su suscripción de Azure debe ser habilitado toocreate las máquinas virtuales, en ubicación de destino de Hola que desea toouse como región de recuperación ante desastres de Hola. Póngase en contacto con soporte técnico tooenable Hola necesario cuota.
**Capacidad de la región de destino** | En la región de Azure de destino de hello, suscripción Hola debe tener suficiente capacidad para las máquinas virtuales, cuentas de almacenamiento y componentes de red.
**Almacenamiento** | Hola de uso [instrucciones sobre el almacenamiento](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) para el origen de máquinas virtuales de Azure, tooavoid los problemas de rendimiento.<br/><br/> Las cuentas de almacenamiento deben estar en hello misma región que el almacén de Hola.<br/><br/> No se puede replicar toopremium cuentas en el centro y sur de India.<br/><br/> Si implementa la replicación con la configuración predeterminada de hello, Site Recovery crea cuentas de almacenamiento de hello necesaria en función de la configuración del origen de Hola. Si personaliza la configuración, siga hello [objetivos de escalabilidad de discos de máquina virtual](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Redes** | Necesitará tooallow conectividad saliente desde máquinas virtuales de Azure, para determinados intervalos de direcciones URL de TCP/IP.<br/><br/> Cuentas de red deben estar en hello misma región que el almacén de Hola. 
**MV de Azure** | Asegúrese de que todos los certificados raíz de la últimos Hola se encuentran en hello VM de Azure de Windows o Linux. Si no lo está, no será hello tooregister capaz de máquina virtual en recuperación del sitio, debido a las restricciones de seguridad.
**Cuenta de usuario de Azure** | Su cuenta de usuario de Azure necesita toohave determinados [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una máquina virtual de Azure.

Obtener una lista completa de requisitos de compatibilidad de hello [matriz de compatibilidad](site-recovery-support-matrix-azure-to-azure.md)


## <a name="set-permissions-on-hello-account"></a>Establecer permisos en la cuenta de hello

1. Obtenga información sobre hello [permisos](site-recovery-role-based-linked-access-control.md) necesario para la replicación.
2. Siga estas [instrucciones](../active-directory/role-based-access-control-configure.md#add-access) tooadd permisos.


## <a name="verify-target-resources"></a>Comprobación de los recursos de destino

1. Habilitar la tooallow de suscripción de Azure VM toocreate Hola destino región desea toouse para la recuperación ante desastres que desea toouse como región de recuperación ante desastres de Hola. Póngase en contacto con soporte técnico tooenable Hola necesario cuota.
2. Asegúrese de que su suscripción tiene suficientes recursos tooenable máquinas virtuales con tamaños que coinciden con el origen de las máquinas virtuales. De forma predeterminada, al configurar la replicación, Site Recovery recoge Hola mismo tamaño para hello VM de destino u Hola tamaño posible más cercano. Obtenga información sobre [cómo solucionar problemas](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) en los recursos de destino.

## <a name="verify-azure-vm-certificates"></a>Comprobación de los certificados de la máquina virtual de Azure

1. Compruebe que todos los certificados raíz de la últimos Hola estén presentes en Windows hello o máquinas virtuales de Linux que desea tooreplicate. Si no hay certificados raíz más recientes de hello, Hola VM no puede ser registrado tooSite recuperación debido a restricciones de toosecurity.
2. Para máquinas virtuales de Windows, Hola siguientes:

    - Instale todas las actualizaciones de Windows más recientes de hello en hello VM para que todos los certificados raíz de confianza de hello estén en la máquina de Hola.
    - En un entorno desconectado, siga Hola estándar Windows Update certificado del proceso o proceso de actualización en su organización, los certificados de raíz más recientes de tooget hello y CRL actualizada, en máquinas virtuales de Hola.
3. Para máquinas virtuales de Linux, siga las instrucciones de hello indicadas por los certificados de raíz de confianza más recientes de Linux distribuidor tooget hello y lista de revocación de certificado más reciente de hello en hello máquina virtual. Obtenga información sobre [cómo solucionar problemas](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) de los certificados raíz de confianza.


## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 3: planear las redes](azure-to-azure-walkthrough-network.md) tooset la conectividad saliente.
