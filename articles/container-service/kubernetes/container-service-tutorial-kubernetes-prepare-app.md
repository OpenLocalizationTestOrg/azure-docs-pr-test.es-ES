---
title: "tutorial de servicio de contenedor aaaAzure: preparar la aplicación | Documentos de Microsoft"
description: "Tutorial de Azure Container Service: preparación de una aplicación"
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
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>Crear contenedor imágenes toobe utilizado con el servicio de contenedor de Azure

En este tutorial, la primera parte de siete, se prepara una aplicación con varios contenedores para usarla en Kubernetes. Los pasos completados incluyen:  

> [!div class="checklist"]
> * La clonación de origen de la aplicación desde GitHub  
> * Crear una imagen de contenedor de origen de la aplicación hello
> * Probar la aplicación hello en un entorno local de Docker

Una vez completada, es accesible en el entorno de desarrollo local Hola tras la aplicación.

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

En los tutoriales posteriores, imagen de contenedor de hello es tooan cargado del registro de contenedor de Azure y, a continuación, ejecutarse en un Azure hospeda Kubernetes clúster.

## <a name="before-you-begin"></a>Antes de empezar

En este tutorial se supone que el usuario tiene un conocimiento básico de los principales conceptos de Docker, como los contenedores, las imágenes de contenedor y los comandos básicos de Docker. Si es necesario, consulte la [introducción a Docker]( https://docs.docker.com/get-started/), donde encontrará datos básicos acerca de los contenedores. 

toocomplete este tutorial, necesitará un entorno de desarrollo de Docker. Docker proporciona paquetes que permiten configurar Docker fácilmente en cualquier sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) o [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Obtención del código de la aplicación

aplicación de ejemplo de Hola usado en este tutorial es una aplicación básica de votación. aplicación Hello consta de un componente de front-end web y una instancia de Redis back-end. componente de Hello web se empaqueta en una imagen de contenedor personalizadas. instancia de Redis Hello usa una imagen sin modificar de Docker Hub.  

Usar git toodownload una copia del entorno de desarrollo de hello aplicación tooyour.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Interior Hola clonado directorio es código de fuente de la aplicación hello, una Docker creada previamente crear archivo y un archivo de manifiesto de Kubernetes. Estos archivos son activos toocreate usado en todo el conjunto de tutorial de Hola. 

## <a name="create-container-images"></a>Creación de imágenes de contenedor

[Redacción de docker](https://docs.docker.com/compose/) puede ser usar tooautomate Hola compilación fuera de las imágenes del contenedor y la implementación de Hola de aplicaciones de contenedor de varios.

Ejecutar la imagen de contenedor de hello docker compose.yml archivo toocreate hello, descarga Hola Redis imagen e iniciar aplicación hello.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

Cuando haya completado, usar hello [imágenes de docker](https://docs.docker.com/engine/reference/commandline/images/) comando toosee imágenes de hello creado.

```bash
docker images
```

Tenga en cuenta que se han descargado o creado tres imágenes. Hola *azure front-voto* imagen contiene aplicación hello. Se derivó de hello *nginx matraz* imagen. imagen de Redis Hola se descargó de Docker Hub.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Ejecute hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) comando toosee hello contenedores en ejecución.

```bash
docker ps
```

Salida:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>Prueba local de la aplicación

Examinar toohttp://localhost:8080 toosee Hola ejecutando la aplicación.

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Limpieza de recursos

Ahora que se ha validado la funcionalidad de la aplicación, Hola contenedores en ejecución posible detener y quitar. No elimine las imágenes del contenedor Hola. Hola *azure front-voto* imagen es la instancia de registro de contenedor de Azure de tooan cargados en el tutorial siguiente Hola.

Ejecute hello después hello toostop contenedores en ejecución.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

Elimine los contenedores de hello detenido con hello siguiente comando.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

Cuando ha finalizado, tendrá una imagen de contenedor que contiene la aplicación de Azure voto Hola.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se probó una aplicación y crearon imágenes del contenedor para la aplicación hello. se completaron Hola pasos:

> [!div class="checklist"]
> * Origen de clonación de aplicación Hola desde GitHub  
> * La creación de una imagen de contenedor desde el origen de la aplicación
> * Aplicación de hello probada en un entorno local de Docker

Avanzar toohello toolearn de tutorial siguiente sobre el almacenamiento de imágenes del contenedor en un registro de contenedor de Azure.

> [!div class="nextstepaction"]
> [Insertar imágenes tooAzure del registro de contenedor](./container-service-tutorial-kubernetes-prepare-acr.md)
