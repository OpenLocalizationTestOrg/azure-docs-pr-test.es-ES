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
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="8d74e-103">Eliminación del almacén de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8d74e-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="8d74e-104">Las dependencias pueden evitar la eliminación de un almacén de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8d74e-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="8d74e-105">Hello acciones necesita tootake varían en función de un escenario de recuperación de sitio hello: tooAzure de VMware, tooAzure de Hyper-V (con y sin System Center Virtual Machine Manager) y copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d74e-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="8d74e-106">vea toodelete un almacén de copia de seguridad de Azure, de [eliminar un almacén de copia de seguridad en Azure](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="8d74e-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="8d74e-107">Si está probando el producto de hello y no le preocupa la pérdida de datos, use Hola Forzar eliminación método toorapidly quitar el almacén de Hola y todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="8d74e-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="8d74e-108">Hola comando PowerShell elimina todo el contenido del almacén de Hola Hola y no es reversible.</span><span class="sxs-lookup"><span data-stu-id="8d74e-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="8d74e-109">Use PowerShell tooforce eliminar el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="8d74e-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="8d74e-110">Hola toodelete del almacén de Site Recovery incluso si no hay elementos protegidos, utilice estos comandos:</span><span class="sxs-lookup"><span data-stu-id="8d74e-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="8d74e-111">Eliminación del almacén de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8d74e-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="8d74e-112">almacén de hello toodelete, Hola seguir pasos recomendado para su escenario.</span><span class="sxs-lookup"><span data-stu-id="8d74e-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="8d74e-113">Máquinas virtuales de VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="8d74e-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="8d74e-114">Eliminar todos los protegidos máquinas virtuales siguiendo los pasos de hello en [deshabilite la protección de una VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="8d74e-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="8d74e-115">Eliminar todas las directivas de replicación mediante pasos de hello en [eliminar una directiva de replicación](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="8d74e-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="8d74e-116">Eliminar las referencias toovCenter por hello siguiente pasos en [eliminar un vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="8d74e-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="8d74e-117">Eliminar el servidor de configuración de hello siguiendo los pasos de hello en [retirar un servidor de configuración](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="8d74e-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="8d74e-118">Eliminar el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d74e-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="8d74e-119">TooAzure de máquinas virtuales de Hyper-V (con Virtual Machine Manager)</span><span class="sxs-lookup"><span data-stu-id="8d74e-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="8d74e-120">Eliminar todos los protegidos máquinas virtuales siguiendo los pasos de hello en [deshabilite la protección de un servidor físico o VM de VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="8d74e-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="8d74e-121">Eliminar todas las directivas de replicación mediante pasos de hello en [eliminar una directiva de replicación](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="8d74e-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="8d74e-122">Delete hace referencia a servidores de tooVirtual Machine Manager siguiendo los pasos de hello en [anular el registro de un servidor VMM conectado](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="8d74e-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="8d74e-123">Eliminar el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d74e-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="8d74e-124">Máquinas virtuales de Hyper-V (sin el Administrador de máquina Virtual) tooAzure</span><span class="sxs-lookup"><span data-stu-id="8d74e-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="8d74e-125">Eliminar todos los protegidos máquinas virtuales siguiendo los pasos de hello en [deshabilite la protección de un servidor físico o VM de VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="8d74e-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="8d74e-126">Eliminar todas las directivas de replicación mediante pasos de hello en [eliminar una directiva de replicación](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="8d74e-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="8d74e-127">Delete hace referencia a servidores tooHyper-V siguiendo los pasos de hello en [anular el registro de un host de Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="8d74e-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="8d74e-128">Eliminar sitio de Hyper-V de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d74e-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="8d74e-129">Eliminar el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d74e-129">Delete hello vault.</span></span>
