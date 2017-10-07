---
title: "aaaManage Swarm de Azure de clúster con la API de Docker | Documentos de Microsoft"
description: "Implementar contenedores tooa Docker Swarm clúster en el servicio de contenedor de Azure"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a>Administración de contenedores con Docker Swarm
Docker Swarm proporciona un entorno para implementar cargas de trabajo en contenedores a través de un conjunto agrupado de hosts de Docker. Conjunto de docker utiliza API de Docker nativa de Hola. flujo de trabajo de Hello para la administración de contenedores en un Docker Swarm es casi idéntico toowhat sería en un host de contenedor único. Este documento proporciona ejemplos sencillos de la implementación de cargas de trabajo en contenedores en una instancia de Azure Container Service (servicio Contenedor de Azure) de Docker Swarm. Para obtener documentación más detallada sobre Docker Swarm, consulte [Docker Swarm en Docker.com](https://docs.docker.com/swarm/).

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Ejercicios de toohello de requisitos previos en este documento:

[Crear un clúster de Swarm en Azure Container Service (servicio Contenedor de Azure)](container-service-deployment.md)

[Conectar con el clúster de conjunto de hello en el servicio de contenedor de Azure](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>Implementación de un contenedor nuevo
toocreate un nuevo contenedor de hello Docker Swarm, usar hello `docker run` comando (asegúrese de que ha abierto un maestros de toohello de túnel SSH según los requisitos previos de hello anteriores). Este ejemplo crea un contenedor de hello `yeasy/simple-web` imagen:

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

Una vez creado el contenedor de hello, use `docker ps` tooreturn información sobre el contenedor de Hola. Aquí, tenga en cuenta que el agente Hola conjunto que se hospeda el contenedor de Hola aparece:

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

Ahora puede acceder a aplicación Hola que se está ejecutando en este contenedor a través del nombre DNS público de Hola Hola conjunto agente del equilibrador de carga. Puede encontrar esta información en hello portal de Azure:  

![Resultados de la visita real](./media/container-service-docker-swarm/real-visit.jpg)  

De forma predeterminada Hola equilibrador de carga tiene los puertos 80, 443 y 8080 abierto. Si desea que tooconnect en otro puerto necesitará tooopen ese puerto en hello equilibrador de carga de Azure para hello grupo de agente.

## <a name="deploy-multiple-containers"></a>Implementación de varios contenedores
Cuando se inician varios contenedores, mediante la ejecución de 'run de docker' varias veces, puede usar hello `docker ps` toosee de comando que hospeda contenedores Hola se ejecutan en. En el ejemplo de Hola siguiente, tres contenedores están repartidos por igual entre tres agentes de conjunto hello:  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>Implementación de contenedores mediante Docker Compose
Puede usar la implementación de hello tooautomate Docker Compose y la configuración de varios contenedores. toodo por lo tanto, asegúrese de que se ha creado un túnel de Shell seguro (SSH) y se ha establecido esa variable DOCKER_HOST Hola (vea Hola cumplen los requisitos previos anteriores).

Cree un archivo docker-compose.yml en el sistema local. toodo, utilícelo [ejemplo](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

Ejecutar `docker-compose up -d` las implementaciones de contenedor de Hola toostart:

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

Por último, se devolverá la lista de Hola de contenedores en ejecución. Esta lista figuran los contenedores de Hola que se implementaron mediante Docker Compose:

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

Naturalmente, puede usar `docker-compose ps` tooexamine sólo Hola contenedores definidos en su `compose.yml` archivo.

## <a name="next-steps"></a>Pasos siguientes
[Más información acerca de Docker Swarm.](https://docs.docker.com/swarm/)

