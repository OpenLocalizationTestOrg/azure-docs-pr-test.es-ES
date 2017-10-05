---
title: "Preparar máquinas para configurar la recuperación ante desastres entre regiones de Azure después de la migración a Azure mediante Site Recovery | Microsoft Docs"
description: "En este artículo se describe cómo preparar máquinas para configurar la recuperación ante desastres entre regiones de Azure después de la migración a Azure mediante Azure Site Recovery."
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
ms.openlocfilehash: 2aee0fb8d1ba1ff1584bee91b4d1cc34b654d97f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-to-another-region-after-migration-to-azure-by-using-azure-site-recovery"></a><span data-ttu-id="76f24-103">Replicar máquinas virtuales de Azure en otra región después de la migración a Azure mediante Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="76f24-103">Replicate Azure VMs to another region after migration to Azure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="76f24-104">La replicación de Azure Site Recovery en máquinas virtuales (VM) de Azure está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="76f24-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="76f24-105">Información general</span><span class="sxs-lookup"><span data-stu-id="76f24-105">Overview</span></span>

<span data-ttu-id="76f24-106">Este artículo le ayudará a preparar máquinas virtuales de Azure para la replicación entre dos regiones de Azure después de que dichas máquinas se hayan migrado desde un entorno local a Azure mediante Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="76f24-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment to Azure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="76f24-107">Recuperación ante desastres y cumplimiento normativo</span><span class="sxs-lookup"><span data-stu-id="76f24-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="76f24-108">En la actualidad, cada vez más empresas están trasladando sus cargas de trabajo a Azure.</span><span class="sxs-lookup"><span data-stu-id="76f24-108">Today, more and more enterprises are moving their workloads to Azure.</span></span> <span data-ttu-id="76f24-109">Las empresas que trasladan a Azure sus cargas de trabajo de producción locales de máxima importancia se ven obligadas a configurar la recuperación ante desastres para dichas cargas de trabajo con vistas a garantizar el cumplimiento y protegerse contra las interrupciones en una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="76f24-109">With enterprises moving mission-critical on-premises production workloads to Azure, setting up disaster recovery for these workloads is mandatory for compliance and to safeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="76f24-110">Pasos para preparar para la replicación las máquinas migradas</span><span class="sxs-lookup"><span data-stu-id="76f24-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="76f24-111">Para preparar las máquinas migradas con vistas a configurar la replicación en otra región de Azure:</span><span class="sxs-lookup"><span data-stu-id="76f24-111">To prepare migrated machines for setting up replication to another Azure region:</span></span>

1. <span data-ttu-id="76f24-112">Complete la migración.</span><span class="sxs-lookup"><span data-stu-id="76f24-112">Complete migration.</span></span>
2. <span data-ttu-id="76f24-113">Si es necesario, instale el agente de Azure.</span><span class="sxs-lookup"><span data-stu-id="76f24-113">Install the Azure agent if needed.</span></span>
3. <span data-ttu-id="76f24-114">Quite Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="76f24-114">Remove the Mobility service.</span></span>  
4. <span data-ttu-id="76f24-115">Reinicie la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76f24-115">Restart the VM.</span></span>

<span data-ttu-id="76f24-116">Estos pasos se describen con más detalle en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="76f24-116">These steps are described in more detail in the following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-to-run-on-azure-vms"></a><span data-ttu-id="76f24-117">Paso 1: migrar cargas de trabajo en ejecución en máquinas virtuales de Hyper-V, máquinas virtuales de VMware y servidores físicos, para que pasen a ejecutarse en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="76f24-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers to run on Azure VMs</span></span>

<span data-ttu-id="76f24-118">Para configurar la replicación y migrar a Azure cargas de trabajo físicas, de Hyper-V y VMware locales, siga los pasos indicados en el artículo [Migración de máquinas virtuales de IaaS de Azure entre regiones de Azure con Azure Site Recovery](site-recovery-migrate-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="76f24-118">To set up replication and migrate your on-premises Hyper-V, VMware, and physical workloads to Azure, follow the steps in the [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="76f24-119">Después de la migración, no es necesario ejecutar una conmutación por error ni eliminarla.</span><span class="sxs-lookup"><span data-stu-id="76f24-119">After migration, you don't need to commit or delete a failover.</span></span> <span data-ttu-id="76f24-120">En su lugar, seleccione la opción **Completar la migración** para cada máquina que quiera migrar:</span><span class="sxs-lookup"><span data-stu-id="76f24-120">Instead, select the **Complete Migration** option for each machine you want to migrate:</span></span>
1. <span data-ttu-id="76f24-121">En **Elementos replicados**, haga clic con el botón derecho en la máquina virtual y después haga clic en **Completar migración**.</span><span class="sxs-lookup"><span data-stu-id="76f24-121">In **Replicated Items**, right-click the VM, and click **Complete Migration**.</span></span> <span data-ttu-id="76f24-122">Haga clic en **Aceptar** para completar el paso.</span><span class="sxs-lookup"><span data-stu-id="76f24-122">Click **OK** to complete the step.</span></span> <span data-ttu-id="76f24-123">Puede realizar un seguimiento del progreso en las propiedades de la máquina virtual. Para ello, supervise el trabajo Completar la migración en **Trabajos de Azure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="76f24-123">You can track progress in the VM properties by monitoring the Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="76f24-124">La acción **Completar la migración** termina el proceso de migración, quita la replicación de la máquina y detiene la facturación de la máquina en Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="76f24-124">The **Complete Migration** action completes the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

   ![Completar migración](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-the-azure-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="76f24-126">Paso 2: instalar el agente de máquina virtual de Azure en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="76f24-126">Step 2: Install the Azure VM agent on the virtual machine</span></span>
<span data-ttu-id="76f24-127">El [agente de máquina virtual](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) de Azure se debe instalar en la máquina virtual para que la extensión de Site Recovery funcione y proteja la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76f24-127">The Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on the virtual machine for the Site Recovery extension to work and to help protect the VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="76f24-128">A partir de la versión 9.7.0.0, en las máquinas virtuales Windows, el instalador de Mobility Service también instalará la versión más reciente del agente de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="76f24-128">Beginning with version 9.7.0.0, on Windows virtual machines, the Mobility service installer also installs the latest available Azure VM agent.</span></span> <span data-ttu-id="76f24-129">Tras la migración, la máquina virtual cumple el requisito previo de instalación del agente para usar cualquier extensión de máquina virtual, incluida la extensión de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="76f24-129">On migration, the virtual machine meets the agent installation prerequisite for using any VM extension, including the Site Recovery extension.</span></span> <span data-ttu-id="76f24-130">El agente de máquina virtual de Azure debe instalarse de forma manual únicamente si la versión de Mobility Service instalada en la máquina migrada es 9.6 o anterior.</span><span class="sxs-lookup"><span data-stu-id="76f24-130">The Azure VM agent needs to be manually installed only if the Mobility service installed on the migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="76f24-131">En la tabla siguiente se proporciona información adicional sobre cómo instalar el agente de máquina virtual y validar que se ha instalado:</span><span class="sxs-lookup"><span data-stu-id="76f24-131">The following table provides additional information about installing the VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="76f24-132">**Operación**</span><span class="sxs-lookup"><span data-stu-id="76f24-132">**Operation**</span></span> | <span data-ttu-id="76f24-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="76f24-133">**Windows**</span></span> | <span data-ttu-id="76f24-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="76f24-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="76f24-135">Instalación del agente de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="76f24-135">Installing the VM agent</span></span> |<span data-ttu-id="76f24-136">Descargue e instale el [MSI del agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="76f24-136">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="76f24-137">Para completar la instalación, necesita privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="76f24-137">You need administrator privileges to complete the installation.</span></span> |<span data-ttu-id="76f24-138">Instale el [agente de Linux](../virtual-machines/linux/agent-user-guide.md) más reciente.</span><span class="sxs-lookup"><span data-stu-id="76f24-138">Install the latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="76f24-139">Para completar la instalación, necesita privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="76f24-139">You need administrator privileges to complete the installation.</span></span> <span data-ttu-id="76f24-140">Se recomienda instalar el agente desde el repositorio de distribución.</span><span class="sxs-lookup"><span data-stu-id="76f24-140">We recommend installing the agent from your distribution repository.</span></span> <span data-ttu-id="76f24-141">*No se recomienda* instalar el agente de máquina virtual Linux directamente desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="76f24-141">We *do not recommend* installing the Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="76f24-142">Validación de la instalación del agente de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="76f24-142">Validating the VM agent installation</span></span> |<span data-ttu-id="76f24-143">1. Vaya a la carpeta C:\WindowsAzure\Packages de la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="76f24-143">1. Browse to the C:\WindowsAzure\Packages folder in the Azure VM.</span></span> <span data-ttu-id="76f24-144">El archivo WaAppAgent.exe debe estar ahí.</span><span class="sxs-lookup"><span data-stu-id="76f24-144">You should see the WaAppAgent.exe file.</span></span> <br><span data-ttu-id="76f24-145">2. Haga clic con el botón derecho en el archivo, desplácese hasta **Propiedades** y seleccione la pestaña **Detalles**.</span><span class="sxs-lookup"><span data-stu-id="76f24-145">2. Right-click the file, go to **Properties**, and then select the **Details** tab.</span></span> <span data-ttu-id="76f24-146">En el campo **Versión del producto**, debe aparecer el valor 2.6.1198.718 o uno superior.</span><span class="sxs-lookup"><span data-stu-id="76f24-146">The **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="76f24-147">N/D</span><span class="sxs-lookup"><span data-stu-id="76f24-147">N/A</span></span> |


### <a name="step-3-remove-the-mobility-service-from-the-migrated-virtual-machine"></a><span data-ttu-id="76f24-148">Paso 3: quitar Mobility Service de la máquina virtual migrada</span><span class="sxs-lookup"><span data-stu-id="76f24-148">Step 3: Remove the Mobility service from the migrated virtual machine</span></span>

<span data-ttu-id="76f24-149">Si ha migrado máquinas de VMware locales o servidores físicos de Windows o Linux, debe quitar o desinstalar manualmente Mobility Service de la máquina virtual migrada.</span><span class="sxs-lookup"><span data-stu-id="76f24-149">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need to manually remove/uninstall the Mobility service from the migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="76f24-150">Este paso no es necesario para las máquinas virtuales de Hyper-V migradas a Azure.</span><span class="sxs-lookup"><span data-stu-id="76f24-150">This step is not required for Hyper-V VMs migrated to Azure.</span></span>

#### <a name="uninstall-the-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="76f24-151">Desinstalar Mobility Service de una máquina virtual de Windows Server</span><span class="sxs-lookup"><span data-stu-id="76f24-151">Uninstall the Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="76f24-152">Use uno de los métodos siguientes para desinstalar Mobility Service de un equipo con Windows Server.</span><span class="sxs-lookup"><span data-stu-id="76f24-152">Use one of the following methods to uninstall the Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-the-windows-ui"></a><span data-ttu-id="76f24-153">Desinstalar mediante la interfaz de usuario de Windows</span><span class="sxs-lookup"><span data-stu-id="76f24-153">Uninstall by using the Windows UI</span></span>
1. <span data-ttu-id="76f24-154">En el Panel de Control, seleccione **Programas**.</span><span class="sxs-lookup"><span data-stu-id="76f24-154">In the Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="76f24-155">Seleccione **Microsoft Azure Site Recovery Mobility Service/Servidor de destino maestro** y, a continuación, haga clic en**Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="76f24-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="76f24-156">Desinstalación en un símbolo del sistema</span><span class="sxs-lookup"><span data-stu-id="76f24-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="76f24-157">Abra una ventana de símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="76f24-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="76f24-158">Para desinstalar Mobility Service, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="76f24-158">To uninstall the Mobility service, run the following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-the-mobility-service-on-a-linux-computer"></a><span data-ttu-id="76f24-159">Desinstalar Mobility Service de un equipo con Linux</span><span class="sxs-lookup"><span data-stu-id="76f24-159">Uninstall the Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="76f24-160">En el servidor Linux, inicie sesión como un usuario **raíz**.</span><span class="sxs-lookup"><span data-stu-id="76f24-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="76f24-161">En un terminal, vaya a /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="76f24-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="76f24-162">Para desinstalar Mobility Service, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="76f24-162">To uninstall the Mobility service, run the following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-the-vm"></a><span data-ttu-id="76f24-163">Paso 4: reiniciar la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="76f24-163">Step 4: Restart the VM</span></span>

<span data-ttu-id="76f24-164">Después de desinstalar Mobility Service, reinicie la máquina virtual antes de configurar la replicación en otra región de Azure.</span><span class="sxs-lookup"><span data-stu-id="76f24-164">After you uninstall the Mobility service, restart the VM before you set up replication to another Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="76f24-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76f24-165">Next steps</span></span>
- <span data-ttu-id="76f24-166">Empiece a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="76f24-166">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="76f24-167">Obtenga más información en las [instrucciones sobre redes para replicar máquinas virtuales de Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="76f24-167">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
