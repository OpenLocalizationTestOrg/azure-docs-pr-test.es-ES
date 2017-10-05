---
title: "Uso de Azure PowerShell para habilitar diagnósticos en una máquina virtual Windows | Microsoft Docs"
services: virtual-machines-windows
documentationcenter: 
description: "Aprenda a usar PowerShell para habilitar Diagnósticos de Azure en una máquina virtual con Windows"
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
ms.openlocfilehash: d0be4a712657edfc516c5f32e66519f5d9486728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="c6800-103">Uso de PowerShell para habilitar Diagnósticos de Azure en una máquina virtual con Windows</span><span class="sxs-lookup"><span data-stu-id="c6800-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="c6800-104">Diagnósticos de Azure es la funcionalidad de Azure que habilita la recopilación de datos de diagnóstico en una aplicación implementada.</span><span class="sxs-lookup"><span data-stu-id="c6800-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="c6800-105">Puede usar la extensión de diagnósticos para recopilar datos de diagnóstico como registros de aplicaciones o contadores de rendimiento de una máquina virtual (VM) de Azure con Windows.</span><span class="sxs-lookup"><span data-stu-id="c6800-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="c6800-106">En este artículo se describe cómo usar Windows PowerShell para habilitar la extensión de diagnósticos para una VM.</span><span class="sxs-lookup"><span data-stu-id="c6800-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span></span> <span data-ttu-id="c6800-107">Para conocer los requisitos previos necesarios para este artículo, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="c6800-107">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a><span data-ttu-id="c6800-108">Habilite la extensión de diagnósticos si usa el modelo de implementación del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="c6800-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span></span>
<span data-ttu-id="c6800-109">Puede habilitar la extensión de diagnósticos al crear una VM de Windows a través del modelo de implementación del Administrador de recursos de Azure añadiendo la configuración de extensiones a la plantilla del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c6800-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span></span> <span data-ttu-id="c6800-110">Vea [Creación de una máquina virtual de Windows con supervisión y diagnóstico mediante la plantilla de Azure Resource Manager](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6800-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c6800-111">Para habilitar la extensión de diagnósticos en una VM existente creada mediante el modelo de implementación de Resource Manager, puede usar el cmdlet de PowerShell [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="c6800-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="c6800-112">*$diagnosticsconfig_path* es la ruta de acceso del archivo que contiene la configuración de diagnóstico en XML como se describe en el [ejemplo](#sample-diagnostics-configuration) a continuación.</span><span class="sxs-lookup"><span data-stu-id="c6800-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="c6800-113">Si especifica el archivo de configuración de diagnósticos de un elemento **StorageAccount** con un nombre de cuenta de almacenamiento, el script *AzureRMVMDiagnosticsExtension conjunto* establecerá automáticamente la extensión de diagnósticos para enviar datos de diagnóstico a esa cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c6800-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span></span> <span data-ttu-id="c6800-114">Para que esto funcione, la cuenta de almacenamiento necesita estar en la misma suscripción que la VM.</span><span class="sxs-lookup"><span data-stu-id="c6800-114">For this to work, the storage account needs to be in the same subscription as the VM.</span></span>

<span data-ttu-id="c6800-115">Si no se ha especificado el parámetro **StorageAccount** en la configuración de diagnóstico, es necesario pasar el parámetro *StorageAccountName* al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c6800-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="c6800-116">Si no se ha especificado el parámetro *StorageAccountName* , el cmdlet siempre usará la cuenta de almacenamiento especificada en el parámetro y no la especificada en el archivo de configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c6800-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="c6800-117">Si la cuenta de almacenamiento de diagnóstico está en una suscripción distinta que la VM, es necesario pasar explícitamente los parámetros *StorageAccountName* y *StorageAccountKey* al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c6800-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="c6800-118">El parámetro *StorageAccountKey* no es necesario cuando la cuenta de almacenamiento de diagnóstico está en la misma suscripción, ya que el cmdlet puede consultar automáticamente y establecer el valor de clave cuando se habilita la extensión de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c6800-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="c6800-119">Sin embargo, si la cuenta de almacenamiento de diagnóstico está en una suscripción diferente, es posible que el cmdlet no pueda obtener la clave automáticamente y que sea necesario especificar explícitamente la clave mediante el parámetro *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="c6800-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="c6800-120">Una vez habilitada la extensión de diagnósticos en una VM, puede obtener la configuración actual mediante el cmdlet [AzureRMVmDiagnosticsExtension Get](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="c6800-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="c6800-121">El cmdlet devuelve *PublicSettings*, que contiene la configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c6800-121">The cmdlet returns *PublicSettings*, which contains the diagnostics configuration.</span></span> <span data-ttu-id="c6800-122">Hay dos tipos de configuraciones compatibles: WadCfg y xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="c6800-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="c6800-123">WadCfg es la configuración JSON y xmlCfg es la configuración XML en formato con codificación Base64.</span><span class="sxs-lookup"><span data-stu-id="c6800-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="c6800-124">Para leer el archivo XML, es necesario descodificarlo.</span><span class="sxs-lookup"><span data-stu-id="c6800-124">To read the XML, you need to decode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="c6800-125">El cmdlet [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) puede usarse para quitar la extensión de diagnósticos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6800-125">The [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used to remove the diagnostics extension from the VM.</span></span>  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a><span data-ttu-id="c6800-126">Habilite la extensión de diagnósticos si usa el modelo de implementación clásico</span><span class="sxs-lookup"><span data-stu-id="c6800-126">Enable the diagnostics extension if you use the classic deployment model</span></span>
<span data-ttu-id="c6800-127">Puede usar el cmdlet [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) para habilitar la extensión de diagnósticos en una VM creada mediante el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="c6800-127">You can use the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span></span> <span data-ttu-id="c6800-128">En el ejemplo siguiente se muestra cómo crear una nueva VM mediante el modelo de implementación clásica con la extensión de diagnósticos habilitada.</span><span class="sxs-lookup"><span data-stu-id="c6800-128">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="c6800-129">Para habilitar la extensión de diagnósticos en una VM existente creada mediante el modelo de implementación clásica, use el cmdlet [Get-AzureVM](/powershell/module/azure/get-azurevm) en primer lugar para obtener la configuración de VM.</span><span class="sxs-lookup"><span data-stu-id="c6800-129">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet to get the VM configuration.</span></span> <span data-ttu-id="c6800-130">A continuación, actualice la configuración de VM para incluir la extensión de diagnósticos mediante el cmdlet [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="c6800-130">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="c6800-131">Por último, aplique la configuración actualizada a la VM mediante [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="c6800-131">Finally, apply the updated configuration to the VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="c6800-132">Configuración de diagnósticos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c6800-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="c6800-133">Se puede utilizar el siguiente XML para la configuración pública de diagnósticos con los scripts anteriores.</span><span class="sxs-lookup"><span data-stu-id="c6800-133">The following XML can be used for the diagnostics public configuration with the above scripts.</span></span> <span data-ttu-id="c6800-134">Esta configuración de ejemplo transferirá diversos contadores de rendimiento a la cuenta de almacenamiento de información de diagnósticos junto con los errores de la aplicación, seguridad y canales del sistema en los registros de eventos de Windows y los errores de los registros de infraestructura de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c6800-134">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span></span>

<span data-ttu-id="c6800-135">La configuración debe actualizarse para incluir lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c6800-135">The configuration needs to be updated to include the following:</span></span>

* <span data-ttu-id="c6800-136">El atributo *resourceID* del elemento **Métricas** tiene que actualizarse con el identificador de recurso de la VM.</span><span class="sxs-lookup"><span data-stu-id="c6800-136">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span></span>
  
  * <span data-ttu-id="c6800-137">El identificador de recursos puede crearse mediante el siguiente patrón: "/subscriptions/{*Identificador de suscripción para la suscripción con la VM*}/resourceGroups/{*Nombre del grupo de recursos para la VM*}/providers/Microsoft.Compute/virtualMachines/{*Nombre de la VM*}".</span><span class="sxs-lookup"><span data-stu-id="c6800-137">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span></span>
  * <span data-ttu-id="c6800-138">Por ejemplo, si el identificador de suscripción para la suscripción donde se está ejecutando la VM es **11111111-1111-1111-1111-111111111111**, el nombre del grupo de recursos para el grupo de recursos es **MyResourceGroup** y el nombre de la VM es**MyWindowsVM**, el valor de *resourceID* sería:</span><span class="sxs-lookup"><span data-stu-id="c6800-138">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="c6800-139">Para obtener más información sobre cómo se generan las métricas según la configuración de las métricas y los contadores de rendimiento, consulte la [tabla de métricas de Diagnósticos de Azure de almacenamiento](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="c6800-139">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="c6800-140">El elemento **StorageAccount** tiene que actualizarse con el nombre de la cuenta de almacenamiento de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="c6800-140">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span></span>
  
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
        <Metrics resourceId="(Update with resource ID for the VM)" >
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

## <a name="next-steps"></a><span data-ttu-id="c6800-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6800-141">Next steps</span></span>
* <span data-ttu-id="c6800-142">Para obtener orientación adicional sobre el uso de la funcionalidad Diagnósticos de Azure y otras técnicas para solucionar problemas, consulte [Habilitación de diagnósticos en Servicios en la nube y Máquinas virtuales de Azure](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="c6800-142">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="c6800-143">[Esquema de configuración de diagnósticos](https://msdn.microsoft.com/library/azure/mt634524.aspx) se explican las distintas opciones de configuración XML para la extensión de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="c6800-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span></span>

