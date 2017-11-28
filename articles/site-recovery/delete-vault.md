---
title: "Eliminación del almacén de Site Recovery"
description: "Aprenda a eliminar un almacén de Azure Site Recovery, en función del escenario de Site Recovery."
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
ms.openlocfilehash: b95b9defa0a037f7d7d3ef36b99bc7c53c751050
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="0f291-103">Eliminación del almacén de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0f291-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="0f291-104">Las dependencias pueden evitar la eliminación de un almacén de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0f291-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="0f291-105">Las acciones que debe llevar a cabo varían según el escenario de Site Recovery: VMware a Azure, Hyper-V (con y sin System Center Virtual Machine Manager) a Azure y Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="0f291-105">The actions you need to take vary based on the Site Recovery scenario: VMware to Azure, Hyper-V (with and without System Center Virtual Machine Manager) to Azure, and Azure Backup.</span></span> <span data-ttu-id="0f291-106">Para eliminar un almacén de Azure Backup, consulte el artículo sobre la [eliminación de un almacén de Azure Backup](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="0f291-106">To delete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="0f291-107">Si va a probar el producto y no le importa perder datos, puede usar el método de eliminación forzada para eliminar el almacén y todas sus dependencias rápidamente.</span><span class="sxs-lookup"><span data-stu-id="0f291-107">If you're testing the product and aren't concerned about data loss, use the force delete method to rapidly remove the vault and all its dependencies.</span></span>

> <span data-ttu-id="0f291-108">El comando de PowerShell eliminará todo el contenido del almacén y la acción es irreversible.</span><span class="sxs-lookup"><span data-stu-id="0f291-108">The PowerShell command deletes all the contents of the vault and is not reversible.</span></span>

## <a name="use-powershell-to-force-delete-the-vault"></a><span data-ttu-id="0f291-109">Uso de PowerShell para forzar la eliminación del almacén</span><span class="sxs-lookup"><span data-stu-id="0f291-109">Use PowerShell to force delete the vault</span></span> 

<span data-ttu-id="0f291-110">Para eliminar el almacén de Site Recovery aunque haya elementos protegidos, use estos comandos:</span><span class="sxs-lookup"><span data-stu-id="0f291-110">To delete the Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="0f291-111">Eliminación del almacén de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0f291-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="0f291-112">Para eliminar el almacén, siga los pasos recomendados para su escenario.</span><span class="sxs-lookup"><span data-stu-id="0f291-112">To delete the vault, follow the recommended steps for your scenario.</span></span>

### <a name="vmware-vms-to-azure"></a><span data-ttu-id="0f291-113">Máquinas virtuales de VMware en Azure</span><span class="sxs-lookup"><span data-stu-id="0f291-113">VMware VMs to Azure</span></span>

1. <span data-ttu-id="0f291-114">Siga los pasos descritos en el artículo sobre la [deshabilitación de la protección para VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server) para eliminar todas las máquinas virtuales protegidas.</span><span class="sxs-lookup"><span data-stu-id="0f291-114">Delete all protected VMs by following the steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="0f291-115">Siga los pasos descritos en [Eliminación de una directiva de aplicación](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy) para eliminar todas las directivas de replicación.</span><span class="sxs-lookup"><span data-stu-id="0f291-115">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="0f291-116">Siga los pasos descritos en el artículo de [eliminación de vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery) para eliminar las referencias a vCenter.</span><span class="sxs-lookup"><span data-stu-id="0f291-116">Delete references to vCenter by following the steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="0f291-117">Siga los pasos descritos en el artículo de [retirada de un servidor de configuración](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server) para eliminar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0f291-117">Delete the configuration server by following the steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="0f291-118">Elimine el almacén.</span><span class="sxs-lookup"><span data-stu-id="0f291-118">Delete the vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-to-azure"></a><span data-ttu-id="0f291-119">Máquinas virtuales de Hyper-V (con Virtual Machine Manager) a Azure</span><span class="sxs-lookup"><span data-stu-id="0f291-119">Hyper-V VMs (with Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="0f291-120">Eliminar todas las máquinas virtuales protegidas siguiendo los pasos descritos en [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server) (Deshabilitar la protección de un servidor físico o una máquina virtual de VMware).</span><span class="sxs-lookup"><span data-stu-id="0f291-120">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="0f291-121">Siga los pasos descritos en [Eliminación de una directiva de aplicación](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy) para eliminar todas las directivas de replicación.</span><span class="sxs-lookup"><span data-stu-id="0f291-121">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="0f291-122">Siga los pasos del artículo sobre la [anulación del registro de un servidor VMM conectado](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server) para eliminar las referencias a los servidores Virtual Machine Manager.</span><span class="sxs-lookup"><span data-stu-id="0f291-122">Delete references to Virtual Machine Manager servers by following the steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="0f291-123">Elimine el almacén.</span><span class="sxs-lookup"><span data-stu-id="0f291-123">Delete the vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-to-azure"></a><span data-ttu-id="0f291-124">Máquinas virtuales de Hyper-V (sin Virtual Machine Manager) a Azure</span><span class="sxs-lookup"><span data-stu-id="0f291-124">Hyper-V VMs (without Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="0f291-125">Eliminar todas las máquinas virtuales protegidas siguiendo los pasos descritos en [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server) (Deshabilitar la protección de un servidor físico o una máquina virtual de VMware).</span><span class="sxs-lookup"><span data-stu-id="0f291-125">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="0f291-126">Siga los pasos descritos en [Eliminación de una directiva de aplicación](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy) para eliminar todas las directivas de replicación.</span><span class="sxs-lookup"><span data-stu-id="0f291-126">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="0f291-127">Siga los pasos del artículo sobre la [anulación del registro de un host de Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site) para eliminar las referencias a los servidores Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0f291-127">Delete references to Hyper-V servers by following the steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="0f291-128">Elimine el sitio de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0f291-128">Delete the Hyper-V site.</span></span>

5. <span data-ttu-id="0f291-129">Elimine el almacén.</span><span class="sxs-lookup"><span data-stu-id="0f291-129">Delete the vault.</span></span>
