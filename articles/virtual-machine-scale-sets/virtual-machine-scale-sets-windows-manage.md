---
title: "aaaManage máquinas virtuales en un conjunto de escala de máquinas virtuales | Documentos de Microsoft"
description: "Administración de máquinas de un conjunto de escalado de máquinas virtuales mediante Azure PowerShell."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>Administración de máquinas virtuales en un conjunto de escalado de máquinas virtuales
Usar tareas de hello en este artículo toomanage máquinas en el conjunto de escalas de máquina virtual.

La mayoría de tareas de Hola que implican la administración de una máquina virtual en un conjunto de escala, debe tener conocimientos Hola Id. de instancia de máquina de Hola que desea toomanage. Puede usar [Explorador de recursos de Azure](https://resources.azure.com) toofind Hola el Id. de instancia de una máquina virtual en un conjunto de escala. También utilizar estado de hello tooverify de explorador de recursos de tareas de Hola que finalizar.

Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y tooyour cuenta de inicio de sesión.

## <a name="display-information-about-a-scale-set"></a>Visualización de información sobre un conjunto de escalado
Puede obtener información general sobre un conjunto de escala, que también es una vista de instancia de hello tooas que se hace referencia. O bien, puede obtener información más específica, como información sobre los recursos de hello en el conjunto de escalas de Hola.

Reemplace Hola entre comillas los valores con nombre de Hola o el grupo de recursos y la escala establecer y, a continuación, ejecute el comando de hello:

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

Entonces, se devuelve algo parecido a lo siguiente:

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de recursos de grupo y la escala. Reemplace  *#*  con el identificador de instancia de Hola de máquina virtual de Hola que desee tooget información acerca de y, a continuación, ejecútelo:

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Devuelve algo parecido al siguiente ejemplo:

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a>Inicio de una máquina virtual de un conjunto de escalado
Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de recursos de grupo y la escala. Reemplace  *#*  con el identificador hello de máquina virtual de Hola que desee toostart y, a continuación, ejecútelo:

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

En el Explorador de recursos, podemos ver que Hola estado de instancia de hello es **ejecutando**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

Puede iniciar todas las máquinas virtuales de hello en conjunto si no utiliza el parámetro - InstanceId de hello de escalas de Hola.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>Detención de una máquina virtual de un conjunto de escalado
Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de recursos de grupo y la escala. Reemplace  *#*  con el identificador hello de máquina virtual de Hola que desee toostop y, a continuación, ejecútelo:

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

En el Explorador de recursos, podemos ver que Hola estado de instancia de hello es **desasignado**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

toostop una máquina virtual y no desasignarla, use el parámetro - StayProvisioned de hello. Puede detener todas las máquinas virtuales de Hola Hola establecido si no utiliza el parámetro - InstanceId de hello.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>Reinicio de una máquina virtual de un conjunto de escalado
Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de escala de hello y grupo de recursos. Reemplace  *#*  con el identificador hello de máquina virtual de Hola que desee toorestart y, a continuación, ejecútelo:

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Puede reiniciar todas las máquinas virtuales de Hola Hola establecido si no utiliza el parámetro - InstanceId de hello.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>Eliminación de una máquina virtual de un conjunto de escalado
Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de escala de hello y grupo de recursos. Reemplace  *#*  con el identificador hello de máquina virtual de Hola que desee tooremove y, a continuación, ejecútelo:  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

Puede quitar el conjunto de escalas de máquina virtual de Hola a la vez si no utiliza el parámetro - InstanceId de hello.

## <a name="change-hello-capacity-of-a-scale-set"></a>Capacidad de Hola de cambio de un conjunto de escala
Puede agregar o quitar máquinas virtuales cambiando Hola capacidad de hello conjunto. Obtener conjunto de escalas de Hola que desee toochange, conjunto Hola capacidad toowhat desee toobe y, a continuación, actualizar el conjunto de escalas de Hola con nueva capacidad de Hola. En estos comandos, reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de escala de hello y grupo de recursos.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

Si va a quitar máquinas virtuales de conjunto de escalas de hello, máquinas virtuales de hello con identificadores de más alto de Hola se quitan primero.

