---
title: "tutorial de instancias de contenedor - aaaAzure Prepare su aplicación | Documentos de Azure"
description: "Preparar una aplicación para la implementación tooAzure instancias de contenedor"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a>Crear contenedor de implementación tooAzure instancias de contenedor

Azure Container Instances permite la implementación de contenedores de Docker en la infraestructura de Azure sin necesidad de aprovisionar ninguna máquina virtual o adoptar algún servicio de nivel superior. En este tutorial, compilará una aplicación web simple en Node.js y la empaquetará en un contenedor que se pueden ejecutar mediante Azure Container Instances. Se tratarán los siguientes temas:

> [!div class="checklist"]
> * La clonación de origen de la aplicación desde GitHub  
> * La creación de imágenes de contenedor desde el origen de la aplicación
> * Pruebe imágenes de hello en un entorno local de Docker

En los tutoriales posteriores, se cargue su tooan de imagen del registro de contenedor de Azure y, a continuación, implementarlos tooAzure instancias de contenedor.

## <a name="before-you-begin"></a>Antes de empezar

En este tutorial se supone que el usuario tiene un conocimiento básico de los principales conceptos de Docker, como los contenedores, las imágenes de contenedor y los comandos básicos de Docker. Si es necesario, consulte la [introducción a Docker]( https://docs.docker.com/get-started/), donde encontrará datos básicos acerca de los contenedores. 

toocomplete este tutorial, necesitará un entorno de desarrollo de Docker. Docker proporciona paquetes que permiten configurar Docker fácilmente en cualquier sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) o [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Obtención del código de la aplicación

ejemplo de Hola en este tutorial incluye una aplicación web simple generada [Node.js](http://nodejs.org). aplicación Hello sirve una página HTML estática y el siguiente aspecto:

![Aplicación del tutorial tal como se muestra en un explorador][aci-tutorial-app]

Ejemplo de Hola a Use git toodownload:

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Crear imagen de contenedor de Hola

Hola Dockerfile proporcionado en el repositorio de ejemplo de Hola muestra cómo se crea el contenedor de Hola. Se inicia desde un [imagen oficial de Node.js] [ dockerhub-nodeimage] basado en [Linux Alpine](https://alpinelinux.org/), una distribución pequeña que es idóneo toouse con contenedores. A continuación, copia los archivos de la aplicación hello en el contenedor de hello, instala las dependencias mediante Administrador de paquetes de nodo de Hola y finalmente inicia la aplicación hello.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Hola de uso `docker build` comando toocreate Hola imagen del contenedor, etiquetado como *aplicación de tutorial de aci*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

Hola de uso `docker images` toosee imagen de hello integrada:

```bash
docker images
```

Salida:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Ejecutar el contenedor de hello localmente

Antes de intentar implementar Hola contenedor tooAzure instancias de contenedor, ejecutarla localmente tooconfirm que funciona. Hola `-d` conmutador permite la ejecución en segundo plano de hello, de contenedor de hello mientras `-p` permite toomap un puerto arbitrario en su tooport cálculo 80 en el contenedor de Hola.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Hola abra Explorador toohttp://localhost:8080 tooconfirm que Hola contenedor se está ejecutando.

![Aplicación en ejecución Hola localmente en el Explorador de Hola][aci-tutorial-app-local]

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha creado una imagen de contenedor que puede ser implementado tooAzure instancias de contenedor. se completaron Hola pasos:

> [!div class="checklist"]
> * Origen de clonación de aplicación Hola desde GitHub  
> * La creación de imágenes de contenedor desde el origen de la aplicación
> * Contenedor de hello pruebas localmente

Avanzar toohello toolearn de tutorial siguiente sobre el almacenamiento de imágenes del contenedor en un registro de contenedor de Azure.

> [!div class="nextstepaction"]
> [Insertar imágenes tooAzure del registro de contenedor](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png