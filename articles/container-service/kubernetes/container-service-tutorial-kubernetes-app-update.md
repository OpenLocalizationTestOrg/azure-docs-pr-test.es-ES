---
title: "Tutorial de Azure Container Service: actualización de una aplicación | Microsoft Docs"
description: "Tutorial de Azure Container Service: actualización de una aplicación"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: db580da3e2d70892bc37305394df5be609ebb8a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="update-an-application-in-kubernetes"></a>Actualización de una aplicación en Kubernetes

Después de implementar una aplicación en Kubernetes, se puede actualizar mediante la especificación de una nueva imagen de contenedor o la versión de la imagen. Cuando se actualiza una aplicación, el lanzamiento de la actualización se preconfigura para que solo una parte de la implementación se actualice simultáneamente. Esta actualización preconfigurada permite que la aplicación siga ejecutándose durante la actualización y proporciona un mecanismo de reversión si se produce un error de implementación. 

En este tutorial, la sección seis de siete, se actualiza la aplicación de ejemplo de Azure Vote. Las tareas que debe completar incluyen las siguientes:

> [!div class="checklist"]
> * Actualización del código de aplicación front-end
> * Creación de una imagen de contenedor actualizado
> * Inserción de una imagen de contenedor en Azure Container Registry
> * Implementación de una imagen de contenedor actualizado

En tutoriales posteriores, se configura Operations Management Suite para supervisar el clúster de Kubernetes.

## <a name="before-you-begin"></a>Antes de empezar

En tutoriales anteriores se ha empaquetado una aplicación en una imagen de contenedor, se ha cargado la imagen en Azure Container Registry y se ha creado un clúster de Kubernetes. La aplicación se ejecutó después en el clúster de Kubernetes. 

Si no ha finalizado estos pasos y desea continuar, vuelva al [Tutorial 1: Creación de las imágenes de contenedor](./container-service-tutorial-kubernetes-prepare-app.md). 

## <a name="update-application"></a>Actualización de una aplicación

Para completar los pasos de este tutorial, debe clonar una copia de la aplicación Azure Vote. Si es necesario, cree esta copia clonada con el siguiente comando:

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Abra el archivo `config_file.cfg` con cualquier editor de texto o código. Puede encontrar este archivo en el siguiente directorio del repositorio clonado.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Cambie los valores de `VOTE1VALUE` y `VOTE2VALUE` y, después, guarde el archivo.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Use [docker-compose](https://docs.docker.com/compose/) para volver a crear la imagen de front-end y ejecutar la aplicación actualizada.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>Prueba local de la aplicación

Navegue hasta `http://localhost:8080` para ver la aplicación actualizada.

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>Etiquetado e inserción de imágenes

Etiquete la imagen *azure-vote-front* con el loginServer del registro de contenedor.

Si usa Azure Container Registry, obtenga el nombre del servidor de inicio de sesión con el comando [az acr list](/cli/azure/acr#list).

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Use la [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) para etiquetar la imagen. Reemplace `<acrLoginServer>` por el nombre del servidor de inicio de sesión de Azure Container Registry o por el nombre de host de registro público.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) para cargar la imagen en el registro. Reemplace `<acrLoginServer>` por el nombre del servidor de inicio de sesión de Azure Container Registry o por el nombre de host de registro público.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>Implementación de una aplicación actualizada

Para garantizar el tiempo máximo de actividad, se deben ejecutar varias instancias de pod de la aplicación. Compruebe esta configuración con el comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).

```bash
kubectl get pod
```

Salida:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

Si no tiene varios pods ejecutando la imagen de azure-vote-front, escale la implementación de *azure-vote-front*.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

Use el comando [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) para actualizar la aplicación. Actualice `<acrLoginServer>` con el nombre de host o servidor de inicio de sesión del registro de contenedor.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

Para supervisar la implementación, use el comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get). A medida que se implementa la aplicación actualizada, sus pods se terminan y se vuelven a crear con la nueva imagen de contenedor.

```azurecli-interactive
kubectl get pod
```

Salida:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>Prueba de la aplicación actualizada

Obtenga la dirección IP externa del servicio *azure -vote-front*.

```azurecli-interactive
kubectl get service azure-vote-front
```

Navegue hasta la dirección IP para ver la aplicación actualizada.

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, actualiza una aplicación y se implanta esta actualización en un clúster de Kubernetes. Se completaron las siguientes tareas:

> [!div class="checklist"]
> * Actualizó el código de aplicación de front-end
> * Creó la imagen de contenedor actualizado
> * Insertó una imagen de contenedor en Azure Container Registry
> * Implemento la aplicación actualizada

Avance al siguiente tutorial para obtener información sobre cómo supervisar Kubernetes con Operations Management Suite.

> [!div class="nextstepaction"]
> [Supervisión de Kubernetes con OMS](./container-service-tutorial-kubernetes-monitor.md)