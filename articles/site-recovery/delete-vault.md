---
title: "aaaDelete un almacén de Site Recovery"
description: "Obtenga información acerca de cómo toodelete un almacén de Azure Site Recovery, en función de un escenario de recuperación de sitio Hola."
service: site-recovery
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
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a>Eliminación del almacén de Site Recovery
Las dependencias pueden evitar la eliminación de un almacén de Azure Site Recovery. Hello acciones necesita tootake varían en función de un escenario de recuperación de sitio hello: tooAzure de VMware, tooAzure de Hyper-V (con y sin System Center Virtual Machine Manager) y copia de seguridad de Azure. vea toodelete un almacén de copia de seguridad de Azure, de [eliminar un almacén de copia de seguridad en Azure](../backup/backup-azure-delete-vault.md).

>[!Important]
>Si está probando el producto de hello y no le preocupa la pérdida de datos, use Hola Forzar eliminación método toorapidly quitar el almacén de Hola y todas sus dependencias.

> Hola comando PowerShell elimina todo el contenido del almacén de Hola Hola y no es reversible.

## <a name="use-powershell-tooforce-delete-hello-vault"></a>Use PowerShell tooforce eliminar el almacén de Hola 

Hola toodelete del almacén de Site Recovery incluso si no hay elementos protegidos, utilice estos comandos:

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Eliminación del almacén de Site Recovery 
almacén de hello toodelete, Hola seguir pasos recomendado para su escenario.

### <a name="vmware-vms-tooazure"></a>Máquinas virtuales de VMware tooAzure

1. Eliminar todos los protegidos máquinas virtuales siguiendo los pasos de hello en [deshabilite la protección de una VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Eliminar todas las directivas de replicación mediante pasos de hello en [eliminar una directiva de replicación](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Eliminar las referencias toovCenter por hello siguiente pasos en [eliminar un vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).

4. Eliminar el servidor de configuración de hello siguiendo los pasos de hello en [retirar un servidor de configuración](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).

5. Eliminar el almacén de Hola.


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>TooAzure de máquinas virtuales de Hyper-V (con Virtual Machine Manager)
1. Eliminar todos los protegidos máquinas virtuales siguiendo los pasos de hello en [deshabilite la protección de un servidor físico o VM de VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Eliminar todas las directivas de replicación mediante pasos de hello en [eliminar una directiva de replicación](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3.  Delete hace referencia a servidores de tooVirtual Machine Manager siguiendo los pasos de hello en [anular el registro de un servidor VMM conectado](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).

4.  Eliminar el almacén de Hola.

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>Máquinas virtuales de Hyper-V (sin el Administrador de máquina Virtual) tooAzure
1. Eliminar todos los protegidos máquinas virtuales siguiendo los pasos de hello en [deshabilite la protección de un servidor físico o VM de VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Eliminar todas las directivas de replicación mediante pasos de hello en [eliminar una directiva de replicación](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Delete hace referencia a servidores tooHyper-V siguiendo los pasos de hello en [anular el registro de un host de Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).

4. Eliminar sitio de Hyper-V de Hola.

5. Eliminar el almacén de Hola.
