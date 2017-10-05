---
title: "Incorporación de runbooks de Azure Automation a los planes de recuperación en Azure Site Recovery | Microsoft Docs"
description: "Obtenga información sobre cómo Azure Site Recovery puede ayudarle a ampliar los planes de recuperación mediante Azure Automation. Aprenda a realizar tareas complejas durante la recuperación en Azure."
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
ms.openlocfilehash: 064a6782970b950543f93c24800998c1f104c8df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans"></a><span data-ttu-id="49773-104">Incorporación de runbooks de Azure Automation a los planes de recuperación</span><span class="sxs-lookup"><span data-stu-id="49773-104">Add Azure Automation runbooks to recovery plans</span></span>
<span data-ttu-id="49773-105">En este artículo se explica cómo se integra Azure Site Recovery con Azure Automation para ayudarle a ampliar los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation to help you extend your recovery plans.</span></span> <span data-ttu-id="49773-106">Los planes de recuperación pueden organizar la recuperación de máquinas virtuales protegidas con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="49773-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="49773-107">Los planes de recuperación funcionan para la replicación en una nube secundaria y para la replicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="49773-107">Recovery plans work both for replication to a secondary cloud, and for replication to Azure.</span></span> <span data-ttu-id="49773-108">Los planes de recuperación además ayudan a que la recuperación sea **coherente y precisa**, **repetible** y **automatizada**.</span><span class="sxs-lookup"><span data-stu-id="49773-108">Recovery plans also help make the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="49773-109">Si conmuta por error las máquinas virtuales en Azure, la integración con Azure Automation amplía los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-109">If you fail over your VMs to Azure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="49773-110">Se puede usar para ejecutar runbooks, que ofrecen eficaces tareas de automatización.</span><span class="sxs-lookup"><span data-stu-id="49773-110">You can use it to execute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="49773-111">Si no está familiarizado con Azure Automation, puede [registrarse](https://azure.microsoft.com/services/automation/) y [descargar scripts de muestra](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="49773-111">If you are new to Azure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="49773-112">Para más información y para aprender a organizar la recuperación en Azure mediante [planes de recuperación](https://azure.microsoft.com/blog/?p=166264), vea [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="49773-112">For more information, and to learn how to orchestrate recovery to Azure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="49773-113">En este artículo se explica cómo integrar runbooks de Azure Automation en los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="49773-114">Se usan ejemplos para automatizar tareas básicas que anteriormente requerían intervención manual.</span><span class="sxs-lookup"><span data-stu-id="49773-114">We use examples to automate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="49773-115">También se explica cómo convertir una recuperación de varios pasos en una acción de recuperación de un solo clic.</span><span class="sxs-lookup"><span data-stu-id="49773-115">We also describe how to convert a multi-step recovery to a single-click recovery action.</span></span>

## <a name="customize-the-recovery-plan"></a><span data-ttu-id="49773-116">Personalización de planes de recuperación</span><span class="sxs-lookup"><span data-stu-id="49773-116">Customize the recovery plan</span></span>
1. <span data-ttu-id="49773-117">Vaya a la hoja de recursos de planes de recuperación de **Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="49773-117">Go to the **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="49773-118">En este ejemplo, el plan de recuperación tiene agregadas dos máquinas virtuales para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-118">For this example, the recovery plan has two VMs added to it, for recovery.</span></span> <span data-ttu-id="49773-119">Para empezar a agregar un runbook, haga clic en la pestaña **Personalizar**.</span><span class="sxs-lookup"><span data-stu-id="49773-119">To begin adding a runbook, click the **Customize** tab.</span></span>

    ![Clic en la pestaña Personalizar](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="49773-121">Haga clic con el botón derecho en **Grupo 1: Iniciar** y luego seleccione **Agregar acción posterior**.</span><span class="sxs-lookup"><span data-stu-id="49773-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Clic con el botón derecho en Grupo 1: Iniciar y adición de acción posterior](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="49773-123">Haga clic en **Elegir un script**.</span><span class="sxs-lookup"><span data-stu-id="49773-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="49773-124">En la hoja **Actualizar acción**, ponga el nombre **Hello World** al script.</span><span class="sxs-lookup"><span data-stu-id="49773-124">On the **Update action** blade, name the script **Hello World**.</span></span>

    ![Hoja Actualizar acción](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="49773-126">Escriba un nombre de cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="49773-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="49773-127">La cuenta de Automation puede estar en cualquier región de Azure.</span><span class="sxs-lookup"><span data-stu-id="49773-127">The Automation account can be in any Azure region.</span></span> <span data-ttu-id="49773-128">La cuenta de Automation debe estar en la misma suscripción que el almacén de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="49773-128">The Automation account must be in the same subscription as the Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="49773-129">En la cuenta de Automation, seleccione un runbook.</span><span class="sxs-lookup"><span data-stu-id="49773-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="49773-130">Este runbook es el script que se ejecuta durante la ejecución del plan de recuperación, después de la recuperación del primer grupo.</span><span class="sxs-lookup"><span data-stu-id="49773-130">This runbook is the script that runs during the execution of the recovery plan, after the recovery of the first group.</span></span>

7. <span data-ttu-id="49773-131">Para guardar el script, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="49773-131">To save the script, click **OK**.</span></span> <span data-ttu-id="49773-132">El script se agrega a **Grupo 1: Pasos posteriores**.</span><span class="sxs-lookup"><span data-stu-id="49773-132">The script is added to **Group 1: Post-steps**.</span></span>

    ![Acción posterior Grupo 1: Iniciar](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="49773-134">Consideraciones para agregar un script</span><span class="sxs-lookup"><span data-stu-id="49773-134">Considerations for adding a script</span></span>

* <span data-ttu-id="49773-135">Para obtener opciones para **eliminar un paso** o **actualizar el script**, haga clic con el botón derecho en el script.</span><span class="sxs-lookup"><span data-stu-id="49773-135">For options to **delete a step** or **update the script**, right-click the script.</span></span>
* <span data-ttu-id="49773-136">Un script se puede ejecutar en Azure durante la conmutación por error desde un equipo local en Azure.</span><span class="sxs-lookup"><span data-stu-id="49773-136">A script can run on Azure during failover from an on-premises machine to Azure.</span></span> <span data-ttu-id="49773-137">También puede ejecutarse en Azure como un script de sitio principal antes de apagar, durante la conmutación por recuperación desde Azure en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="49773-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure to an on-premises machine.</span></span>
* <span data-ttu-id="49773-138">Cuando se ejecuta un script, inserta un contexto del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="49773-139">El ejemplo siguiente muestra una variable de contexto:</span><span class="sxs-lookup"><span data-stu-id="49773-139">The following example shows a context variable:</span></span>

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

    <span data-ttu-id="49773-140">La tabla siguiente indica el nombre y la descripción de cada una de las variables del contexto.</span><span class="sxs-lookup"><span data-stu-id="49773-140">The following table lists the name and description of each variable in the context.</span></span>

    | <span data-ttu-id="49773-141">**Nombre de la variable**</span><span class="sxs-lookup"><span data-stu-id="49773-141">**Variable name**</span></span> | <span data-ttu-id="49773-142">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="49773-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="49773-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="49773-143">RecoveryPlanName</span></span> |<span data-ttu-id="49773-144">Nombre del plan que se va a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="49773-144">The name of the plan being run.</span></span> <span data-ttu-id="49773-145">Esta variable le ayuda a realizar diferentes acciones según el nombre del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-145">This variable helps you take different actions based on the recovery plan name.</span></span> <span data-ttu-id="49773-146">También puede volver a usar el script.</span><span class="sxs-lookup"><span data-stu-id="49773-146">You also can reuse the script.</span></span> |
    | <span data-ttu-id="49773-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="49773-147">FailoverType</span></span> |<span data-ttu-id="49773-148">Especifica si la conmutación por error es una prueba, planeada o no.</span><span class="sxs-lookup"><span data-stu-id="49773-148">Specifies whether the failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="49773-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="49773-149">FailoverDirection</span></span> |<span data-ttu-id="49773-150">Especifica si la recuperación es en un sitio principal o secundario.</span><span class="sxs-lookup"><span data-stu-id="49773-150">Specifies whether recovery is to a primary or secondary site.</span></span> |
    | <span data-ttu-id="49773-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="49773-151">GroupID</span></span> |<span data-ttu-id="49773-152">Identifica el número de grupo del plan de recuperación cuando este se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="49773-152">Identifies the group number in the recovery plan when the plan is running.</span></span> |
    | <span data-ttu-id="49773-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="49773-153">VmMap</span></span> |<span data-ttu-id="49773-154">Matriz de todas las máquinas virtuales del grupo.</span><span class="sxs-lookup"><span data-stu-id="49773-154">An array of all VMs in the group.</span></span> |
    | <span data-ttu-id="49773-155">Clave de VMMap</span><span class="sxs-lookup"><span data-stu-id="49773-155">VMMap key</span></span> |<span data-ttu-id="49773-156">Clave única (GUID) para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49773-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="49773-157">Es igual que el identificador de Azure Virtual Machine Manager (VMM) de la máquina virtual, si procede.</span><span class="sxs-lookup"><span data-stu-id="49773-157">It's the same as the Azure Virtual Machine Manager (VMM) ID of the VM, where applicable.</span></span> |
    | <span data-ttu-id="49773-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="49773-158">SubscriptionId</span></span> |<span data-ttu-id="49773-159">Identificador de la suscripción de Azure en la que se ha creado la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49773-159">The Azure subscription ID in which the VM was created.</span></span> |
    | <span data-ttu-id="49773-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="49773-160">RoleName</span></span> |<span data-ttu-id="49773-161">Nombre de la máquina virtual de Azure que se está recuperando.</span><span class="sxs-lookup"><span data-stu-id="49773-161">The name of the Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="49773-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="49773-162">CloudServiceName</span></span> |<span data-ttu-id="49773-163">Nombre del servicio en la nube de Azure en el que se ha creado la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49773-163">The Azure cloud service name under which the VM was created.</span></span> |
    | <span data-ttu-id="49773-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="49773-164">ResourceGroupName</span></span>|<span data-ttu-id="49773-165">Nombre del grupo de recursos de Azure en el que se ha creado la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49773-165">The Azure resource group name under which the VM was created.</span></span> |
    | <span data-ttu-id="49773-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="49773-166">RecoveryPointId</span></span>|<span data-ttu-id="49773-167">Marca de tiempo de cuando se recupera la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49773-167">The timestamp for when the VM is recovered.</span></span> |

* <span data-ttu-id="49773-168">Asegúrese de que la cuenta de Automation tenga los siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="49773-168">Ensure that the Automation account has the following modules:</span></span>
    * <span data-ttu-id="49773-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="49773-169">AzureRM.profile</span></span>
    * <span data-ttu-id="49773-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="49773-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="49773-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="49773-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="49773-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="49773-172">AzureRM.Network</span></span>
    * <span data-ttu-id="49773-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="49773-173">AzureRM.Compute</span></span>

<span data-ttu-id="49773-174">Todos los módulos deben ser de versiones compatibles.</span><span class="sxs-lookup"><span data-stu-id="49773-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="49773-175">Una manera sencilla de garantizar que todos los módulos sean compatibles es usar las versiones más recientes de todos los módulos.</span><span class="sxs-lookup"><span data-stu-id="49773-175">An easy way to ensure that all modules are compatible is to use the latest versions of all the modules.</span></span>

### <a name="access-all-vms-of-the-vmmap-in-a-loop"></a><span data-ttu-id="49773-176">Acceso a todas las máquinas virtuales de VMMap en un bucle</span><span class="sxs-lookup"><span data-stu-id="49773-176">Access all VMs of the VMMap in a loop</span></span>
<span data-ttu-id="49773-177">Use el siguiente código para crear un bucle con todas las máquinas virtuales de Microsoft VMMap:</span><span class="sxs-lookup"><span data-stu-id="49773-177">Use the following code to loop across all VMs of the Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is to ensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="49773-178">Los valores de nombre de grupo de recursos y nombre de rol están vacíos cuando el script es una acción anterior a un grupo de arranque.</span><span class="sxs-lookup"><span data-stu-id="49773-178">The resource group name and role name values are empty when the script is a pre-action to a boot group.</span></span> <span data-ttu-id="49773-179">Los valores se rellenan solo si se realiza correctamente la conmutación por error de la máquina virtual de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="49773-179">The values are populated only if the VM of that group succeeds in failover.</span></span> <span data-ttu-id="49773-180">El script es una acción posterior del grupo de arranque.</span><span class="sxs-lookup"><span data-stu-id="49773-180">The script is a post-action of the boot group.</span></span>

## <a name="use-the-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="49773-181">Uso del mismo runbook de Automation en varios planes de recuperación</span><span class="sxs-lookup"><span data-stu-id="49773-181">Use the same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="49773-182">Puede usar un solo script en varios planes de recuperación gracias a las variables externas.</span><span class="sxs-lookup"><span data-stu-id="49773-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="49773-183">Las [variables de Azure Automation](../automation/automation-variables.md) se pueden usar para almacenar los parámetros que se pueden pasar para la ejecución de un plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-183">You can use [Azure Automation variables](../automation/automation-variables.md) to store parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="49773-184">Al agregar el nombre del plan de recuperación como prefijo a la variable, puede crear variables individuales para cada plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-184">By adding the recovery plan name as a prefix to the variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="49773-185">Luego, use las variables como parámetros.</span><span class="sxs-lookup"><span data-stu-id="49773-185">Then, use the variables as parameters.</span></span> <span data-ttu-id="49773-186">Puede cambiar un parámetro sin cambiar el script y aun así cambiar la forma en que el script funciona.</span><span class="sxs-lookup"><span data-stu-id="49773-186">You can change a parameter without changing the script, but still change the way the script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="49773-187">Uso de una variable de cadena simple en un script de runbook</span><span class="sxs-lookup"><span data-stu-id="49773-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="49773-188">En este ejemplo, un script toma la entrada de un grupo de seguridad de red (NSG) y la aplica a las máquinas virtuales de un plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-188">In this example, a script takes the input of a Network Security Group (NSG) and applies it to the VMs of a recovery plan.</span></span>

<span data-ttu-id="49773-189">Para que el script detecte qué plan de recuperación se está ejecutando, use el contexto del plan de recuperación:</span><span class="sxs-lookup"><span data-stu-id="49773-189">For the script to detect which recovery plan is running, use the recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="49773-190">Para aplicar un NSG existente, debe conocer el nombre del NSG y el nombre del grupo de recursos del NSG.</span><span class="sxs-lookup"><span data-stu-id="49773-190">To apply an existing NSG, you must know the NSG name and the NSG resource group name.</span></span> <span data-ttu-id="49773-191">Use estas variables como entradas para los scripts del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="49773-192">Para ello, cree dos variables en los activos de la cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="49773-192">To do this, create two variables in the Automation account assets.</span></span> <span data-ttu-id="49773-193">Agregue el nombre del plan de recuperación para el que va a crear los parámetros como prefijo al nombre de la variable.</span><span class="sxs-lookup"><span data-stu-id="49773-193">Add the name of the recovery plan that you are creating the parameters for as a prefix to the variable name.</span></span>

1. <span data-ttu-id="49773-194">Cree una variable para almacenar el nombre del NSG.</span><span class="sxs-lookup"><span data-stu-id="49773-194">Create a variable to store the NSG name.</span></span> <span data-ttu-id="49773-195">Agregue un prefijo al nombre de la variable mediante el nombre del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-195">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Creación de una variable de nombre de NSG](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="49773-197">Cree una variable para almacenar el nombre del grupo de recursos del NSG.</span><span class="sxs-lookup"><span data-stu-id="49773-197">Create a variable to store the NSG's resource group name.</span></span> <span data-ttu-id="49773-198">Agregue un prefijo al nombre de la variable mediante el nombre del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-198">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Creación de un nombre de grupo de recursos de NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="49773-200">En el script, use el siguiente código de referencia para obtener los valores de variable:</span><span class="sxs-lookup"><span data-stu-id="49773-200">In the script, use the following reference code to get the variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="49773-201">Use las variables del runbook para aplicar el NSG a la interfaz de red de la máquina virtual conmutada por error:</span><span class="sxs-lookup"><span data-stu-id="49773-201">Use the variables in the runbook to apply the NSG to the network interface of the failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply the NSG to a network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="49773-202">Para cada plan de recuperación, cree variables independientes para poder volver a usar el script.</span><span class="sxs-lookup"><span data-stu-id="49773-202">For each recovery plan, create independent variables so that you can reuse the script.</span></span> <span data-ttu-id="49773-203">Agregue un prefijo mediante el nombre del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-203">Add a prefix by using the recovery plan name.</span></span> <span data-ttu-id="49773-204">Para obtener un script completo de un extremo a otro para este escenario, vea [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan (Agregar una dirección IP pública y un NSG a las máquinas virtuales durante la conmutación por error de prueba de un plan de recuperación de Site Recovery)](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="49773-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-to-store-more-information"></a><span data-ttu-id="49773-205">Uso de una variable compleja para almacenar más información</span><span class="sxs-lookup"><span data-stu-id="49773-205">Use a complex variable to store more information</span></span>

<span data-ttu-id="49773-206">Considere un escenario en el que quiera que un único script active una dirección IP pública en máquinas virtuales concretas.</span><span class="sxs-lookup"><span data-stu-id="49773-206">Consider a scenario in which you want a single script to turn on a public IP on specific VMs.</span></span> <span data-ttu-id="49773-207">En otro escenario, podría querer aplicar diferentes NSG en diferentes máquinas virtuales (no en todas las máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="49773-207">In another scenario, you might want to apply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="49773-208">Puede crear un script que se pueda volver a usar para cualquier plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="49773-209">Cada plan de recuperación puede tener un número variable de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="49773-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="49773-210">Por ejemplo, una recuperación de SharePoint tiene dos servidores front-end.</span><span class="sxs-lookup"><span data-stu-id="49773-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="49773-211">Una aplicación básica de línea de negocio (LOB) tiene solo un servidor front-end.</span><span class="sxs-lookup"><span data-stu-id="49773-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="49773-212">No puede crear variables independientes para cada plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="49773-213">En el siguiente ejemplo se usa una técnica nueva y se crea una [variable compleja](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) en los activos de la cuenta de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="49773-213">In the following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in the Azure Automation account assets.</span></span> <span data-ttu-id="49773-214">Para ello se especifican varios valores.</span><span class="sxs-lookup"><span data-stu-id="49773-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="49773-215">Debe usar Azure PowerShell para realizar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="49773-215">You must use Azure PowerShell to complete the following steps:</span></span>

1. <span data-ttu-id="49773-216">En PowerShell, inicie sesión en la suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="49773-216">In PowerShell, sign in to your Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="49773-217">Para almacenar los parámetros, cree la variable compleja mediante el plan de recuperación:</span><span class="sxs-lookup"><span data-stu-id="49773-217">To store the parameters, create the complex variable by using the name of the recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="49773-218">En esta variable compleja, **VMDetails** es el identificador de la máquina virtual protegida.</span><span class="sxs-lookup"><span data-stu-id="49773-218">In this complex variable, **VMDetails** is the VM ID for the protected VM.</span></span> <span data-ttu-id="49773-219">Para obtener el identificador de la máquina virtual, en Azure Portal, vea las propiedades de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="49773-219">To get the VM ID, in the Azure portal, view the VM properties.</span></span> <span data-ttu-id="49773-220">En la captura de pantalla siguiente se muestra una variable que almacena los detalles de dos máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="49773-220">The following screenshot shows a variable that stores the details of two VMs:</span></span>

    ![Empleo del identificador de la máquina virtual como GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="49773-222">Use esta variable en el runbook.</span><span class="sxs-lookup"><span data-stu-id="49773-222">Use this variable in your runbook.</span></span> <span data-ttu-id="49773-223">Si el GUID indicado de la máquina virtual se encuentra en el contexto del plan de recuperación, aplique el NSG en la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="49773-223">If the indicated VM GUID is found in the recovery plan context, apply the NSG on the VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="49773-224">En el runbook, cree un bucle con las máquinas virtuales del contexto del plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-224">In your runbook, loop through the VMs of the recovery plan context.</span></span> <span data-ttu-id="49773-225">Compruebe si la máquina virtual existe en **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="49773-225">Check whether the VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="49773-226">En caso afirmativo, acceda a las propiedades de la variable para aplicar el NSG:</span><span class="sxs-lookup"><span data-stu-id="49773-226">If it exists, access the properties of the variable to apply the NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If the VM exists in the context, this will not b Null
                $VM = $vmMap.$VMID
                # Access the properties of the variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code to apply the NSG properties to the VM
            }
        }
    ```

<span data-ttu-id="49773-227">Puede usar el mismo script para distintos planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="49773-227">You can use the same script for different recovery plans.</span></span> <span data-ttu-id="49773-228">Escriba distintos parámetros al almacenar el valor que corresponde a un plan de recuperación en variables diferentes.</span><span class="sxs-lookup"><span data-stu-id="49773-228">Enter different parameters by storing the value that corresponds to a recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="49773-229">Scripts de ejemplo</span><span class="sxs-lookup"><span data-stu-id="49773-229">Sample scripts</span></span>

<span data-ttu-id="49773-230">Para implementar scripts de ejemplo en la cuenta de Automation, haga clic en el botón **Implementar en Azure**.</span><span class="sxs-lookup"><span data-stu-id="49773-230">To deploy sample scripts to your Automation account, click the **Deploy to Azure** button.</span></span>

<span data-ttu-id="49773-231">[![Implementación en Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="49773-231">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="49773-232">Para obtener otro ejemplo, vea el siguiente vídeo.</span><span class="sxs-lookup"><span data-stu-id="49773-232">For another example, see the following video.</span></span> <span data-ttu-id="49773-233">En él se muestra cómo recuperar una aplicación de WordPress de dos niveles en Azure:</span><span class="sxs-lookup"><span data-stu-id="49773-233">It demonstrates how to recover a two-tier WordPress application to Azure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="49773-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="49773-234">Additional resources</span></span>
* [<span data-ttu-id="49773-235">Cuenta de ejecución del servicio Azure Automation</span><span class="sxs-lookup"><span data-stu-id="49773-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="49773-236">Información general sobre Azure Automation</span><span class="sxs-lookup"><span data-stu-id="49773-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Información general sobre Azure Automation")
* [<span data-ttu-id="49773-237">Scripts de ejemplo de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="49773-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Scripts de ejemplo de Azure Automation")
