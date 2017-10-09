---
title: "aaaCreate conjuntos de escalas de máquina Virtual para Linux en Azure | Documentos de Microsoft"
description: "Cree e implemente una aplicación de alta disponibilidad en máquinas virtuales Linux con un conjunto de escalado de máquinas virtuales."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Creación de un conjunto de escalado de máquinas virtuales e implementación de una aplicación de alta disponibilidad en Linux
Un conjunto de escalas de máquina virtual permite toodeploy y administrar un conjunto de máquinas virtuales idénticos, la escala automática. Puede escalar el número de Hola de máquinas virtuales en el conjunto de escalas de hello manualmente, o definir tooautoscale reglas en función de uso de CPU, la demanda de memoria o el tráfico de red. En este tutorial, implementará un conjunto de escalado de máquinas virtuales en Azure. Aprenderá a:

> [!div class="checklist"]
> * Usar en la nube init toocreate una tooscale de aplicación
> * Crear un conjunto de escalado de máquinas virtuales
> * Aumentar o disminuir el número de Hola de instancias de un conjunto de escala
> * Ver la información de conexión de las instancias del conjunto de escalado
> * Usar discos de datos con conjuntos de escalado


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Introducción al conjunto de escalado
Un conjunto de escalas de máquina virtual permite toodeploy y administrar un conjunto de máquinas virtuales idénticos, la escala automática. Escala establece uso Hola mismos componentes tal y como ha aprendido en el tutorial anterior Hola demasiado[crear máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md). Las máquinas virtuales de un conjunto de escalado se crean en un conjunto de disponibilidad y se distribuyen entre los dominios de error lógico y de actualización.

Las máquinas virtuales se crean según sea necesario en un conjunto de escalado. Definir toocontrol de reglas de escalado automático cómo y cuándo se agregan o se quitan del conjunto de escalas de hello las máquinas virtuales. Estas reglas se pueden desencadenar en función de métricas como la carga de la CPU, el uso de la memoria o el tráfico de red.

Escala establece compatibilidad con seguridad too1, 000 máquinas virtuales cuando se usa una imagen de la plataforma Windows Azure. Para las cargas de trabajo de producción, es recomendable demasiado[crear una imagen de máquina virtual personalizada](tutorial-custom-images.md). Puede crear las máquinas virtuales de too100 en una escala establecida cuando se usa una imagen personalizada.


## <a name="create-an-app-tooscale"></a>Crear una aplicación tooscale
Para su uso en producción, es recomendable demasiado[crear una imagen de máquina virtual personalizada](tutorial-custom-images.md) que incluye la aplicación instalada y configurada. Para este tutorial, permite personalizar Hola que máquinas virtuales de primera tooquickly arranque ver una escala establecido en acción.

En un tutorial anterior, ha aprendido [cómo toocustomize una máquina virtual de Linux en el primer arranque](tutorial-automate-vm-deployment.md) con init de la nube. Puede usar Hola mismo tooinstall de archivo de configuración de nube init NGINX y ejecutar una aplicación sencilla de Node.js de "Hello World". 

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


## <a name="create-a-scale-set"></a>Creación de un conjunto de escalado
Antes de poder crear un conjunto de escalado, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupScaleSet* en hello *eastus* ubicación:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Ahora, cree un conjunto de escalado de máquinas virtuales con [az vmss create](/cli/azure/vmss#create). Hello en el ejemplo siguiente se crea un conjunto con nombre de escalas *myScaleSet*, utiliza Hola de toocustomize de archivo VM de hello init de la nube y genera claves SSH si no existen:

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

Toma toocreate unos minutos y configurará todos los recursos de conjunto de escala de Hola y máquinas virtuales. Hay tareas en segundo plano que continúan toorun después de hello CLI de Azure devuelve toohello símbolo del sistema. Es posible que otro par de minutos antes de que se puede tener acceso a la aplicación hello.


## <a name="allow-web-traffic"></a>Permitir tráfico web
Un equilibrador de carga se creó automáticamente como parte del conjunto de escalas de máquina virtual de Hola. equilibrador de carga de Hello distribuye el tráfico a través de un conjunto de máquinas virtuales definidas mediante reglas de equilibrador de carga. Puede aprender más sobre conceptos de equilibrador de carga y la configuración en el siguiente tutorial Hola, [cómo tooload equilibrar las máquinas virtuales en Azure](tutorial-load-balancer.md).

tooallow tráfico tooreach hello web app, cree una regla con [crear regla de carga equilibrada de red az](/cli/azure/network/lb/rule#create). Hello en el ejemplo siguiente se crea una regla denominada *myLoadBalancerRuleWeb*:

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a>Prueba de la aplicación
toosee la aplicación Node.js en web de hello, obtener la dirección IP pública de Hola de un equilibrador de carga con [show de public-ip de red az](/cli/azure/network/public-ip#show). Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myScaleSetLBPublicIP* creado como parte del conjunto de escalas de hello:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Escriba la dirección IP pública hello en el Explorador de web tooa. se muestra la aplicación Hello, incluido Hola nombre de host de hello VM ese Hola la carga del tráfico de equilibrador distribuida para:

![Ejecución de la aplicación Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

escala de hello toosee establecida en acción, se puede forzar actualización su carga de hello web explorador toosee equilibrador de distribuir el tráfico entre todas las máquinas virtuales de hello ejecutando la aplicación.


## <a name="management-tasks"></a>Tareas de administración
A lo largo del ciclo de vida de Hola de conjunto de escalas de hello, puede que necesite toorun una o más tareas de administración. Además, puede que desee toocreate scripts que automaticen diversas tareas de ciclo de vida. Hola 2.0 de CLI de Azure proporciona una forma rápida toodo esas tareas. A continuación, presentamos algunas tareas comunes.

### <a name="view-vms-in-a-scale-set"></a>Visualización de máquinas virtuales en un conjunto de escalado
tooview una lista de máquinas virtuales en ejecución en la escala de conjunto, utilice [instancias de lista az vmss](/cli/azure/vmss#list-instances) como se indica a continuación:

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

Hola de salida es similar toohello siguiente ejemplo:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Aumento o disminución de instancias de máquina virtual
número de hello toosee de instancias actualmente en una escala estableciste, use [presentación con az vmss](/cli/azure/vmss#show) y realizar consultas sobre *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

Puede, a continuación, manualmente aumentar o reducir el número de Hola de máquinas virtuales en la escala de hello establecida con [escala de vmss az](/cli/azure/vmss#scale). Hello en el ejemplo siguiente se establece Hola número de máquinas virtuales de la escala establecida demasiado*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Las reglas de escalado automático le permiten definir cómo tooscale hacia arriba o hacia abajo el número de Hola de máquinas virtuales en la escala se establece en toodemand de respuesta como el tráfico de red o el uso de CPU. Actualmente, no se pueden establecer estas reglas en la CLI de Azure 2.0. Hola de uso [portal de Azure](https://portal.azure.com) tooconfigure Autoescala.

### <a name="get-connection-info"></a>Obtención de información de conexión
información de conexión de tooobtain aproximadamente Hola a las máquinas virtuales en los conjuntos de escala, use [vmss az-instancia de lista-info conexión](/cli/azure/vmss#list-instance-connection-info). Este comando da como resultado la dirección IP pública Hola y el puerto para cada máquina virtual que permite tooconnect mediante SSH:

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Uso de discos de datos con conjuntos de escalado
Puede crear y usar discos de datos con conjuntos de escalado. En un tutorial anterior, ha aprendido cómo demasiado[discos Azure administrar](tutorial-manage-disks.md) que contornos Hola prácticas recomendadas y mejoras de rendimiento para la creación de aplicaciones en los discos de datos en lugar de en disco de SO Hola.

### <a name="create-scale-set-with-data-disks"></a>Creación de conjunto de escalado con discos de datos
toocreate una escala establecido y conectar discos de datos, agregar hello `--data-disk-sizes-gb` parámetro toohello [crear az vmss](/cli/azure/vmss#create) comando. Hello en el ejemplo siguiente se crea una escala establecida con *50*Gb discos de datos adjunta la instancia de tooeach:

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

Cuando se quitan las instancias de un conjunto de escalado, también se quitan los discos de datos conectados.

### <a name="add-data-disks"></a>Adición de discos de datos
establecer un tooinstances de disco de datos en la escala de tooadd, use [adjuntar disco de az vmss](/cli/azure/vmss/disk#attach). Hello ejemplo siguiente se agrega un *50*instancia de tooeach de disco Gb:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Desacoplamiento de discos de datos
establecer un tooinstances de disco de datos en la escala de tooremove, use [desasociar el disco de vmss az](/cli/azure/vmss/disk#detach). Hello en el ejemplo siguiente se quita disco de datos de hello en el LUN *2* de cada instancia de:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha creado un conjunto de escalado de máquinas virtuales. Ha aprendido a:

> [!div class="checklist"]
> * Usar en la nube init toocreate una tooscale de aplicación
> * Crear un conjunto de escalado de máquinas virtuales
> * Aumentar o disminuir el número de Hola de instancias de un conjunto de escala
> * Ver la información de conexión de las instancias del conjunto de escalado
> * Usar discos de datos con conjuntos de escalado

Avanzar toohello siguiente tutorial toolearn más información sobre los conceptos de máquinas virtuales de equilibrio de carga.

> [!div class="nextstepaction"]
> [Load balance virtual machines](tutorial-load-balancer.md) (Equilibrio de carga de máquinas virtuales)