---
title: "aplicación web de aaaCreate una HTML estático en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de la aplicación de ejemplo de toorun las aplicaciones web en el servicio de aplicación de Azure implementando una HTML estático."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a>Creación de una aplicación web HTML estática en Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.  Este tutorial rápido muestra cómo toodeploy básica HTML + CSS sitio tooAzure las aplicaciones Web. Crear una aplicación de web de hello usando hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), y usar Git toodeploy ejemplo HTML toohello contenido web app.

![Página principal de la aplicación de ejemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux. Una vez instalados los requisitos previos de hello, tarda aproximadamente cinco minutos toocomplete pasos Hola.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial rápido:

- [Instalación de Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Descargar el ejemplo hello

En una ventana de terminal, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

Utilice esta ventana de terminal toorun todos los comandos de hello en este tutorial rápido.

## <a name="view-hello-html"></a>Hola vista HTML

Navegue toohello directorio que contiene el ejemplo hello HTML. Abra hello *index.html* archivo en el explorador.

![Página de inicio de la aplicación de ejemplo](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de la aplicación web vacía](media/app-service-web-get-started-html/app-service-web-service-created.png)

Ha creado una nueva aplicación web vacía en Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Examinar toohello aplicación

En un explorador, vaya la URL de la aplicación web de Azure toohello:

```
http://<app_name>.azurewebsites.net
```

página de saludo se está ejecutando como una aplicación web de servicio de aplicaciones de Azure.

![Página de inicio de la aplicación de ejemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**¡Enhorabuena!** Ha implementado la primera tooApp de aplicación servicio HTML.

## <a name="update-and-redeploy-hello-app"></a>Actualizar y volver a implementar la aplicación hello

Abra hello *index.html* un archivo en un editor de texto y realizar un toohello cambian el formato. Por ejemplo, cambiar encabezado H1 Hola de "Azure aplicación servicio – ejemplo sitio HTML estático" toojust "servicio de aplicaciones de Azure'.

Confirmar los cambios de Git y, a continuación, insertar tooAzure de cambios de código de hello.

```bash
git commit -am "updated HTML"
git push azure master
```

Una vez completada la implementación, actualización de los cambios de hello toosee de explorador.

![Página de inicio de la aplicación de ejemplo actualizada](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>Administración de la nueva aplicación web de Azure

Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web aplicación que creó.

Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-html/portal1.png)

Podrá ver la página de información general de la aplicación web. En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar. 

![Hoja de App Service en Azure Portal](./media/app-service-web-get-started-html/portal2.png)

menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Asignación de un dominio personalizado](app-service-web-tutorial-custom-domain.md)
