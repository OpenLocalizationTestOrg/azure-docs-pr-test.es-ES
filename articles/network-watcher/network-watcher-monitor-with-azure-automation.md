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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Supervisión de las puertas de enlace de VPN con la solución de problemas de Network Watcher

Obtener información detallada sobre el rendimiento de red es crítico tooprovide toocustomers de servicios de confianza. Es por lo tanto, crítico toodetect condiciones de interrupción de red rápidamente y tomar la condición de interrupción de acción correctiva toomitigate Hola. Automatización de Azure permite tooimplement y ejecuta una tarea en un modo mediante programación a través de runbooks. El uso de Azure Automation crea una receta perfecta para realizar la supervisión continua y proactiva de la red y crear alertas.

## <a name="scenario"></a>Escenario

escenario de Hola Hola después de la imagen es una aplicación de varios niveles, con conectividad local establecida mediante un túnel y una puerta de enlace VPN. Asegurándose de hello que puerta de enlace VPN está activo y ejecutando son toohello críticos de rendimiento de aplicaciones.

Se crea un runbook con un toocheck de secuencia de comandos para el estado de la conexión de túnel de VPN de hello, mediante toocheck de API de solución de problemas de recursos de hello para el estado de conexión de túnel. Si el estado de hello no es correcto, un desencadenador de correo electrónico se envía tooadministrators.

![Escenario de ejemplo][scenario]

En este escenario:

- Crear un hello llamada runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` estado de la conexión de cmdlet tootroubleshoot
- Vincular un runbook de toohello de programación

## <a name="before-you-begin"></a>Antes de empezar

Antes de empezar este escenario, debe tener Hola siguiendo los requisitos previos:

- Tener una cuenta de Azure Automation en Azure. Asegúrese de que cuenta de automatización de hello tiene módulos más recientes de Hola y también tiene hello AzureRM.Network módulo. módulo de Hello AzureRM.Network está disponible en la Galería de módulos de hello si necesita tooadd se tooyour cuenta de automatización.
- Tener un conjunto de credenciales configuradas en Azure Automation. Obtenga más información en el artículo sobre [seguridad en Azure Automation](../automation/automation-security-overview.md)
- Tener un servidor SMTP válido (Office 365, correo electrónico local u otro) y las credenciales definidas en Azure Automation
- Tener una puerta de enlace de Virtual Network configurada en Azure.
- Registra una cuenta de almacenamiento existente con un hello toostore de contenedor existente en.

> [!NOTE]
> infraestructura de Hello representado en hello anterior imagen es con fines meramente ilustrativos y no se crean con pasos de hello contenidas en este artículo.

### <a name="create-hello-runbook"></a>Crear Hola runbook

ejemplo de Hola primer paso tooconfiguring hello es toocreate Hola runbook. Este ejemplo utiliza una cuenta de ejecución. toolearn acerca de las cuentas de ejecución, visite [Runbooks autenticarse con Azure cuenta de ejecución](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>Paso 1

Navegue tooAzure automatización en hello [portal de Azure](https://portal.azure.com) y haga clic en **Runbooks**

![Información general sobre las cuentas de Automation][1]

### <a name="step-2"></a>Paso 2

Haga clic en **agregar un runbook** toostart proceso de creación de hello de runbook de Hola.

![Hoja de runbooks][2]

### <a name="step-3"></a>Paso 3

En **creación rápida**, haga clic en **crear un nuevo runbook** toocreate Hola runbook.

![Hoja para agregar una hoja de runbook][3]

### <a name="step-4"></a>Paso 4

En este paso, proporcionamos a runbook Hola un nombre, en el ejemplo de Hola se denomina **VPNGatewayStatus Get**. Es importante toogive Hola runbook un nombre descriptivo y recomienda darle un nombre que sigue a los estándares de nomenclatura estándares de PowerShell. tipo de runbook de Hello en este ejemplo es **PowerShell**, hello otras opciones son gráficos, flujo de trabajo de PowerShell y el flujo de trabajo de PowerShell gráfica.

![Hoja de runbook][4]

### <a name="step-5"></a>Paso 5

En este paso hello runbook se crea, Hola el ejemplo de código siguiente proporciona que todos Hola código necesario para el ejemplo de Hola. Hola elementos en el código de hello que contienen \<valor\> necesita toobe reemplazan por valores de hello desde su suscripción.

Use Hola siguiente de código como haga clic en **guardar**

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

### <a name="step-6"></a>Paso 6

Una vez que se guarda Hola runbook, debe ser una programación vinculada inicio de hello tooit tooautomate de runbook de Hola. proceso de hello toostart, haga clic en **programación**.

![Paso 6][6]

## <a name="link-a-schedule-toohello-runbook"></a>Vincular un runbook de toohello de programación

Tiene que crear una nueva programación. Haga clic en **vincular un runbook de programación tooyour**.

![Paso 7][7]

### <a name="step-1"></a>Paso 1

En hello **programación** hoja, haga clic en **crear una nueva programación**

![Paso 8][8]

### <a name="step-2"></a>Paso 2

En hello **nueva programación** hoja rellene la información de programación de Hola. los valores de Hello que se pueden establecer son Hola lista siguiente:

- **Nombre de** -nombre descriptivo de Hola de programación de Hola.
- **Descripción** -una descripción de la programación de Hola.
- **Inicia** -este valor es una combinación de fecha, hora y zona horaria que componen los desencadenadores de programación de hello tiempo Hola.
- **Periodicidad** -este valor determina la repetición de las programaciones de Hola.  Los valores posibles son **Una vez** o **Periódica**.
- **Repetir cada** -intervalo de periodicidad de saludo de programación de hello en horas, días, semanas o meses.
- **Caducidad del conjunto de** -valor Hola determina si debe expirar la programación de Hola o no. Se puede establecer demasiado**Sí** o **No**. Una fecha y hora válidas son toobe proporcionada si se elige Sí.

> [!NOTE]
> Si necesita toohave un runbook que se ejecute con más frecuencia que cada hora, deben crearse varias programaciones en intervalos diferentes (es decir, 15, 30, 45 minutos después de la hora de hello)

![Paso 9:][9]

### <a name="step-3"></a>Paso 3

Haga clic en Guardar toosave Hola programación toohello runbook.

![Paso 10][10]

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene una descripción sobre cómo toointegrate solucionar problemas de Monitor de red con la automatización de Azure, obtenga información acerca de la captura de paquetes de tootrigger en alertas VM visitando [crear una captura de paquetes desencadenadas alerta con Monitor de red de Azure](network-watcher-alert-triggered-packet-capture.md).

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
