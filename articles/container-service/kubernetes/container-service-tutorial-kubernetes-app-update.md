---
title: "tutorial de servicio de contenedor de aaaAzure - la aplicación de actualización | Documentos de Microsoft"
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
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>Actualización de una aplicación en Kubernetes

Después de implementar una aplicación en Kubernetes, se puede actualizar mediante la especificación de una nueva imagen de contenedor o la versión de la imagen. Cuando se actualiza una aplicación, la implementación de actualización de hello preconfigurada para que solo una parte de la implementación de Hola se actualicen al mismo tiempo. Esta actualización por fases permite tookeep de aplicación Hola ejecutando durante la actualización de Hola y proporciona un mecanismo de reversión si se produce un error de implementación. 

En este tutorial, se actualiza la parte seis de siete, aplicación de Azure voto de ejemplo de Hola. Las tareas que debe completar incluyen las siguientes:

> [!div class="checklist"]
> * Actualizar el código de aplicación front-end de Hola
> * Creación de una imagen de contenedor actualizado
> * Insertar tooAzure de imagen de contenedor de hello del registro de contenedor
> * Implementación de imagen de contenedor se actualizaron Hola

En los tutoriales posteriores, Operations Management Suite es clúster de Kubernetes hello toomonitor configurado.

## <a name="before-you-begin"></a>Antes de empezar

En los tutoriales anteriores, una aplicación se empaqueta en una imagen de contenedor, imagen Hola cargó tooAzure del registro de contenedor y un clúster de Kubernetes creado. a continuación, se ejecutó la aplicación de Hello en clúster de Kubernetes Hola. 

Si no se han completado estos pasos y desea toofollow a lo largo, devolver demasiado[Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md). 

## <a name="update-application"></a>Actualización de una aplicación

pasos de hello toocomplete en este tutorial, debe clonar una copia del programa Hola a aplicaciones de Azure voto. Si es necesario, cree esta copia clonada con hello siguiente comando:

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Abra hello `config_file.cfg` archivo con cualquier editor de texto o código. Puede encontrar este archivo en hello siguiendo el directorio del repositorio de hello clonado.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Cambiar los valores de hello de `VOTE1VALUE` y `VOTE2VALUE`y, a continuación, guarde el archivo hello.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Use [crear docker](https://docs.docker.com/compose/) toore-crear imagen de front-end de Hola y aplicación hello ejecución actualizado.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>Prueba local de la aplicación

Examinar demasiado`http://localhost:8080` toosee Hola aplicación actualizada.

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>Etiquetado e inserción de imágenes

Hola etiqueta *azure front-voto* imagen con hello loginServer de registro de contenedor de Hola.

Si usas registro de contenedor de Azure, obtener el nombre del servidor de inicio de sesión de hello con hello [lista de acr az](/cli/azure/acr#list) comando.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Use [etiqueta docker](https://docs.docker.com/engine/reference/commandline/tag/) imagen de hello tootag. Reemplace `<acrLoginServer>` por el nombre del servidor de inicio de sesión de Azure Container Registry o por el nombre de host de registro público.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

Use [inserción de docker](https://docs.docker.com/engine/reference/commandline/push/) registro tooyour de tooupload Hola imágenes. Reemplace `<acrLoginServer>` por el nombre del servidor de inicio de sesión de Azure Container Registry o por el nombre de host de registro público.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>Implementación de una aplicación actualizada

tooensure tiempo de actividad máxima, deben ejecutar varias instancias de pod de aplicación Hola. Compruebe esta configuración con hello [kubectl obtener pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.

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

Si no dispone de varios pod ejecuta hello azure front-voto imagen, escalar hello *azure front-voto* implementación.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

aplicación de hello tooupdate, use hello [kubectl conjunto](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) comando. Actualización `<acrLoginServer>` con el nombre de host o servidor de inicio de sesión de Hola de seguridad del registro de contenedor.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

implementación de hello toomonitor, use hello [kubectl obtener pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando. Tal y como se implementa la aplicación hello actualizado, se terminan y se vuelve a crear con la nueva imagen de contenedor Hola su pod.

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

Obtener dirección IP externa de Hola de hello *azure front-voto* servicio.

```azurecli-interactive
kubectl get service azure-vote-front
```

Examinar toohello IP dirección toosee Hola aplicación actualizada.

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, una aplicación actualizada e implantado este clúster de Kubernetes tooa de actualización. se completaron Hola siguientes tareas:

> [!div class="checklist"]
> * Código de la aplicación front-end de hello actualizada
> * Creó la imagen de contenedor actualizado
> * Insertar tooAzure de imagen de contenedor de hello del registro de contenedor
> * Aplicación hello implementado actualizado

Avanzar toohello toolearn de tutorial siguiente acerca de cómo toomonitor Kubernetes con Operations Management Suite.

> [!div class="nextstepaction"]
> [Supervisión de Kubernetes con OMS](./container-service-tutorial-kubernetes-monitor.md)