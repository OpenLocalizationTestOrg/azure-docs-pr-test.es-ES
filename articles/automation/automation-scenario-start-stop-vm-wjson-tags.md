---
title: "Uso de etiquetas con formato JSON para programar el estado de la máquina virtual de Azure | Microsoft Docs"
description: "En este artículo se explica cómo usar cadenas JSON en las etiquetas para automatizar la programación de inicio y apagado de máquinas virtuales."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f8d9563318c3afe299cebb7c889874392f114f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="8c47b-103">Escenario de Automatización de Azure: uso de etiquetas con formato JSON para crear una programación de inicio y apagado de VM de Azure</span><span class="sxs-lookup"><span data-stu-id="8c47b-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="8c47b-104">Normalmente, los clientes quieren programar el inicio y apagado de las máquinas virtuales para reducir los costos de suscripción o dar cabida a requisitos empresariales y técnicos.</span><span class="sxs-lookup"><span data-stu-id="8c47b-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="8c47b-105">El siguiente escenario le permite configurar el inicio y apagado automatizados de máquinas virtuales por medio de una etiqueta denominada Schedule en un nivel de grupo de recursos o de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c47b-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="8c47b-106">Esta programación se puede configurar de domingo a sábado con una hora de inicio y una hora de apagado.</span><span class="sxs-lookup"><span data-stu-id="8c47b-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="8c47b-107">Tenemos algunas opciones disponibles de forma inmediata.</span><span class="sxs-lookup"><span data-stu-id="8c47b-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="8c47b-108">Entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="8c47b-108">These include:</span></span>

* <span data-ttu-id="8c47b-109">[Conjuntos de escalado de máquinas virtuales](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) con una configuración de escalado automático que le permite escalar o reducir horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="8c47b-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="8c47b-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) , que tiene una funcionalidad integrada para programar las operaciones de inicio y apagado.</span><span class="sxs-lookup"><span data-stu-id="8c47b-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="8c47b-111">Sin embargo, estas opciones solo admiten escenarios específicos y no se pueden aplicar a las máquinas virtuales de infraestructura como servicio (IaaS).</span><span class="sxs-lookup"><span data-stu-id="8c47b-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="8c47b-112">Cuando la etiqueta Schedule se aplica a un grupo de recursos, se aplica también a todas las máquinas virtuales dentro de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8c47b-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="8c47b-113">Si también se aplica una programación directamente a una máquina virtual, tiene prioridad la última programación en el siguiente orden:</span><span class="sxs-lookup"><span data-stu-id="8c47b-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="8c47b-114">Programación aplicada a un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8c47b-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="8c47b-115">Programación aplicada a un grupo de recursos y a una máquina virtual en el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8c47b-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="8c47b-116">Programación aplicada a una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8c47b-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="8c47b-117">En este escenario, lo que ocurre básicamente es que se toma una cadena JSON con un formato especificado y se agrega como el valor de una etiqueta denominada Schedule.</span><span class="sxs-lookup"><span data-stu-id="8c47b-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="8c47b-118">Posteriormente, un Runbook muestra todos los grupos de recursos y máquinas virtuales e identifica las programaciones para cada máquina virtual según los escenarios mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8c47b-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="8c47b-119">A continuación, recorre las máquinas virtuales que tienen programaciones adjuntas y evalúa qué acciones deben realizarse.</span><span class="sxs-lookup"><span data-stu-id="8c47b-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="8c47b-120">Por ejemplo, determina qué máquinas virtuales necesitan detenerse, apagarse o ignorarse.</span><span class="sxs-lookup"><span data-stu-id="8c47b-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="8c47b-121">Estos runbooks se autentican mediante la [Cuenta de ejecución de Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="8c47b-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="8c47b-122">Descarga de los Runbooks para el escenario</span><span class="sxs-lookup"><span data-stu-id="8c47b-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="8c47b-123">Este escenario consta de cuatro Runbooks de flujo de trabajo de PowerShell que puede descargar de la [Galería de TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) o del repositorio [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) relativo a este proyecto.</span><span class="sxs-lookup"><span data-stu-id="8c47b-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="8c47b-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="8c47b-124">Runbook</span></span> | <span data-ttu-id="8c47b-125">Descripción</span><span class="sxs-lookup"><span data-stu-id="8c47b-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c47b-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8c47b-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="8c47b-127">Comprueba la programación de cada máquina virtual y realiza el apagado o inicio de estas según la programación.</span><span class="sxs-lookup"><span data-stu-id="8c47b-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="8c47b-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8c47b-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="8c47b-129">Agrega la etiqueta Schedule a una máquina virtual o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8c47b-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="8c47b-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8c47b-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="8c47b-131">Modifica la etiqueta Schedule existente reemplazándola por una nueva.</span><span class="sxs-lookup"><span data-stu-id="8c47b-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="8c47b-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8c47b-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="8c47b-133">Quita la etiqueta Schedule de una máquina virtual o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8c47b-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="8c47b-134">Instalación y configuración de este escenario</span><span class="sxs-lookup"><span data-stu-id="8c47b-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="8c47b-135">Instalar y publicar los Runbooks</span><span class="sxs-lookup"><span data-stu-id="8c47b-135">Install and publish the runbooks</span></span>
<span data-ttu-id="8c47b-136">Después de descargar los Runbooks, puede importarlos mediante el procedimiento descrito en [Creación o importación de un runbook en Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="8c47b-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="8c47b-137">Publique cada Runbook después de que se hayan importado correctamente en la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="8c47b-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="8c47b-138">Incorporación de una programación al Runbook Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8c47b-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="8c47b-139">Haga lo siguiente para habilitar la programación en el Runbook Test-ResourceSchedule.</span><span class="sxs-lookup"><span data-stu-id="8c47b-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="8c47b-140">Este es el Runbook que comprueba las máquinas virtuales que debe iniciar, apagar o quedar como están.</span><span class="sxs-lookup"><span data-stu-id="8c47b-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="8c47b-141">Desde el Portal de Azure, abra la cuenta de Automatización y haga clic en el icono **Runbooks** .</span><span class="sxs-lookup"><span data-stu-id="8c47b-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="8c47b-142">En la hoja de **Test-ResourceSchedule**, haga clic en el icono **Programaciones**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="8c47b-143">En la hoja **Programaciones**, haga clic en **Agregar una programación**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="8c47b-144">En la hoja **Programaciones**, seleccione **Vincular una programación a su Runbook**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="8c47b-145">A continuación, seleccione **Crear una programación nueva**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="8c47b-146">En la hoja **Nueva programación** , escriba el nombre de esta programación, por ejemplo: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="8c47b-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="8c47b-147">Para la programación **Inicio**, establezca la hora de inicio en un incremento de hora.</span><span class="sxs-lookup"><span data-stu-id="8c47b-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="8c47b-148">Seleccione **Periodicidad** y, en **Recur every interval** (Repetir cada intervalo), seleccione **1 hora**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="8c47b-149">Compruebe que **Configurar expiración** está establecido en **No** y, después, haga clic en **Crear** para guardar la nueva programación.</span><span class="sxs-lookup"><span data-stu-id="8c47b-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="8c47b-150">En hoja de opciones **Programar Runbook**, seleccione **Configuración de ejecución y parámetros**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="8c47b-151">En la hoja **Parámetros** de Test-ResourceSchedule, escriba el nombre de la suscripción en el campo **SubscriptionName**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="8c47b-152">Este es el único parámetro necesario para el Runbook.</span><span class="sxs-lookup"><span data-stu-id="8c47b-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="8c47b-153">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="8c47b-154">La programación del Runbook debe parecerse a lo siguiente cuando se complete:</span><span class="sxs-lookup"><span data-stu-id="8c47b-154">The runbook schedule should look like the following when it's completed:</span></span>

![Runbook Test-ResourceSchedule configurado](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="8c47b-156">Formato de la cadena JSON</span><span class="sxs-lookup"><span data-stu-id="8c47b-156">Format the JSON string</span></span>
<span data-ttu-id="8c47b-157">Esta solución básicamente toma una cadena JSON con un formato especificado y lo agrega como el valor de una etiqueta denominada Schedule.</span><span class="sxs-lookup"><span data-stu-id="8c47b-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="8c47b-158">Posteriormente, un Runbook muestra todos los grupos de recursos y máquinas virtuales e identifica las programaciones para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8c47b-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="8c47b-159">El Runbook recorre las máquinas virtuales que tienen programaciones adjuntas y comprueba qué acciones deben ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="8c47b-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="8c47b-160">Este es un ejemplo de cómo aplicar el formato a las soluciones:</span><span class="sxs-lookup"><span data-stu-id="8c47b-160">The following is an example of how the solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="8c47b-161">Información detallada sobre esta estructura:</span><span class="sxs-lookup"><span data-stu-id="8c47b-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="8c47b-162">El formato de esta estructura JSON está optimizado para evitar la limitación de 256 caracteres de un valor de etiqueta única en Azure.</span><span class="sxs-lookup"><span data-stu-id="8c47b-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="8c47b-163">*TzId* es la zona horaria de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8c47b-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="8c47b-164">Este identificador se puede obtener con la clase .NET. TimeZoneInfo en una sesión de PowerShell: **[System.TimeZoneInfo]::GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones en PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="8c47b-166">Los días de la semana se representan con un valor numérico entre 0 y 6.</span><span class="sxs-lookup"><span data-stu-id="8c47b-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="8c47b-167">El valor 0 corresponde al domingo.</span><span class="sxs-lookup"><span data-stu-id="8c47b-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="8c47b-168">La hora de inicio se representa con el atributo **S** y su valor se presenta en un formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8c47b-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="8c47b-169">La hora de fin o apagado se representa con el atributo **E** y su valor se presenta en un formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8c47b-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="8c47b-170">Si los atributos **S** y **E** tienen un valor de cero (0), la máquina virtual permanecerá en el estado que tenga en el momento de la evaluación.</span><span class="sxs-lookup"><span data-stu-id="8c47b-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="8c47b-171">Si quiere omitir la evaluación para un determinado día de la semana, no agregue la sección del día de la semana en cuestión.</span><span class="sxs-lookup"><span data-stu-id="8c47b-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="8c47b-172">En el siguiente ejemplo solo se evaluará el lunes y se ignorarán los demás días de la semana:</span><span class="sxs-lookup"><span data-stu-id="8c47b-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="8c47b-173">Etiquetado de máquinas virtuales o grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="8c47b-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="8c47b-174">Para apagar las máquinas virtuales, debe etiquetar las máquinas virtuales o los grupos de recursos en los que se encuentran.</span><span class="sxs-lookup"><span data-stu-id="8c47b-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="8c47b-175">No se evalúan las máquinas virtuales que no tienen una etiqueta Schedule.</span><span class="sxs-lookup"><span data-stu-id="8c47b-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="8c47b-176">Por lo tanto, estas no se iniciarán ni apagarán.</span><span class="sxs-lookup"><span data-stu-id="8c47b-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="8c47b-177">Hay dos maneras de etiquetar máquinas virtuales o grupos de recursos con esta solución.</span><span class="sxs-lookup"><span data-stu-id="8c47b-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="8c47b-178">Puede hacerlo directamente desde el portal.</span><span class="sxs-lookup"><span data-stu-id="8c47b-178">You can do it directly from the portal.</span></span> <span data-ttu-id="8c47b-179">O bien, puede usar los Runbooks Add-ResourceSchedule, Update-ResourceSchedule y Remove-ResourceSchedule.</span><span class="sxs-lookup"><span data-stu-id="8c47b-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="8c47b-180">Etiquetado a través del portal</span><span class="sxs-lookup"><span data-stu-id="8c47b-180">Tag through the portal</span></span>
<span data-ttu-id="8c47b-181">Haga lo siguiente para etiquetar una máquina virtual o un grupo de recursos en el portal:</span><span class="sxs-lookup"><span data-stu-id="8c47b-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="8c47b-182">Acople la cadena JSON y compruebe que no hay espacios.</span><span class="sxs-lookup"><span data-stu-id="8c47b-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="8c47b-183">La cadena JSON debe tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="8c47b-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="8c47b-184">Seleccione el icono de **etiqueta** de una máquina virtual o grupo de recursos para aplicarle esta programación.</span><span class="sxs-lookup"><span data-stu-id="8c47b-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![Opción de etiqueta de máquina virtual](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="8c47b-186">Las etiquetas se definen siguiendo un par clave/valor.</span><span class="sxs-lookup"><span data-stu-id="8c47b-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="8c47b-187">Escriba **Schedule** en el campo **Clave** y pegue la cadena JSON en el campo **Valor**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="8c47b-188">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="8c47b-188">Click **Save**.</span></span> <span data-ttu-id="8c47b-189">La nueva etiqueta debería aparecer en la lista de etiquetas del recurso.</span><span class="sxs-lookup"><span data-stu-id="8c47b-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![Etiqueta Schedule de máquina virtual](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="8c47b-191">Etiquetado en PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c47b-191">Tag from PowerShell</span></span>
<span data-ttu-id="8c47b-192">Todos los Runbooks importados contienen información de ayuda al principio del script que describe cómo ejecutar los Runbooks directamente desde PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c47b-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="8c47b-193">Puede llamar a los Runbooks Add-ScheduleResource y Update-ScheduleResource desde PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c47b-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="8c47b-194">Para ello, utilice los parámetros necesarios que le permiten crear o actualizar la etiqueta Schedule en una máquina virtual o grupo de recursos fuera del portal.</span><span class="sxs-lookup"><span data-stu-id="8c47b-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="8c47b-195">Para crear, agregar y eliminar etiquetas a través de PowerShell, primero es preciso [configurar el entorno de PowerShell para Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8c47b-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="8c47b-196">Una vez completada la configuración, puede continuar con los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="8c47b-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="8c47b-197">Creación de una etiqueta Schedule con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c47b-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="8c47b-198">Abra una sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c47b-198">Open a PowerShell session.</span></span> <span data-ttu-id="8c47b-199">A continuación, use lo siguiente para autenticarse con la cuenta de ejecución y especificar una suscripción:</span><span class="sxs-lookup"><span data-stu-id="8c47b-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="8c47b-200">Defina una tabla hash de programación.</span><span class="sxs-lookup"><span data-stu-id="8c47b-200">Define a schedule hash table.</span></span> <span data-ttu-id="8c47b-201">Este es un ejemplo de cómo debe estar conformada:</span><span class="sxs-lookup"><span data-stu-id="8c47b-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="8c47b-202">Defina los parámetros que el Runbook necesita.</span><span class="sxs-lookup"><span data-stu-id="8c47b-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="8c47b-203">En el siguiente ejemplo, el destino es una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="8c47b-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="8c47b-204">Si quiere etiquetar un grupo de recursos, quite el parámetro *VMName* de la tabla hash $params de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="8c47b-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="8c47b-205">Ejecute el Runbook Add-ResourceSchedule con los siguientes parámetros para crear la etiqueta Schedule:</span><span class="sxs-lookup"><span data-stu-id="8c47b-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="8c47b-206">Para actualizar una etiqueta de una máquina virtual o un grupo de recursos, ejecute el Runbook **Update-ResourceSchedule** con los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="8c47b-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="8c47b-207">Eliminación de una etiqueta Schedule con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c47b-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="8c47b-208">Abra una sesión de PowerShell y ejecute lo siguiente para autenticarse con la cuenta de ejecución y seleccionar y especificar una suscripción:</span><span class="sxs-lookup"><span data-stu-id="8c47b-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="8c47b-209">Defina los parámetros que el Runbook necesita.</span><span class="sxs-lookup"><span data-stu-id="8c47b-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="8c47b-210">En el siguiente ejemplo, el destino es una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="8c47b-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="8c47b-211">Si quiere eliminar una etiqueta de un grupo de recursos, simplemente quite el parámetro *VMName* de la tabla hash $params de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="8c47b-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="8c47b-212">Ejecute el Runbook Remove-ResourceSchedule para eliminar la etiqueta Schedule:</span><span class="sxs-lookup"><span data-stu-id="8c47b-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="8c47b-213">Para actualizar una etiqueta de una máquina virtual o un grupo de recursos, ejecute el Runbook Remove-ResourceSchedule con los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="8c47b-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="8c47b-214">Se recomienda supervisar de forma proactiva estos Runbooks (y el estado de las máquinas virtuales) para comprobar que las máquinas virtuales se apagan e inician como es debido.</span><span class="sxs-lookup"><span data-stu-id="8c47b-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="8c47b-215">Para ver los detalles del trabajo del Runbook Test-ResourceSchedule en el Portal de Azure, seleccione el icono **Trabajos** del Runbook.</span><span class="sxs-lookup"><span data-stu-id="8c47b-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="8c47b-216">La opción de resumen del trabajo le mostrará los parámetros de entrada y el flujo de salida, además de información general sobre el trabajo y las excepciones que se hayan producido.</span><span class="sxs-lookup"><span data-stu-id="8c47b-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="8c47b-217">El **resumen del trabajo** incluye los mensajes de los flujos de salida, advertencia y error.</span><span class="sxs-lookup"><span data-stu-id="8c47b-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="8c47b-218">Seleccione el icono **Salida** para ver los resultados detallados de la ejecución del Runbook.</span><span class="sxs-lookup"><span data-stu-id="8c47b-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Salida de Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="8c47b-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c47b-220">Next steps</span></span>
* <span data-ttu-id="8c47b-221">Para empezar a trabajar con Runbooks de flujo de trabajo de PowerShell, consulte [Mi primer Runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="8c47b-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="8c47b-222">Para aprender más sobre los tipos de Runbook, sus ventajas y sus limitaciones, consulte [Tipos de Runbooks de Automatización de Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="8c47b-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="8c47b-223">Para más información sobre las características de compatibilidad con scripts de PowerShell, consulte [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)(Anuncio de la compatibilidad nativa con scripts de PowerShell en Automatización de Azure).</span><span class="sxs-lookup"><span data-stu-id="8c47b-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="8c47b-224">Para más información sobre el registro y salida de Runbooks, vea [Salidas de runbook y mensajes en Automatización de Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="8c47b-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="8c47b-225">Para obtener más información sobre una cuenta de ejecución de Azure y de cómo autenticar sus runbooks mediante ella, consulte [Autenticación de Runbooks con una cuenta de ejecución de Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="8c47b-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
