---
title: "Supervisión de las puertas de enlace de VPN con la solución de problemas de Azure Network Watcher | Documentos de Microsoft"
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
ms.openlocfilehash: 55ec52dd0d94a0347cc67a8785b89611da955111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="88cce-103">Supervisión de las puertas de enlace de VPN con la solución de problemas de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="88cce-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="88cce-104">Obtener información detallada sobre el rendimiento de la red es fundamental para proporcionar servicios de confianza a los clientes.</span><span class="sxs-lookup"><span data-stu-id="88cce-104">Gaining deep insights on your network performance is critical to provide reliable services to customers.</span></span> <span data-ttu-id="88cce-105">Por lo tanto, es fundamental detectar rápidamente las condiciones de interrupción de la red y tomar medidas correctivas para mitigar los efectos de la condición de interrupción.</span><span class="sxs-lookup"><span data-stu-id="88cce-105">It is therefore critical to detect network outage conditions quickly and take corrective action to mitigate the outage condition.</span></span> <span data-ttu-id="88cce-106">Azure Automation permite implementar y ejecutar una tarea de forma programática a través de runbooks.</span><span class="sxs-lookup"><span data-stu-id="88cce-106">Azure Automation enables you to implement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="88cce-107">El uso de Azure Automation crea una receta perfecta para realizar la supervisión continua y proactiva de la red y crear alertas.</span><span class="sxs-lookup"><span data-stu-id="88cce-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="88cce-108">Escenario</span><span class="sxs-lookup"><span data-stu-id="88cce-108">Scenario</span></span>

<span data-ttu-id="88cce-109">El escenario en la siguiente imagen es una aplicación de varios niveles, con conectividad local establecida mediante una puerta de enlace de VPN y un túnel.</span><span class="sxs-lookup"><span data-stu-id="88cce-109">The scenario in the following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="88cce-110">Asegurarse de que VPN Gateway está activo y ejecutándose es fundamental para el correcto rendimiento de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="88cce-110">Ensuring the VPN Gateway is up and running is critical to the applications performance.</span></span>

<span data-ttu-id="88cce-111">Se crea un runbook con un script para comprobar el estado de la conexión de túnel de VPN, usando la API de solución de problemas de recursos para comprobar el estado del túnel de conexión.</span><span class="sxs-lookup"><span data-stu-id="88cce-111">A runbook is created with a script to check for connection status of the VPN tunnel, using the Resource Troubleshooting API to check for connection tunnel status.</span></span> <span data-ttu-id="88cce-112">Si el estado no es correcto, se envía a los administradores un desencadenador de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="88cce-112">If the status is not healthy, an email trigger is sent to administrators.</span></span>

![Escenario de ejemplo][scenario]

<span data-ttu-id="88cce-114">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="88cce-114">This scenario will:</span></span>

- <span data-ttu-id="88cce-115">Creará un runbook que llama al cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` para solucionar los problemas de estado de la conexión</span><span class="sxs-lookup"><span data-stu-id="88cce-115">Create a runbook calling the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet to troubleshoot connection status</span></span>
- <span data-ttu-id="88cce-116">Vinculará una programación al runbook</span><span class="sxs-lookup"><span data-stu-id="88cce-116">Link a schedule to the runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="88cce-117">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="88cce-117">Before you begin</span></span>

<span data-ttu-id="88cce-118">Antes de comenzar con este escenario, tiene que cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="88cce-118">Before you start this scenario, you must have the following pre-requisites:</span></span>

- <span data-ttu-id="88cce-119">Tener una cuenta de Azure Automation en Azure.</span><span class="sxs-lookup"><span data-stu-id="88cce-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="88cce-120">Asegúrese de que la cuenta de automatización tiene los módulos más recientes y de que además tiene el módulo AzureRM.Network.</span><span class="sxs-lookup"><span data-stu-id="88cce-120">Ensure that the automation account has the latest modules and also has the AzureRM.Network module.</span></span> <span data-ttu-id="88cce-121">Si tiene que agregar el módulo AzureRM.Network a la cuenta de automatización, lo tiene a su disposición en la galería de módulos.</span><span class="sxs-lookup"><span data-stu-id="88cce-121">The AzureRM.Network module is available in the module gallery if you need to add it to your automation account.</span></span>
- <span data-ttu-id="88cce-122">Tener un conjunto de credenciales configuradas en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="88cce-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="88cce-123">Obtenga más información en el artículo sobre [seguridad en Azure Automation](../automation/automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="88cce-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="88cce-124">Tener un servidor SMTP válido (Office 365, correo electrónico local u otro) y las credenciales definidas en Azure Automation</span><span class="sxs-lookup"><span data-stu-id="88cce-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="88cce-125">Tener una puerta de enlace de Virtual Network configurada en Azure.</span><span class="sxs-lookup"><span data-stu-id="88cce-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="88cce-126">Una cuenta de almacenamiento existente con un contenedor existente en el que almacenar los registros.</span><span class="sxs-lookup"><span data-stu-id="88cce-126">An existing storage account with an existing container to store the logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="88cce-127">La infraestructura que se muestra en la imagen anterior tiene fines meramente ilustrativos y no se creó con los pasos que se incluyen en este artículo.</span><span class="sxs-lookup"><span data-stu-id="88cce-127">The infrastructure depicted in the preceding image is for illustration purposes and are not created with the steps contained in this article.</span></span>

### <a name="create-the-runbook"></a><span data-ttu-id="88cce-128">Creación del runbook</span><span class="sxs-lookup"><span data-stu-id="88cce-128">Create the runbook</span></span>

<span data-ttu-id="88cce-129">El primer paso para configurar el ejemplo es crear el runbook.</span><span class="sxs-lookup"><span data-stu-id="88cce-129">The first step to configuring the example is to create the runbook.</span></span> <span data-ttu-id="88cce-130">Este ejemplo utiliza una cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="88cce-130">This example uses a run-as account.</span></span> <span data-ttu-id="88cce-131">Para obtener información acerca de las cuentas de ejecución, visite [Autenticación de Runbooks con una cuenta de ejecución de Azure](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="88cce-131">To learn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="88cce-132">Paso 1</span><span class="sxs-lookup"><span data-stu-id="88cce-132">Step 1</span></span>

<span data-ttu-id="88cce-133">Navegue a Azure Automation en [Azure Portal](https://portal.azure.com) y haga clic en **Runbooks**</span><span class="sxs-lookup"><span data-stu-id="88cce-133">Navigate to Azure Automation in the [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Información general sobre las cuentas de Automation][1]

### <a name="step-2"></a><span data-ttu-id="88cce-135">Paso 2</span><span class="sxs-lookup"><span data-stu-id="88cce-135">Step 2</span></span>

<span data-ttu-id="88cce-136">Haga clic en **Agregar un runbook** para iniciar el proceso de creación del runbook.</span><span class="sxs-lookup"><span data-stu-id="88cce-136">Click **Add a runbook** to start the creation process of the runbook.</span></span>

![Hoja de runbooks][2]

### <a name="step-3"></a><span data-ttu-id="88cce-138">Paso 3</span><span class="sxs-lookup"><span data-stu-id="88cce-138">Step 3</span></span>

<span data-ttu-id="88cce-139">En **Creación rápida**, haga clic en **Crear un runbook nuevo** para crear el runbook.</span><span class="sxs-lookup"><span data-stu-id="88cce-139">Under **Quick Create**, click **Create a new runbook** to create the runbook.</span></span>

![Hoja para agregar una hoja de runbook][3]

### <a name="step-4"></a><span data-ttu-id="88cce-141">Paso 4</span><span class="sxs-lookup"><span data-stu-id="88cce-141">Step 4</span></span>

<span data-ttu-id="88cce-142">En este paso, se le da un nombre al runbook, en el ejemplo se llama **VPNGatewayStatus Get**.</span><span class="sxs-lookup"><span data-stu-id="88cce-142">In this step, we give the runbook a name, in the example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="88cce-143">Es importante darle al runbook un nombre descriptivo y se recomienda que el nombre siga los estándares de nomenclatura de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88cce-143">It is important to give the runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="88cce-144">El tipo de runbook para este ejemplo es **PowerShell**, las otras opciones son Gráfico, Flujo de trabajo de PowerShell y Flujo de trabajo de PowerShell gráfico.</span><span class="sxs-lookup"><span data-stu-id="88cce-144">The runbook type for this example is **PowerShell**, the other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![Hoja de runbook][4]

### <a name="step-5"></a><span data-ttu-id="88cce-146">Paso 5</span><span class="sxs-lookup"><span data-stu-id="88cce-146">Step 5</span></span>

<span data-ttu-id="88cce-147">En este paso se crea el runbook, el ejemplo de código siguiente proporciona todo el código necesario para el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="88cce-147">In this step the runbook is created, the following code example provides all the code needed for the example.</span></span> <span data-ttu-id="88cce-148">Los elementos en el código que contienen \<value\> tienen que reemplazarse con los valores de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="88cce-148">The items in the code that contain \<value\> need to be replaced with the values from your subscription.</span></span>

<span data-ttu-id="88cce-149">Use el código siguiente y haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="88cce-149">Use the following code as click **Save**</span></span>

```PowerShell
# Set these variables to the proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<to email address>"
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

# Get the connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in to Azure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context to a specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView the logs at $($storagePath) to learn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -To $toEmail `
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

### <a name="step-6"></a><span data-ttu-id="88cce-150">Paso 6</span><span class="sxs-lookup"><span data-stu-id="88cce-150">Step 6</span></span>

<span data-ttu-id="88cce-151">Una vez guardado el runbook, tiene que haber una programación vinculada al mismo para automatizar su inicio.</span><span class="sxs-lookup"><span data-stu-id="88cce-151">Once the runbook is saved, a schedule must be linked to it to automate the start of the runbook.</span></span> <span data-ttu-id="88cce-152">Para iniciar el proceso, haga clic en **Programación**.</span><span class="sxs-lookup"><span data-stu-id="88cce-152">To start the process, click **Schedule**.</span></span>

![Paso 6][6]

## <a name="link-a-schedule-to-the-runbook"></a><span data-ttu-id="88cce-154">Vinculará una programación al runbook</span><span class="sxs-lookup"><span data-stu-id="88cce-154">Link a schedule to the runbook</span></span>

<span data-ttu-id="88cce-155">Tiene que crear una nueva programación.</span><span class="sxs-lookup"><span data-stu-id="88cce-155">A new schedule must be created.</span></span> <span data-ttu-id="88cce-156">Haga clic en **Vincular una programación a su runbook**.</span><span class="sxs-lookup"><span data-stu-id="88cce-156">Click **Link a schedule to your runbook**.</span></span>

![Paso 7][7]

### <a name="step-1"></a><span data-ttu-id="88cce-158">Paso 1</span><span class="sxs-lookup"><span data-stu-id="88cce-158">Step 1</span></span>

<span data-ttu-id="88cce-159">En la hoja **Programación**, haga clic en **Crear una programación nueva**</span><span class="sxs-lookup"><span data-stu-id="88cce-159">On the **Schedule** blade, click **Create a new schedule**</span></span>

![Paso 8][8]

### <a name="step-2"></a><span data-ttu-id="88cce-161">Paso 2</span><span class="sxs-lookup"><span data-stu-id="88cce-161">Step 2</span></span>

<span data-ttu-id="88cce-162">En la hoja **Nueva programación** rellene la información de programación.</span><span class="sxs-lookup"><span data-stu-id="88cce-162">On the **New Schedule** blade fill out the schedule information.</span></span> <span data-ttu-id="88cce-163">La lista siguiente enumera los valores que se pueden establecer:</span><span class="sxs-lookup"><span data-stu-id="88cce-163">The values that can be set are in the following list:</span></span>

- <span data-ttu-id="88cce-164">**Nombre**: el nombre descriptivo de la programación.</span><span class="sxs-lookup"><span data-stu-id="88cce-164">**Name** - The friendly name of the schedule.</span></span>
- <span data-ttu-id="88cce-165">**Description**: descripción de la programación.</span><span class="sxs-lookup"><span data-stu-id="88cce-165">**Description** - A description of the schedule.</span></span>
- <span data-ttu-id="88cce-166">**Se inicia el**: este valor es una combinación de fecha, hora y zona horaria que componen el horario en el que se desencadena la programación.</span><span class="sxs-lookup"><span data-stu-id="88cce-166">**Starts** - This value is a combination of date, time, and time zone that make up the time the schedule triggers.</span></span>
- <span data-ttu-id="88cce-167">**Periodicidad**: este valor determina la repetición de programaciones.</span><span class="sxs-lookup"><span data-stu-id="88cce-167">**Recurrence** - This value determines the schedules repetition.</span></span>  <span data-ttu-id="88cce-168">Los valores posibles son **Una vez** o **Periódica**.</span><span class="sxs-lookup"><span data-stu-id="88cce-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="88cce-169">**Repetir cada**: el intervalo de periodicidad de la programación en horas, días, semanas o meses.</span><span class="sxs-lookup"><span data-stu-id="88cce-169">**Recur every** - The recurrence interval of the schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="88cce-170">**Configurar expiración**: el valor determina si la programación debería expirar o no.</span><span class="sxs-lookup"><span data-stu-id="88cce-170">**Set Expiration** - The value determines if the schedule should expire or not.</span></span> <span data-ttu-id="88cce-171">Se puede establecer en **Sí** o **No**.</span><span class="sxs-lookup"><span data-stu-id="88cce-171">Can be set to **Yes** or **No**.</span></span> <span data-ttu-id="88cce-172">Si se elige Sí es necesario proporcionar una fecha y hora válidas.</span><span class="sxs-lookup"><span data-stu-id="88cce-172">A valid date and time are to be provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="88cce-173">Si necesita que un runbook se ejecute con más frecuencia que cada hora, tiene que crear varias programaciones en intervalos diferentes (es decir, 15, 30, 45 minutos después de la hora)</span><span class="sxs-lookup"><span data-stu-id="88cce-173">If you need to have a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after the hour)</span></span>

![Paso 9:][9]

### <a name="step-3"></a><span data-ttu-id="88cce-175">Paso 3</span><span class="sxs-lookup"><span data-stu-id="88cce-175">Step 3</span></span>

<span data-ttu-id="88cce-176">Haga clic en Guardar para guardar la programación del runbook.</span><span class="sxs-lookup"><span data-stu-id="88cce-176">Click Save to save the schedule to the runbook.</span></span>

![Paso 10][10]

## <a name="next-steps"></a><span data-ttu-id="88cce-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="88cce-178">Next steps</span></span>

<span data-ttu-id="88cce-179">Ahora que comprende mejor cómo integrar la solución de problemas de Network Watcher con Azure Automation, aprenda a desencadenar capturas de paquetes en las alertas de máquina virtual consultando el artículo en el que se describe cómo [crear una captura de paquetes desencadenada mediante alertas con Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="88cce-179">Now that you have an understanding on how to integrate Network Watcher troubleshooting with Azure Automation, learn how to trigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
