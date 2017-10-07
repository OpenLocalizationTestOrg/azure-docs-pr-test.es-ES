---
title: "tutorial de servicio de contenedor de aaaAzure - aplicación de escala | Documentos de Microsoft"
description: "Tutorial de Azure Container Service: escalado de una aplicación"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>Escalado de pods de Kubernetes e infraestructura de Kubernetes

Si ha seguido los tutoriales de hello, tienes un clúster de Kubernetes en funcionamiento en el servicio de contenedor de Azure y ha implementado la aplicación de Azure votos hello. 

En este tutorial, parte cinco de siete, escalar horizontalmente pod hello en la aplicación hello y pruebe pod Autoescala. También aprenderá cómo número de hello tooscale de toochange de nodos de agente de máquina virtual de Azure Hola capacidad del clúster para hospedar las cargas de trabajo. Las tareas completadas incluyen:

> [!div class="checklist"]
> * Escalado manual de pods de Kubernetes
> * Configurar pod de escalado automático que se ejecuta el front-end de la aplicación de Hola
> * Escalar los nodos de agente de Azure de hello Kubernetes

En los tutoriales posteriores, se actualiza Hola aplicación voto de Azure y Operations Management Suite configurado el clúster de toomonitor hello Kubernetes.

## <a name="before-you-begin"></a>Antes de empezar

En los tutoriales anteriores, una aplicación se empaqueta en una imagen de contenedor, esta imagen cargó tooAzure del registro de contenedor y un clúster de Kubernetes creado. a continuación, se ejecutó la aplicación de Hello en clúster de Kubernetes Hola. Si aún no ha hecho estos pasos y desearía toofollow a lo largo, devolver toohello [Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md). 

Como mínimo, este tutorial requiere un clúster de Kubernetes con una aplicación en ejecución.

## <a name="manually-scale-pods"></a>Escalado manual de pods

Hasta ahora, hello Azure voto front-end y la instancia de Redis se han implementado, cada uno con una única réplica. tooverify, ejecute hello [kubectl obtener](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.

```azurecli-interactive
kubectl get pods
```

Salida:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

Cambiar manualmente el número de Hola de pod Hola `azure-vote-front` implementación mediante hello [kubectl escala](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) comando. Este ejemplo aumenta Hola número too5.

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

Ejecutar [kubectl obtener pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify que Kubernetes crea pod Hola. Tras un minuto aproximadamente, ejecutan pod de hello adicionales:

```azurecli-interactive
kubectl get pods
```

Salida:

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>Escalado automático de pods

Admite Kubernetes [pod horizontal Autoescala](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) número de hello tooadjust de pod en una implementación de la función de uso de CPU u otros selecciona métricas. 

toouse hello autoscaler, debe tener su pod solicitudes de CPU y los límites definidos. Hola `azure-vote-front` implementación, Hola CPU de las solicitudes 0,25 contenedor front-end, con un límite de 0,5 CPU. configuración de Hello tiene el siguiente aspecto:

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

Hello en el ejemplo siguiente se usa hello [escalado automático de kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) comando tooautoscale número de Hola de pod Hola `azure-vote-front` implementación. En este caso, si el uso de CPU supera el 50%, hello autoscaler aumenta Hola pod tooa como máximo de 10.


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

estado de hello toosee de hello autoscaler, ejecute el siguiente comando de hello:

```azurecli-interactive
kubectl get hpa
```

Salida:

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

Después de unos minutos, con una carga mínima en la aplicación de Azure voto hello, número de Hola de réplicas de pod disminuye automáticamente too3.

## <a name="scale-hello-agents"></a>Agentes de Hola de escala

Si ha creado su clúster de Kubernetes mediante comandos de manera predeterminada en el tutorial anterior hello, tiene tres nodos de agente. Puede ajustar manualmente número Hola de agentes si tiene previsto más o menos cargas de trabajo de contenedor en el clúster. Hola de uso [az acs escalar](/cli/azure/acs#scale) comando y especifique el número de Hola de agentes con hello `--new-agent-count` parámetro.

Hello en el ejemplo siguiente se aumenta número Hola de too4 de nodos de agente en clúster de hello Kubernetes denominado *myK8sCluster*. comando de Hello toma un par de minutos toocomplete.

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

Hello salida del comando muestra hello número del agente de nodos de valor de Hola de `agentPoolProfiles:count`:

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se han usado distintas características de escalado en el clúster de Kubernetes. Las tareas tratadas incluyen:

> [!div class="checklist"]
> * Escalado manual de pods de Kubernetes
> * Configurar pod de escalado automático que se ejecuta el front-end de la aplicación de Hola
> * Escalar los nodos de agente de Azure de hello Kubernetes

Avanzar toohello toolearn de tutorial siguiente acerca de cómo actualizar la aplicación en Kubernetes.

> [!div class="nextstepaction"]
> [Actualización de una aplicación en Kubernetes](./container-service-tutorial-kubernetes-app-update.md)

