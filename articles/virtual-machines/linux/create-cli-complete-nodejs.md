---
title: aaaCreate un entorno completo de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "Crear almacenamiento, una VM de Linux, una red virtual y subred, un equilibrador de carga, una NIC, una dirección IP pública y un grupo de seguridad de red, todo ello desde Hola descárguese de corriente mediante el uso de hello 1.0 de CLI de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>Crear un entorno completo de Linux con hello Azure CLI 1.0
En este artículo, vamos a crear una red sencilla con un equilibrador de carga y un par de máquinas virtuales útiles para el desarrollo y la computación simple. Le guían en el proceso de Hola por comando, hasta que haya trabajo dos, proteja toowhich de máquinas virtuales de Linux que puede conectarse desde cualquier lugar en hello Internet. A continuación, puede mover en entornos y las redes complejas toomore.

A lo largo de la manera de hello, información sobre jerarquía de dependencias de Hola que ofrece modelo de implementación del Administrador de recursos de Hola y sobre Cuánta energía proporciona. Después de ver cómo se crea el sistema de hello, puede volver a compilarlo mucho más rápidamente mediante el uso de [plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Además, después de obtener información sobre cómo encajan partes de Hola de su entorno, crear plantillas tooautomate les hace más fácil.

entorno de Hello contiene:

* Dos máquinas virtuales dentro de un conjunto de disponibilidad.
* Un equilibrador de carga con una regla de equilibrio de carga en el puerto 80.
* Grupo de seguridad de red (NSG) reglas tooprotect la máquina virtual de tráfico no deseado.

toocreate este entorno personalizado, deberá hello más reciente [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en modo de administrador de recursos (`azure config mode arm`). También necesitará una herramienta de análisis JSON. En este ejemplo se usa [jq](https://stedolan.github.io/jq/).


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="quick-commands"></a>Comandos rápidos
Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base tooupload comandos tooAzure de una máquina virtual. Obtener más información y el contexto de cada paso puede encontrarse en el resto de saludo del documento de hello, a partir de [aquí](#detailed-walkthrough).

Asegúrese de que dispone de [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) iniciado la sesión y utilizar el modo de administrador de recursos:

```azurecli
azure config mode arm
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.

Crear grupo de recursos de Hola. Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` ubicación:

```azurecli
azure group create -n myResourceGroup -l westeurope
```

Comprobar el grupo de recursos de hello mediante analizador JSON de hello:

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Crear cuenta de almacenamiento de Hola. Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`. (nombre de cuenta de almacenamiento de hello debe ser único, por lo que proporcionar su propio nombre único.)

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

Comprobar la cuenta de almacenamiento de hello mediante analizador JSON de hello:

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

Crear red virtual de Hola. Hello en el ejemplo siguiente se crea una red virtual denominada `myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

Cree una subred. Hello en el ejemplo siguiente se crea una subred denominada `mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

Comprobar Hola de red virtual y subred mediante el analizador JSON de hello:

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Cree una IP pública. Hello en el ejemplo siguiente se crea una IP pública denominada `myPublicIP` con el nombre DNS de Hola de `mypublicdns`. (nombre DNS de hello debe ser único, por lo que proporcionar su propio nombre único.)

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

Crear el equilibrador de carga de Hola. Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre `myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

Crear un grupo IP front-end de equilibrador de carga de Hola y asociar IP pública Hola. Hello en el ejemplo siguiente se crea un grupo IP front-end denominado `mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

Crear grupo IP de back-end de Hola Hola equilibrador de carga. Hello en el ejemplo siguiente se crea un grupo IP de back-end denominado `myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

Crear reglas NAT (traducción) de dirección Hola equilibrador de carga de red de entrada de SSH. Hello en el ejemplo siguiente se crea dos reglas de equilibrador de carga, `myLoadBalancerRuleSSH1` y `myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

Crear sitio web de hello equilibrador de carga de reglas NAT de entrada para saludo. Hello en el ejemplo siguiente se crea una regla de equilibrador de carga denominada `myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

Crear el sondeo de estado del equilibrador de carga de Hola. Hello en el ejemplo siguiente se crea un sondeo TCP denominado `myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

Comprobar equilibrador de carga de hello, grupos de direcciones IP y las reglas de NAT mediante el analizador JSON de hello:

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

Crear Hola primera interfaz tarjeta de red (NIC). Reemplace hello `#####-###-###` secciones con su propio identificador de suscripción de Azure. Su suscripción ID se indica en la salida de hello de **jq** al examinar los recursos de Hola que se va a crear. Su identificador de suscripción también puede verlo con `azure account list`.

Hello en el ejemplo siguiente se crea una NIC denominada `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

Crear NIC de hello segundo. Hello en el ejemplo siguiente se crea una NIC denominada `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

Comprobar Hola dos NIC mediante el analizador JSON de hello:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

Crear grupo de seguridad de red de Hola. Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado `myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

Agregue dos reglas de entrada para el grupo de seguridad de red de Hola. Hello en el ejemplo siguiente se crea dos reglas, `myNetworkSecurityGroupRuleSSH` y `myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

Comprobar grupo de seguridad de red de Hola y reglas de entrada mediante el analizador JSON de hello:

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

Enlace de seguridad de la red de hello grupo toohello dos NIC:

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

Crear conjunto de disponibilidad de Hola. Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad `myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

Crear Hola primera VM de Linux. Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Crear hello segunda VM de Linux. Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Use Hola JSON analizador tooverify que todo lo que se creó:

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

Exportar sus nuevo entorno tooa tooquickly volver a crear nuevas instancias de plantilla:

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>Tutorial detallado
Hello pasos detallados que van a continuación explican lo que hace cada comando mientras se generan fuera de su entorno. Estos conceptos sirven de ayuda mientras crea sus propios entornos personalizados con fines de desarrollo o producción.

Asegúrese de que dispone de [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) iniciado la sesión y utilizar el modo de administrador de recursos:

```azurecli
azure config mode arm
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.

## <a name="create-resource-groups-and-choose-deployment-locations"></a>Creación de grupos de recursos y elección de las ubicaciones para la implementación
Grupos de recursos de Azure son entidades de lógica de implementación que contienen información y metadatos tooenable Hola lógica administración de la configuración de las implementaciones de recursos. Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` ubicación:

```azurecli
azure group create --name myResourceGroup --location westeurope
```

Salida:

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento
Necesita cuentas de almacenamiento para los discos de máquina virtual y para los discos de datos adicionales que desea que tooadd. Las cuentas de almacenamiento se crean casi inmediatamente después de crear los grupos de recursos.

Aquí usamos hello `azure storage account create` comando, pasar la ubicación de Hola de cuenta de hello, grupo de recursos de Hola que controla la base de datos y tipo de Hola de compatibilidad de almacenamiento que desee. Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada `mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

Salida:

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

tooexamine nuestro recurso de grupo mediante el uso de hello `azure group show` command, vamos a usar hello [jq](https://stedolan.github.io/jq/) herramienta junto con hello `--json` opción de CLI de Azure. (Puede usar **jsawk** o cualquier biblioteca de idioma que prefiera tooparse Hola JSON.)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Salida:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

cuenta de almacenamiento tooinvestigate Hola utilizando Hola CLI, primero debe claves y nombres de cuenta de hello tooset. Reemplazar Hola nombre de cuenta de almacenamiento de Hola Hola siguiente ejemplo con un nombre que elija:

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

Luego podrá ver la información de almacenamiento fácilmente:

```azurecli
azure storage container list
```

Salida:

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>Creación de una red virtual y una subred
A continuación va tooneed toocreate una red virtual que se ejecuta en Azure y una subred en la que puede crear las máquinas virtuales. Hello en el ejemplo siguiente se crea una red virtual denominada `myVnet` con hello `192.168.0.0/16` prefijo de dirección:

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

Salida:

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

De nuevo, vamos a usar la opción de json: Hola de `azure group show` y `jq` toosee cómo estamos creando nuestros recursos. Ya tenemos un recurso de `storageAccounts` y un recurso de `virtualNetworks`.  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Salida:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

Ahora vamos a crear una subred en hello `myVnet` red virtual en qué Hola se implementan máquinas virtuales. Usamos hello `azure network vnet subnet create` comando, junto con los recursos de hello ya hemos creado: Hola `myResourceGroup` hello y grupo de recursos `myVnet` red virtual. En el siguiente ejemplo de Hola, agregamos con el nombre de subred de hello `mySubnet` con prefijo de dirección de subred Hola `192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

Salida:

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

Porque la subred de hello es, lógicamente, dentro de la red virtual de hello, adentrarnos para obtener información de subred de hello con un comando ligeramente diferente. se utiliza el comando Hello es `azure network vnet show`, pero continuamos salida JSON de hello tooexamine utilizando `jq`.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Salida:

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>Crear una dirección IP pública
Ahora vamos a crear la dirección IP pública hello (PIP) que asignamos tooyour equilibrador de carga. Le permite tooconnect tooyour máquinas virtuales de hello Internet mediante el uso de hello `azure network public-ip create` comando. Debido a la dirección predeterminada hello es dinámica, creamos una entrada DNS con nombre en hello **cloudapp.azure.com** dominio mediante el uso de hello `--domain-name-label` opción. Hello en el ejemplo siguiente se crea una IP pública denominada `myPublicIP` con el nombre DNS de Hola de `mypublicdns`. Como nombre DNS de hello debe ser único, proporcionar su propio nombre DNS único:

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

Salida:

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

Hello dirección IP pública también es un recurso de nivel superior, por lo que puede verla con `azure group show`.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Salida:

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

Puede investigar más detalles de recursos, incluidos el nombre de dominio completo (FQDN) de hello del subdominio de hello, mediante el uso de hello completa `azure network public-ip show` comando. se ha asignado el recurso de dirección IP público Hola lógicamente, pero todavía no se ha asignado una dirección específica. tooobtain una dirección IP, que vaya tooneed un equilibrador de carga, que todavía no hemos creado.

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

Salida:

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>Creación de un equilibrador de carga y grupos de direcciones IP
Cuando se crea un equilibrador de carga, permite el tráfico toodistribute en varias máquinas virtuales. También proporciona aplicaciones de tooyour de redundancia mediante la ejecución de varias máquinas virtuales que responden a las solicitudes de toouser en caso de hello de mantenimiento o cargas pesadas. Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre `myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

Salida:

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

Nuestro equilibrador de carga está bastante vacío, así que vamos a crear algunos grupos de direcciones IP. Queremos toocreate dos grupos de direcciones IP para el equilibrador de carga, uno para el front-end de hello y otro para back-end de Hola. grupo de direcciones IP de front-end de Hello es sean visible públicamente. También es Hola ubicación toowhich que asignamos Hola PIP que hemos creado con anterioridad. A continuación, utilizamos grupo back-end de hello como una ubicación para nuestro tooconnect de máquinas virtuales a. De este modo, el tráfico de hello puedan fluir a través de toohello de equilibrador de carga de hello las máquinas virtuales.

En primer lugar, vamos a crear nuestro grupo IP de front-end. Hello en el ejemplo siguiente se crea un grupo de servidor front-end denominado `myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

Salida:

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

Tenga en cuenta cómo se usa hello `--public-ip-name` cambiar toopass Hola `myPublicIP` que hemos creado con anterioridad. Asignar dirección IP pública de hello equilibrador de carga de dirección toohello permite tooreach las máquinas virtuales a través de Internet de Hola.

Después, vamos a crear nuestro el grupo IP, esta vez para el tráfico de back-end. Hello en el ejemplo siguiente se crea un grupo de back-end denominado `myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

Salida:

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

Podemos ver cómo el equilibrador de carga está realizando consultando con `azure network lb show` y examinar los resultados JSON de hello:

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

Salida:

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>Creación de reglas NAT del equilibrador de carga
tooget el tráfico que fluye a través de nuestro equilibrador de carga, necesitamos toocreate reglas NAT (traducción) de direcciones de red que especifican acciones de entrada o de salida. Puede especificar Hola protocolo toouse, a continuación, asignar puertos externos toointernal puertos según sea necesario. Para nuestro entorno, vamos a crear algunas reglas que permiten SSH a través de nuestro tooour de equilibrador de carga de máquinas virtuales. Configuramos toodirect tooTCP puerto 22 de TCP puertos 4222 y 4223 en nuestra máquinas virtuales (que crearemos más adelante). Hello en el ejemplo siguiente se crea una regla denominada `myLoadBalancerRuleSSH1` toomap TCP puerto 4222 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

Salida:

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

Repita el procedimiento de hello para la segunda regla NAT de SSH. Hello en el ejemplo siguiente se crea una regla denominada `myLoadBalancerRuleSSH2` toomap TCP puerto 4223 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

También vamos a seguir adelante y crear una regla NAT para el puerto TCP 80 para el tráfico de web, enlazar regla hello tooour grupos de direcciones IP. Si se enlazó Hola regla tooan de direcciones IP, en lugar de enlazar Hola regla tooour máquinas virtuales individualmente, podemos agregar o quitar las máquinas virtuales del grupo de direcciones IP de Hola. equilibrador de carga de Hello ajusta automáticamente flujo Hola de tráfico. Hello en el ejemplo siguiente se crea una regla denominada `myLoadBalancerRuleWeb` toomap TCP puerto 80 tooport 80:

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

Salida:

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>Creación del sondeo de estado de un equilibrador de carga
Un estado de sondeo periódicamente comprobaciones en hello las máquinas virtuales que están detrás de nuestro toomake de equilibrador de carga que encuentra operativo y responde toorequests tal como se define. Si no es así, que se quitan del tooensure de operación que los usuarios no están dirigidas toothem. Puede definir las comprobaciones personalizadas para el sondeo de estado de hello, junto con los intervalos y los valores de tiempo de espera. Para más información sobre los sondeos de estado, consulte [Sondeos del Equilibrador de carga](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hello en el ejemplo siguiente se crea un TCP mantenimiento sondea con nombre `myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

Salida:

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

Aquí, especificamos un intervalo de 15 segundos para las comprobaciones de estado. Se puede perder un máximo de cuatro sondeos (un minuto) antes de equilibrador de carga de hello tiene en cuenta que hospedan Hola deja de funcionar.

## <a name="verify-hello-load-balancer"></a>Compruebe el equilibrador de carga de Hola
Ahora se realiza la configuración de equilibrador de carga de Hola. Estos son los pasos de hello que llevados a cabo:

1. Creó un equilibrador de carga.
2. Ha creado un grupo IP de front-end y asignado un tooit IP pública.
3. Creó un grupo de direcciones IP back-end al que pueden conectarse las máquinas virtuales.
4. Crear reglas NAT que permiten a las máquinas virtuales toohello SSH para la administración, junto con una regla que permita el puerto TCP 80 para nuestra aplicación web.
5. Ha agregado un Hola de comprobación de mantenimiento sondeo tooperiodically máquinas virtuales. Este sondeo de estado se asegura de que los usuarios no intentan tooaccess una máquina virtual que ya no está funcionando o que sirve al contenido.

Revisemos cuál es ahora el aspecto del equilibrador de carga:

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

Salida:

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>Crear un toouse NIC con hello VM de Linux
NIC están disponibles mediante programación porque puede aplicar reglas tootheir uso. También puede tener más de una. En el siguiente de hello `azure network nic create` de comandos, enlazar grupo de direcciones IP de hello NIC toohello carga back-end y asociarlo con hello tráfico SSH de toopermit de regla NAT.

Reemplace hello `#####-###-###` secciones con su propio identificador de suscripción de Azure. Su suscripción ID se indica en la salida de hello de `jq` al examinar los recursos de Hola que se va a crear. Su identificador de suscripción también puede verlo con `azure account list`.

Hello en el ejemplo siguiente se crea una NIC denominada `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

Salida:

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

Puede ver detalles de hello examinando recursos Hola directamente. Examinar recursos de hello mediante hello `azure network nic show` comando:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

Salida:

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

Ahora creamos Hola segundo NIC, enlazar en el grupo de direcciones IP de back-end de tooour de nuevo. Esta regla NAT de tiempo Hola segunda permite el tráfico SSH. Hello en el ejemplo siguiente se crea una NIC denominada `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>Creación de un grupo de seguridad de red (NSG) y las reglas
Ahora se crea un grupo de seguridad de red y Hola entrantes reglas que rigen tener acceso a la NIC de toohello. Un grupo de seguridad de red puede ser aplicada tooa NIC o subred. Definir el flujo de hello toocontrol de reglas de tráfico de dentro y fuera de las máquinas virtuales. Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado `myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

Vamos a agregar regla de entrada de Hola de hello NSG tooallow conexiones entrantes en el puerto 22 (SSH de toosupport). Hello en el ejemplo siguiente se crea una regla denominada `myNetworkSecurityGroupRuleSSH` tooallow TCP en el puerto 22:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

Ahora vamos a agregar regla de entrada de Hola de hello NSG tooallow conexiones entrantes en el puerto 80 (tráfico de web toosupport). Hello en el ejemplo siguiente se crea una regla denominada `myNetworkSecurityGroupRuleHTTP` tooallow TCP en el puerto 80:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> regla de entrada de Hello es un filtro para las conexiones de red de entrada. En este ejemplo, se enlaza hello NSG toohello NIC virtual de máquinas virtuales, lo que significa que cualquier tooport solicitud 22 se pasa a través de toohello NIC en la máquina virtual. Esta regla de entrada es sobre una conexión de red y no sobre un punto de conexión, como en el caso de las implementaciones clásicas. tooopen un puerto, debe dejar hello `--source-port-range` establecido demasiado '\*' tooaccept (valor predeterminado de hello) entrada las solicitudes de **cualquier** solicitando el puerto. Los puertos suelen ser dinámicos.
>
>

## <a name="bind-toohello-nic"></a>Enlazar toohello NIC
Enlazar hello NSG toohello NIC. Necesitamos tooconnect nuestro NIC con nuestro grupo de seguridad de red. Ejecutar ambos comandos, toohook tanto de nuestro NIC:

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>Crear un conjunto de disponibilidad
Los conjuntos de disponibilidad ayudan a propagar las máquinas virtuales a los dominios de error y dominios de actualización. Vamos a crear un conjunto de disponibilidad para sus máquinas virtuales. Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad `myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

Los dominios de error definen un grupo de máquinas virtuales que comparten una fuente de alimentación común y un conmutador de red. De forma predeterminada, máquinas virtuales de Hola que estén configuradas en el conjunto de disponibilidad están separadas a través de dominios de error toothree. idea Hello es que un problema de hardware en uno de estos dominios de error no afecta a cada máquina virtual que se ejecuta la aplicación. Azure distribuye automáticamente las máquinas virtuales entre dominios de error de hello cuando se coloquen en un conjunto de disponibilidad.

Dominios de actualización indican los grupos de máquinas virtuales y el hardware físico subyacente que puede reiniciarse en hello mismo tiempo. orden de Hello en el que se reinician los dominios de actualización no puede ser secuencial durante el mantenimiento planeado, pero se reinicia solo una actualización a la vez. De nuevo, Azure distribuye automáticamente las máquinas virtuales en los dominios de actualización al incluirlos en un sitio de disponibilidad.

Obtenga más información sobre [administrar la disponibilidad de Hola de máquinas virtuales](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="create-hello-linux-vms"></a>Crear máquinas virtuales de Linux de Hola
Ha creado los recursos de red y almacenamiento de hello máquinas virtuales toosupport accesible desde Internet. Ahora crearemos dichas máquinas virtuales y las protegeremos con una clave SSH sin contraseña. En este caso, vamos toocreate una VM Ubuntu según hello LTS más reciente. Vamos a buscar esa información de la imagen mediante `azure vm image list`, tal como se describe en el artículo sobre cómo [buscar imágenes de máquina virtual de Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Se selecciona una imagen mediante el comando de hello `azure vm image list westeurope canonical | grep LTS`. En este caso, usamos `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`. Último campo hello, pasamos `latest` para que en un futuro Hola obtenemos siempre compilación más reciente de Hola. (cadena Hola usamos es `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).

Este paso siguiente es familiar tooanyone que ya ha creado un ssh clave de rsa pública y privada emparejar en Linux o Mac usando **ssh-keygen - t rsa -b 2048**. Si no tiene ningún par de claves de certificado en el directorio `~/.ssh` , puede crearlas:

* Automáticamente, mediante el uso de hello `azure vm create --generate-ssh-keys` opción.
* Manualmente, mediante [Hola instrucciones toocreate ellos usted mismo](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Como alternativa, puede usar hello `--admin-password` método tooauthenticate las conexiones SSH después Hola máquina virtual se crea. Este método suele ser menos seguro.

Creamos Hola VM si se ponen todos nuestros recursos e información junto con hello `azure vm create` comando:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Salida:

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

Puede conectar tooyour VM inmediatamente mediante las claves SSH de forma predeterminada. Asegúrese de que especifique el puerto adecuado de hello puesto que estamos pasando a través del equilibrador de carga de Hola. (Para la primera VM, configuramos Hola NAT regla tooforward puerto 4222 tooour VM.)

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

Salida:

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

Voy a crear la segunda máquina virtual en hello misma manera:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Y ahora puede usar hello `azure vm show myResourceGroup myVM1` comando tooexamine lo que ha creado. Llegados a este punto, ejecuta las máquinas virtuales con Ubuntu detrás de un equilibrador de carga en Azure en las que solo puede iniciar sesión con el par de claves SSH (porque las contraseñas están deshabilitadas). Puede instalar nginx o httpd, implementar una aplicación web y ver el tráfico de hello fluyen a través de hello tooboth de equilibrador de carga de máquinas virtuales de Hola.

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

Salida:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>Entorno de Hola de exportación como plantilla
Ahora que ha creado este entorno, ¿qué ocurre si desea toocreate un entorno de desarrollo adicional con hello mismos parámetros o un entorno de producción que coincida con él? Administrador de recursos usa plantillas JSON que definen todos los parámetros de Hola para su entorno. Puede crear entornos enteros haciendo referencia a esta plantilla JSON. También puede [generar plantillas JSON de forma manual](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o exportar una plantilla JSON de entorno toocreate Hola existente para usted:

```azurecli
azure group export --name myResourceGroup
```

Este comando crea hello `myResourceGroup.json` archivo en el directorio de trabajo actual. Cuando se crea un entorno de esta plantilla, le pediremos todos los nombres de recursos de hello, incluidos los nombres de hello para el equilibrador de carga de hello, interfaces de red o máquinas virtuales. Puede rellenar estos nombres en el archivo de plantilla mediante la adición de hello `-p` o `--includeParameterDefaultValue` toohello parámetro `azure group export` comando que se mostró anteriormente. Editar los nombres de recursos JSON plantilla toospecify hello, o [crear un archivo parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifica los nombres de recursos de Hola.

toocreate un entorno a partir de la plantilla:

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

Es recomendable tooread [más información acerca de cómo toodeploy de plantillas de](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Obtenga información acerca de cómo usar el archivo de parámetros de hello tooincrementally entornos de actualización y tener acceso a plantillas desde una sola ubicación de almacenamiento.

## <a name="next-steps"></a>Pasos siguientes
Ahora está listo toobegin trabajar con varios componentes de red y máquinas virtuales. Puede usar este toobuild de entorno de ejemplo horizontalmente la aplicación con los componentes principales de hello introducidos aquí.
