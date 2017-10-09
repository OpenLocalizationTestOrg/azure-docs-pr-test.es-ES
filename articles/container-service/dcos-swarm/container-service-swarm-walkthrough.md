---
title: "aaaQuickstart - Azure Docker Swarm clúster para Linux | Documentos de Microsoft"
description: "Aprender rápidamente un clúster para los contenedores de Linux en el servicio de contenedor de Azure con hello CLI de Azure Docker Swarm toocreate."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a>Implementación del clúster de Docker Swarm

En esta guía de inicio rápido, un clúster de Docker Swarm se implementa mediante Hola CLI de Azure. Una aplicación de contenedor múltiples que consta de front-end web y una instancia de Redis es, a continuación, implementar y ejecutar en el clúster de Hola. Una vez completado, la aplicación hello es accesible a través de internet de Hola.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

Este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un grupo lógico en el que se implementan y se administran los recursos de Azure.

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *oesteee. UU.* ubicación.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Salida:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Creación de un clúster de Docker Swarm

Crear un clúster de Docker Swarm en el servicio de contenedor de Azure con hello [az acs crear](/cli/azure/acs#create) comando. 

Hello en el ejemplo siguiente se crea un clúster denominado *mySwarmCluster* con un Linux maestro de nodo y tres nodos de agente de Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

Tras varios minutos, comando hello completa y devuelve información de formato json sobre clúster Hola.

## <a name="connect-toohello-cluster"></a>Conectar el clúster toohello

En esta guía de inicio rápido, necesitará la dirección IP de Hola de maestro de hello Docker Swarm y del grupo de agente de Docker de Hola. Siguiente ejecución Hola comando tooreturn ambas direcciones IP.


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

Salida:

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

Crear un SSH conjunto maestro de túnel toohello. Reemplace `IPAddress` con la dirección IP de hello del maestro de conjunto de Hola.

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

Conjunto hello `DOCKER_HOST` variable de entorno. Esto le permite comandos de docker de toorun contra Hola Docker Swarm sin necesidad de toospecify Hola nombre de host de Hola.

```bash
export DOCKER_HOST=:2375
```

Ya estás listo toorun servicios de Docker en hello Docker Swarm.


## <a name="run-hello-application"></a>Ejecutar la aplicación hello

Cree un archivo denominado `docker-compose.yaml` y Hola copia siguen contenido en él.

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Ejecute hello después de comando toocreate hello Azure voto servicio.

```bash
docker-compose up -d
```

Salida:

```bash
Creating network "user_default" with hello default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-hello-application"></a>Probar la aplicación hello

Examinar la dirección IP de toohello de hello conjunto agente grupo tootest aplicación de Azure voto Hola.

![Imagen de la exploración tooAzure voto](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Eliminación de clúster
Cuando ya no se necesita el clúster hello, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, servicio de contenedor y todos ellos relacionados con recursos.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Obtener el código de hello

En esta guía de inicio rápido, imágenes del contenedor creada previamente han sido toocreate usa un servicio de Docker. Hola relacionadas con código de aplicación, Dockerfile, y crear archivos están disponibles en GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Pasos siguientes

En esta guía de inicio rápido, implementar un clúster de Docker Swarm e implementa una aplicación de contenedor de varios tooit.

toolearn sobre la integración de Docker activa con Visual Studio Team Services, continuar toohello CI/CD con Docker Swarm y VSTS.

> [!div class="nextstepaction"]
> [Integración y entrega continuas con Docker Swarm y VSTS](./container-service-docker-swarm-setup-ci-cd.md)