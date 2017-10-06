---
title: "servidores de aaaRemove y deshabilite la protección | Documentos de Microsoft"
description: "Este artículo describe cómo almacén toounregister servidores de recuperación del sitio y que toodisable protección para máquinas virtuales y servidores físicos."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="deea4-103">Quitar servidores y deshabilitar la protección</span><span class="sxs-lookup"><span data-stu-id="deea4-103">Remove servers and disable protection</span></span>

<span data-ttu-id="deea4-104">Hola servicio Azure Site Recovery contribuye tooyour la continuidad del negocio y estrategia de recuperación (BCDR).</span><span class="sxs-lookup"><span data-stu-id="deea4-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="deea4-105">servicio de Hello organiza la replicación, conmutación por error y recuperación de máquinas virtuales y servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="deea4-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="deea4-106">Máquinas pueden ser replicada tooAzure o centro de datos local secundario tooa.</span><span class="sxs-lookup"><span data-stu-id="deea4-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="deea4-107">Para obtener una introducción rápida, lea [¿Qué es Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="deea4-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="deea4-108">Este artículo describe cómo toounregister servidores de servicios de recuperación de un almacén en hello portal de Azure y cómo se protege toodisable protección para máquinas con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="deea4-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="deea4-109">Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="deea4-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="deea4-110">Anulación del registro de un servidor de configuración conectado</span><span class="sxs-lookup"><span data-stu-id="deea4-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="deea4-111">Si replica máquinas virtuales de VMware o tooAzure de servidores físicos de Windows o Linux, puede anular el registro un servidor de configuración conectado desde un almacén como sigue:</span><span class="sxs-lookup"><span data-stu-id="deea4-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="deea4-112">Deshabilite la protección de la máquina.</span><span class="sxs-lookup"><span data-stu-id="deea4-112">Disable machine protection.</span></span> <span data-ttu-id="deea4-113">En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="deea4-114">Anule la asociación de todas las directivas.</span><span class="sxs-lookup"><span data-stu-id="deea4-114">Disassociate any policies.</span></span> <span data-ttu-id="deea4-115">En **infraestructura del sitio de recuperación** > **para VMWare & máquinas físicas** > **directivas de replicación**, haga doble clic en hello directiva asociada.</span><span class="sxs-lookup"><span data-stu-id="deea4-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="deea4-116">Servidor de configuración contextual hello > **desasociar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="deea4-117">Retire cualquier proceso local o servidores de destino maestros adicionales.</span><span class="sxs-lookup"><span data-stu-id="deea4-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="deea4-118">En **infraestructura del sitio de recuperación** > **para VMWare & máquinas físicas** > **servidores de configuración**, servidor de Hola de menú contextual > **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="deea4-119">Eliminar el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="deea4-120">Desinstalar manualmente el servicio de movilidad de hello ejecutando en el servidor de destino maestro hello (se trata de cualquier otro servidor o servidor de configuración de hello en ejecución).</span><span class="sxs-lookup"><span data-stu-id="deea4-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="deea4-121">Desinstale todos los servidores de procesos adicionales.</span><span class="sxs-lookup"><span data-stu-id="deea4-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="deea4-122">Desinstale el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="deea4-123">En el servidor de configuración de hello, desinstale la instancia de Hola de MySQL que se instaló con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="deea4-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="deea4-124">En el registro de Hola Hola del servidor de configuración eliminar la clave de hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="deea4-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="deea4-125">Anulación del registro de un servidor de configuración no conectado</span><span class="sxs-lookup"><span data-stu-id="deea4-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="deea4-126">Si replica máquinas virtuales de VMware o tooAzure de servidores físicos de Windows o Linux, puede anular el registro un servidor de configuración no conectada desde un almacén como sigue:</span><span class="sxs-lookup"><span data-stu-id="deea4-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="deea4-127">Deshabilite la protección de la máquina.</span><span class="sxs-lookup"><span data-stu-id="deea4-127">Disable machine protection.</span></span> <span data-ttu-id="deea4-128">En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="deea4-129">Seleccione **dejar de administrar Hola máquina**.</span><span class="sxs-lookup"><span data-stu-id="deea4-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="deea4-130">Retire cualquier proceso local o servidores de destino maestros adicionales.</span><span class="sxs-lookup"><span data-stu-id="deea4-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="deea4-131">En **infraestructura del sitio de recuperación** > **para VMWare & máquinas físicas** > **servidores de configuración**, servidor de Hola de menú contextual > **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="deea4-132">Eliminar el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="deea4-133">Desinstalar manualmente el servicio de movilidad de hello ejecutando en el servidor de destino maestro hello (se trata de cualquier otro servidor o servidor de configuración de hello en ejecución).</span><span class="sxs-lookup"><span data-stu-id="deea4-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="deea4-134">Desinstale todos los servidores de procesos adicionales.</span><span class="sxs-lookup"><span data-stu-id="deea4-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="deea4-135">Desinstale el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="deea4-136">En el servidor de configuración de hello, desinstale la instancia de Hola de MySQL que se instaló con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="deea4-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="deea4-137">En el registro de Hola Hola del servidor de configuración eliminar la clave de hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="deea4-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="deea4-138">Anulación del registro de un servidor VMM conectado</span><span class="sxs-lookup"><span data-stu-id="deea4-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="deea4-139">Como práctica recomendada, se recomienda que anule el registro de servidor VMM hello cuando se ha conectado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="deea4-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="deea4-140">Esto garantiza que en los servidores VMM hello (y en otros servidores VMM a nubes emparejadas) se borra la configuración correctamente.</span><span class="sxs-lookup"><span data-stu-id="deea4-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="deea4-141">Debe quitar un servidor no conectado solo si hay un problema permanente con la conectividad.</span><span class="sxs-lookup"><span data-stu-id="deea4-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="deea4-142">Si no está conectado el servidor VMM hello, será necesario toomanually ejecutar un tooclean script la configuración.</span><span class="sxs-lookup"><span data-stu-id="deea4-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="deea4-143">Detener la replicación de máquinas virtuales en nubes en el servidor VMM que desee tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="deea4-144">Eliminar cualquier asignación de red utilizado por las nubes en el servidor VMM que desee toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="deea4-145">En **infraestructura del sitio de recuperación** > **para System Center VMM** > **asignación de red**, haga clic en la asignación de red hello >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="deea4-146">Desvincular directivas de replicación de las nubes en el servidor VMM que desee tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="deea4-147">En **infraestructura del sitio de recuperación** > **para System Center VMM** >  **directivas de replicación**, haga doble clic en directiva de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="deea4-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="deea4-148">Pulse el botón derecho en la nube hello > **desasociar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="deea4-149">Eliminar servidor VMM de Hola o un nodo activo de VMM.</span><span class="sxs-lookup"><span data-stu-id="deea4-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="deea4-150">En **infraestructura del sitio de recuperación** > **para System Center VMM** > **servidores VMM**, servidor de hello contextual >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="deea4-151">Desinstalar Hola proveedor de forma manual en el servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="deea4-152">Si tiene un clúster, quítelo de todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="deea4-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="deea4-153">Si replica tooAzure, quite manualmente el agente de servicios de recuperación de Microsoft de Hola de hosts de Hyper-V en nubes de hello eliminado.</span><span class="sxs-lookup"><span data-stu-id="deea4-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="deea4-154">Anulación del registro de un servidor VMM desconectado</span><span class="sxs-lookup"><span data-stu-id="deea4-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="deea4-155">Detener la replicación de máquinas virtuales en nubes en el servidor VMM que desee tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="deea4-156">Eliminar cualquier asignación de red utilizado por las nubes en servidores VMM de Hola que desee toodelete.</span><span class="sxs-lookup"><span data-stu-id="deea4-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="deea4-157">En **infraestructura del sitio de recuperación** > **para System Center VMM** > **asignación de red**, haga clic en la asignación de red hello >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="deea4-158">Tenga en cuenta Id. de Hola Hola del servidor de VMM.</span><span class="sxs-lookup"><span data-stu-id="deea4-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="deea4-159">Desvincular directivas de replicación de las nubes en el servidor VMM que desee tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="deea4-160">En **infraestructura del sitio de recuperación** > **para System Center VMM** >  **directivas de replicación**, haga doble clic en directiva de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="deea4-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="deea4-161">Pulse el botón derecho en la nube hello > **desasociar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="deea4-162">Eliminar servidor VMM de Hola o un nodo activo.</span><span class="sxs-lookup"><span data-stu-id="deea4-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="deea4-163">En **infraestructura del sitio de recuperación** > **para System Center VMM** > **servidores VMM**, servidor de hello contextual >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="deea4-164">Descargue y ejecute hello [script de limpieza](http://aka.ms/asr-cleanup-script-vmm) en servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="deea4-165">Abra PowerShell con hello **ejecutar como administrador** opción, la directiva de ejecución de toochange hello para el ámbito de hello predeterminado (LocalMachine).</span><span class="sxs-lookup"><span data-stu-id="deea4-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="deea4-166">En el script de Hola, especificar el identificador de Hola de hello servidor VMM que desee tooremove.</span><span class="sxs-lookup"><span data-stu-id="deea4-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="deea4-167">script de Hola quita el registro y la información del servidor de Hola de emparejamiento de nube.</span><span class="sxs-lookup"><span data-stu-id="deea4-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="deea4-168">Ejecutar script de limpieza de hello en otros servidores VMM que contienen las nubes que se emparejan con nubes en el servidor VMM que desee tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="deea4-169">Ejecutar script de limpieza de Hola en cualquier otros pasivo VMM nodos del clúster que tengan Hola que proveedor instalado.</span><span class="sxs-lookup"><span data-stu-id="deea4-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="deea4-170">Desinstalar Hola proveedor de forma manual en el servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="deea4-171">Si tiene un clúster, quítelo de todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="deea4-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="deea4-172">Si replicar tooAzure, se puede quitar al agente de servicios de recuperación de Microsoft hello desde hosts de Hyper-V en nubes de hello eliminado.</span><span class="sxs-lookup"><span data-stu-id="deea4-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="deea4-173">Anulación del registro de un host Hyper-V en un sitio de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="deea4-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="deea4-174">Los hosts Hyper-V que no están administrados por VMM se reúnen en un sitio de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="deea4-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="deea4-175">Puede eliminar un host en un sitio Hyper-V de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="deea4-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="deea4-176">Deshabilite la replicación para máquinas virtuales de Hyper-V ubicadas en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="deea4-177">Anular la asociación de las directivas para el sitio de Hyper-V de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="deea4-178">En **infraestructura del sitio de recuperación** > **para sitios de Hyper-V** >  **directivas de replicación**, haga doble clic en directiva de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="deea4-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="deea4-179">Sitio de hello contextual > **desasociar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="deea4-180">Elimine los hosts de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="deea4-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="deea4-181">En **infraestructura del sitio de recuperación** > **para System Center VMM** > **Hosts de Hyper-V**, servidor de hello contextual >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="deea4-182">Eliminar sitio Hola Hyper-V después de han eliminados todos los hosts del mismo.</span><span class="sxs-lookup"><span data-stu-id="deea4-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="deea4-183">En **infraestructura del sitio de recuperación** > **para System Center VMM** > **sitios de Hyper-V**, sitio de hello contextual >  **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="deea4-184">Ejecute hello siguiente secuencia de comandos en cada host de Hyper-V que se haya quitado.</span><span class="sxs-lookup"><span data-stu-id="deea4-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="deea4-185">script de Hola limpia la configuración en el servidor de Hola y anula el registro del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="deea4-186">Deshabilitación de la protección de una máquina virtual de VMware o un servidor físico</span><span class="sxs-lookup"><span data-stu-id="deea4-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="deea4-187">En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="deea4-188">En **Remove Machine** (Quitar máquina), seleccione una de estas opciones:</span><span class="sxs-lookup"><span data-stu-id="deea4-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="deea4-189">**Deshabilite la protección de máquina de hello (recomendado)**.</span><span class="sxs-lookup"><span data-stu-id="deea4-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="deea4-190">Utilice este toostop opción replicar máquina Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="deea4-191">La configuración de Site Recovery se limpiará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="deea4-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="deea4-192">Solo verá esta opción en hello siguientes circunstancias:</span><span class="sxs-lookup"><span data-stu-id="deea4-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="deea4-193">**Se cambia el tamaño de volumen de la máquina virtual de Hola**: cuando cambia el tamaño de un saludo del volumen virtual máquina entra en un estado crítico.</span><span class="sxs-lookup"><span data-stu-id="deea4-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="deea4-194">Seleccione esta opción de la protección de toodisables conservando los puntos de recuperación en Azure.</span><span class="sxs-lookup"><span data-stu-id="deea4-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="deea4-195">Al habilitar la protección de máquina de Hola de nuevo, datos de hello para el volumen de hello cambia de tamaño serán tooAzure transferido.</span><span class="sxs-lookup"><span data-stu-id="deea4-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="deea4-196">**Se ha ejecutado recientemente una conmutación por error**: una vez ejecutado un tootest de conmutación por error en su entorno, seleccione este toostart opción proteger máquinas locales de nuevo.</span><span class="sxs-lookup"><span data-stu-id="deea4-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="deea4-197">Deshabilita cada máquina virtual y, a continuación, necesita tooenable protección para ellos nuevo.</span><span class="sxs-lookup"><span data-stu-id="deea4-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="deea4-198">Deshabilitar máquina Hola con esta configuración no afecta a la máquina virtual de réplica hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="deea4-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="deea4-199">No desinstale el servicio de movilidad de saludo de la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="deea4-200">**Detener administración de máquina de hello**.</span><span class="sxs-lookup"><span data-stu-id="deea4-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="deea4-201">Si selecciona esta opción, solo se quitará máquina Hola del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="deea4-202">No se verá afectada la configuración de protección local para la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="deea4-203">configuración de tooremove de máquina de Hola y máquina de hello tooremove de hello suscripción de Azure, necesita una configuración de hello tooclean, desinstale el servicio de movilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="deea4-204">Deshabilitación de la protección de una máquina virtual de Hyper-V en una nube VMM</span><span class="sxs-lookup"><span data-stu-id="deea4-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="deea4-205">En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="deea4-206">En **Remove Machine** (Quitar máquina), seleccione una de estas opciones:</span><span class="sxs-lookup"><span data-stu-id="deea4-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="deea4-207">**Deshabilite la protección de máquina de hello (recomendado)**.</span><span class="sxs-lookup"><span data-stu-id="deea4-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="deea4-208">Utilice este toostop opción replicar máquina Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="deea4-209">La configuración de Site Recovery se limpiará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="deea4-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="deea4-210">**Detener administración de máquina de hello**.</span><span class="sxs-lookup"><span data-stu-id="deea4-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="deea4-211">Si selecciona esta opción, solo se quitará máquina Hola del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="deea4-212">No se verá afectada la configuración de protección local para la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="deea4-213">configuración de tooremove de máquina de Hola y máquina de hello tooremove de hello suscripción de Azure, necesita tooclean Hola una configuración de seguridad manualmente, mediante instrucciones de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="deea4-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="deea4-214">Tenga en cuenta que si selecciona la máquina virtual de toodelete hello y sus discos duros, deberá quitarse de ubicación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="deea4-215">Limpiar la configuración de protección - sitio secundario de VMM de replicación tooa</span><span class="sxs-lookup"><span data-stu-id="deea4-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="deea4-216">Si seleccionó **detener administración de máquina de hello** y que replicar tooa sitio secundario, ejecute este script en hello servidor principal tooclean la configuración de Hola de máquina virtual principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="deea4-217">En la consola VMM Hola haga clic en consola de PowerShell VMM Hola PowerShell botón tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="deea4-218">Reemplace SQLVM1 por nombre de saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="deea4-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="deea4-219">En el servidor VMM secundario de hello ejecute este tooclean script la configuración de hello para la máquina virtual secundaria de hello:</span><span class="sxs-lookup"><span data-stu-id="deea4-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="deea4-220">En el servidor VMM secundario de hello, actualizar máquinas virtuales de hello en el servidor de host de Hyper-V de hello, de modo que hello VM secundaria obtiene volvió a detectar en la consola VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="deea4-221">Hola anteriormente pasos borrar la configuración de replicación de hello en el servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="deea4-222">Si desea que la replicación de toostop para la máquina virtual de hello, ejecutar la siguiente secuencia de comandos al final de Hola Hola máquinas virtuales principales y secundarias.</span><span class="sxs-lookup"><span data-stu-id="deea4-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="deea4-223">Reemplace SQLVM1 por nombre de saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="deea4-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="deea4-224">Limpiar la configuración de protección - tooAzure de replicación</span><span class="sxs-lookup"><span data-stu-id="deea4-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="deea4-225">Si seleccionó **detener administración de máquina de hello** y replicar tooAzure, ejecute este script Hola servidor VMM de origen, con PowerShell desde la consola VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="deea4-226">Hola anteriormente pasos borrar la configuración de replicación de hello en servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="deea4-227">replicación de toostop para la máquina virtual de hello ejecutando en el servidor de host de Hyper-V de hello, ejecute este script.</span><span class="sxs-lookup"><span data-stu-id="deea4-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="deea4-228">Reemplace SQLVM1 por nombre de hello de la máquina virtual y host01.contoso.com con el nombre de saludo del servidor de host de Hyper-V de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="deea4-229">Deshabilitación de la protección de una máquina virtual de Hyper-V en un sitio de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="deea4-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="deea4-230">Utilice este procedimiento si replica máquinas virtuales de Hyper-V tooAzure sin un servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="deea4-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="deea4-231">En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="deea4-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="deea4-232">En **quitar máquina**, puede seleccionar Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="deea4-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="deea4-233">**Deshabilite la protección de máquina de hello (recomendado)**.</span><span class="sxs-lookup"><span data-stu-id="deea4-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="deea4-234">Utilice este toostop opción replicar máquina Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="deea4-235">La configuración de Site Recovery se limpiará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="deea4-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="deea4-236">**Detener administración de máquina de hello**.</span><span class="sxs-lookup"><span data-stu-id="deea4-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="deea4-237">Si selecciona esta opción máquina Hola solo se quitará del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="deea4-238">No se verá afectada la configuración de protección local para la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="deea4-239">configuración de tooremove de máquina de Hola y tooremove Hola virtual machine de hello suscripción de Azure, necesita tooclean Hola una configuración de seguridad manualmente.</span><span class="sxs-lookup"><span data-stu-id="deea4-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="deea4-240">Si selecciona la máquina virtual de toodelete hello y sus discos duros se quitarán de la ubicación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="deea4-241">Si seleccionó **detener administración de máquina de hello**, ejecute este script en el servidor de host de Hyper-V de origen de hello, la replicación de tooremove para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="deea4-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="deea4-242">Reemplace SQLVM1 por nombre de saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="deea4-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
