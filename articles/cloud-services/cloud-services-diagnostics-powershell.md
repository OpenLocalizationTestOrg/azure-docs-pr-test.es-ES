---
title: "Habilitar el diagnóstico en Azure Cloud Services mediante PowerShell | Microsoft Docs"
description: "Obtener información sobre cómo habilitar el diagnóstico en servicios en la nube mediante PowerShell"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 8dd9724981860c9cd4ccc443cc2bfdc465811e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="3f72f-103">Habilitar el diagnóstico en Servicios en la nube de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f72f-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="3f72f-104">Puede recopilar datos de diagnóstico como registros de aplicaciones, contadores de rendimiento, etc., de un servicio en la nube mediante la extensión de Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f72f-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using the Azure Diagnostics extension.</span></span> <span data-ttu-id="3f72f-105">En este artículo se describe cómo habilitar la extensión de Diagnósticos de Azure para un servicio en la nube mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f72f-105">This article describes how to enable the Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="3f72f-106">Para conocer los requisitos previos necesarios para este artículo, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="3f72f-106">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="3f72f-107">Habilitar la extensión de diagnósticos como parte de la implementación de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="3f72f-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="3f72f-108">Este enfoque es aplicable para el tipo de integración continua de escenarios en los que se puede habilitar la extensión de diagnóstico como parte de la implementación del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="3f72f-108">This approach is applicable to continuous integration type of scenarios, where the diagnostics extension can be enabled as part of deploying the cloud service.</span></span> <span data-ttu-id="3f72f-109">Al crear una nueva implementación del servicio en la nube, puede habilitar la extensión de diagnóstico si pasa el parámetro *ExtensionConfiguration* al cmdlet [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="3f72f-109">When creating a new Cloud Service deployment you can enable the diagnostics extension by passing in the *ExtensionConfiguration* parameter to the [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="3f72f-110">El parámetro *ExtensionConfiguration* toma una matriz de configuraciones de diagnóstico que se pueden crear mediante el cmdlet [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="3f72f-110">The *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using the [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="3f72f-111">En el ejemplo siguiente se muestra cómo habilitar el diagnóstico de un servicio en la nube con un WebRole y WorkerRole, cada uno con una configuración de diagnóstico diferente.</span><span class="sxs-lookup"><span data-stu-id="3f72f-111">The following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

<span data-ttu-id="3f72f-112">Si el archivo de configuración de diagnóstico especifica un elemento `StorageAccount` con un nombre de cuenta de almacenamiento, el cmdlet `New-AzureServiceDiagnosticsExtensionConfig` usará automáticamente esa cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3f72f-112">If the diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="3f72f-113">Para que esto funcione, la cuenta de almacenamiento debe estar en la misma suscripción que el servicio en la nube que se está implementando.</span><span class="sxs-lookup"><span data-stu-id="3f72f-113">For this to work, the storage account needs to be in the same subscription as the Cloud Service being deployed.</span></span>

<span data-ttu-id="3f72f-114">A partir de Azure SDK 2.6, los archivos de configuración de extensión generados por la salida de destino de publicación de MSBuild incluirán el nombre de la cuenta de almacenamiento en función de la cadena de configuración de diagnóstico que se haya especificado en el archivo de configuración de servicio (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="3f72f-114">From Azure SDK 2.6 onward the extension configuration files generated by the MSBuild publish target output will include the storage account name based on the diagnostics configuration string specified in the service configuration file (.cscfg).</span></span> <span data-ttu-id="3f72f-115">El script siguiente muestra cómo analizar los archivos de configuración de extensión desde la salida de destino de publicación y cómo configurar la extensión de diagnóstico de cada rol al implementar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="3f72f-115">The script below shows you how to parse the Extension configuration files from the publish target output and configure diagnostics extension for each role when deploying the cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find the Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find the RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

<span data-ttu-id="3f72f-116">Visual Studio Online usa un enfoque similar para las implementaciones automatizadas de servicios en la nube con la extensión de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3f72f-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with the diagnostics extension.</span></span> <span data-ttu-id="3f72f-117">Consulte [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) para obtener un ejemplo completo.</span><span class="sxs-lookup"><span data-stu-id="3f72f-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="3f72f-118">Si no se ha especificado el parámetro `StorageAccount` en la configuración de diagnóstico, es necesario pasar el parámetro *StorageAccountName* al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f72f-118">If no `StorageAccount` was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="3f72f-119">Si no se ha especificado el parámetro *StorageAccountName* , el cmdlet siempre usará la cuenta de almacenamiento especificada en el parámetro y no la especificada en el archivo de configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3f72f-119">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="3f72f-120">Si la cuenta de almacenamiento de diagnóstico está en una suscripción distinta que el servicio en la nube, es necesario pasar explícitamente los parámetros *StorageAccountName* y *StorageAccountKey* al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f72f-120">If the diagnostics storage account is in a different subscription from the Cloud Service, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="3f72f-121">El parámetro *StorageAccountKey* no es necesario cuando la cuenta de almacenamiento de diagnóstico está en la misma suscripción, ya que el cmdlet puede consultar automáticamente y establecer el valor de clave cuando se habilita la extensión de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3f72f-121">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="3f72f-122">Sin embargo, si la cuenta de almacenamiento de diagnóstico está en una suscripción diferente, es posible que el cmdlet no pueda obtener la clave automáticamente y que sea necesario especificar explícitamente la clave mediante el parámetro *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="3f72f-122">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="3f72f-123">Habilitar la extensión de diagnóstico en un servicio en la nube existente</span><span class="sxs-lookup"><span data-stu-id="3f72f-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="3f72f-124">Puede usar el cmdlet [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) para habilitar o actualizar la configuración de diagnóstico en un servicio en la nube que ya se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="3f72f-124">You can use the [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to enable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="3f72f-125">Obtener la configuración actual de la extensión de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="3f72f-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="3f72f-126">Use el cmdlet [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) para obtener la configuración actual de diagnósticos para un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="3f72f-126">Use the [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to get the current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="3f72f-127">Eliminar la extensión de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="3f72f-127">Remove diagnostics extension</span></span>
<span data-ttu-id="3f72f-128">Para desactivar el diagnóstico en un servicio en la nube, puede usar el cmdlet [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="3f72f-128">To turn off diagnostics on a cloud service you can use the [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="3f72f-129">Si ha habilitado la extensión de diagnóstico mediante *Set-AzureServiceDiagnosticsExtension* o *New-AzureServiceDiagnosticsExtensionConfig* sin el parámetro *Role*, podrá eliminar la extensión mediante *Remove-AzureServiceDiagnosticsExtension* sin el parámetro *Role*.</span><span class="sxs-lookup"><span data-stu-id="3f72f-129">If you enabled the diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or the *New-AzureServiceDiagnosticsExtensionConfig* without the *Role* parameter then you can remove the extension using *Remove-AzureServiceDiagnosticsExtension* without the *Role* parameter.</span></span> <span data-ttu-id="3f72f-130">Si se ha usado el parámetro *Role* al habilitar la extensión, entonces se debe utilizar también al quitar la extensión.</span><span class="sxs-lookup"><span data-stu-id="3f72f-130">If the *Role* parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="3f72f-131">Para quitar la extensión de diagnóstico de cada rol individual:</span><span class="sxs-lookup"><span data-stu-id="3f72f-131">To remove the diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="3f72f-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f72f-132">Next Steps</span></span>
* <span data-ttu-id="3f72f-133">Para obtener orientación adicional sobre el uso de diagnósticos de Azure y otras técnicas para solucionar problemas, consulte [Habilitación de diagnósticos en Servicios en la nube y Máquinas virtuales de Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3f72f-133">For additional guidance on using Azure diagnostics and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="3f72f-134">En el [Esquema de configuración de diagnósticos](https://msdn.microsoft.com/library/azure/dn782207.aspx) se explican las distintas opciones de configuración xml para la extensión de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="3f72f-134">The [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains the various xml configurations options for the diagnostics extension.</span></span>
* <span data-ttu-id="3f72f-135">Para obtener información sobre cómo habilitar la extensión de diagnósticos para las máquinas virtuales, consulte [Crear una máquina virtual de Windows con supervisión y diagnóstico mediante la plantilla de Administrador de recursos de Azure](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="3f72f-135">To learn how to enable the diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
