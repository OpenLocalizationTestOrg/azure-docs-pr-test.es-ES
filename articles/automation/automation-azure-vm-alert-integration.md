---
title: " Corrección de alertas de VM de Azure con runbooks de Automation | Microsoft Docs"
description: "En este artículo se muestra cómo integrar las alertas de la máquina virtual de Azure con runbooks de Automatización de Azure y problemas de corrección automática"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: 738959b8e1ee5da989bb996d1ce8148cbf912781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="8f6a2-103">Escenario de Automatización de Azure: corrección de las alertas de la máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="8f6a2-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="8f6a2-104">Automatización de Azure y Máquinas virtuales de Azure han publicado una nueva característica que permite configurar las alertas de la máquina virtual (VM) para ejecutar runbooks de automatización.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span></span> <span data-ttu-id="8f6a2-105">Esta nueva funcionalidad le permite realizar automáticamente la corrección estándar de alertas de la máquina virtual, como reiniciar o detener la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span></span>

<span data-ttu-id="8f6a2-106">Anteriormente, durante la creación de la regla de alertas de la máquina virtual podía [especificar un Webhook de automatización](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) en un runbook para ejecutar el runbook cada vez que se desencadene la alerta.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span></span> <span data-ttu-id="8f6a2-107">Sin embargo, para esto es necesario que realice el trabajo de creación del runbook, la creación del Webhook para el runbook y, después, la copia y pegado del Webhook durante la creación de la regla de alertas.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span></span> <span data-ttu-id="8f6a2-108">Con esta nueva versión, el proceso es mucho más fácil porque puede elegir directamente un runbook de una lista durante la creación de la regla de alertas, y puede elegir una cuenta de automatización que ejecute el runbook o crear fácilmente una cuenta.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span></span>

<span data-ttu-id="8f6a2-109">En este artículo, le mostraremos lo fácil que es establecer una alerta de máquina virtual de Azure y configurar un runbook de automatización para ejecutar cada vez que se desencadena la alerta.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span></span> <span data-ttu-id="8f6a2-110">Entre los escenarios de ejemplo se incluyen el tener que reiniciar una máquina virtual cuando el uso de memoria supera cierto límite debido a que una aplicación de la misma tiene una fuga de memoria, o el detener la máquina virtual si el tiempo de usuario de CPU ha sido inferior al 1% durante la última hora y no está en uso.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="8f6a2-111">También explicaremos cómo la creación automatizada de una entidad de servicio en la cuenta de automatización simplifica el uso de runbooks en la corrección de alertas de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="8f6a2-112">Creación de una alerta para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8f6a2-112">Create an alert on a VM</span></span>
<span data-ttu-id="8f6a2-113">Realice los pasos siguientes para configurar una alerta para iniciar un runbook cuando se haya alcanzado el umbral.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="8f6a2-114">En esta versión solo se admiten máquinas virtuales de V2 y pronto se agregará el soporte técnico para máquinas virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="8f6a2-115">Inicie sesión en el Portal de Azure y haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-115">Log in to the Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="8f6a2-116">Seleccione una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="8f6a2-117">Aparecerá la hoja de panel de la máquina virtual y la hoja **Configuración** a la derecha.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span></span>  
3. <span data-ttu-id="8f6a2-118">En la hoja **Configuración**, en la sección de supervisión, seleccione **Reglas de alerta**.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="8f6a2-119">En la hoja **Reglas de alerta**, haga clic en **Agregar alerta**.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-119">On the **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="8f6a2-120">Esto abre la hoja **Agregar una regla de alerta** , donde puede configurar las condiciones de la alerta y elegir entre una o todas estas opciones: enviar un correo electrónico a alguien, utilizar un Webhook para reenviar la alerta a otro sistema o ejecutar un runbook de automatización para intentar corregir el problema.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="8f6a2-121">Configuración de un runbook</span><span class="sxs-lookup"><span data-stu-id="8f6a2-121">Configure a runbook</span></span>
<span data-ttu-id="8f6a2-122">Para configurar un runbook parar que se ejecute cuando se cumpla el umbral de alerta de la máquina virtual, seleccione **Runbook de automatización**.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="8f6a2-123">En la hoja **Configurar runbook** , puede seleccionar el runbook que desea ejecutar y la cuenta de automatización en la que quiere ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span></span>

![Configuración de un runbook de automatización y creación de una nueva cuenta de automatización](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="8f6a2-125">En esta versión puede elegir entre los tres runbooks que proporciona el servicio: reiniciar, detener o quitar (eliminar) la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="8f6a2-126">La capacidad para seleccionar otros runbooks o uno de sus propios runbooks estará disponible en próximas versiones.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Runbooks que puede elegir](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="8f6a2-128">Después de seleccionar uno de los tres runbooks disponibles, aparecerá la lista desplegable **Cuenta de automatización** y podrá seleccionar la cuenta de automatización en la que se ejecutará el runbook.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span></span> <span data-ttu-id="8f6a2-129">Los runbooks se deben ejecutar en el contexto de una [cuenta de automatización](automation-security-overview.md) que se incluye en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="8f6a2-130">Puede seleccionar una cuenta de automatización que ya haya creado o puede crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="8f6a2-131">Los runbooks proporcionados se autentican en Azure mediante una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-131">The runbooks that are provided authenticate to Azure using a service principal.</span></span> <span data-ttu-id="8f6a2-132">Si elige ejecutar el runbook en una de sus cuentas de automatización existentes, la entidad de servicio se creará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span></span> <span data-ttu-id="8f6a2-133">Si decide crear una nueva cuenta de automatización, se creará automáticamente la cuenta y la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span></span> <span data-ttu-id="8f6a2-134">En ambos casos, también se crearán dos recursos en la cuenta de Automation: un recurso de certificado denominado **AzureRunAsCertificate** y un recurso de conexión denominado **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="8f6a2-135">Los runbooks utilizarán **AzureRunAsConnection** para autenticarse con Azure para realizar la acción de administración en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="8f6a2-136">La entidad de servicio se crea en el ámbito de la suscripción y se le asigna el rol Colaborador.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span></span> <span data-ttu-id="8f6a2-137">Este rol es necesario para otorgar permiso a la cuenta para ejecutar runbooks de automatización para administrar máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span></span>  <span data-ttu-id="8f6a2-138">La creación de una cuenta de automatización o una entidad de servicio es un evento único.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-138">The creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="8f6a2-139">Una vez creados, puede utilizar esa cuenta para ejecutar runbooks para otras alertas de la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="8f6a2-140">Al hacer clic en **Aceptar** se configurará la alerta y si ha seleccionado la opción para crear una nueva cuenta de automatización, esta se creará junto con la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span></span>  <span data-ttu-id="8f6a2-141">Este proceso puede tardar unos segundos en completarse.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-141">This can take a few seconds to complete.</span></span>  

![Runbook que se está configurando](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="8f6a2-143">Una vez completada la configuración aparecerá el nombre del runbook en la hoja **Agregar una regla de alerta** .</span><span class="sxs-lookup"><span data-stu-id="8f6a2-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span></span>

![Runbook configurado](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="8f6a2-145">Haga clic en **Aceptar** in the **Agregar una regla de alerta** y se creará la regla de alerta y se activará si la máquina virtual está en estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="8f6a2-146">Habilitamiento o deshabilitamiento de un runbook</span><span class="sxs-lookup"><span data-stu-id="8f6a2-146">Enable or disable a runbook</span></span>
<span data-ttu-id="8f6a2-147">Si tiene un runbook configurado para una alerta, puede deshabilitarlo sin quitar la configuración del mismo.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span></span> <span data-ttu-id="8f6a2-148">Esto le permitirá mantener la alerta en ejecución y quizás probar algunas de las reglas de alerta y, a continuación, volver a habilitar el runbook.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="8f6a2-149">Creación de un Runbook que funciona con una alerta de Azure</span><span class="sxs-lookup"><span data-stu-id="8f6a2-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="8f6a2-150">Cuando se elige un Runbook como parte de una regla de alerta de Azure, el Runbook debe contener lógica para administrar los datos de alerta que se le pasen.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span></span>  <span data-ttu-id="8f6a2-151">Cuando se configura un Runbook en una regla de alerta, se crea un webhook para el Runbook; luego, se utiliza este webhook para iniciar el Runbook cada vez que se desencadene la alerta.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span></span>  <span data-ttu-id="8f6a2-152">La llamada real para iniciar el Runbook es una solicitud HTTP POST a la dirección URL de webhook.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span></span> <span data-ttu-id="8f6a2-153">El cuerpo de la solicitud POST contiene un objeto con formato JSON que incluye propiedades útiles relacionadas con la alerta.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span></span>  <span data-ttu-id="8f6a2-154">Como puede ver a continuación, los datos de alerta contienen detalles como subscriptionID, resourceGroupName, resourceName y resourceType.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="8f6a2-155">Ejemplo de datos de alerta</span><span class="sxs-lookup"><span data-stu-id="8f6a2-155">Example of Alert data</span></span>
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

<span data-ttu-id="8f6a2-156">Cuando el servicio de webhook de automatización recibe HTTP POST, extrae los datos de alerta y los pasa al Runbook en el parámetro de entrada de Runbook WebhookData.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span></span>  <span data-ttu-id="8f6a2-157">A continuación se muestra un Runbook de ejemplo que muestra cómo usar el parámetro WebhookData, extraer los datos de alerta y usarlos para administrar el recurso de Azure que activó la alerta.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="8f6a2-158">Runbook de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8f6a2-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response to an Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get the data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that the alert status is 'Activated' (alert condition went from false to true)
    # and not 'Resolved' (alert condition went from true to false)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get the info needed to identify the VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is the expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate to Azure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart the VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # The alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant to be started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="8f6a2-159">Resumen</span><span class="sxs-lookup"><span data-stu-id="8f6a2-159">Summary</span></span>
<span data-ttu-id="8f6a2-160">Cuando configura una alerta en una máquina virtual de Azure, tiene la capacidad de configurar fácilmente un runbook de automatización para que realice la acción correctora automáticamente cuando se desencadene la alerta.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span></span> <span data-ttu-id="8f6a2-161">En esta versión, puede elegir entre los runbooks para reiniciar, detener o eliminar una máquina virtual según el escenario de la alerta.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="8f6a2-162">Esto es solo el principio de la habilitación de escenarios en los que puede controlar las acciones (notificación, solución de problemas, corrección) que se realizarán automáticamente cuando se desencadene una alerta.</span><span class="sxs-lookup"><span data-stu-id="8f6a2-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f6a2-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f6a2-163">Next Steps</span></span>
* <span data-ttu-id="8f6a2-164">Para empezar a trabajar con Runbooks gráficos, consulte [Mi primer runbook gráfico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="8f6a2-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="8f6a2-165">Para empezar a trabajar con Runbooks de flujo de trabajo de PowerShell, consulte [Mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="8f6a2-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="8f6a2-166">Para más información sobre los tipos de Runbook, sus ventajas y sus limitaciones, consulte [Tipos de runbooks de Automatización de Azure](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="8f6a2-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

