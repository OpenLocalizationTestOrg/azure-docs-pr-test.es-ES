---
title: "aaaHow tooload equilibrar máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse hello Azure carga equilibrador toocreate una aplicación de alta disponibilidad y segura entre tres máquinas virtuales de Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>¿Cómo tooload equilibrar máquinas virtuales de Linux en Azure toocreate una aplicación de alta disponibilidad
El equilibrio de carga proporciona un mayor nivel de disponibilidad al distribuir las solicitudes entrantes entre varias máquinas virtuales. En este tutorial, aprenderá acerca de los componentes diferentes Hola Hola Azure del equilibrador de carga que distribución el tráfico y proporcionan una alta disponibilidad. Aprenderá a:

> [!div class="checklist"]
> * Creación de un equilibrador de carga de Azure
> * Creación del sondeo de estado de un equilibrador de carga
> * Crear reglas de tráfico del equilibrador de carga
> * Usar en la nube init toocreate una aplicación básica de Node.js
> * Crear máquinas virtuales y adjuntar tooa equilibrador de carga
> * Ver un equilibrador de carga en acción
> * Agregar y quitar las máquinas virtuales de un equilibrador de carga


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="azure-load-balancer-overview"></a>Información general sobre Azure Load Balancer
Un equilibrador de carga de Azure es un equilibrador de carga de nivel 4 (TCP, UDP) que proporciona una alta disponibilidad mediante la distribución del tráfico entrante entre máquinas virtuales con un estado correcto. Un sondeo de estado de equilibrador de carga supervisa un puerto determinado en cada máquina virtual y sólo distribuye el tráfico tooan VM operativa.

Se define una configuración de IP de front-end que contiene una o varias direcciones IP públicas. Esta configuración de IP de front-end permite que su toobe de aplicaciones y el equilibrador de carga puede tener acceso a través de Internet de Hola. 

Máquinas virtuales se conectarán tooa equilibrador de carga con la tarjeta de interfaz de red virtual (NIC). toodistribute tráfico toohello máquinas virtuales, un grupo de direcciones de back-end contiene direcciones IP de Hola Hola virtual (NIC) toohello conectados del equilibrador de carga.

flujo de hello toocontrol de tráfico, defina reglas de equilibrador de carga para determinados puertos y protocolos que se asignan tooyour las máquinas virtuales.

Si ha seguido tutorial anterior Hola demasiado[crear un conjunto de escalas de máquina virtual](tutorial-create-vmss.md), se creó un equilibrador de carga. Todos estos componentes se configuran automáticamente como parte del conjunto de escalas de Hola.


## <a name="create-azure-load-balancer"></a>Creación del equilibrador de carga de Azure
Esta sección detalla cómo puede crear y configurar cada componente Hola de equilibrador de carga. Antes de poder crear el equilibrador de carga, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupLoadBalancer* en hello *eastus* ubicación:

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>Crear una dirección IP pública
tooaccess Hola de la aplicación en Internet, necesita una dirección IP pública para el equilibrador de carga de Hola. Cree una dirección IP pública con [az network public-ip create](/cli/azure/network/public-ip#create). Hello en el ejemplo siguiente se crea una dirección IP pública denominada *myPublicIP* en hello *myResourceGroupLoadBalancer* grupo de recursos:

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>Crear un equilibrador de carga
Cree un equilibrador de carga con [az network lb create](/cli/azure/network/lb#create). Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre *myLoadBalancer* asigna hello y *myPublicIP* configuración de IP de front-end de dirección toohello:

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>Creación de un sondeo de estado
tooallow Hola equilibrador toomonitor Hola estado de carga de la aplicación, utilice un sondeo de estado. sondeo de estado de Hello dinámicamente agrega o quita las máquinas virtuales de rotación del equilibrador de carga de hello en función de sus comprobaciones de toohealth de respuesta. De forma predeterminada, una máquina virtual se quita de la distribución de equilibrador de carga de hello después de dos errores consecutivos en intervalos de 15 segundos. Cree un sondeo de estado en función de un protocolo o una página de comprobación de mantenimiento específica para la aplicación. 

Hola siguiente ejemplo crea un sondeo TCP. También se pueden crear sondeos HTTP personalizados para comprobaciones de estado más específicas. Al utilizar un sondeo HTTP personalizado, debe crear página de comprobación de mantenimiento de hello, como *healthcheck.js*. sondeo de Hello debe devolver un **HTTP 200 OK** respuesta para host Hola carga equilibrador tookeep Hola de rotación.

toocreate un sondeo de estado TCP, use [crear la prueba de carga equilibrada de red az](/cli/azure/network/lb/probe#create). Hello en el ejemplo siguiente se crea un sondeo de estado denominado *myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>Creación de una regla de equilibrador de carga
Una regla de equilibrador de carga es toodefine usado cómo tráfico es distribuida toohello máquinas virtuales. Definir configuración de IP front-end de hello para el tráfico entrante de Hola y Hola back-end grupo tooreceive Hola tráfico IP, junto con el origen de hello necesarios y el puerto de destino. toomake seguro que solo las máquinas virtuales correcto reciban tráfico, también definir toouse de sondeo de estado de Hola.

Cree una regla de equilibrador de carga con [az network lb rule create](/cli/azure/network/lb/rule#create). Hello en el ejemplo siguiente se crea una regla denominada *myLoadBalancerRule*, usa hello *myHealthProbe* sondeo de estado y equilibra el tráfico en el puerto *80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>Configuración de una red virtual
Antes de implementar algunas máquinas virtuales y puede probar su equilibrador, crear Hola compatibilidad con recursos de red virtual. Para obtener más información sobre las redes virtuales, vea hello [administrar redes virtuales de Azure](tutorial-virtual-network.md) tutorial.

### <a name="create-network-resources"></a>Crear recursos de red
Cree la red virtual con el comando [az network vnet create](/cli/azure/network/vnet#create). Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* con una subred denominada *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

tooadd un grupo de seguridad de red, use [crear az red nsg](/cli/azure/network/nsg#create). Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

Cree una regla de grupo de seguridad de red con el comando [az network nsg rule create](/cli/azure/network/nsg/rule#create). Hello en el ejemplo siguiente se crea una regla de grupo de seguridad de red denominada *myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

Las NIC virtuales se crean con el comando [az network nic create](/cli/azure/network/nic#create). Hello en el ejemplo siguiente se crea tres NIC virtuales. (Una NIC virtual para cada máquina virtual crea para la aplicación Hola siguiendo los pasos). Puede crear NIC virtuales adicionales y las máquinas virtuales en cualquier momento y agregarlos toohello equilibrador de carga:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>Creación de máquinas virtuales

### <a name="create-cloud-init-config"></a>Creación de cloud-init config
En un tutorial anterior en [cómo toocustomize una máquina virtual de Linux en el primer arranque](tutorial-automate-vm-deployment.md), también habrá aprendido cómo tooautomate personalización de máquina virtual con init de la nube. Puede usar Hola mismo tooinstall de archivo de configuración de nube init NGINX y ejecutar una aplicación sencilla de Node.js de "Hello World".

En el shell actual, cree un archivo denominado *init.txt nube* y pegar Hola siguiente configuración. Por ejemplo, crear archivo hello en hello Shell en la nube, no en el equipo local. Escriba `sensible-editor cloud-init.txt` toocreate Hola archivo y ver una lista de editores disponibles. Asegúrese de que ese archivo de nube-init todo Hola se copia correctamente, especialmente Hola primera línea:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a>Creación de máquinas virtuales
alta disponibilidad de Hola de tooimprove de la aplicación, coloque las máquinas virtuales en un conjunto de disponibilidad. Para obtener más información acerca de los conjuntos de disponibilidad, vea Hola anterior [cómo máquinas virtuales de alta disponibilidad toocreate](tutorial-availability-sets.md) tutorial.

Cree el conjunto de disponibilidad con [az vm availability-set create](/cli/azure/vm/availability-set#create). Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad *myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

Ahora puede crear máquinas virtuales de hello con [crear vm az](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea tres máquinas virtuales y genera claves de SSH si aún no existen:

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

Hay tareas en segundo plano que continúan toorun después de hello CLI de Azure devuelve toohello símbolo del sistema. Hola `--no-wait` parámetro no esperar todos Hola toocomplete de tareas. Es posible que otro par de minutos antes de que se puede tener acceso a la aplicación hello. Hello sondeo de estado del equilibrador de carga detecta automáticamente cuando se ejecuta la aplicación hello en cada máquina virtual. Una vez que se ejecuta la aplicación hello, regla de equilibrador de carga de hello inicia toodistribute tráfico.


## <a name="test-load-balancer"></a>Prueba del equilibrador de carga
Obtener dirección IP pública de Hola de un equilibrador de carga con [show de public-ip de red az](/cli/azure/network/public-ip#show). Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIP* creado anteriormente:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

A continuación, puede escribir la dirección IP pública hello en el Explorador de web tooa. Recuerde: tarda unos minutos Estados de Hola de Hola de máquinas virtuales toobe listo antes de equilibrador de carga de hello inicia toodistribute tráfico toothem. se muestra la aplicación Hello, incluyendo hostname Hola de hello VM ese equilibrador de carga de hello distribuye tooas de tráfico en el siguiente ejemplo de Hola:

![Ejecución de la aplicación Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

equilibrador de carga de hello toosee distribuir el tráfico entre todas las tres VM que se ejecuta la aplicación, se puede forzar actualización el explorador web.


## <a name="add-and-remove-vms"></a>Agregar y quitar máquinas virtuales
Puede que necesite tooperform mantenimiento en hello máquinas virtuales que ejecutan la aplicación, como la instalación de actualizaciones del sistema operativo. toodeal con un aumento del tráfico tooyour aplicación, puede que necesite tooadd máquinas virtuales adicionales. Esta sección muestra cómo tooremove o agregar una máquina virtual desde el equilibrador de carga de Hola.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Quitar una máquina virtual de equilibrador de carga de Hola
Puede quitar una máquina virtual del grupo de direcciones de back-end de hello con [az red nic ip-config-grupo de direcciones quitar](/cli/azure/network/nic/ip-config/address-pool#remove). Hola siguiente ejemplo quita Hola NIC virtual para **myVM2** de *myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

equilibrador de carga de hello toosee distribuir el tráfico entre Hola otras dos máquinas virtuales que ejecutan la aplicación puede forzar actualización el explorador web. Ahora puede realizar el mantenimiento en Hola de máquina virtual, como instalar actualizaciones del sistema operativo o realizar un reinicio de máquina virtual.

### <a name="add-a-vm-toohello-load-balancer"></a>Agregar un equilibrador de carga de toohello VM
Después de realizar el mantenimiento de la máquina virtual, o si necesita capacidad de tooexpand, puede agregar un grupo de direcciones de back-end VM toohello con [agregar az red nic ip-config-grupo de direcciones](/cli/azure/network/nic/ip-config/address-pool#add). Hello en el ejemplo siguiente se agrega Hola NIC virtual para **myVM2** demasiado*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha creado un equilibrador de carga y adjunta tooit de máquinas virtuales. Ha aprendido a:

> [!div class="checklist"]
> * Creación de un equilibrador de carga de Azure
> * Creación del sondeo de estado de un equilibrador de carga
> * Crear reglas de tráfico del equilibrador de carga
> * Usar en la nube init toocreate una aplicación básica de Node.js
> * Crear máquinas virtuales y adjuntar tooa equilibrador de carga
> * Ver un equilibrador de carga en acción
> * Agregar y quitar las máquinas virtuales de un equilibrador de carga

Avanzar toohello siguiente tutorial toolearn más información acerca de los componentes de red virtual de Azure.

> [!div class="nextstepaction"]
> [Administración de máquinas y redes virtuales](tutorial-virtual-network.md)
