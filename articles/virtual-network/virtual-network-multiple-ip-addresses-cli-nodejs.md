---
title: aaaVM con varias direcciones IP con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooassign varias direcciones IP tooa máquina virtual usando Hola 1.0 de CLI de Azure | Administrador de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>Asignar varias direcciones IP máquinas toovirtual mediante Azure CLI 1.0

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Este artículo explica cómo toocreate una máquina virtual (VM) a través de modelo de implementación de Azure Resource Manager de hello mediante Hola 1.0 de CLI de Azure. No se puede asignar tooresources que se creó mediante el modelo de implementación clásica de Hola a varias direcciones IP. más información acerca de los modelos de implementación de Azure, lea hello toolearn [comprender los modelos de implementación](../resource-manager-deployment-model.md) artículo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Creación de una máquina virtual con varias direcciones IP

Puede completar esta tarea mediante hello Azure CLI 1.0 (en este artículo) o hello [CLI de Azure 2.0](virtual-network-multiple-ip-addresses-cli.md). pasos de Hola que siguen explican cómo toocreate aborda un máquina virtual con varias IP de ejemplo, tal y como se describe en el escenario de Hola. Cambie los nombres de variable los y tipos de direcciones IP según sea necesario para la implementación.

1. Instalar y configurar hello Azure CLI 1.0 por hello siguiente pasos en hello [instalar y configurar hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo e inicie sesión en su cuenta de Azure con hello `azure-login` comando.

2. Cree un grupo de recursos:
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. Cree una red virtual:

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. Crear una subred de red virtual de hello:

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. Crear una cuenta de almacenamiento para VM Hola. Antes de ejecutar Hola siguiente comando, reemplace *mystorageaccount* con un nombre único. nombre de Hello debe ser único en Azure:

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. Crear configuraciones de IP, una NIC de Hola y asignar Hola IP configuraciones toohello equipo NIC. Puede agregar, quitar o cambiar las configuraciones de hello según sea necesario. Hola siguiendo configuraciones se describe en el escenario de hello:

    **IPConfig-1**

    Escriba los comandos de Hola que siguen toocreate:

    - Un recurso de dirección IP pública con una dirección IP pública estática
    - Una NIC, asignación de dirección IP pública de Hola y un estático tooit de dirección IP privada.
    
    Reemplace *mypublicdns* con un nombre que sea único dentro de hello ubicación de Azure.

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > Las direcciones IP públicas tienen un precio simbólico. toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción. toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.

    **IPConfig-2**

     Un nuevo recurso de dirección IP público y una nueva configuración de IP con una dirección IP pública estática y una dirección IP privada estática, escriba Hola después toocreate de comandos:
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **IPConfig-3**

    Escriba Hola después comandos toocreate una configuración de IP con una dirección IP privada estática y ninguna dirección IP pública:

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >Aunque este artículo asigna todos los tooa de configuraciones de IP única NIC, también puede asignar varias IP configuraciones tooany NIC en una máquina virtual. toolearn cómo leer de una máquina virtual con varias NIC toocreate Hola crear una máquina virtual con varias NIC el artículo.

7. Creación de una máquina virtual Linux 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    toochange Hola v2 de tooStandard DS2 de tamaño de máquina virtual, por ejemplo, basta con agregar Hola después de la propiedad `--vm-size Standard_DS3_v2` toohello `azure vm create` comando en el paso 6.

8. Escriba Hola después comando tooview hello NIC y Hola asociados configuraciones IP:

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. Sistema operativo de la VM de toohello las direcciones IP privada de agregar Hola siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.

## <a name="add"></a>Agregar tooa de direcciones IP virtual

Puede agregar adicionales pública y privada IP direcciones tooan existente NIC siguiendo los pasos de Hola que siguen. ejemplos de Hello parten de hello [escenario](#Scenario) descrito en este artículo.

1. Abra completa hello restantes pasos de esta sección dentro de una sola sesión CLI y CLI de Azure. Si aún no tiene la CLI de Azure instalado y configurado, Hola completa los pasos de hello [instalar y configurar hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo e inicie sesión en su cuenta de Azure.

2. Complete los pasos de hello en una de las siguientes secciones, según sus requisitos de hello:

    - **Incorporación de una dirección IP privada**
    
        tooadd una tooa de dirección IP privada NIC, debe crear una configuración de IP mediante el siguiente comando de Hola. dirección estática Hola debe ser una dirección no utilizada para la subred de Hola.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        Cree tantas configuraciones como sea necesario mediante nombres de configuración únicos y direcciones IP privadas (para las configuraciones con direcciones IP estáticas).

    - **Incorporación de una dirección IP pública**
    
        Se agrega una dirección IP pública asociando tooeither una nueva configuración de IP o una configuración de IP existente. Complete los pasos de hello en una de las secciones de Hola que siguen, como sea necesario.

        > [!NOTE]
        > Las direcciones IP públicas tienen un precio simbólico. toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción. toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.
        >

        **Asociar Hola recursos tooa nueva configuración de IP**
    
        Siempre que agregue una dirección IP pública en una nueva configuración de IP, también debe agregar una dirección IP privada, porque todas las configuraciones de IP deben tener una dirección IP privada. Puede agregar un recurso de dirección IP pública existente o crear uno nuevo. toocreate uno nuevo, escriba el siguiente comando de hello:

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        toocreate una nueva configuración de IP con una dirección IP privada estática y Hola asociados *myPublicIP3* IP pública recurso Dirección, escriba el siguiente comando de hello:

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **Asociar la configuración de IP existente de hello recursos tooan**

        Configuración de IP de tooan asociado que ya no tiene asociado sólo puede ser un recurso de dirección IP público. Puede determinar si una configuración de IP tiene una dirección IP pública asociada mediante la especificación de hello siguiente comando:

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        Busque un toohello similar de la línea que aparece más adelante para IPConfig-3 en hello devolvía los resultados:

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        Desde hello **IP pública** columna para *IpConfig-3* está en blanco, ningún recurso de dirección IP pública está asociada actualmente tooit. Puede agregar una existente pública IP dirección recursos tooIpConfig-3, o escriba Hola después toocreate comando uno:

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        Escriba el siguiente comando con el nombre por la configuración de IP existente de recursos toohello de dirección IP pública de tooassociate Hola de hello *IPConfig-3*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. Ver direcciones IP privadas de Hola y Hola pública IP dirección recursos asignado toohello NIC escribiendo Hola el siguiente comando:

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      Hola devuelve el resultado será similar siguiente toohello:
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. Agregar direcciones IP privadas Hola que se ha agregado el sistema operativo la VM de toohello NIC toohello siguiendo las instrucciones de Hola Hola [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo. No agregue el sistema de operativo para toohello el público direcciones IP Hola.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
