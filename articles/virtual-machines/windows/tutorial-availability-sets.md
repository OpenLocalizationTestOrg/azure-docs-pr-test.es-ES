---
title: "aaaAvailability establece el tutorial para máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello disponibilidad conjuntos para máquinas virtuales de Windows en Azure."
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>¿Cómo se establece toouse disponibilidad

En este tutorial, obtendrá información sobre cómo la disponibilidad de hello tooincrease y la confiabilidad de las soluciones de la máquina Virtual en Azure con una capacidad de llamar conjuntos de disponibilidad. Conjuntos de disponibilidad Asegúrese de que las máquinas virtuales se implementan en Azure se distribuyen entre varios clústeres de hardware aislados de Hola. Esto garantiza que, si se produce un error de hardware o software dentro de Azure, solo un subjuego de las máquinas virtuales se verán afectado y que la solución general permanecerá disponible y en funcionamiento desde la perspectiva de Hola de los clientes de usarlo. 

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear un conjunto de disponibilidad
> * Crear una máquina virtual en un conjunto de disponibilidad
> * Comprobar los tamaños de máquina virtual disponibles

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Información general sobre conjuntos de disponibilidad

Un conjunto de disponibilidad es una capacidad de agrupación lógica que puede usar en Azure tooensure que los recursos de máquina virtual de Hola que se coloca dentro de él están aislados entre sí cuando se implementan en un centro de datos de Azure. Azure garantiza que las máquinas virtuales se coloca dentro de un conjunto de disponibilidad que se ejecute en varios servidores físicos de hello, proceso racks, unidades de almacenamiento y conmutadores de red. Esto garantiza que en caso de hello de un error hardware o software de Azure, solo un subconjunto de las máquinas virtuales se verán afectado, y la aplicación global se mantienen actualizados y continuar a toobe tooyour disponibles clientes. Usar conjuntos de disponibilidad es una capacidad fundamental tooleverage cuando desee que las soluciones de nube confiable toobuild.

Veamos una solución basada en máquina virtual típica en la podría haber 4 servidores web front-end y usar 2 máquinas virtuales de back-end que hospedan una base de datos. Con Azure, desearía toodefine dos conjuntos de disponibilidad antes de implementar las máquinas virtuales: conjunto de disponibilidad de uno para la capa de "web" de Hola y un conjunto de disponibilidad de nivel de "database" Hola. Cuando se crea una nueva máquina virtual, a continuación, puede especificar el conjunto como una máquina virtual de parámetro toohello az crear comandos y Azure automáticamente asegurará de que hello las máquinas virtuales que cree en hello disponible de la disponibilidad de hello conjunto están aislados entre varios recursos de hardware físico. Esto significa que si el hardware físico de Hola que uno de su servidor Web o máquinas virtuales del servidor de base de datos se ejecuta en tiene un problema, sabe que Hola otras instancias de servidor Web y máquinas virtuales de la base de datos seguirá ejecutándose correctamente porque están en un hardware diferente.

Debe utilizar siempre los conjuntos de disponibilidad cuando se desean toodeploy las soluciones basadas en VM confiables dentro de Azure.

## <a name="create-an-availability-set"></a>Crear un conjunto de disponibilidad

Puede crear un conjunto de disponibilidad con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). En este ejemplo, establecemos ambos en número de dominios de actualización y error en hello *2* para el conjunto con nombre de la disponibilidad de hello *myAvailabilitySet* en hello *myResourceGroupAvailability*grupo de recursos.

Cree un grupo de recursos.

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>Creación de VM dentro de un conjunto de disponibilidad

Las máquinas virtuales deben toobe creado dentro de hello disponibilidad conjunto toomake seguro de que se distribuyen correctamente a través de hardware de Hola. No se puede agregar un grupo de disponibilidad de tooan VM establecer después de crearlo. 

hardware de Hello en una ubicación se divide en toomultiple actualizar dominios y dominios de error. Un **Actualizar dominio** es un grupo de máquinas virtuales y el hardware físico subyacente que puede reiniciarse en hello mismo tiempo. Máquinas virtuales en el mismo Hola **dominio de error** comparten un almacenamiento común, así como un conmutador de origen y de red común de energía. 

Cuando se crea una máquina virtual mediante la configuración mediante [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) especificar Hola conjunto de disponibilidad mediante hello `-AvailabilitySetId` Id. del parámetro toospecify Hola Hola del conjunto de disponibilidad.

Crear 2 máquinas virtuales con [AzureRmVM New](/powershell/module/azurerm.compute/new-azurermvm) en conjunto de disponibilidad de Hola.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

Toma toocreate unos minutos y configurar las máquinas virtuales. Cuando termine, tendrá 2 máquinas virtuales que se distribuyen a través de hello subyacente de hardware. 

## <a name="check-for-available-vm-sizes"></a>Comprobación de los tamaños de VM disponibles 

Puede agregar más máquinas virtuales toohello conjunto de disponibilidad posteriormente, pero necesita tooknow qué tamaños de máquinas virtuales están disponibles en el hardware de Hola. Use [AzureRMVMSize Get](/powershell/module/azurerm.compute/get-azurermvmsize) toolist todos los tamaños disponibles de hello en hardware de Hola de clúster para el conjunto de disponibilidad de Hola.

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Crear un conjunto de disponibilidad
> * Crear una máquina virtual en un conjunto de disponibilidad
> * Comprobar los tamaños de máquina virtual disponibles

Avanzar toohello toolearn de tutorial siguiente sobre conjuntos de escalas de máquina virtual.

> [!div class="nextstepaction"]
> [Creación de un conjunto de escalado de máquinas virtuales](tutorial-create-vmss.md)


