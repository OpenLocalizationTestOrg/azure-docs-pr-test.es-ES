---
title: "aaaUpgrade un almacén de servicios de recuperación de Azure Site Recovery tooan de almacén"
description: "Obtenga información acerca de cómo tooupgrade un almacén de Azure Site Recovery tooa servicios de recuperación del almacén"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a>Actualizar un almacén de servicios de recuperación basados en el Administrador de recursos de Azure Site Recovery tooan de almacén

Este artículo describe cómo los almacenes de Azure Site Recovery tooupgrade credenciales tooAzure basado en el Administrador de recursos del servicio de recuperación almacenes sin que ello afecte de replicación en curso. Para más información sobre las características y las ventajas de Azure Resource Manager, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="introduction"></a>Introducción
Un almacén de servicios de recuperación es un recurso de Azure Resource Manager para administrar la copia de seguridad y recuperación ante desastres forma nativa en la nube de Hola. Es un almacén unificado que puede usar en el nuevo portal de Azure hello y sustituye a la copia de seguridad clásico de Hola y almacenes de credenciales de Site Recovery.

Los almacenes de Recovery Services ofrecen diversas características, como son:

* Soporte técnico de Azure Resource Manager: puede proteger las máquinas virtuales y las máquinas físicas en la pila de Azure Resource Manager y realizar una conmutación por error de ellas.

* Excluir el disco: si tiene archivos temporales o datos de renovación de código elevada que no desea toouse todo el ancho de banda para, puede excluir volúmenes de replicación. Esta funcionalidad se ha habilitado actualmente en *VMware tooAzure* y *tooAzure de Hyper-V* y se extiende tooother escenarios así.

* Compatibilidad con premium y almacenamiento con redundancia local: ahora puede proteger los servidores en el almacenamiento premium cuentas que permiten que los clientes tooprotect aplicaciones con mayor entrada/salida operaciones por segundo (IOPS). Esta funcionalidad está habilitada actualmente en *tooAzure VMware*.

* Una mejor experiencia de iniciación: Hola mejorado Introducción a experiencia se ha diseñado toomake recuperación ante desastres el programa de instalación sencilla.

* Copia de seguridad y administración de la recuperación del sitio de Hola mismo almacén: ahora puede proteger los servidores de recuperación ante desastres o realizar copia de seguridad de hello mismo almacén, que puede reducir la sobrecarga notablemente su administración.

Para obtener más información acerca de la experiencia de hello actualizado y características, vea hello [blog de almacenamiento, copia de seguridad y recuperación](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).

## <a name="salient-features"></a>Características más destacadas

* Ningún impacto en la replicación en curso: las replicaciones en curso continúan sin ninguna interrupción durante la actualización y después.

* Sin costo adicional: obtenga un conjunto completo de funcionalidades actualizadas sin costo adicional alguno.

* Sin pérdida de datos: dado que este proceso es una actualización y no una migración, puntos de recuperación existentes de replicación y la configuración permanece intacta durante y después de la actualización de Hola.


## <a name="what-happens-during-hello-vault-upgrade"></a>¿Qué ocurre durante la actualización del almacén de hello?

Durante la actualización de hello, no puede realizar operaciones tales como registrar un nuevo servidor o habilitar la replicación para una máquina virtual (VM). Las operaciones que implican datos de lectura o escritura toohello el almacén de datos, como la replicación continua de los elementos protegidos toohello almacén, continúan sin interrupciones.

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a>Tooautomation de cambios y herramientas después de la actualización de Hola
A medida que actualizar Hola almacén tipo de modelo de implementación de administrador de recursos de toohello modelo de implementación clásica de hello, actualizan automatización existente de Hola o tooensure de herramientas que sigue toowork después de la actualización de Hola.

### <a name="prepare-your-environment-for-hello-upgrade"></a>Preparar el entorno para la actualización de Hola

* [Instale PowerShell o actualizarla tooversion 5 o posterior](https://www.microsoft.com/download/details.aspx?id=50395)
* [Instalar la versión más reciente de Hola de MSI de PowerShell de Azure](https://github.com/Azure/azure-powershell/releases)
* [Descargar el script de actualización del almacén de servicios de recuperación de Hola](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a>Requisitos previos
tooupgrade de Site Recovery tooAzure basado en el Administrador de recursos del servicio de recuperación almacenes de almacenes de credenciales, debe cumplir Hola según los requisitos:

* Versión mínima de agente: versión de Hola de proveedor de Azure Site Recovery instalado en el servidor debe ser 5.1.1700.0 o posterior.

* Configuración admitida: no se puede configurar el almacén con la red de área de almacenamiento (SAN) o grupos de disponibilidad AlwaysOn de SQL Server. Se admiten todas las demás configuraciones.

    >[!NOTE]
    >Después de la actualización de hello, puede administrar la asignación de almacenamiento sólo a través de PowerShell.

* Escenario de implementación compatible: el almacén no debería tener hello *tooAzure VMware* modelo de implementación heredada. Antes de continuar, mueva primero el modelo de implementación mejorada de toohello.

* No hay trabajos activos iniciada por el usuario que implican management plano operaciones: porque plano de administración de toohello de acceso está restringido durante la actualización, complete las acciones de plano de administración antes de desencadenar la actualización Hola. Este proceso no incluye la replicación en curso.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**¿Esta actualización afecta a la replicación en curso?**

No. La replicación en curso continúa sin interrupciones durante y después de la actualización de Hola.

**¿Qué ocurre toonetwork configuración como la configuración de IP y VPN de sitio a sitio?**

actualización de Hello no afecta a la configuración de red de Hola. Todas las conexiones de Azure a local permanecen intactas.

**Toomy almacenes ¿qué ocurre si no tengo intención de tooupgrade Hola futuro próximo?**

Soporte técnico para el almacén de Site Recovery en el portal de Azure anterior Hola dejará de utilizarse a partir de septiembre de 2017. Se recomienda encarecidamente que utilice toomove toohello nuevo portal de hello característica de actualización.

**¿Qué supone este plan de migración para las herramientas existentes?**  

Actualización del modelo de implementación del Administrador de recursos de toohello de herramientas es uno de los cambios más importantes de Hola que debe tener en cuenta para en los planes de actualización. almacenes de servicios de recuperación de Hola se basan en el modelo de implementación del Administrador de recursos de Hola. 

**¿Durante cuánto tiempo Hola tiempo de inactividad de plano de administración última?**

actualización de Hello normalmente tarda unos 15 minutos de too30 y pueden tardar tooa máximo de una hora.

**¿Puedo revertir la actualización?**

No. No se admite la reversión después de actualizar correctamente los recursos de Hola.

**¿Validar mi suscripción o toosee de recursos si se pueden actualizar?**

Sí. En Hola admitida por la plataforma opción de actualización, Hola primer paso en la actualización de hello es toovalidate que los recursos de hello son capaces de realizar una actualización. Si se produce un error en la validación de hello, recibirá mensajes de error adecuado o advertencias.

**¿Cómo informar de un problema con la actualización de hello?**

Si experimenta errores durante la actualización de hello, tenga en cuenta Hola Id. de operación que se muestra en el error de Hola. Microsoft Support proactivamente funcionará para resolver el problema de Hola. También puede ponerse en contacto con equipo de soporte técnico de hello con su Id. de suscripción, el nombre del almacén y el identificador de operación. Compatibilidad con funcionará problema de hello tooresolve tan pronto como sea posible. No vuelva a intentar la operación de Hola a menos que esté siguiendo las instrucciones explícitamente toodo es así por Microsoft.

## <a name="run-hello-script"></a>Ejecutar script de Hola

En PowerShell, ejecute el siguiente comando de hello:

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* Id. de suscripción: Hola Id. de suscripción que está asociado con el almacén de Hola que va a actualizar.

* Nombre de almacén: el nombre de Hola de almacén de Hola que va a actualizar.

* : Hola ubicación de almacén de Hola que va a actualizar.

* ResourceType: valor de HyperVRecoveryManagerVault para los almacenes de Site Recovery.

* TargetResourceGroupName: grupo de recursos de hello en la que desea Hola actualizado toobe almacén colocado. El valor de TargetResourceGroupName puede ser un grupo de recursos existente de Azure Resource Manager u otro nuevo. Si hello TargetResourceGroupName proporcionado no existe, se crea como parte de la actualización de hello en hello misma ubicación que el almacén de Hola. Para obtener más información, vea "Grupos de recursos" Hola sección [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).

    >[!NOTE]
    >Nombres de grupo de recursos es restricciones de toocertain de asunto. almacén de tooprevent actualizar error, seguro hello tooobserve convención de nomenclatura con cuidado.
    >
    >Por ejemplo:
    >
    >.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc

Como alternativa, puede ejecutar Hola siguiente secuencia de comandos. Especifique valores de hello para parámetros de hello necesario.

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. Hola script de PowerShell le pide tooenter sus credenciales. Escríbalas dos veces, una vez para la cuenta de modelo de implementación clásica de Hola y otra para hello cuenta de administrador de recursos de Azure.

2. Después de haber especificado las credenciales, script de Hola ejecuta una comprobación toodetermine si su Hola de cumple el programa de instalación de infraestructura mencionó anteriormente en requisitos.

3. Después de que se han comprobado y confirmado los requisitos previos de hello, son tooproceed solicitada con actualización del almacén de Hola. inicia el proceso de actualización de Hello actualizar el almacén. actualización completa de Hello puede tardar 15 too30 minutos toocomplete.

4. Después de la actualización de Hola se ha completado correctamente, puede tener acceso a almacén actualizado de hello en el nuevo portal de Azure Hola.

## <a name="post-upgrade-vault-management"></a>Administración del almacén posterior a la actualización

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a>Replicar mediante Azure Site Recovery en hello que del almacén de servicios de recuperación

* Ahora puede proteger las máquinas virtuales de Azure desde una región tooanother. Para más información, consulte [Replicación de máquinas virtuales de Azure entre regiones con Azure Site Recovery](site-recovery-azure-to-azure.md).

* Para obtener más información acerca de la replicación de máquinas virtuales VMware tooAzure, consulte [tooAzure replicar máquinas virtuales de VMware con Site Recovery](vmware-walkthrough-overview.md).

* Para obtener más información acerca de la replicación de máquinas virtuales de Hyper-V (sin WMM) tooAzure, consulte [Hyper-V replicar máquinas virtuales (sin WMM) tooAzure](hyper-v-site-walkthrough-overview.md).

* Para obtener más información acerca de la replicación de máquinas virtuales de Hyper-V (con VMM) tooAzure, consulte [Hola de máquinas virtuales de Hyper-V replicar en tooAzure de nubes VMM mediante la recuperación de sitio de portal de Azure](vmm-to-azure-walkthrough-overview.md).

* Para obtener más información acerca de la replicación de sitio secundario de tooa Hyper-VMs (con VMM), consulte [máquinas virtuales de Hyper-V replicar en VMM nubes tooa secundaria VMM sitio usando Hola portal de Azure](site-recovery-vmm-to-vmm.md).

* Para obtener más información acerca de la replicación de sitio secundario de tooa de máquinas virtuales VMware, consulte [Replicate local máquinas virtuales de VMware o un sitio secundario de tooa servidores físicos en el portal de Azure clásico hello](site-recovery-vmware-to-vmware.md).

### <a name="view-your-replicated-items"></a>Visualización de los elementos replicados

Hello siguiente imagen muestra página de panel de almacén de servicios de recuperación de Hola que muestra las entidades de clave para el almacén de Hola. Seleccione tooview una lista de las entidades protegidas en el almacén de hello, **Site Recovery** > **replican elementos**.


![Elementos replicados](./media/upgrade-site-recovery-vaults/replicateditems.png)

Hello siguiente imagen muestra el flujo de trabajo de Hola para ver los elementos replicados y hello **conmutación por error** comando para iniciar una conmutación por error.

![Elementos replicados](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a>Visualización de la configuración de replicación

En el almacén de Site Recovery hello, cada grupo de protección se configura con la frecuencia de copia, retención de punto de recuperación, la frecuencia de las instantáneas coherentes de aplicación y otras opciones de replicación. En el almacén de servicios de recuperación de hello, estas opciones se configuran como una directiva de replicación. nombre de Hola de directiva de hello es el nombre de Hola de grupo de protección de Hola o hello *primarycloud_Policy*.

Para obtener más información acerca de la directiva de replicación, vea [administrar la directiva de replicación para VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).
