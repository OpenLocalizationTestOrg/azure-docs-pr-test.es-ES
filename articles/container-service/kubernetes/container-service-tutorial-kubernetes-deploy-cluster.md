---
title: "tutorial de servicio de contenedor de aaaAzure - implementar clústeres | Documentos de Microsoft"
description: "Tutorial de Azure Container Service: Implementación de clúster"
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
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Implementación de un clúster de Kubernetes en Azure Container Service

Kubernetes proporciona una plataforma distribuida para aplicaciones en contenedores. Con Azure Container Service, el aprovisionamiento de un clúster de Kubernetes listo para producción se realiza de forma rápida y sencilla. En este tutorial, la tercera parte de siete, se implementa un clúster de Kubernetes de Azure Container Service. Los pasos completados incluyen:

> [!div class="checklist"]
> * Implementación de un clúster de ACS de Kubernetes
> * Instalación de hello Kubernetes CLI (kubectl)
> * Configuración de kubectl

En los tutoriales posteriores, Hola voto de Azure es de aplicación implementado clúster toohello, escalada, actualiza y Operations Management Suite es clúster de Kubernetes hello toomonitor configurado.

## <a name="before-you-begin"></a>Antes de empezar

En los tutoriales anteriores, una imagen de contenedor se ha creado y cargado tooan instancia de registro de contenedor de Azure. Si aún no ha hecho estos pasos y desearía toofollow a lo largo, devolver demasiado[Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Creación de un clúster de Kubernetes

Hola [tutorial anterior](./container-service-tutorial-kubernetes-prepare-acr.md), un grupo de recursos denominado *myResourceGroup* se creó. Si todavía no lo ha hecho, cree ahora este grupo de recursos.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Crear un clúster de Kubernetes en el servicio de contenedor de Azure con hello [az acs crear](/cli/azure/acs#create) comando. 

Hello en el ejemplo siguiente se crea un clúster denominado *myK8sCluster* con un Linux maestro de nodo y tres nodos de agente de Linux.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

Después de varios minutos, comando hello completa y, en formato json de devuelve información acerca de la implementación de hello ACS.

## <a name="install-hello-kubectl-cli"></a>Instalar hello kubectl CLI

tooconnect toohello Kubernetes de clúster desde el equipo cliente, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), cliente de línea de comandos de Kubernetes Hola. 

Si usa Azure CloudShell, `kubectl` ya está instalado. Si desea que tooinstall forma local, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

Si está ejecutando en Linux o Mac OS, debe toorun con sudo. En Windows, asegúrese de que el shell se ha ejecutado como administrador.

```azurecli-interactive 
az acs kubernetes install-cli 
```

En Windows, es la instalación predeterminada de hello *c:\program files (x86)\kubectl.exe*. Puede que tenga tooadd esta ruta de acceso de archivo toohello Windows. 

## <a name="connect-with-kubectl"></a>Conexión con kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes clúster, ejecute hello [az kubernetes get-credenciales de acs](/cli/azure/acs/kubernetes#get-credentials) comando.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

clúster de tooyour de conexión de hello tooverify, ejecute hello [kubectl obtener nodos](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.

```azurecli-interactive
kubectl get nodes
```

Salida:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

Al finalizar el tutorial, tendrá un clúster de ACS de Kubernetes preparado para cargas de trabajo. En los tutoriales posteriores, una aplicación de contenedor múltiples es clúster toothis implementado, escalar horizontalmente, actualizar y supervisar.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se implementó un clúster de Kubernetes de Azure Container Service. se completaron Hola pasos:

> [!div class="checklist"]
> * Implementación de un clúster de ACS de Kubernetes
> * Hola instalado Kubernetes CLI (kubectl)
> * Configuración de kubectl

Avanzar toohello toolearn de tutorial siguiente sobre cómo ejecutar la aplicación en clúster de Hola.

> [!div class="nextstepaction"]
> [Implementación de una aplicación en Kubernetes](./container-service-tutorial-kubernetes-deploy-application.md)
