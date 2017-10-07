---
title: "aaaAzure inicio rápido: crear VM CLI | Documentos de Microsoft"
description: "Aprender rápidamente máquinas virtuales de toocreate con hello CLI de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a>Crear una máquina virtual Linux con hello CLI de Azure

Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts. Esta guía se detalla con hello Azure CLI toodeploy una máquina virtual con Ubuntu server. Una vez implementado el servidor de hello, se crea una conexión SSH y se instala un servidor Web NGINX.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine

Crear una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando. 

Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* y crea las claves de SSH si aún no existen en una ubicación de la clave predeterminada. toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

Cuando se ha creado la VM de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo. Tome nota de hello `publicIpAddress`. Esta dirección es hello tooaccess usa máquinas virtuales.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Apertura del puerto 80 para el tráfico web 

De forma predeterminada, solo se permiten conexiones mediante SSH con las máquinas virtuales Linux implementadas en Azure. Si esta máquina virtual va toobe un servidor Web, deberá tooopen puerto 80 de hello Internet. Hola de uso [az de vm abrir puerto](/cli/azure/vm#open-port) comando tooopen hello deseado puerto.  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>Conexión SSH con la máquina virtual

Siguiente Hola de uso del comando toocreate una sesión SSH con la máquina virtual de Hola. Asegúrese de que tooreplace  *<publicIpAddress>*  con hello corregir la dirección IP pública de la máquina virtual.  En el ejemplo anterior, la dirección IP era *40.68.254.142*.

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>Instalación de NGINX

Hola a uso continuación bash orígenes de paquetes de secuencia de comandos tooupdate e instala paquete NGINX más reciente de Hola. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a>Página de bienvenida de vista hello NGINX

Con NGINX instalado y el puerto 80 ahora abierta en la máquina virtual de Internet - Hola puede usar un explorador web de su elección tooview hello NGINX página de bienvenida predeterminada. Estar seguro de hello toouse *publicIpAddress* documentó anteriormente página predeterminada de toovisit Hola. 

![Sitio predeterminado de NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando ya no necesite, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, VM y todos ellos relacionados con recursos.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web. toolearn más información acerca de máquinas virtuales de Azure, continuar con tutorial toohello para máquinas virtuales de Linux.


> [!div class="nextstepaction"]
> [Tutoriales de máquinas virtuales Linux de Azure](./tutorial-manage-vm.md)
