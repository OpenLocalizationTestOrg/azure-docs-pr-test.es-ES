---
title: "equilibrador de carga de aaaCreate una conexión a Internet con IPv6 - CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un Internet orientados al equilibrador de carga con IPv6 en el Administrador de recursos de Azure en Hola CLI de Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, Azure Load Balancer, pila doble, dirección ip pública, ipv6 nativo, móvil, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>Crear una red orientada hacia el equilibrador de carga con IPv6 en Azure Resource Manager mediante Hola CLI de Azure

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [CLI de Azure](load-balancer-ipv6-internet-cli.md)
> * [Plantilla](load-balancer-ipv6-internet-template.md)

Azure Load Balancer es un equilibrador de carga de nivel 4 (TCP y UDP) equilibrador de carga de Hello proporciona alta disponibilidad mediante la distribución de tráfico entrante entre instancias de servicio de estado de servicios en la nube o máquinas virtuales en un conjunto de equilibrador de carga. Azure Load Balancer también pueden presentar prestar servicios en varios puertos, varias direcciones IP o ambos.

## <a name="example-deployment-scenario"></a>Escenario de implementación de ejemplo

Hello siguiente diagrama ilustra Hola solución equilibrio de carga que se implementarán mediante la plantilla de ejemplo de Hola se describe en este artículo.

![Escenario del equilibrador de carga](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

En este escenario, creará hello Azure recursos siguientes:

* dos máquinas virtuales (VM)
* una interfaz de red virtual para cada máquina virtual con las direcciones IPv4 e IPv6 asignadas
* un equilibrador de carga orientado a Internet con una dirección IP pública IPv4 e IPv6
* un conjunto de disponibilidad toothat contiene máquinas virtuales de hello dos
* dos equilibrio reglas toomap Hola VIP toohello privados extremos públicos de carga

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Implementar soluciones de hello mediante Hola CLI de Azure

Hola pasos muestra cómo toocreate una conexión a Internet cargar equilibrador con Azure Resource Manager CLI. Con el Administrador de recursos de Azure, cada recurso se crea y configura de forma individual y, a continuación, reunir toocreate un recurso.

toodeploy un equilibrador de carga, se crea y configura Hola siguientes objetos:

* Configuración de direcciones IP de front-end: contiene direcciones IP públicas para el tráfico de red entrante.
* Grupo de direcciones de back-end - contiene interfaces de red (NIC) de tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga.
* Reglas de equilibrio de carga - contiene reglas de asignación de un puerto público en tooport de equilibrador de carga de hello en el grupo de direcciones de back-end de Hola.
* Reglas NAT de entrada: contiene las reglas de asignación de un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola.
* Sondea: contiene toocheck disponibilidad de sondeos que se usan de mantenimiento de instancias de máquinas virtuales en el grupo de direcciones de back-end de Hola.

Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>Configurar la toouse de entorno de CLI Azure Resource Manager

En este ejemplo, se está ejecutando herramientas CLI de hello en una ventana de comandos de PowerShell. No estamos utilizando cmdlets de PowerShell de Azure de hello, sin embargo, los usamos capacidades tooimprove legibilidad y reutilización de secuencias de comandos de PowerShell.

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello **configuración azure modo** modo de comando tooswitch tooResource Manager.

    ```azurecli
    azure config mode arm
    ```

    Resultado esperado:

        info:    New mode is arm

3. Inicie sesión en tooAzure y obtener una lista de suscripciones.

    ```azurecli
    azure login
    ```

    Escriba sus credenciales de Azure cuando se le solicite.

    ```azurecli
    azure account list
    ```

    Seleccionar suscripción Hola que desea toouse. Tome nota del identificador de la suscripción de hello para el paso siguiente de saludo.

4. Configurar variables de PowerShell para su uso con los comandos de CLI de Hola.

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>Creación de un grupo de recursos, un equilibrador de carga, una red virtual y subredes

1. Crear un grupo de recursos

    ```azurecli
    azure group create $rgName $location
    ```

2. Crear un equilibrador de carga

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. Cree una red virtual (VNet)

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    Cree dos subredes en esta red virtual

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>Crear direcciones IP públicas para el grupo de servidores front-end de Hola

1. Establecer las variables de PowerShell de Hola

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. Crear un público Hola front-end IP grupo de direcciones IP.

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > equilibrador de carga de Hello usa la etiqueta de Hola de dominio de la dirección IP pública de hello como su FQDN. Este un cambio de implementación clásico, que utiliza el nombre de servicio de nube de hello como Hola FQDN del equilibrador de carga.
    > En este ejemplo, hello FQDN es *contoso09152016.southcentralus.cloudapp.azure.com*.

## <a name="create-front-end-and-back-end-pools"></a>Creación de grupos de servidores front-end y back-end

Este ejemplo crea el grupo IP front-end Hola que recibe el tráfico de red entrante de hello en el equilibrador de carga de Hola y grupo de direcciones IP de back-end de Hola donde grupo front-end de hello envía tráfico de red con equilibrio de carga de Hola.

1. Establecer las variables de PowerShell de Hola

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Cree un grupo IP front-end asociar IP pública Hola creado en el paso anterior de Hola y equilibrador de carga de Hola.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>Crear reglas de carga Equilibrada, las reglas NAT y sondeo Hola

Este ejemplo crea Hola siguientes elementos:

* un toocheck de regla de sondeo para el puerto de la conectividad tooTCP 80
* un dispositivo NAT regla tootranslate todo el tráfico entrante en el puerto 3389 tooport 3389 para RDP<sup>1</sup>
* un dispositivo NAT regla tootranslate todo el tráfico entrante en el puerto 3391 tooport 3389 para RDP<sup>1</sup>
* un toobalance de regla de equilibrador de carga todo el tráfico entrante en el puerto 80 tooport 80 en hello direcciones de grupo de back-end de Hola.

<sup>1</sup> reglas NAT son la instancia de máquina virtual específica de tooa asociado detrás de equilibrador de carga de Hola. máquina virtual específica de toohello y el puerto asociado con la regla NAT de hello, se envía tráfico de red de Hola que llegan en el puerto 3389. Debe especificar un protocolo (UDP o TCP) para una regla NAT. Ambos protocolos no se pueden asignar toohello mismo puerto.

1. Establecer las variables de PowerShell de Hola

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Crear el sondeo de Hola

    Hello en el ejemplo siguiente se crea un sondeo TCP comprueba para el puerto TCP de tooback final conectividad 80 cada 15 segundos. Marcará los recursos de back-end de hello disponible después de dos errores consecutivos.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Crear reglas NAT de entrada que permiten las conexiones RDP toohello recursos de back-end

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. Crear reglas que envían el tráfico de puertos de back-end de toodifferent dependiendo de qué solicitud de Hola de front-end que recibió de un equilibrador de carga

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. Compruebe la configuración

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    Resultado esperado:

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>Cree tarjetas NIC

Crear NIC y asociarlos tooNAT reglas, reglas de equilibrador de carga y sondeos.

1. Establecer las variables de PowerShell de Hola

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. Cree una NIC para cada back-end y agregue una configuración de IPv6

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>Crear recursos de máquina virtual de back-end de Hola y asociar cada NIC

toocreate las máquinas virtuales, debe tener una cuenta de almacenamiento. Equilibrio de carga, las máquinas virtuales de hello necesitan a toobe miembros de un conjunto de disponibilidad. Para obtener más información sobre cómo crear máquinas virtuales, consulte [Creación de una máquina virtual de Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Establecer las variables de PowerShell de Hola

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > Este ejemplo utiliza Hola username y password para máquinas virtuales de hello en texto no cifrado. Adecuada se debe tener cuidado al utilizando credenciales de hello claro. Para obtener un método más seguro de controlar las credenciales en PowerShell, vea hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

2. Crear conjunto de cuenta y la disponibilidad de almacenamiento de Hola

    Puede usar una cuenta de almacenamiento existente al crear hello las máquinas virtuales. Hola siguiente comando crea una nueva cuenta de almacenamiento.

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    A continuación, crear conjunto de disponibilidad de Hola.

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. Crear máquinas virtuales de hello con NIC Hola asociado

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>Pasos siguientes

[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-cli.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
