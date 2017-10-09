---
title: "aaaCreate un conjuntos para Windows de máquina Virtual de escala en Azure | Documentos de Microsoft"
description: "Creación e implementación de una aplicación de alta disponibilidad en VM Windows con un conjunto de escalado de máquinas virtuales"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>Creación de un conjunto de escalado de máquinas virtuales e implementación de una aplicación de alta disponibilidad en Windows
Un conjunto de escalas de máquina virtual permite toodeploy y administrar un conjunto de máquinas virtuales idénticos, la escala automática. Puede escalar el número de Hola de máquinas virtuales en el conjunto de escalas de hello manualmente, o definir tooautoscale reglas en función de uso de CPU, la demanda de memoria o el tráfico de red. En este tutorial, implementará un conjunto de escalado de máquinas virtuales en Azure. Aprenderá a:

> [!div class="checklist"]
> * Usar la extensión de Script personalizado de hello toodefine un tooscale de sitio IIS
> * Crear un equilibrador de carga para el conjunto de escalado
> * Crear un conjunto de escalado de máquinas virtuales
> * Aumentar o disminuir el número de Hola de instancias de un conjunto de escala
> * Crear reglas de escalado automático

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="scale-set-overview"></a>Introducción al conjunto de escalado
Conjuntos de escalas de utilizan conceptos similares, tal y como ha aprendido en el tutorial anterior Hola demasiado[crear máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md). Las VM de un conjunto de escalado se distribuyen entre los dominios de error y actualización como las VM en un conjunto de disponibilidad.

Las máquinas virtuales se crean según sea necesario en un conjunto de escalado. Definir toocontrol de reglas de escalado automático cómo y cuándo se agregan o se quitan del conjunto de escalas de hello las máquinas virtuales. Estas reglas se pueden desencadenar en función de métricas como la carga de la CPU, el uso de la memoria o el tráfico de red.

Escala establece compatibilidad con seguridad too1, 000 máquinas virtuales cuando se usa una imagen de la plataforma Windows Azure. Para las cargas de trabajo con importantes de instalación o los requisitos de personalización de máquina virtual, es recomendable demasiado[crear una imagen de máquina virtual personalizada](tutorial-custom-images.md). Puede crear las máquinas virtuales de too100 en una escala establecida cuando se usa una imagen personalizada.


## <a name="create-an-app-tooscale"></a>Crear una aplicación tooscale
Antes de poder crear un conjunto de escalado, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupAutomate* en hello *EastUS* ubicación:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

En un tutorial anterior, ha aprendido cómo demasiado[configuración de máquina virtual automatizar](tutorial-automate-vm-deployment.md) utilizando Hola extensión de Script personalizado. Crear la configuración de un conjunto de escala, a continuación, aplicar un tooinstall de extensión de Script personalizado y configurar IIS:

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a>Creación de un equilibrador de carga de escalado
Un equilibrador de carga de Azure es un equilibrador de carga de nivel 4 (TCP, UDP) que proporciona una alta disponibilidad mediante la distribución del tráfico entrante entre máquinas virtuales con un estado correcto. Un sondeo de estado de equilibrador de carga supervisa un puerto determinado en cada máquina virtual y sólo distribuye el tráfico tooan VM operativa. Para obtener más información, vea el tutorial siguiente hello en [cómo tooload equilibrar máquinas virtuales de Windows](tutorial-load-balancer.md).

Cree un equilibrador de carga que tenga una dirección IP pública y distribuye el tráfico web en el puerto 80:

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a>Creación de un conjunto de escalado
Ahora, cree un conjunto de escalado de máquinas virtuales con [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm). Hello en el ejemplo siguiente se crea un conjunto con nombre de escalas *myScaleSet*:

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

Toma toocreate unos minutos y configurará todos los recursos de conjunto de escala de Hola y máquinas virtuales.


## <a name="test-your-app"></a>Prueba de la aplicación
toosee el sitio Web IIS en acción, obtener la dirección IP pública de Hola de un equilibrador de carga con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIP* creado como parte del conjunto de escalas de hello:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Escriba la dirección IP pública hello en el Explorador de web tooa. se muestra la aplicación Hello, incluido Hola nombre de host de hello VM ese Hola la carga del tráfico de equilibrador distribuida para:

![Ejecución del sitio de IIS](./media/tutorial-create-vmss/running-iis-site.png)

escala de hello toosee establecida en acción, se puede forzar actualización su carga de hello web explorador toosee equilibrador de distribuir el tráfico entre todas las máquinas virtuales de hello ejecutando la aplicación.


## <a name="management-tasks"></a>Tareas de administración
A lo largo del ciclo de vida de Hola de conjunto de escalas de hello, puede que necesite toorun una o más tareas de administración. Además, puede que desee toocreate scripts que automaticen diversas tareas de ciclo de vida. PowerShell de Azure proporciona una manera rápida toodo esas tareas. A continuación, presentamos algunas tareas comunes.

### <a name="view-vms-in-a-scale-set"></a>Visualización de máquinas virtuales en un conjunto de escalado
tooview una lista de máquinas virtuales en ejecución en la escala de conjunto, utilice [AzureRmVmssVM Get](/powershell/module/azurerm.compute/get-azurermvmssvm) como se indica a continuación:

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a>Aumento o disminución de instancias de máquina virtual
número de hello toosee de instancias actualmente en una escala estableciste, use [Get AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) y realizar consultas sobre *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

Puede, a continuación, manualmente aumentar o reducir el número de Hola de máquinas virtuales en la escala de hello establecida con [AzureRmVmss actualización](/powershell/module/azurerm.compute/update-azurermvmss). Hello en el ejemplo siguiente se establece Hola número de máquinas virtuales de la escala establecida demasiado*5*:

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

Si toma Hola de tooupdate de unos minutos un número especificado de instancias en el conjunto de escala.


### <a name="configure-autoscale-rules"></a>Configuración de reglas de escalado automático
En lugar de establece manualmente escalar el número de Hola de instancias en la escala, definir reglas de escalado automático. Estas reglas supervisan Hola instancias en la escala de establecerán y responden según corresponda, basándose en las métricas y los umbrales que defina. Hola siguiente ejemplo admita la ampliación horizontal número Hola de instancias en uno cuando la carga promedio de CPU de hello es mayor que 60% durante un período de 5 minutos. Si carga de CPU promedio de hello, a continuación, cae por debajo de 30% durante un período de 5 minutos, instancias de Hola se escalan en una instancia:

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha creado un conjunto de escalado de máquinas virtuales. Ha aprendido a:

> [!div class="checklist"]
> * Usar la extensión de Script personalizado de hello toodefine un tooscale de sitio IIS
> * Crear un equilibrador de carga para el conjunto de escalado
> * Crear un conjunto de escalado de máquinas virtuales
> * Aumentar o disminuir el número de Hola de instancias de un conjunto de escala
> * Crear reglas de escalado automático

Avanzar toohello siguiente tutorial toolearn más información sobre los conceptos de máquinas virtuales de equilibrio de carga.

> [!div class="nextstepaction"]
> [Load balance virtual machines](tutorial-load-balancer.md) (Equilibrio de carga de máquinas virtuales)
