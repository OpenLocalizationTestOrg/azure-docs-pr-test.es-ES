---
title: "Aplicación Web en Linux con CLI de Azure 2.0 aaaManage | Documentos de Microsoft"
description: "Administre Aplicación web en Linux mediante la CLI de Azure."
keywords: azure app service, web app, cli, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Administración de Aplicación web en Linux mediante la CLI de Azure

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Mediante comandos de hello en este artículo son capaz de toocreate y administrar una aplicación Web en Linux con CLI de Azure 2.0.
Puede comenzar a usar la nueva versión de hello de hello CLI de dos maneras:

* [Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) en su equipo.
* Uso de [Azure Cloud Shell (versión preliminar)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>Creación de un plan de App Service de Linux

toocreate un Plan de servicio de aplicaciones de Linux, puede usar Hola siguiente comando:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Creación de una aplicación web del contenedor de Docker personalizada

toocreate una aplicación web y configurarlo toorun contenedor Docker personalizado, puede usar Hola siguiente comando:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>Activar el registro de contenedor de Docker de Hola

tooactivate Hola registro de contenedor de Docker, puede utilizar Hola siguiente comando:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Contenedor Docker cambio Hola personalizadas para una aplicación Web existente en Linux App

toochange una aplicación creada anteriormente, de hello actual Docker imagen tooa nueva imagen, puede usar Hola siguiente comando:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Uso de imágenes de Docker de un Registro privado

Puede configurar imágenes de toouse su aplicación desde un registro privada. Necesitará tooprovide Hola url para el registro, el nombre de usuario y la contraseña. Esto puede lograrse mediante Hola siguiente comando:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Habilitación de implementaciones continuas para imágenes de Docker personalizadas

Con el siguiente comando de Hola puede habilitar la funcionalidad del CD de Hola y obtener la dirección url del webhook Hola. Esta dirección url puede ser usado tooconfigure se DockerHub o del registro de contenedor de Azure repositorios.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Creación de una aplicación web en Linux mediante uno de nuestros marcos en tiempo de ejecución integrados

toocreate una aplicación PHP 5.6 en App Linux que, se puede usar el siguiente comando de Hola.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Cambio de la versión de .NET Framework por una aplicación web en Linux existente

toochange una aplicación creada anteriormente, de hello actual framework versión tooNode.js 6.11, puede usar Hola siguiente comando:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Configuración de implementaciones Git para su aplicación web

tooset una de las implementaciones de Git para la aplicación, puede usar Hola siguiente comando:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Pasos siguientes
* [¿Qué es Web App on Linux de Azure?](app-service-linux-intro.md)
* [Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell (versión preliminar)](../cloud-shell/overview.md)
* [Configuración de entornos de ensayo en Azure App Service](./web-sites-staged-publishing.md)
* [Implementación continua con Azure Web App en Linux](./app-service-linux-ci-cd.md)
