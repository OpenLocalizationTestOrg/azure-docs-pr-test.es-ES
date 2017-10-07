---
title: aaaCreate un entorno de Linux con hello 2.0 de CLI de Azure | Documentos de Microsoft
description: "Crear almacenamiento, una VM de Linux, una red virtual y subred, un equilibrador de carga, una NIC, una dirección IP pública y un grupo de seguridad de red, todo ello desde Hola descárguese de corriente mediante el uso de hello 2.0 de CLI de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a>Crear una máquina virtual de Linux completa con hello CLI de Azure
tooquickly crear una máquina virtual (VM) en Azure, puede usar un solo comando de CLI de Azure que usa de forma predeterminada valores toocreate cualquier requiere compatibilidad con recursos. Los recursos como una red virtual, una dirección IP pública y reglas de grupo de seguridad de red se crean automáticamente. Para tener más control de su entorno de producción usar, puede crear estos recursos antes de tiempo y, a continuación, agregue el toothem de las máquinas virtuales. En este artículo le guiará en el proceso de cómo toocreate una máquina virtual y cada uno de Hola recursos de soporte uno por uno.

Asegúrese de que ha instalado hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) y tooan inició Azure cuenta con [inicio de sesión de az](/cli/azure/#login).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.

## <a name="create-resource-group"></a>Creación de un grupo de recursos
Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. Se debe crear un grupo de recursos antes que una máquina virtual y los recursos de red virtual de apoyo. Crear grupo de recursos de hello con [crear grupo az](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create --name myResourceGroup --location eastus
```

De forma predeterminada, la salida de hello de comandos de CLI de Azure está en JSON (JavaScript Object Notation). toochange Hola predeterminado salida tooa lista o tabla, por ejemplo, utilice [az configurar--salida](/cli/azure/#configure). También puede agregar `--output` cambiar tooany comando para una sola vez en formato de salida. Hello en el ejemplo siguiente se muestra resultado JSON Hola Hola `az group create` comando:

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a>Creación de una red virtual y una subred
A continuación, crear una red virtual en Azure y una subred de toowhich puede crear las máquinas virtuales. Use [crear red virtual de red az](/cli/azure/network/vnet#create) toocreate una red virtual denominada *myVnet* con hello *192.168.0.0/16* prefijo de dirección. También agregar una subred denominada *mySubnet* con prefijo de dirección de hello *192.168.1.0/24*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

salida de Hello muestra subred Hola que lógicamente se crea dentro de la red virtual de hello:

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a>Crear una dirección IP pública
Ahora cree una dirección IP pública con [az network public-ip create](/cli/azure/network/public-ip#create). Esta dirección IP pública permite tooconnect tooyour máquinas virtuales de hello Internet. Debido a la dirección predeterminada hello es dinámica, también creamos una entrada DNS con nombre con hello `--domain-name-label` opción. Hello en el ejemplo siguiente se crea una IP pública denominada *myPublicIP* con el nombre DNS de Hola de *mypublicdns*. Como nombre DNS de hello debe ser único, proporcionar su propio nombre DNS único:

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

Salida:

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a>Crear un grupo de seguridad de red
flujo de hello toocontrol de tráfico dentro y fuera de las máquinas virtuales, cree un grupo de seguridad de red. Un grupo de seguridad de red puede ser aplicada tooa NIC o subred. Hello siguiente ejemplo se utiliza [crear az red nsg](/cli/azure/network/nsg#create) toocreate un grupo de seguridad de red denominado *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

Definir reglas que permitan o denieguen el tráfico específico de Hola. tooallow las conexiones entrantes en el puerto 22 (SSH de toosupport), cree una regla de entrada para el grupo de seguridad de red de hello con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create). Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

tooallow las conexiones entrantes en el puerto 80 (tráfico de web toosupport), agregue otra regla de grupo de seguridad de red. Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRuleHTTP*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

Examinar el grupo de seguridad de red de Hola y las reglas con [show de nsg de red az](/cli/azure/network/nsg#show):

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

Salida:

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a>Crear un adaptador de red virtual
Tarjetas de interfaz de red virtual (NIC) están disponibles mediante programación porque puede aplicar reglas tootheir uso. También puede tener más de una. Siguiente hello [crear nic de red az](/cli/azure/network/nic#create) comando, cree una NIC denominada *myNic* y asocie al grupo de seguridad de red de Hola. dirección IP pública de Hola *myPublicIP* también está asociado a la NIC virtual Hola.

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

Salida:

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a>Crear un conjunto de disponibilidad
Los conjuntos de disponibilidad ayudan a propagar las máquinas virtuales a los dominios de error y de actualización. Aunque solo crear ahora una máquina virtual, es mejor práctica toouse disponibilidad conjuntos toomake sea más fácil tooexpand Hola futuras. 

Los dominios de error definen un grupo de máquinas virtuales que comparten una fuente de alimentación común y un conmutador de red. De forma predeterminada, máquinas virtuales de Hola que estén configuradas en el conjunto de disponibilidad están separadas a través de dominios de error toothree. Un problema de hardware en uno de estos dominios de error no afecta a todas las máquinas virtuales que ejecutan la aplicación.

Dominios de actualización indican los grupos de máquinas virtuales y el hardware físico subyacente que puede reiniciarse en hello mismo tiempo. Durante el mantenimiento planeado, orden de hello en los de actualización de dominios se reinician no sea secuencial, pero solo una actualización de dominio se reinicia cada vez.

Azure distribuye automáticamente las máquinas virtuales entre dominios de error y actualización de hello cuando se coloquen en un conjunto de disponibilidad. Para obtener más información, consulte [administrar la disponibilidad de Hola de máquinas virtuales](manage-availability.md).

Cree un conjunto de disponibilidad para las máquinas virtuales con [az vm availability-set create](/cli/azure/vm/availability-set#create). Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad *myAvailabilitySet*:

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

dominios de error de notas de la salida de Hello y dominios de actualización:

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a>Crear máquinas virtuales de Linux de Hola
Ha creado toosupport de recursos de red de hello VM accesibles desde Internet. Ahora cree una máquina virtual y protéjala con una clave SSH. En este caso, vamos toocreate una VM Ubuntu según hello LTS más reciente. Puede encontrar imágenes adicionales con [az vm image list](/cli/azure/vm/image#list), como se explica en [Finding Azure VM images (Búsqueda de imágenes de máquina virtual de Azure)](cli-ps-findimage.md).

También especificamos un toouse clave SSH para la autenticación. Si no tiene un par de claves públicas de SSH, puede [crearlos](mac-create-ssh-keys.md) o usar hello `--generate-ssh-keys` toocreate parámetro usarlas para usted. Si ya tiene un par de claves, este parámetro usa las claves existentes en `~/.ssh`.

Crear Hola VM si se ponen todos nuestros recursos e información junto con hello [crear vm az](/cli/azure/vm#create) comando. Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM con hello entrada DNS que proporcionó al crear la dirección IP pública Hola. Esto `fqdn` se muestra en la salida de hello a medida que cree la máquina virtual:

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Salida:

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

Puede instalar NGINX y vea toohello de flujo de tráfico de hello máquina virtual. Instale NGINX como se indica a continuación:

```bash
sudo apt-get install -y nginx
```

sitio NGINX toosee Hola predeterminado en acción, abra el explorador web y escriba su FQDN:

![Sitio NGINX predeterminado en la máquina virtual](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a>Exportar como plantilla
¿Qué ocurre si ahora desea toocreate un entorno de desarrollo adicional con hello mismos parámetros o un entorno de producción que coincida con él? Administrador de recursos usa plantillas JSON que definen todos los parámetros de Hola para su entorno. Puede crear entornos enteros haciendo referencia a esta plantilla JSON. También puede [generar plantillas JSON de forma manual](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o exportar una plantilla JSON de entorno toocreate Hola existente para usted. Use [exportación de grupo az](/cli/azure/group#export) tooexport el recurso de grupo como sigue:

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

Este comando crea hello `myResourceGroup.json` archivo en el directorio de trabajo actual. Cuando se crea un entorno de esta plantilla, le pediremos todos los nombres de recursos de Hola. Puede rellenar estos nombres en el archivo de plantilla mediante la adición de hello `--include-parameter-default-value` toohello parámetro `az group export` comando. Editar los nombres de recursos JSON plantilla toospecify hello, o [crear un archivo parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifica los nombres de recursos de Hola.

un entorno a partir de la plantilla, utilice toocreate [Crear implementación de grupo az](/cli/azure/group/deployment#create) como se indica a continuación:

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

Es recomendable tooread [más información acerca de cómo toodeploy de plantillas de](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Obtenga información acerca de cómo usar el archivo de parámetros de hello tooincrementally entornos de actualización y tener acceso a plantillas desde una sola ubicación de almacenamiento.

## <a name="next-steps"></a>Pasos siguientes
Ahora está listo toobegin trabajar con varios componentes de red y máquinas virtuales. Puede usar este toobuild de entorno de ejemplo horizontalmente la aplicación con los componentes principales de hello introducidos aquí.
