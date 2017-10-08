---
title: "aaaCreate un PHP web aplicación en Azure | Documentos de Microsoft"
description: "Implementación de su primera aplicación Hola mundo de PHP en Azure App Service Web Apps en cuestión de minutos."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a>Creación de una aplicación web de PHP en Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.  Este tutorial de inicio rápido se muestra cómo toodeploy una tooAzure de aplicación PHP aplicaciones Web. Crear una aplicación de web de hello usando hello [CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) en el Shell de nube y usar Git toodeploy ejemplo PHP código toohello web app.

![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)

Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux. Una vez instalados los requisitos previos de hello, tarda aproximadamente cinco minutos toocomplete pasos Hola.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial rápido:

* [Instalación de Git](https://git-scm.com/)
* [Instalación de PHP](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Descargar el ejemplo hello localmente

En una ventana de terminal, ejecute hello siga los comandos. Esto clonar la máquina local de tooyour de aplicación de ejemplo de Hola y navegar por el código de ejemplo de toohello directory contenedor Hola.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Ejecutar la aplicación hello localmente

Ejecutar la aplicación hello localmente o abriendo una ventana de terminal y utilizando hello `php` comando toolaunch Hola PHP servidor web integrado de.

```bash
php -S localhost:8080
```

Abra un explorador web y navegar por la aplicación de ejemplo de toohello en http://localhost: 8080.

Vea hello **Hola a todos!** mensaje de la aplicación de ejemplo de Hola mostrado en la página de Hola.

![Aplicación de ejemplo que se ejecuta localmente](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

En la ventana de terminal, presione **Ctrl + C** servidor web de tooexit Hola.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Página de la aplicación web vacía](media/app-service-web-get-started-php/app-service-web-service-created.png)

Ha creado una nueva aplicación web vacía en Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a>Examinar toohello aplicación localmente

Examinar toohello implementa la aplicación mediante el explorador web.

```bash
http://<app_name>.azurewebsites.net
```

Hola código de ejemplo PHP se está ejecutando en una aplicación web de servicio de aplicaciones de Azure.

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

**¡Enhorabuena!** Ha implementado la primera tooApp de aplicación PHP servicio.

## <a name="update-locally-and-redeploy-hello-code"></a>Actualizar de forma local e implementar código de hello

Use un editor de texto local, abrir hello `index.php` archivo dentro de la aplicación PHP de hello y aplique un pequeño cambio toohello al texto en cadena Hola junto demasiado`echo`:

```php
echo "Hello Azure!";
```

Confirmar los cambios de Git y, a continuación, insertar tooAzure de cambios de código de hello.

```bash
git commit -am "updated output"
git push azure master
```

Una vez completada la implementación, cambie toohello atrás ventana del explorador que abrió en hello **examinar toohello aplicación** paso y página de actualización de Hola.

![Aplicación de ejemplo actualizada que se ejecuta en Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Administración de la nueva aplicación web de Azure

Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web aplicación que creó.

Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

Podrá ver la página de información general de la aplicación web. En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.

![Hoja de App Service en Azure Portal](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [PHP con MySQL](app-service-web-tutorial-php-mysql.md)
