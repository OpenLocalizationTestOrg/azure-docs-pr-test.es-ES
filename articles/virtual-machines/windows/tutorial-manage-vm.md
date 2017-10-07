---
title: "Hola a aaaCreate y administrar máquinas virtuales de Windows con el módulo de PowerShell de Azure | Documentos de Microsoft"
description: "Tutorial: crear y administrar máquinas virtuales de Windows con Hola módulo Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>Crear y administrar máquinas virtuales de Windows con Hola módulo Azure PowerShell

Las máquinas virtuales de Azure proporcionan un entorno informático completamente configurable y flexible. En este tutorial se tratan elementos básicos de la implementación de máquinas virtuales de Azure, como la selección de su tamaño, la selección de una imagen de máquina virtual y la implementación de una máquina virtual. Aprenderá a:

> [!div class="checklist"]
> * Crear y conectar tooa VM
> * Seleccionar y usar imágenes de máquinas virtuales
> * Ver y usar tamaños de una máquina virtual específicos
> * Cambiar el tamaño de una máquina virtual
> * Ver y entender el estado de las máquinas virtuales

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-resource-group"></a>Creación de un grupo de recursos

Crear un grupo de recursos con hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando. 

Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. Se debe crear un grupo de recursos antes de una máquina virtual. En este ejemplo, un grupo de recursos denominado *myResourceGroupVM* se crea en hello *EastUS* región. 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

grupo de recursos de Hola se especifica al crear o modificar una máquina virtual, que puede ser vista a lo largo de este tutorial.

## <a name="create-virtual-machine"></a>Create virtual machine

Una máquina virtual debe estar conectado tooa red virtual. Comunicarse con la máquina virtual de hello mediante una dirección IP pública a través de una tarjeta de interfaz de red.

### <a name="create-virtual-network"></a>Creación de una red virtual

Cree una subred con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

Cree una red virtual con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>Creación de una dirección IP pública

Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>Creación de una tarjeta de interfaz de red

Cree una tarjeta de interfaz de red con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>Creación de un grupo de seguridad de red

Un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) de Azure controla el tráfico entrante y saliente para una o varias máquinas virtuales. Las reglas del grupo de seguridad de red permiten o deniegan el tráfico de red en un puerto específico o en un intervalo de puertos. Estas reglas también pueden incluir un prefijo de dirección de origen para que solo el tráfico que se origine en un origen predefinido pueda comunicarse con una máquina virtual. tooaccess servidor Web IIS de Hola que va a instalar, debe agregar una regla de NSG de entrada.

usar toocreate una regla de entrada NSG, [AzureRmNetworkSecurityRuleConfig agregar](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig). Hello en el ejemplo siguiente se crea una regla NSG denominada *myNSGRule* que abre el puerto *3389* para la máquina virtual de hello:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

Crear hello NSG mediante *myNSGRule* con [AzureRmNetworkSecurityGroup New](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

Agregar subred de hello NSG toohello en red virtual de hello con [AzureRmVirtualNetworkSubnetConfig conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

Red virtual de Hola de actualización con [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>Create virtual machine

Al crear una máquina virtual, están disponibles varias opciones, como la imagen de sistema operativo, tamaño de disco y credenciales administrativas. En este ejemplo, se crea una máquina virtual con el nombre de *myVM* versión más reciente en ejecución Hola del centro de datos de Windows Server 2016.

Establecer nombre de usuario de Hola y la contraseña necesarios para la cuenta de administrador de hello en hello la máquina virtual con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Crear la configuración inicial de hello para la máquina virtual de hello con [AzureRmVMConfig New](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

Agregar configuración de máquina virtual de hello sistema operativo información toohello con [AzureRmVMOperatingSystem conjunto](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Agregar configuración de máquina virtual de hello imagen información toohello con [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

Agregar configuración de máquina virtual de toohello configuración disco de sistema operativo Hola con [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

Tarjeta de interfaz de red de Hola de complemento que creó anteriormente toohello configuración de máquina virtual con [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Crear la máquina virtual Hola con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>Conectar tooVM

Una vez finalizada la implementación de hello, cree una conexión a escritorio remota con la máquina virtual de Hola.

Ejecute hello después comandos tooreturn Hola dirección IP pública de la máquina virtual de Hola. Tome nota de esta dirección IP para que pueda conectarse tooit con la conectividad de web tootest de explorador en un paso posterior.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

Siguiente Hola de uso del comando toocreate una sesión de escritorio remoto con la máquina virtual de Hola. Reemplace la dirección IP de hello con hello *publicIPAddress* de la máquina virtual. Cuando se le solicite, escriba credenciales de hello usadas al crear la máquina virtual de Hola.

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>Descripción de las imágenes de máquina virtual

Hello Azure marketplace incluye muchas imágenes de máquina virtual que pueden ser usado toocreate una nueva máquina virtual. En los pasos anteriores de hello, se crea una máquina virtual mediante la imagen de Windows Server 2016-Datacenter Hola. En este paso, módulo de PowerShell de hello es marketplace de hello toosearch usado otras imágenes de Windows, puede también como base para nuevas máquinas virtuales. Este proceso consiste en Buscar publicador de hello, oferta y nombre de la imagen de hello (Sku). 

Hola de uso [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) comando tooreturn una lista de publicadores de imagen.  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

Hola de uso [AzureRmVMImageOffer Get](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn una lista de ofertas de imagen. Con este comando, Hola devuelve la lista se filtra en el publicador especificado Hola. 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

Hola [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) comando, a continuación, filtrará en tooreturn de nombre de publicador y oferta de hello una lista de nombres de imagen.

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

Esta información puede ser toodeploy usa una máquina virtual con una imagen específica. Este ejemplo establece el nombre de la imagen de hello en objeto de máquina virtual de Hola. En este tutorial para los pasos de implementación completa, consulte toohello en los ejemplos anteriores.

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>Comprensión de los tamaños de máquina virtual

Un tamaño de máquina virtual determina la cantidad de Hola de recursos de proceso, como CPU y GPU, memoria que se realizan la máquina virtual de toohello disponible. Máquinas virtuales deben toobe creado con un tamaño adecuado para hello esperar que la carga de trabajo. Si aumenta la carga de trabajo, se puede cambiar el tamaño de una máquina virtual existente.

### <a name="vm-sizes"></a>Tamaños de máquina virtual

Hello en la tabla siguiente clasifica tamaños en casos de uso.  

| Tipo                     | Tamaños           |    Descripción       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Uso general         |DSv2, Dv2, DS, D, Av2, A0-7| Uso equilibrado de CPU y memoria. Ideal para desarrollo / pruebas y las soluciones de aplicaciones y datos de toomedium pequeños.  |
| Proceso optimizado      | Fs, F             | Uso elevado de la CPU respecto a la memoria. Adecuado para aplicaciones, dispositivos de red y procesos por lotes de tráfico medio.        |
| Memoria optimizada       | GS, G, DSv2, DS, Dv2 y D   | Uso elevado de memoria respecto al núcleo. Muy bien para bases de datos relacionales, las cachés de toolarge intermedio y análisis en memoria.                 |
| Almacenamiento optimizado       | LS                | Alto rendimiento de disco y E/S. Perfecto para bases de datos SQL y NoSQL y macrodatos.                                                         |
| GPU           | NV, NC            | Máquinas virtuales especializadas específicas para actividades intensas de representación de gráficos y edición de vídeo.       |
| Alto rendimiento | H, A8-11          | Nuestras máquinas virtuales con CPU más eficaces e interfaces de red de alto rendimiento (RDMA) opcionales. 


### <a name="find-available-vm-sizes"></a>Búsqueda de los tamaños de máquina virtual disponibles

toosee una lista de la máquina virtual los tamaños disponibles en una región determinada, use hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) comando.

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>Cambiar el tamaño de una máquina virtual

Una vez implementada una máquina virtual, puede tooincrease cuyo tamaño ha cambiado o reducir la asignación de recursos.

Antes de cambiar el tamaño de una máquina virtual, compruebe si hello tamaño deseado está disponible en el clúster VM actual Hola. Hola [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) comando devuelve una lista de tamaños. 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

Si Hola deseado tamaño está disponible, hello VM puede cambiarse desde un estado encendido, sin embargo, se reinicia durante la operación de Hola.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

Si Hola tamaño deseado no está en el clúster actual hello, Hola VM necesidades puede producirse toobe cancela la asignación antes de hello cambiar el tamaño de operación. Tenga en cuenta que cuando Hola máquina virtual está encendida nuevo, se quitan todos los datos en disco temporal de Hola y la dirección IP pública Hola cambia a menos que se está usando una dirección IP estática. 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>Estados de una máquina virtual

Una máquina virtual de Azure puede tener uno de muchos estados de energía. Este estado representa estado actual de Hola de hello VM desde la perspectiva de Hola de hipervisor de Hola. 

### <a name="power-states"></a>Estados de energía

| Estado de energía | Descripción
|----|----|
| Iniciando | Indica que se está iniciando la máquina virtual de Hola. |
| En ejecución | Indica que la máquina virtual Hola se está ejecutando. |
| Deteniéndose | Indica que la máquina virtual Hola se está deteniendo. | 
| Stopped | Indica que la máquina virtual Hola se ha detenido. Tenga en cuenta que máquinas virtuales en estado de hello detenido sigue acumulando cargos de proceso.  |
| Desasignando | Indica que la máquina virtual Hola se está desasignando. |
| Desasignado | Indica que la máquina virtual Hola se quita completamente del hipervisor de hello pero sigue estando disponible en el plano de control de Hola. Máquinas virtuales en estado desasignado hello no acumulando cargos de proceso. |
| - | Indica que el estado de energía de Hola de máquina virtual de hello es desconocido. |

### <a name="find-power-state"></a>Búsqueda del estado de una máquina virtual

estado de hello tooretrieve de una máquina virtual concreta, use hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) comando. Ser seguro toospecify un nombre válido para una máquina virtual y el grupo de recursos. 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

Salida:

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>Tareas de administración

Durante el ciclo de vida de Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual. Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de secuencias de comandos. Uso de PowerShell de Azure, muchas tareas comunes de administración pueden realizarse desde la línea de comandos de Hola o en scripts.

### <a name="stop-virtual-machine"></a>Detener una máquina virtual

Detenga y desasigne una máquina virtual con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

Si desea tookeep Hola virtual machine en un estado de aprovisionamiento, use el parámetro de - StayProvisioned de Hola.

### <a name="start-virtual-machine"></a>Iniciar una máquina virtual

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>Eliminación de un grupo de recursos

Al eliminar un grupo de recursos se eliminan también todos los recursos contenidos en el mismo.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido conceptos básicos sobre la creación y administración de máquinas virtuales. Por ejemplo:

> [!div class="checklist"]
> * Crear y conectar tooa VM
> * Seleccionar y usar imágenes de máquinas virtuales
> * Ver y usar tamaños de una máquina virtual específicos
> * Cambiar el tamaño de una máquina virtual
> * Ver y entender el estado de las máquinas virtuales

Avanzar toohello toolearn de tutorial siguiente acerca de los discos de máquina virtual.  

> [!div class="nextstepaction"]
> [Creación y administración de discos de máquinas virtuales](./tutorial-manage-data-disk.md)
