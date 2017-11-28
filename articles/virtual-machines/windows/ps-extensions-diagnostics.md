---
title: "aaaUse diagnósticos de Azure PowerShell tooenable en una máquina virtual de Windows | Documentos de Microsoft"
services: virtual-machines-windows
documentationcenter: 
description: "Obtenga información acerca de cómo toouse PowerShell tooenable diagnósticos de Azure en una máquina virtual con Windows"
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="518bd-103">Usar el diagnóstico de Azure de tooenable de PowerShell en una máquina virtual con Windows</span><span class="sxs-lookup"><span data-stu-id="518bd-103">Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="518bd-104">Diagnósticos de Azure es la capacidad de hello dentro de Azure que habilita la recopilación de Hola de datos de diagnóstico en una aplicación implementada.</span><span class="sxs-lookup"><span data-stu-id="518bd-104">Azure Diagnostics is hello capability within Azure that enables hello collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="518bd-105">Puede usar Hola diagnósticos extensión toocollect datos de diagnóstico como registros de la aplicación o los contadores de rendimiento de una máquina virtual Azure (VM) que ejecuta Windows.</span><span class="sxs-lookup"><span data-stu-id="518bd-105">You can use hello diagnostics extension toocollect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="518bd-106">Este artículo describe cómo toouse Windows PowerShell tooenable Hola extensión de diagnósticos para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="518bd-106">This article describes how toouse Windows PowerShell tooenable hello diagnostics extension for a VM.</span></span> <span data-ttu-id="518bd-107">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) de requisitos previos de hello necesarios para este artículo.</span><span class="sxs-lookup"><span data-stu-id="518bd-107">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a><span data-ttu-id="518bd-108">Habilitar la extensión de diagnósticos de hello si usa el modelo de implementación del Administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="518bd-108">Enable hello diagnostics extension if you use hello Resource Manager deployment model</span></span>
<span data-ttu-id="518bd-109">Puede habilitar la extensión de diagnósticos de Hola durante la creación de una máquina virtual de Windows a través del modelo de implementación de hello Azure Resource Manager mediante la adición de la plantilla de administrador de recursos de toohello de configuración de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="518bd-109">You can enable hello diagnostics extension while you create a Windows VM through hello Azure Resource Manager deployment model by adding hello extension configuration toohello Resource Manager template.</span></span> <span data-ttu-id="518bd-110">Vea [crear una máquina virtual de Windows con la supervisión y el diagnóstico mediante hello Azure Resource Manager plantilla](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="518bd-110">See [Create a Windows virtual machine with monitoring and diagnostics by using hello Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="518bd-111">extensión de diagnósticos de hello tooenable en una máquina virtual existente creada mediante el modelo de implementación del Administrador de recursos de hello, puede usar hello [AzureRMVMDiagnosticsExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) cmdlet de PowerShell tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="518bd-111">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="518bd-112">*$diagnosticsconfig_path* es Hola ruta toohello archivo que contiene la configuración de diagnóstico de hello en XML, como se describe en hello [ejemplo](#sample-diagnostics-configuration) a continuación.</span><span class="sxs-lookup"><span data-stu-id="518bd-112">*$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML, as described in hello [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="518bd-113">Si especifica el archivo de configuración de diagnósticos de hello un **StorageAccount** elemento con un nombre de cuenta de almacenamiento, a continuación, Hola *AzureRMVMDiagnosticsExtension conjunto* script establecerá automáticamente Hola cuenta de almacenamiento de la toothat de datos de diagnóstico de toosend con diagnósticos extensión.</span><span class="sxs-lookup"><span data-stu-id="518bd-113">If hello diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then hello *Set-AzureRMVMDiagnosticsExtension* script will automatically set hello diagnostics extension toosend diagnostic data toothat storage account.</span></span> <span data-ttu-id="518bd-114">Para este toowork debe toobe en cuenta de almacenamiento de Hola Hola misma suscripción como Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="518bd-114">For this toowork, hello storage account needs toobe in hello same subscription as hello VM.</span></span>

<span data-ttu-id="518bd-115">Si no hay ningún **StorageAccount** se especificó en la configuración de diagnóstico de hello, deberá toopass en hello *StorageAccountName* parámetro toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="518bd-115">If no **StorageAccount** was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="518bd-116">Si hello *StorageAccountName* se especifica el parámetro, a continuación, usará siempre cuenta de almacenamiento de Hola que se especifica en el parámetro hello y no Hola uno que se especifica en el archivo de configuración de diagnósticos de Hola Hola cmdlet.</span><span class="sxs-lookup"><span data-stu-id="518bd-116">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="518bd-117">Si pasan Hola diagnósticos Hola cuenta de almacenamiento está en una suscripción diferente de Hola de máquina virtual, deberá tooexplicitly *StorageAccountName* y *StorageAccountKey* parámetros toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="518bd-117">If hello diagnostics storage account is in a different subscription from hello VM, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="518bd-118">Hola *StorageAccountKey* parámetro no es necesario cuando diagnósticos de hello cuenta de almacenamiento está en Hola misma suscripción, como Hola cmdlet automáticamente puede consultar y establecer el valor de clave de hello al habilitar la extensión de diagnósticos de Hola.</span><span class="sxs-lookup"><span data-stu-id="518bd-118">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="518bd-119">Sin embargo, si hello es la cuenta de almacenamiento de información de diagnóstico en una suscripción diferente, a continuación, Hola cmdlet podría no ser capaz de tooget clave de hello automáticamente y debe tooexplicitly especificar clave de Hola a través de hello *StorageAccountKey* parámetro.</span><span class="sxs-lookup"><span data-stu-id="518bd-119">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="518bd-120">Una vez habilitada la extensión de diagnósticos de hello en una máquina virtual, puede obtener la configuración actual de hello mediante hello [AzureRMVmDiagnosticsExtension Get](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="518bd-120">Once hello diagnostics extension is enabled on a VM, you can get hello current settings by using hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="518bd-121">Hello cmdlet devuelve *PublicSettings*, que contiene la configuración de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="518bd-121">hello cmdlet returns *PublicSettings*, which contains hello diagnostics configuration.</span></span> <span data-ttu-id="518bd-122">Hay dos tipos de configuraciones compatibles: WadCfg y xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="518bd-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="518bd-123">WadCfg es la configuración JSON y xmlCfg es la configuración XML en formato con codificación Base64.</span><span class="sxs-lookup"><span data-stu-id="518bd-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="518bd-124">tooread Hola XML, deberá toodecode lo.</span><span class="sxs-lookup"><span data-stu-id="518bd-124">tooread hello XML, you need toodecode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="518bd-125">Hola [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet puede ser la extensión de diagnósticos de hello tooremove usado de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="518bd-125">hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used tooremove hello diagnostics extension from hello VM.</span></span>  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a><span data-ttu-id="518bd-126">Habilitar la extensión de diagnósticos de hello si usa el modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="518bd-126">Enable hello diagnostics extension if you use hello classic deployment model</span></span>
<span data-ttu-id="518bd-127">Puede usar hello [AzureVMDiagnosticsExtension conjunto](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable una extensión de diagnósticos en una máquina virtual que cree mediante el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="518bd-127">You can use hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable a diagnostics extension on a VM that you create through hello classic deployment model.</span></span> <span data-ttu-id="518bd-128">Hello en el ejemplo siguiente se muestra cómo toocreate una nueva máquina virtual a través del modelo de implementación clásica de hello con extensión de diagnósticos de hello habilita.</span><span class="sxs-lookup"><span data-stu-id="518bd-128">hello following example shows how toocreate a new VM through hello classic deployment model with hello diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="518bd-129">extensión de diagnósticos de hello tooenable en una máquina virtual existente creada mediante el modelo de implementación clásica de hello, primer Hola de uso [Get-AzureVM](/powershell/module/azure/get-azurevm) configuración de máquina virtual de cmdlet tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="518bd-129">tooenable hello diagnostics extension on an existing VM that was created through hello classic deployment model, first use hello [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM configuration.</span></span> <span data-ttu-id="518bd-130">A continuación, actualizar extensión de diagnósticos de hello VM configuración tooinclude hello mediante hello [AzureVMDiagnosticsExtension conjunto](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="518bd-130">Then update hello VM configuration tooinclude hello diagnostics extension by using hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="518bd-131">Por último, aplique Hola actualizar configuración toohello VM mediante el uso de [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="518bd-131">Finally, apply hello updated configuration toohello VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="518bd-132">Configuración de diagnósticos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="518bd-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="518bd-133">Hola que XML siguiente puede utilizarse para la configuración pública de diagnósticos de hello con hello por encima de las secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="518bd-133">hello following XML can be used for hello diagnostics public configuration with hello above scripts.</span></span> <span data-ttu-id="518bd-134">Esta configuración de ejemplo transferirá diversos rendimiento contadores toohello diagnósticos cuenta de almacenamiento, junto con los errores de aplicación hello, seguridad y los canales de sistema en registros de eventos de Windows hello y cualquier error de diagnóstico de Hola registros de infraestructura.</span><span class="sxs-lookup"><span data-stu-id="518bd-134">This sample configuration will transfer various performance counters toohello diagnostics storage account, along with errors from hello application, security, and system channels in hello Windows event logs and any errors from hello diagnostics infrastructure logs.</span></span>

<span data-ttu-id="518bd-135">configuración de Hello debe siguiente Hola de toobe tooinclude actualizada:</span><span class="sxs-lookup"><span data-stu-id="518bd-135">hello configuration needs toobe updated tooinclude hello following:</span></span>

* <span data-ttu-id="518bd-136">Hola *resourceID* atributo de hello **métricas** elemento necesita toobe actualizada con Id. de recurso de Hola para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="518bd-136">hello *resourceID* attribute of hello **Metrics** element needs toobe updated with hello resource ID for hello VM.</span></span>
  
  * <span data-ttu-id="518bd-137">Hola identificador puede crearse mediante Hola sigue el patrón de recurso: "/ subscriptions / {*Id. de suscripción para la suscripción de hello con hello VM*} / ResourceGroups / {*nombre de grupo de recursos de Hola para hello VM*} / providers/Microsoft.Compute/virtualMachines/ {*Hola nombre de máquina virtual*} ".</span><span class="sxs-lookup"><span data-stu-id="518bd-137">hello resource ID can be constructed by using hello following pattern: "/subscriptions/{*subscription ID for hello subscription with hello VM*}/resourceGroups/{*hello resourcegroup name for hello VM*}/providers/Microsoft.Compute/virtualMachines/{*hello VM Name*}".</span></span>
  * <span data-ttu-id="518bd-138">Por ejemplo, si hello Id. de suscripción para la suscripción de Hola donde hello máquina virtual se está ejecutando es **11111111-1111-1111-1111-111111111111**, es el nombre del grupo de recursos de hello para el grupo de recursos de hello **MyResourceGroup**, y Hola nombre de máquina virtual es **MyWindowsVM**, a continuación, Hola valor para *resourceID* sería:</span><span class="sxs-lookup"><span data-stu-id="518bd-138">For example, if hello subscription ID for hello subscription where hello VM is running is **11111111-1111-1111-1111-111111111111**, hello resource group name for hello resource group is **MyResourceGroup**, and hello VM Name is **MyWindowsVM**, then hello value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="518bd-139">Para obtener más información sobre cómo métricas son los contadores de rendimiento de hello según generado y configuración de métricas, vea [tabla de métricas de diagnóstico de Azure en almacenamiento](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="518bd-139">For more information on how metrics are generated based on hello performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="518bd-140">Hola **StorageAccount** elemento necesita toobe actualizar con hello nombre de cuenta de almacenamiento de diagnósticos de Hola.</span><span class="sxs-lookup"><span data-stu-id="518bd-140">hello **StorageAccount** element needs toobe updated with hello name of hello diagnostics storage account.</span></span>
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for hello VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a><span data-ttu-id="518bd-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="518bd-141">Next steps</span></span>
* <span data-ttu-id="518bd-142">Para obtener orientación adicional acerca del uso de la capacidad de diagnóstico de Azure de Hola y otros problemas de tootroubleshoot técnicas, consulte [habilitar diagnósticos en servicios en la nube y máquinas virtuales](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="518bd-142">For additional guidance on using hello Azure Diagnostics capability and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="518bd-143">[Esquema de configuración de diagnósticos](https://msdn.microsoft.com/library/azure/mt634524.aspx) explica Hola opciones diversas configuraciones de XML para extensión de diagnósticos de Hola.</span><span class="sxs-lookup"><span data-stu-id="518bd-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains hello various XML configurations options for hello diagnostics extension.</span></span>

