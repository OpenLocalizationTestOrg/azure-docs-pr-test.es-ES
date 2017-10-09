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
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="0aec2-103">Actualizar un almacén de servicios de recuperación basados en el Administrador de recursos de Azure Site Recovery tooan de almacén</span><span class="sxs-lookup"><span data-stu-id="0aec2-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="0aec2-104">Este artículo describe cómo los almacenes de Azure Site Recovery tooupgrade credenciales tooAzure basado en el Administrador de recursos del servicio de recuperación almacenes sin que ello afecte de replicación en curso.</span><span class="sxs-lookup"><span data-stu-id="0aec2-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="0aec2-105">Para más información sobre las características y las ventajas de Azure Resource Manager, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0aec2-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="0aec2-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="0aec2-106">Introduction</span></span>
<span data-ttu-id="0aec2-107">Un almacén de servicios de recuperación es un recurso de Azure Resource Manager para administrar la copia de seguridad y recuperación ante desastres forma nativa en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="0aec2-108">Es un almacén unificado que puede usar en el nuevo portal de Azure hello y sustituye a la copia de seguridad clásico de Hola y almacenes de credenciales de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0aec2-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="0aec2-109">Los almacenes de Recovery Services ofrecen diversas características, como son:</span><span class="sxs-lookup"><span data-stu-id="0aec2-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="0aec2-110">Soporte técnico de Azure Resource Manager: puede proteger las máquinas virtuales y las máquinas físicas en la pila de Azure Resource Manager y realizar una conmutación por error de ellas.</span><span class="sxs-lookup"><span data-stu-id="0aec2-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="0aec2-111">Excluir el disco: si tiene archivos temporales o datos de renovación de código elevada que no desea toouse todo el ancho de banda para, puede excluir volúmenes de replicación.</span><span class="sxs-lookup"><span data-stu-id="0aec2-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="0aec2-112">Esta funcionalidad se ha habilitado actualmente en *VMware tooAzure* y *tooAzure de Hyper-V* y se extiende tooother escenarios así.</span><span class="sxs-lookup"><span data-stu-id="0aec2-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="0aec2-113">Compatibilidad con premium y almacenamiento con redundancia local: ahora puede proteger los servidores en el almacenamiento premium cuentas que permiten que los clientes tooprotect aplicaciones con mayor entrada/salida operaciones por segundo (IOPS).</span><span class="sxs-lookup"><span data-stu-id="0aec2-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="0aec2-114">Esta funcionalidad está habilitada actualmente en *tooAzure VMware*.</span><span class="sxs-lookup"><span data-stu-id="0aec2-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="0aec2-115">Una mejor experiencia de iniciación: Hola mejorado Introducción a experiencia se ha diseñado toomake recuperación ante desastres el programa de instalación sencilla.</span><span class="sxs-lookup"><span data-stu-id="0aec2-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="0aec2-116">Copia de seguridad y administración de la recuperación del sitio de Hola mismo almacén: ahora puede proteger los servidores de recuperación ante desastres o realizar copia de seguridad de hello mismo almacén, que puede reducir la sobrecarga notablemente su administración.</span><span class="sxs-lookup"><span data-stu-id="0aec2-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="0aec2-117">Para obtener más información acerca de la experiencia de hello actualizado y características, vea hello [blog de almacenamiento, copia de seguridad y recuperación](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="0aec2-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="0aec2-118">Características más destacadas</span><span class="sxs-lookup"><span data-stu-id="0aec2-118">Salient features</span></span>

* <span data-ttu-id="0aec2-119">Ningún impacto en la replicación en curso: las replicaciones en curso continúan sin ninguna interrupción durante la actualización y después.</span><span class="sxs-lookup"><span data-stu-id="0aec2-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="0aec2-120">Sin costo adicional: obtenga un conjunto completo de funcionalidades actualizadas sin costo adicional alguno.</span><span class="sxs-lookup"><span data-stu-id="0aec2-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="0aec2-121">Sin pérdida de datos: dado que este proceso es una actualización y no una migración, puntos de recuperación existentes de replicación y la configuración permanece intacta durante y después de la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="0aec2-122">¿Qué ocurre durante la actualización del almacén de hello?</span><span class="sxs-lookup"><span data-stu-id="0aec2-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="0aec2-123">Durante la actualización de hello, no puede realizar operaciones tales como registrar un nuevo servidor o habilitar la replicación para una máquina virtual (VM).</span><span class="sxs-lookup"><span data-stu-id="0aec2-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="0aec2-124">Las operaciones que implican datos de lectura o escritura toohello el almacén de datos, como la replicación continua de los elementos protegidos toohello almacén, continúan sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="0aec2-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="0aec2-125">Tooautomation de cambios y herramientas después de la actualización de Hola</span><span class="sxs-lookup"><span data-stu-id="0aec2-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="0aec2-126">A medida que actualizar Hola almacén tipo de modelo de implementación de administrador de recursos de toohello modelo de implementación clásica de hello, actualizan automatización existente de Hola o tooensure de herramientas que sigue toowork después de la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="0aec2-127">Preparar el entorno para la actualización de Hola</span><span class="sxs-lookup"><span data-stu-id="0aec2-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="0aec2-128">Instale PowerShell o actualizarla tooversion 5 o posterior</span><span class="sxs-lookup"><span data-stu-id="0aec2-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="0aec2-129">Instalar la versión más reciente de Hola de MSI de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="0aec2-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="0aec2-130">Descargar el script de actualización del almacén de servicios de recuperación de Hola</span><span class="sxs-lookup"><span data-stu-id="0aec2-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="0aec2-131">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0aec2-131">Prerequisites</span></span>
<span data-ttu-id="0aec2-132">tooupgrade de Site Recovery tooAzure basado en el Administrador de recursos del servicio de recuperación almacenes de almacenes de credenciales, debe cumplir Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="0aec2-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="0aec2-133">Versión mínima de agente: versión de Hola de proveedor de Azure Site Recovery instalado en el servidor debe ser 5.1.1700.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0aec2-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="0aec2-134">Configuración admitida: no se puede configurar el almacén con la red de área de almacenamiento (SAN) o grupos de disponibilidad AlwaysOn de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0aec2-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="0aec2-135">Se admiten todas las demás configuraciones.</span><span class="sxs-lookup"><span data-stu-id="0aec2-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="0aec2-136">Después de la actualización de hello, puede administrar la asignación de almacenamiento sólo a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0aec2-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="0aec2-137">Escenario de implementación compatible: el almacén no debería tener hello *tooAzure VMware* modelo de implementación heredada.</span><span class="sxs-lookup"><span data-stu-id="0aec2-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="0aec2-138">Antes de continuar, mueva primero el modelo de implementación mejorada de toohello.</span><span class="sxs-lookup"><span data-stu-id="0aec2-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="0aec2-139">No hay trabajos activos iniciada por el usuario que implican management plano operaciones: porque plano de administración de toohello de acceso está restringido durante la actualización, complete las acciones de plano de administración antes de desencadenar la actualización Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="0aec2-140">Este proceso no incluye la replicación en curso.</span><span class="sxs-lookup"><span data-stu-id="0aec2-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="0aec2-141">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="0aec2-141">Frequently asked questions</span></span>

<span data-ttu-id="0aec2-142">**¿Esta actualización afecta a la replicación en curso?**</span><span class="sxs-lookup"><span data-stu-id="0aec2-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="0aec2-143">No.</span><span class="sxs-lookup"><span data-stu-id="0aec2-143">No.</span></span> <span data-ttu-id="0aec2-144">La replicación en curso continúa sin interrupciones durante y después de la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="0aec2-145">**¿Qué ocurre toonetwork configuración como la configuración de IP y VPN de sitio a sitio?**</span><span class="sxs-lookup"><span data-stu-id="0aec2-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="0aec2-146">actualización de Hello no afecta a la configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="0aec2-147">Todas las conexiones de Azure a local permanecen intactas.</span><span class="sxs-lookup"><span data-stu-id="0aec2-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="0aec2-148">**Toomy almacenes ¿qué ocurre si no tengo intención de tooupgrade Hola futuro próximo?**</span><span class="sxs-lookup"><span data-stu-id="0aec2-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="0aec2-149">Soporte técnico para el almacén de Site Recovery en el portal de Azure anterior Hola dejará de utilizarse a partir de septiembre de 2017.</span><span class="sxs-lookup"><span data-stu-id="0aec2-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="0aec2-150">Se recomienda encarecidamente que utilice toomove toohello nuevo portal de hello característica de actualización.</span><span class="sxs-lookup"><span data-stu-id="0aec2-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="0aec2-151">**¿Qué supone este plan de migración para las herramientas existentes?**</span><span class="sxs-lookup"><span data-stu-id="0aec2-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="0aec2-152">Actualización del modelo de implementación del Administrador de recursos de toohello de herramientas es uno de los cambios más importantes de Hola que debe tener en cuenta para en los planes de actualización.</span><span class="sxs-lookup"><span data-stu-id="0aec2-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="0aec2-153">almacenes de servicios de recuperación de Hola se basan en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="0aec2-154">**¿Durante cuánto tiempo Hola tiempo de inactividad de plano de administración última?**</span><span class="sxs-lookup"><span data-stu-id="0aec2-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="0aec2-155">actualización de Hello normalmente tarda unos 15 minutos de too30 y pueden tardar tooa máximo de una hora.</span><span class="sxs-lookup"><span data-stu-id="0aec2-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="0aec2-156">**¿Puedo revertir la actualización?**</span><span class="sxs-lookup"><span data-stu-id="0aec2-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="0aec2-157">No.</span><span class="sxs-lookup"><span data-stu-id="0aec2-157">No.</span></span> <span data-ttu-id="0aec2-158">No se admite la reversión después de actualizar correctamente los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="0aec2-159">**¿Validar mi suscripción o toosee de recursos si se pueden actualizar?**</span><span class="sxs-lookup"><span data-stu-id="0aec2-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="0aec2-160">Sí.</span><span class="sxs-lookup"><span data-stu-id="0aec2-160">Yes.</span></span> <span data-ttu-id="0aec2-161">En Hola admitida por la plataforma opción de actualización, Hola primer paso en la actualización de hello es toovalidate que los recursos de hello son capaces de realizar una actualización.</span><span class="sxs-lookup"><span data-stu-id="0aec2-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="0aec2-162">Si se produce un error en la validación de hello, recibirá mensajes de error adecuado o advertencias.</span><span class="sxs-lookup"><span data-stu-id="0aec2-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="0aec2-163">**¿Cómo informar de un problema con la actualización de hello?**</span><span class="sxs-lookup"><span data-stu-id="0aec2-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="0aec2-164">Si experimenta errores durante la actualización de hello, tenga en cuenta Hola Id. de operación que se muestra en el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="0aec2-165">Microsoft Support proactivamente funcionará para resolver el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="0aec2-166">También puede ponerse en contacto con equipo de soporte técnico de hello con su Id. de suscripción, el nombre del almacén y el identificador de operación.</span><span class="sxs-lookup"><span data-stu-id="0aec2-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="0aec2-167">Compatibilidad con funcionará problema de hello tooresolve tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="0aec2-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="0aec2-168">No vuelva a intentar la operación de Hola a menos que esté siguiendo las instrucciones explícitamente toodo es así por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0aec2-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="0aec2-169">Ejecutar script de Hola</span><span class="sxs-lookup"><span data-stu-id="0aec2-169">Run hello script</span></span>

<span data-ttu-id="0aec2-170">En PowerShell, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="0aec2-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="0aec2-171">Id. de suscripción: Hola Id. de suscripción que está asociado con el almacén de Hola que va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="0aec2-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="0aec2-172">Nombre de almacén: el nombre de Hola de almacén de Hola que va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="0aec2-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="0aec2-173">: Hola ubicación de almacén de Hola que va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="0aec2-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="0aec2-174">ResourceType: valor de HyperVRecoveryManagerVault para los almacenes de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0aec2-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="0aec2-175">TargetResourceGroupName: grupo de recursos de hello en la que desea Hola actualizado toobe almacén colocado.</span><span class="sxs-lookup"><span data-stu-id="0aec2-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="0aec2-176">El valor de TargetResourceGroupName puede ser un grupo de recursos existente de Azure Resource Manager u otro nuevo.</span><span class="sxs-lookup"><span data-stu-id="0aec2-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="0aec2-177">Si hello TargetResourceGroupName proporcionado no existe, se crea como parte de la actualización de hello en hello misma ubicación que el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="0aec2-178">Para obtener más información, vea "Grupos de recursos" Hola sección [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="0aec2-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="0aec2-179">Nombres de grupo de recursos es restricciones de toocertain de asunto.</span><span class="sxs-lookup"><span data-stu-id="0aec2-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="0aec2-180">almacén de tooprevent actualizar error, seguro hello tooobserve convención de nomenclatura con cuidado.</span><span class="sxs-lookup"><span data-stu-id="0aec2-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="0aec2-181">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0aec2-181">For example:</span></span>
    >
    ><span data-ttu-id="0aec2-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="0aec2-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="0aec2-183">Como alternativa, puede ejecutar Hola siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="0aec2-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="0aec2-184">Especifique valores de hello para parámetros de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="0aec2-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="0aec2-185">Hola script de PowerShell le pide tooenter sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="0aec2-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="0aec2-186">Escríbalas dos veces, una vez para la cuenta de modelo de implementación clásica de Hola y otra para hello cuenta de administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0aec2-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="0aec2-187">Después de haber especificado las credenciales, script de Hola ejecuta una comprobación toodetermine si su Hola de cumple el programa de instalación de infraestructura mencionó anteriormente en requisitos.</span><span class="sxs-lookup"><span data-stu-id="0aec2-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="0aec2-188">Después de que se han comprobado y confirmado los requisitos previos de hello, son tooproceed solicitada con actualización del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="0aec2-189">inicia el proceso de actualización de Hello actualizar el almacén.</span><span class="sxs-lookup"><span data-stu-id="0aec2-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="0aec2-190">actualización completa de Hello puede tardar 15 too30 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0aec2-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="0aec2-191">Después de la actualización de Hola se ha completado correctamente, puede tener acceso a almacén actualizado de hello en el nuevo portal de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="0aec2-192">Administración del almacén posterior a la actualización</span><span class="sxs-lookup"><span data-stu-id="0aec2-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="0aec2-193">Replicar mediante Azure Site Recovery en hello que del almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="0aec2-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="0aec2-194">Ahora puede proteger las máquinas virtuales de Azure desde una región tooanother.</span><span class="sxs-lookup"><span data-stu-id="0aec2-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="0aec2-195">Para más información, consulte [Replicación de máquinas virtuales de Azure entre regiones con Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0aec2-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="0aec2-196">Para obtener más información acerca de la replicación de máquinas virtuales VMware tooAzure, consulte [tooAzure replicar máquinas virtuales de VMware con Site Recovery](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0aec2-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="0aec2-197">Para obtener más información acerca de la replicación de máquinas virtuales de Hyper-V (sin WMM) tooAzure, consulte [Hyper-V replicar máquinas virtuales (sin WMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0aec2-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="0aec2-198">Para obtener más información acerca de la replicación de máquinas virtuales de Hyper-V (con VMM) tooAzure, consulte [Hola de máquinas virtuales de Hyper-V replicar en tooAzure de nubes VMM mediante la recuperación de sitio de portal de Azure](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0aec2-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="0aec2-199">Para obtener más información acerca de la replicación de sitio secundario de tooa Hyper-VMs (con VMM), consulte [máquinas virtuales de Hyper-V replicar en VMM nubes tooa secundaria VMM sitio usando Hola portal de Azure](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="0aec2-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="0aec2-200">Para obtener más información acerca de la replicación de sitio secundario de tooa de máquinas virtuales VMware, consulte [Replicate local máquinas virtuales de VMware o un sitio secundario de tooa servidores físicos en el portal de Azure clásico hello](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="0aec2-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="0aec2-201">Visualización de los elementos replicados</span><span class="sxs-lookup"><span data-stu-id="0aec2-201">View your replicated items</span></span>

<span data-ttu-id="0aec2-202">Hello siguiente imagen muestra página de panel de almacén de servicios de recuperación de Hola que muestra las entidades de clave para el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aec2-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="0aec2-203">Seleccione tooview una lista de las entidades protegidas en el almacén de hello, **Site Recovery** > **replican elementos**.</span><span class="sxs-lookup"><span data-stu-id="0aec2-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![Elementos replicados](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="0aec2-205">Hello siguiente imagen muestra el flujo de trabajo de Hola para ver los elementos replicados y hello **conmutación por error** comando para iniciar una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="0aec2-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![Elementos replicados](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="0aec2-207">Visualización de la configuración de replicación</span><span class="sxs-lookup"><span data-stu-id="0aec2-207">View your replication settings</span></span>

<span data-ttu-id="0aec2-208">En el almacén de Site Recovery hello, cada grupo de protección se configura con la frecuencia de copia, retención de punto de recuperación, la frecuencia de las instantáneas coherentes de aplicación y otras opciones de replicación.</span><span class="sxs-lookup"><span data-stu-id="0aec2-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="0aec2-209">En el almacén de servicios de recuperación de hello, estas opciones se configuran como una directiva de replicación.</span><span class="sxs-lookup"><span data-stu-id="0aec2-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="0aec2-210">nombre de Hola de directiva de hello es el nombre de Hola de grupo de protección de Hola o hello *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="0aec2-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="0aec2-211">Para obtener más información acerca de la directiva de replicación, vea [administrar la directiva de replicación para VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="0aec2-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>
