---
title: aaaCreate un interno cargar equilibrador - CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga interno mediante el uso de Hola CLI de Azure en el Administrador de recursos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>Crear un equilibrador de carga interno mediante Hola CLI de Azure

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Plantilla](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](load-balancer-get-started-ilb-classic-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>Implementar soluciones de hello mediante Hola CLI de Azure

Hola siguientes pasos muestra cómo toocreate una conexión a Internet el equilibrador de carga mediante el Administrador de recursos de Azure con CLI. Con el Administrador de recursos de Azure, cada recurso se crea y configura de forma individual y, a continuación, reunir toocreate un recurso.

Necesita toocreate y configurar Hola después objetos toodeploy un equilibrador de carga:

* **Configuración de direcciones IP de front-end**: contiene direcciones IP públicas para el tráfico de red entrante
* **Grupo de direcciones de back-end**: contiene interfaces de red (NIC) que permitan el tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga
* **Las reglas de equilibrio de carga**: contiene reglas que se asignan a un puerto público en tooport de equilibrador de carga de hello en el grupo de direcciones de back-end de Hola
* **Reglas NAT de entrada**: contiene reglas que se asignan a un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola
* **Sondeos**: contiene los sondeos de mantenimiento que son utilizados toocheck Hola disponibilidad de instancias de máquinas virtuales en el grupo de direcciones de back-end de Hola

Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Configurar la CLI toouse el Administrador de recursos

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md). Siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello **modo de configuración de azure** comando modo de administrador de tooswitch tooResource, como se indica a continuación:

    ```azurecli
    azure config mode arm
    ```

    Resultado esperado:

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>Creación de un equilibrador de carga interno paso a paso

1. Inicie sesión en tooAzure.

    ```azurecli
    azure login
    ```

    Cuando se le solicite, escriba sus credenciales de Azure.

2. Cambiar el modo de administrador de recursos de hello comando herramientas tooAzure.

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Todos los recursos de Azure Resource Manager están asociados a un grupo de recursos. Si todavía no lo ha hecho, cree un grupo de recursos.

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>Crear un conjunto de equilibrador de carga interno

1. Creación de un conjunto de equilibrador de carga interno

    Hola siguiendo el escenario, se crea un grupo de recursos denominado nrprg en la región Este de EE..

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > Todos los recursos para una equilibradores de carga interno, como redes virtuales y subredes de red virtual, deben estar en Hola el mismo grupo de recursos y de Hola misma región.

2. Crear una dirección IP front-end de equilibrador de carga interno de Hola.

    dirección IP de Hola que utilice debe ser en intervalo de subred de hello de la red virtual.

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. Crear grupo de direcciones de back-end de Hola.

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    Después de definir una dirección IP de front-end y un grupo de direcciones de back-end, puede crear reglas de equilibradores de carga, reglas NAT de entrada y sondeos de estado personalizados.

4. Crear una regla de equilibrador de carga para el equilibrador de carga interno de Hola.

    Al seguir los pasos anteriores de hello, comando hello crea una regla de equilibrador de carga para tooport escucha 1433 en el grupo de servidores front-end de Hola y envío con equilibrio de carga de red tráfico toohello back-end grupo de direcciones, también utiliza el puerto 1433.

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. Crear reglas NAT de entrada.

    Reglas NAT de entrada son puntos de conexión toocreate usado en un equilibrador de carga que vaya tooa instancia de máquina virtual específica. los pasos anteriores de Hello crean dos reglas NAT para escritorio remoto.

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. Crear sondeos de mantenimiento para el equilibrador de carga de Hola.

    Un sondeo de estado comprueba todos los toomake de instancias de máquina virtual que puede enviar tráfico de red. instancia de la máquina virtual de Hello con las comprobaciones de sondeo con error se quita del equilibrador de carga de hello hasta que deja de estar en línea y una comprobación de sondeo determina que es correcto.

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > plataforma de Microsoft Azure de Hello usa una dirección IPv4 estática, enrutable públicamente para una amplia variedad de escenarios de administración. dirección IP de Hello es 168.63.129.16. Ningún firewall debe bloquear esta dirección IP, ya que puede causar un comportamiento inesperado.
    > Con sentido tooAzure de equilibrio de carga interno, se usa esta dirección IP mediante la supervisión de sondeos de estado de mantenimiento de Hola de toodetermine equilibrador de carga de Hola para máquinas virtuales en un conjunto de equilibrio de carga. Si un grupo de seguridad de red es toorestrict usado tráfico tooAzure máquinas en un conjunto de carga equilibrada internamente o subred de red virtual tooa aplicado, asegúrese de que una regla de seguridad de red se agrega tráfico tooallow desde 168.63.129.16.

## <a name="create-nics"></a>Cree tarjetas NIC

Necesita toocreate NIC (o modificar los existentes) y asociarlos a tooNAT reglas, reglas de equilibrador de carga y sondeos.

1. Cree una NIC denominado *nic1 de carga equilibrada puede*y, a continuación, asociar hello *rdp1* NAT hello y regla *beilb* grupo de direcciones de back-end.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
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

2. Cree una NIC denominado *nic2 de carga equilibrada puede*y, a continuación, asociar hello *rdp2* NAT hello y regla *beilb* grupo de direcciones de back-end.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. Crear una máquina virtual denominada *DB1*y, a continuación, asociar Hola NIC denominado *nic1 de carga equilibrada puede*. Llama a una cuenta de almacenamiento *web1nrp* se crea antes de hello después de la ejecución del comando:

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > Hola a las máquinas virtuales en un toobe de necesidad de equilibrador de carga en el mismo conjunto de disponibilidad. Use `azure availset create` toocreate un conjunto de disponibilidad.

4. Crear una máquina virtual (VM) con el nombre *DB2*y, a continuación, asociar Hola NIC denominado *nic2 de carga equilibrada puede*. Llama a una cuenta de almacenamiento *web1nrp* se creó antes de ejecutar el siguiente comando de Hola.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>Eliminar un equilibrador de carga

tooremove un equilibrador de carga, use Hola siguiente comando:

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>Pasos siguientes

[Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)

