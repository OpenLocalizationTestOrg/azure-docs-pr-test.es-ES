---
title: "Implementación de aplicación Web de Azure en Linux aaaContinuous | Documentos de Microsoft"
description: "¿Cómo toosetup la implementación continua en la aplicación Web de Azure en Linux."
keywords: azure app service, linux, oss, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Implementación continua con Aplicación web de Azure en Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

En este tutorial, configurará una implementación continua para una imagen de contenedor personalizada desde los repositorios administrados de [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) o [Docker Hub](https://hub.docker.com).

## <a name="step-1---sign-in-tooazure"></a>Paso 1: tooAzure de inicio de sesión

Inicie sesión en toohello portal de Azure en http://portal.azure.com

## <a name="step-2---enable-container-continuous-deployment-feature"></a>Paso 2: Habilitación de la característica de implementación continua del contenedor

Puede habilitar la característica de implementación continua de hello mediante [CLI de Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) y ejecutando el siguiente comando de Hola

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

Hola  **[portal de Azure](https://portal.azure.com/)**, haga clic en hello **servicio de aplicaciones** opción izquierda Hola de página Hola.

Haga clic en el nombre de saludo de la aplicación que desee tooconfigure Docker Hub una implementación continua para.

Hola **configuración de la aplicación**, agregar una aplicación llamada `DOCKER_ENABLE_CI` con el valor de hello `true`.

![insert image of app setting](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>Paso 3: Preparación de la dirección URL de webhook

Puede obtener utilizando de hello URL del Webhook [CLI de Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) y ejecutando el siguiente comando de Hola

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Para hello URL del Webhook, necesita hello toohave después de punto de conexión: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

Puede obtener la `publishingusername` y `publishingpwd` mediante la descarga de aplicación web de hello publicar perfil mediante Hola portal de Azure.

![insert image of adding webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>Paso 4: Incorporación de webhook

### <a name="azure-container-registry"></a>Azure Container Registry

En la hoja del portal de registro, haga clic en **Webhooks** y cree un nuevo webhook haciendo clic en **Agregar**. Hola **crear webhook** hoja, asigne un nombre a su webhook. Para hello Webhook URI, necesita tooprovide Hola URL obtenido de **paso 3**

Asegúrese de que define el ámbito de hello como Hola repositorio que contiene la imagen de contenedor.

![insertar imagen de webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Cuando se actualiza la imagen de hello, aplicación web de hello se actualizan automáticamente con la nueva imagen de Hola.

### <a name="docker-hub"></a>Docker Hub

En la página de Docker Hub, haga clic en **Webhooks** y, luego, en **CREAR NUEVO WEBHOOK**.

![insert image of adding webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Para la dirección URL del Webhook hello, necesita tooprovide Hola URL obtenido de **paso 3**

![insert image of adding webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Cuando se actualiza la imagen de hello, aplicación web de hello se actualizan automáticamente con la nueva imagen de Hola.

## <a name="next-steps"></a>Pasos siguientes
* [¿Qué es Web App on Linux de Azure?](./app-service-linux-intro.md)
* [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/)
* [Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure](app-service-linux-using-nodejs-pm2.md)
* [Uso de .NET Core en Web App on Linux de Azure](app-service-linux-using-dotnetcore.md)
* [Uso de Ruby en Web App on Linux de Azure](app-service-linux-ruby-get-started.md)
* [Cómo la imagen toouse una Docker personalizada para la aplicación Web de Azure en Linux](./app-service-linux-using-custom-docker-image.md)
* [Preguntas más frecuentes sobre Web App on Linux de Azure App Service](./app-service-linux-faq.md) 
* [Administración de Aplicación web en Linux mediante la CLI de Azure 2.0](./app-service-linux-cli.md)



