---
title: "establece de aaaConvert una escala de tooa de máquina virtual de Azure | Documentos de Microsoft"
description: "Cree e implemente una escala de máquinas virtuales de Linux Azure establecido con hello CLI de Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>Convertir un conjunto de escala de tooa de máquina virtual de Azure existente

Este tutorial muestra cómo toouse CLI de Azure 2.0 tooconvert una escala de máquinas virtuales de máquina virtual tooa establece. También aprenderá cómo establece la configuración de hello tooautomate de máquinas virtuales de hello en escala de Hola. Para obtener más información sobre cómo tooinstall CLI de Azure 2.0, consulte [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Para más información acerca de los conjuntos de escala, consulte [Conjuntos de escala de máquinas virtuales](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-hello-vm"></a>Paso 1: desaprovisionar Hola VM

Utilizar SSH tooconnect toohello máquina virtual.

Hola de desaprovisionamiento VM utilizando archivos de toodelete del agente de máquina virtual de Azure de Hola y los datos. Para obtener una descripción detallada de desaprovisionamiento, consulte [Captura una máquina virtual Linux](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>Paso 2: capturar una imagen de máquina virtual de hello

Para obtener una descripción detallada de la captura, consulte [Captura de una máquina virtual Linux](capture-image.md).

Cancela la asignación de Hola VM con [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Generalizar Hola VM con [az vm generalizar](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Crear una imagen desde el recurso de máquina virtual de hello con [crear imagen az](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>Paso 3: crear el conjunto de escalas de Hola

Obtener hello **identificador** de imagen de Hola.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

Cree una máquina virtual a partir de un recurso de imagen con [az vmss create](/cli/azure/vmss#create):

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

Este comando también adjunta un disco de datos de 10gb. Tenga en cuenta que dependiendo de hello VM tamaño elegido (utilizáramos **Standard_DS1_v2**), número de Hola de discos de datos permitido es diferente. Para obtener más información, consulte hello [tamaños de máquina virtual](sizes.md).

Una vez que termine de conjunto de escalado de hello, conectar tooit. Obtener una lista de direcciones IP para las instancias de Hola de SSH con [vmss az-instancia de lista-info conexión](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Ahora puede conectar el disco de datos de la instancia tooinitialize toohello máquina virtual Hola

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>Paso 4: disco de datos de inicialización Hola

Mientras la máquina virtual de toohello conectado, particionar el disco de hello con `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Escribir una partición de toohello de sistema de archivos con hello `mkfs` comando:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Montar el disco nuevo de Hola para que sea accesible en el sistema operativo de hello:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

disco de Hello ahora puede tener acceso a través de hello datadrive punto de montaje, que se puede comprobar con `ls /datadrive/`.

Finalizar la sesión SSH Hola.


## <a name="step-5---configure-firewall"></a>Paso 5: Configuración del firewall

Perforación un "agujero" a través de hello firewall toohello webserver hospedado por conjunto de escalas de Hola. Cuando se creó el conjunto de escalas de hello, también se ha creado un equilibrador de carga y utilizó **SSH** toohello las máquinas virtuales individuales. tooopen un puerto, necesita dos fragmentos de información, que puede obtener mediante la CLI de Azure.

* **Grupo de direcciones IP de front-end**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Grupo de direcciones IP de back-end**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Con los dos nombres, puede abrir el puerto **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Paso 6: Automatización de la configuración

disco de datos de Hello debe toobe configurado en cada instancia de máquina virtual. Se puede automatizar la configuración de Hola de máquina virtual de hello con hello **CustomScript** extensión.

En primer lugar, cree un *.sh* secuencia de comandos que incluye comandos de formato de disco de Hola.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

A continuación, cargar ese Hola de toowhere del archivo de script **CustomScript** extensión puede tener acceso a él. Hay disponible una copia [aquí](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Cree un archivo local denominado **settings.json** y put hello siguiente bloque JSON en ella. Hola `flieUris` propiedad se debe establecer toowhere cargado en el archivo de script.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Implementar esta escala de tooyour comando establecida con hello **CustomScript** extensión, que hacen referencia a hello **settings.json** archivos que acabamos de crear.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

Esta extensión se ejecuta automáticamente en todas las instancias actuales y en todas las instancias creadas después ajustando la escala.

## <a name="step-7---configure-autoscale-rules"></a>Paso 7: Configuración de reglas de escalado automático

Actualmente, no se pueden establecer reglas de escalado automático en la CLI de Azure. Hola de uso [portal de Azure](https://portal.azure.com) tooconfigure Autoescala.

## <a name="step-8---management-tasks"></a>Paso 8: Tareas de administración

A lo largo del ciclo de vida de Hola de conjunto de escalas de hello, puede que necesite toorun una o más tareas de administración. Además, puede que desee toocreate scripts que automaticen diversas tareas de ciclo de vida y Hola CLI de Azure proporciona una manera rápida toodo esas tareas. A continuación, presentamos algunas tareas comunes.

### <a name="get-connection-info"></a>Obtención de información de conexión

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>Establecimiento del número de instancias (escalado manual)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>Eliminación de un grupo de recursos

Al eliminar un grupo de recursos se eliminan también todos los recursos contenidos en el mismo.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más información sobre algunas de las escalas de máquina virtual de hello establecer características presentadas en este tutorial, vea Hola siguiente información:

- [Introducción a los conjuntos de escalado de máquinas virtuales de Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Información general sobre Azure Load Balancer](../../load-balancer/load-balancer-overview.md)
- [Control del flujo de tráfico de red con grupos de seguridad de red](../../virtual-network/virtual-networks-nsg.md)