---
title: 'tutorial de instancias de contenedor aaaAzure: preparar el registro de contenedor de Azure | Documentos de Microsoft'
description: "Tutorial de Azure Container Instances: preparación de Azure Container Registry"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Implementación y uso de Azure Container Registry

Esta es la segunda parte de un tutorial de tres partes. Hola [paso anterior](./container-instances-tutorial-prepare-app.md), una imagen de contenedor se creó para una aplicación web simple escrita en [Node.js](http://nodejs.org). En este tutorial, esta imagen se inserta tooan del registro de contenedor de Azure. Si no ha creado la imagen de contenedor de hello, devolver demasiado[Tutorial 1: crear la imagen de contenedor](./container-instances-tutorial-prepare-app.md). 

Hola del registro de contenedor de Azure es un registro basado en Azure, privado, para las imágenes de contenedor de Docker. Este tutorial le guía a través de la implementación de una instancia de registro de contenedor de Azure e insertar un tooit de imagen de contenedor. Los pasos completados incluyen:

> [!div class="checklist"]
> * Implementación de una instancia de Azure Container Registry
> * Etiquetado de una imagen de contenedor para Azure Container Registry
> * Cargar imagen tooAzure del registro de contenedor

En los tutoriales posteriores, implemente el contenedor de Hola desde su tooAzure registro privada instancias de contenedor.

## <a name="before-you-begin"></a>Antes de empezar

Este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="deploy-azure-container-registry"></a>Implementación de Azure Container Registry

Para implementar Azure Container Registry, necesita tener antes un grupo de recursos. Un grupo de recursos de Azure es una colección lógica en la que se implementan y se administran los recursos de Azure.

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. En este ejemplo, un grupo de recursos denominado *myResourceGroup* se crea en hello *eastus* región.

```azurecli
az group create --name myResourceGroup --location eastus
```

Crear un registro de contenedor de Azure con hello [crear acr az](/cli/azure/acr#create) comando. nombre de Hola de un registro de contenedor **deben ser únicos**. En el siguiente ejemplo de Hola, usamos nombre hello *mycontainerregistry082*.

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

A lo largo del resto de Hola de este tutorial, usamos `<acrname>` como un marcador de posición para el nombre del registro de hello contenedor que eligió.

## <a name="container-registry-login"></a>Inicio de sesión en Container Registry

Debe iniciar sesión en la instancia ACR tooyour antes de insertar imágenes tooit. Hola de uso [inicio de sesión de acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) operación de hello toocomplete de comandos. Necesita tooprovide Hola único nombre dado del registro de contenedor de toohello cuando se creó.

```azurecli
az acr login --name <acrName>
```

comando de Hello devuelve un mensaje de 'Inicio de sesión correcto' cuando se haya completado.

## <a name="tag-container-image"></a>Etiquetado de la imagen de contenedor

toodeploy una imagen de contenedor de un registro privada, imagen Hola necesita toobe etiquetado con hello `loginServer` nombre del registro de hello.

una lista de imágenes actuales, use hello toosee `docker images` comando.

```bash
docker images
```

Salida:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

nombre de loginServer en hello tooget, ejecute el siguiente comando de Hola.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Hola etiqueta *aplicación de tutorial de aci* imagen con hello loginServer de registro de contenedor de Hola. Además, agregue `:v1` toohello final del nombre de la imagen de Hola. Esta etiqueta indica el número de versión de imagen de Hola.

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

Una vez que estén etiquetadas, ejecutar `docker images` operación de hello tooverify.

```bash
docker images
```

Salida:

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>Insertar imagen tooAzure del registro de contenedor

Insertar hello *aplicación de tutorial de aci* registro toohello de imágenes.

Con el siguiente ejemplo de Hola, sustituya Hola contenedor del registro loginServer con loginServer Hola de su entorno.

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>Lista de imágenes en Azure Container Registry

una lista de imágenes que se han insertado tooyour registro de contenedor de Azure, Hola usuario tooreturn [lista de repositorios de acr az](/cli/azure/acr/repository#list) comando. Actualizar un comando hello con el nombre de registro del contenedor de Hola.

```azurecli
az acr repository list --name <acrName> --output table
```

Salida:

```azurecli
Result
----------------
aci-tutorial-app
```

Y, a continuación, etiquetas de hello toosee para una imagen específica, use hello [az acr repositorio Mostrar etiquetas](/cli/azure/acr/repository#show-tags) comando.

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

Salida:

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, un registro de contenedor de Azure se ha preparado para su uso con instancias de contenedor de Azure y se inserta la imagen de contenedor de Hola. se completaron Hola pasos:

> [!div class="checklist"]
> * Implementación de una instancia de Azure Container Registry
> * Etiquetado de una imagen de contenedor para Azure Container Registry
> * Cargar imagen tooAzure del registro de contenedor

Avanzar toohello toolearn de tutorial siguiente acerca de la implementación Hola contenedor tooAzure mediante instancias de contenedor de Azure.

> [!div class="nextstepaction"]
> [Implementar contenedores tooAzure instancias de contenedor](./container-instances-tutorial-deploy-app.md)
