---
title: aaaAvailability y la escala en las plantillas de administrador de recursos de Azure | Documentos de Microsoft
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a>Disponibilidad y escala en plantillas de Azure Resource Manager para máquinas virtuales Linux

Disponibilidad y escalabilidad consulte hello y toouptime demanda de toomeet de capacidad. Si una aplicación debe estar 99,9% de tiempo de hello, debe toohave una arquitectura que permite a varios recursos de proceso simultáneas. Por ejemplo, en lugar de tener un único sitio Web, una configuración con un mayor nivel de disponibilidad incluye varias instancias de hello al mismo sitio, con tecnología frente a ellos de equilibrio. En esta configuración, una instancia de la aplicación hello puede desactivarse por razones de mantenimiento, mientras que Hola restantes continúa toofunction. Escala en hello otra parte hace referencia la petición de tooserve de capacidad de las aplicaciones de tooan. Con una carga equilibrada aplicación, agregar o quitar instancias de grupo de hello permite una petición de toomeet tooscale de aplicación.

Este documento describe cómo configurar el Hola implementación de ejemplo de tienda de música de disponibilidad y escalabilidad. Se resaltan todas las dependencias y configuraciones únicas. Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager. plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="availability-set"></a>Conjunto de disponibilidad
Un conjunto de disponibilidad abarca de forma lógica máquinas virtuales de Azure entre hosts físicos y otros componentes de infraestructura tales como fuentes de alimentación y hardware de red físico. Los conjuntos de disponibilidad garantizan que no todas las máquinas virtuales se vean afectadas durante las tareas de mantenimiento, los errores de dispositivo u otros tiempos de inactividad. Un conjunto de disponibilidad se pueden agregar plantilla de Azure Resource Manager tooan usando Visual Studio agregar Asistente para nuevo recurso de Hola o insertar un valor JSON válido en una plantilla.

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [conjunto de disponibilidad](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

Un conjunto de disponibilidad se declara como una propiedad de un recurso de máquina virtual. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [conjunto de disponibilidad de la asociación con la máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
disponibilidad de Hello establecida tal como se muestra de Hola portal de Azure. Cada máquina virtual y los detalles sobre la configuración de Hola se detallan aquí.

![Conjunto de disponibilidad](./media/dotnet-core-4-availability-scale/aset.png)

Para más información detallada sobre los conjuntos de disponibilidad, consulte [Administración de la disponibilidad de las máquinas virtuales](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

## <a name="network-load-balancer"></a>Equilibrador de carga de red
Mientras que un conjunto de disponibilidad proporciona tolerancia a errores, un equilibrador de carga hace muchas instancias de aplicación hello estén disponibles en una única dirección de red. Se pueden hospedar varias instancias de una aplicación en varias máquinas virtuales, cada uno conectado tooa equilibrador de carga. Tal y como se tiene acceso a la aplicación hello, rutas de equilibrador de carga de Hola Hola solicitud entrante a través de los miembros de hello adjuntada. Un equilibrador de carga se pueden agregar utilizando Visual Studio agregar Asistente para nuevo recurso de Hola o insertando correctamente recursos JSON con formato en la plantilla de Azure Resource Manager Hola.

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [equilibrador de carga de red](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

Dado que es de aplicación de ejemplo de Hola toohello expuesto internet con una dirección IP pública, esta dirección está asociada con el equilibrador de carga de Hola. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [asociaciones de equilibrador de carga de red con dirección IP pública](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Desde Hola portal de Azure, hello información general del equilibrador de carga de red muestra asociación Hola con la dirección IP pública Hola.

![Equilibrador de carga de red](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a>Regla de equilibrador de carga
Cuando se utiliza un equilibrador de carga, se configuran reglas que controlan cómo se equilibra el tráfico a través de recursos de hello diseñado. Con la aplicación de tienda de música de ejemplo de Hola, tráfico llega en el puerto 80 de la dirección IP pública hello y se distribuye a través del puerto 80 de todas las máquinas virtuales. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [regla del equilibrador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

Una vista de red de hello cargar regla del equilibrador de desde el portal de Hola.

![Regla de equilibrador de carga de red](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a>Sondeo de equilibrador de carga
equilibrador de carga de Hello también necesita toomonitor cada máquina virtual para que se atienden las solicitudes solo toorunning sistemas. Esta supervisión se realiza mediante un sondeo constante en un puerto definido previamente. implementación de la tienda de música de Hello es máquinas virtuales de tooprobe configurado el puerto 80 en todos los incluye. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [sondeo del equilibrador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

sondeo de equilibrador de carga de Hello ven de hello portal de Azure.

![Sondeo de equilibrador de carga de red](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a>Reglas NAT de entrada
Cuando se utiliza un equilibrador de carga, las reglas deben toobe implanten que proporcionan acceso con equilibrio de carga no tooeach Máquina Virtual. Por ejemplo, al crear una conexión SSH con cada máquina virtual, este tráfico no debe tener equilibrio de carga; en su lugar, se debe configurar una ruta de acceso predeterminada. Las rutas de acceso predeterminadas se configuran mediante un recurso de regla NAT de entrada. Con este recurso, la comunicación entrante puede ser asignado tooindividual máquinas virtuales. 

Con la aplicación de la tienda de música de hello, un puerto a partir de 5000 es asignada tooport 22 en cada máquina Virtual para el acceso SSH. Hola `copyindex()` función es tooincrement usado Hola puerto de entrada, que Hola segunda Máquina Virtual recibe un puerto de entrada de 5001, Hola 5002 tercera y así sucesivamente. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [reglas de NAT de entrada](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270). 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

Ejemplo de una regla NAT de entrada como Hola encontrada en el portal de Azure. Se crea una regla de NAT SSH para cada máquina virtual en la implementación de Hola.

![Regla NAT de entrada](./media/dotnet-core-4-availability-scale/natrule.png)

Para obtener información detallada sobre Hola equilibrador de carga de red de Azure, vea [equilibrio de carga para servicios de infraestructura de Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Implementación de varias máquinas virtuales
Por último, para una función de tooeffectively conjunto de disponibilidad o equilibrio de carga, son necesarias varias máquinas virtuales. Varias máquinas virtuales pueden implementarse mediante la función de copia de plantilla de hello Azure Resource Manager. Mediante la función de copia de hello, no es necesario toodefine un número finito de máquinas virtuales, en su lugar este valor se puede proporcionar dinámicamente en tiempo de Hola de implementación. función de copia de Hello consume número Hola de instancias toocreated e identificadores de implementar el número apropiado de Hola de máquinas virtuales y recursos asociados.

En la plantilla de ejemplo de la tienda de música de hello, se define un parámetro que toma un número de instancia. Este número se utiliza a lo largo de la plantilla de hello al crear máquinas virtuales y recursos relacionados.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

En hello recurso de máquina Virtual, bucles de copia de Hola se da un nombre y Hola número de instancias parámetro usa toocontrol Hola un número de copias resultantes.

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [función de copia de la máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300). 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

iteración actual de Hola de función de copia de hello puede obtenerse con hello `copyIndex()` función. valor de Hola de función de índice de hello copia puede ser usado tooname las máquinas virtuales y otros recursos. Por ejemplo, si se implementan dos instancias de una máquina virtual, necesitan nombres diferentes. Hola `copyIndex()` función puede utilizarse como parte de la máquina virtual de hello nombre toocreate un nombre único. Un ejemplo de Hola `copyindex()` función que se usa para asignar nombres a fines puede verse en hello recurso de máquina Virtual. En este caso, el nombre del equipo de hello es una concatenación de hello `vmName` hello y parámetro `copyIndex()` función. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [función de copia del índice](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319). 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

Hola `copyIndex` función se utiliza varias veces en la plantilla de ejemplo de Hola tienda de música. Recursos y utilización de las funciones `copyIndex` incluyen tooa nada específico de instancia única de la máquina virtual de hello como la interfaz de red, las reglas del equilibrador de carga, y cualquier depende de las funciones. 

Para obtener más información sobre la función de copia de hello, consulte [crear varias instancias de recursos en el Administrador de recursos de Azure](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Paso siguiente
<hr>

[Paso 4: implementación de aplicaciones con plantillas de Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

