---
title: aaaLoad equilibrio en varias configuraciones de IP mediante la CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooassign varias direcciones IP de máquina virtual de tooa mediante la CLI de Azure | Administrador de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a>Equilibrio de carga en varias configuraciones de IP

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [CLI](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

Este artículo describe cómo aborda toouse equilibrador de carga de Azure con varias IP en una interfaz de red secundaria (NIC). En este escenario, tenemos dos máquinas virtuales que ejecutan Windows. Cada una de ellas cuenta con una NIC principal y otra secundaria. Cada uno de hello secundaria NIC tienen dos configuraciones de IP. Cada máquina virtual hospeda dos sitios web: contoso.com y fabrikam.com. Cada sitio Web está enlazado tooone Hola de configuraciones de IP en la NIC de hello secundaria. Utilizamos el equilibrador de carga Azure tooexpose dos front-end direcciones IP, una para cada sitio Web, toodistribute tráfico toohello respectivo configuración IP para el sitio Web de Hola. Este escenario utiliza Hola el mismo número de puerto a través de front-ends, así como las direcciones IP de back-end del grupo.

![Imagen del escenario de equilibrio de carga](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Saldo de tooload de pasos en varias configuraciones de IP

Siga los pasos de hello debajo de escenario de hello tooachieve descrito en este artículo:

1. [Instalar y configurar hello Azure CLI](../cli-install-nodejs.md) Hola CLI de Azure siguiendo los pasos de hello en el artículo vinculado de Hola y registro en su cuenta de Azure.
2. [Cree un grupo de recursos](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) llamado *contosofabrikam*, tal y como se describe en el artículo vinculado.

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. [Crear un conjunto de disponibilidad](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor Hola dos máquinas virtuales. En este escenario, utilice Hola siguiente comando:

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. [Cree una red virtual](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) llamada *myVNet* y una subred denominada *mySubnet*:

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. [Crear el equilibrador de carga de hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) llama *mylb*:

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. Cree dos direcciones IP públicas dinámicas para configuraciones de IP de front-end de Hola de un equilibrador de carga:

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. Crear configuraciones de IP, de hello dos front-end *contosofe* y *fabrikamfe* respectivamente:

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. Cree los grupos de direcciones del back-end: *contosopool* y *fabrikampool*; un [sondeo](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json):  - *HTTP*, y las reglas de equilibrado de carga: *HTTPc* y *HTTPf*:

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. Siguiente ejecución Hola comando a continuación y, a continuación, compruebe el resultado de hello demasiado[comprobar el equilibrador de carga](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) se creó correctamente:

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. [Cree una dirección IP pública](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address): *myPublicIp*, y una [cuenta de almacenamiento](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json): *mystorageaccont1*, para la primera máquina virtual (VM1), tal y como se muestra a continuación:

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. [Crear interfaces de red de hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) para VM1 y agregue una segunda configuración IP, *VM1 ipconfig2*, y [crear hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) tal y como se muestra a continuación:

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. Repita los pasos 10 y 11 con la segunda máquina virtual:

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. Por último, debe configurar el dirección IP de DNS recursos registros toopoint toohello respectivos front-end de hello equilibrador de carga. Puede hospedar los dominios en Azure DNS. Para más información sobre el uso de Azure DNS con Load Balancer, consulte [Uso de Azure DNS con otros servicios de Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Pasos siguientes
- Obtener más información acerca de cómo Equilibrio de carga de toocombine services en Azure en [con servicios de equilibrio de carga en Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Obtenga información acerca de cómo puede usar varios tipos de registros de Azure toomanage y solucionar problemas de equilibrador de carga en [análisis de registros para el equilibrador de carga de Azure](../load-balancer/load-balancer-monitor-log.md).
