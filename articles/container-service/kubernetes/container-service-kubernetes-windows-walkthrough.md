---
title: "aaaQuickstart - clúster Kubernetes de Azure para Windows | Documentos de Microsoft"
description: "Aprender rápidamente toocreate un clúster Kubernetes para contenedores de Windows en el servicio de contenedor de Azure con hello CLI de Azure."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Implementación de un clúster de Kubernetes para los contenedores de Windows

Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts. Esta guía se detalla con hello Azure CLI toodeploy una [Kubernetes](https://kubernetes.io/docs/home/) de clúster en [servicio de contenedor de Azure](../container-service-intro.md). Una vez que se implementa el clúster de hello, conectar tooit con hello Kubernetes `kubectl` herramienta de línea de comandos y, implementar el primer contenedor de Windows.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

> [!NOTE]
> La compatibilidad para contenedores de Windows en Kubernetes en Azure Container Service está en versión preliminar. 
>

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un grupo lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Creación de un clúster de Kubernetes
Crear un clúster de Kubernetes en el servicio de contenedor de Azure con hello [az acs crear](/cli/azure/acs#create) comando. 

Hello en el ejemplo siguiente se crea un clúster denominado *myK8sCluster* con un Linux maestro de nodo y dos nodos de agente de Windows. Este ejemplo crea SSH maestros de claves necesario tooconnect toohello Linux. Este ejemplo se utiliza *azureuser* para un nombre de usuario administrativo y *myPassword12* como contraseña de hello en nodos de Windows hello. Actualice estos entorno de valores toosomething tooyour adecuado. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

Después de varios minutos, comando hello completa y muestra información acerca de la implementación.

## <a name="install-kubectl"></a>Instalación de kubectl

tooconnect toohello Kubernetes de clúster desde el equipo cliente, use [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), cliente de línea de comandos de Kubernetes Hola. 

Si usa Azure CloudShell, `kubectl` ya está instalado. Si desea que tooinstall localmente, puede usar hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

Hola después de la instalación de CLI de Azure en el ejemplo se `kubectl` tooyour sistema. En Windows, ejecute este comando como administrador.

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>Conexión con kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes clúster, ejecute hello [az kubernetes get-credenciales de acs](/cli/azure/acs/kubernetes#get-credentials) comando. Hello en el ejemplo siguiente se descarga configuración de clúster de hello para el clúster de Kubernetes.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

clúster de tooyour de tooverify Hola conexión desde el equipo, ejecute:

```azurecli-interactive
kubectl get nodes
```

`kubectl`Enumera los nodos de patrón y el agente de Hola.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Implementación de un contenedor de Windows IIS

Puede ejecutar un contenedor de Docker dentro de un *pod* de Kubernetes que contiene uno o varios contenedores. 

Este ejemplo básico se usa un toospecify de archivo JSON un contenedor de servicios de Microsoft Internet Information Server (IIS) y, a continuación, crea pod hello mediante hello `kubctl apply` comando. 

Cree un archivo local denominado `iis.json` y Hola copia siguiendo el texto. Este archivo indica Kubernetes toorun IIS en Windows Server 2016 Nano Server, con una imagen de contenedor público de [Docker Hub](https://hub.docker.com/r/nanoserver/iis/). contenedor de Hello usa el puerto 80, pero inicialmente solo es accesible dentro de la red de clústeres de Hola.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

pod de hello toostart, tipo:
  
```azurecli-interactive
kubectl apply -f iis.json
```  

implementación de hello tootrack, tipo:
  
```azurecli-interactive
kubectl get pods
```

Mientras se está implementando pod hello, estado de hello es `ContainerCreating`. Puede tardar unos minutos para hello de hello contenedor tooenter `Running` estado.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>Hola de vista Página de bienvenida de IIS

tooexpose hello world de toohello de pod con una dirección IP pública, Hola de tipo siguiente comando:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

Con este comando, Kubernetes crea un servicio y un [regla del equilibrador de carga de Azure](container-service-kubernetes-load-balancing.md) con una dirección IP pública para el servicio de Hola. 

Ejecute hello siguiendo el estado del comando toosee Hola del servicio de Hola.

```azurecli-interactive
kubectl get svc
```

Dirección IP de hello aparece inicialmente como `pending`. Después de unos minutos, Hola dirección IP externa de hello `iis` pod está establecido:
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

Puede usar un explorador web de la página de bienvenida de IIS de elección toosee Hola predeterminado en la dirección IP externa de hello:

![Imagen de la exploración tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>Eliminación de clúster
Cuando ya no se necesita el clúster hello, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, servicio de contenedor y todos ellos relacionados con recursos.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Pasos siguientes

En esta guía de inicio rápido, ha implementado un clúster de Kubernetes, conectado con `kubectl` y un pod con un contenedor IIS. toolearn más información sobre el servicio de contenedor de Azure, continuar toohello Kubernetes tutorial.

> [!div class="nextstepaction"]
> [Administración de un clúster de ACS Kubernetes](container-service-tutorial-kubernetes-prepare-app.md)
