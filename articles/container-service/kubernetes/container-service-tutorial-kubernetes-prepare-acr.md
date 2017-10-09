---
title: tutorial de servicio de contenedor de aaaAzure - preparar ACR | Documentos de Microsoft
description: "Tutorial de Azure Container Service tutorial: preparación de ACR"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Implementación y uso de Azure Container Registry

Azure Container Registry (ACR) es un registro privado basado en Azure para imágenes de contenedor de Docker. Este tutorial, la segunda parte de siete, explica paso a paso de implementación de una instancia de registro de contenedor de Azure e insertar un tooit de imagen de contenedor. Los pasos completados incluyen:

> [!div class="checklist"]
> * Implementación de una instancia de Azure Container Registry (ACR)
> * Etiquetado de una imagen de contenedor para ACR
> * Cargando Hola imagen tooACR

En posteriores tutoriales, esta instancia de ACR se integra con un clúster de Kubernetes en Azure Container Service, para la ejecución segura de imágenes de contenedor. 

## <a name="before-you-begin"></a>Antes de empezar

Hola [tutorial anterior](./container-service-tutorial-kubernetes-prepare-app.md), una imagen de contenedor se creó para una aplicación sencilla de votación de Azure. En este tutorial, esta imagen se inserta tooan del registro de contenedor de Azure. Si no ha creado la imagen de aplicación de Azure votos hello, devolver demasiado[Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md). Como alternativa, los pasos de hello aquí detallan trabajar con cualquier imagen de contenedor.

Este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="deploy-azure-container-registry"></a>Implementación de Azure Container Registry

Para implementar Azure Container Registry, necesita tener antes un grupo de recursos. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. En este ejemplo, un grupo de recursos denominado *myResourceGroup* se crea en hello *westeurope* región.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Crear un registro de contenedor de Azure con hello [crear acr az](/cli/azure/acr#create) comando. nombre de Hola de un registro de contenedor **deben ser únicos**.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

A lo largo del resto de Hola de este tutorial, usamos "acrname" como un marcador de posición para el nombre del registro de hello contenedor que eligió.

## <a name="container-registry-login"></a>Inicio de sesión en Container Registry

Debe iniciar sesión en la instancia ACR tooyour antes de insertar imágenes tooit. Hola de uso [inicio de sesión de acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) operación de hello toocomplete de comandos. Necesita tooprovide Hola único nombre dado del registro de contenedor de toohello cuando se creó.

```azurecli
az acr login --name <acrName>
```

comando de Hello devuelve un mensaje de 'Inicio de sesión correcto' cuando se haya completado.

## <a name="tag-container-images"></a>Etiquetado de imágenes de contenedor

Cada imagen de contenedor debe toobe etiquetado con el nombre de hello loginServer del registro de hello. Esta etiqueta se utiliza para el enrutamiento al activar el registro de imágenes de tooan de imágenes de contenedor.

una lista de imágenes actuales, use hello toosee [imágenes de docker](https://docs.docker.com/engine/reference/commandline/images/) comando.

```bash
docker images
```

Salida:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

nombre de loginServer en hello tooget, ejecute el siguiente comando de Hola.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Ahora, Hola de etiqueta *azure front-voto* imagen con hello loginServer de registro de contenedor de Hola. Además, agregue `:redis-v1` toohello final del nombre de la imagen de Hola. Esta etiqueta indica la versión de la imagen de Hola.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

Una vez que estén etiquetadas, ejecute [imágenes de docker] operación de hello tooverify (https://docs.docker.com/engine/reference/commandline/images/).

```bash
docker images
```

Salida:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>Insertar imágenes tooregistry

Insertar hello *azure front-voto* registro toohello de imágenes. 

Con el siguiente ejemplo de Hola, sustituya Hola ACR loginServer con loginServer Hola de su entorno.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

Esto tiene un par de minutos toocomplete.

## <a name="list-images-in-registry"></a>Lista de imágenes en el registro

una lista de imágenes que se han insertado tooyour registro de contenedor de Azure, Hola usuario tooreturn [lista de repositorios de acr az](/cli/azure/acr/repository#list) comando. Actualizar un comando hello con nombre de instancia ACR Hola.

```azurecli
az acr repository list --name <acrName> --output table
```

Salida:

```azurecli
Result
----------------
azure-vote-front
```

Y, a continuación, etiquetas de hello toosee para una imagen específica, use hello [az acr repositorio Mostrar etiquetas](/cli/azure/acr/repository#show-tags) comando.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

Salida:

```azurecli
Result
--------
redis-v1
```

Tutorial se complete, imagen de contenedor de Hola se ha almacenado en una instancia de registro de contenedor de Azure privada. Esta imagen se implementa de clúster ACR tooa Kubernetes en los tutoriales posteriores.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se ha preparado una instancia de Azure Container Registry para su uso en un clúster de ACS Kubernetes. se completaron Hola pasos:

> [!div class="checklist"]
> * Implementación de una instancia de Azure Container Registry
> * Etiquetado de una imagen de contenedor para ACR
> * Hola cargado imagen tooACR

Avanzar toohello toolearn de tutorial siguiente acerca de cómo implementar un clúster de Kubernetes en Azure.

> [!div class="nextstepaction"]
> [Implementación de un clúster de Kubernetes](./container-service-tutorial-kubernetes-deploy-cluster.md)