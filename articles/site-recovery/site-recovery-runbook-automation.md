---
title: "Automatización de Azure los planes toorecovery aaaAdd runbooks en Azure Site Recovery | Documentos de Microsoft"
description: "Obtenga información sobre cómo Azure Site Recovery puede ayudarle a ampliar los planes de recuperación mediante Azure Automation. Obtenga información acerca de cómo toocomplete complejo tareas durante la recuperación tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="c4e63-104">Agregar planes de toorecovery de runbooks de automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="c4e63-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="c4e63-105">En este artículo se describe cómo se integra Azure Site Recovery con toohelp de automatización de Azure extiende los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="c4e63-106">Los planes de recuperación pueden organizar la recuperación de máquinas virtuales protegidas con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c4e63-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="c4e63-107">Planes de recuperación de trabajo para la nube secundaria tooa de replicación tanto para tooAzure de replicación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="c4e63-108">Planes de recuperación también ayudan a realizar la recuperación de hello **coherentes y precisos**, **repetible**, y **automatizada**.</span><span class="sxs-lookup"><span data-stu-id="c4e63-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="c4e63-109">Si la conmutación por error el tooAzure de las máquinas virtuales, la integración con automatización de Azure amplía los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="c4e63-110">Puede usar tooexecute runbooks, que ofrecen las tareas de automatización eficaz.</span><span class="sxs-lookup"><span data-stu-id="c4e63-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="c4e63-111">Si es nuevo tooAzure automatización, puede [registrarse](https://azure.microsoft.com/services/automation/) y [descargar scripts de muestra](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="c4e63-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="c4e63-112">Para obtener más información y toolearn cómo tooorchestrate tooAzure de recuperación mediante el uso de [planes de recuperación](https://azure.microsoft.com/blog/?p=166264), consulte [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="c4e63-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="c4e63-113">En este artículo se explica cómo integrar runbooks de Azure Automation en los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="c4e63-114">Se usan tareas básicas de ejemplos tooautomate que anteriormente requerían intervención manual.</span><span class="sxs-lookup"><span data-stu-id="c4e63-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="c4e63-115">También se describe cómo tooconvert una tooa de recuperación de varios pasos con un solo clic acción de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="c4e63-116">Personalizar plan de recuperación de Hola</span><span class="sxs-lookup"><span data-stu-id="c4e63-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="c4e63-117">Vaya toohello **Site Recovery** hoja de recursos del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="c4e63-118">En este ejemplo, el plan de recuperación de hello tiene tooit agregado dos de las máquinas virtuales, para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="c4e63-119">toobegin adición de un runbook, haga clic en hello **personalizar** ficha.</span><span class="sxs-lookup"><span data-stu-id="c4e63-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![Haga clic en el botón Personalizar de Hola](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="c4e63-121">Haga clic con el botón derecho en **Grupo 1: Iniciar** y luego seleccione **Agregar acción posterior**.</span><span class="sxs-lookup"><span data-stu-id="c4e63-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Clic con el botón derecho en Grupo 1: Iniciar y adición de acción posterior](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="c4e63-123">Haga clic en **Elegir un script**.</span><span class="sxs-lookup"><span data-stu-id="c4e63-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="c4e63-124">En hello **actualizar acción** hoja, la secuencia de comandos de nombre hello **Hello World**.</span><span class="sxs-lookup"><span data-stu-id="c4e63-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![módulo de acción de actualización de Hola](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="c4e63-126">Escriba un nombre de cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="c4e63-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="c4e63-127">Hola cuenta de automatización puede estar en cualquier región de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e63-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="c4e63-128">Hola cuenta de automatización debe estar en hello misma suscripción como almacén de Azure Site Recovery Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="c4e63-129">En la cuenta de Automation, seleccione un runbook.</span><span class="sxs-lookup"><span data-stu-id="c4e63-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="c4e63-130">Este runbook es el script de Hola que se ejecuta durante la ejecución de Hola Hola del plan de recuperación, después de la recuperación de hello del primer grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="c4e63-131">script de Hola toosave, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c4e63-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="c4e63-132">script de Hola se agrega demasiado**grupo 1: pasos posteriores a la**.</span><span class="sxs-lookup"><span data-stu-id="c4e63-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![Acción posterior Grupo 1: Iniciar](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="c4e63-134">Consideraciones para agregar un script</span><span class="sxs-lookup"><span data-stu-id="c4e63-134">Considerations for adding a script</span></span>

* <span data-ttu-id="c4e63-135">Opciones de demasiado**eliminar un paso** o **actualizar script de Hola**, haga clic en el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="c4e63-136">Una secuencia de comandos puede ejecutar en Azure durante la conmutación por error desde un tooAzure de la máquina local.</span><span class="sxs-lookup"><span data-stu-id="c4e63-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="c4e63-137">También puede ejecutarse en Azure como una secuencia de comandos del sitio primario antes del cierre, durante la conmutación por recuperación de máquina local de Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="c4e63-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="c4e63-138">Cuando se ejecuta un script, inserta un contexto del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="c4e63-139">Hola de ejemplo siguiente muestra una variable de contexto:</span><span class="sxs-lookup"><span data-stu-id="c4e63-139">hello following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="c4e63-140">Hello en la tabla siguiente enumera Hola nombre y una descripción de cada variable de contexto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="c4e63-141">**Nombre de la variable**</span><span class="sxs-lookup"><span data-stu-id="c4e63-141">**Variable name**</span></span> | <span data-ttu-id="c4e63-142">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="c4e63-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="c4e63-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="c4e63-143">RecoveryPlanName</span></span> |<span data-ttu-id="c4e63-144">nombre de Hello del plan de Hola que se va a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="c4e63-144">hello name of hello plan being run.</span></span> <span data-ttu-id="c4e63-145">Esta variable le ayuda a realizar diferentes acciones basadas en nombre del plan de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="c4e63-146">También puede volver a usar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="c4e63-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="c4e63-147">FailoverType</span></span> |<span data-ttu-id="c4e63-148">Especifica si la conmutación por error de hello es una prueba, planeada o no planeada.</span><span class="sxs-lookup"><span data-stu-id="c4e63-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="c4e63-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="c4e63-149">FailoverDirection</span></span> |<span data-ttu-id="c4e63-150">Especifica si la recuperación es sitio primario o secundario de tooa.</span><span class="sxs-lookup"><span data-stu-id="c4e63-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="c4e63-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="c4e63-151">GroupID</span></span> |<span data-ttu-id="c4e63-152">Identifica el número de grupo de hello en el plan de recuperación de hello cuando se ejecuta el plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="c4e63-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="c4e63-153">VmMap</span></span> |<span data-ttu-id="c4e63-154">Una matriz de todas las máquinas virtuales en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="c4e63-155">Clave de VMMap</span><span class="sxs-lookup"><span data-stu-id="c4e63-155">VMMap key</span></span> |<span data-ttu-id="c4e63-156">Clave única (GUID) para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4e63-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="c4e63-157">Su Hola igual Hola Id. de Azure Virtual Machine Manager (VMM) de Hola de máquina virtual, si procede.</span><span class="sxs-lookup"><span data-stu-id="c4e63-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="c4e63-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="c4e63-158">SubscriptionId</span></span> |<span data-ttu-id="c4e63-159">Id. de suscripción de Azure de Hola Hola a máquina virtual en el que se creó.</span><span class="sxs-lookup"><span data-stu-id="c4e63-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="c4e63-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="c4e63-160">RoleName</span></span> |<span data-ttu-id="c4e63-161">nombre de Hola de hello VM de Azure que se va a recuperar.</span><span class="sxs-lookup"><span data-stu-id="c4e63-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="c4e63-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="c4e63-162">CloudServiceName</span></span> |<span data-ttu-id="c4e63-163">nombre de servicio de nube de Azure Hola que Hola a VM en la que se creó.</span><span class="sxs-lookup"><span data-stu-id="c4e63-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="c4e63-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="c4e63-164">ResourceGroupName</span></span>|<span data-ttu-id="c4e63-165">nombre del grupo de recursos de Azure Hola que Hola a VM en la que se creó.</span><span class="sxs-lookup"><span data-stu-id="c4e63-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="c4e63-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="c4e63-166">RecoveryPointId</span></span>|<span data-ttu-id="c4e63-167">marca de tiempo de Hola para cuando se recupera Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4e63-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="c4e63-168">Asegúrese de que esa cuenta de automatización de hello tiene Hola siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="c4e63-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="c4e63-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="c4e63-169">AzureRM.profile</span></span>
    * <span data-ttu-id="c4e63-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="c4e63-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="c4e63-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="c4e63-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="c4e63-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="c4e63-172">AzureRM.Network</span></span>
    * <span data-ttu-id="c4e63-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="c4e63-173">AzureRM.Compute</span></span>

<span data-ttu-id="c4e63-174">Todos los módulos deben ser de versiones compatibles.</span><span class="sxs-lookup"><span data-stu-id="c4e63-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="c4e63-175">Un tooensure de manera sencilla que todos los módulos sean compatibles es versiones más recientes de hello toouse de todos los módulos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="c4e63-176">Obtener acceso a todas las máquinas virtuales de hello VMMap en un bucle</span><span class="sxs-lookup"><span data-stu-id="c4e63-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="c4e63-177">Usar hello siguiendo tooloop de código en todas las máquinas virtuales de hello VMMap Microsoft:</span><span class="sxs-lookup"><span data-stu-id="c4e63-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="c4e63-178">Hola recursos grupo nombre de rol de valores de nombre y están vacíos al script de Hola es un grupo de arranque de acción previa tooa.</span><span class="sxs-lookup"><span data-stu-id="c4e63-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="c4e63-179">valores de Hello se llenan solo si se realiza correctamente Hola máquinas virtuales de ese grupo de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="c4e63-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="c4e63-180">script de Hola es una acción posterior a la del grupo de arranque de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="c4e63-181">Use Hola mismo runbook de automatización en varios planes de recuperación</span><span class="sxs-lookup"><span data-stu-id="c4e63-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="c4e63-182">Puede usar un solo script en varios planes de recuperación gracias a las variables externas.</span><span class="sxs-lookup"><span data-stu-id="c4e63-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="c4e63-183">Puede usar [las variables de automatización de Azure](../automation/automation-variables.md) toostore parámetros que se pueden pasar en una recuperación del plan de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c4e63-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="c4e63-184">Al agregar el nombre del plan de recuperación de hello como una variable de toohello de prefijo, puede crear variables individuales para cada plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="c4e63-185">A continuación, utilice las variables de hello como parámetros.</span><span class="sxs-lookup"><span data-stu-id="c4e63-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="c4e63-186">Puede cambiar un parámetro sin cambiar el script de Hola, pero todavía cambio Hola Hola forma funciona de la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="c4e63-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="c4e63-187">Uso de una variable de cadena simple en un script de runbook</span><span class="sxs-lookup"><span data-stu-id="c4e63-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="c4e63-188">En este ejemplo, una secuencia de comandos toma la entrada de Hola de un grupo de seguridad de red (NSG) y aplica toohello las máquinas virtuales de un plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="c4e63-189">Para hello toodetect de script se ejecuta el plan de recuperación, use el contexto del plan de recuperación de hello:</span><span class="sxs-lookup"><span data-stu-id="c4e63-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="c4e63-190">tooapply un NSG existente, debe conocer el nombre NSG de Hola y nombre del grupo de recursos de hello NSG.</span><span class="sxs-lookup"><span data-stu-id="c4e63-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="c4e63-191">Use estas variables como entradas para los scripts del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="c4e63-192">toodo esto, cree dos variables Hola activos de automatización de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="c4e63-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="c4e63-193">Agregar nombre de Hola Hola del plan de recuperación que va a crear parámetros de Hola para que un nombre de variable de toohello de prefijo.</span><span class="sxs-lookup"><span data-stu-id="c4e63-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="c4e63-194">Crear un nombre de variable toostore hello NSG.</span><span class="sxs-lookup"><span data-stu-id="c4e63-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="c4e63-195">Agregar un nombre de variable de prefijo toohello mediante nombre de Hola Hola del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Creación de una variable de nombre de NSG](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="c4e63-197">Crear nombre de grupo de recursos de un NSG de hello toostore variable.</span><span class="sxs-lookup"><span data-stu-id="c4e63-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="c4e63-198">Agregar un nombre de variable de prefijo toohello mediante nombre de Hola Hola del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Creación de un nombre de grupo de recursos de NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="c4e63-200">En el script de Hola, utilice Hola siguiendo los valores de variable de referencia código tooget hello:</span><span class="sxs-lookup"><span data-stu-id="c4e63-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="c4e63-201">Utilice variables de hello en el interfaz de red de hello runbook tooapply hello NSG toohello de Hola conmutó por error máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="c4e63-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="c4e63-202">Para cada plan de recuperación, crear variables independientes para que se puede volver a usar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="c4e63-203">Agregar un prefijo mediante el nombre del plan de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="c4e63-204">Para obtener un script completo, to-end para este escenario, vea [agregar un tooVMs NSG e IP públicas durante la conmutación por error de prueba de un plan de recuperación de Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="c4e63-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="c4e63-205">Usar una variable complejo toostore más información</span><span class="sxs-lookup"><span data-stu-id="c4e63-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="c4e63-206">Considere un escenario en el que desea que un tooturn script único en una IP pública en máquinas virtuales específicas.</span><span class="sxs-lookup"><span data-stu-id="c4e63-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="c4e63-207">En otro escenario, le podría interesar tooapply NSG diferentes en diferentes máquinas virtuales (no en todas las máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="c4e63-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="c4e63-208">Puede crear un script que se pueda volver a usar para cualquier plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="c4e63-209">Cada plan de recuperación puede tener un número variable de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c4e63-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="c4e63-210">Por ejemplo, una recuperación de SharePoint tiene dos servidores front-end.</span><span class="sxs-lookup"><span data-stu-id="c4e63-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="c4e63-211">Una aplicación básica de línea de negocio (LOB) tiene solo un servidor front-end.</span><span class="sxs-lookup"><span data-stu-id="c4e63-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="c4e63-212">No puede crear variables independientes para cada plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c4e63-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="c4e63-213">En el siguiente ejemplo de Hola, se utiliza una técnica nuevo y cree una [complejo de variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) en los activos de cuenta de automatización de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="c4e63-214">Para ello se especifican varios valores.</span><span class="sxs-lookup"><span data-stu-id="c4e63-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="c4e63-215">Debe usar Azure PowerShell toocomplete Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c4e63-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="c4e63-216">En PowerShell, inicie sesión en tooyour suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="c4e63-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="c4e63-217">parámetros de hello toostore, crear Hola complejo variable mediante nombre de Hola Hola del plan de recuperación:</span><span class="sxs-lookup"><span data-stu-id="c4e63-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="c4e63-218">En esta variable complejo, **VMDetails** es hello Id. de máquina virtual para hello protegido la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4e63-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="c4e63-219">Id. de máquina virtual, del tooget Hola Hola portal de Azure, ver las propiedades VM Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="c4e63-220">Hello captura de pantalla siguiente muestra una variable que almacena los detalles de Hola de dos máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="c4e63-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Usar hello Id. de máquina virtual como Hola GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="c4e63-222">Use esta variable en el runbook.</span><span class="sxs-lookup"><span data-stu-id="c4e63-222">Use this variable in your runbook.</span></span> <span data-ttu-id="c4e63-223">Si Hola indica el que GUID de la VM se encuentra en el contexto del plan de recuperación de hello, hello NSG se aplican en hello VM:</span><span class="sxs-lookup"><span data-stu-id="c4e63-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="c4e63-224">En su runbook, recorrer las máquinas virtuales de Hola de contexto del plan de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4e63-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="c4e63-225">Compruebe si existe Hola VM en **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="c4e63-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="c4e63-226">Si existe, obtener acceso a propiedades de Hola de Hola tooapply variable Hola NSG:</span><span class="sxs-lookup"><span data-stu-id="c4e63-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="c4e63-227">Puede usar Hola mismo script para los planes de recuperación diferente.</span><span class="sxs-lookup"><span data-stu-id="c4e63-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="c4e63-228">Escriba los parámetros diferentes mediante el almacenamiento de valor de Hola que corresponde el plan de recuperación de tooa en distintas variables.</span><span class="sxs-lookup"><span data-stu-id="c4e63-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="c4e63-229">Scripts de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c4e63-229">Sample scripts</span></span>

<span data-ttu-id="c4e63-230">tooyour secuencias de comandos de ejemplo toodeploy cuenta de automatización, haga clic en hello **implementar tooAzure** botón.</span><span class="sxs-lookup"><span data-stu-id="c4e63-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="c4e63-231">[![Implementar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="c4e63-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="c4e63-232">Para obtener otro ejemplo, vea Hola después de vídeo.</span><span class="sxs-lookup"><span data-stu-id="c4e63-232">For another example, see hello following video.</span></span> <span data-ttu-id="c4e63-233">Muestra cómo toorecover una tooAzure de aplicación de WordPress de dos niveles:</span><span class="sxs-lookup"><span data-stu-id="c4e63-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="c4e63-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c4e63-234">Additional resources</span></span>
* [<span data-ttu-id="c4e63-235">Cuenta de ejecución del servicio Azure Automation</span><span class="sxs-lookup"><span data-stu-id="c4e63-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="c4e63-236">Información general sobre Azure Automation</span><span class="sxs-lookup"><span data-stu-id="c4e63-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Información general sobre Azure Automation")
* [<span data-ttu-id="c4e63-237">Scripts de ejemplo de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="c4e63-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Scripts de ejemplo de Azure Automation")
