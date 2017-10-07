---
title: "entorno de prueba de nube híbrida de aaaSimulated | Documentos de Microsoft"
description: "Cree un entorno de nube híbrida simulado para profesionales de TI o pruebas de desarrollo con dos redes virtuales de Azure y una conexión de red virtual a red virtual."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>Configuración de un entorno de nube híbrida simulado para pruebas
Este artículo le guiará en el proceso de creación de un entorno de nube híbrida simulado con Microsoft Azure mediante dos redes virtuales de Azure. Esta es la configuración resultante de Hola.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Esto simula un entorno de producción en la nube híbrida y consta de los siguientes elementos:

* Una red simulada y simplificado local hospedada en una red virtual (red virtual de hello práctica de prueba).
* Una red virtual simulada entre locales hospedada en Azure (TestVNET).
* Una conexión de red virtual a red virtual entre redes virtuales Hola dos.
* Un controlador de dominio secundario en la red virtual de hello TestVNET.

Esto proporciona una base y un punto de partida común desde el que puede:

* Desarrollar y probar las aplicaciones en un entorno de nube híbrida simulado.
* Crear configuraciones de pruebas de equipos, algunas dentro de la red virtual de hello práctica de prueba y otras en red virtual hello TestVNET, toosimulate híbrida basada en la nube TI las cargas de trabajo.

Hay cuatro toosetting fases principales en este entorno de prueba de nube híbrida:

1. Configurar red virtual de hello práctica de prueba.
2. Crear red virtual entre entornos de Hola.
3. Crear la conexión de VPN de red virtual a red virtual de Hola.
4. Configuración de DC2. 

Esta configuración requiere una suscripción de Azure. Si tiene una suscripción de MSDN o de Visual Studio, consulte [Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

> [!NOTE]
> Las máquinas virtuales y las puertas de enlace de redes virtuales en Azure incurren en un coste económico constante cuando se están ejecutando. Este costo se factura en su suscripción de pago o MSDN. Una puerta de enlace de VPN de Azure se implementa como un conjunto de dos máquinas virtuales de Azure. los costos de hello toominimize, crear el entorno de prueba de Hola y realizar las pruebas y demostración necesarios lo más rápido posible.
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a>Fase 1: Configurar red virtual de hello práctica de prueba
Utilice instrucciones de Hola Hola [entorno de prueba de configuración de Base](https://technet.microsoft.com/library/mt771177.aspx) tema tooconfigure Hola DC1, APP1 y CLIENT1 equipos Hola red virtual de Azure denominado práctica de prueba. 

Después, inicie un símbolo del sistema de Azure PowerShell.

> [!NOTE]
> Hola siguientes conjuntos de comandos usa Azure PowerShell 1.0 y versiones posterior.
> 
> 

Inicie sesión en la cuenta de tooyour.

    Login-AzureRMAccount

Obtiene el nombre de la suscripción con el siguiente comando de Hola.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Establezca su suscripción a Azure. Use Hola misma suscripción utilizada toobuild de la configuración base en la fase 1. Reemplace todo el contenido de las comillas de hello, incluidos Hola < y > caracteres, con el nombre correcto de Hola.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

A continuación, agregar una puerta de enlace subred toohello práctica de prueba red virtual de la configuración base, que será usado toohost Hola puerta de enlace de Azure.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

A continuación, solicitar pública IP dirección tooassign toohello puerta de enlace de red virtual de hello práctica de prueba.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

A continuación, cree la puerta de enlace.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Tenga en cuenta que las nuevas puertas de enlace pueden tardar 20 minutos o más toocreate.

En hello portal de Azure en el equipo local, conéctese tooDC1 con las credenciales de CORP\User1 Hola. dominio CORP hello tooconfigure para que los usuarios y equipos de usan su controlador de dominio local para la autenticación, ejecute estos comandos desde un símbolo de Windows PowerShell de nivel de administrador en DC1.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

Se trata de la configuración actual.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a>Fase 2: Crear red virtual de hello TestVNET
En primer lugar, crear red virtual de hello TestVNET y protéjala con un grupo de seguridad de red.

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

A continuación, la solicitud una toobe de dirección IP pública asignada toohello puerta de enlace de red virtual de hello TestVNET y crear la puerta de enlace.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Se trata de la configuración actual.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a>Fase 3: Crear la conexión de red virtual a red virtual de Hola
En primer lugar, solicite una clave previamente compartida aleatoria criptográficamente segura de 32 caracteres al administrador de red o de seguridad. Como alternativa, use la información de hello en [crear una cadena aleatoria de una clave previamente compartida IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain una clave previamente compartida.

A continuación, use estas conexiones de VPN de red virtual a red virtual de comandos toocreate hello, lo que pueden tardar algún tiempo toocomplete.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

Después de unos minutos, se debe establecer la conexión de Hola.

Se trata de la configuración actual.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>Fase 4: configuración de DC2
Primero, cree una máquina virtual para DC2. Ejecute estos comandos en línea de comandos de PowerShell de Azure de hello en el equipo local.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

A continuación, conectar toohello DC2 máquina virtual de hello portal de Azure.

A continuación, configure un tráfico de tooallow de regla de Firewall de Windows para probar la conectividad básica. Desde un símbolo del sistema de Windows PowerShell con nivel de administrador en DC2, ejecute estos comandos.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

comando ping de Hello debe producir cuatro respuestas correctas de dirección IP 10.0.0.4. Esto es una prueba de tráfico a través de hello conexión de red virtual a red virtual.

A continuación, agregue Hola disco de datos adicionales en DC2 como un volumen nuevo con una letra de unidad de hello F:.

1. En el panel izquierdo del administrador del servidor de hello, haga clic en **File and Storage Services**y, a continuación, haga clic en **discos**.
2. En panel de contenido de hello, Hola **discos** grupo, haga clic en **disco 2** (con hello **partición** establecido demasiado**desconocido**).
3. Haga clic en **Tareas** y luego haga clic en **Nuevo volumen**.
4. En hello antes de comenzar la página del Asistente para nuevo volumen hello, haga clic en **siguiente**.
5. En el servidor seleccione Hola de Hola y página de disco, haga clic en **disco 2**y, a continuación, haga clic en **siguiente**. Cuando se le solicite, haga clic en **Aceptar**.
6. En especificar el tamaño de Hola de página de volumen de Hola Hola, haga clic en **siguiente**.
7. En hello asignar tooa unidad carpeta o letra de página, haga clic en **siguiente**.
8. En la página Configuración del sistema seleccione archivo hello, haga clic en **siguiente**.
9. En la página Confirmar selecciones de hello, haga clic en **crear**.
10. Cuando haya terminado, haga clic en **Cerrar**.

A continuación, configure DC2 como un controlador de dominio de réplica para el dominio de corp.contoso.com Hola. Ejecutar estos comandos desde la línea de comandos de Windows PowerShell de hello en DC2.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

Tenga en cuenta que toosupply solicitada ambos Hola CORP\User1 contraseña y una contraseña de modo de restauración de servicios de directorio (DSRM) y toorestart DC2.

Ahora que hello TestVNET red virtual no tiene su propio servidor DNS (DC2), debe configurar toouse de red virtual de hello TestVNET este servidor DNS.

1. En panel izquierdo de Hola de hello portal de Azure, haga clic en el icono de redes virtuales de hello y, a continuación, haga clic en **TestVNET**.
2. En hello **configuración** , haga clic en **servidores DNS**.
3. En **servidor DNS principal**, tipo **192.168.0.4** tooreplace 10.0.0.4.
4. Haga clic en **Guardar**.

Se trata de la configuración actual. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Su entorno de nube híbrida simulado ya está listo para las pruebas.

## <a name="next-step"></a>Paso siguiente
* Configure una [aplicación de línea de negocio web](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en este entorno.

