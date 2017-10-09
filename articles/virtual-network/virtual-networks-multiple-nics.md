---
title: "aaaCreate una máquina virtual (clásica) con varias NIC mediante PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y configurar las máquinas virtuales con varias NIC con PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>Creación de una máquina virtual (clásica) con varias NIC
Puede crear máquinas virtuales (VM) en Azure y conectar múltiples tooeach (NIC) de interfaces de red de las máquinas virtuales. Tener varias NIC es un requisito para muchos dispositivos virtuales de red, por ejemplo, las soluciones de optimización de WAN y de entrega de aplicaciones. Varias NIC también aportan aislamiento del tráfico entre ellas.

![Varias NIC para máquina virtual](./media/virtual-networks-multiple-nics/IC757773.png)

Hola ilustración, se muestra una máquina virtual con tres NICs, cada uno conectado tooa otra subred.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que las implementaciones más recientes usen Resource Manager.

* VIP a través de Internet (implementaciones clásicas) solo se admite en la NIC de Hola "predeterminada". Hay solo una dirección IP de toohello de VIP de NIC de hello predeterminada.
* En estos momentos, no se admiten direcciones IP públicas (implementaciones clásicas) de nivel de instancia (LPIP) para máquinas virtuales con varias NIC.
* Hola orden de NIC de Hola desde dentro de hello VM será aleatorio y también podría cambiar en todas las actualizaciones de infraestructura de Azure. Sin embargo, direcciones IP de Hola y Hola MAC de ethernet correspondiente permanecerán direcciones Hola igual. Por ejemplo, suponga **Eth1** tiene la dirección IP 10.1.0.100 y la dirección MAC 00-0D-3A-B0-39-0D; después de una actualización de la infraestructura de Azure y un reinicio, se podría cambiar demasiado**Eth2**, pero Hola IP y MAC emparejamiento will permanecen Hola igual. Cuando un reinicio es iniciado por el cliente, Hola orden de NIC seguirá siendo Hola igual.
* Hello dirección para cada NIC en cada máquina virtual debe estar ubicado en una subred, varias NIC en una sola máquina virtual cada uno se puede asignar direcciones que se encuentran en Hola misma subred.
* Hola tamaño de máquina virtual determina el número de Hola de NIC que se pueden crear para una máquina virtual. Hola de referencia [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tamaños de VM artículos toodetermine cuántas NIC es compatible con el tamaño de cada máquina virtual. 

## <a name="network-security-groups-nsgs"></a>Grupos de seguridad de red (NSG)
En una implementación del Administrador de recursos, cualquier NIC de una máquina virtual puede asociarse a un grupo de seguridad de red (NSG), incluyendo cualquier NIC de una máquina virtual que tenga varias NIC habilitadas. Si una NIC se asigna una dirección de una subred que está asociado con un NSG subred hello, a continuación, hello reglas en NSG la subred de hello también aplican toothat equipo NIC. En subredes tooassociating de suma con NSG, también puede asociar una NIC con un NSG.

Si una subred está asociada con un NSG y una NIC en esa subred individualmente asociada a un NSG, se aplican las reglas NSG de hello asociado en **flujo orden** según la dirección de toohello del tráfico de Hola que se pasa dentro o fuera de Hola NIC:

* **El tráfico entrante** cuyo destino es hello NIC en cuestión fluyen primero a través de la subred hello, desencadenar reglas NSG de la subred de hello, antes de pasar a Hola NIC, a continuación, desencadenar reglas de NSG Hola NIC.
* **El tráfico saliente** cuyo origen es hello NIC en cuestión fluyen primero en salir de hello NIC, desencadenar reglas NSG del NIC hello, antes de pasar a través de la subred de hello, a continuación, desencadenar reglas de NSG Hola la subred.

Obtenga más información sobre [grupos de seguridad de red](virtual-networks-nsg.md) y cómo se aplican en función de las asociaciones toosubnets, las máquinas virtuales y NIC...

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a>¿Cómo tooConfigure una VM de NIC múltiples en una implementación clásica
instrucciones de Hola a continuación le ayudará a crear una VM de NIC con 3 NIC múltiples: una NIC predeterminada y dos NIC adicionales. pasos de configuración de Hello creará una máquina virtual que se configurarán según el fragmento de archivo de configuración de servicio de toohello siguiente:

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


Necesita Hola siguiendo los requisitos previos antes de intentar toorun comandos de PowerShell de hello en el ejemplo de Hola.

* Una suscripción de Azure.
* Una red virtual configurada. Para obtener más información sobre redes virtuales, consulte [Información general sobre redes virtuales](virtual-networks-overview.md) .
* versión más reciente de Hola de Azure PowerShell descargado e instalado. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

toocreate una máquina virtual con varias NIC, Hola completa siguiendo los pasos, escriba cada comando en una única sesión de PowerShell:

1. Seleccione una imagen de máquina virutal en la galería de imágenes de máquinas virtuales de Azure. Tenga en cuenta que las imágenes cambian con frecuencia y están disponibles por región. Hello imagen especificada en el siguiente ejemplo de Hola puede cambiar o puede no estar en su región, por lo que toospecify imagen de Hola que se necesita.

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. Creación de una configuración de máquina virtual

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. Crear el inicio de sesión de administrador de hello predeterminado.

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. Agregar configuración de máquina virtual de toohello NIC adicional.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. Especifique una subred de Hola y dirección IP para la NIC de hello predeterminada.

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. Crear Hola VM en la red virtual.

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > Hola red virtual que especifique aquí debe existir (como se menciona en los requisitos previos de hello). ejemplo de Hola siguiente especifica una red virtual denominada **MultiNIC-VNet**.
    >

## <a name="limitations"></a>Limitaciones
Hola siguientes limitaciones es aplicable al uso de varias NIC:

* Las máquinas virtuales con varias NIC deben crearse en redes virtuales de Azure. Las máquinas virtuales que no son de redes virtuales no se pueden configurar con varias NIC.
* Todas las máquinas virtuales en la disponibilidad de un conjunto necesidad toouse varios NIC o una NIC único. En un conjunto de disponibilidad no puede haber una combinación de máquinas virtuales de varias NIC y de NIC única. Para las máquinas virtuales de un servicio en la nube se aplican las mismas reglas. Varias NIC máquinas virtuales, no están necesarios que toohave Hola el mismo número de NIC, siempre y cuando cada uno de ellos tiene al menos dos.
* Una máquina virtual con una NIC única no se puede configurar con varias NIC (y viceversa) una vez implementada si no se elimina y se vuelve a crear.

## <a name="secondary-nics-access-tooother-subnets"></a>NIC secundarias tener acceso a subredes de tooother
De forma predeterminada la NIC secundarias no se configurarán con una puerta de enlace predeterminada, debido toowhich flujo de tráfico de hello en hello NIC secundarias será toobe limitado en hello misma subred. Si desean que los usuarios de hello tooenable secundaria NIC tootalk fuera de su propia subred, necesitarán tooadd una entrada de hello enrutamiento tabla tooconfigure Hola puerta de enlace como se describe a continuación.

> [!NOTE]
> Las máquinas virtuales creadas antes de julio de 2015 pueden tener una puerta de enlace predeterminada configurada para todas las NIC. Hola puerta de enlace predeterminada NIC secundarias no se quitará hasta que estas máquinas virtuales se reinician. En los sistemas operativos que utilizan Hola modelo enrutamiento de host no seguro, como Linux, puede interrumpir la conectividad a Internet si el tráfico de entrada y salida hello usa NIC diferentes.
> 

### <a name="configure-windows-vms"></a>Configurar las máquinas virtuales de Windows
Suponga que tiene una máquina virtual de Windows con dos NIC, tal y como se muestra a continuación:

* Dirección IP de la NIC principal: 192.168.1.4
* Dirección IP de la NIC secundaria: 192.168.2.5

tabla de rutas de IPv4 de Hola para esta máquina virtual sería similar al siguiente:

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

Tenga en cuenta que esa ruta de hello predeterminada (0.0.0.0) es sólo toohello disponibles de NIC principal No será capaz de tooaccess recursos externos a subred Hola para hello secundaria NIC, tal como se muestra a continuación:

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

tooadd enrutar el valor predeterminado de Hola NIC secundaria, siga los pasos de Hola a continuación:

1. Desde un símbolo del sistema, ejecute el comando de Hola por debajo del número de índice de hello tooidentify de hello NIC secundaria:
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. Observe la segunda entrada de hello en la tabla de hello, con un índice de 27 (en este ejemplo).
3. Hola desde línea de comandos, ejecute hello **Agregar ruta** comando tal y como se muestra a continuación. En este ejemplo, está especificando 192.168.2.1 como Hola puerta de enlace predeterminada Hola NIC secundaria:
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. conectividad de tootest atrás toohello símbolo e intenta tooping una subred distinta de Hola NIC secundaria como se muestra int eh ejemplo siguiente:
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. También puede comprobar su hello toocheck de tabla de ruta recién agregado ruta, tal y como se muestra a continuación:
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a>Configurar máquinas virtuales de Linux
Para máquinas virtuales de Linux, puesto que comportamiento predeterminado de hello utiliza host débil enrutamiento, es recomendable que Hola NIC secundarias son flujos de tootraffic restringida solo dentro de hello misma subred. Sin embargo, si determinados escenarios exigen conectividad exterior de la subred hello, los usuarios deben habilitar tooensure de enrutamiento basada en directivas que Hola entrada y usos de tráfico de salida Hola mismo NIC.

## <a name="next-steps"></a>Pasos siguientes
* Implemente [máquinas virtuales MultiNIC en un escenario de aplicación de 2 niveles en una implementación del Administrador de recursos](virtual-network-deploy-multinic-arm-template.md).
* Implemente [máquinas virtuales MultiNIC en un escenario de aplicación de 2 niveles en una implementación clásica](virtual-network-deploy-multinic-classic-ps.md).

