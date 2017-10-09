---
title: "aaaAzure redes virtuales y máquinas virtuales de Linux | Documentos de Microsoft"
description: "Tutorial: administrar redes virtuales de Azure y máquinas virtuales de Linux con hello CLI de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Administrar redes virtuales de Azure y máquinas virtuales de Linux con hello CLI de Azure

Las máquinas virtuales de Azure utilizan las redes de Azure para la comunicación de red interna y externa. Este tutorial le guía a través de la implementación de dos máquinas virtuales y la configuración de redes de Azure para estas máquinas virtuales. ejemplos de Hello en este tutorial se supone que hello las máquinas virtuales hospedan una aplicación web con una base de datos back-end, sin embargo, no se implementa una aplicación de tutorial de Hola. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Implementar una red virtual
> * Crear una subred dentro de una red virtual
> * Conectar máquinas virtuales tooa subred
> * Administrar direcciones IP públicas de máquinas virtuales
> * Proteger el tráfico entrante de Internet
> * Proteger el tráfico de tooVM VM


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="vm-networking-overview"></a>Introducción a las redes de máquinas virtuales

Redes virtuales de Azure habilitar las conexiones de red segura entre las máquinas virtuales, Hola internet y otros servicios de Azure como base de datos de SQL Azure. Las redes virtuales se dividen en segmentos lógicos llamados subredes. Se utilizan subredes toocontrol flujo de red y como un límite de seguridad. Al implementar una máquina virtual, por lo general incluye una interfaz de red virtual, subred tooa adjunto.

## <a name="deploy-virtual-network"></a>Implementación de una red virtual

Para este tutorial, se crea una única red virtual con dos subredes: una subred de front-end para hospedar una aplicación web y una subred de back-end para hospedar un servidor de bases de datos.

Antes de poder crear una red virtual, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myRGNetwork* en ubicación de eastus Hola.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>Creación de una red virtual

Nos Hola [crear red virtual de red az](/cli/azure/network/vnet#create) comando toocreate una red virtual. En este ejemplo, se denomina red hello *mvVnet* y se le asigna un prefijo de dirección de *10.0.0.0/16*. También se crea una subred con el nombre de *mySubnetFrontEnd* y un prefijo de *10.0.1.0/24*. Más adelante en este tutorial una VM front-end está conectado toothis subred. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>Creación de una subred

Una subred nueva se agrega la red virtual de toohello con hello [crear subredes de red virtual de red az](/cli/azure/network/vnet/subnet#create) comando. En este ejemplo, se denomina subred hello *mySubnetBackEnd* y se le asigna un prefijo de dirección de *10.0.2.0/24*. Esta subred se usa con todos los servicios back-end.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

Entonces, se ha creado una red y se ha segmentado en dos subredes, una para servicios front-end y otra para servicios back-end. En la siguiente sección hello, máquinas virtuales se crean y toothese subredes conectadas.

## <a name="understand-public-ip-address"></a>Información sobre la dirección IP pública

Una dirección IP pública permite pueden tener acceso a recursos de Azure toobe Hola internet. En esta sección del tutorial de hello, una máquina virtual se crea toodemonstrate cómo aborda toowork con la dirección IP pública.

### <a name="allocation-method"></a>Método de asignación

Una dirección IP pública puede asignarse ya sea de forma dinámica o estática. De forma predeterminada, la dirección IP pública se asigna dinámicamente. Las direcciones IP dinámicas se liberan al desasignar una máquina virtual. Este comportamiento provoca toochange de dirección IP de Hola durante cualquier operación que incluya una cancelación de asignación de máquina virtual.

se puede establecer el método de asignación de Hello toostatic, lo que garantiza que la dirección IP de Hola permanecen asignados tooa máquina virtual, incluso durante un estado de asignación ha sido cancelado. Cuando se usa una dirección IP asignada estáticamente, no se puede especificar la dirección IP hello en sí misma. sino que se asigna desde un grupo de direcciones disponibles.

### <a name="dynamic-allocation"></a>Asignación dinámica

Al crear una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando, método de asignación de hello predeterminado público IP dirección es dinámico. En el siguiente ejemplo de Hola, se crea una máquina virtual con una dirección IP dinámica. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>Asignación estática

Al crear una máquina virtual mediante hello [crear vm az](/cli/azure/vm#create) de comando, se incluyen hello `--public-ip-address-allocation static` argumento tooassign una dirección IP pública estática. Esta operación no está demostrada en este tutorial, sin embargo en la sección siguiente de hello una dirección IP asignada dinámicamente es tooa modificado estáticamente dirección asignada. 

### <a name="change-allocation-method"></a>Cambio del método de asignación

se puede cambiar el método de asignación de direcciones IP de Hello mediante hello [actualizar la ip pública de red az](/cli/azure/network/public-ip#update) comando. En este ejemplo, método de asignación de direcciones IP de hello VM front-end se cambia de Hola toostatic.

En primer lugar, desasignar Hola máquina virtual.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

Hola de uso [actualizar la ip pública de red az](/cli/azure/network/public-ip#update) método de asignación de hello tooupdate de comandos. En este caso, Hola `--allocation-method` se establece demasiado*estático*.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Iniciar VM Hola.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>Sin dirección IP pública

A menudo, una máquina virtual no es necesario toobe accesible a través de internet de Hola. una máquina virtual sin una dirección IP pública, use hello toocreate `--public-ip-address ""` argumento con un conjunto vacío de comillas dobles. Esta configuración se muestra más adelante en este tutorial.

## <a name="secure-network-traffic"></a>Protegen el tráfico de red.

Un grupo de seguridad de red (NSG) contiene una lista de reglas de seguridad que permiten o deniegan tooresources de tráfico de red conectados a redes virtuales tooAzure (VNet). Los NSG pueden toosubnets asociado o interfaces de red individuales. Cuando un NSG está asociado a una interfaz de red, se aplica solo Hola asociados máquina virtual. Cuando un NSG está asociado tooa subred, Hola reglas aplican tooall recursos toohello conectado subred. 

### <a name="network-security-group-rules"></a>Reglas del grupo de seguridad de red

Las reglas de NSG definen puertos de redes a través de los que se permite o deniega el tráfico. las reglas de Hello pueden incluir intervalos de direcciones IP de origen y destino para que controle el tráfico entre sistemas específicos o subredes. Las reglas de NSG también incluyen una prioridad (entre 1 y 4096). Las reglas se evalúan en orden de Hola de prioridad. Una regla con una prioridad de 100 se evalúa antes que una regla con prioridad de 200.

Todos los grupos de seguridad de red contienen un conjunto de reglas predeterminadas. no se puede eliminar las reglas predeterminadas de Hello, pero dado que se asignan prioridad más baja de hello, pueden reemplazarse por reglas de Hola que cree.

- **Red virtual:** el tráfico que se origina y termina en una red virtual se permite en las direcciones tanto de entrada como de salida.
- **Internet:** se permite el tráfico saliente pero se bloquea el entrante.
- **El equilibrador de carga** -estado hello tooprobe de equilibrador de carga de Azure permiten de las máquinas virtuales y las instancias de rol. Si no va a usar un conjunto con equilibrio de carga, puede invalidar esta regla.

### <a name="create-network-security-groups"></a>Creación de grupos de seguridad de red

Un grupo de seguridad de red se puede crear en hello mismo tiempo como una máquina virtual mediante hello [crear vm az](/cli/azure/vm#create) comando. Al hacerlo, hello NSG está asociado a la interfaz de red de máquinas virtuales de hello y una regla de NSG tooallow creados de forma automática un tráfico en el puerto *22* de cualquier origen. Anteriormente en este tutorial, hello NSG front-end fue creado automáticamente con Hola VM front-end. También se crea automáticamente una regla de NSG para el puerto 22. 

En algunos casos, puede ser útil toopre-crear un NSG, como cuando no se deben crear reglas predeterminadas de SSH o cuando hello NSG debe ser subred tooa adjunto. 

Hola de uso [crear az red nsg](/cli/azure/network/nsg#create) comando toocreate un grupo de seguridad de red.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

En lugar de asociación de interfaz de red de hello NSG tooa, está asociado a una subred. En esta configuración, todas las máquinas virtuales que está adjunto toohello subred hereda reglas NSG Hola.

Actualizar Hola subred existente denominado *mySubnetBackEnd* con Hola nuevo NSG.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

Ahora cree una máquina virtual, que está adjunto toohello *mySubnetBackEnd*. Tenga en cuenta que hello `--nsg` argumento tiene un valor de comillas dobles vacías. Un NSG no es necesario toobe creado con hello máquina virtual. Hola VM es la subred de back-end toohello adjunto, que está protegido con hello NSG de back-end ha creado previamente. Esta NSG aplica toohello máquina virtual. Además, tenga en cuenta aquí que hello `--public-ip-address` argumento tiene un valor de comillas dobles vacías. Esta configuración crea una máquina virtual sin una dirección IP pública. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>Protección del tráfico entrante

Cuando hello front-end se crea la VM, se creó una regla NSG tooallow el tráfico entrante en el puerto 22. Esta regla permite las conexiones de SSH toohello VM. En este ejemplo, también se debería permitir el tráfico en el puerto *80*. Esta configuración permite que un toobe de aplicación web tiene acceso en hello máquina virtual.

Hola de uso [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) toocreate una regla para el puerto de comando *80*.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

Hello VM front-end ahora solo es accesible en el puerto *22* y el puerto *80*. El resto del tráfico entrante se bloquea en el grupo de seguridad de red de Hola. Puede ser útil toovisualize las configuraciones de reglas de hello NSG. Configuración de reglas NSG Hola devuelto con hello [lista de reglas de red az](/cli/azure/network/nsg/rule#list) comando. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

Salida:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>Proteger el tráfico de tooVM VM

También pueden aplicar reglas del grupo de seguridad de red entre máquinas virtuales. En este ejemplo, hello VM front-end debe toocommunicate con Hola VM back-end en el puerto *22* y *3306*. Esta configuración permite que las conexiones de SSH de Hola VM front-end y también permiten que una aplicación en hello toocommunicate front-end de máquina virtual con una base de datos de MySQL de back-end. Se debe bloquear todo el tráfico entre Hola front-end y back-end las máquinas virtuales.

Hola de uso [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) comando toocreate una regla para el puerto 22. Tenga en cuenta que hello `--source-address-prefix` argumento especifica un valor de *10.0.1.0/24*. Esta configuración garantiza que se permite únicamente el tráfico de subred de front-end de Hola a través de hello NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

Ahora, agregue una regla para el tráfico de MySQL en el puerto 3306.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

Por último, porque los NSG tienen una regla predeterminada que permite todo el tráfico entre máquinas virtuales en hello misma red virtual, puede puede crear una regla para hello back-end NSG tooblock todo el tráfico. Tenga en cuenta aquí que hello `--priority` se le asigna un valor de *300*, que es menor que ambos Hola reglas de NSG y MySQL. Esta configuración garantiza que todavía se permite el tráfico SSH y MySQL a través de hello NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

Hello VM back-end ahora solo es accesible en el puerto *22* y el puerto *3306* de subred de front-end de Hola. El resto del tráfico entrante se bloquea en el grupo de seguridad de red de Hola. Puede ser útil toovisualize las configuraciones de reglas de hello NSG. Configuración de reglas NSG Hola devuelto con hello [lista de reglas de red az](/cli/azure/network/nsg/rule#list) comando. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

Salida:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha creado y protege las redes de Azure como máquinas toovirtual relacionados. Ha aprendido a:

> [!div class="checklist"]
> * Implementar una red virtual
> * Crear una subred dentro de una red virtual
> * Conectar máquinas virtuales tooa subred
> * Administrar direcciones IP públicas de máquinas virtuales
> * Proteger el tráfico entrante de Internet
> * Proteger el tráfico de tooVM VM

Avanzar toohello toolearn de tutorial siguiente sobre la protección de datos en máquinas virtuales mediante copia de seguridad de Azure. 

> [!div class="nextstepaction"]
> [Copia de seguridad de máquinas virtuales Linux en Azure](./tutorial-backup-vms.md)
