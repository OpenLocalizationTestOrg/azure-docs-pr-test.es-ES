---
title: registro de contenedor de Docker privada de aaaCreate - CLI de Azure | Documentos de Microsoft
description: Empezar a crear y administrar registros de contenedor de Docker privados con hello 2.0 de CLI de Azure
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>Crear un registro de contenedor administrado mediante Hola CLI de Azure

Azure Container Registry es un servicio de registro de contenedores de Docker administrado usado para almacenar imágenes de contenedor de Docker privadas. Esta guía se detalla la creación de una instancia de registro de contenedor de Azure administrados mediante Hola CLI de Azure.

Azure Container Registry está en versión preliminar y no está disponible en todas las regiones.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westcentralus* ubicación.

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>Creación de un registro de contenedor

Crear una instancia ACR mediante hello [crear acr az](/cli/azure/acr#create) comando.

> [!NOTE]
> Cuando cree un registro, especifique un nombre de dominio de nivel superior único global que contenga solo letras y números.

 nombre del registro de Hello en el ejemplo de Hola *myContainerRegistry1*, sustituir un nombre único de su elección.

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

Cuando se crea el registro de hello, salida de hello es siguiente de toohello similar:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>Inicie sesión en la instancia de tooACR

Antes de insertar y extraer imágenes de contenedor, primero debe iniciar sesión en la instancia ACR toohello. toodo por lo tanto, usar hello [inicio de sesión de acr az](/cli/azure/acr#login) comando.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

comando de Hello devuelve un mensaje de 'Inicio de sesión correcto' cuando se haya completado.

## <a name="use-azure-container-registry"></a>Uso de Azure Container Registry

### <a name="list-container-images"></a>Lista de imágenes de contenedor

Hola de uso `az acr` tooquery imágenes de Hola y etiquetas en un repositorio de los comandos de CLI.

> [!NOTE]
> Actualmente, el registro de contenedor no admite hello `docker search` tooquery de comando para imágenes y etiquetas.

### <a name="list-repositories"></a>Lista de repositorios

Hello en el ejemplo siguiente se enumera los repositorios de hello en un registro, en formato JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Lista de etiquetas

Hello en el ejemplo siguiente se muestra etiquetas de hello en hello **ejemplos/nginx** repositorio, en formato JSON:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha creado una instancia administrada de registro de contenedor de Azure con hello CLI de Azure.

> [!div class="nextstepaction"]
> [Insertar la primera imagen con hello CLI de Docker](container-registry-get-started-docker-cli.md)
