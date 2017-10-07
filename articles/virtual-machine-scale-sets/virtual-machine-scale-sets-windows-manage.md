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
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="35889-103">Administración de máquinas virtuales en un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="35889-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="35889-104">Usar tareas de hello en este artículo toomanage máquinas en el conjunto de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="35889-104">Use hello tasks in this article toomanage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="35889-105">La mayoría de tareas de Hola que implican la administración de una máquina virtual en un conjunto de escala, debe tener conocimientos Hola Id. de instancia de máquina de Hola que desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="35889-105">Most of hello tasks that involve managing a virtual machine in a scale set require that you know hello instance ID of hello machine that you want toomanage.</span></span> <span data-ttu-id="35889-106">Puede usar [Explorador de recursos de Azure](https://resources.azure.com) toofind Hola el Id. de instancia de una máquina virtual en un conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="35889-106">You can use [Azure Resource Explorer](https://resources.azure.com) toofind hello instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="35889-107">También utilizar estado de hello tooverify de explorador de recursos de tareas de Hola que finalizar.</span><span class="sxs-lookup"><span data-stu-id="35889-107">You also use Resource Explorer tooverify hello status of hello tasks that you finish.</span></span>

<span data-ttu-id="35889-108">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y tooyour cuenta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="35889-108">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="35889-109">Visualización de información sobre un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="35889-109">Display information about a scale set</span></span>
<span data-ttu-id="35889-110">Puede obtener información general sobre un conjunto de escala, que también es una vista de instancia de hello tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="35889-110">You can get general information about a scale set, which is also referred tooas hello instance view.</span></span> <span data-ttu-id="35889-111">O bien, puede obtener información más específica, como información sobre los recursos de hello en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="35889-111">Or, you can get more specific information, such as information about hello resources in hello scale set.</span></span>

<span data-ttu-id="35889-112">Reemplace Hola entre comillas los valores con nombre de Hola o el grupo de recursos y la escala establecer y, a continuación, ejecute el comando de hello:</span><span class="sxs-lookup"><span data-stu-id="35889-112">Replace hello quoted values with hello name or your resource group and scale set and then run hello command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="35889-113">Entonces, se devuelve algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="35889-113">It returns something like this:</span></span>

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

<span data-ttu-id="35889-114">Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de recursos de grupo y la escala.</span><span class="sxs-lookup"><span data-stu-id="35889-114">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="35889-115">Reemplace  *#*  con el identificador de instancia de Hola de máquina virtual de Hola que desee tooget información acerca de y, a continuación, ejecútelo:</span><span class="sxs-lookup"><span data-stu-id="35889-115">Replace *#* with hello instance identifier of hello virtual machine that you want tooget information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="35889-116">Devuelve algo parecido al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="35889-116">It returns something like this example:</span></span>

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="35889-117">Inicio de una máquina virtual de un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="35889-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="35889-118">Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de recursos de grupo y la escala.</span><span class="sxs-lookup"><span data-stu-id="35889-118">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="35889-119">Reemplace  *#*  con el identificador hello de máquina virtual de Hola que desee toostart y, a continuación, ejecútelo:</span><span class="sxs-lookup"><span data-stu-id="35889-119">Replace *#* with hello identifier of hello virtual machine that you want toostart and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="35889-120">En el Explorador de recursos, podemos ver que Hola estado de instancia de hello es **ejecutando**:</span><span class="sxs-lookup"><span data-stu-id="35889-120">In Resource Explorer, we can see that hello status of hello instance is **running**:</span></span>

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

<span data-ttu-id="35889-121">Puede iniciar todas las máquinas virtuales de hello en conjunto si no utiliza el parámetro - InstanceId de hello de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="35889-121">You can start all hello virtual machines in hello scale set by not using hello -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="35889-122">Detención de una máquina virtual de un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="35889-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="35889-123">Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de recursos de grupo y la escala.</span><span class="sxs-lookup"><span data-stu-id="35889-123">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="35889-124">Reemplace  *#*  con el identificador hello de máquina virtual de Hola que desee toostop y, a continuación, ejecútelo:</span><span class="sxs-lookup"><span data-stu-id="35889-124">Replace *#* with hello identifier of hello virtual machine that you want toostop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="35889-125">En el Explorador de recursos, podemos ver que Hola estado de instancia de hello es **desasignado**:</span><span class="sxs-lookup"><span data-stu-id="35889-125">In Resource Explorer, we can see that hello status of hello instance is **deallocated**:</span></span>

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

<span data-ttu-id="35889-126">toostop una máquina virtual y no desasignarla, use el parámetro - StayProvisioned de hello.</span><span class="sxs-lookup"><span data-stu-id="35889-126">toostop a virtual machine and not deallocate it, use hello -StayProvisioned parameter.</span></span> <span data-ttu-id="35889-127">Puede detener todas las máquinas virtuales de Hola Hola establecido si no utiliza el parámetro - InstanceId de hello.</span><span class="sxs-lookup"><span data-stu-id="35889-127">You can stop all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="35889-128">Reinicio de una máquina virtual de un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="35889-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="35889-129">Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de escala de hello y grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="35889-129">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="35889-130">Reemplace  *#*  con el identificador hello de máquina virtual de Hola que desee toorestart y, a continuación, ejecútelo:</span><span class="sxs-lookup"><span data-stu-id="35889-130">Replace *#* with hello identifier of hello virtual machine that you want toorestart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="35889-131">Puede reiniciar todas las máquinas virtuales de Hola Hola establecido si no utiliza el parámetro - InstanceId de hello.</span><span class="sxs-lookup"><span data-stu-id="35889-131">You can restart all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="35889-132">Eliminación de una máquina virtual de un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="35889-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="35889-133">Reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de escala de hello y grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="35889-133">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="35889-134">Reemplace  *#*  con el identificador hello de máquina virtual de Hola que desee tooremove y, a continuación, ejecútelo:</span><span class="sxs-lookup"><span data-stu-id="35889-134">Replace *#* with hello identifier of hello virtual machine that you want tooremove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="35889-135">Puede quitar el conjunto de escalas de máquina virtual de Hola a la vez si no utiliza el parámetro - InstanceId de hello.</span><span class="sxs-lookup"><span data-stu-id="35889-135">You can remove hello virtual machine scale set all at once by not using hello -InstanceId parameter.</span></span>

## <a name="change-hello-capacity-of-a-scale-set"></a><span data-ttu-id="35889-136">Capacidad de Hola de cambio de un conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="35889-136">Change hello capacity of a scale set</span></span>
<span data-ttu-id="35889-137">Puede agregar o quitar máquinas virtuales cambiando Hola capacidad de hello conjunto.</span><span class="sxs-lookup"><span data-stu-id="35889-137">You can add or remove virtual machines by changing hello capacity of hello set.</span></span> <span data-ttu-id="35889-138">Obtener conjunto de escalas de Hola que desee toochange, conjunto Hola capacidad toowhat desee toobe y, a continuación, actualizar el conjunto de escalas de Hola con nueva capacidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="35889-138">Get hello scale set that you want toochange, set hello capacity toowhat you want it toobe, and then update hello scale set with hello new capacity.</span></span> <span data-ttu-id="35889-139">En estos comandos, reemplace Hola entre comillas los valores con el nombre de Hola de su conjunto de escala de hello y grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="35889-139">In these commands, replace hello quoted values with hello name of your resource group and hello scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="35889-140">Si va a quitar máquinas virtuales de conjunto de escalas de hello, máquinas virtuales de hello con identificadores de más alto de Hola se quitan primero.</span><span class="sxs-lookup"><span data-stu-id="35889-140">If you are removing virtual machines from hello scale set, hello virtual machines with hello highest ids are removed first.</span></span>

