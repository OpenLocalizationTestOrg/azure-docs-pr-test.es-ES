---
title: "aaaQuickstart - clúster de Azure Docker CE para Linux | Documentos de Microsoft"
description: "Aprender rápidamente toocreate un clúster de Docker CE para contenedores de Linux en el servicio de contenedor de Azure con hello CLI de Azure."
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a>Implementación del clúster de Docker CE

En esta guía de inicio rápido, un clúster de CE de Docker se implementa mediante Hola CLI de Azure. Una aplicación de contenedor múltiples que consta de front-end web y una instancia de Redis es, a continuación, implementar y ejecutar en el clúster de Hola. Una vez completado, la aplicación hello es accesible a través de internet de Hola.

Docker CE en Azure Container Service se encuentra en versión preliminar y **no se debe usar con cargas de trabajo de producción**.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un grupo lógico en el que se implementan y se administran los recursos de Azure.

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *ukwest* ubicación.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
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

Crear un clúster de CE de Docker en el servicio de contenedor de Azure con hello [az acs crear](/cli/azure/acs#create) comando. 

Hello en el ejemplo siguiente se crea un clúster denominado *mySwarmCluster* con un Linux maestro de nodo y tres nodos de agente de Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

Tras varios minutos, comando hello completa y devuelve información de formato json sobre clúster Hola.

## <a name="connect-toohello-cluster"></a>Conectar el clúster toohello

En esta guía de inicio rápido, deberá Hola FQDN del maestro de hello Docker Swarm y grupo de agente de Docker de Hola. Ejecute hello siguiente comando tooreturn ambos Hola FQDN maestra y el agente.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Salida:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Crear un SSH conjunto maestro de túnel toohello. Reemplace `MasterFQDN` con la dirección FQDN de hello del maestro de conjunto de Hola.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Conjunto hello `DOCKER_HOST` variable de entorno. Esto le permite comandos de docker de toorun contra Hola Docker Swarm sin necesidad de toospecify Hola nombre de host de Hola.

```bash
export DOCKER_HOST=localhost:2374
```

Ya estás listo toorun servicios de Docker en hello Docker Swarm.


## <a name="run-hello-application"></a>Ejecutar la aplicación hello

Cree un archivo denominado `azure-vote.yaml` y Hola copia siguen contenido en él.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Ejecute hello [implementar pila docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) comando servicio de toocreate Hola voto de Azure.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Salida:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Hola de uso [docker ps de pila](https://docs.docker.com/engine/reference/commandline/stack_ps/) comando estado de implementación de hello tooreturn de aplicación hello.

```bash
docker stack ps azure-vote
```

Una vez Hola `CURRENT STATE` de cada servicio es `Running`, aplicación hello está listo.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Probar la aplicación hello

Examinar toohello FQDN del grupo de agente de hello conjunto tootest out Hola aplicación voto de Azure.

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