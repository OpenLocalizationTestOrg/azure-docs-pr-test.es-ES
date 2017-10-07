---
title: "estado de máquina virtual de Azure de etiquetas con formato JSON tooschedule aaaUse | Documentos de Microsoft"
description: "Este artículo demuestra cómo toouse JSON cadenas en la programación de hello tooautomate de etiquetas de cierre e inicio de máquina virtual."
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
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="bcf93-103">Escenario de automatización de Azure: usar con formato JSON etiquetas toocreate una programación para la máquina virtual de Azure inicio y apagado</span><span class="sxs-lookup"><span data-stu-id="bcf93-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="bcf93-104">A menudo, los clientes desean tooschedule inicio de Hola y cierre de las máquinas virtuales toohelp reducir los costos de suscripción o admitir requisitos empresariales y técnicos.</span><span class="sxs-lookup"><span data-stu-id="bcf93-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="bcf93-105">Hello siguiente escenario permite tooset seguridad automatizada inicio y cierre de las máquinas virtuales mediante el uso de una etiqueta denominada programación con un nivel de máquina virtual en Azure o el nivel de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bcf93-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="bcf93-106">Esta programación puede configurarse en domingo tooSaturday con un tiempo de inicio y la hora de cierre.</span><span class="sxs-lookup"><span data-stu-id="bcf93-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="bcf93-107">Tenemos algunas opciones disponibles de forma inmediata.</span><span class="sxs-lookup"><span data-stu-id="bcf93-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="bcf93-108">Entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="bcf93-108">These include:</span></span>

* <span data-ttu-id="bcf93-109">[Conjuntos de escalas de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) con valores de escalado automático que le permiten tooscale o alejar.</span><span class="sxs-lookup"><span data-stu-id="bcf93-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="bcf93-110">[Laboratorios de desarrollo y pruebas](../devtest-lab/devtest-lab-overview.md) servicio, que ofrece la capacidad integrada de Hola de programación de operaciones de inicio y cierre.</span><span class="sxs-lookup"><span data-stu-id="bcf93-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="bcf93-111">Sin embargo, estas opciones solo admiten escenarios específicos y no puede ser aplicada tooinfrastructure como-servicio (IaaS) las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bcf93-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="bcf93-112">Una vez Hola etiqueta programación aplicada tooa grupo de recursos, también es tooall aplicado las máquinas virtuales dentro de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bcf93-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="bcf93-113">Si una programación también está directamente aplicado tooa VM, última programación de hello tiene prioridad en hello siguiendo el orden:</span><span class="sxs-lookup"><span data-stu-id="bcf93-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="bcf93-114">Grupo de recursos de programación tooa aplicado</span><span class="sxs-lookup"><span data-stu-id="bcf93-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="bcf93-115">Programar el grupo de recursos de tooa aplicados y máquina virtual en el grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="bcf93-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="bcf93-116">Máquina virtual de programación aplica tooa</span><span class="sxs-lookup"><span data-stu-id="bcf93-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="bcf93-117">Este escenario básicamente toma una cadena JSON con un formato especificado y lo agrega como valor de Hola para una etiqueta denominada programación.</span><span class="sxs-lookup"><span data-stu-id="bcf93-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="bcf93-118">A continuación, un runbook enumera todos los grupos de recursos y máquinas virtuales e identifica programaciones de Hola para cada máquina virtual basándose en los escenarios de hello enumerados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bcf93-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="bcf93-119">A continuación recorre en bucle hello las máquinas virtuales que tienen programaciones que se adjunta y se evalúa como la acción que debe realizarse.</span><span class="sxs-lookup"><span data-stu-id="bcf93-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="bcf93-120">Por ejemplo, determina que las máquinas virtuales necesitan toobe detener, apagar o tenga en cuenta.</span><span class="sxs-lookup"><span data-stu-id="bcf93-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="bcf93-121">Estos runbooks autenticar mediante hello [cuenta de identificación de Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="bcf93-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="bcf93-122">Descargar runbooks de hello para el escenario de Hola</span><span class="sxs-lookup"><span data-stu-id="bcf93-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="bcf93-123">Este escenario consta de cuatro runbooks de flujo de trabajo de PowerShell que puede descargar desde hello [Galería de TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) o hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repositorio para este proyecto.</span><span class="sxs-lookup"><span data-stu-id="bcf93-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="bcf93-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="bcf93-124">Runbook</span></span> | <span data-ttu-id="bcf93-125">Descripción</span><span class="sxs-lookup"><span data-stu-id="bcf93-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bcf93-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="bcf93-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="bcf93-127">Comprueba la programación de cada máquina virtual y realiza inicio según la programación de Hola o cierre.</span><span class="sxs-lookup"><span data-stu-id="bcf93-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="bcf93-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="bcf93-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="bcf93-129">Agrega Hola programación etiqueta tooa VM o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bcf93-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="bcf93-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="bcf93-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="bcf93-131">Modifica la etiqueta de programación de hello existente si se reemplaza por una nueva.</span><span class="sxs-lookup"><span data-stu-id="bcf93-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="bcf93-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="bcf93-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="bcf93-133">Quita la etiqueta de la programación de Hola desde un máquina virtual o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bcf93-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="bcf93-134">Instalación y configuración de este escenario</span><span class="sxs-lookup"><span data-stu-id="bcf93-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="bcf93-135">Instalar y publicar runbooks Hola</span><span class="sxs-lookup"><span data-stu-id="bcf93-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="bcf93-136">Después de descargar runbooks hello, puede importar utilizando el procedimiento de hello en [crear o importar un runbook en automatización de Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="bcf93-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="bcf93-137">Publique cada Runbook después de que se hayan importado correctamente en la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="bcf93-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="bcf93-138">Agregar un runbook de toohello ResourceSchedule de prueba de programación</span><span class="sxs-lookup"><span data-stu-id="bcf93-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="bcf93-139">Siga estos programación de hello tooenable de pasos de runbook de prueba ResourceSchedule Hola.</span><span class="sxs-lookup"><span data-stu-id="bcf93-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="bcf93-140">Se trata de runbook de Hola que comprueba las máquinas virtuales que se debe iniciar, apagar, o dejarlos como están.</span><span class="sxs-lookup"><span data-stu-id="bcf93-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="bcf93-141">De hello portal de Azure, abra su cuenta de automatización y, a continuación, haga clic en hello **Runbooks** icono.</span><span class="sxs-lookup"><span data-stu-id="bcf93-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="bcf93-142">En hello **prueba ResourceSchedule** hoja, haga clic en hello **programaciones** icono.</span><span class="sxs-lookup"><span data-stu-id="bcf93-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="bcf93-143">En hello **programaciones** hoja, haga clic en **agregar una programación**.</span><span class="sxs-lookup"><span data-stu-id="bcf93-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="bcf93-144">En hello **programaciones** hoja, seleccione **vincular un runbook de programación tooyour**.</span><span class="sxs-lookup"><span data-stu-id="bcf93-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="bcf93-145">A continuación, seleccione **Crear una programación nueva**.</span><span class="sxs-lookup"><span data-stu-id="bcf93-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="bcf93-146">En hello **nueva programación** hoja, escriba el nombre de Hola de esta programación, por ejemplo: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="bcf93-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="bcf93-147">Para las programaciones de hello **iniciar**, establezca Hola inicio tiempo tooan hora incremento.</span><span class="sxs-lookup"><span data-stu-id="bcf93-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="bcf93-148">Seleccione **Periodicidad** y, en **Recur every interval** (Repetir cada intervalo), seleccione **1 hora**.</span><span class="sxs-lookup"><span data-stu-id="bcf93-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="bcf93-149">Compruebe que **caducidad del conjunto de** se establece demasiado**No**y, a continuación, haga clic en **crear** toosave al nuevo esquema.</span><span class="sxs-lookup"><span data-stu-id="bcf93-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="bcf93-150">En hello **programación Runbook** hoja de opciones, seleccione **parámetros y parámetros de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="bcf93-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="bcf93-151">Hola prueba ResourceSchedule **parámetros** hoja, escriba el nombre de Hola de su suscripción en hello **SubscriptionName** campo.</span><span class="sxs-lookup"><span data-stu-id="bcf93-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="bcf93-152">Esto es Hola único parámetro necesario para runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="bcf93-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="bcf93-153">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bcf93-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="bcf93-154">programación de runbook de Hello debería parecerse a la siguiente de hello cuando se completan:</span><span class="sxs-lookup"><span data-stu-id="bcf93-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![Runbook Test-ResourceSchedule configurado](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="bcf93-156">Hola formato cadena JSON</span><span class="sxs-lookup"><span data-stu-id="bcf93-156">Format hello JSON string</span></span>
<span data-ttu-id="bcf93-157">Esta solución básicamente toma JSON de cadena con un formato especificado y lo agrega como valor de Hola para una etiqueta llamada Schedule.</span><span class="sxs-lookup"><span data-stu-id="bcf93-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="bcf93-158">A continuación, un runbook enumera todos los grupos de recursos y máquinas virtuales e identifica programaciones de Hola para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bcf93-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="bcf93-159">Hola runbook itera sobre máquinas virtuales de Hola que tienen programaciones asociadas y comprueba qué acciones deben ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="bcf93-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="bcf93-160">Hola te mostramos un ejemplo de cómo se deben dar formato soluciones hello:</span><span class="sxs-lookup"><span data-stu-id="bcf93-160">hello following is an example of how hello solutions should be formatted:</span></span>

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

<span data-ttu-id="bcf93-161">Información detallada sobre esta estructura:</span><span class="sxs-lookup"><span data-stu-id="bcf93-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="bcf93-162">formato de Hola de esta estructura JSON es toowork optimizada de limitación de 256 caracteres de Hola de un valor de etiqueta única en Azure.</span><span class="sxs-lookup"><span data-stu-id="bcf93-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="bcf93-163">*TzId* representa Hola zona horaria de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcf93-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="bcf93-164">Este identificador puede obtenerse mediante la clase TimeZoneInfo .NET de hello en una sesión de PowerShell:**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="bcf93-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones en PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="bcf93-166">Días de la semana se representan con un valor numérico de cero toosix.</span><span class="sxs-lookup"><span data-stu-id="bcf93-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="bcf93-167">Hola valor cero es igual al domingo.</span><span class="sxs-lookup"><span data-stu-id="bcf93-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="bcf93-168">hora de inicio Hello se representa una con hello **S** atributo y su valor está en un formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="bcf93-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="bcf93-169">hora de finalización o apagado Hello se representa una con hello **E** atributo y su valor está en un formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="bcf93-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="bcf93-170">Si hello **S** y **E** atributos tienen un valor de cero (0), la máquina virtual de Hola se quedará en su estado actual en tiempo de Hola de evaluación.</span><span class="sxs-lookup"><span data-stu-id="bcf93-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="bcf93-171">Si desea que la evaluación tooskip para un día concreto de la semana de hello, no agregue una sección para ese día de la semana de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcf93-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="bcf93-172">Hola se evalúa el siguiente ejemplo, solo lunes y hello otros días de la semana de Hola se pasan por alto:</span><span class="sxs-lookup"><span data-stu-id="bcf93-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="bcf93-173">Etiquetado de máquinas virtuales o grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="bcf93-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="bcf93-174">tooshut hacia abajo de las máquinas virtuales, deberá tootag hello las máquinas virtuales o grupos de recursos de hello en el que se encuentren.</span><span class="sxs-lookup"><span data-stu-id="bcf93-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="bcf93-175">No se evalúan las máquinas virtuales que no tienen una etiqueta Schedule.</span><span class="sxs-lookup"><span data-stu-id="bcf93-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="bcf93-176">Por lo tanto, estas no se iniciarán ni apagarán.</span><span class="sxs-lookup"><span data-stu-id="bcf93-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="bcf93-177">Hay dos grupos de recursos de maneras tootag o máquinas virtuales con esta solución.</span><span class="sxs-lookup"><span data-stu-id="bcf93-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="bcf93-178">Puede hacerlo directamente desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcf93-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="bcf93-179">O bien, puede usar Hola agregar ResourceSchedule y ResourceSchedule de actualización, Remove-ResourceSchedule runbooks.</span><span class="sxs-lookup"><span data-stu-id="bcf93-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="bcf93-180">Etiqueta a través del portal de Hola</span><span class="sxs-lookup"><span data-stu-id="bcf93-180">Tag through hello portal</span></span>
<span data-ttu-id="bcf93-181">Siga estos pasos tootag una máquina virtual o el grupo de recursos en el portal de hello:</span><span class="sxs-lookup"><span data-stu-id="bcf93-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="bcf93-182">Aplanar la cadena JSON de Hola y compruebe que no hay espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="bcf93-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="bcf93-183">La cadena JSON debe tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="bcf93-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="bcf93-184">Seleccione hello **etiqueta** icono para una máquina virtual o un recurso de grupo tooapply esta programación.</span><span class="sxs-lookup"><span data-stu-id="bcf93-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![Opción de etiqueta de máquina virtual](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="bcf93-186">Las etiquetas se definen siguiendo un par clave/valor.</span><span class="sxs-lookup"><span data-stu-id="bcf93-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="bcf93-187">Tipo de **programación** en hello **clave** campo y, a continuación, pegue cadena JSON de Hola Hola **valor** campo.</span><span class="sxs-lookup"><span data-stu-id="bcf93-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="bcf93-188">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bcf93-188">Click **Save**.</span></span> <span data-ttu-id="bcf93-189">La nueva etiqueta debería aparecer ahora en la lista de Hola de etiquetas para el recurso.</span><span class="sxs-lookup"><span data-stu-id="bcf93-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![Etiqueta Schedule de máquina virtual](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="bcf93-191">Etiquetado en PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcf93-191">Tag from PowerShell</span></span>
<span data-ttu-id="bcf93-192">Todos los runbooks importados contienen información de ayuda al principio de Hola de script de Hola que describe cómo tooexecute Hola runbooks directamente desde PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcf93-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="bcf93-193">Puede llamar a runbooks de agregar ScheduleResource y ScheduleResource de actualización de Hola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcf93-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="bcf93-194">Para ello, pasando los parámetros necesarios que le permiten etiqueta de programación de hello toocreate o update en un máquina virtual o grupo de recursos fuera de portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcf93-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="bcf93-195">toocreate, agregar y eliminar etiquetas a través de PowerShell, primero debe demasiado[configurar el entorno de PowerShell para Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bcf93-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="bcf93-196">Después de completar el programa de instalación de hello, puede continuar con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="bcf93-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="bcf93-197">Creación de una etiqueta Schedule con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcf93-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="bcf93-198">Abra una sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcf93-198">Open a PowerShell session.</span></span> <span data-ttu-id="bcf93-199">A continuación, usar hello después tooauthenticate de ejemplo con su cuenta de ejecución y toospecify una suscripción:</span><span class="sxs-lookup"><span data-stu-id="bcf93-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="bcf93-200">Defina una tabla hash de programación.</span><span class="sxs-lookup"><span data-stu-id="bcf93-200">Define a schedule hash table.</span></span> <span data-ttu-id="bcf93-201">Este es un ejemplo de cómo debe estar conformada:</span><span class="sxs-lookup"><span data-stu-id="bcf93-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="bcf93-202">Definir parámetros de Hola que requieren Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="bcf93-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="bcf93-203">En el siguiente ejemplo de Hola que estamos usando como objetivo una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="bcf93-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="bcf93-204">Si está etiquetado de un grupo de recursos, quite hello *VMName* parámetro de hash de hello $params tabla como sigue:</span><span class="sxs-lookup"><span data-stu-id="bcf93-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="bcf93-205">Ejecute hello ResourceSchedule agregar runbook con hello sigue parámetros toocreate Hola programación etiqueta:</span><span class="sxs-lookup"><span data-stu-id="bcf93-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="bcf93-206">tooupdate una etiqueta de máquina virtual o el grupo de recursos, ejecute hello **ResourceSchedule actualización** runbook con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="bcf93-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="bcf93-207">Eliminación de una etiqueta Schedule con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcf93-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="bcf93-208">Abra una sesión de PowerShell y ejecute hello después tooauthenticate con su cuenta de ejecución y tooselect y especifique una suscripción:</span><span class="sxs-lookup"><span data-stu-id="bcf93-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="bcf93-209">Definir parámetros de Hola que requieren Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="bcf93-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="bcf93-210">En el siguiente ejemplo de Hola que estamos usando como objetivo una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="bcf93-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="bcf93-211">Si elimina una etiqueta de un grupo de recursos, quitar hello *VMName* parámetro de hash de hello $params tabla como sigue:</span><span class="sxs-lookup"><span data-stu-id="bcf93-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="bcf93-212">Execute (etiqueta) Hola Remove-ResourceSchedule runbook tooremove Hola programación:</span><span class="sxs-lookup"><span data-stu-id="bcf93-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="bcf93-213">tooupdate una etiqueta de máquina virtual o el grupo de recursos, ejecute hello Remove-ResourceSchedule runbook con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="bcf93-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="bcf93-214">Se recomienda que supervise proactivamente Estos runbooks (y los Estados de máquina virtual de hello) tooverify que las máquinas virtuales que se apague y se inicia en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="bcf93-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="bcf93-215">detalles de hello tooview de hello ResourceSchedule prueba runbook trabajo Hola portal de Azure, seleccione hello **trabajos** icono de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcf93-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="bcf93-216">parámetros de entrada de Hello trabajo proporciona resúmenes hello y salida de hello streaming, además toogeneral información sobre el trabajo de Hola y las excepciones que se hayan producido.</span><span class="sxs-lookup"><span data-stu-id="bcf93-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="bcf93-217">Hola **resumen del trabajo** incluye mensajes de secuencias de salida, advertencia y error de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcf93-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="bcf93-218">Seleccione hello **salida** icono tooview resultados de ejecución de un runbook Hola detallados.</span><span class="sxs-lookup"><span data-stu-id="bcf93-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Salida de Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="bcf93-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bcf93-220">Next steps</span></span>
* <span data-ttu-id="bcf93-221">tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="bcf93-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="bcf93-222">toolearn más información acerca de los tipos de runbook y sus ventajas y limitaciones, consulte [tipos de runbook de automatización de Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="bcf93-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="bcf93-223">Para más información sobre las características de compatibilidad con scripts de PowerShell, consulte [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)(Anuncio de la compatibilidad nativa con scripts de PowerShell en Automatización de Azure).</span><span class="sxs-lookup"><span data-stu-id="bcf93-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="bcf93-224">toolearn más información sobre el registro de runbook y salida, vea [Runbook salida y mensajes en automatización de Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="bcf93-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="bcf93-225">más información acerca de una cuenta de identificación de Azure y cómo tooauthenticate sus runbooks mediante el uso de, consulte toolearn [autenticar runbooks con Azure cuenta de ejecución](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="bcf93-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
