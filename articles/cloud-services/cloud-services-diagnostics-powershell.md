---
title: "aaaEnable diagnósticos en servicios de nube de Azure mediante PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable diagnósticos para la nube services mediante PowerShell"
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
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="a8fea-103">Habilitar el diagnóstico en Servicios en la nube de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8fea-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="a8fea-104">Puede recopilar datos de diagnóstico como registros de aplicaciones, etc. desde un servicio en la nube mediante los contadores de rendimiento Hola extensión de diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8fea-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="a8fea-105">Este artículo describe cómo tooenable Hola extensión de diagnósticos de Azure para un servicio de nube mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8fea-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="a8fea-106">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) de requisitos previos de hello necesarios para este artículo.</span><span class="sxs-lookup"><span data-stu-id="a8fea-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="a8fea-107">Habilitar la extensión de diagnósticos como parte de la implementación de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="a8fea-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="a8fea-108">Este enfoque es el tipo de integración de toocontinuous aplicables de escenarios, donde extensión pueda habilitarse como parte de la implementación de diagnósticos de Hola Hola servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="a8fea-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="a8fea-109">Al crear una nueva implementación del servicio de nube puede habilitar la extensión de diagnósticos de hello pasando hello *ExtensionConfiguration* parámetro toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8fea-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="a8fea-110">Hola *ExtensionConfiguration* parámetro toma una matriz de configuraciones de diagnóstico que pueden crearse con hello [AzureServiceDiagnosticsExtensionConfig New](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8fea-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="a8fea-111">Hello en el ejemplo siguiente se muestra cómo se pueden habilitar los diagnósticos para un servicio de nube con un WebRole y WorkerRole, cada uno con una configuración de diagnóstico diferentes.</span><span class="sxs-lookup"><span data-stu-id="a8fea-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="a8fea-112">Si especifica el archivo de configuración de diagnósticos de hello un `StorageAccount` elemento con un nombre de cuenta de almacenamiento, a continuación, Hola `New-AzureServiceDiagnosticsExtensionConfig` cmdlet usarán automáticamente esa cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a8fea-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="a8fea-113">Para este toowork debe toobe en cuenta de almacenamiento de Hola Hola misma suscripción como Hola servicio en la nube que se está implementando.</span><span class="sxs-lookup"><span data-stu-id="a8fea-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="a8fea-114">De Azure SDK 2.6 publicación archivos de configuración de extensión de hello ulterior generados por hello MSBuild salida del destino incluirá el nombre de la cuenta de almacenamiento hello en función de la cadena de configuración de diagnósticos de hello especificado en el archivo de configuración de servicio (.cscfg) de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8fea-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="a8fea-115">script de Hola a continuación muestra cómo tooparse archivos de configuración de extensión de Hola de Hola resultados de destino de publicación y configurar la extensión de diagnóstico para cada rol al implementar el servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8fea-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
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

<span data-ttu-id="a8fea-116">Visual Studio Online, se usa un enfoque similar para implementaciones automatizadas de servicios en la nube con la extensión de diagnósticos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8fea-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="a8fea-117">Consulte [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) para obtener un ejemplo completo.</span><span class="sxs-lookup"><span data-stu-id="a8fea-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="a8fea-118">Si no hay ningún `StorageAccount` se especificó en la configuración de diagnóstico de hello, deberá toopass en hello *StorageAccountName* parámetro toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8fea-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="a8fea-119">Si hello *StorageAccountName* se especifica el parámetro, a continuación, usará siempre cuenta de almacenamiento de Hola que se especifica en el parámetro hello y no Hola uno que se especifica en el archivo de configuración de diagnósticos de Hola Hola cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8fea-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="a8fea-120">Si pasan Hola diagnósticos Hola cuenta de almacenamiento está en una suscripción diferente de hello servicio en la nube, deberá tooexplicitly *StorageAccountName* y *StorageAccountKey* parámetros cmdlet de toohello.</span><span class="sxs-lookup"><span data-stu-id="a8fea-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="a8fea-121">Hola *StorageAccountKey* parámetro no es necesario cuando diagnósticos de hello cuenta de almacenamiento está en Hola misma suscripción, como Hola cmdlet automáticamente puede consultar y establecer el valor de clave de hello al habilitar la extensión de diagnósticos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8fea-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="a8fea-122">Sin embargo, si hello es la cuenta de almacenamiento de información de diagnóstico en una suscripción diferente, a continuación, Hola cmdlet podría no ser capaz de tooget clave de hello automáticamente y debe tooexplicitly especificar clave de Hola a través de hello *StorageAccountKey* parámetro.</span><span class="sxs-lookup"><span data-stu-id="a8fea-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="a8fea-123">Habilitar la extensión de diagnóstico en un servicio en la nube existente</span><span class="sxs-lookup"><span data-stu-id="a8fea-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="a8fea-124">Puede usar hello [AzureServiceDiagnosticsExtension conjunto](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) configuración de diagnóstico de cmdlet tooenable o actualización en un servicio de nube que ya se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="a8fea-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="a8fea-125">Obtener la configuración actual de la extensión de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="a8fea-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="a8fea-126">Hola de uso [AzureServiceDiagnosticsExtension Get](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget Hola actual configuración de diagnóstico para un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="a8fea-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="a8fea-127">Eliminar la extensión de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="a8fea-127">Remove diagnostics extension</span></span>
<span data-ttu-id="a8fea-128">tooturn desactivar diagnósticos en una nube de servicio se puede usar hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8fea-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="a8fea-129">Si ha habilitado extensión de diagnósticos de hello mediante *conjunto AzureServiceDiagnosticsExtension* o hello *New-AzureServiceDiagnosticsExtensionConfig* sin hello *rol* parámetro, a continuación, se puede quitar extensión hello mediante *Remove-AzureServiceDiagnosticsExtension* sin hello *rol* parámetro.</span><span class="sxs-lookup"><span data-stu-id="a8fea-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="a8fea-130">Si hello *rol* parámetro se utiliza al habilitar la extensión de hello, a continuación, se debe también pueden usarse para quitar la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8fea-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="a8fea-131">extensión de diagnósticos de hello tooremove de cada rol individual:</span><span class="sxs-lookup"><span data-stu-id="a8fea-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="a8fea-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8fea-132">Next Steps</span></span>
* <span data-ttu-id="a8fea-133">Para obtener instrucciones adicionales sobre el uso de diagnósticos de Azure y otros problemas de tootroubleshoot técnicas, consulte [habilitar diagnósticos en servicios en la nube y máquinas virtuales](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="a8fea-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="a8fea-134">Hola [esquema de configuración de diagnósticos](https://msdn.microsoft.com/library/azure/dn782207.aspx) explica Hola opciones diversas configuraciones de xml para extensión de diagnósticos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8fea-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="a8fea-135">toolearn tooenable extensión de diagnósticos de Hola para máquinas virtuales, vea [crear una máquina Virtual de Windows con la supervisión y diagnósticos mediante la plantilla de administrador de recursos de Azure](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="a8fea-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
