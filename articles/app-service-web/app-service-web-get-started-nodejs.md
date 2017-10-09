---
title: "aaaCreate una aplicación web de Node.js en Azure | Documentos de Microsoft"
description: "Implementación de su primera aplicación Hola mundo de Node.js en Azure App Service Web Apps en cuestión de minutos."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a>Creación de una aplicación web de Node.js en Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.  Este tutorial rápido muestra cómo toodeploy una tooAzure de aplicación Node.js aplicaciones Web. Crear una aplicación de web de hello usando hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), y usar Git toodeploy ejemplo Node.js código toohello web app.

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux. Una vez instalados los requisitos previos de hello, tarda aproximadamente cinco minutos toocomplete pasos Hola.   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial rápido:

* [Instalación de Git](https://git-scm.com/)
* [Instalación de Node.js y NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Descargar el ejemplo hello

En una ventana de terminal, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

Utilice esta ventana de terminal toorun todos los comandos de hello en este tutorial rápido.

Cambie el directorio toohello que contiene código de ejemplo de Hola.

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Ejecutar la aplicación hello localmente

Ejecutar la aplicación hello localmente o abriendo una ventana de terminal y utilizando hello `npm start` hello toolaunch de secuencia de comandos integrada en el servidor HTTP de Node.js.

```bash
npm start
```

Abra un explorador web y navegar por la aplicación de ejemplo de toohello en http://localhost:1337.

Vea hello **Hello World** mensaje desde la aplicación de ejemplo de Hola mostrado en la página de Hola.

![Aplicación de ejemplo que se ejecuta localmente](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

En la ventana de terminal, presione **Ctrl + C** servidor web de tooexit Hola.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de la aplicación web vacía](media/app-service-web-get-started-php/app-service-web-service-created.png)

Ha creado una nueva aplicación web vacía en Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Examinar toohello aplicación

Examinar toohello implementa la aplicación mediante el explorador web.

```bash
http://<app_name>.azurewebsites.net
```

Hola Node.js código de ejemplo se ejecuta en una aplicación web de servicio de aplicaciones de Azure.

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

**¡Enhorabuena!** Ha implementado la primera tooApp de aplicación Node.js servicio.

## <a name="update-and-redeploy-hello-code"></a>Actualizar y volver a implementar código de hello

Con un editor de texto, abra hello `index.js` de archivos de aplicación de Node.js hello y realizar un pequeño cambio de texto toohello en llamada de hello demasiado`response.end`:

```nodejs
response.end("Hello Azure!");
```

Confirmar los cambios de Git y, a continuación, insertar tooAzure de cambios de código de hello.

```bash
git commit -am "updated output"
git push azure master
```

Una vez completada la implementación, cambie toohello atrás ventana del explorador que abrió en hello **examinar toohello aplicación** paso a paso y actualice la vista.

![Aplicación de ejemplo actualizada que se ejecuta en Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Administración de la nueva aplicación web de Azure

Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web aplicación que creó.

Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

Podrá ver la página de información general de la aplicación web. En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar. 

![Hoja de App Service en Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Node.js con MongoDB](app-service-web-tutorial-nodejs-mongodb-app.md)
