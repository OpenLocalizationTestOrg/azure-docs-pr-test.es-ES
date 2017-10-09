---
title: "aaaQuickstart - clúster Kubernetes de Azure para Linux | Documentos de Microsoft"
description: "Aprender rápidamente toocreate un clúster Kubernetes para contenedores de Linux en el servicio de contenedor de Azure con hello CLI de Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a>Implementación de un clúster de Kubernetes para los contenedores de Linux

En esta guía de inicio rápido, un clúster de Kubernetes se implementa mediante Hola CLI de Azure. Una aplicación de contenedor múltiples que consta de front-end web y una instancia de Redis es, a continuación, implementar y ejecutar en el clúster de Hola. Una vez completado, la aplicación hello es accesible a través de internet de Hola. 

aplicación de ejemplo de Hola usado en este documento está escrita en Python. conceptos de Hola y pasos que se detallan a continuación pueden ser utilizado toodeploy cualquier contenedor de la imagen en un clúster de Kubernetes. Hello código, Dockerfile y el proyecto de toothis relacionados de archivos de manifiesto de Kubernetes creada previamente están disponibles en [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).

![Imagen de la exploración tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)

Este inicio rápido asume un conocimiento básico de conceptos de Kubernetes, para obtener información detallada en Kubernetes vea hello [Kubernetes documentación]( https://kubernetes.io/docs/home/).

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un grupo lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westeurope* ubicación.

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

Salida:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a>Creación de un clúster de Kubernetes

Crear un clúster de Kubernetes en el servicio de contenedor de Azure con hello [az acs crear](/cli/azure/acs#create) comando. Hello en el ejemplo siguiente se crea un clúster denominado *myK8sCluster* con un Linux maestro de nodo y tres nodos de agente de Linux.

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

Tras varios minutos, comando hello completa y devuelve información de formato json sobre clúster Hola. 

## <a name="connect-toohello-cluster"></a>Conectar el clúster toohello

usar un clúster de Kubernetes toomanage [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), cliente de línea de comandos de Kubernetes Hola. 

Si usa Azure CloudShell, kubectl ya está instalado. Si desea que tooinstall localmente, puede usar hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

tooconfigure kubectl tooconnect tooyour Kubernetes clúster, ejecute hello [az kubernetes get-credenciales de acs](/cli/azure/acs/kubernetes#get-credentials) comando. Este paso descarga las credenciales y configura hello Kubernetes CLI toouse ellos.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

clúster de tooyour conexión tooverify hello, use hello [kubectl obtener](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando tooreturn una lista de nodos de clúster de Hola.

```azurecli-interactive
kubectl get nodes
```

Salida:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a>Ejecutar la aplicación hello

Un archivo de manifiesto de Kubernetes define un estado deseado para el clúster de hello, incluidos lo que deben estar en ejecución imágenes del contenedor. En este ejemplo, un manifiesto es toocreate usado todos los objetos necesarios toorun Hola aplicación voto de Azure. 

Cree un archivo denominado `azure-vote.yml` y copie en él Hola siguientes YAML. Si está trabajando en Azure Cloud Shell, este archivo se puede crear mediante vi o Nano, como si trabajara en un sistema físico o virtual.

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

Hola de uso [kubectl crear](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) aplicación hello de toorun de comandos.

```azurecli-interactive
kubectl create -f azure-vote.yml
```

Salida:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a>Probar la aplicación hello

Cuando se ejecuta la aplicación hello, un [Kubernetes servicio](https://kubernetes.io/docs/concepts/services-networking/service/) se crea que expone Hola aplicación front-end toohello internet. Este proceso puede tardar unos toocomplete minutos. 

curso toomonitor, use hello [kubectl obtener servicio](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando con hello `--watch` argumento.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Hola inicialmente **IP externas** para hello *azure front-voto* servicio aparece como *pendiente*. Una vez que la dirección de hello externo IP ha cambiado desde *pendiente* tooan *dirección IP*, use `CTRL-C` proceso de inspección de toostop hello kubectl. 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

Ahora puede examinar Hola de toohello externo IP dirección toosee voto de aplicación de Azure.

![Imagen de la exploración tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a>Eliminación de clúster
Cuando ya no se necesita el clúster hello, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, servicio de contenedor y todos ellos relacionados con recursos.

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Obtener el código de hello

En esta guía de inicio rápido, imágenes del contenedor creada previamente han sido toocreate usa una implementación de Kubernetes. Hola relacionadas con código de aplicación, Dockerfile, y archivo de manifiesto de Kubernetes están disponibles en GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Pasos siguientes

En esta guía de inicio rápido, implementar un clúster de Kubernetes e implementa una aplicación de contenedor de varios tooit. 

toolearn más información sobre el servicio de contenedor de Azure y recorrido a través de un ejemplo de código completo toodeployment, continuar con tutorial de clúster de toohello Kubernetes.

> [!div class="nextstepaction"]
> [Administración de un clúster de ACS Kubernetes](./container-service-tutorial-kubernetes-prepare-app.md)
