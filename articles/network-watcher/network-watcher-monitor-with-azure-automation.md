---
title: "las puertas de enlace VPN aaaMonitor con la solución de problemas de Monitor de red de Azure | Documentos de Microsoft"
description: "En este artículo se describe cómo diagnosticar la conectividad local con Azure Automation y Network Watcher"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="0858c-103">Supervisión de las puertas de enlace de VPN con la solución de problemas de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="0858c-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="0858c-104">Obtener información detallada sobre el rendimiento de red es crítico tooprovide toocustomers de servicios de confianza.</span><span class="sxs-lookup"><span data-stu-id="0858c-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="0858c-105">Es por lo tanto, crítico toodetect condiciones de interrupción de red rápidamente y tomar la condición de interrupción de acción correctiva toomitigate Hola.</span><span class="sxs-lookup"><span data-stu-id="0858c-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="0858c-106">Automatización de Azure permite tooimplement y ejecuta una tarea en un modo mediante programación a través de runbooks.</span><span class="sxs-lookup"><span data-stu-id="0858c-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="0858c-107">El uso de Azure Automation crea una receta perfecta para realizar la supervisión continua y proactiva de la red y crear alertas.</span><span class="sxs-lookup"><span data-stu-id="0858c-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="0858c-108">Escenario</span><span class="sxs-lookup"><span data-stu-id="0858c-108">Scenario</span></span>

<span data-ttu-id="0858c-109">escenario de Hola Hola después de la imagen es una aplicación de varios niveles, con conectividad local establecida mediante un túnel y una puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="0858c-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="0858c-110">Asegurándose de hello que puerta de enlace VPN está activo y ejecutando son toohello críticos de rendimiento de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0858c-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="0858c-111">Se crea un runbook con un toocheck de secuencia de comandos para el estado de la conexión de túnel de VPN de hello, mediante toocheck de API de solución de problemas de recursos de hello para el estado de conexión de túnel.</span><span class="sxs-lookup"><span data-stu-id="0858c-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="0858c-112">Si el estado de hello no es correcto, un desencadenador de correo electrónico se envía tooadministrators.</span><span class="sxs-lookup"><span data-stu-id="0858c-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![Escenario de ejemplo][scenario]

<span data-ttu-id="0858c-114">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="0858c-114">This scenario will:</span></span>

- <span data-ttu-id="0858c-115">Crear un hello llamada runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` estado de la conexión de cmdlet tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="0858c-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="0858c-116">Vincular un runbook de toohello de programación</span><span class="sxs-lookup"><span data-stu-id="0858c-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0858c-117">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="0858c-117">Before you begin</span></span>

<span data-ttu-id="0858c-118">Antes de empezar este escenario, debe tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="0858c-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="0858c-119">Tener una cuenta de Azure Automation en Azure.</span><span class="sxs-lookup"><span data-stu-id="0858c-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="0858c-120">Asegúrese de que cuenta de automatización de hello tiene módulos más recientes de Hola y también tiene hello AzureRM.Network módulo.</span><span class="sxs-lookup"><span data-stu-id="0858c-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="0858c-121">módulo de Hello AzureRM.Network está disponible en la Galería de módulos de hello si necesita tooadd se tooyour cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="0858c-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="0858c-122">Tener un conjunto de credenciales configuradas en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="0858c-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="0858c-123">Obtenga más información en el artículo sobre [seguridad en Azure Automation](../automation/automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0858c-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="0858c-124">Tener un servidor SMTP válido (Office 365, correo electrónico local u otro) y las credenciales definidas en Azure Automation</span><span class="sxs-lookup"><span data-stu-id="0858c-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="0858c-125">Tener una puerta de enlace de Virtual Network configurada en Azure.</span><span class="sxs-lookup"><span data-stu-id="0858c-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="0858c-126">Registra una cuenta de almacenamiento existente con un hello toostore de contenedor existente en.</span><span class="sxs-lookup"><span data-stu-id="0858c-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="0858c-127">infraestructura de Hello representado en hello anterior imagen es con fines meramente ilustrativos y no se crean con pasos de hello contenidas en este artículo.</span><span class="sxs-lookup"><span data-stu-id="0858c-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="0858c-128">Crear Hola runbook</span><span class="sxs-lookup"><span data-stu-id="0858c-128">Create hello runbook</span></span>

<span data-ttu-id="0858c-129">ejemplo de Hola primer paso tooconfiguring hello es toocreate Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="0858c-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="0858c-130">Este ejemplo utiliza una cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0858c-130">This example uses a run-as account.</span></span> <span data-ttu-id="0858c-131">toolearn acerca de las cuentas de ejecución, visite [Runbooks autenticarse con Azure cuenta de ejecución](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="0858c-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="0858c-132">Paso 1</span><span class="sxs-lookup"><span data-stu-id="0858c-132">Step 1</span></span>

<span data-ttu-id="0858c-133">Navegue tooAzure automatización en hello [portal de Azure](https://portal.azure.com) y haga clic en **Runbooks**</span><span class="sxs-lookup"><span data-stu-id="0858c-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Información general sobre las cuentas de Automation][1]

### <a name="step-2"></a><span data-ttu-id="0858c-135">Paso 2</span><span class="sxs-lookup"><span data-stu-id="0858c-135">Step 2</span></span>

<span data-ttu-id="0858c-136">Haga clic en **agregar un runbook** toostart proceso de creación de hello de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0858c-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![Hoja de runbooks][2]

### <a name="step-3"></a><span data-ttu-id="0858c-138">Paso 3</span><span class="sxs-lookup"><span data-stu-id="0858c-138">Step 3</span></span>

<span data-ttu-id="0858c-139">En **creación rápida**, haga clic en **crear un nuevo runbook** toocreate Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="0858c-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![Hoja para agregar una hoja de runbook][3]

### <a name="step-4"></a><span data-ttu-id="0858c-141">Paso 4</span><span class="sxs-lookup"><span data-stu-id="0858c-141">Step 4</span></span>

<span data-ttu-id="0858c-142">En este paso, proporcionamos a runbook Hola un nombre, en el ejemplo de Hola se denomina **VPNGatewayStatus Get**.</span><span class="sxs-lookup"><span data-stu-id="0858c-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="0858c-143">Es importante toogive Hola runbook un nombre descriptivo y recomienda darle un nombre que sigue a los estándares de nomenclatura estándares de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0858c-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="0858c-144">tipo de runbook de Hello en este ejemplo es **PowerShell**, hello otras opciones son gráficos, flujo de trabajo de PowerShell y el flujo de trabajo de PowerShell gráfica.</span><span class="sxs-lookup"><span data-stu-id="0858c-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![Hoja de runbook][4]

### <a name="step-5"></a><span data-ttu-id="0858c-146">Paso 5</span><span class="sxs-lookup"><span data-stu-id="0858c-146">Step 5</span></span>

<span data-ttu-id="0858c-147">En este paso hello runbook se crea, Hola el ejemplo de código siguiente proporciona que todos Hola código necesario para el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0858c-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="0858c-148">Hola elementos en el código de hello que contienen \<valor\> necesita toobe reemplazan por valores de hello desde su suscripción.</span><span class="sxs-lookup"><span data-stu-id="0858c-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="0858c-149">Use Hola siguiente de código como haga clic en **guardar**</span><span class="sxs-lookup"><span data-stu-id="0858c-149">Use hello following code as click **Save**</span></span>

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a><span data-ttu-id="0858c-150">Paso 6</span><span class="sxs-lookup"><span data-stu-id="0858c-150">Step 6</span></span>

<span data-ttu-id="0858c-151">Una vez que se guarda Hola runbook, debe ser una programación vinculada inicio de hello tooit tooautomate de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0858c-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="0858c-152">proceso de hello toostart, haga clic en **programación**.</span><span class="sxs-lookup"><span data-stu-id="0858c-152">toostart hello process, click **Schedule**.</span></span>

![Paso 6][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="0858c-154">Vincular un runbook de toohello de programación</span><span class="sxs-lookup"><span data-stu-id="0858c-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="0858c-155">Tiene que crear una nueva programación.</span><span class="sxs-lookup"><span data-stu-id="0858c-155">A new schedule must be created.</span></span> <span data-ttu-id="0858c-156">Haga clic en **vincular un runbook de programación tooyour**.</span><span class="sxs-lookup"><span data-stu-id="0858c-156">Click **Link a schedule tooyour runbook**.</span></span>

![Paso 7][7]

### <a name="step-1"></a><span data-ttu-id="0858c-158">Paso 1</span><span class="sxs-lookup"><span data-stu-id="0858c-158">Step 1</span></span>

<span data-ttu-id="0858c-159">En hello **programación** hoja, haga clic en **crear una nueva programación**</span><span class="sxs-lookup"><span data-stu-id="0858c-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![Paso 8][8]

### <a name="step-2"></a><span data-ttu-id="0858c-161">Paso 2</span><span class="sxs-lookup"><span data-stu-id="0858c-161">Step 2</span></span>

<span data-ttu-id="0858c-162">En hello **nueva programación** hoja rellene la información de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0858c-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="0858c-163">los valores de Hello que se pueden establecer son Hola lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="0858c-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="0858c-164">**Nombre de** -nombre descriptivo de Hola de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0858c-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="0858c-165">**Descripción** -una descripción de la programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0858c-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="0858c-166">**Inicia** -este valor es una combinación de fecha, hora y zona horaria que componen los desencadenadores de programación de hello tiempo Hola.</span><span class="sxs-lookup"><span data-stu-id="0858c-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="0858c-167">**Periodicidad** -este valor determina la repetición de las programaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="0858c-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="0858c-168">Los valores posibles son **Una vez** o **Periódica**.</span><span class="sxs-lookup"><span data-stu-id="0858c-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="0858c-169">**Repetir cada** -intervalo de periodicidad de saludo de programación de hello en horas, días, semanas o meses.</span><span class="sxs-lookup"><span data-stu-id="0858c-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="0858c-170">**Caducidad del conjunto de** -valor Hola determina si debe expirar la programación de Hola o no.</span><span class="sxs-lookup"><span data-stu-id="0858c-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="0858c-171">Se puede establecer demasiado**Sí** o **No**.</span><span class="sxs-lookup"><span data-stu-id="0858c-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="0858c-172">Una fecha y hora válidas son toobe proporcionada si se elige Sí.</span><span class="sxs-lookup"><span data-stu-id="0858c-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="0858c-173">Si necesita toohave un runbook que se ejecute con más frecuencia que cada hora, deben crearse varias programaciones en intervalos diferentes (es decir, 15, 30, 45 minutos después de la hora de hello)</span><span class="sxs-lookup"><span data-stu-id="0858c-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![Paso 9:][9]

### <a name="step-3"></a><span data-ttu-id="0858c-175">Paso 3</span><span class="sxs-lookup"><span data-stu-id="0858c-175">Step 3</span></span>

<span data-ttu-id="0858c-176">Haga clic en Guardar toosave Hola programación toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="0858c-176">Click Save toosave hello schedule toohello runbook.</span></span>

![Paso 10][10]

## <a name="next-steps"></a><span data-ttu-id="0858c-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0858c-178">Next steps</span></span>

<span data-ttu-id="0858c-179">Ahora que tiene una descripción sobre cómo toointegrate solucionar problemas de Monitor de red con la automatización de Azure, obtenga información acerca de la captura de paquetes de tootrigger en alertas VM visitando [crear una captura de paquetes desencadenadas alerta con Monitor de red de Azure](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="0858c-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
