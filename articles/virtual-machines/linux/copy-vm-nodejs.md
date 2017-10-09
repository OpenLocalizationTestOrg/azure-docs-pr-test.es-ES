---
title: aaaCreate una copia de la VM de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una copia de la máquina virtual de Linux de Azure con Hola 1.0 de CLI de Azure en el modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>Crear una copia de una máquina virtual de Linux con Azure con hello Azure CLI 1.0
Este artículo muestra cómo toocreate una copia de la máquina virtual de Azure (VM) en ejecución Linux mediante Hola modelo de implementación del Administrador de recursos. En primer lugar debe copiar sobre el sistema operativo de Hola y el nuevo contenedor de datos discos tooa, a continuación, configurar los recursos de red de Hola y crea nueva máquina virtual de Hola.

También puede [cargar y crear una máquina virtual a partir de una imagen de disco personalizada](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- CLI de Azure 1.0 – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="before-you-begin"></a>Antes de empezar
Asegúrese de que se cumple Hola siguiendo los requisitos previos antes de comenzar los pasos de hello:

* Tienes hello [CLI de Azure](../../cli-install-nodejs.md) descargado e instalado en su equipo. 
* También necesitará cierta información acerca de la máquina virtual Linux de Azure existente:

| Información de la máquina virtual de origen | Donde tooget se |
| --- | --- |
| Nombre de la máquina virtual |`azure vm list` |
| Nombre del grupo de recursos |`azure vm list` |
| Ubicación |`azure vm list` |
| Nombre de la cuenta de almacenamiento |`azure storage account list -g <resourceGroup>` |
| Nombre del contenedor |`azure storage container list -a <sourcestorageaccountname>` |
| Nombre del archivo del VHD de la máquina virtual de origen |`azure storage blob list --container <containerName>` |

* Necesitará toomake algunas opciones sobre la nueva máquina virtual:   <br> -Nombre del contenedor    <br> -Nombre de la máquina virtual    <br> -Tamaño de la máquina virtual    <br> -Nombre de red virtual    <br> -Nombre de subred    <br> -Nombre de IP    <br> -nombre de NIC

## <a name="login-and-set-your-subscription"></a>Inicio de sesión y establecimiento de la suscripción
1. Inicio de sesión toohello CLI.

    ```azurecli
    azure login
    ```
2. Asegúrese de que está en modo de Resource Manager.

    ```azurecli
    azure config mode arm
    ```
3. Establecer la suscripción correcta Hola. Puede usar 'lista de cuentas de azure' toosee todas las suscripciones.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>Detener Hola VM
Detener y cancelar la asignación de una VM de origen Hola. Puede usar 'lista de vm de azure' tooget una lista de todas las máquinas virtuales de hello en su suscripción y sus nombres de grupo de recursos.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>Copiar Hola VHD
Puede copiar Hola VHD de hello origen almacenamiento toohello destino mediante hello `azure storage blob copy start`. En este ejemplo, vamos toocopy Hola VHD toohello misma cuenta de almacenamiento, pero un contenedor diferente.

contenedor de tooanother de disco duro virtual toocopy Hola Hola misma cuenta de almacenamiento, escriba:

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>Configurar una red virtual de hello para la nueva máquina virtual
Configure una red virtual y una NIC para la nueva máquina virtual. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>Crear nueva máquina virtual de Hola
Ahora puede crear una máquina virtual desde el disco virtual cargado [mediante una plantilla de administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) o a través de hello CLI especificando Hola URI tooyour copiados disco escribiendo:

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>Pasos siguientes
toolearn cómo toouse CLI de Azure toomanage la nueva máquina virtual, consulte [comandos de CLI de Azure para hello Azure Resource Manager](../azure-cli-arm-commands.md).

