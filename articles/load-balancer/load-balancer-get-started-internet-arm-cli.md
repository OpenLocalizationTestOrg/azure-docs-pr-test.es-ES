---
title: "aaaCreate una conexión a Internet cargar equilibrador - CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga con conexión a Internet en el Administrador de recursos en Hola CLI de Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>Creación de un equilibrador de carga de internet mediante Hola CLI de Azure

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Plantilla](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación del Administrador de recursos de Hola. También puede [Obtenga información acerca de cómo el equilibrador mediante la implementación clásica de la carga de toocreate una conexión a Internet](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Implementar soluciones de hello mediante Hola CLI de Azure

Hola pasos muestra cómo toocreate una conexión a Internet cargar equilibrador con Azure Resource Manager CLI. Con Azure Resource Manager se crea y se configuran individualmente cada recurso, a continuación, reunir toocreate un recurso.

Debe crear y configurar Hola después objetos toodeploy un equilibrador de carga:

* Configuración de direcciones IP de front-end: contiene direcciones IP públicas para el tráfico de red entrante.
* Grupo de direcciones de back-end - contiene interfaces de red (NIC) de tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga.
* Reglas de equilibrio de carga - contiene reglas de asignación de un puerto público en tooport de equilibrador de carga de hello en el grupo de direcciones de back-end de Hola.
* Reglas NAT de entrada: contiene las reglas de asignación de un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola.
* Sondea: contiene toocheck disponibilidad de sondeos que se usan de mantenimiento de instancias de máquinas virtuales en el grupo de direcciones de back-end de Hola.

Para más información, consulte [Compatibilidad de Azure Resource Manager con Load Balancer](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Configurar la CLI toouse el Administrador de recursos

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello **configuración azure modo** modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.

    ```azurecli
        azure config mode arm
    ```

    Resultado esperado:

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Crear una red virtual y una dirección IP pública para el grupo de direcciones IP de front-end de Hola

1. Crear una red virtual (VNet) con el nombre *NRPVnet* en ubicación de UU hello mediante un grupo de recursos denominado *NRPRG*.

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    Cree una subred llamada *NRPVnetSubnet* con un bloque CIDR de 10.0.0.0/24 en *NRPVnet*.

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. Crear una dirección IP pública denominada *NRPPublicIP* toobe utilizado por un grupo IP front-end con el nombre DNS *loadbalancernrp.eastus.cloudapp.azure.com*. comando hello siguiente utiliza el tipo de asignación estático de Hola y tiempo de inactividad de 4 minutos.

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > equilibrador de carga de Hello utilizará la etiqueta de Hola de dominio de la dirección IP pública de hello como su FQDN. Este un cambio de implementación clásica, que utiliza el servicio de nube de hello como Hola nombre de dominio completo (FQDN) de equilibrador de carga.
   > En este ejemplo, hello FQDN es *loadbalancernrp.eastus.cloudapp.azure.com*.

## <a name="create-a-load-balancer"></a>Crear un equilibrador de carga

Hello siguiente comando crea un equilibrador de carga con el nombre *NRPlb* en hello *NRPRG* grupo de recursos de hello *UU* ubicación de Azure.

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>Creación de un grupo de direcciones IP de front-end y un grupo de direcciones de back-end
En este ejemplo se muestra cómo toocreate Hola grupo IP front-end que recibe el tráfico de red entrante de hello en hello equilibrador de carga y Hola grupo de direcciones IP de back-end que grupo front-end de hello envía tráfico de red con equilibrio de carga de Hola.

1. Cree un grupo IP front-end asociar IP pública Hola creado en el paso anterior de Hola y equilibrador de carga de Hola.

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. Configurar un grupo de direcciones de back-end utiliza tooreceive el tráfico entrante de grupo de direcciones IP de front-end de Hola.

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>Crear reglas de equilibrador de carga, reglas NAT y sondeo

Este ejemplo crea Hola siguientes elementos.

* regla de NAT tootranslate todo el tráfico entrante en el puerto 21 tooport 22<sup>1</sup>
* regla de NAT tootranslate todo el tráfico entrante en el puerto 23 tooport 22
* un toobalance de regla de equilibrador de carga todo el tráfico entrante en el puerto 80 tooport 80 en hello direcciones de grupo de back-end de Hola.
* un estado de mantenimiento de sondeo regla toocheck hello en una página denominada *HealthProbe.aspx*.

<sup>1</sup> reglas NAT son la instancia de máquina virtual específica de tooa asociado detrás de equilibrador de carga de Hola. tráfico de red de Hola que llegan en el puerto 21 se envía la máquina virtual específica de tooa en el puerto asociado con esta regla NAT de 22. Debe especificar un protocolo (UDP o TCP) para una regla NAT. Ambos protocolos no se pueden asignar toohello mismo puerto.

1. Crear hello las reglas NAT.

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. Cree una regla de equilibrador de carga.

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. Cree un sondeo de estado.

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. Compruebe la configuración.

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    Resultado esperado:

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>Cree tarjetas NIC

Necesita toocreate NIC (o modificar los existentes) y asociarlos a tooNAT reglas, reglas de equilibrador de carga y sondeos.

1. Cree una NIC denominada *nic1 de carga equilibrada puede*y asociar con hello *rdp1* NAT hello y regla *NRPbackendpool* grupo de direcciones de back-end.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    Resultado esperado:

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. Cree una NIC denominada *nic2 de carga equilibrada puede*y asociar con hello *rdp2* NAT hello y regla *NRPbackendpool* grupo de direcciones de back-end.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. Crear una máquina virtual (VM) con el nombre *web1*y asociar con hello NIC denominado *nic1 de carga equilibrada puede*. Llama a una cuenta de almacenamiento *web1nrp* se creó antes de ejecutar el siguiente comando de Hola.

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > Hola a las máquinas virtuales en un toobe de necesidad de equilibrador de carga en el mismo conjunto de disponibilidad. Use `azure availset create` toocreate un conjunto de disponibilidad.

    salida de Hello debe ser similar siguiente toohello:

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > mensaje informativo de Hello **se trata de una NIC sin publicIP configurado** se espera desde que hello NIC creó Hola equilibrador de carga conecta tooInternet utilizando la dirección IP pública de equilibrador de carga de Hola.

    Desde hello *nic1 de carga equilibrada puede* NIC está asociado con hello *rdp1* regla de NAT, puede conectar demasiado*web1* mediante RDP a través del puerto 3441 en equilibrador de carga de Hola.

4. Crear una máquina virtual (VM) con el nombre *web2*y asociar con hello NIC denominado *nic2 de carga equilibrada puede*. Llama a una cuenta de almacenamiento *web1nrp* se creó antes de ejecutar el siguiente comando de Hola.

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>Actualización de un equilibrador de carga existente
Puede agregar reglas que hacen referencia a un equilibrador de carga existente. En el siguiente ejemplo de Hola, una nueva regla de equilibrador de carga se agrega el equilibrador de carga existente tooan **NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>Eliminar un equilibrador de carga
Usar hello después comando tooremove un equilibrador de carga:

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>Pasos siguientes
[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-cli.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
