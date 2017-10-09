---
title: aaaCreate una VM de Linux con una plantilla de Azure 1.0 de CLI de Azure | Documentos de Microsoft
description: Crear una VM de Linux en Azure con hello 1.0 de CLI de Azure y una plantilla de Azure Resource Manager.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>¿Cómo toocreate una VM de Linux con hello Azure CLI 1.0 una plantilla de Azure Resource Manager
Este artículo muestra cómo tooquickly implementar una máquina Virtual de Linux con hello 1.0 de CLI de Azure y una plantilla de Azure Resource Manager. Hola artículo requiere:

* una cuenta de Azure ([obtenga aquí una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/));
* Hola [Azure CLI 1.0](../../cli-install-nodejs.md) inició sesión `azure login`.
* Hola CLI de Azure *debe estar en* modo Azure Resource Manager `azure config mode arm`.

Puede implementar rápidamente una plantilla de VM de Linux mediante el uso de hello [portal de Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#quick-command-summary) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](create-ssh-secured-vm-from-template.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="quick-command-summary"></a>Resumen rápido de comandos
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>Tutorial detallado
Las plantillas permiten toocreate las máquinas virtuales en Azure con la configuración que desee toocustomize durante el inicio de hello, opciones, como nombres de usuario y los nombres de host. En este artículo, hemos iniciado una plantilla de Azure mediante una máquina virtual de Ubuntu junto con un grupo de seguridad de red (NSG) con el puerto 22 abierto para SSH.

Las plantillas de Azure Resource Manager son archivos JSON que se pueden usar para tareas sencillas y excepcionales, como iniciar una máquina virtual de Ubuntu, como lo hizo en este artículo.  Plantillas de Azure también pueden ser configuraciones complejas de Azure usa tooconstruct de entornos completas como una pila de implementación de prueba, desarrollo o de producción.

## <a name="create-hello-linux-vm"></a>Crear hello VM de Linux
Hola siguiendo el ejemplo de código muestra cómo toocall `azure group create` toocreate un recurso de grupo e implementar una VM de Linux protegidas mediante SSH en hello mismo tiempo, use [esta plantilla de Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). Recuerde que en el ejemplo, es preciso nombres toouse tooyour único entorno. Este ejemplo se utiliza *myResourceGroup* como nombre de grupo de recursos de hello, y *myVM* como nombre de la máquina virtual de Hola.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

salida de Hello debería ser similar Hola siguiente bloque de salida:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

En el ejemplo que se implementa una máquina virtual mediante hello `--template-uri` parámetro.  También puede descargar o crear una plantilla de forma local y pasar la plantilla de hello con hello `--template-file` parámetro con un archivo de plantilla de ruta de acceso toohello como un argumento. Hola CLI de Azure le pide parámetros de hello requeridos por plantilla de Hola.

## <a name="next-steps"></a>Pasos siguientes
Hola de búsqueda [Galería de plantillas](https://azure.microsoft.com/documentation/templates/) toodiscover qué toodeploy de marcos de aplicación siguiente.

