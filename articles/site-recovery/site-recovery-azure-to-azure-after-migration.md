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
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="52bf5-103">Replicar máquinas virtuales de Azure tooanother región después tooAzure de migración mediante el uso de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="52bf5-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="52bf5-104">La replicación de Azure Site Recovery en máquinas virtuales (VM) de Azure está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="52bf5-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="52bf5-105">Información general</span><span class="sxs-lookup"><span data-stu-id="52bf5-105">Overview</span></span>

<span data-ttu-id="52bf5-106">En este artículo le ayudará a preparar las máquinas virtuales de Azure para la replicación entre dos regiones de Azure después de que estos equipos se han migrado desde un tooAzure del entorno local mediante el uso de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="52bf5-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="52bf5-107">Recuperación ante desastres y cumplimiento normativo</span><span class="sxs-lookup"><span data-stu-id="52bf5-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="52bf5-108">En la actualidad, cada vez más empresas están cambiando su tooAzure de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="52bf5-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="52bf5-109">Con las empresas que mover la producción de misión crítica local tooAzure de cargas de trabajo, configurar la recuperación ante desastres para estas cargas de trabajo es obligatorio para toosafeguard contra las interrupciones en una región de Azure y cumplimiento de normas.</span><span class="sxs-lookup"><span data-stu-id="52bf5-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="52bf5-110">Pasos para preparar para la replicación las máquinas migradas</span><span class="sxs-lookup"><span data-stu-id="52bf5-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="52bf5-111">tooprepare migrar máquinas para configurar la replicación tooanother región de Azure:</span><span class="sxs-lookup"><span data-stu-id="52bf5-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="52bf5-112">Complete la migración.</span><span class="sxs-lookup"><span data-stu-id="52bf5-112">Complete migration.</span></span>
2. <span data-ttu-id="52bf5-113">Instalar hello Azure agente si es necesario.</span><span class="sxs-lookup"><span data-stu-id="52bf5-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="52bf5-114">Quitar el servicio de movilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="52bf5-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="52bf5-115">Reinicie Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="52bf5-115">Restart hello VM.</span></span>

<span data-ttu-id="52bf5-116">Estos pasos se describen con más detalle en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="52bf5-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="52bf5-117">Paso 1: Migre cargas de trabajo que se ejecutan en máquinas virtuales de Hyper-V, máquinas virtuales de VMware y toorun de servidores físicos en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="52bf5-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="52bf5-118">tooset replicación de una copia de seguridad y migrar sus local Hyper-V, VMware y tooAzure de las cargas de trabajo físico, seguimiento Hola pasos de hello [máquinas virtuales de IaaS de Azure migrar entre regiones de Azure con Azure Site Recovery](site-recovery-migrate-to-azure.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="52bf5-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="52bf5-119">Tras la migración, no necesita toocommit o eliminar una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="52bf5-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="52bf5-120">En su lugar, seleccione hello **completar la migración** opción para cada máquina que desee toomigrate:</span><span class="sxs-lookup"><span data-stu-id="52bf5-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="52bf5-121">En **replican elementos**, haga clic en hello VM y haga clic en **completar la migración**.</span><span class="sxs-lookup"><span data-stu-id="52bf5-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="52bf5-122">Haga clic en **Aceptar** paso de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="52bf5-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="52bf5-123">Puede realizar el seguimiento del progreso en las propiedades de la máquina virtual de hello mediante la supervisión de trabajos de completar la migración de hello en **trabajos de recuperación del sitio**.</span><span class="sxs-lookup"><span data-stu-id="52bf5-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="52bf5-124">Hola **completar la migración** acción completa el proceso de migración de hello, quita la replicación de la máquina de Hola y detiene la facturación de Site Recovery para la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="52bf5-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![Completar migración](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="52bf5-126">Paso 2: Instalar a agente de VM de Azure de hello en la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="52bf5-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="52bf5-127">Hello Azure [agente de máquina virtual](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) debe instalarse en la máquina virtual de Hola para toowork de extensión de Site Recovery de Hola y toohelp protegerán Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="52bf5-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="52bf5-128">A partir de la versión 9.7.0.0, en máquinas virtuales de Windows, instalador del servicio de movilidad de hello también instala a hello más reciente disponible Azure agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="52bf5-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="52bf5-129">Durante la migración, máquina virtual de hello cumple lo requisitos previos para utilizar cualquier extensión de máquina virtual, incluidos la extensión de Site Recovery Hola de instalación del agente.</span><span class="sxs-lookup"><span data-stu-id="52bf5-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="52bf5-130">Hello Azure VM agent necesidades toobe instalado manualmente solo si el servicio de movilidad instalado en Hola Hola migra máquina es 9,6 o versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="52bf5-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="52bf5-131">Hello tabla siguiente proporciona información adicional sobre la instalación de agente de máquina virtual de Hola y validar que se ha instalado:</span><span class="sxs-lookup"><span data-stu-id="52bf5-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="52bf5-132">**operación**</span><span class="sxs-lookup"><span data-stu-id="52bf5-132">**Operation**</span></span> | <span data-ttu-id="52bf5-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="52bf5-133">**Windows**</span></span> | <span data-ttu-id="52bf5-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="52bf5-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="52bf5-135">Instalar agente de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="52bf5-135">Installing hello VM agent</span></span> |<span data-ttu-id="52bf5-136">Descargue e instale hello [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="52bf5-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="52bf5-137">Necesita la instalación de Hola de toocomplete de privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="52bf5-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="52bf5-138">Instalar más reciente hello [agente Linux](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="52bf5-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="52bf5-139">Necesita la instalación de Hola de toocomplete de privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="52bf5-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="52bf5-140">Se recomienda instalar el agente de Hola desde el repositorio de distribución.</span><span class="sxs-lookup"><span data-stu-id="52bf5-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="52bf5-141">Se *no se recomienda* instalar agente de VM de Linux de hello directamente desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="52bf5-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="52bf5-142">Validar la instalación del agente VM de Hola</span><span class="sxs-lookup"><span data-stu-id="52bf5-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="52bf5-143">1. Examinar toohello C:\WindowsAzure\Packages carpeta Hola VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="52bf5-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="52bf5-144">Debería ver archivo de hello WaAppAgent.exe.</span><span class="sxs-lookup"><span data-stu-id="52bf5-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="52bf5-145">2. Haga clic en archivo hello, vaya demasiado**propiedades**y, a continuación, seleccione hello **detalles** Hola de ficha **versión del producto** campo debe ser 2.6.1198.718 o superior.</span><span class="sxs-lookup"><span data-stu-id="52bf5-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="52bf5-146">N/D</span><span class="sxs-lookup"><span data-stu-id="52bf5-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="52bf5-147">Paso 3: Hola de quitar el servicio de movilidad de hello migra máquina virtual</span><span class="sxs-lookup"><span data-stu-id="52bf5-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="52bf5-148">Si ha migrado los máquinas de VMware locales o servidores físicos en Windows/Linux, debe toomanually quitar o desinstalar Hola Mobility service de hello migró la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="52bf5-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="52bf5-149">Este paso no es necesario para máquinas virtuales de Hyper-V migrado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="52bf5-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="52bf5-150">Desinstalar el servicio de movilidad de hello en una VM de Windows Server</span><span class="sxs-lookup"><span data-stu-id="52bf5-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="52bf5-151">Utilice uno de hello después el servicio de movilidad de métodos toouninstall hello en un equipo con Windows Server.</span><span class="sxs-lookup"><span data-stu-id="52bf5-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="52bf5-152">Desinstalar mediante la interfaz de usuario de Windows hello</span><span class="sxs-lookup"><span data-stu-id="52bf5-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="52bf5-153">En el Panel de Control de hello, seleccione **programas**.</span><span class="sxs-lookup"><span data-stu-id="52bf5-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="52bf5-154">Seleccione **Microsoft Azure Site Recovery Mobility Service/Servidor de destino maestro** y, a continuación, haga clic en**Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="52bf5-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="52bf5-155">Desinstalación en un símbolo del sistema</span><span class="sxs-lookup"><span data-stu-id="52bf5-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="52bf5-156">Abra una ventana de símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="52bf5-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="52bf5-157">servicio de movilidad en hello toouninstall, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="52bf5-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="52bf5-158">Desinstalar el servicio de movilidad de hello en un equipo Linux</span><span class="sxs-lookup"><span data-stu-id="52bf5-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="52bf5-159">En el servidor Linux, inicie sesión como un usuario **raíz**.</span><span class="sxs-lookup"><span data-stu-id="52bf5-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="52bf5-160">En un terminal, vaya demasiado/usuario/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="52bf5-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="52bf5-161">servicio de movilidad en hello toouninstall, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="52bf5-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="52bf5-162">Paso 4: Reinicie Hola VM</span><span class="sxs-lookup"><span data-stu-id="52bf5-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="52bf5-163">Después de desinstalar el servicio de movilidad de hello, reinicio Hola VM antes de configurar la replicación tooanother región de Azure.</span><span class="sxs-lookup"><span data-stu-id="52bf5-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="52bf5-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52bf5-164">Next steps</span></span>
- <span data-ttu-id="52bf5-165">Empiece a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="52bf5-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="52bf5-166">Obtenga más información en las [instrucciones sobre redes para replicar máquinas virtuales de Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="52bf5-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
