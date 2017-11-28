---
title: "aaa\"corregir las alertas de la máquina virtual de Azure con Runbooks de automatización | Documentos de Microsoft\""
description: "En este artículo se muestra cómo las alertas toointegrate Máquina Virtual de Azure con runbooks de automatización de Azure y auto-corregir problemas"
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
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="617b1-103">Escenario de Automatización de Azure: corrección de las alertas de la máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="617b1-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="617b1-104">Automatización de Azure y máquinas virtuales de Azure ha publicado una nueva característica permitiéndole runbooks de automatización de toorun las alertas de tooconfigure Máquina Virtual (VM).</span><span class="sxs-lookup"><span data-stu-id="617b1-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="617b1-105">Esta nueva capacidad le permite tooautomatically realizar correcciones de estándar en las alertas de tooVM de respuesta, como reiniciar o detener Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="617b1-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="617b1-106">Anteriormente, durante la creación de la regla de alerta de VM podía demasiado[especificar un webhook de automatización](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook en orden toorun Hola runbook cada vez que desencadene Hola alerta.</span><span class="sxs-lookup"><span data-stu-id="617b1-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="617b1-107">Sin embargo, esto requiere trabajo de hello toodo de creación de runbook de hello, crear webhook Hola Hola runbook y, a continuación, copiar y pegar hello webhook durante la creación de la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="617b1-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="617b1-108">Con esta nueva versión, el proceso de hello es mucho más fácil porque directamente, puede elegir un runbook de una lista durante la creación de la regla de alerta, y puede elegir una cuenta de automatización que se ejecuten runbook Hola o crear fácilmente una cuenta.</span><span class="sxs-lookup"><span data-stu-id="617b1-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="617b1-109">En este artículo, agregaremos muestra lo fácil que es tooset una alerta de la máquina virtual de Azure y configurar una toorun de runbook de automatización siempre que desencadena la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="617b1-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="617b1-110">Escenarios de ejemplo incluyen reiniciar una máquina virtual cuando el uso de memoria de hello supera determinado umbral debido tooan aplicación Hola VM con una pérdida de memoria, o detener una máquina virtual al tiempo de usuario de hello CPU ha sido por debajo de % 1 de última hora y no está en uso.</span><span class="sxs-lookup"><span data-stu-id="617b1-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="617b1-111">También explicaremos cómo Hola automatiza la creación de una entidad de servicio en la automatización cuenta simplifica el uso de Hola de runbooks en Azure corrección de alerta.</span><span class="sxs-lookup"><span data-stu-id="617b1-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="617b1-112">Creación de una alerta para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="617b1-112">Create an alert on a VM</span></span>
<span data-ttu-id="617b1-113">Realizar Hola siguientes pasos tooconfigure una alerta toolaunch un runbook cuando se ha alcanzado el umbral.</span><span class="sxs-lookup"><span data-stu-id="617b1-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="617b1-114">En esta versión solo se admiten máquinas virtuales de V2 y pronto se agregará el soporte técnico para máquinas virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="617b1-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="617b1-115">Inicie sesión en toohello portal de Azure y haga clic en **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="617b1-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="617b1-116">Seleccione una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="617b1-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="617b1-117">Hello hoja de panel de máquina virtual aparecerá y Hola **configuración** derecha tooits de hoja.</span><span class="sxs-lookup"><span data-stu-id="617b1-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="617b1-118">De hello **configuración** hoja bajo Seleccione de la sección de supervisión de hello **reglas de alerta**.</span><span class="sxs-lookup"><span data-stu-id="617b1-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="617b1-119">En hello **reglas de alerta** hoja, haga clic en **Agregar alerta**.</span><span class="sxs-lookup"><span data-stu-id="617b1-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="617b1-120">Esto abrirá hello **agregar una regla de alerta** hoja, donde puede configurar las condiciones de Hola de alerta de Hola y elegir entre una o todas estas opciones: enviar correo electrónico toosomeone, utilice un sistema de alerta tooanother webhook tooforward hello, o ejecutar un runbook de automatización problema de respuesta intento tooremediate Hola.</span><span class="sxs-lookup"><span data-stu-id="617b1-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="617b1-121">Configuración de un runbook</span><span class="sxs-lookup"><span data-stu-id="617b1-121">Configure a runbook</span></span>
<span data-ttu-id="617b1-122">Seleccione tooconfigure un toorun runbook cuando se cumpla el umbral de alerta de VM de hello, **Runbook de automatización**.</span><span class="sxs-lookup"><span data-stu-id="617b1-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="617b1-123">Hola **configurar runbook** hoja, puede seleccionar toorun de runbook de Hola y Hola automatización cuenta toorun Hola runbook en.</span><span class="sxs-lookup"><span data-stu-id="617b1-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![Configuración de un runbook de automatización y creación de una nueva cuenta de automatización](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="617b1-125">Para esta versión puede elegir entre tres runbooks que proporciona el servicio de hello: reiniciar VM, detener la máquina virtual o VM quitar (eliminar).</span><span class="sxs-lookup"><span data-stu-id="617b1-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="617b1-126">Hola tooselect capacidad otros runbooks o uno de sus propios runbooks estará disponible en futuras versiones.</span><span class="sxs-lookup"><span data-stu-id="617b1-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Toochoose de runbooks desde](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="617b1-128">Después de seleccionar uno de los runbooks disponibles Hola tres, Hola **cuenta de automatización** aparece la lista desplegable y puede seleccionar una automatización cuenta Hola runbook se ejecutará como.</span><span class="sxs-lookup"><span data-stu-id="617b1-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="617b1-129">Runbooks necesita toorun en contexto de Hola de un [cuenta de automatización](automation-security-overview.md) que se encuentra en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="617b1-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="617b1-130">Puede seleccionar una cuenta de automatización que ya haya creado o puede crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="617b1-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="617b1-131">Hola runbooks que se proporcionan autenticar tooAzure con una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="617b1-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="617b1-132">Si elige toorun Hola runbook en una de las cuentas de automatización existentes, se creará automáticamente servicio Hola principal para usted.</span><span class="sxs-lookup"><span data-stu-id="617b1-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="617b1-133">Si elige una nueva cuenta de automatización toocreate, a continuación, se creará automáticamente cuenta hello y entidad de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="617b1-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="617b1-134">En ambos casos, también se creará dos recursos Hola cuenta de automatización: un activo de certificado denominado **AzureRunAsCertificate** y un recurso de conexión denominado **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="617b1-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="617b1-135">Hola runbooks usará **AzureRunAsConnection** tooauthenticate con Azure en acción de administración de orden tooperform Hola contra Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="617b1-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="617b1-136">entidad de servicio de Hola se crea en el ámbito de la suscripción de Hola y se asigna el rol de colaborador de Hola.</span><span class="sxs-lookup"><span data-stu-id="617b1-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="617b1-137">Este rol es necesario para hello cuenta toohave permiso toorun Automation runbooks toomanage máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="617b1-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="617b1-138">creación de Hello de una cuenta de automatización o una entidad de servicio es un evento único.</span><span class="sxs-lookup"><span data-stu-id="617b1-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="617b1-139">Una vez que se crean, puede usar ese runbooks de toorun cuenta otras alertas de la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="617b1-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="617b1-140">Al hacer clic en **Aceptar** alerta Hola está configurado y si seleccionó Hola opción toocreate una nueva cuenta de automatización, se crea junto con la entidad de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="617b1-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="617b1-141">Esta operación puede tardar unos segundos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="617b1-141">This can take a few seconds toocomplete.</span></span>  

![Runbook que se está configurando](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="617b1-143">Una vez finalizada la configuración de hello verán el nombre de Hola de hello runbook aparecen en hello **agregar una regla de alerta** hoja.</span><span class="sxs-lookup"><span data-stu-id="617b1-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![Runbook configurado](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="617b1-145">Haga clic en **Aceptar** en hello **agregar una regla de alerta** hello y hoja de regla de alerta se va a crear y activar si la máquina virtual de hello está en un estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="617b1-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="617b1-146">Habilitamiento o deshabilitamiento de un runbook</span><span class="sxs-lookup"><span data-stu-id="617b1-146">Enable or disable a runbook</span></span>
<span data-ttu-id="617b1-147">Si tiene un runbook configurado para una alerta, puede deshabilitarlo sin quitar la configuración de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="617b1-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="617b1-148">Esto permite alerta de hello tookeep ejecutando y es posible probar algunas de las reglas de alerta de hello y, a continuación, volver a habilitar Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="617b1-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="617b1-149">Creación de un Runbook que funciona con una alerta de Azure</span><span class="sxs-lookup"><span data-stu-id="617b1-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="617b1-150">Cuando se elige un runbook como parte de una regla de alerta de Azure, Hola runbook debe lógica toohave toomanage Hola datos de alertas que se pasan tooit.</span><span class="sxs-lookup"><span data-stu-id="617b1-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="617b1-151">Cuando se configura un runbook en una regla de alerta, se crea un webhook de hello runbook; ese webhook es toostart usado Hola runbook cada desencadenadores de alerta de Hola de tiempo.</span><span class="sxs-lookup"><span data-stu-id="617b1-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="617b1-152">Hola llamada real toostart Hola runbook es una dirección URL webhook de toohello de solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="617b1-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="617b1-153">cuerpo de saludo de solicitud POST de hello contiene un objeto con formato JSON que contiene propiedades útiles relacionados toohello alerta.</span><span class="sxs-lookup"><span data-stu-id="617b1-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="617b1-154">Como puede ver a continuación, los datos de alertas de hello contienen detalles como el Id. de suscripción, resourceGroupName, resourceName y resourceType.</span><span class="sxs-lookup"><span data-stu-id="617b1-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="617b1-155">Ejemplo de datos de alerta</span><span class="sxs-lookup"><span data-stu-id="617b1-155">Example of Alert data</span></span>
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

<span data-ttu-id="617b1-156">Cuando Hola servicio de webhook de automatización recibe Hola HTTP POST extrae datos de alertas de Hola y pasa toohello runbook hello WebhookData runbook parámetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="617b1-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="617b1-157">A continuación se muestra un runbook de ejemplo que muestre cómo Hola WebhookData parámetro toouse y extraer datos de alertas de Hola y usar toomanage Hola recursos de Azure que desencadenó la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="617b1-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="617b1-158">Runbook de ejemplo</span><span class="sxs-lookup"><span data-stu-id="617b1-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="617b1-159">Resumen</span><span class="sxs-lookup"><span data-stu-id="617b1-159">Summary</span></span>
<span data-ttu-id="617b1-160">Al configurar una alerta en una máquina virtual de Azure, ahora tiene Hola capacidad tooeasily configurar una automatización de runbook tooautomatically realizar acción correctora cuando se desencadena la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="617b1-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="617b1-161">En esta versión, puede elegir entre toorestart runbooks, detener o eliminar una máquina virtual según el escenario de alerta.</span><span class="sxs-lookup"><span data-stu-id="617b1-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="617b1-162">Se trata de principio simplemente Hola de habilitar escenarios donde se controlan las acciones de hello (notificaciones, solución de problemas, corrección) que se realizará automáticamente cuando se desencadena una alerta.</span><span class="sxs-lookup"><span data-stu-id="617b1-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="617b1-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="617b1-163">Next Steps</span></span>
* <span data-ttu-id="617b1-164">tooget a trabajar con runbooks gráficos, consulte [mi primer runbook gráfico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="617b1-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="617b1-165">tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="617b1-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="617b1-166">toolearn más información acerca de los tipos de runbook, sus ventajas y limitaciones, consulte [tipos de runbook de automatización de Azure](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="617b1-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

