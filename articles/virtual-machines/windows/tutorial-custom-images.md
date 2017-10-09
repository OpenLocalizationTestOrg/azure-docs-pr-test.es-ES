---
title: "imágenes de máquina virtual personalizadas aaaCreate con hello Azure PowerShell | Documentos de Microsoft"
description: "Tutorial: crear una imagen de máquina virtual personalizada con hello Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>Creación de una imagen personalizada de una máquina virtual de Azure mediante PowerShell

Las imágenes personalizadas son como las imágenes de Marketplace, pero las puede crear usted mismo. Imágenes personalizadas pueden ser configuraciones toobootstrap usado como carga previa de aplicaciones, configuraciones de aplicaciones y otras configuraciones del sistema operativo. En este tutorial, creará su propia imagen personalizada de una máquina virtual de Azure. Aprenderá a:

> [!div class="checklist"]
> * Ejecutar Sysprep y generalizar máquinas virtuales
> * Crear una imagen personalizada
> * Crear una imagen personalizada a partir de una máquina virtual
> * Una lista de todas las imágenes de hello en su suscripción
> * Eliminar una imagen

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="before-you-begin"></a>Antes de empezar

Hola los pasos siguientes detalla cómo tootake una máquina virtual existente y a su vez en un personalizado reutilizable de la imagen que pueden usar toocreate nuevas instancias de máquina virtual.

ejemplo de Hola a toocomplete en este tutorial, debe tener una máquina virtual existente. Si es necesario, este [script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) puede crear una. Cuando reemplace trabajar a través de tutorial de hello, grupo de recursos de Hola y VM nombres cuando sea necesario.

## <a name="prepare-vm"></a>Preparación de la VM

toocreate una imagen de una máquina virtual, deberá tooprepare Hola VM por hello generalizar VM desasignar y, a continuación, marcar origen Hola VM tal y como se ha generalizado en Azure.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalizar Hola VM de Windows con Sysprep

Sysprep quita toda la información de cuenta personal, entre otras cosas y prepara Hola máquina toobe utilizado como una imagen. Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).


1. Conectar la máquina virtual de toohello.
2. Abra la ventana de símbolo del sistema de hello como administrador. Cambie el directorio de hello demasiado*%windir%\system32\sysprep*y, a continuación, ejecute *sysprep.exe*.
3. Hola **herramienta de preparación del sistema** cuadro de diálogo, seleccione *sistema Out-of-Box experiencia inmediata (OOBE)*y asegúrese de que ese hello *generalizar* casilla está activada.
4. En **Opciones de apagado**, seleccione *Apagar* y, a continuación, haga clic en **Aceptar**.
5. Cuando Sysprep finalice, se apaga máquina virtual de Hola. **No se reinician Hola VM**.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Cancelar la asignación y marcar Hola VM como generalizado

toocreate una imagen, Hola VM debe toobe cancela la asignación y está marcado como generalizada en Azure.

Hola desasignada VM con [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm).

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Establecer el estado de saludo de la máquina virtual de hello demasiado`-Generalized` con [AzureRmVm conjunto](/powershell/module/azurerm.compute/set-azurermvm). 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Crear imagen de Hola

Ahora puede crear una imagen de máquina virtual de hello mediante [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) y [AzureRmImage nuevo](/powershell/module/azurerm.compute/new-azurermimage). Hello en el ejemplo siguiente se crea una imagen denominada *myImage* desde una máquina virtual denominada *myVM*.

Obtenga la máquina virtual de Hola. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Crear configuración de la imagen de Hola.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Crear imagen de Hola.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Crear máquinas virtuales de la imagen de Hola

Ahora que tiene una imagen, puede crear una o varias nuevas máquinas virtuales de la imagen de Hola. Crear una máquina virtual a partir de una imagen personalizada es muy similar toocreating una máquina virtual mediante una imagen de Marketplace. Cuando se usa una imagen de Marketplace, tener tooinformation acerca de la imagen de hello, proveedor de imágenes, oferta, SKU y versión. Con una imagen personalizada, debe tooprovide Hola identificador de recurso de imagen personalizado de Hola. 

En la siguiente secuencia de comandos de hello, creamos una variable *$image* toostore información sobre el uso de la imagen personalizada de hello [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) y, a continuación, usamos [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)y especifique el identificador de hello mediante hello *$image* variable que acabamos de crear. 

script de Hola crea una máquina virtual denominada *myVMfromImage* desde la imagen personalizada en un nuevo grupo de recursos denominado *myResourceGroupFromImage* en hello *oeste de Estados Unidos* ubicación.


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>Administración de imágenes 

Estos son algunos ejemplos de tareas de imágenes comunes de administración y cómo toocomplete mediante PowerShell.

Enumere todas las imágenes por nombre.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

Elimine una imagen. Este ejemplo elimina Hola imagen denominada *myOldImage* de hello *myResourceGroup*.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha creado una imagen de máquina virtual personalizada. Ha aprendido a:

> [!div class="checklist"]
> * Ejecutar Sysprep y generalizar máquinas virtuales
> * Crear una imagen personalizada
> * Crear una imagen personalizada a partir de una máquina virtual
> * Una lista de todas las imágenes de hello en su suscripción
> * Eliminar una imagen

Avanzar toohello toolearn de tutorial siguiente sobre máquinas virtuales de la alta disponibilidad.

> [!div class="nextstepaction"]
> [Creación de máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md)



