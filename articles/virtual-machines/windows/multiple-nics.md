---
title: "aaaCreate y administrar máquinas virtuales de Windows en Azure que usan varios NIC | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y administrar una máquina virtual de Windows que tenga varias NIC a adjunto tooit mediante plantillas de Azure PowerShell o administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Crear y administrar una máquina virtual con Windows que tiene varias NIC
Máquinas virtuales (VM) en Azure puede tener varios toothem de tarjetas (NIC) adjuntadas de interfaz de red virtual. Un escenario común es toohave subredes diferentes para la conectividad de front-end y back-end o una red dedicada tooa supervisión o una solución de copia de seguridad. Este artículo detalla cómo toocreate una máquina virtual con varias NIC había conectado tooit. También aprenderá cómo NIC tooadd o quitar de una máquina virtual existente. Diferentes [tamaños de máquina virtual](sizes.md) admiten un número distinto de NIC, así que ajuste el tamaño de su máquina virtual teniendo esto en cuenta.

Para obtener información detallada, incluyendo cómo toocreate varios NIC dentro de sus propios scripts de PowerShell, consulte [implementar máquinas virtuales de varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que dispone de hello [versión más reciente de Azure PowerShell instalado y configurado](/powershell/azure/overview).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Creación de una máquina virtual con varias NIC
En primer lugar, cree un grupo de recursos. Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *EastUs* ubicación:

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Creación de redes virtuales y subredes
Un escenario común es para una red virtual toohave dos o más subredes. Puede ser una subred para el tráfico de front-end, Hola otro para el tráfico de back-end. tooconnect tooboth subredes, a continuación, usa varios NIC en la máquina virtual.

1. Defina dos subredes de red virtual con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Hello en el ejemplo siguiente se define subredes Hola de *mySubnetFrontEnd* y *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Cree la red virtual y las subredes con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Creación de varias NIC
Cree dos NIC con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Adjuntar una subred de front-end de toohello NIC y una subred de back-end de toohello NIC. Hello en el ejemplo siguiente se crea con el nombre de NIC *myNic1* y *myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

Normalmente se crea también un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) o [equilibrador de carga](../../load-balancer/load-balancer-overview.md) toohelp administrar y distribuir el tráfico entre las máquinas virtuales. Hola [más VM de varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artículo le guía en la creación de un grupo de seguridad de red y la asignación de NIC.

### <a name="create-hello-virtual-machine"></a>Crear la máquina virtual de Hola
Iniciar toobuild la configuración de máquina virtual. El tamaño de cada máquina virtual tiene un límite para el número total de Hola de NIC que se puede agregar tooa VM. Para más información, vea [Tamaños de las máquinas virtuales con Windows](sizes.md).

1. Establecer el toohello de las credenciales de la máquina virtual `$cred` variable como se indica a continuación:

    ```powershell
    $cred = Get-Credential
    ```

2. Defina la máquina virtual con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig). Hello en el ejemplo siguiente se define una máquina virtual denominada *myVM* y utiliza un tamaño de memoria virtual que es compatible con más de dos NIC (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. Crear el resto de saludo de la configuración de máquina virtual con [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) y [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage). Hola de ejemplo siguiente crea una máquina virtual de Windows Server 2016:

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. Adjuntar Hola dos NIC que creó anteriormente con [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Por último, cree la máquina virtual con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>Agregar un tooan NIC existente de la máquina virtual
Agregar tooadd una tooan NIC virtual existente de la máquina virtual, se cancela la asignación de hello VM, Hola NIC virtual e inicie Hola máquina virtual.

1. Cancela la asignación de Hola VM con [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm). Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM* en *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Obtener la configuración existente de Hola de hello VM con [AzureRmVm Get](/powershell/module/azurerm.compute/get-azurermvm). Hello en el ejemplo siguiente se obtiene información de máquina virtual denominada hello *myVM* en *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Hello en el ejemplo siguiente se crea una NIC virtual con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) denominado *myNic3* que está conectada demasiado*mySubnetBackEnd*. Hola NIC virtual es, a continuación, adjunta toohello máquina virtual denominada *myVM* en *myResourceGroup* con [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>NIC virtuales principales
    Uno de hello NIC en una VM de varias NIC debe toobe principal. Si uno de Hola NIC virtuales existentes en hello VM ya está establecida como principal, puede omitir este paso. Hello en el ejemplo siguiente se supone que dos NIC virtuales ahora están presentes en una máquina virtual y desea tooadd Hola primera NIC (`[0]`) como Hola principal:
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Iniciar Hola VM con [AzureRmVm inicio](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Eliminación de una NIC de una máquina virtual existente
tooremove una NIC virtual de una máquina virtual existente, se cancela la asignación de hello VM, quite Hola NIC virtual y, a continuación, inicio Hola máquina virtual.

1. Cancela la asignación de Hola VM con [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm). Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM* en *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Obtener la configuración existente de Hola de hello VM con [AzureRmVm Get](/powershell/module/azurerm.compute/get-azurermvm). Hello en el ejemplo siguiente se obtiene información de máquina virtual denominada hello *myVM* en *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Obtener información acerca de hello NIC quitar con [AzureRmNetworkInterface Get](/powershell/module/azurerm.network/get-azurermnetworkinterface). Hello en el ejemplo siguiente se obtiene información sobre *myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Quitar Hola NIC con [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) y actualice Hola VM con [AzureRmVm actualización](/powershell/module/azurerm.compute/update-azurermvm). Quita de Hello en el ejemplo siguiente se *myNic3* obtenida por `$nicId` Hola anterior paso:

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Iniciar Hola VM con [AzureRmVm inicio](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Crear varias NIC con plantillas
Plantillas de administrador de recursos de Azure proporcionan una manera toocreate varias instancias de un recurso durante la implementación, como la creación de varias NIC. Plantillas de administrador de recursos utilizan declarativa toodefine de archivos JSON en su entorno. Para más información, vea [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Puede usar *copia* número de hello toospecify de toocreate de instancias:

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Para más información, vea [Creación de varias instancias mediante *copy*](../../resource-group-create-multiple.md). 

También puede usar `copyIndex()` tooappend un nombre de recurso tooa número. Después, puede crear *myNic1*, *MyNic2* y así sucesivamente. Hello código siguiente muestra un ejemplo de anexar el valor de índice de hello:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Puede leer un ejemplo completo de [cómo crear varias NIC mediante plantillas de Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Pasos siguientes
Revisión [tamaños de máquina virtual de Windows](sizes.md) al que está tratando de toocreate una máquina virtual que tiene varios NIC. Pagar el número máximo de toohello de atención de NIC que admite cada tamaño de máquina virtual. 


