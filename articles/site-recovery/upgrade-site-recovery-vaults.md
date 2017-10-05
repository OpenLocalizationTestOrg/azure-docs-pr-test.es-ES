---
title: "Actualización de un almacén de Site Recovery en un almacén de Recovery Services"
description: "Aprenda a actualizar el almacén de Azure Site Recovery en un almacén de Recovery Services"
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
ms.openlocfilehash: fdb33ea0d08353b491f2934fcf885fcb6910b9a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-site-recovery-vault-to-an-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="b31fd-103">Actualización de un almacén de Site Recovery en un almacén de Recovery Services basado en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b31fd-103">Upgrade a Site Recovery vault to an Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="b31fd-104">En este artículo se describe cómo actualizar almacenes de Azure Site Recovery en almacenes de Recovery Service basados en Azure Resource Manager sin que ello influya en la replicación en curso.</span><span class="sxs-lookup"><span data-stu-id="b31fd-104">This article describes how to upgrade Azure Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="b31fd-105">Para más información sobre las características y las ventajas de Azure Resource Manager, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b31fd-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="b31fd-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="b31fd-106">Introduction</span></span>
<span data-ttu-id="b31fd-107">El almacén de Recovery Services es un recurso de Azure Resource Manager para administrar las operaciones de copia de seguridad y recuperación ante desastres de forma nativa en la nube.</span><span class="sxs-lookup"><span data-stu-id="b31fd-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in the cloud.</span></span> <span data-ttu-id="b31fd-108">Se trata de un almacén unificado que puede usarse en la nueva versión de Azure Portal, que reemplaza a los almacenes clásicos de Backup y Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b31fd-108">It is a unified vault that you can use in the new Azure portal, and it replaces the classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="b31fd-109">Los almacenes de Recovery Services ofrecen diversas características, como son:</span><span class="sxs-lookup"><span data-stu-id="b31fd-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="b31fd-110">Soporte técnico de Azure Resource Manager: puede proteger las máquinas virtuales y las máquinas físicas en la pila de Azure Resource Manager y realizar una conmutación por error de ellas.</span><span class="sxs-lookup"><span data-stu-id="b31fd-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="b31fd-111">Excluir el disco: si tiene archivos temporales o datos de renovación elevada que no desea que usen todo el ancho de banda, puede excluir volúmenes de la replicación.</span><span class="sxs-lookup"><span data-stu-id="b31fd-111">Exclude disk: If you have temp files or high churn data that you don’t want to use all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="b31fd-112">Esta funcionalidad se ha habilitado actualmente en *VMware a Azure* y en *Hyper-V a Azure*, y pronto se extenderá también a otros escenarios.</span><span class="sxs-lookup"><span data-stu-id="b31fd-112">This capability has been enabled currently in *VMware to Azure* and *Hyper-V to Azure* and is extended to other scenarios as well.</span></span>

* <span data-ttu-id="b31fd-113">Soporte técnico del almacenamiento con redundancia local (LRS) y Premium Storage: ahora puede proteger los servidores en cuentas de Premium Storage que permiten a los clientes proteger las aplicaciones con más operaciones de E/S por segundo.</span><span class="sxs-lookup"><span data-stu-id="b31fd-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers to protect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="b31fd-114">Esta funcionalidad se ha habilitado actualmente en *VMware a Azure*.</span><span class="sxs-lookup"><span data-stu-id="b31fd-114">This capability is currently enabled in *VMware to Azure*.</span></span>

* <span data-ttu-id="b31fd-115">Experiencia de iniciación simplificada: la experiencia de iniciación mejorada se ha diseñado para facilitar la configuración de la recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="b31fd-115">Streamlined getting-started experience: The enhanced getting-started experience has been designed to make disaster-recovery setup easy.</span></span>

* <span data-ttu-id="b31fd-116">Administración de Backup y Site Recovery desde el mismo almacén: ahora puede proteger los servidores para la recuperación ante desastres o la realización de copias de seguridad desde el mismo almacén, lo que permite reducir significativamente la sobrecarga de administración.</span><span class="sxs-lookup"><span data-stu-id="b31fd-116">Backup and Site Recovery management from the same vault: You can now protect servers for disaster recovery or perform backup from the same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="b31fd-117">Para más información sobre las características y experiencia actualizadas, consulte el [blog de almacenamiento, copia de seguridad y recuperación](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="b31fd-117">For more information about the upgraded experience and features, see the [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="b31fd-118">Características más destacadas</span><span class="sxs-lookup"><span data-stu-id="b31fd-118">Salient features</span></span>

* <span data-ttu-id="b31fd-119">Ningún impacto en la replicación en curso: las replicaciones en curso continúan sin ninguna interrupción durante la actualización y después.</span><span class="sxs-lookup"><span data-stu-id="b31fd-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="b31fd-120">Sin costo adicional: obtenga un conjunto completo de funcionalidades actualizadas sin costo adicional alguno.</span><span class="sxs-lookup"><span data-stu-id="b31fd-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="b31fd-121">Sin pérdida de datos: puesto que este proceso es una actualización y no una migración, la configuración y los puntos de recuperación de la replicación existentes permanecen intactos durante la actualización y después.</span><span class="sxs-lookup"><span data-stu-id="b31fd-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after the upgrade.</span></span>


## <a name="what-happens-during-the-vault-upgrade"></a><span data-ttu-id="b31fd-122">¿Qué ocurre durante la actualización del almacén?</span><span class="sxs-lookup"><span data-stu-id="b31fd-122">What happens during the vault upgrade?</span></span>

<span data-ttu-id="b31fd-123">Durante la actualización, no puede realizar operaciones tales como registrar un nuevo servidor o habilitar la replicación para una máquina virtual (VM).</span><span class="sxs-lookup"><span data-stu-id="b31fd-123">During the upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="b31fd-124">Las operaciones que conlleven la lectura de datos del almacén o la escritura de datos en él, como la replicación en curso de elementos protegidos en el almacén, continúan sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="b31fd-124">Operations that involve reading data from or writing data to the vault, such as ongoing replication of protected items to the vault, continue uninterrupted.</span></span>

### <a name="changes-to-automation-and-tooling-after-the-upgrade"></a><span data-ttu-id="b31fd-125">Cambios en la automatización y herramientas después de la actualización</span><span class="sxs-lookup"><span data-stu-id="b31fd-125">Changes to automation and tooling after the upgrade</span></span>
<span data-ttu-id="b31fd-126">A medida que actualiza el tipo de almacén del modelo de implementación clásica al de Resource Manager, actualice la automatización o las herramientas existentes para asegurarse de que siguen funcionando después de la actualización.</span><span class="sxs-lookup"><span data-stu-id="b31fd-126">As you upgrade the vault type from the classic deployment model to the Resource Manager deployment model, update the existing automation or tooling to ensure that it continues to work after the upgrade.</span></span>

### <a name="prepare-your-environment-for-the-upgrade"></a><span data-ttu-id="b31fd-127">Preparación del entorno para la actualización</span><span class="sxs-lookup"><span data-stu-id="b31fd-127">Prepare your environment for the upgrade</span></span>

* [<span data-ttu-id="b31fd-128">Instale PowerShell o actualícelo a la versión 5 o posterior</span><span class="sxs-lookup"><span data-stu-id="b31fd-128">Install PowerShell or upgrade it to version 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="b31fd-129">Instale la versión más reciente de Azure PowerShell MSI</span><span class="sxs-lookup"><span data-stu-id="b31fd-129">Install the latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="b31fd-130">Descargue el script de actualización del almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b31fd-130">Download the Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="b31fd-131">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b31fd-131">Prerequisites</span></span>
<span data-ttu-id="b31fd-132">Para actualizar los almacenes de Site Recovery en almacenes de Recovery Services basados en Azure Resource Manager, se deben cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="b31fd-132">To upgrade from Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults, you must meet the following requirements:</span></span>

* <span data-ttu-id="b31fd-133">Versión mínima del agente: la versión del proveedor de Azure Site Recovery instalada en el servidor sea la 5.1.1700.0, o una posterior.</span><span class="sxs-lookup"><span data-stu-id="b31fd-133">Minimum agent version: The version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="b31fd-134">Configuración admitida: no se puede configurar el almacén con la red de área de almacenamiento (SAN) o grupos de disponibilidad AlwaysOn de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b31fd-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="b31fd-135">Se admiten todas las demás configuraciones.</span><span class="sxs-lookup"><span data-stu-id="b31fd-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b31fd-136">Después de la actualización, puede administrar la asignación de almacenamiento solo a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b31fd-136">After the upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="b31fd-137">Escenario de implementación admitido: el almacén no debe estar en el modelo de implementación heredada *VMware a Azure*.</span><span class="sxs-lookup"><span data-stu-id="b31fd-137">Supported deployment scenario: Your vault shouldn’t be the *VMware to Azure* legacy deployment model.</span></span> <span data-ttu-id="b31fd-138">Antes de continuar, pase primero al modelo de implementación mejorada.</span><span class="sxs-lookup"><span data-stu-id="b31fd-138">Before you proceed, first move to the enhanced deployment model.</span></span>

* <span data-ttu-id="b31fd-139">Ningún trabajo activo iniciado por el usuario que conlleve operaciones de planeamiento de administración: como el acceso al plan de administración está restringido durante la actualización, complete todas las acciones de planeamiento de la administración antes de activar la actualización.</span><span class="sxs-lookup"><span data-stu-id="b31fd-139">No active user-initiated jobs that involve management plane operations: Because access to the management plane is restricted during upgrade, complete all your management plane actions before you trigger the upgrade.</span></span> <span data-ttu-id="b31fd-140">Este proceso no incluye la replicación en curso.</span><span class="sxs-lookup"><span data-stu-id="b31fd-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="b31fd-141">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="b31fd-141">Frequently asked questions</span></span>

<span data-ttu-id="b31fd-142">**¿Esta actualización afecta a la replicación en curso?**</span><span class="sxs-lookup"><span data-stu-id="b31fd-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="b31fd-143">No.</span><span class="sxs-lookup"><span data-stu-id="b31fd-143">No.</span></span> <span data-ttu-id="b31fd-144">La replicación en curso continúa sin interrupciones durante la actualización y después.</span><span class="sxs-lookup"><span data-stu-id="b31fd-144">Your ongoing replication continues uninterrupted during and after the upgrade.</span></span>

<span data-ttu-id="b31fd-145">**¿Qué ocurre con la configuración de red, como la VPN de sitio a sitio o la configuración de la dirección IP?**</span><span class="sxs-lookup"><span data-stu-id="b31fd-145">**What happens to network settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="b31fd-146">La actualización no afecta a la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="b31fd-146">The upgrade doesn't affect the network settings.</span></span> <span data-ttu-id="b31fd-147">Todas las conexiones de Azure a local permanecen intactas.</span><span class="sxs-lookup"><span data-stu-id="b31fd-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="b31fd-148">**¿Qué ocurre con los almacenes si se prevé realizar una actualización próximamente?**</span><span class="sxs-lookup"><span data-stu-id="b31fd-148">**What happens to my vaults if I don’t plan to upgrade in the near future?**</span></span>

<span data-ttu-id="b31fd-149">El almacén de Site Recovery en la versión anterior de Azure Portal dejará de ser admitido partir de septiembre de 2017.</span><span class="sxs-lookup"><span data-stu-id="b31fd-149">Support for Site Recovery vault in the old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="b31fd-150">Se recomienda encarecidamente que use la característica de actualización para migrar al nuevo portal.</span><span class="sxs-lookup"><span data-stu-id="b31fd-150">We strongly recommend that you use the upgrade feature to move to the new portal.</span></span>

<span data-ttu-id="b31fd-151">**¿Qué supone este plan de migración para las herramientas existentes?**</span><span class="sxs-lookup"><span data-stu-id="b31fd-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="b31fd-152">La actualización de sus herramientas al modelo de implementación de Resource Manager es uno de los cambios más importantes que debe considerar en sus planes de actualización.</span><span class="sxs-lookup"><span data-stu-id="b31fd-152">Updating your tooling to the Resource Manager deployment model is one of the most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="b31fd-153">Los almacenes de Recovery Services se basan en el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b31fd-153">The Recovery Services vaults are based on the Resource Manager deployment model.</span></span> 

<span data-ttu-id="b31fd-154">**¿Cuánto dura el tiempo de inactividad del plan de administración?**</span><span class="sxs-lookup"><span data-stu-id="b31fd-154">**How long does the management-plane downtime last?**</span></span>

<span data-ttu-id="b31fd-155">La actualización normalmente tarda entre 15 y 30 minutos, y puede tardar hasta una hora, como máximo.</span><span class="sxs-lookup"><span data-stu-id="b31fd-155">The upgrade ordinarily takes about 15 to 30 minutes, and it could take up to a maximum of one hour.</span></span>

<span data-ttu-id="b31fd-156">**¿Puedo revertir la actualización?**</span><span class="sxs-lookup"><span data-stu-id="b31fd-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="b31fd-157">No.</span><span class="sxs-lookup"><span data-stu-id="b31fd-157">No.</span></span> <span data-ttu-id="b31fd-158">No se admite la reversión una vez actualizados correctamente los recursos.</span><span class="sxs-lookup"><span data-stu-id="b31fd-158">Rollback is not supported after the resources have been successfully upgraded.</span></span>

<span data-ttu-id="b31fd-159">**¿Puedo validar mi suscripción o mis recursos para comprobar si se pueden actualizar?**</span><span class="sxs-lookup"><span data-stu-id="b31fd-159">**Can I validate my subscription or resources to see whether they can be upgraded?**</span></span>

<span data-ttu-id="b31fd-160">Sí.</span><span class="sxs-lookup"><span data-stu-id="b31fd-160">Yes.</span></span> <span data-ttu-id="b31fd-161">En la opción de actualización compatible con la plataforma, el primer paso para la actualización consiste en validar si los recursos pueden actualizarse.</span><span class="sxs-lookup"><span data-stu-id="b31fd-161">In the platform-supported upgrade option, the first step in the upgrade is to validate that the resources are capable of an upgrade.</span></span> <span data-ttu-id="b31fd-162">Si la validación no puede realizarse, se recibirán las advertencias o mensajes de error apropiados.</span><span class="sxs-lookup"><span data-stu-id="b31fd-162">If the validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="b31fd-163">**¿Cómo informo de un problema con la actualización?**</span><span class="sxs-lookup"><span data-stu-id="b31fd-163">**How do I report an issue with the upgrade?**</span></span>

<span data-ttu-id="b31fd-164">Si experimenta errores durante la actualización, anote el identificador de operación que se muestra en el error.</span><span class="sxs-lookup"><span data-stu-id="b31fd-164">If you experience any failures during the upgrade, note the operation ID that's listed in the error.</span></span> <span data-ttu-id="b31fd-165">El soporte técnico de Microsoft trabajará proactivamente para resolver el problema.</span><span class="sxs-lookup"><span data-stu-id="b31fd-165">Microsoft Support will proactively work on resolving the issue.</span></span> <span data-ttu-id="b31fd-166">También puede ponerse en contacto con el equipo de soporte técnico y proporcionarle el identificador de la suscripción, el nombre del almacén y el identificador de la operación.</span><span class="sxs-lookup"><span data-stu-id="b31fd-166">You can also contact the Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="b31fd-167">Se procurará resolver el problema lo antes posible.</span><span class="sxs-lookup"><span data-stu-id="b31fd-167">Support will work to resolve the issue as quickly as possible.</span></span> <span data-ttu-id="b31fd-168">No vuelva a intentar la operación a menos que Microsoft se lo indique explícitamente.</span><span class="sxs-lookup"><span data-stu-id="b31fd-168">Do not retry the operation unless you are explicitly instructed to do so by Microsoft.</span></span>

## <a name="run-the-script"></a><span data-ttu-id="b31fd-169">Ejecute el script</span><span class="sxs-lookup"><span data-stu-id="b31fd-169">Run the script</span></span>

<span data-ttu-id="b31fd-170">En PowerShell, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b31fd-170">In PowerShell, run the following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="b31fd-171">SubscriptionId: identificador de la suscripción asociado con el almacén que se va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="b31fd-171">SubscriptionID: The subscription ID that's associated with the vault that you're upgrading.</span></span>

* <span data-ttu-id="b31fd-172">VaultName: nombre del almacén que se va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="b31fd-172">VaultName: The name of the vault that you're upgrading.</span></span>

* <span data-ttu-id="b31fd-173">Location: ubicación del almacén que se va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="b31fd-173">Location: The location of the vault that you're upgrading.</span></span>

* <span data-ttu-id="b31fd-174">ResourceType: valor de HyperVRecoveryManagerVault para los almacenes de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b31fd-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="b31fd-175">TargetResourceGroupName: grupo de recursos en el que se desea colocar el almacén actualizado.</span><span class="sxs-lookup"><span data-stu-id="b31fd-175">TargetResourceGroupName: The resource group into which you want the upgraded vault to be placed.</span></span> <span data-ttu-id="b31fd-176">El valor de TargetResourceGroupName puede ser un grupo de recursos existente de Azure Resource Manager u otro nuevo.</span><span class="sxs-lookup"><span data-stu-id="b31fd-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="b31fd-177">En caso de que el valor de TargetResourceGroupName proporcionado no exista, se crea como parte de la actualización en la misma ubicación que el almacén.</span><span class="sxs-lookup"><span data-stu-id="b31fd-177">If the TargetResourceGroupName that's supplied does not exist, it is created as part of the upgrade in the same location as the vault.</span></span> <span data-ttu-id="b31fd-178">Para más información, vea la sección "Grupos de recursos" en [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="b31fd-178">For more information, see the "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="b31fd-179">La denominación de los grupos de recursos está sujeta a determinadas restricciones.</span><span class="sxs-lookup"><span data-stu-id="b31fd-179">Resource group naming is subject to certain constraints.</span></span> <span data-ttu-id="b31fd-180">Para evitar errores durante la actualización del almacén, asegúrese de seguir la convención de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="b31fd-180">To prevent vault upgrade failure, be sure to observe the naming convention carefully.</span></span>
    >
    ><span data-ttu-id="b31fd-181">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b31fd-181">For example:</span></span>
    >
    ><span data-ttu-id="b31fd-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="b31fd-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="b31fd-183">Como alternativa, puede ejecutar el script siguiente.</span><span class="sxs-lookup"><span data-stu-id="b31fd-183">Alternatively, you can run the following script.</span></span> <span data-ttu-id="b31fd-184">Escriba los valores para los parámetros necesarios.</span><span class="sxs-lookup"><span data-stu-id="b31fd-184">Enter the values for the required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for the following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="b31fd-185">El script de PowerShell le pide que escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="b31fd-185">The PowerShell script prompts you to enter your credentials.</span></span> <span data-ttu-id="b31fd-186">Escríbalas dos veces, una para la cuenta del modelo de implementación clásica y otra para la cuenta de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b31fd-186">Enter them twice, once for the classic deployment model account and once for the Azure Resource Manager account.</span></span>

2. <span data-ttu-id="b31fd-187">Después de especificar las credenciales, el script ejecuta una comprobación para determinar si la instalación de la infraestructura cumple los requisitos mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b31fd-187">After you've entered your credentials, the script runs a check to determine whether your infrastructure setup meets the previously mentioned requirements.</span></span>

3. <span data-ttu-id="b31fd-188">Después de comprobar y confirmar los requisitos previos, se le pide que continúe con la actualización del almacén.</span><span class="sxs-lookup"><span data-stu-id="b31fd-188">After the prerequisites have been checked and confirmed, you are prompted to proceed with the vault upgrade.</span></span> <span data-ttu-id="b31fd-189">En el proceso de actualización se empieza a actualizar el almacén.</span><span class="sxs-lookup"><span data-stu-id="b31fd-189">The upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="b31fd-190">La actualización completa puede durar entre 15 y 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="b31fd-190">The entire upgrade can take 15 to 30 minutes to complete.</span></span>

4. <span data-ttu-id="b31fd-191">Cuando la actualización haya finalizado correctamente, puede acceder al almacén actualizado en la nueva versión de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b31fd-191">After the upgrade has been completed successfully, you can access the upgraded vault in the new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="b31fd-192">Administración del almacén posterior a la actualización</span><span class="sxs-lookup"><span data-stu-id="b31fd-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-the-recovery-services-vault"></a><span data-ttu-id="b31fd-193">Replicación mediante Azure Site Recovery en el almacén Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b31fd-193">Replicate by using Azure Site Recovery in the Recovery Services vault</span></span>

* <span data-ttu-id="b31fd-194">Ahora puede proteger las máquinas virtuales de Azure de una región a otra.</span><span class="sxs-lookup"><span data-stu-id="b31fd-194">You can now protect your Azure VMs from one region to another.</span></span> <span data-ttu-id="b31fd-195">Para más información, consulte [Replicación de máquinas virtuales de Azure entre regiones con Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b31fd-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="b31fd-196">Para más información acerca de la replicación de máquinas virtuales VMware en Azure, consulte [Replicación de máquinas virtuales de VMware en Azure con Site Recovery](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b31fd-196">For more information about replicating VMware VMs to Azure, see [Replicate VMware VMs to Azure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="b31fd-197">Para más información acerca de la replicación de máquinas virtuales de Hyper-V (sin WMM) en Azure, consulte [Replicación de máquinas virtuales de Hyper-V (sin WMM) en Azure](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b31fd-197">For more information about replicating Hyper-V VMs (without VMM) to Azure, see [Replicate Hyper-V virtual machines (without VMM) to Azure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="b31fd-198">Para más información acerca de la replicación de máquinas virtuales de Hyper-V (con WMM) en Azure, consulte [Replicación de máquinas virtuales de Hyper-V que están en nubes VMM en Azure mediante Site Recovery en Azure Portal](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b31fd-198">For more information about replicating Hyper-V VMs (with VMM) to Azure, see [Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="b31fd-199">Para más información acerca de la replicación de máquinas virtuales de Hyper-VM (con WMM) en un sitio secundario, consulte [Replicación de máquinas virtuales de Hyper-V que están en nubes VMM en un sitio VMM secundario mediante Azure Portal](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="b31fd-199">For more information about replicating Hyper-VMs (with VMM) to a secondary site, see [Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using the Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="b31fd-200">Para más información sobre la replicación de máquinas virtuales de VMware en un sitio secundario, consulte [Replicación de máquinas virtuales locales de VMware o de servidores físicos en un sitio secundario en el Portal de Azure clásico](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="b31fd-200">For more information about replicating VMware VMs to a secondary site, see [Replicate on-premises VMware virtual machines or physical servers to a secondary site in the classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="b31fd-201">Visualización de los elementos replicados</span><span class="sxs-lookup"><span data-stu-id="b31fd-201">View your replicated items</span></span>

<span data-ttu-id="b31fd-202">La imagen siguiente muestra la página del panel de información del almacén de Recovery Services con las entidades clave del almacén.</span><span class="sxs-lookup"><span data-stu-id="b31fd-202">The following image shows the Recovery Services vault dashboard page that displays key entities for the vault.</span></span> <span data-ttu-id="b31fd-203">Para ver la lista de entidades protegidas en el almacén, haga clic en **Site Recovery** > **Elementos replicados**.</span><span class="sxs-lookup"><span data-stu-id="b31fd-203">To view a list of protected entities in the vault, select **Site Recovery** > **Replicated items**.</span></span>


![Elementos replicados](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="b31fd-205">La siguiente imagen muestra el flujo de trabajo para ver los elementos replicados y el comando **Failover** para iniciar una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="b31fd-205">The following image shows the workflow for viewing your replicated items and the **Failover** command for initiating a failover.</span></span>

![Elementos replicados](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="b31fd-207">Visualización de la configuración de replicación</span><span class="sxs-lookup"><span data-stu-id="b31fd-207">View your replication settings</span></span>

<span data-ttu-id="b31fd-208">En el almacén de Site Recovery, cada grupo de protección se configura con la frecuencia de copia, retención de punto de recuperación, frecuencia de las instantáneas coherentes de la aplicación, y otras opciones de replicación.</span><span class="sxs-lookup"><span data-stu-id="b31fd-208">In the Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="b31fd-209">En el almacén de Recovery Services, estas opciones se configuran como una directiva de replicación.</span><span class="sxs-lookup"><span data-stu-id="b31fd-209">In the Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="b31fd-210">El nombre de la directiva es el del grupo de protección o *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="b31fd-210">The name of the policy is the name of the protection group or the *primarycloud_Policy*.</span></span>

<span data-ttu-id="b31fd-211">Para más información acerca de la directiva de replicación, consulte [Administración de una directiva de replicación de VMware en Azure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="b31fd-211">For more information about replication policy, see [Manage replication policy for VMware to Azure](site-recovery-setup-replication-settings-vmware.md).</span></span>
