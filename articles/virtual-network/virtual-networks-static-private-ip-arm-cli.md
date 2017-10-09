---
title: "aaaConfigure de direcciones IP privadas para las máquinas virtuales - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure de direcciones IP privadas de máquinas virtuales mediante hello Azure interfaz de línea de comandos (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a>Configurar las direcciones IP privadas para una máquina virtual mediante Hola 2.0 de CLI de Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello 

Puede completar la tarea hello mediante uno de hello después de las versiones CLI: 

- [Azure 1.0 de CLI](virtual-networks-static-private-ip-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola 
- [Azure 2.0 CLI](#specify-a-static-private-ip-address-when-creating-a-vm) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación del Administrador de recursos de Hola. También puede [administrar dirección IP privada estática en el modelo de implementación clásica de hello](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> comandos de CLI de Azure 2.0 de ejemplo de Hola a continuación esperan un entorno simple ya creado. Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola se describe en [crear una red virtual](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Especificación de una dirección IP privada estática al crear una VM

una máquina virtual denominada toocreate *DNS01* en hello *front-end* subred de una red virtual denominada *TestVNet* con una dirección IP estática privada de *192.168.1.101*, Siga los pasos de hello siguientes:

1. Si aún no lo ha aún, instalar y configurar hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login). 

2. Crear una dirección IP pública para hello VM con hello [crear az red public-ip](/cli/azure/network/public-ip#create) comando. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.

    > [!NOTE]
    > Puede quiere o necesita toouse valores diferentes para los argumentos de esta y pasos siguientes, dependiendo de su entorno.
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    Resultado esperado:
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * `--resource-group`: Nombre del grupo de recursos de hello en qué dirección IP pública de toocreate Hola.
   * `--name`: Nombre de la dirección IP pública de Hola.
   * `--location`: Región azure en qué dirección IP pública de toocreate Hola.

3. Ejecute hello [crear nic de red az](/cli/azure/network/nic#create) comando toocreate una NIC con una dirección IP estática privada. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados. 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    Resultado esperado:
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    Parámetros:

    * `--private-ip-address`: Dirección IP privada estática para hello NIC.
    * `--vnet-name`: Nombre de red virtual de hello en qué toocreate Hola NIC.
    * `--subnet`: Nombre de subred de hello en qué hello toocreate NIC.

4. Ejecute hello [crear la máquina virtual de azure](/cli/azure/vm/nic#create) comando toocreate hello máquina virtual con la dirección IP pública de Hola y formación creada anteriormente. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    Resultado esperado:
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   Parámetros que no sean de hello básico [crear vm az](/cli/azure/vm#create) parámetros.

   * `--nics`: Nombre del programa Hola toowhich a Hola NIC virtual está conectado.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Recuperación de la información de la dirección IP privada estática para una VM

tooview Hola privada dirección IP estática que ha creado, ejecute hello siguiente comando de CLI de Azure y observar los valores de hello para *IP privada alloc (método)* y *dirección IP privada*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Resultado esperado:

```json
"192.168.1.101"
```

toodisplay Hola información específica de IP de hello NIC para esa máquina virtual, Hola consulta NIC específicamente:

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

salida de Hello es similar:

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a>Eliminación de una dirección IP privada estática de una VM

No se puede eliminar una dirección IP privada estática de una NIC en la CLI de Azure para implementaciones de Resource Manager. Debe:
- Crear una nueva NIC que use una dirección IP dinámica.
- Establecer Hola NIC en Hola Hola VM recién creado NIC. 

Hola toochange NIC para hello máquina virtual que se utiliza en los comandos de hello anteriores, siga los pasos de Hola a continuación.

1. Ejecute hello **crear nic de red de azure** comando toocreate una NIC nuevo mediante la asignación de IP dinámica con una nueva dirección IP. Tenga en cuenta que dado que no se especifica ninguna dirección IP, método de asignación de hello **dinámica**.

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    Resultado esperado:

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. Ejecute hello **conjunto de máquina virtual de azure** comando toochange hello NIC que se utiliza por hello máquina virtual.
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    Resultado esperado:
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > Si Hola VM es lo suficientemente grande como toohave más de una NIC, ejecute hello **nic de red de azure eliminar** comando toodelete Hola antigua NIC
   
## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .
* Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consulte hello [API de REST para IP reservadas](https://msdn.microsoft.com/library/azure/dn722420.aspx).

