---
title: "aaaMultiple las direcciones IP para máquinas virtuales de Azure - PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooassign varias direcciones IP de máquina virtual de tooa mediante PowerShell | Administrador de recursos."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>Asignar varias direcciones IP máquinas toovirtual con PowerShell

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Este artículo explica cómo toocreate una máquina virtual (VM) a través de la implementación de Azure Resource Manager Hola modelar con PowerShell. No se puede asignar tooresources que se creó mediante el modelo de implementación clásica de Hola a varias direcciones IP. más información acerca de los modelos de implementación de Azure, lea hello toolearn [comprender los modelos de implementación](../resource-manager-deployment-model.md) artículo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Creación de una máquina virtual con varias direcciones IP

pasos de Hola que siguen explican cómo toocreate aborda un máquina virtual con varias IP de ejemplo, tal y como se describe en el escenario de Hola. Cambie los valores de variable según sea necesario para la implementación.

1. Abra un símbolo del sistema de PowerShell y Hola completa restante pasos de esta sección dentro de una sola sesión de PowerShell. Si aún no tiene PowerShell instalado y configurado, Hola completa los pasos de hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.
2. Cuenta de inicio de sesión tooyour con hello `login-azurermaccount` comando.
3. Reemplace *myResourceGroup* y *westus* por un nombre y una ubicación de su elección. Cree un grupo de recursos. Un grupo de recursos es un contenedor lógico en el que se implementan y se administran los recursos de Azure.

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. Crear una red virtual (VNet) y la subred en hello misma ubicación que el grupo de recursos de hello:

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. Cree un grupo de seguridad de red (NSG) y una regla. Hola NSG protege Hola VM mediante reglas entrantes y salientes. En este caso, se crea una regla de entrada para el puerto 3389, que permite las conexiones entrantes al Escritorio remoto.

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. Definir configuración IP primaria de Hola para hello NIC. Cambio 10.0.0.4 tooa dirección válida en la subred de Hola que ha creado, si no utiliza valor Hola definido previamente. Antes de asignar una dirección IP estática, se recomienda que primero confirme que no está en uso. Escriba el comando hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`. Si está disponible la dirección de hello, Hola output devuelve *True*. Si no está disponible, Hola salida devuelve *False* y una lista de direcciones que están disponibles. 

    Hola, siga los comandos, **reemplace < reemplazar-con-your-único-name > por hello toouse de nombre DNS único.** nombre de Hello debe ser único en todas las direcciones IP públicas dentro de una región de Azure. Se trata de un parámetro opcional. Se puede quitar si sólo desea tooconnect toohello máquina virtual con la dirección IP pública Hola.

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    Cuando asigna varias IP configuraciones tooa NIC, se debe asignar una configuración como hello *-principal*.

    > [!NOTE]
    > Las direcciones IP públicas tienen un precio simbólico. toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción. toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.

7. Definir configuraciones de IP secundarias Hola para hello NIC. Puede agregar o quitar las configuraciones que sean necesarias. Cada configuración de dirección IP debe tener asignada una dirección IP privada. Cada configuración puede tener asignada opcionalmente una dirección IP pública.

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. Crear hello NIC y asociar Hola tres IP configuraciones tooit:

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >Aunque todas las configuraciones se asignan tooone NIC en este artículo, puede asignar varios tooevery NIC conectada toohello VM configuraciones de IP. toolearn cómo leer toocreate una máquina virtual con varias NIC hello [crear una máquina virtual con varias NIC](virtual-network-deploy-multinic-arm-ps.md) artículo.

9. Crear Hola VM escribiendo Hola siguientes comandos:

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. Sistema operativo de la VM de toohello las direcciones IP privada de agregar Hola siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo. No agregue el sistema de operativo para toohello el público direcciones IP Hola.

## <a name="add"></a>Agregar tooa de direcciones IP virtual

Puede agregar pública y privada tooa de direcciones IP NIC siguiendo los pasos de Hola que siguen. Hello en los ejemplos de hello las secciones siguientes se suponen que ya tiene una máquina virtual con configuraciones de IP de hello tres descritas en hello [escenario](#Scenario) en este artículo, pero no es necesario que lo haga.

1. Abra un símbolo del sistema de PowerShell y Hola completa restante pasos de esta sección dentro de una sola sesión de PowerShell. Si aún no tiene PowerShell instalado y configurado, Hola completa los pasos de hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.
2. Cambiar los valores"hello" de hello después $Variables toohello nombre de hello NIC que desee tooadd IP dirección tooand Hola recursos grupo y ubicación Hola en que NIC existe:

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    Si no conoce el nombre de Hola de hello NIC que desee toochange, escriba Hola siga los comandos, a continuación, cambiar los valores de hello de variables anteriores hello:

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. Cree una variable y establézcalo toohello existente NIC escribiendo el siguiente comando de hello:

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. Hola después de comandos, cambiar *MyVNet* y *MySubnet* toohello nombres de Hola Hola de red virtual y subred NIC está conectada a. Escriba Hola comandos tooretrieve Hola red virtual y subred objetos Hola A que NIC está conectada:

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    Si no sabe Hola red virtual o la subred nombre Hola A que NIC está conectada, escriba Hola siguiente comando:
    ```powershell
    $MyNIC.IpConfigurations
    ```
    En la salida de hello, buscar texto toohello similar después de la salida de ejemplo:
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    En esta salida, *MyVnet* es hello red virtual y *MySubnet* es Hola subred hello NIC está conectada a.

5. Complete los pasos de hello en una de las siguientes secciones, según sus requisitos de hello:

    **Incorporación de una dirección IP privada**

    tooadd una tooa de dirección IP privada NIC, debe crear una configuración de IP. Hello siguiente comando crea una configuración con una dirección IP estática de 10.0.0.7. Al especificar una dirección IP estática, debe ser una dirección no utilizada para la subred de Hola. Se recomienda que primero pruebe Hola dirección tooensure está disponible mediante la especificación de hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` comando. Si está disponible la dirección IP de hello, Hola output devuelve *True*. Si no está disponible, Hola salida devuelve *False*y una lista de direcciones que están disponibles.

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    Cree tantas configuraciones como sea necesario mediante nombres de configuración únicos y direcciones IP privadas (para las configuraciones con direcciones IP estáticas).

    Agregar: sistema operativo de la VM de hello privado IP dirección toohello siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.

    **Incorporación de una dirección IP pública**

    Se agrega una dirección IP pública asociando un tooeither de recurso de dirección IP pública de una nueva configuración de IP o una configuración de IP existente. Complete los pasos de hello en una de las secciones de Hola que siguen, como sea necesario.

    > [!NOTE]
    > Las direcciones IP públicas tienen un precio simbólico. toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción. toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.
    >

    - **Asociar Hola pública recursos tooa nueva IP configuración de dirección IP**
    
        Siempre que agregue una dirección IP pública en una nueva configuración de IP, también debe agregar una dirección IP privada, porque todas las configuraciones de IP deben tener una dirección IP privada. Puede agregar un recurso de dirección IP pública existente o crear uno nuevo. toocreate uno nuevo, escriba el siguiente comando de hello:
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        toocreate una nueva configuración de IP con una dirección IP privada estática y Hola asociados *myPublicIp3* IP pública recurso Dirección, escriba el siguiente comando de hello:

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **Asociar Hola pública recursos tooan existente IP configuración de dirección IP**

        Configuración de IP de tooan asociado que ya no tiene asociado sólo puede ser un recurso de dirección IP público. Puede determinar si una configuración de IP tiene una dirección IP pública asociada mediante la especificación de hello siguiente comando:

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        Se ve resultados similares toohello siguiente:

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        Desde hello **PublicIpAddress** columna para *IpConfig-3* está en blanco, ningún recurso de dirección IP pública está asociada actualmente tooit. Puede agregar una existente pública IP dirección recursos tooIpConfig-3, o escriba Hola después toocreate comando uno:

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        Escriba el siguiente comando con el nombre por la configuración de IP existente de recursos toohello de dirección IP pública de tooassociate Hola de hello *IpConfig-3*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. Establecer Hola NIC con una nueva configuración de IP Hola escribiendo Hola siguiente comando:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. Ver direcciones IP privadas de Hola y Hola pública IP dirección recursos asignado toohello NIC escribiendo Hola el siguiente comando:

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. Agregar: sistema operativo de la VM de hello privado IP dirección toohello siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo. No agregue el sistema de operativo para toohello el público dirección IP Hola.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
