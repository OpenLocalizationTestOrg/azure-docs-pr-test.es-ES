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
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Usar el diagnóstico de Azure de tooenable de PowerShell en una máquina virtual con Windows
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Diagnósticos de Azure es la capacidad de hello dentro de Azure que habilita la recopilación de Hola de datos de diagnóstico en una aplicación implementada. Puede usar Hola diagnósticos extensión toocollect datos de diagnóstico como registros de la aplicación o los contadores de rendimiento de una máquina virtual Azure (VM) que ejecuta Windows. Este artículo describe cómo toouse Windows PowerShell tooenable Hola extensión de diagnósticos para una máquina virtual. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) de requisitos previos de hello necesarios para este artículo.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Habilitar la extensión de diagnósticos de hello si usa el modelo de implementación del Administrador de recursos de Hola
Puede habilitar la extensión de diagnósticos de Hola durante la creación de una máquina virtual de Windows a través del modelo de implementación de hello Azure Resource Manager mediante la adición de la plantilla de administrador de recursos de toohello de configuración de extensión de Hola. Vea [crear una máquina virtual de Windows con la supervisión y el diagnóstico mediante hello Azure Resource Manager plantilla](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

extensión de diagnósticos de hello tooenable en una máquina virtual existente creada mediante el modelo de implementación del Administrador de recursos de hello, puede usar hello [AzureRMVMDiagnosticsExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) cmdlet de PowerShell tal y como se muestra a continuación.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* es Hola ruta toohello archivo que contiene la configuración de diagnóstico de hello en XML, como se describe en hello [ejemplo](#sample-diagnostics-configuration) a continuación.  

Si especifica el archivo de configuración de diagnósticos de hello un **StorageAccount** elemento con un nombre de cuenta de almacenamiento, a continuación, Hola *AzureRMVMDiagnosticsExtension conjunto* script establecerá automáticamente Hola cuenta de almacenamiento de la toothat de datos de diagnóstico de toosend con diagnósticos extensión. Para este toowork debe toobe en cuenta de almacenamiento de Hola Hola misma suscripción como Hola máquina virtual.

Si no hay ningún **StorageAccount** se especificó en la configuración de diagnóstico de hello, deberá toopass en hello *StorageAccountName* parámetro toohello cmdlet. Si hello *StorageAccountName* se especifica el parámetro, a continuación, usará siempre cuenta de almacenamiento de Hola que se especifica en el parámetro hello y no Hola uno que se especifica en el archivo de configuración de diagnósticos de Hola Hola cmdlet.

Si pasan Hola diagnósticos Hola cuenta de almacenamiento está en una suscripción diferente de Hola de máquina virtual, deberá tooexplicitly *StorageAccountName* y *StorageAccountKey* parámetros toohello cmdlet. Hola *StorageAccountKey* parámetro no es necesario cuando diagnósticos de hello cuenta de almacenamiento está en Hola misma suscripción, como Hola cmdlet automáticamente puede consultar y establecer el valor de clave de hello al habilitar la extensión de diagnósticos de Hola. Sin embargo, si hello es la cuenta de almacenamiento de información de diagnóstico en una suscripción diferente, a continuación, Hola cmdlet podría no ser capaz de tooget clave de hello automáticamente y debe tooexplicitly especificar clave de Hola a través de hello *StorageAccountKey* parámetro.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Una vez habilitada la extensión de diagnósticos de hello en una máquina virtual, puede obtener la configuración actual de hello mediante hello [AzureRMVmDiagnosticsExtension Get](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Hello cmdlet devuelve *PublicSettings*, que contiene la configuración de diagnóstico de Hola. Hay dos tipos de configuraciones compatibles: WadCfg y xmlCfg. WadCfg es la configuración JSON y xmlCfg es la configuración XML en formato con codificación Base64. tooread Hola XML, deberá toodecode lo.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Hola [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet puede ser la extensión de diagnósticos de hello tooremove usado de hello máquina virtual.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Habilitar la extensión de diagnósticos de hello si usa el modelo de implementación clásica de Hola
Puede usar hello [AzureVMDiagnosticsExtension conjunto](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable una extensión de diagnósticos en una máquina virtual que cree mediante el modelo de implementación clásica de Hola. Hello en el ejemplo siguiente se muestra cómo toocreate una nueva máquina virtual a través del modelo de implementación clásica de hello con extensión de diagnósticos de hello habilita.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

extensión de diagnósticos de hello tooenable en una máquina virtual existente creada mediante el modelo de implementación clásica de hello, primer Hola de uso [Get-AzureVM](/powershell/module/azure/get-azurevm) configuración de máquina virtual de cmdlet tooget Hola. A continuación, actualizar extensión de diagnósticos de hello VM configuración tooinclude hello mediante hello [AzureVMDiagnosticsExtension conjunto](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet. Por último, aplique Hola actualizar configuración toohello VM mediante el uso de [Update-AzureVM](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>Configuración de diagnósticos de ejemplo
Hola que XML siguiente puede utilizarse para la configuración pública de diagnósticos de hello con hello por encima de las secuencias de comandos. Esta configuración de ejemplo transferirá diversos rendimiento contadores toohello diagnósticos cuenta de almacenamiento, junto con los errores de aplicación hello, seguridad y los canales de sistema en registros de eventos de Windows hello y cualquier error de diagnóstico de Hola registros de infraestructura.

configuración de Hello debe siguiente Hola de toobe tooinclude actualizada:

* Hola *resourceID* atributo de hello **métricas** elemento necesita toobe actualizada con Id. de recurso de Hola para hello máquina virtual.
  
  * Hola identificador puede crearse mediante Hola sigue el patrón de recurso: "/ subscriptions / {*Id. de suscripción para la suscripción de hello con hello VM*} / ResourceGroups / {*nombre de grupo de recursos de Hola para hello VM*} / providers/Microsoft.Compute/virtualMachines/ {*Hola nombre de máquina virtual*} ".
  * Por ejemplo, si hello Id. de suscripción para la suscripción de Hola donde hello máquina virtual se está ejecutando es **11111111-1111-1111-1111-111111111111**, es el nombre del grupo de recursos de hello para el grupo de recursos de hello **MyResourceGroup**, y Hola nombre de máquina virtual es **MyWindowsVM**, a continuación, Hola valor para *resourceID* sería:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Para obtener más información sobre cómo métricas son los contadores de rendimiento de hello según generado y configuración de métricas, vea [tabla de métricas de diagnóstico de Azure en almacenamiento](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* Hola **StorageAccount** elemento necesita toobe actualizar con hello nombre de cuenta de almacenamiento de diagnósticos de Hola.
  
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

## <a name="next-steps"></a>Pasos siguientes
* Para obtener orientación adicional acerca del uso de la capacidad de diagnóstico de Azure de Hola y otros problemas de tootroubleshoot técnicas, consulte [habilitar diagnósticos en servicios en la nube y máquinas virtuales](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [Esquema de configuración de diagnósticos](https://msdn.microsoft.com/library/azure/mt634524.aspx) explica Hola opciones diversas configuraciones de XML para extensión de diagnósticos de Hola.

