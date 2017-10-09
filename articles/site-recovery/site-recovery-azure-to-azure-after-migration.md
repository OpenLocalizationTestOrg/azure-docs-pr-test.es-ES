---
title: "aaaPrepare máquinas tooset la recuperación ante desastres entre regiones de Azure después de tooAzure de migración mediante el uso de Site Recovery | Documentos de Microsoft"
description: "Este artículo describe cómo tooprepare máquinas tooset la recuperación ante desastres entre regiones de Azure después de tooAzure de migración mediante el uso de Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Replicar máquinas virtuales de Azure tooanother región después tooAzure de migración mediante el uso de Azure Site Recovery

>[!NOTE]
> La replicación de Azure Site Recovery en máquinas virtuales (VM) de Azure está actualmente en versión preliminar.

## <a name="overview"></a>Información general

En este artículo le ayudará a preparar las máquinas virtuales de Azure para la replicación entre dos regiones de Azure después de que estos equipos se han migrado desde un tooAzure del entorno local mediante el uso de Azure Site Recovery.

## <a name="disaster-recovery-and-compliance"></a>Recuperación ante desastres y cumplimiento normativo
En la actualidad, cada vez más empresas están cambiando su tooAzure de cargas de trabajo. Con las empresas que mover la producción de misión crítica local tooAzure de cargas de trabajo, configurar la recuperación ante desastres para estas cargas de trabajo es obligatorio para toosafeguard contra las interrupciones en una región de Azure y cumplimiento de normas.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>Pasos para preparar para la replicación las máquinas migradas
tooprepare migrar máquinas para configurar la replicación tooanother región de Azure:

1. Complete la migración.
2. Instalar hello Azure agente si es necesario.
3. Quitar el servicio de movilidad de Hola.  
4. Reinicie Hola máquina virtual.

Estos pasos se describen con más detalle en las secciones siguientes de Hola.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>Paso 1: Migre cargas de trabajo que se ejecutan en máquinas virtuales de Hyper-V, máquinas virtuales de VMware y toorun de servidores físicos en máquinas virtuales de Azure

tooset replicación de una copia de seguridad y migrar sus local Hyper-V, VMware y tooAzure de las cargas de trabajo físico, seguimiento Hola pasos de hello [máquinas virtuales de IaaS de Azure migrar entre regiones de Azure con Azure Site Recovery](site-recovery-migrate-to-azure.md) artículo. 

Tras la migración, no necesita toocommit o eliminar una conmutación por error. En su lugar, seleccione hello **completar la migración** opción para cada máquina que desee toomigrate:
1. En **replican elementos**, haga clic en hello VM y haga clic en **completar la migración**. Haga clic en **Aceptar** paso de hello toocomplete. Puede realizar el seguimiento del progreso en las propiedades de la máquina virtual de hello mediante la supervisión de trabajos de completar la migración de hello en **trabajos de recuperación del sitio**.
2. Hola **completar la migración** acción completa el proceso de migración de hello, quita la replicación de la máquina de Hola y detiene la facturación de Site Recovery para la máquina de Hola.

   ![Completar migración](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>Paso 2: Instalar a agente de VM de Azure de hello en la máquina virtual de Hola
Hello Azure [agente de máquina virtual](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) debe instalarse en la máquina virtual de Hola para toowork de extensión de Site Recovery de Hola y toohelp protegerán Hola máquina virtual.

>[!IMPORTANT]
>A partir de la versión 9.7.0.0, en máquinas virtuales de Windows, instalador del servicio de movilidad de hello también instala a hello más reciente disponible Azure agente de máquina virtual. Durante la migración, máquina virtual de hello cumple lo requisitos previos para utilizar cualquier extensión de máquina virtual, incluidos la extensión de Site Recovery Hola de instalación del agente. Hello Azure VM agent necesidades toobe instalado manualmente solo si el servicio de movilidad instalado en Hola Hola migra máquina es 9,6 o versiones anteriores.

Hello tabla siguiente proporciona información adicional sobre la instalación de agente de máquina virtual de Hola y validar que se ha instalado:

| **operación** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalar agente de máquina virtual de Hola |Descargue e instale hello [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Necesita la instalación de Hola de toocomplete de privilegios de administrador. |Instalar más reciente hello [agente Linux](../virtual-machines/linux/agent-user-guide.md). Necesita la instalación de Hola de toocomplete de privilegios de administrador. Se recomienda instalar el agente de Hola desde el repositorio de distribución. Se *no se recomienda* instalar agente de VM de Linux de hello directamente desde GitHub.  |
| Validar la instalación del agente VM de Hola |1. Examinar toohello C:\WindowsAzure\Packages carpeta Hola VM de Azure. Debería ver archivo de hello WaAppAgent.exe. <br>2. Haga clic en archivo hello, vaya demasiado**propiedades**y, a continuación, seleccione hello **detalles** Hola de ficha **versión del producto** campo debe ser 2.6.1198.718 o superior. |N/D |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>Paso 3: Hola de quitar el servicio de movilidad de hello migra máquina virtual

Si ha migrado los máquinas de VMware locales o servidores físicos en Windows/Linux, debe toomanually quitar o desinstalar Hola Mobility service de hello migró la máquina virtual.

>[!IMPORTANT]
>Este paso no es necesario para máquinas virtuales de Hyper-V migrado tooAzure.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Desinstalar el servicio de movilidad de hello en una VM de Windows Server
Utilice uno de hello después el servicio de movilidad de métodos toouninstall hello en un equipo con Windows Server.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Desinstalar mediante la interfaz de usuario de Windows hello
1. En el Panel de Control de hello, seleccione **programas**.
2. Seleccione **Microsoft Azure Site Recovery Mobility Service/Servidor de destino maestro** y, a continuación, haga clic en**Desinstalar**.

##### <a name="uninstall-at-a-command-prompt"></a>Desinstalación en un símbolo del sistema
1. Abra una ventana de símbolo del sistema como administrador.
2. servicio de movilidad en hello toouninstall, ejecute el siguiente comando de hello:

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Desinstalar el servicio de movilidad de hello en un equipo Linux
1. En el servidor Linux, inicie sesión como un usuario **raíz**.
2. En un terminal, vaya demasiado/usuario/local/ASR.
3. servicio de movilidad en hello toouninstall, ejecute el siguiente comando de hello:

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>Paso 4: Reinicie Hola VM

Después de desinstalar el servicio de movilidad de hello, reinicio Hola VM antes de configurar la replicación tooanother región de Azure.


## <a name="next-steps"></a>Pasos siguientes
- Empiece a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure.md).
- Obtenga más información en las [instrucciones sobre redes para replicar máquinas virtuales de Azure](site-recovery-azure-to-azure-networking-guidance.md).
