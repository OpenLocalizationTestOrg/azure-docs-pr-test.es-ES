---
title: 'tutorial de servicio de contenedor aaaAzure: implementar aplicaciones | Documentos de Microsoft'
description: "Tutorial de Azure Container Service: implementación de una aplicación"
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
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a>Ejecución de aplicaciones en Kubernetes

En este tutorial, la cuarta parte de siete, se implementa una aplicación de ejemplo en un clúster de Kubernetes. Los pasos completados incluyen:

> [!div class="checklist"]
> * Descargar archivos de manifiesto de Kubernetes
> * Ejecución de una aplicación en Kubernetes
> * Probar la aplicación hello

En los tutoriales posteriores, esta aplicación es escalar horizontalmente, actualizado, y Operations Management Suite configurado el clúster de toomonitor hello Kubernetes.

Este tutorial supone un conocimiento básico de conceptos de Kubernetes, para obtener información detallada en Kubernetes vea hello [Kubernetes documentación](https://kubernetes.io/docs/home/).

## <a name="before-you-begin"></a>Antes de empezar

En tutoriales anteriores, una aplicación se empaqueta en una imagen de contenedor, esta imagen es tooAzure cargado del registro de contenedor y se ha creado un clúster de Kubernetes. Si aún no ha hecho estos pasos y desearía toofollow a lo largo, devolver demasiado[Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md). 

Como mínimo, este tutorial requiere un clúster de Kubernetes.

## <a name="get-manifest-file"></a>Obtención del archivo de manifiesto

En este tutorial, los [objetos de Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) se implementan mediante un manifiesto de Kubernetes. Un manifiesto de Kubernetes es un archivo con formato de YAML o JSON que contiene instrucciones de implementación y configuración del objeto de Kubernetes.

archivo de manifiesto de aplicación Hola para este tutorial está disponible en el repositorio de aplicación de Azure voto hello, que se clonó en un tutorial anterior. Si no lo ha hecho ya, clonar el repositorio de hello con hello siguiente comando: 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

archivo de manifiesto de Hola se encuentra en hello siguiendo el directorio del repositorio de hello clonado.

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>Actualización del archivo de manifiesto

Si utiliza imágenes del contenedor del registro de contenedor de Azure toostore hello, Hola toobe necesidades manifiesto actualizado con el nombre de hello ACR loginServer.

Obtener el nombre del servidor de inicio de sesión de hello ACR con hello [lista de acr az](/cli/azure/acr#list) comando.

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Hello manifiesto de ejemplo se ha creado previamente con el nombre de repositorio de *microsoft*. Abra el archivo hello con cualquier editor de texto y reemplace hello *microsoft* valor con nombre del servidor de inicio de sesión de saludo de la instancia ACR.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>Implementación de la aplicación

Hola de uso [kubectl crear](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) aplicación hello de toorun de comandos. Este comando analiza hello archivo de manifiesto y crear objetos de Kubernetes de hello definido.

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

Salida:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>Prueba de la aplicación

A [Kubernetes servicio](https://kubernetes.io/docs/concepts/services-networking/service/) se crea que expone Hola aplicación toohello internet. Este proceso puede tardar unos minutos. 

curso toomonitor, use hello [kubectl obtener servicio](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) comando con hello `--watch` argumento.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Inicialmente, Hola **IP externas** para hello *azure front-voto* servicio aparece como *pendiente*. Una vez que la dirección de hello externo IP ha cambiado desde *pendiente* tooan *dirección IP*, use `CTRL-C` proceso de inspección de toostop hello kubectl.

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

aplicación de hello toosee, dirección IP externa de examinar toohello.

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, Hola aplicación de Azure voto era implementado tooan Kubernetes de servicio de contenedor de Azure clúster. Las tareas completadas incluyen:  

> [!div class="checklist"]
> * Descargar archivos de manifiesto de Kubernetes
> * Ejecutar la aplicación hello en Kubernetes
> * Aplicación hello probados

Avanzar toohello toolearn de tutorial siguiente acerca de cómo escalar una aplicación de Kubernetes y el Hola Kubernetes infraestructura subyacente. 

> [!div class="nextstepaction"]
> [Escalar infraestructura y aplicación de Kubernetes](./container-service-tutorial-kubernetes-scale.md)